##Install Unity3d
######MacOSX
	破解工具 <Unity Medkit 2018.x.app>
######Windows
	...
##MonoFramework
######MacOSX
	# vscode [OmniSharp] 需要这个环境变量
	export FrameworkPathOverride=/Library/Frameworks/Mono.framework/Versions/6.4.0
	# vscode [Debugger for Unity] 需要mono运行时
	export PATH=${FrameworkPathOverride}/bin:$PATH
	注意：如果未安装MonoFramework，建议使用`brew install mono`安装。
######Windows
	下载安装 [net framework Dev Pack 4.7.1](https://download.microsoft.com/download/9/0/1/901B684B-659E-4CBD-BEC8-B3F06967C2E7/NDP471-DevPack-ENU.exe)