##Install
###macosx
	mysql8.0直接使用brew安装。mysql8.0以下推荐直接从官网下载安装包安装。安装包下载地址：
	https://dev.mysql.com/downloads/mysql/

##FQA
###Access denied for user 'root'@'localhost' (using password: YES)
	问题原因：连接数据库密码错误
	第一步：关闭mysql
		苹果->系统偏好设置->点击服务栏(Mysql)->关闭mysql服务
		或者
		在终端输入 mysql.server stop
	第二步： 重置密码
		1、进入mysql命令行目录
			cd /usr/local/mysql/bin/
		2、获取管理员权限
			sudo su
		3、禁止mysql验证功能，mysql会自动重启，系统偏好中的mysql服务状态会变成running
			./mysqld_safe --skip-grant-tables &
		4、连接mysql
			./mysql
		5、刷新权限（这是mysql语句别忘记输入结尾分号）
			flush privileges;
		6、重置密码
			ALTER USER 'root'@'localhost' IDENTIFIED BY '你的新密码';
		7、退出mysql
			quit
		8、退出sudo
			exit;
		9、重新登录mysql
			![](/Users/joli/Priv/blog/mysql/alter_psw.png)
		
		
		
		
		
	
	