1. [文件管理](#file)
2. [硬件维护](#hardware)
3. [系统维护](#system)
4. [用户权限](#users)
5. [HomeBrew](#homebrew)

# <span id="file">文件管理</span>
##cd 切换文件夹
`cd {dir}`

##pushd popd 栈式切换
`pushd {dir}`
`popd`

##pwd 打印当前工作目录路径

##ls 列出当前目录
	-a 包含隐藏文件
	-i 详细信息
	-w 显示中文
`ls -a -i`

##mkdir 新建文件夹
	-m 文件夹模式
`mkdir {dir}`
	
##cp 拷贝
	-R 递归文件夹
`cp -R {src_dir} {dst_dir}` 拷贝文件夹

##rm 删除
	-r 递归文件夹
	-f 强制执行
**`rm -rf /`删库跑路，谨慎！！！**

##mv 移动
`mv {src_file} {dst_dir}` 将文件{src_file}拷贝到文件夹{dst_dir}下
	
# <span id="hardware">硬件维护</span>

# <span id="system">系统维护</span>
##ps
	ps -axu {user} | grep {process_name}
	ps -ef | grep {process_name} 列出进程
##kill
	sudo kill -9 {process_id} 关闭进程
	
# <span id="users">用户权限</span>
##sudo
	允许系统管理员让普通用户执行一些或者全部的root命令的一个工具，它是面向每个命令的。
	执行sudo时要求输入当前用户密码而不是root用户的密码。
	
##su
	su 申请切换root用户，需要输入root用户密码。
`sudo su` 暂时申请root权限，使用`exit`退出。

`sudo passwd root` 如果没有设置root用户的密码，使用这个指令设置root用户密码。

##lsof
	sudo lsof -i :{port} 查看端口占用
	sudo lsof -i :3005|grep -i "listen"
	
# <span id="homebrew">HomeBrew</span>
##brew
	brew update 更新homebrew自身
	brew upgrade {target} 更新安装包（如果不指定具体对象会将所有的安装包更到最新）