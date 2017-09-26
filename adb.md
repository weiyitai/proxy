列出设备列表  

	adb devices  
安装应用  

	adb install + 文件路径		//adb install D:\微信.apk
指定某个设备安装应用(当电脑连接多个设备时)

	adb -s 设备序列号 install	 + 文件路径		//adb -s PBV7N16913007233 install 文件路径 
保存原apk数据并安装应用

	adb install -r + 文件路径			//adb install -r D:\微信.apk
卸载应用

	adb uninstall + 应用包名			//adb uninstall com.tencent.mobileqq
重启设备

	adb reboot
复制手机文件到电脑

	adb pull sdcard/360 d:\log		//将SD卡上名为360的文件夹复制到电脑 D盘下的log文件夹,文件同理
复制电脑文件到手机

	adb push d:\log\a.txt sdcard   //将电脑D盘下log文件夹下的a.txt文件复制到SD卡,文件夹同理
### 以下为 进入设备后的命令
进入设备

	adb shell
切换到当前目录的子目录

	cd sdcard			 //切换到sdcard
列出当前目录下的所有文件

	ls				
切换到上一层目录

	cd ..
切换到根目录

	cd /
删除文件

	rm 文件路径			//rm sdcard/a.log  删除SD卡名为a.log的文件
强制删除文件

	rm -f 文件路径   		//rm sdcard/1/a.txt		强制删除SD卡文件夹1下的a.txt文件
创建文件

	touch sdcard/1/b.md			//在SD卡1文件夹下创建b.md文件
	echo> sdcard/1/c.txt		//在SD卡1文件夹下创建c.txt文件
查看文件内容

	cat casdrd/1/c.txt			//查看c.txt的内容并输出到控制台
重定向写入文件

	echo "new text" > sdcard/1/c.txt	//清空c.txt里面的内容并写入新内容 new text
追加写入文件
	
	echo "another new text" > sdcard/1/c.txt	//在c.txt的末尾另起一行追加写入another new text

删除空文件夹 

	rmdir 文件夹名称		//rmdir sdcard/1   删除SD卡上名为1的空文件夹
删除文件夹及该文件夹下的所有文件

	rm -r 文件夹名称		//rm sdcard/2	   删除SD卡下名为2的文件夹及该文件夹下的所有文件
创建文件夹

	mkdir 文件夹名称			//mkdir sdcard/2	   在SD卡上创建名为2的文件夹
移动文件

	mv sdcard/360/a.jpg sdcard/2			//将SD卡360文件夹下的a.jpg移动到SD卡名为2的文件夹下
移动文件并改名

	mv sdcard/360/a.jpg sdcard/2/b.png		//将SD卡360文件夹下的a.jpg移动到SD卡名为2的文件夹下并改名为b.png
移动文件夹

	mv sdcard/2 sdcard/360/		//将SD卡名为2的文件夹移动到360文件夹下
复制文件

	cp sdcard/360/aa.jpg sdcard/2/			//将SD卡360文件夹下的aa.jpg复制到SD卡名为2的文件夹下
文件重命名

	rename 2/a.png 2/ c.png			//将文件夹2下名为 a.png的文件重命名为 c.png

---
#### 手机截屏  
1.保存到手机
	
	screencap -p sdcard/a.png						//进入设备后(adb shell)的操作,保存截屏到SD卡并命名为a.png
	adb shell screencap -p sdcard/a.png				//截取当前屏幕并保存到SD卡并命名为a.png
	adb shell system/bin/screencap -p sdcard/a.png		//截取当前屏幕并保存到SD卡并命名为a.png
2.保存到电脑  
 在电脑D盘新建文件并命名为 cap.bat的批处理文件,将以下代码拷贝到文件并保存,双击运行批处理文件,就会截取当前屏幕并保存到批处理文件所在文件夹

	@echo off
	set year=%date:~0,4%
	set month=%date:~5,2%
	set day=%date:~8,2%
	set hour=%time:~0,2%
	set min=%time:~3,2%
	set sec=%time:~6,2%
	set name=%year%%month%%day%_%hour%%min%%sec%.png
	rem 下面是输出语句
	::echo %name%
	adb shell screencap -p /sdcard/1/%name%
	adb pull /sdcard/1/%name%
	adb shell rm /sdcard/1/%name%
	::pause >nul
参考:[https://stackoverflow.com/questions/1192476/format-date-and-time-in-a-windows-batch-script](https://stackoverflow.com/questions/1192476/format-date-and-time-in-a-windows-batch-script)

	

#### 手机录屏,支持MP4及avi格式(部分手机不支持),默认180s,不录制声音,按Ctrl + C停止录屏
可以输入  `adb shell screenrecord --help` 查看支持哪些参数

	adb shell screenrecord sdcard/1/a.mp4		//手机录屏并保存到SD卡的1文件夹下名为a.mp4
指定录制时间(支持 1 ~ 180 s),如果不指定,默认180s

	adb shell screenrecord --time-limit 10 sdcard/1/b.mp4	//手机录屏10s并保存到SD卡的1文件夹下名为b.mp4
指定录制分辨率

	adb shell screenrecord --size 2560x1440 sdcard/1/c.mp4
指定录制时间跟分辨率

	adb shell screenrecord --time-limit 5 --size 2560x1440 sdcard/1/d.mp4
指定码率

	adb shell screenrecord --bit-rate 5000000 sdcard/1/g.mp4
	
#### 日志
输出日志到控制台
	adb logcat *:d		//打印debug级别日志到控制台
日志输出到文件
	
	adb logcat -d time > D:\log.txt		//将debug级别日志输出到D盘log.txt文件
	



#### 模拟点击屏幕

	adb shell input tap 1000 500 	//模拟点击屏幕上坐标为(1000,500)的点

	
	

  
  
  
  
