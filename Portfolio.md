# Task 6
## Subtask 1
11. Popełniłam błąd wpisując nazwisko Ani Miler – wpisałam Muler. Znajdź i zastosuj funkcję, która poprawi mój karkołomny błąd 🙈

```sql
update customers
set surname = 'Miler'
where customer_id = 3
```
![image](https://user-images.githubusercontent.com/63921367/220200505-c21ce45d-2a2f-4679-80e3-5346f624172b.png)

12. Pobrałam za dużo pieniędzy od klienta, który kupił w ostatnim czasie film o id 4. Korzystając z funkcji join sprawdź, jak ma na imię klient i jakiego ma maila. W celu napisania mu wiadomości o pomyłce fantastycznej szefowej.

```sql
select name, surname, email from customers
join sale on customers.customer_id = sale.customer_id
where sale.movie_id= 4
```
![image](https://user-images.githubusercontent.com/63921367/220200882-07c55450-ff64-4a26-85b7-fa880a1a171d.png)


13. Na pewno zauważył_ś, że sprzedawca zapomniał wpisać emaila klientce Patrycji. Uzupełnij ten brak wpisując: pati@mail.com

```sql
update customers
set email = 'pati@mail.com'
where customer_id = 4
```
![image](https://user-images.githubusercontent.com/63921367/220201070-9ef099ae-9e2c-40e1-8170-886fee48d3b4.png)

14. Dla każdego zakupu wyświetl, imię i nazwisko klienta, który dokonał wypożyczenia oraz tytuł wypożyczonego filmu. (wykorzystaj do tego funkcję inner join, zastanów się wcześniej, które tabele Ci się przydadzą do wykonania ćwiczenia).

```sql
select c.name, c.surname, m.title from customers as c
join sale as s
on c.customer_id=s.customer_id
join movies as m on m.movie_id = s.movie_id
```
![image](https://user-images.githubusercontent.com/63921367/220201128-b2b437d5-2048-4def-9127-f4743b7fe552.png)


15. W celu anonimizacji danych, chcesz stworzyć pseudonimy swoich klientów. - Dodaj kolumnę o nazwie ‘pseudonym’ do tabeli customer,- Wypełnij kolumnę w taki sposób, aby pseudonim stworzył się z dwóch pierwszych liter imienia i ostatniej litery nazwiska. Np. Natalie Pilling → Nag

```sql
alter table customers
add pseudonim varchar(20)
update customers
set pseudonim = concat(left(customers.name, 2), right(customers.surname, 1))
```
![image](https://user-images.githubusercontent.com/63921367/220201288-671f72d8-2135-4d0d-8dde-c768c6b0dbf1.png)


16. Wyświetl tytuły filmów, które zostały zakupione, wyświetl tabelę w taki sposób, aby tytuły się nie powtarzały.

```sql
select title, count(*) as ilosc from movies m
join sale s on s.movie_id = m.movie_id
group by title
```
![image](https://user-images.githubusercontent.com/63921367/220201467-df35939d-74d6-4d81-83ad-cc41086968e3.png)


17. Wyświetl wspólną listę imion wszystkich aktorów i klientów, a wynik uporządkuj alfabetycznie. (Wykorzystaj do tego funkcji UNION)

```sql
select name from customers
union
select name from actors
order by name asc
```
![image](https://user-images.githubusercontent.com/63921367/220201535-d3f999b8-4baf-4cb9-a2fc-7f65a6cae136.png)


18. Polskę opanowała inflacja i nasz sklepik z filmami również dotknął ten problem. Podnieś cenę wszystkich filmów wyprodukowanych po 2000 roku o 2,5 $ (Pamiętaj, że dolar to domyślna jednostka- nie używaj jej nigdzie).

```sql
alter table movies
update movies
set price = price + 2.5
where year_of_production > 2000
```
![image](https://user-images.githubusercontent.com/63921367/220201602-e2a280c4-927c-4efc-8120-f37f4342b2e4.png)


19. Wyświetl imię i nazwisko aktora o id 4 i tytuł filmu, w którym zagrał

```sql
select a.name, a.surname, m.title from actors a
join "cast" c on c.actor_id = a.actor_id
join movies m on m.movie_id = c.movie_id
where a.actor_id = 4
```
![image](https://user-images.githubusercontent.com/63921367/220201666-8be7a29d-80a5-4a2c-a531-9ac3a2f399cb.png)


20. A gdzie nasza HONIA!? Dodaj do tabeli customers nową krotkę, gdzie customer_id = 7, name = Honia, surname = Stuczka-Kucharska, email = honia@mail.com oraz pseudonym = Hoa

```sql
insert 
into customers(customer_id, name, surname, email, pseudonim)
values (7,'Honia','Stuczka-Kucharska', 'honia@mail.com', 'Hoa')
```

![image](https://user-images.githubusercontent.com/63921367/220201741-c59aa84b-705c-45c8-afd1-10b10f081d81.png)

## Subtask 2
## Subtask 3
