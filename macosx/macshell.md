##拷贝
	cp -R {src} {dst}
##列出文件夹
	ls -a
##列出进程
	ps -axu {user} | grep {process_name}
	ps -ef | grep {process_name}
##关闭进程
	sudo kill -9 {process_id}
##lsof	查看端口占用
	sudo lsof -i :{port}
	sudo lsof -i :3005|grep -i "listen"