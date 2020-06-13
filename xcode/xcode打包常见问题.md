##Mach-O Type 系列问题
###Relocatable Object File
######-rpath can only be used when creating a dynamic final linked image
	在 Build Settings 里清空 Runpath Search Paths
	(@executable_path/Frameworks、@loader_path/Frameworks)
	
##IPA processing failed
![](/Users/joli/Priv/blog/xcode/images/20200328095340182.png)
	
	第一步，点击 Show logs
	第二步，打开 IDEDistribution.standard.log
	第三步，拉倒log末尾，向上搜索x86_64，找到出问题的framework。
	第四步，查看framework的构架
		lipo -info ${xxx}.framework/xxx
	第五步，删除i386和x86_64构架
		lipo -remove i386 ${xxx}.framework/xxx -o ${xxx}.framework/xxx
		lipo -remove x86_64 ${xxx}.framework/xxx -o ${xxx}.framework/xxx
	