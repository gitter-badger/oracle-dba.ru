---
layout: page
title: Инсталляция Oracle RAC 12.1 в операционной системе Oracle Linux 6.7 (SHARED FILE SYSTEM)
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/
---

# Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM  в операционной системе Oracle Linux 6.7


<br/>

В документе описывается один из способов инсталляции базы данных Oracle в операционной системе Oracle Linux в конфигурации Real Application Cluster (RAC).


В случае обнаружения ошибок, неточностей, опечаток или Вам известны лучшие способы, пишите мне адрес эл. почты:


<div>
	<img src="http://img.fotografii.org/a3333333mail.gif" border="0">
</div>

<br/><br/>



## Документация:

<ul>
	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/docs/">Официальная документация</a></li>
</ul>


<br/><br/>


## Описание окружения для инсталляции Oracle RAC:

<ul>
	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/environment-description/">Описание окружения для инсталляции Oracle RAC</a></li>
</ul>



<br/><br/>
<h2>Дистрибутивы:</h2>


<ul>
	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/distrib/">Дистрибутивы баз данных и дополнительное программное обеспечение</a></li>
</ul>

<br/>

### Конфиги виртуальных машин virtualbox:


<ul>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/vm/">Конфиги виртуальных машин virtualbox</a></li>

</ul>



<br/>

### Подготовка окружения для инсталляции RAC:


<ul>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/network-interfaces/">Настройка сетевых интерфейсов</a></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/setup-os-parameters-before-begin/">Предварительные настройки</a></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/setup-dns-server/">Настройка DNS сервера</a></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/install-mandatory-packages/">Инсталляция обязательных пакетов</a></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/autostart-only-packages-what-needed/">Выбор пакетов для автозапуска</a> (Необязательный шаг, можно пропустить)</li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/setup-actual-time/">Настройка сервисов отвечающих за синхронизацию времени</a></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/users-and-groups-creation/">Создание пользователя oracle12 и административных групп</a></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/secure-shell-between-nodes/">Настройка Secure Shell между узлами кластера</a></li>


<br/><br/><br/><br/><br/><br/>


	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/prepare-storage/">Подготовка сервера storage (ISCSI)</a></li>


	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/prepare-hdd-to-install-oracle/">Подготовка локальных дисков на узлах кластера для инсталляции на них Oracle Database Software</a></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/mount-iscsi-on-nodes/">Монтирование SCSI дисков на узлах кластера</a></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/asmlib-installation/">Инсталляция ASMLIB на узлах кластера</a></li>


	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/prepare-asm-discs/">Настройка конфигурации для работы в ASM</a></li>


<br/><br/><br/><br/><br/><br/>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/configure-kernel-parameters-and-user-environments/">Изменение параметров ядра и параметров учетной записи администратора базы данных</a></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/create-folder-structure-and-user-permissions/">Создание структуры каталогов и назначение необходимых прав</a></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/copy-oracle-distrib-on-server/">Копирование дистрибутивов базы данных на сервер</a></li>


	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/check-environment-before-install/">Проверка конфигурации кластера перед инсталляцией RAC</a></li>

	<li>Проверка работы Display Manager</li>


</ul>

<br/><br/>

## Инсталляция RAC и создание экземпляров баз данных:


<ul>
	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/grid-installation/">Инсталляция Grid</a></li>

	<li><a href=" /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/oracle-database-software-installation/">Инсталляция Oracle Database Software</a></li>

	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/oracle-instance-creation/">Создание экземпляра (instance) базы данных</a></li>

</ul>


<br/><br/>

## Шаги, выполняемые после развертывания RAC:


<ul>
	<li><a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/post-installation-tasks/">После инсталляции</a></li>
</ul>