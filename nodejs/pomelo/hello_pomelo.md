##Install
	cnpm i pomelo -g
##New Project
	1、进入工程目录
		mkdir HelloPomelo
		cd HelloPomelo
	2、初始化pomelo工程
		pomelo init
		... select 2 for socket.io
	3、修改根目录下的 npm-install.sh，将所有的npm改为cnpm
		`
		cd ./game-server && cnpm install -d
		echo '============   game-server npm installed ============'
		cd ..
		cd ./web-server && cnpm install -d
		echo '============   web-server npm installed ============'
		`
	4、安装依赖包
		sh npm-install.sh
##Start Project
	cd ./game-server
	pomelo start
##FQA
###env: node\r: No such file or directory
	原因：pomelo是个doc命令行，含有\r\n换行符，需转换成unix命令行。
	1、安装 dos2unix
		brew install dos2unix
	2、进入 pomelo 执行文件处
		cd ~/.nvm/versions/node/v12.13.0/lib/node_modules/pomelo/bin
	3、执行转换
		sudo dos2unix pomelo