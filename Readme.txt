Лабораторная работа № 2
1.	Определить, кто из клиентов покупал настольные лампы (Desc lamp) 
2.	Определить названия фирм, производящих Бронзовые скульптуры (Bronze sculpture).
3.	Определить, кто из клиентов покупал товар производства фирмы Лампы Лама (Lampy Lama).
4.	Определить имена сотрудников, продававших товары, произведенные в Перу (Peru).
5.	Определить фамилии клиентов, покупавших товары у сотрудника Родни Джонса.

Примеры:
Клиенты из Японии:
select c.country from country c, customer cu
where cu.c_name='Wotaib' 
and c.cn_id=cu.cn_id;

select c.country from country c join customer cu
on c.cn_id=cu.cn_id
where cu.c_name='Wotaib';

select country from country
where cn_id=(select cn_id from customer
where c_name='Wotaib');

В какой стране производятся свмтера:
select c.country
from country c, manufact m, product p
where p.p_desc='Sweater' and
c.cn_id=m.cn_id and m.m_id=p.m_id;

select country
from country c join manufact m
on c.cn_id=m.cn_id join  product p
on m.m_id=p.m_id
where p.p_desc='Sweater';

select country from country 
where cn_id in(select cn_id from manufact
where m_id in(select m_id from product
where p_desc='Sweater'));

Кто продавал настольные лампы
select distinct s.sp_name
from product p, sale sa, sperson s
where p.p_desc='Desc lamp' and
p.p_id =sa.p_id and s.sp_id=sa.sp_id;

select distinct s.sp_name
from sperson s join sale sa
on s.sp_id=sa.sp_id join product p
on p.p_id=sa.p_id
where p.p_desc='Desc lamp';

select sp_name from sperson where sp_id in
(select sp_id from sale where p_id in
(select p_id from product 
where p_desc='Desc lamp')); 

Кто продавал товары из Перу клиентам из Японии
select distinct s.sp_name 
from country c1, country c2, customer cu,
manufact m, product p, sale sa, sperson s
where c1.country='Japan' and c2.country='Peru'
and s.sp_id=sa.sp_id and p.p_id=sa.p_id
and p.m_id=m.m_id and m.cn_id=c2.cn_id
and cu.c_id=sa.c_id and cu.cn_id=c1.cn_id;

select sp_name from sperson where sp_id in
(select sp_id from sale where c_id in
(select c_id from customer where cn_id=
(select cn_id from country where country='Japan'))
and p_id in(select p_id from product where m_id in
(select m_id from manufact where cn_id=
(select cn_id from country where country='Peru'))));





