---
layout: page
title: Создание схемы в базе данных для приложения OBIEE с помощью Repository Creation Utility (RCU)
permalink: /docs/business-intelligence/repository-creation-utility/
---


<h2>Создание схемы в базе данных для приложения OBIEE с помощью Repository Creation Utility (RCU):</h2>


Дистрибутив RCU спраятали, что его не так просто и найти.

Скачал следующим образом:  
Зашел на сайт Oracle по следующей ссылке:  
http://www.oracle.com/technetwork/middleware/soasuite/downloads/index.html

Поставил галочку о принятии условий.

Далее скачал дистрибутив по ссылке:

Linux:  
http://download.oracle.com/otn/linux/middleware/11g/111170/ofm_rcu_linux_11.1.1.7.0_64_disk1_1of1.zip


Windows:  
http://download.oracle.com/otn/nt/middleware/11g/111170/ofm_rcu_win_11.1.1.7.0_32_disk1_1of1.zip



	# groupadd -g 1001 oraclebi
	# useradd -g oraclebi -d /home/oraclebi -m oraclebi
	# passwd oraclebi


<br/>

	# yum install -y unzip
	# yum install -y nc


на клиенте с которого идет процесс управления инсталляции

	$ xhost +192.168.1.9

<br/>

	# nc -vv 192.168.1.5 6000
	Connection to 192.168.1.5 6000 port [tcp/x11] succeeded!

<br/>

	$ su - oraclebi

<br/>

	$ unzip ofm_rcu_linux_11.1.1.7.0_64_disk1_1of1.zip

<br/>

	Exception in thread "main" java.lang.UnsatisfiedLinkError: /files/rcu/rcuHome/jdk/jre/lib/amd64/xawt/libmawt.so: libXtst.so.6: cannot open shared object file: No such file or directory

<br/>

	# yum install -y xdpyinfo

Если ошибка не пропадет, рекомендую установить

	# yum install -y libXp

<br/>

	$ export DISPLAY=192.168.1.5:0.0

<br/>

	$ cd /tmp/rcuHome/bin
	$ ./rcu


<br/><br/>

<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/repository_creation_utility/Repository_Creation_Utility_01.png"><br/><br/>
<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/repository_creation_utility/Repository_Creation_Utility_02.png"><br/><br/>
<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/repository_creation_utility/Repository_Creation_Utility_04.png"><br/><br/>
<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/repository_creation_utility/Repository_Creation_Utility_05.png"><br/><br/>
<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/repository_creation_utility/Repository_Creation_Utility_06.png"><br/><br/>
<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/repository_creation_utility/Repository_Creation_Utility_07.png"><br/><br/>
<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/repository_creation_utility/Repository_Creation_Utility_08.png"><br/><br/>
<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/repository_creation_utility/Repository_Creation_Utility_09.png"><br/><br/>
<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/repository_creation_utility/Repository_Creation_Utility_10.png"><br/><br/>
<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/repository_creation_utility/Repository_Creation_Utility_11.png"><br/><br/>
<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/repository_creation_utility/Repository_Creation_Utility_12.png"><br/><br/>
<br/><img src="http://img.oradba.net/img/oracle/middleware/oracle-bi/repository_creation_utility/Repository_Creation_Utility_13.png"><br/><br/>
