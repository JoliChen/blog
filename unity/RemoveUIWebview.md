##去除libiPhone-lib.a中的UIWebview
###新建URLUtility.o
####1、新建文件 URLUtility.mm
	#include <iostream>
	#import <UIKit/UIKit.h>
	using namespace std;
	namespace core {
		template <class type>
		class StringStorageDefault {};
		template <class type,class type2>
		class basic_string {
		public:
		char *c_str(void);
		};
	}
	void OpenURLInGame(core::basic_string< char,core::StringStorageDefault<char> > const&arg){}
	void OpenURL(core::basic_string<char,core::StringStorageDefault<char> >const&arg){
		const void *arg2= &arg;
		UIApplication *app = [UIApplication sharedApplication];
		NSString *urlStr = [NSString stringWithUTF8String:(char *)arg2];
		NSURL *url = [NSURL URLWithString:urlStr];
		[app openURL:url];
	}
	void OpenURL(std::string const&arg){
		UIApplication *app = [UIApplication sharedApplication];
		NSString *urlStr = [NSString stringWithUTF8String:arg.c_str()];
		NSURL *url = [NSURL URLWithString:urlStr];
		[app openURL:url];
	}
####2、使用clang编译成目标文件
	clang -fembed-bitcode -c URLUtility.mm -arch armv7 -isysroot ${iPhoneOS.sdk}
	clang -fembed-bitcode -c URLUtility.mm -arch arm64 -isysroot ${iPhoneOS.sdk}
	${iPhoneOS.sdk}：/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk
	--------------------------------------------------------------------------

##拆分libiPhone-lib.a
	lipo -info libiPhone-lib.a
	***Architectures in the fat file: libiPhone-lib.a are: armv7 arm64***
	
	lipo libiPhone-lib.a -thin armv7 -output ./libiPhone-lib7.a
	lipo libiPhone-lib.a -thin arm64 -output ./libiPhone-lib64.a
	
##替换静态库中URLUtility.o（注意对应ARM）
	【方式 1】
	查看静态库中object
	xcrun -r ar -v -t libiPhone-lib.a
	
	删除静态库中object
	xcrun -r ar -v -d libiPhone-lib7.a URLUtility.o
	将object文件添加到静态库末尾
	xcrun -r ar -v -q libiPhone-lib7.a ./armv7/URLUtility.o
	
	删除静态库中object
	xcrun -r ar -v -d libiPhone-lib64.a URLUtility.o
	将object文件添加到静态库末尾
	xcrun -r ar -v -q libiPhone-lib64.a ./arm64/URLUtility.o
	
	你也可以直接替换静态库中object
	xcrun -r ar -v -r libiPhone-lib7.a URLUtility.o
	xcrun -r ar -v -r libiPhone-lib64.a URLUtility.o
	
	纯ar命令操作可能会收到如下错误，因为这可能是运行系统的ar工具，故使用xcrun运行ar命令。
	*** ar: ./libiPhone-lib.a: malformed archive ***
	--------------------------------------------------------------------------
	
	【方式 2】
	1、将静态库中所有object文件解压到当前目录
	xcrun -r ar -v -x libiPhone-lib7.a
	xcrun -r ar -v -x libiPhone-lib64.a
	2、直接文件替换操作（用clang编译的URLUtility.o替换解压出来的URLUtility.o）
	3、使用libtool将所有object文件打包成新的静态库
	xcrun -r libtool -no_warning_for_no_symbols -static -o ../libiPhone-lib7.a *.o
	xcrun -r libtool -no_warning_for_no_symbols -static -o ../libiPhone-lib64.a *.o

##合并libiPhone-lib.a
	lipo -create ./libiPhone-lib7.a ./libiPhone-lib64.a -output libiPhone-lib.a
