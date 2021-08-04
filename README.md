# LINUX常用命令

### 开关机

```
shutdown -h now  // 立刻关机
shutdown -h 5    // 5分钟后关机

shutdown -r now  // 立刻重启
shutdown -r 5    // 5分钟后重启
```



### 系统信息

```
fdisk -l            // 查看磁盘及分区信息
df -h               // 查看硬盘使用情况  -h人性化显示 -T 显示硬盘类型
du -h 目录或文件名    // 查看目录或文件大小
top                 // 动态显示系统运行信息，相当于任务管理器
cat /proc/cpuinfo   // 查看cpu硬件信息
uptime              // 查看CPU使用情况（同top第一行）
free -h -s 10       // 查看内存使用情况，每10s刷新一次
```



### 进程

```
ps aux|grep 进程名     // 查看运行的进程
ps -ef|grep 进程名     // 查看运行的进程，包括父进程ID
nohup 命令 &           // 后台执行程序
kill -9 PID           // 终止进程  -9表示强制终止
killall 进程名         // 终止一组进程
```



### 服务

**管理服务运行状态**

​		systemctl start|stop|status|restart|reload 服务名

​		分别指启动|停止|查看状态|重启|重新加载 服务

**管理服务启动状态**

​		systemctl enable|disable|is-enabled 服务名

​		分别指开机自动启动|禁止自动启动|查看启动状态



### 网络

**查看IP**

ifconfig

**更改IP**

ifconfig -interface 地址

例：sudo ifconfig eth0 192.168.1.5 netmask 255.255.255.0

**查看路由**

route

**查看网络状态**

netstat -natu

* -a (all)显示所有选项，默认不显示LISTEN相关
* -t (tcp)仅显示tcp相关选项
* -u (udp)仅显示udp相关选项
* -n 拒绝显示别名，能显示数字的全部转化成数字。
* -l 仅列出有在 Listen (监听) 的服務状态
* -p 显示建立相关链接的程序名
* -r 显示路由信息，路由表
* -e 显示扩展信息，例如uid等
* -s 按各个协议进行统计
* -c 每隔一个固定时间，执行该netstat命令。



### 用户

```
w            // 当前登录用户信息
last         // 查看登录记录
```



### 挂载

```
mount 设备 挂载点目录         // 挂载
mount -o loop 镜像文件 目录  // 挂载ISO镜像
umount 设备或挂载点目录       // 卸载
df -hT                     // 查看已挂载的设备
```

**自动挂载 **

* blkid 设备   // 查看设备的UUID
* 修改/etc/fstab文件 增加新的设备挂载信息
* 运行 mount -a 使挂载生效



### 辅助命令

```
--help          // 如：shutdown --help
man 命令         // 帮助手册
clear           // 清屏
<Tab>键补全路径
!$ 调用上一条命令路径
```



### 文件、目录操作

```
cd /          // 切换到根目录
cd /usr       // 切换到根目录下的usr目录
cd ..         // 切换到上一级目录
cd ~          // 切换到home目录
cd -          // 切换到上次访问的目录

ls                // 查看当前目录下的所有目录和文件
ls -a             // 查看当前目录下的所有目录和文件（包括隐藏的文件）
ls -l 或 ll       // 列表查看当前目录下的所有目录和文件（列表查看，显示更多信息）
ls /dir           // 查看指定目录下的所有目录和文件   如：ls /usr

mkdir aaa         // 在当前目录下创建一个名为aaa的目录
mkdir /usr/aaa    // 在指定目录下创建一个名为aaa的目录

rm 文件           // 删除当前目录下的文件
rm -f 文件        // 删除当前目录的的文件（不询问）
rm -r aaa        // 递归删除当前目录下的aaa目录
rm -rf aaa       // 递归删除当前目录下的aaa目录（不询问）
rm -rf *         // 将当前目录下的所有目录和文件全部删除

mv 当前文件或目录名 新名称   // 重命名 如：mv aaa bbb    将目录aaa改为bbb
mv 文件或目录名 新路径   // 将/usr/tmp目录下的aaa目录剪切到/usr目录下面  mv /usr/tmp/aaa /usr

cp -r 文件或目录名 目标位置  // 复制到新路径 如果是目录-r代表递归

find 目录 参数 名称    // 例：find /usr -name 'a*' 查找/usr目录下的所有以a开头的目录或文件

chmod -R 777 文件名   // -R表示目录下所有文件夹和文件。3个数字依次代表文件所有者、所属组、其他用户的权限，r、w、x分别表示为数字4、2、1，一个权限组合需将数字累加。


```



### 文件查看

```
more 文件名       // 分页查看文件，空格下一页，<Q>键退出
less 文件名       // 分页查看文件，可上下翻页，<Q>键退出
head -n 文件名    // 显示前n行内容，默认10行
tail -nf 文件名   // 显示末尾n行内容，默认10行，f-实时更新内容
wc 文件名         // 统计文件 （-l 行数，-w 单词数 -c 字节数）
stat 文件名       // 查看文件元数据
```



### vim编辑

```
1) 命令行模式command mode）    控制屏幕光标的移动，字符、字或行的删除，查找，移动复制某区段。    命令行模式下的常用命令：    【1】控制光标移动：↑，↓，j    【2】删除当前行：dd     【3】查找：/字符    【4】进入编辑模式：i o a    【5】进入底行模式：:    【6】取消编辑： u ，取消所有编辑： U         2) 编辑模式（Insert mode）    只有在Insert mode下，才可以做文字输入，按「ESC」键可回到命令行模式。    编辑模式下常用命令：    【1】ESC 退出编辑模式到命令行模式；      3) 底行模式（last line mode）    将文件保存或退出vi，也可以设置编辑环境，如寻找字符串、列出行号……等。    底行模式下常用命令：    【1】退出编辑：   :q    【2】强制退出：   :q!    【3】保存并退出：  :wq
```



### 压缩解压

**压缩命令**

​		tar -zcf 打包后的文件名 源文件或目录

* -c 创建“ .tar ”包文件，不会对包文件压缩 **必需**
* -z 调用gzip压缩文件，并把文件打包成“.tar.gz”包文件
* -j 调用bzip2来压缩文件，并把文件打包成“.tar.bz2”包文件
* -J 调用xz来压缩文件，并把文件打包成“.tar.xz”包文件
* -v 显示命令执行过程
* -f 指定打包或解包的文件名，该选项必须放到最后一位

**解压命令**

​		tar -xf 压缩文件名 [-C 目标目录]

* -x 解压“ .tar ”包文件
* -f 指定文件名，该选项必须放到最后一位
* -t 不解压，查看压缩文件内容



### 软件安装

**YUM方式**（自动安装依赖）

* 配置YUM源

1. 删掉默认的源，避免混乱

   rm -f /etc/yum.repos.d/* 

2. 下载阿里源配置文件

   wget http://mirrors.aliyun.com/repo/Centos-8.repo -O /etc/yum.repos.d/Centos8.repo

* 常用命令

  ```
  yum list [软件包名]    // 检测YUM源yum info 软件包名      // 查看软件包信息yum install 软件包名   // 安装软件yum remove 软件包名    // 卸载软件（会删除依赖）yum clean all        // 清除本地缓存
  ```

**RPM方式**（不安装依赖，主要用于查询）

* 安装

  rpm -ivh 软件包路径

  * -i 安装
  * -v 显示过程
  * -h 显示进度

* 卸载

  rpm -r 软件包

  * -r 删除

* 查询

  rpm -q 软件包

  * -q 查询
  * -a 列出系统中所有已安装软件包
  * -i 查询软件包信息
  * -l 查询软件包所安装的文件及安装位置
  * -c 查询安装包所安装的配置文件
  * -f 查询某个文件所属的软件包

**源码方式**

* 安装编译器

  1. 检查是否已安装gcc

     rpm -qa gcc   

  2. 没安装的话安装

     yum install gcc

* 编译安装

  1. 下载软件

     wget 文件路径

  2. 解压

     tar -zxf 文件 -C 目录

  3. 配置

     运行源码目录configure进行。./configure

     --prefix 参数可设置安装目录

  4. 编译

     make

  5. 安装部署

     make install

