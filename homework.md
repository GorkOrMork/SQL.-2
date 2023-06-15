# Домашнее задание к занятию "SQL. Часть 2" - Вебер Сергей


### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

фамилия и имя сотрудника из этого магазина;
город нахождения магазина;
количество пользователей, закреплённых в этом магазине.


select s.store_id, count(c.customer_id) as "ФИО", city, concat(st.last_name, ' ', st.first_name) as "Количество покупателей"

from store s

join customer c on c.store_id = s.store_id

join address a on a.address_id = s.address_id

join city ci on ci.city_id = a.city_id

join staff st on st.store_id = s.store_id

group by s.store_id, ci.city_id, st.staff_id

having count(c.customer_id) > 301;

![image](https://github.com/GorkOrMork/SQL.-2/assets/109193124/be463320-e5eb-46a5-9431-518546a9c76b)


### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.


select count(film_id) as 'Количество фильмов'

from (select *, avg(length) over () as time from film) t

where time < length;

![image](https://github.com/GorkOrMork/SQL.-2/assets/109193124/bc4df069-af7e-4c76-852b-754e21ecdc98)


### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.


select date_format(p.payment_date, '%Y-%M') as Дата , (sum(p.amount )) as Наибольшая_сумма , count((p.rental_id )) as Количество_аренд

from payment p 

group by Дата

order by Наибольшая_сумма desc

limit 1;

![image](https://github.com/GorkOrMork/SQL.-2/assets/109193124/6f514e79-4f1c-4601-9dfb-67d01cafda0d)


