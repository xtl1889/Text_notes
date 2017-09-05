#记录Android开发中遇到的问题


1、包冲突

	错误提示：
			Error:Execution failed for task ':app:preDexDebug'.
			> com.android.ide.common.process.ProcessException: org.gradle.process.internal.ExecException:
			 Process 'command 'D:\Program Files\Java\jdk\bin\java.exe'' finished with non-zero exit value 1
			 
	解决办法：
	//需要添加的代码
		defaultConfig {
	    multiDexEnabled true 
	}
	
2、包太陈旧(需要在android studio 里面新增一些代码  来兼容这些老版)

	错误提示：
			Error:Execution failed for task ':app:packageDebug'.
	> Duplicate files copied in APK META-INF/LICENSE.txt
		File 1: F:\work\My_Demo\social_sdk_example2\app\libs\httpmime-4.1.3.jar
		File 2: F:\work\My_Demo\social_sdk_example2\app\libs\twitter4j-core-4.0.4.jar
		
		解决办法：（http://stackoverflow.com/questions/22467127/error-duplicate-files-during-packaging-of-apk）
			//需要添加的代码
			android {
    			packagingOptions {
		        exclude 'META-INF/DEPENDENCIES'
		        exclude 'META-INF/NOTICE'
		        exclude 'META-INF/LICENSE'
		        exclude 'META-INF/LICENSE.txt'
		        exclude 'META-INF/NOTICE.txt'
		        exclude 'META-INF/ASL2.0'
		        exclude 'META-INF/notice.txt'
   			 }
			}
			
			
3、
	
		错误提示:
		Error:Execution failed for task ':ProjectName:mergeDebugResources'. 
		> Crunching Cruncher *some file* failed, see logs
		
		解决办法： http://stackoverflow.com/questions/29026024/errorexecution-failed-for-task-projectnamemergedebugresources-crunching
			1、Open your Android Studio (AS) program.
			2、Go to your build.gradle file in your project.
			3、Change:
				dependencies {
				    classpath 'com.android.tools.build:gradle:1.1.0'
				to:
				dependencies {
				    classpath 'com.android.tools.build:gradle:1.1.3'
			4、Clean your project.
			5、Rebuild your project.
			6、Done!
			
4、android studio 提示gradle project sync failed.Basic functionality(e.g.editing,debugging) will not work properly.
		出现在之前项目正常，再次打开后出现该错误。
		这种情况下在Project Structure下Compile Sdk Version  各种依赖包等等设置都为空
		
		解决办法：点击 tools ->Android->sync project with gradles files
		
