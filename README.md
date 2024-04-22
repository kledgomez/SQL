# SQL
SQL tasks
SQL Academy.

1. Вывод  уникальнх имён (first_name) студентов из таблицы Student:
select distinct first_name from Student;
![image](https://github.com/kledgomez/SQL/assets/89851642/4f7519fd-b483-451b-93a5-7c81c95c10b3)

2. Выведите идентификаторы товаров (поле good) из таблицы Payments, стоимость которых больше 2000 единиц. Стоимость товара хранится в поле unit_price.
select good from Payments  where unit_price > 2000 ;
![image](https://github.com/kledgomez/SQL/assets/89851642/4b14e4ab-237a-4b3c-905d-475c4060728f)

3. Выведите информацию о студентах из таблицы Student, у которых год рождения соответствует одному из перечисленных: 2000, 2002 и 2004.
SELECT * FROM Student
WHERE YEAR(birthday) IN ('2000', '2002', '2004');
![image](https://github.com/kledgomez/SQL/assets/89851642/81677c24-7d24-4226-9c70-20f89a791517)

