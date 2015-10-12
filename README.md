####工具说明：

liveshell工具是采用Wilddog云以及WildDog C/嵌入式SDK制作的，远程调用shell脚本的工具。它监听某个url下数据的变化，当数据发生变化后，触发预先安排好的可执行程序或者shell脚本，同时将变化后的数据作为参数传入。

WildDog C/嵌入式的SDK 使用的是CoAP UDP + DTLS + COBR技术。

Linux发行版均可使用该工具，已在以下发行版中测试过：

	Linux版本                                                       内核版本
	centos-release-7-1.1503.el7.centos.2.8.x86_64                   3.10.0-229.el7.x86_64
	centos-release-6-5.el6.centos.11.1.x86_64                       2.6.32-431.el6.x86_64
	centos-release-5.5.el5.centos                                   2.6.18-194.el5
	Red Hat Enterprise Linux Server release 7.1  (Maipo)            3.10.0-229.el7.x86_64
	Red Hat Enterprise Linux Server release 6.6 (Santiago)          2.6.32-504.el6.x86_64
	Red Hat Enterprise Linux Server release 5.11 (Tikanga)          2.6.18-398.el5
	Ubuntu14.04.01                                                  3.16.0-30-generic
	Ubuntu12.04                                                     3.13.0-32-generic

####linux环境下安装说明：
#####1. 下载

从git下载到文件夹

	git clone https://github.com/WildDogTeam/liveshell.git
	
更新C/嵌入式SDK

	cd liveshell	
	git submodule update --init --recursive

#####2. 安装
注意权限，install需要sudo

	./configure
	make
	make install

#####3.使用

	liveshell  [option] <your wilddog url> <your callback command>

#####4. 参数说明

	-o 获取到原始数据也会触发一次command回调

	-s 当数据为字符串时，不解析该字符串，完整的将该字符串（以双引号包裹）传递给command回调
	
	-v 触发回调时将命令完整打出
	
	-h 打印帮助信息
	
#####5. 例子

######显示根目录的文件

1. 在Wilddog云端建立一颗数据树，结构为

		{
		  "path": "/"
		}	

2. 终端运行liveshell，将`<your Appid>`替换成你自己的appid

		liveshell coaps://<your Appid>.wilddogio.com/path ls

3. 终端的显示结果等同于在终端运行"ls /"，修改云端数据，把"/"改为"-l /"，在终端立刻显示"ls -l /"的结果；类似的，你也可以将<your callback command>改为shell脚本，执行更加复杂的操作。
