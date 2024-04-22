# SQL
SQL Academy tasks.

1. Вывод  уникальнх имён (first_name) студентов из таблицы Student:
 select distinct first_name from Student;
![image](https://github.com/kledgomez/SQL/assets/89851642/4f7519fd-b483-451b-93a5-7c81c95c10b3)

2. Выведите идентификаторы товаров (поле good) из таблицы Payments, стоимость которых больше 2000 единиц. Стоимость товара хранится в поле unit_price.
select good from Payments  where unit_price > 2000 ;
![image](https://github.com/kledgomez/SQL/assets/89851642/4b14e4ab-237a-4b3c-905d-475c4060728f)

3. Выведите информацию о студентах из таблицы Student, у которых год рождения соответствует одному из перечисленных: 2000, 2002 и 2004.
/SELECT * FROM Student
/WHERE YEAR(birthday) IN ('2000', '2002', '2004');
![image](https://github.com/kledgomez/SQL/assets/89851642/81677c24-7d24-4226-9c70-20f89a791517)

**Многотабличные запросы, JOIN. Внутреннее соединение INNER JOIN. Внешнее соединение OUTER JOIN.**

4.1. Объедините таблицы Class и Student_in_class с помощью внутреннего соединения по полям Class.id и Student_in_class.class. Выведите название класса (поле Class.name) и идентификатор ученика (поле Student_in_class.student).
select  Class.name,  Student_in_class.student
from  Class
inner join  Student_in_class on Class.id = Student_in_class.class;
![image](https://github.com/kledgomez/SQL/assets/89851642/8301fb74-05d1-48aa-92af-e2223497436a)

4.2. Дополните запрос из предыдущего задания, добавив ещё одно внутреннее соединение с таблицей Student.
Объедините по полям Student_in_class.student и Student.id и вместо идентификатора ученика выведите его имя (поле first_name).
select Class.name, first_name
from  Class inner join  Student_in_class 
on Class.id = Student_in_class.class
join Student on Student_in_class.student = Student.id;
![image](https://github.com/kledgomez/SQL/assets/89851642/8301fb74-05d1-48aa-92af-e2223497436a)

5. Выведите названия продуктов, которые покупал член семьи со статусом "son". Для получения выборки вам нужно объединить таблицу Payments с таблицей FamilyMembers по полям family_member и member_id, а также с таблицей Goods по полям good и good_id.
SELECT good_name FROM Payments join FamilyMembers on family_member = member_id join Goods on good = good_id
where status = 'son';
![image](https://github.com/kledgomez/SQL/assets/89851642/40939ade-07cc-47bc-a25f-216481b3722c)

7. Выведите идентификатор (поле room_id) и среднюю оценку комнаты (поле rating, для вывода используйте псевдоним avg_score), составленную на основании отзывов из таблицы Reviews.
Данная таблица связана с Reservations (таблица, где вы можете взять идентификатор комнаты) по полям reservation_id и Reservations.id.
select room_id, AVG(rating) as avg_score
from Reviews join Reservations 
on reservation_id = Reservations.id
Group by room_id;
![image](https://github.com/kledgomez/SQL/assets/89851642/69b5b5c4-1c58-482a-a4f3-d89efba6021a)

8. Выведите имя first_name и фамилию last_name каждого учителя из таблицы Teacher, а также количество занятий, в которых он был назначен преподавателем. Если преподаватель не был назначен ни на одно занятие, то выведите 0.
select first_name, last_name, count(s.teacher) as amount_classes from Teacher t 
left join Schedule s on t.id = s.teacher
group by first_name, last_name;
![image](https://github.com/kledgomez/SQL/assets/89851642/cf9804c6-1b75-4a24-8de5-a102175f0f75)

**LIMIT.**
9. Отсортируйте список компаний (таблица Company) по их названию в алфавитном порядке и выведите первые две записи.
select * from company
order by name
limit 2;
![image](https://github.com/kledgomez/SQL/assets/89851642/9ffca35f-2222-4f5e-acf7-e28026bbe062)

10.Выведите начало (поле start_pair) и окончание (поле end_pair) второго и третьего занятия из таблицы Timepair.
select start_pair, end_pair from Timepair limit 1, 2;
![image](https://github.com/kledgomez/SQL/assets/89851642/a0424dc2-7610-49f0-96ac-f5a44fae3890)

**Подзапросы. Многостолбцовые подзапросы.**

11. Выведите всю информацию о пользователе из таблицы Users, кто является владельцем самого дорого жилья (таблица Rooms).
select * from Users 
where id = (
select owner_id from Rooms
where price = (select max(price) from Rooms));
![image](https://github.com/kledgomez/SQL/assets/89851642/cc8da39c-7734-4cd8-81ff-eaf390433398)

12. Выведите названия товаров из таблицы Goods (поле good_name), которые ещё ни разу не покупались ни одним из членов семьи (таблица Payments).
13. SELECT good_name
FROM (select * from Goods) RDYTFUGIHOJPK
WHERE RDYTFUGIHOJPK.good_id NOT IN (SELECT good FROM Payments);
![image](https://github.com/kledgomez/SQL/assets/89851642/44041fb5-400d-459a-b552-bc6165b4088a)

14.  Строковые подзапросы. Выведите список комнат (все поля, таблица Rooms), которые по своим удобствам (has_tv, has_internet, has_kitchen, has_air_con) совпадают с комнатой с идентификатором "11".
select r_1.id, r_1.home_type, r_1.address, r_1.has_tv, r_1.has_internet, r_1.has_kitchen, r_1.has_air_con, r_1.price, r_1.owner_id, r_1.latitude, r_1.longitude from Rooms r_1
left join Rooms r_2 on r_2.id = 11
where r_1.has_tv = r_2.has_tv
and r_1.has_internet = r_2.has_internet
and r_1.has_kitchen = r_2.has_kitchen
and r_1.has_air_con = r_2.has_air_con;
![image](https://github.com/kledgomez/SQL/assets/89851642/66b3c08d-964a-4d8e-b944-1994784afe31)

15. Коррелированные подзапросы. С помощью коррелированного подзапроса выведите имена всех членов семьи (member_name) и цену их самого дорогого купленного товара.
Для вывода цены самого дорогого купленного товара используйте псевдоним good_price. Если такого товара нет, выведите NULL.
SELECT FamilyMembers.member_name, (
    SELECT MAX(Payments.unit_price)
    FROM Payments
    WHERE Payments.family_member = FamilyMembers.member_id
) AS good_price
FROM FamilyMembers;
![image](https://github.com/kledgomez/SQL/assets/89851642/c688c803-d302-41f7-a0a1-84b428489820)

**UNION. CASE. IF, IFNULL и NULLIF**

16. Выведите полные имена (поля first_name, middle_name и last_name) всех студентов и преподавателей.
SELECT first_name, middle_name, last_name  FROM Student
UNION
SELECT DISTINCT first_name, middle_name, last_name  FROM Teacher
![image](https://github.com/kledgomez/SQL/assets/89851642/6fde21e5-6caa-4e4b-88f1-b0ee5d5d68b7)

17. Из таблицы Reviews выведите идентификаторы отзывов (поле id) и их категорию: для рейтинга 4-5 проставьте категорию «positive», для 3 проставьте «neutral», а для 1-2 - «negative».
Для вывода категории рейтинга используйте псевдоним rating.
SELECT id, rating,
CASE
  WHEN SUBSTRING(rating, 1, INSTR(rating, '')) IN (4, 5) THEN "positive"
  WHEN SUBSTRING(rating, 1, INSTR(rating, '')) IN (1, 2) THEN "negative"
   WHEN SUBSTRING(rating, 1, INSTR(rating, '')) IN (3) THEN "neutral"
END AS rating
FROM Reviews
![image](https://github.com/kledgomez/SQL/assets/89851642/1d11a561-3c57-4581-bda0-2bd1bd5aae32)

18. Из таблицы Rooms выведите идентификаторы сдаваемых жилых помещений (поле id) и наличие телевизора в помещении: если телевизор присутствует выведите «YES», иначе «NO».
Для вывода наличия телевизора используйте псевдоним has_tv.
select id, has_tv,
if (has_tv = true, "YES", "NO") as has_tv
from Rooms;
![image](https://github.com/kledgomez/SQL/assets/89851642/1da0919a-4ea1-430d-b370-0b12fb739a3b)

19. Из таблицы Teacher выведите имена (поле first_name), отчества (поле middle_name) и фамилии (поле last_name) учителей. Если отчество у учителя отсутствует, выведите в поле middle_name значение «Empty».
select first_name,
    IFNULL (middle_name, "Empty") as middle_name,
last_name
from Teacher;
![image](https://github.com/kledgomez/SQL/assets/89851642/aa272849-97a7-4b2a-a6b8-8a5471f423bb)

** INSERT. UPDATE. DELETE**

20. Добавьте новый товар в таблицу Goods с именем «Table» и типом «equipment».
В качестве первичного ключа (good_id) укажите количество записей в таблице + 1.
insert into Goods (good_id, good_name, type)
values ((select count(*) +1 from Goods as a),'Table', (select good_type_id from GoodTypes
 where good_type_name ='equipment' ))
![image](https://github.com/kledgomez/SQL/assets/89851642/5c33fb39-506c-4ac7-bfa0-059e1182edf0)

21.Измените имя у "Wednesday Addams" на новое "Tuesday Addams".
UPDATE FamilyMembers
SET member_name = "Tuesday Addams"
WHERE member_name = "Wednesday Addams";
![image](https://github.com/kledgomez/SQL/assets/89851642/fb35443a-0644-4709-a8ce-821a4a1ad6c9)

22.1. Удалить запись из таблицы Goods, у которой поле good_name равно "milk"
delete Goods from Goods where good_name = "milk"
22.2. Измените запрос так, чтобы удалить товары (Goods), имеющие тип деликатесов (delicacies).
delete Goods FROM Goods JOIN GoodTypes ON
Goods.type = GoodTypes.good_type_id 
WHERE GoodTypes.good_type_name = "delicacies"
![image](https://github.com/kledgomez/SQL/assets/89851642/ce719459-912b-433d-bbeb-d4e35f63b498)

**ТИПЫ ДАННЫХ**
23. Выведите список цен всего доступного жилья (из таблицы Rooms), округлённых к ближайшему кратному 10-ти числу. Например, если цена равна "9676", то после округления она будет равна "9680".
Для вывода цены используйте псевдоним rounded_price.
SELECT ROUND(price, -1) as rounded_price from Rooms;
![image](https://github.com/kledgomez/SQL/assets/89851642/7dc9011f-101c-454f-93d5-635dc300d215)

24. Пропишите формат строки во втором аргументе функции STR_TO_DATE, чтобы функция корректно отработала и вернула дату, на основании переданной первым аргументом строки.
SELECT STR_TO_DATE('December 31, 2023', ' %M  %d, %Y') AS date;
![image](https://github.com/kledgomez/SQL/assets/89851642/e19f8ced-aefa-433b-bc89-5ff83dae47b8)

25. Выведите имена (поле member_name) и возраст для каждого человека из таблицы FamilyMembers.
Для вывода возраста используйте псевдоним age.
select member_name, TIMESTAMPDIFF(YEAR, birthday, NOW()) as age from FamilyMembers;
![image](https://github.com/kledgomez/SQL/assets/89851642/4597b3d6-41b9-4057-94b2-918025cf7009)

**Оконные функции. Партиции**
26. Из таблицы Rooms вывести поля home_type и price, а также добавить колонку min_price_by_type, в которой необходимо вывести минимальную стоимость жилья для текущего типа жилья (home_type). Для вычисления минимальной стоимости нужно использовать оконную функцию MIN.
SELECT home_type, price, 
min(price) 
OVER (
    PARTITION BY home_type
) as min_price_by_type
from Rooms
![image](https://github.com/kledgomez/SQL/assets/89851642/e8842b05-7dd0-46fd-b9f4-8d40382db321)

27. Из таблицы Rooms вывести id, home_type и price у всех жилых помещений, а также в отдельной колонке room_rank вывести ранг данного жилого помещения в его категории (home_type) по цене, используя для этого функцию DENSE_RANK так, чтобы самое дешёвое жилое помещение имело ранг 1, следующие за ним по цене — 2 и так далее.
select id, home_type, price,
DENSE_RANK() over (partition by home_type 
order by price) as 'room_rank' from Rooms;
![image](https://github.com/kledgomez/SQL/assets/89851642/983ffd45-dfcf-4d06-ac3b-2e4f3df0d917)

28. Дополните запрос так, чтобы найти разницу во времени между вылетами среди рейсов одной компании.
В качестве результирующей выборки выведите идентификаторы компаний (в поле company), время вылета их рейсов (в поле time_out) и время (в поле time_diff), прошедшее с предыдущего вылета в формате ЧЧ-MM-СС. Если это был первый рейс компании, то в поле time_diff нужно вывести "00:00:00".

SELECT 
    company,
    time_out,
    CASE
        WHEN ROW_NUMBER() OVER(PARTITION BY company order by time_out) = 1 THEN '00:00:00'
        ELSE TIMEDIFF(
            time_out,
            lag(time_out) OVER(partition by company order by time_out)
        )
    END AS time_diff
FROM Trip
![image](https://github.com/kledgomez/SQL/assets/89851642/32c90d6d-2d61-4ba7-b41c-e40bcbba3e5f)

**VIEW**
29. На основании таблицы Student создайте представление ViewStudent, содержащие только поля id, first_name и last_name.
create view ViewStudent as 
select id, first_name, last_name
from Student;
![image](https://github.com/kledgomez/SQL/assets/89851642/72ab61f9-bb12-4bed-983e-be21d502a66f)




