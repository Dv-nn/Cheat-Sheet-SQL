# Шпаргалка SQL  

## *Типы данных*  
![Типы данных SQL](https://github.com/Dv-nn/Cheat-Sheet-SQL/blob/main/img/type.PNG)   

Нулевое значение (NULL) — это значение поля, которое является пустым (не имеющего значения).

## *Таблица и данные в SQL*     
CREATE - создание базы данных   
> CREATE DATABASE databasename  

BACKUP DATABASE - полная резервная копия  
> BACKUP DATABASE databasename   
> TO DISK = 'filepath'   

###  Работа с таблицами     
CREATE TABLE - создание таблицы  
> CREATE TABLE table_name (  
> column1 datatype,  
> column2 datatype,  
> ....  
> ) 
 
ALTER - добавление, удаление или изменение столбцов в существующей таблице  
> ALTER TABLE table_name  
> ADD column_name datatype 

AUTO INCREMENT - автоматически генерирует уникальное число при вставке новой записи в таблицу  
> ALTER TABLE Persons AUTO_INCREMENT=100  

DROP TABLE - удаление таблицы  

CREATE INDEX - для более быстрого извлечения данных из базы данных, чем в других случаях   
> CREATE INDEX index_name  
> ON table_name (column1, column2, ...)  

### Ограничения  
Ограничения (constraints) — это правила, которые используются для ограничения данных.   
Ограничения могут устанавливаться как на уровне колонки, так и на уровне таблицы.  
> NOT NULL - столбец не может иметь нулевое значение        
> UNIQUE - все значения в столбце будут разными        
> PRIMARY KEY - уникально идентифицирует каждую строку в таблице        
> FOREIGN KEY - идентифицирует строку/запись в другой таблице        
> CHECK - все значения в столбце удовлетворяют определенному условию          
> DEFAULT - задает значение по умолчанию для столбца             
> INDEX - для быстрого создания и извлечения данных из базы данных        

###  Вставка и изменение данных  
INSERT INTO - вставка новых записей в таблицу   
> INSERT INTO table_name  
> VALUES (value1, value2, value3, ...)  

UPDATE - изменение существующих данных    
> UPDATE table_name  
> SET column1 = value1, column2 = value2, ...  
> WHERE condition  

DELETE  - удаление данных  
>DELETE FROM table_name WHERE condition  
___  
## *Запросы к данным*  
### Запрос данных 
SELECT - используется для выбора данных из базы данных   
> SELECT column1, column2, ...  
> FROM table_name 
  
- SELECT MIN() и MAX() - возвращает наименьшее/наибольшее значение выбранного столбца  
> SELECT MIN(column_name)/SELECT MAX(column_name)
> FROM table_name
> WHERE condition 
   
- SELECT COUNT(), AVG() и SUM() - возвращает количество строк, соответствующих заданному критерию/среднее значение/общую сумму  
> SELECT COUNT(column_name)  
> FROM table_name  
> WHERE condition 
 
- SELECT DISTINCT - для возврата только определенных значений  
> SELECT DISTINCT column1, column2, ...  
> FROM table_name  
    
- SELECT INTO - копирует данные из одной таблицы в новую    
> SELECT column1, column2, column3, ...  
> INTO newtable   
> FROM oldtable  
> WHERE condition

- INSERT INTO SELECT - копирует данные из одной таблицы и вставляет их в другую таблицу  
> INSERT INTO table2 (column1, column2, column3, ...)  
> SELECT column1, column2, column3, ...  
> FROM table1  
> WHERE condition   
 
CASE - проходит через условия и возвращает значение, когда выполняется первое условие  
> SELECT column1  
>  CASE  
>   WHEN condition1 THEN result1  
>   WHEN condition2 THEN result2  
>   WHEN conditionN THEN resultN  
>  ELSE result  
> END  
> FROM table1    
 
FROM - из какой таблицы(таблиц) извлекаем данные  
 
WHERE - для извлечения только тех записей, которые удовлетворяют заданному условию   
` + AND/OR/NOT - спользуются для фильтрации записей на основе более чем одного условия `   
 > SELECT column1, column2, ...  
 > FROM table_name  
 > WHERE condition AND condition2 AND condition3 ...  
В выражении WHERE используются следующие операторы:  
 - BETWEEN - значения в заданном диапазоне  
 > SELECT column_name(s)  
 > FROM table_name  
 > WHERE column_name BETWEEN value1 AND value2  
 - LIKE - поиск шаблона   
  > SELECT column1, column2, ...  
  > FROM table_name  
  > WHERE columnN LIKE pattern  
 - IN - чтобы указать несколько возможных значений для столбца  
 > SELECT column_name(s)
 > FROM table_name    
 > WHERE column_name IN (value1, value2, ...)  
  
ORDER BY - сортируем данные в порядке возрастания или убывания    
`+ASC - по умолчанию(в порядке возрастания)`      
`+DESC - по убыванию`    
> SELECT column1, column2, ...    
> FROM table_name  
> ORDER BY column1, column2, ... ASC|DESC  

LIMIT - ограничиваем количество выводимых строк 
> SELECT column_name(s)    
> FROM table_name  
> WHERE condition  
> LIMIT number  
 
### Объединение данных из нескольких таблиц   
JOIN - объединение данных из двух или более таблиц  
> SELECT column_name(s)  
> FROM table1  
> INNER JOIN table2 / LEFT JOIN table2 / RIGHT JOIN table2 / FULL OUTER JOIN table2   
> ON table1.column_name = table2.column_name 
 
UNION - объединение результирующего набора из двух или более заявлений SELECT  
> SELECT column_name(s) FROM table1  
> UNION / UNION ALL  
> SELECT column_name(s) FROM table2 
 
### Группировки  
GROUP BY - группировать данные 
> SELECT column_name(s)  
> FROM table_name  
> WHERE condition  
> GROUP BY column_name(s)  
> ORDER BY column_name(s) 
 
HAVING - фильтровать данные, полученные на основе группировки 
> SELECT column_name(s)  
> FROM table_name  
> WHERE condition  
> GROUP BY column_name(s)  
> HAVING condition  
> ORDER BY column_name(s)   
    
### Подзапросы  
ANY  - возвращает true, если какое-либо из значений подзапроса удовлетворяет условию  
ALL - возвращает true, если все значения подзапроса удовлетворяют условию 
> SELECT column_name(s)  
> FROM table_name  
> WHERE column_name operator ANY / ALL  
> (SELECT column_name FROM table_name WHERE condition  
  
EXISTS - для проверки наличия любой записи в подзапросе  
> SELECT column_name(s)  
> FROM table_name  
> WHERE EXISTS  
> (SELECT column_name FROM table_name WHERE condition)  
 
### Представления - псевдонимы для запросов SELECT    
> SELECT column_name AS alias_name    
> FROM table_name      

### Поиск данных в таблице 
Вывод ограниченного набора строк  
> SELECT * FROM table  
> WHERE ROWNUM <= 5    

Поиск по таблицам в существующей схеме / по всем доступным схемам       
> SELECT table_name FROM user_tables / all_tables       

Поиск по полям и таблицам в существующей схеме / по всем доступным схемам       
> SELECT table_name FROM user_tab_columns / all_tab_columns  

Поиск по всем объектам базы данных        
> SELECT * FROM all_objects  
> WHERE object_type = 'table'  

Просмотр даты создания и изменения таблицы  
> SELECT object_name, created, last_ddl_time  

Искать комментарии / привязать поиск к полям таблицы  
> SELECT * FROM all_tab_comments / all_col_comments       

___  
## *Grant и Revoke - выдача и отзыв привилегий на таблицу*    
Выдача привилегий  
> GRAND select ON table_1 TO cheme_name 
or    
> GRAND all ON table_1 TO cheme_name  

Отзыв привилегий    
> REVOKE select ON table_1 FROM cheme_name  

Какие привилегии выданы    
> SELECT * FROM dba_tab_privs  

___
## *CREATE VIEW - виртуальная таблица, основанная на результирующем наборе инструкции* 
Представление доступно для пользователя как таблица, но само оно не содержит данных, а извлекает их из таблиц в момент обращения к нему  
> CREATE VIEW view_name AS  
> SELECT column1, column2, ...  
> FROM table_name  
> WHERE condition 

Удаление  
> DROP VIEW view_name  
___ 
## *Дата*  
`SELECT * FROM Orders WHERE OrderDate='2008-11-11' `
  
> DATE - формат YYYY-MM-DD  
> DATETIME - формат: YYYY-MM-DD HH:MI:SS  
> SMALLDATETIME - формат: YYYY-MM-DD HH:MI:SS  
> TIMESTAMP - формат: уникальное число 
___ 
## *Хранимая процедура - код, который можно использовать повторно*  
> CREATE PROCEDURE SelectAllCustomers  
> AS  
> SELECT * FROM Customers  
> GO  
> EXEC SelectAllCustomers  
___
## *Комментарии*  
`-- Однострочный комментарий`    
`/* Многострочный    
комментарий */ `    
___  
## *Функции систем управления базами данных*  
+ Функции для обработки текста  
> LEFT()	отбирает символы в тексте слева    
> RIGHT()	отбирает символы в тексте справа    
> MID()	отбирает символы с середины текста  
> UCase()	переводит символы в верхний регистр  
> LCase()	переводит символы в нижний регистр  
> LTrim()	удаляет все пустые символы слева от текста  
> RTrim()	удаляет все пустые символы справа от текста  
> Trim()	удаляет все пустые символы с обеих сторон текста  

+ Функции для обработкт чисел  
> SQR()	возвращает корень квадратный указанного числа    
> ABS()	возвращает абсолютное значение числа     
> EXP()	возвращает экспоненту указанного числа    
> SIN()	возвращает синус указанного угла    
> COS()	возвращает косинус указанного угла    
> TAN()	возвращает тангенс указанного угла  
    
+ Функции для обработки даты и времени 
> DatePart()	возвращает часть даты: год, квартал, месяц, неделя, день, час, минуты, секунды    
> Year(), Month()	возвращает год и месяц соответственно  
> Hour(), Minute(), Second()	возвращает час, минуты и секунды указанной даты  
> WeekdayName()	возвращает название дня недели  

+ Статические функции 
> COUNT()	возвращает число строк в таблице или столбце    
> SUM()	возвращает сумму значений в столбце    
> MIN()	возвращает наименьшее значение в столбце    
> MAX()	возвращает наибольшее значение в столбце    
> AVG()	возвращает среднее значение в столбце      
___  
## Оконные фукции 
> SELECT  
> Название функции (столбец для вычислений)   
> OVER (  
      > PARTITION BY столбец для группировки  
      > ORDER BY столбец для сортировки  
      > ROWS или RANGE выражение для ограничения строк в пределах группы  
      > )  
      
+ Агрегатные функции    
SUM – возвращает сумму значений в столбце  
COUNT — вычисляет количество значений в столбце (значения NULL не учитываются)  
AVG — определяет среднее значение в столбце  
MAX — определяет максимальное значение в столбце  
MIN — определяет минимальное значение в столбце  

+ Ранжирующие функции    
ROW_NUMBER – функция возвращает номер строки и используется для нумерации  
RANK — функция возвращает ранг каждой строки. В данном случае значения уже анализируются и, в случае нахождения одинаковых, возвращает одинаковый ранг с пропуском следующего значения  
DENSE_RANK — функция возвращает ранг каждой строки. Но в отличие от функции RANK, она для одинаковых значений возвращает ранг, не пропуская следующий  
NTILE – это функция, которая позволяет определить к какой группе относится текущая строка. Количество групп задается в скобках  

+ Функции смещения  
LAG или LEAD – функция LAG обращается к данным из предыдущей строки окна, а LEAD к данным из следующей строки. Функцию можно использовать для того, чтобы сравнивать текущее значение строки с предыдущим или следующим. Имеет три параметра: столбец, значение которого необходимо вернуть, количество строк для смещения (по умолчанию 1), значение, которое необходимо вернуть если после смещения возвращается значение NULL  
FIRST_VALUE или LAST_VALUE — с помощью функции можно получить первое и последнее значение в окне. В качестве параметра принимает столбец, значение которого необходимо вернуть  

+ Аналитические функции  
CUME_DIST — вычисляет интегральное распределение (относительное положение) значений в окне  
PERCENT_RANK — вычисляет относительный ранг строки в окне  
PERCENTILE_CONT — вычисляет процентиль на основе постоянного распределения значения столбца. В качестве параметра принимает процентиль, который необходимо вычислить (в этой статье я рассказываю как посчитать медиану, благодаря этой функции)  
PERCENTILE_DISC — вычисляет определенный процентиль для отсортированных значений в наборе данных. В качестве параметра принимает процентиль, который необходимо вычислить  
___
## *Согласованность данных в базе: транзакции и ограничения* 


___    
## *Повышение производительности запросов: индексы*   
___    
Примечание:  
[sqlfiddle](http://www.sqlfiddle.com) поиграть с запросами можно здесь  
[часть 1](https://habr.com/ru/articles/448072/) понимание джойнов сломано  
[часть 2](https://habr.com/ru/articles/450528/) попытка альтернативной визуализации  
[Упражнения по SQL](https://sql-ex.ru)  
[Интерактивный учебник по SQL](http://sql-tutorial.ru)  
