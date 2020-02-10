##Install
	cnpm i pomelo -g
##New Project
	1、进入工程目录
		mkdir HelloPomelo
		cd HelloPomelo
	2、初始化pomelo工程
		pomelo init
		... select 2 for socket.io
	3、安装依赖包
		~sh npm-install.sh~
		**./web-server: No such file or directory**
		**正确做法**
		cd ./game-server
		npm install -d
		cd ../
		cd ./web-server
		npm install -d
##Start Project
	cd ./web-server
	pomelo start
	cd ./game-server
	pomelo start
##FQA
###env: node\r: No such file or directory
	原因：pomelo是个在windows下裸奔的node命令行（含有\r\n换行符），需转换成unix命令行。
	1、安装 dos2unix
		brew install dos2unix
	2、进入 pomelo 执行文件处
		cd ~/.nvm/versions/node/v12.13.0/lib/node_modules/pomelo/bin
	3、执行转换
		sudo dos2unix pomelo