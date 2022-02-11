---
title: 使用mvnd替代mvn打包
date: 2021-12-26 21:14:15
tags: 
- maven
- java
categories: 
- 后端
---

​	以linux为例，windows和mac安装步骤类似

1. 安装mvnd,从github上下载最新的release包

   ```
   https://github.com/apache/maven-mvnd/releases
   ```

2. 解压缩

   ```
   sudo unzip mvnd-0.7.1-linux-amd64.zip -d /usr/maven/
   ```

3. 配置环境变量,把执行文件目录追加到PATH中

   ```
   echo 'export PATH=$PATH:/usr/maven/mvnd-0.7.1-linux-amd64/bin'|sudo tee -a /etc/profile
   ```

4. 修改配置文件(复制解压缩目录下的配置文件到.m2目录下)

   ```
   cp /usr/maven/mvnd-0.7.1-linux-amd64/conf/mvnd.properties ~/.m2/
   vim ~/.m2/mvnd.properties
   ```

   修改

   ```
   mvnd.minHeapSize = 512M
   mvnd.maxHeapSize = 3G
   mvnd.maxLostKeepAlive = 180
   ```

5. 重启电脑（或者使用source命令使环境变量生效）

   ```
   reboot
   或者
   source /etc/profile
   ```

6. 可以使用啦

   ```
   mvnd clean install -DskipITs -DskipTests
   打包完成后记得手动关闭后台进程哦
   mvnd --stop
   如果不想手动关闭可以在mvnd.properties中加上
   mvnd.noDaemon = true
   ```

7. 效果

   3-4分钟左右可以打包完web-components

   电脑配置ThinkPad-E431

   系统：Ubuntu 20.04.3 LTS

   CPU：Intel® Core™ i5-3320M CPU @ 2.60GHz × 4 

   内存：16G

   硬盘：256G固态

8. 遇见过的错误

   （1）超时报错

   ​		解决：修改配置文件的mvnd.maxLostKeepAlive为180
