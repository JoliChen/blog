##cp
	cp -R {src} {dst} 拷贝文件夹
##ls
	ls -a 列出文件夹（包括隐藏文件）
##ps
	ps -axu {user} | grep {process_name}
	ps -ef | grep {process_name} 列出进程
##kill
	sudo kill -9 {process_id} 关闭进程
##lsof
	sudo lsof -i :{port} 查看端口占用
	sudo lsof -i :3005|grep -i "listen"
##brew
	brew update 更新homebrew自身
	brew upgrade {target} 更新安装包（如果不指定具体对象会将所有的安装包更到最新）