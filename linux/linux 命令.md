# linux 命令

## Linux 命令组成部分
```
command [option] [arguments]
```

* 主要命令区分大小写
* 使用tab可以补全命令剩余部分
* 使用帮助 find --help


## 常用命令

### 目录操作命令
* `sudo su` 登录高级管理员
* `init 0` 或者 `sudo init 0` 关机
* `ls` 列出文件 （不包含隐藏文件）
  * `ls -alh` 展示文件的权限用户大小时间等信息
* `ll` 列出所有文件
* `pwd` 列出所在位置
* `cd` 切换目录 
  * `cd` 切换到根目录
  * `cd .` 切换到当前目录
  * `cd ..` 切换到上层目录
* `mkdir` 创建文件夹
  * `mkdir aa bb` 在同目录下创建aa bb两个文件夹
* `rmdir` 删除文件夹
* 
### 文件操作命令
* `cp` 拷贝文件（单个文件）
  * `cp 源文件 目标地址`
    * `cp -R` 文件夹下的所有文件
* `rm -rf` 删除文件或目录（r：递归 f：强制）
* `mv` 移动文件/重命名文件
  * `mv 源文件 目标地址`
* `find` 查找文件

### 文件查看命令

* `cat` 查看文件
* `more` 
* `less` 
* `head` 查看文件，重头开始
* `tail` 查看文件，重尾开始
  * `tail -f` 实时滚动

### 磁盘
* `df -h` 查看使用磁盘情况
* `du -sh` 统计查看当前目录使用量
  * `du -sh *` 统计查看当前目录各个文件夹使用量



## 系统

* `ps` 查看进程状态
  * ps -ef | grep ...  查询某个进行 然后kill 9 进程号删除
* top 实时显示进程动态
* 查看系统版本
  * uname -a 查看内核信息
  * cat /ect/issue 查看是ubuntu、centos
  * cat /ect/lsb-release     ubuntu存在该文件
  * cat /ect/redhat-release   centos 存在该文件



## 网络

* netstat 查看网络状态
  * netstat -pln | grep ... 查看当前所有端口
  * netstat -an | grep 3306   //查看所有3306端口使用情况



## 快捷键

* `ctrl c` 强制退出当前程序
* `ctrl d` 退出当前用户

