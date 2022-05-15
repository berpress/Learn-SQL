Рассмотрим запросы **SELECT**

1) Сделаем запрос на полную выборку пользователей 
```SQL
SELECT * FROM users;
```

результат 

```SQL
	"Alexander"	"Ivanov"
	"Maxim"	"Petrov"
	"Maria"	"Lukashina"
	"Igor"	"Semenov"
	"Sveta"	"Ivanova"
	"Aidar"	"Mahmutov"
```

2) Выведем только имя 
```SQL
SELECT name FROM users;
```
результат 

```SQL
	"Alexander"
	"Maxim"
	"Maria"
	"Igor"
	"Sveta"
	"Aidar"
```

3) **DISTINCT** позволяет нам вывести уникальные строки. У нас есть сотрудники, которые живут
в городе "Kazan" (таблица user_address). Попробуем вывести уникальные города

```SQL
SELECT DISTINCT city FROM user_address;
```

результат 

```SQL
"NY"
"Moscow"
"Krakov"
"Kazan"
```
Город "Kazan" отоброзился один раз

4) **COUNT** возвращающая количество записей (строк) таблицы. Вычислим количество городов в таблице user_address WHERE
```SQL
SELECT COUNT(city) FROM user_address;
```
результат

```SQL
5
```

5) **WHERE** оператор для дополнительного выбора. Попробуем выбрать всех сотрудников, у кого зарплата больше 150000 рублей
```SQL
SELECT * FROM user_work WHERE salary > 150000;
```

результат

```SQL
1	1	"QA Lead"	220000	"true"
2	2	"C++ developer"	380000	"true"
5	5	"JS developer"	238000	"true"
6	6	"Project owner"	500000	"true"
```

6. **AND OR** предикаты языка SQL, служащие для создания логических выражений. Выберем всех сотрудников, которые получают меньше 150000 и не работают в данный момент (is_working)
```SQL
SELECT * FROM user_work WHERE salary < 150000 AND is_working is FALSE;
```

результат

```SQL
3	3	"QA manual"	80000	false
```

7) **MIN MAX AVG** Минимальное, максимальное и среднее значение. Посчитаем среднюю зарплату в фирме. 
```SQL
SELECT AVG(salary) FROM user_work WHERE is_working is TRUE;
```

результат

```SQL
289600.000000000000
```

8) **LIKE** устанавливает соответствие символьной строки с шаблоном. Выберем всех Ивановых
```SQL
SELECT * FROM users WHERE surname LIKE '%Ivano%';
```
результат
```SQL
1	"Alexander"	"Ivanov"
5	"Sveta"	"Ivanova"
```

9) **LIMIT** позволяет вывести указанное число строк из таблицы
```SQL
SELECT * FROM users LIMIT 2;
```

результат

```SQL
1	"Alexander"	"Ivanov"
2	"Maxim"	"Petrov"
```

10) **GROUP BY** используется для объединения результатов выборки по одному или нескольким столбцам. Сгруппируем города

```SQL
SELECT city FROM user_address GROUP BY(city);
```

результат

```SQL

"NY"
"Moscow"
"Krakov"
"Kazan"
```

11) **HAVING** является указателем на результат выполнения агрегатных функций (COUNT, MIN, MAX, AVG)
```SQL
SELECT SUM(salary) FROM user_work GROUP BY(salary) HAVING SUM(salary) > 200000; 
```
результат

```SQL
500000
380000
220000
238000
```