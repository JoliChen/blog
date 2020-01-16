##Install
###macosx
	mysql8.0直接使用brew安装。mysql8.0以下推荐直接从官网下载安装包安装。
	安装包下载地址：https://dev.mysql.com/downloads/mysql/

##FQA
###Access denied for user 'root'@'localhost' (using password: YES)
	原因：连接数据库密码错误
	第一步：关闭mysql
		苹果->系统偏好设置->点击服务栏(Mysql)->关闭mysql服务 或者 在终端输入mysql.server stop
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
![alter psw commands](https://github.com/JoliChen/joli-blog/blob/master/mysql/images/alter_psw.png?raw=true)

###ERROR 1819 (HY000): Your password does not satisfy the current policy requirements
	原因：自定义密码不符合密码策略
	1、查看mysql的密码策略
		 SHOW VARIABLES LIKE 'validate_password%';
	2、设置密码验证强度等级
		set global validate_password_policy=LOW;
	3、设置密码长度，默认是8位，一般使用6位
		set global validate_password_length=6;
	4、设置好密码策略后，可以重新更改密码
		ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';
	
	密码策略相关参数：
		validate_password_length 固定密码的总长度
		validate_password_dictionary_file 指定密码验证的字典文件路径
		validate_password_mixed_case_count 整个密码中至少要包含大/小写字母的总个数
		validate_password_number_count 整个密码中至少要包含阿拉伯数字的个数
		validate_password_policy 指定密码的强度验证等级，默认为 MEDIUM
	关于 validate_password_policy 的取值：
		LOW：只验证长度
		MEDIUM：验证长度、数字、大小写、特殊字符
		STRONG：验证长度、数字、大小写、特殊字符、字典文件
	