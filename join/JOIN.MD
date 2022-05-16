Рассмотрим запросы **JOIN**

1) **INNER JOIN** формирует таблицу из записей двух или нескольких таблиц. Каждая строка из первой (левой) таблицы, сопоставляется с каждой строкой из второй (правой) таблицы, после чего происходит проверка условия. 
Попробуем теперь соеденить две таблицы пользователей и рабочей информации о них 

```SQL
SELECT users.name, users.surname, user_work.position, user_work.salary FROM users INNER JOIN user_work ON users.id = user_work.user_id; 
```

результат 
```SQL
"Alexander"	"Ivanov"	"QA Lead"	220000
"Maxim"	"Petrov"	"C++ developer"	380000
"Maria"	"Lukashina"	"QA manual"	80000
"Igor"	"Semenov"	"Tech writer"	110000
"Sveta"	"Ivanova"	"JS developer"	238000
"Aidar"	"Mahmutov"	"Project owner"	500000
```
2) **LEFT JOIN** Команда используются для связывания таблиц по определенным полям связи. Что бы проверить, как работает оператор, добавим в таблицу пользователей нового сотрудника

```SQL
INSERT INTO users (id, name, surname) VALUES
(7,'Ekaterina', 'Ivshina');
```

теперь выполним запрос LEFT JOIN, узнаем в каких городах живут сотрудники
```SQL
SELECT users.name, user_address.city FROM users LEFT JOIN user_address ON users.id=user_address.user_id;
```
 результат 
 
```SQL
"Alexander"	"Kazan"
"Maxim"	"NY"
"Maria"	"Moscow"
"Igor"	"Kazan"
"Sveta"	NULL
"Aidar"	"Krakov"
"Ekaterina"	NULL
```

новый добавленный пользователь 'Ekaterina' не имеет соответсвий в таблице user_addres, поэтому 
у данного пользователя проставился город **NULL** (у пользователя 'Sveta' город не был заполнен изначально)

3) **RIGHT JOIN** Команда используются для связывания таблиц по определенным полям связи. Сделаем аналогичный запрос, но с RIGHT JOIN

```SQL
SELECT users.name, user_address.city FROM users RIGHT JOIN user_address ON users.id=user_address.user_id;
```

результат 

```SQL
"Alexander"	"Kazan"
"Maxim"	"NY"
"Maria"	"Moscow"
"Igor"	"Kazan"
"Sveta"	NULL
"Aidar"	"Krakov"
```

Теперь же пользователь 'Ekaterina' не попала в выборку, так как данных в таблице user_address нет.