---
layout: page
title: Вопросы, которые задают претендентам на позицию Oracle DBA на собеседованиях
permalink: /database/beginning/questions-on-interview/
---

<h3>Вопросы, которые задают претендентам на позицию Oracle DBA на собеседованиях:</h3>>



СОБИРАЕМ ВОПРОСЫ!


<h3>Yandex:</h3>

<br/>

Вопрос 1:

<br/><br/>


На сервере СУБД на диске заканчивается место (используется Linux). Вы выяснили, что процесс lns1 начал по какой-то причине очень активно писать в файл <diagnostic_dest>/dbname/sid/trace/<sid>_lns1_<pid>.trc, из-за чего стало заканчиваться место на диске.
<br/><br/>
Каким образом средствами ОС освободить место на диске(процесс lns1 завершать (штатно или kill-ом ) нельзя)?



<br/>
<br/><br/>
Вопрос 2:
<br/><br/>
Могут ли две функции (stored functions) одного пользователя Oracle иметь одинаковые имена?


<br/>
<br/><br/>
Вопрос 3:
<br/><br/>


Тезисно опишите отличия взаимодействия СУБД Оракл (версии 10.2 и старше) с ОС Linux в случае использования AMM (Automatic Memory, начиная с версии 11.1) и ASMM (Automatic Shared Memory Management), СУБД Оракл и ОС Linux 64битные.


<br/>
<br/><br/>
Вопрос 4:
<br/><br/>


Есть БД Оракл размером 7 ТБ, в которой в том числе хранятся данные в 10 партиционированных таблицах (range partitions, 1 партиция — одни сутки) за 3 года. Вам необходимо поднять частичную копию этой БД, в которой присутствовали бы данные только за последний месяц. На сервере, где необходимо поднять БД-копию, места для полного восстановления исходной БД недостаточно.
<br/><br/>
Каким образом вы будете решать эту задачу?



<br/>
<br/><br/>
Вопрос 5:
<br/><br/>
Чем отличаются в плане выполнения запроса операции hash join от nested loops. какая выполняется быстрее, при каких условиях?


<br/>
<br/><br/>
Вопрос 6:
<br/><br/>


Дана PL/SQL-коллекция, объявленная следующим образом:

<br/><br/>

    declare
       type TNumList is varray(10) of number;
       lstN TNumList;
    ...


<br/>

 Перечислите, какие из 5-ти логических выражений истинны независимо от содержимого переменной lstN:

 lstN.Limit is not NULL

 lstN.First = 1 or lstN.First is NULL

 lstN.Trim is NULL

 Nvl(lstN.Last,0) = lstN.Count

 lstN.Prior(lstN.First) is NULL


<br/>
<br/><br/>
Вопрос 7:
<br/><br/>

Каким образом в 4-х узловом Real Application Cluster сделать так, чтобы задача, запускаемая с использованием dbms_scheduler в случае доступности всех узлов исполнялась только на 1 узле, в случае недоступности 1-го узла - на любом работоспособном.
