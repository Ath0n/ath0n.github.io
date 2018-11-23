---
layout: post
title: "ubantu安装burpsuite"
date: 2018-11-22
description: "burpsuite"
tag: burpsuite

---
# ubantu安装burpsuite
> 本文中的ubantu系统为16.04 64 位
## 1.安装java环境
java8的下载的地址为:[https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html),我这里选择jdk-8u191-linux-x64.tar.gz。你们看好自已系统的配置，不过现在应该都是用的64位的系统吧，32位的自已变通一下。
下载完了，然后打开终端以root用户进入该文件目录下，记得你的文件下载放在哪里，进入那个目录下就行了。将刚才下载的jdk-8u191-linux-x64.tar.gz文件解压: **tar zxvf jdk-8u191-linux-x64.tar.gz**(这个是终端命令)
将解压的得到的jdk-1.8.0_191复制到/opt目录下: **mv jdk-1.8.0_191 /opt**。
我们再进入/bin目录下(cd /bin)，并在/bin目录下建立java软链接: **ln -s /opt/jdk-1.8.0-191/bin/java java**。
然后再进入/etc目录，我这里用vim修改/etc/profile文件，在文件末尾加上这四行:
```
export JAVA_HOME=/opt/jdk1.8.0_191 #注意版本
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH={JAVA_HOME}/bin:$PATH
```
最后使用命令 **source /etc/profile** 重新执行profile文件。我们回到终端下，输入**echo $JAVA_HOME** ,如果出现**/opt/java1.8.0_191** 则说明安装是成功了。
## 2.安装burpsuite
我们还是通过命令来下载burpsuite,回到终端输入`wget http://labfile.oss.aliyuncs.com/courses/726/burpsuite_free.jar`
等待下载完了之后，将burpsuite_free.jar文件移动到/opt/burpsuite文件夹下。你要先在/opt下建立burpsuite文件夹，通过命令**mkdir burpsuite**来建立文件夹。
这时候就可以使用命令 **sudo java -jar /opt/burpsuite/burpsuite_free.jar** 来直接运行burpsuite_free.jar了，但是我们为了方便，我们还可以更简便一些:
```
cd /opt/burpsuite
sudo chmod +x burpsuite_free.jar
sudo vim /usr/bin/burpsuite #打开文件，输入下面代码,保存就行
    #!/bin/bash
    java -jar /opt/burpsuite/burpsuite_free.jar 
sudo chmod +x /usr/bin/burpsuite

```
之后我们就可以在终端直接输入**sudo burpsuite** 就可以运行burpsuite了。
我也是踩了很多坑才用上burpsuite这个大杀器，这里记录一下ubantu安装burpsuite的过程。