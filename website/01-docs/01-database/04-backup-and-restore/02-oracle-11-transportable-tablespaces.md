---
layout: page
title: Транспортируемые табличные пространства (Transportable tablespaces) в Oracle 11g
permalink: /database/backup-and-restore/oracle-11-transportable-tablespaces/
---


### Транспортируемые табличные пространства (Transportable tablespaces) в Oracle 11g


Оригинал:<br/>
http://habrahabr.ru/post/148535/<br/><br/>

Marley: Я никогда не пользовался данной возможностью. Всегда обходиться утилитами dpdump и dpimp. Правильность я не проверял.<br/>
Утилиты imp и exp имеет смысл использовать только, если вы работаете с 9 версией базы.

<br/><br/>

Табличное пространство можно клонировать и затем включить в другую базу данных путем копирования, а также можно исключить из одной базы данных Oracle и включить в другую базу данных Oracle на той же платформе с помощью перемещения.<br>
<a name="habracut"></a><br>
Перенос данных с помощью перемещения табличных пространств выполняется на порядок быстрее, чем при операциях экспорта/импорта или выгрузки/загрузки, поскольку перемещение табличных пространств состоит только из операций копирования файлов данных и интегрирования метаданных табличных пространств. Перемещение табличных пространств позволяет также перемещать соответствующие индексы, так что после импорта или загрузки табличных данных не требуется перестраивать индексы.<br>
  <br>
<h5>Работа с утилитами экспорта и импорта</h5><br>
Oracle Database позволяет копировать данные между базами данных, а также обмениваться ими с внешними файлами. Копирование осуществляется посредством экспорта и импорта.<br>
Для осуществления данной задачи есть утилиты imp.exe и exp.exe<br>
<br>
<h5>Переносимые табличные пространства </h5><br>
Оперативное предоставление разработчикам свежей копии данных производственной системы. Использование информации, публикуемой на неперезаписываемых носителях (CD-ROM, DVD и т.п.). Быстрое перемещение данных из оперативной системы в хранилище или в витрину данных.<br>
Ускорение переноса информации достигается за счет замены ресурсоемких процессов экспорта-импорта или выгрузки-загрузки значительно более быстрым копированием файлов данных с одной вычислительной установки на другую.<br>
<br>
<h6> Выбор самодостаточного набора табличных пространств </h6><br>
Существует ряд условий ограничивающих применение описываемой возможности. <br>
Можно перемещать табличные пространства только между такими базами данных, которые: <br>
<br>
1. Имеют одинаковый размер блока (db_block_size), созданы с одинаковой кодировкой (character set), в файлах инициализации (INIT.ORA) исходной и целевых баз данных параметр COMPATIBLE должен быть установлен в значение, работают на совместимых платформах одного и того же производителя оборудования. <br>
Удовлетворение требований можно проверить, выполнив в исходной и целевой БД запрос: <br>
<pre><code class="sql"><span class="operator"><span class="keyword">select</span> name, <span class="keyword">value</span> <span class="keyword">from</span> v$parameter <span class="keyword">where</span> name <span class="keyword">in</span> (<span class="string">'db_block_size'</span>,<span class="string">'compatible'</span>)
<span class="keyword">union</span> <span class="keyword">all</span>
selct parameter, <span class="keyword">value</span> <span class="keyword">from</span> nls_database_parameters <span class="keyword">where</span> parameter <span class="keyword">like</span> <span class="string">'%characterset'</span>
</span></code></pre><br>
Результаты запросов в исходной и целевой БД, должны быть одинаковые.<br>
<br>
2. В целевой базе данных не должно быть табличного пространства с таким же именем, как у подключаемого.<br>
<br>
3. Не поддерживается транспортировка: снапшотов и тиражируемых таблиц, функциональных индексов, локальных ссылок на объекты, доменных индексов.<br>
<br>
4. Выбор самодостаточного набора табличных пространств<br>
Самодостаточный набор табличных пространств – это совокупность табличных пространств, объекты которых не ссылаются на какие-либо объекты, не содержащиеся в данном наборе.<br>
Для проверки самодостаточности удобно использовать процедуру TRANSPORT_SET_CHECK(для выполнения процедуры требуется роль EXECUTE_CATALOG_ROLE). <br>

<pre><code class="sql">begin
sys.dbms_tts.transport_set_check (ts_list =&gt; 'USER_DATA', incl_constraints =&gt; true);
end;
</code></pre>

<br>
Результаты ее работы записываются во временную таблицу и их можно посмотреть через системное представление SYS.TRANSPORT_SET_VIOLATIONS:<br>
<pre><code class="sql"><span class="operator"><span class="keyword">select</span> * <span class="keyword">from</span> sys.transport_set_violations
</span></code></pre><br>
<h6>Перенос набора табличных пространств </h6><br>
Сначала следует перевести табличные пространства в состояние READ ONLY(далее в тексте XXX — имя табличного пространства): <br>
<pre><code class="sql"><span class="operator"><span class="keyword">ALTER</span> TABLESPACE TS_XXX <span class="keyword">READ</span> <span class="keyword">ONLY</span>;</span>
</code></pre><br>
Затем с помощью утилиты EXP экспортируются метаданные словаря.<br>
В командной строке следует изменить кодировку для корректного отображения информации.<br>
<pre><code class="dos"><span class="keyword">set</span> nls_lang=russian_cis.ru8pc866
</code></pre><br>
<pre><code class="dos">exp transport_tablespace=y tablespaces=(TS_XXX) triggers=y constraints=y grants=y file=d:\exp_xxx log=d:\exp_xxx
</code></pre><br>
oracle попросит ввести имя пользователя и пароль:<br>
Имя пользователя: sys/system@orcl2012 as sysdba <br>
orcl2012 – строка подключения к исходной БД.<br>
TRANSPORT_TABLESPACE=Y — указывает, что выполняется экспорт метаданных транспортируемых табличных пространств, TABLESPACES=(USERS, USER_DATA, INDX) — задает список транспортируемых табличных пространств, TRIGGERS=Y – Экспортировать табличные триггеры (если указать N, то триггеры экспортироваться не будут) CONSTRAINTS=Y – Экспортировать ограничения целостности (при N не экспортируются ограничения типов PRIMARY KEY, UNIQUE, FOREIGN KEY и CHECK, однако ограничения NOT NULL экспортируются), GRANTS=Y – Экспортировать привилегии доступа к таблицам (N отменяет экспорт привилегий), FILE=exp_tts и log=exp_tts имя файла с данными и имя файла журнала экспорта. <br>
После того как утилита успешно экспортирует метаданные на выходе будет файл с расширением .dmp.(exp_xxx.dmp)<br>
После экспорта метаданных, можно перевести табличные пространства назад в состояние READ WRITE:<br>
<pre><code class="sql"><span class="operator"><span class="keyword">ALTER</span> TABLESPACE TS_XXX <span class="keyword">READ</span> <span class="keyword">WRITE</span>;</span>
</code></pre><br>
<h6>Подключение набора табличных пространств к целевой БД</h6><br>
Перед импортом, необходимо перенести данные от исходной базы данных к целевой:<br>
Это можно сделать средствами ftp, командной строки или копированием средствами Windows.<br>
Нужно копировать файл табличного пространства(.dbf) от исходной БД к целевой.<br>
В командной строке.<br>
<pre><code class="dos"><span class="keyword">Copy</span> \\server1\oradata\orcl\TS_XXX.dbf  \\server2\oradata\orcl\
</code></pre><br>
\\server1\oradata\orcl\TS_XXX.dbf — путь к файлу перемещаемого табличного пространства на исходной базе данных<br>
\\server2\oradata\orcl\ — путь, где будет хранится перемещаемое табличное пространство на целевой базе данных<br>
Теперь можно подключать набор табличных пространств к целевой БД<br>
<pre><code class="dos">imp transport_tablespace=y DATAFILES=('E:\server2\oradata\orcl\TS_XXX.dbf') TABLESPACES=(TS_XXX) TTS_OWNERS=(XXXCORE) fromuser=(XXXCORE) touser=(XXXCORE) FILE=D:\ exp_xxx.dmp LOG=D:\imp_xxx.log
</code></pre><br>
oracle попросит ввести имя пользователя и пароль:<br>
sys/system@ora2015 as sysdba <br>
ora2015 – строка подключения к целевой БД.<br>
TRANSPORT_TABLESPACE=Y – указывает, что импортируются метаданные набора подключаемых табличных пространств, DATAFILES=(…) – список, определяющий имена и место расположения подключаемых файлов данных, TABLESPACES=(TS_XXX) – список табличных пространств. Если параметр не задан, то список берется из файла экспорта. Если задан, то сверяется со списком, содержащимся в файле экспорта (в случае несовпадения будет выдано сообщение об ошибке). TTS_OWNERS=( XXXCORE) – список схем, которым принадлежат объекты в подключаемых табличных пространствах. Если параметр не задан, то список берется из файла экспорта. Если задан, то сверяется со списком, содержащимся в файле экспорта (в случае несовпадения будет выдано сообщение об ошибке). FROMUSER=( XXXCORE), TOUSER=( XXXCORE) – имена исходных и соответствующих им целевых схем.<br>
Если импорт завершен успешно, можно проверять наличие данных на целевой БД. 