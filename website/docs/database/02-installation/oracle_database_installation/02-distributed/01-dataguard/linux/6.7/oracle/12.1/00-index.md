---
layout: page
title: Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/
---

# Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7

# Alfa версия. Документ пока в разработке!  


Технология Oracle Data Guard предалагает решение для обеспечения высокой доступности, повышенной производительности и автоматического преодоления последствий сбоя.

Изменения в основной базе данных могут быть переданы в резернвые базы данных с гарантией отсутствия потерь данных в процессе передачи.


Поддерживаются 2 типа резервных баз данных - с осуществлением физического и логическог резервирования.
Физическая резервная база данных содержит те же самые структуры, что и основная. Логическая - может иметь другие внутренние структуры (например, дополнительные индексы, используемые для генерации отчетов). Синхронизация основной базы данных с резервными осуществляется путем передачи журнальных данных через SQL - операторы, выполняемые над резервной базой данных.

Физическая резервная база данных является поблочной копией первичной базы данных. Во время восстановления в аварийных ситуациях, резервная база даных в точности похожа на основную базу данных.

Логическая база данных - используется для подготовки отчетов (при подготовке отчетов требуются существенные ресурсы системы). В этом случае резервная база данных открывается только для чтения и пользователи, которым необходимо сформировать отчеты работают с ней. При этом основная база данных продолжает работать на прием данных от операторов.


<br/>

У меня нет environment, где бы я постоянно работал с dataguard. Здесь я постараюсь его настроить. Буду обновлять по мере появления новых знаний.

В случае обнаружения ошибок, неточностей, опечаток или вам известны лучшие способы, пишите мне на адрес эл. почты:


<div>
	<img src="http://img.fotografii.org/a3333333mail.gif" border="0">
</div>


<br/>

**И да, я пока не читал Concepts Guide по DataGuard и в ближайшее время не планирую. Нигде, где бы я работал, она не использовалась, т.к. дорого. Как будут задачи, так сразу приступлю к более глубокому изучению.
Поэтому, уточнения будут оч. полезны.**


Суть DataGuard для человека, не читавшего Concepts Guide выглядит достаточно просто. Нужно 2 одинаковых (или приблизительно одинаковых) сервера. На одном будут выполняться какие-то повседневные задачи, на другом, например строиться отчеты, которые жрут много процессорного времени, памяти и т.д.

Для этого делается копия основного сервера. Основной сервер делится архивлогами с резервным, поддерживая таким образом актуальной базу. При этом если первый сервер пиздой накроется, то можно будет их поменять местами.

Можно также настроить работу сервера в режиме failover (Аварийное переключение) и switchover.


DataGuard работает Enterprise конфигурации, цена за лицензию будет выше, чем за стандарт. Раз так, то может быть дешевле будет развернуть 2 Standart сервера и одному подкладывать архивлоги от другого, например с помощью RSYNC.

Еще можно подобную задачу решить с помощью Oracle Golden Gate. Может быть решение с Golden Gate будет лучше.


<br/>

<div style="padding:10px; border:thin solid black;">

<strong>Для информации:</strong>

<br/>

db_name - имя нашей базы (одинаковое для основного и standby экземпляра).  <br/>

db_unique_name - это уникальное имя для каждого экземпляра, оно не меняется при смене ролей со standby на production.


</div>


<br/>

## Подготовка виртуальных машин:


<ul>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/info-about-env/">Описание системы, которое будет настраиваться</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/prepare-env/">Предварительные шаги по настройке environment</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/prepare-instance/">Предварительные шаги по настройке параметров instance</a></li>

</ul>



<br/>


## Подготовка и создание DATAGUARD:

<ul>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/create-foder-structure-like-on-primary/">Создание каталогов на standby, котырые есть на primary</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/copy-passwords-file/">Копирование файла паролей с primary на standby</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/startup-instance-on-standby/">Стартую instance на standby</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/setup-oracle-network-services/">Настройка сетевых служб Oracle для создания дупликата primary на standby</a></li>


	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/setup-instance-parameters-to-work-in-dataguard/">Настройка параметров instance на primary для работы в DataGuard конфигурации</a></li>


	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/standby-redologs-on-primary-instance/">Создание standby redologs на primary</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/rman-connection-check/">Проверка подключения RMAN к обоим Instance</a></li>


	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/run-rman-script-for-duplicate-instance/">Создание rman скрипта для создания дупликата primary и его выполнение</a></li>


	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/post-duplicate-steps-on-standby/">Настройка параметров Instance после создания дупликата на standby</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/post-duplicate-steps-standby-redologs/">Создание standby redologs (Не знаю, нужен этот шаг или нет. Работает и без него. Может быть еще и не получится его выполнить)</a></li>

	<li><a href="/oracle-database-installation/dataguard/linux/6.7/oracle/12.1/check-redo-apply/">Проверка применения redo</a></li>

</ul>




<br/>
<br/>

**Материалы по теме: (Сортирока от более полезных, к менее)**:


<ul>
	<li><a href="https://pierreforstmanndotcom.wordpress.com/2014/11/28/create-a-physical-standby-database-with-oracle-12-1-0-2-and-rman-active-duplication/">[ENG] Create a physical standby database with Oracle 12.1.0.2 and RMAN active duplication</a></li>
	<li><a href="http://habrahabr.ru/post/120495/">[HabraHabr] Еще раз про Oracle standby</a></li>
	<li><a href="http://docs.oracle.com/cd/B19306_01/server.102/b14239/toc.htm">[ENG] Data Guard Concepts and Administration</a></li>
	<li><a href="http://docs.oracle.com/cd/B28359_01/server.111/b28294/rcmbackp.htm">[ENG] Creating a Standby Database with Active Database Duplication</a></li>
</ul>