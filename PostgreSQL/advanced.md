Вопрос 1. 
Существует структура базы данных. Какая команда на месте [...] позволит создать новую запись в таблице role?

--структура базы данных
create type permission as enum (
    'read',
    'write',
    'execute'
);
create table role(
    ...
    permissions permission[],
    ...
);
-- Запрос
Insert into role(...) values (..., [...],...);

Ответы:
1. {"read"} as permission[]
2. "read"
3. {permission.read}
4. array['read']
5. array['read']::permission[]

Выбран 5 ответ.


Вопрос 2. 
Какое утверждение относительно генерируемых колонок является ложью?

Ответы:
1. Выражение для вычисления генерируемой колонки не может содержать ссылки на большинство системных таблиц
2. Для stored генерируемых колонок значение сохраняется в таблице и не пересчитывается при каждом обращении
3. Значение генерируемой колонки нельзя установить вручную через INSERT или UPDATE
4. Генерируемые колонки могут ссылаться на другие генерируемые колонки
5. Генерируемые колонки бывают двух типов: stored и virtual

Ответ 4 точно правильный.


Вопрос 3. 
Имеется следующая структура представленная на изображении. Было решено во все существующие записи в таблице role добавить пермиссию 'read' так, чтобы не было дубликатов. Как этого достичь?

create type permission as enum ('read', 'write', 'execute', 'transfer','download'); 
create table role (
...
    permissions permission[],
    ...
);

Ответы: 
1. update table role alter column permissions = distinct( array_append(permissions, 'read'))
2. update role set permissions = array_append(permissions, 'read') where array_position(permission, 'read') is null
3. update role set permissions = array_append(permissions, 'demoMode') where permissions-> 'demoMode' is null
4. update role set permissions = array_append(permissions, 'read') where array_position(permission, 'read') is -1
5. update table role alter column permissions = array_append (permissions, 'read')

Выбран 2 ответ.
ChatGPT говорит, что возможно 4 (решили пока не проверять).

Вопрос 4. 
Вы создаёте временную таблицу temp_data, объединяя результаты двух запросов с несовместимыми типами данных (например, integer и text).
Таблица должна:
- Автоматически принимать структуру первого запроса.
- Сохранять дублирующиеся строки.
Какой подход нужно использовать?

create temporary table temp_data as
<оператор> select id, data from source1
<оператор> select id, info from source2;

Ответы: 
1. Использовать UNION, но предварительно привести типы данных в запросах
2. Использовать INTERSECT, чтобы сохранить только общие строки из обоих запросов
3. Использовать UNION ALL, но предварительно создать временную таблицу с заданными типами данных
4. Использовать UNION, чтобы исключить дубликаты и автоматически привести типы данных
5. Использовать UNION ALL, чтобы сохранить дубликаты и автоматически привести типы данных

Выбран 5 ответ, возможно верный был 3.


Вопрос 5.
У вас есть две связанные таблицы, где t2 использует значение из последовательности по умолчанию при обновлении ссылочной записи. Какие проблемы могут возникнуть при удалении записей из t1?

create sequence seq start with 1 increment by 1;
create table t1(
    id serial primary key
);
create table t2(
    id integer default nextval('seq') references t1(id) on delete set default
);

1. Удаление записи из t1 приведёт к изменению ссылающихся записей в t2 на значение по умолчанию из последовательности, что может нарушить логику приложения
2. Операция удаления возможна только при явном использовании CASCADE, даже если задано ON DELETE SET DEFAULT
3. Транзакция с операцией удаления завершится с ошибкой, если в таблице t2 есть строки, ссылающиеся на удаляемую запись в t1
4. Удаление завершится успешно, но строки в t2, ссылающиеся на удалённые записи, станут недействительными, требуя дополнительной проверки
5. Если nextval('seq') возвращает значение, отсутствующее в t1, операция удаления завершится с ошибкой

Ответ 5 точно правильный.


Вопрос 6.
В таблице some_table содержится 1 миллион записей. На колонке id создан индекс B-Tree, а на колонке пате - индекс GIN для полнотекстового поиска. Какой запрос оптимально использует индекс, если выборка данных составляет менее 0.1% от общего объёма?

create table some_table(
    id serial,
    name varchar(30),
    description text
);
create index some_table_id_index on some_table using btree(id);
create index some_table_name_gin_index on some_table using gin(to_tsvector('english', name));

Ответы: 
1. select * from some_table where to_tsvector('english', name) @@ to_tsquery('example');
2. select * from some_table where name like "A%';
3. select * from some_table where id > 500000 and id < 500010;
4. select * from some_table where id = 1000;
5. select * from some_table where description ilike '%example%';

Выбран 3 ответ, возможно верный был 4.


Вопрос 7.
Таблица logs содержит миллиарды записей и используется для анализа активности. Наиболее частый запрос к таблице выбирает записи по колонке user_id и фильтрует их по диапазону значений в колонке event_time. Какой индекс лучше всего подходит для ускорения выполнения этого запроса?
create table logs (
    id serial primary key,
    user_id integer not null,
    event_time timestamp not null,
    action text
);
-- Часто используемый запрос
select * from logs
where user_id = 12345 and event_time between '2024-01-01' and '2024-01-31';

Ответы:
1. create index logs_event_user_index on logs(event_time, user_id);
2. create index logs_user_event_index on logs(user_id, event_time);
3. create index logs_event_index on logs(event_tine);
4. create index logs_user_event_hash on logs using hash(user_id, event_tine);
5. create index logs_user_index on logs (user_id);

Выбран 2 ответ.

Вопрос 8.
Существует таблица some_table
class value
1 10
1 20
1 100
2 200
Запускаются две транзакции Т1 и Т2. Какой вид изолированности транзакции НЕ позволит исполнить commit?

-T1
SELECT SUM(value) FROM mytab WHERE class= 1;
INSERT INTO some_table(class, value) VALUES (2, 30);
COMMIT;
--T2
SELECT SUM(value) FROM mytab WHERE class = 2;
INSERT INTO some_table(class, value) VALUES (1, 380);
COMMIT;

Ответы:
1. repeatable read
2. serializable
3. read uncommited
4. read commited
5. snapshot

Выбран 2 ответ.

Вопрос 9.
B PostgreSQL вы создаёте индекс в транзакции над таблицей users. Во время выполнения этой транзакции другая транзакция пытается выполнить одну из следующих команд над той же таблицей. Какая команда выполнится без конфликтов?

-- Первая транзакция
begin;
create index idx_users_name on users(name);
-- Вторая транзакция
<выбранная команда>;

Ответы: 
1. select * from users where id = 1000 for update;
2. create index concurrently idx_users_email on users(email);
3. select * from users;
4. insert into users(name) values ('Alice');
5. vacuum users;

Выбран 3 ответ.


Вопрос 10.
Какие утверждения о следующем запросе правдивы?

create materialized view some_view as select * from some_table order by id desc with no data

Ответы: 
1. Для представления some_view можно создать индекс
2. Возможна операция вставки в представление some_view
3. Так как использовалось выражение select*, при модификации таблицы some_table изменятся и колонки в преставлении some_view
4. Возможна операция refresh materialized view concurrently some_view
5. Чтение возможно сразу после создания представления some_view

Выбран 1 ответ.
Claude предлагает 4 (пока не проверяли).


Вопрос 11. 
У вас есть рабочая база данных с высокой нагрузкой и её копия. Вы хотите проанализировать
производительность запроса, чтобы исключить влияние нагрузки на результаты анализа. Какую команду следует использовать для тестирования на копии базы данных?

1. explain
2. explain (analyze, buffers)
3. pgbench для эмуляции нагрузки и затем использовать explain analyze
4. explain analyze
5. Выполнить запрос несколько раз и взять среднее время выполнения.

Выбран 2 ответ.


Вопрос 12.
В таблице orders содержится 1 миллион записей. На колонке customer_id есть индекс B-Tree. Вы выполняете следующий запрос с фильтрацией по customer_id и выбираете 90% строк. Какой тип сканирования таблицы будет использован планировщиком PostgreSQL?

create table orders (
    order_id serial primary key,
    customer_id integer not null,
    order date date,
    total amount numeric
);
-- Индекс
create index idx_orders_customer_id on orders(customer_id);
-- Запрос
explain select from orders where customer_id 900000;

Ответы:
1. bitmap index scan
2. seq scan
3. bitmap heap scan
4. index only scan
5. index scan

Выбран 2 ответ.


Вопрос 13.
Существует таблица, представленная на изображении. В эту таблицу сохраняются данные, журналирующие некоторые действия. После очередного релиза частота вставки записей, где action = 'login', возросла в десять раз. Оперативно релиз починить не удается, но есть доступ к базе данных. Было решено временно не вставлять данные, где action='login', сохранив уже существующие записи.
Как этого достичь?

create table action_log(
id serial,
action varchar,
description text
);

Ответы:
1. Создать before insert trigger, запрещающий login'
2. Создать instead of trigger, запрещающий login'
3. Создать представление с условием: where action != login'
4. Создать after insert trigger, удаляющий вставленную строку
5. Создать constraint на колонку action, запрещающий login'

Выбран 1 ответ.
ChatGPT говорит, что возможно верный ответ 5 (пока не проверяли).

Вопрос 14.
В PostgreSQL пользователь manuel должен получить полный доступ к таблице kinds. Следующая команда выполнена другим пользователем. Какой будет результат выполнения команды, если исполняющий пользователь не является суперпользователем и не является владельцем таблицы?
GRANT ALL PRIVILEGES ON kinds TO manuel;

ответы:
1. manuel получит все права, которые есть у исполнителя команды на таблицу kinds
2. Команда завершится ошибкой, так как исполнитель команды не является владельцем таблицы
3. manuel получит доступ только на чтение таблицы kinds, если исполнитель команды обладает таким правом
4. Права на таблицу kinds будут изменены только для схемы, в которой она находится, но manuel доступ не получит
5. manuel получит полный доступ к таблице kinds, включая возможность передавать права другим пользователям

Выбран 2 ответ.


Вопрос 15.
По мере продвижения бизнеса росло количество запросов к бд, а именно возросло в несколько раз количество запросов на записть при том же уровне запросов на чтение и повысилось требование к отказоустойчивости
какими методиками можно воспользоваться для поддержания работоспособностьи сервиса с учетом того, что запросов по ключу большинство?
ответы:
1.вертикальное шардирование
2.горизонтальное шардирование
3.репликация вместе с вертикальным шардированием
4.репликация
5.репликация вместе с горизонтальным шардированием

Выбран 5 ответ.


12 правильных ответов из 15


06.10 (12 правильных ответов из 15)
Вопрос 16.
В таблице profiles поле skills — массив строк (text[]). Ваша задача — добавить навык 'sql' всем пользователям, у кого он ещё не указан в массиве. Какой SQL-запрос справится с этим корректно?

Ответы:
1. update profiles set skills = array['sql']
2. update profiles set skills = skills + array['sql']
3. update profiles set skills = array_cat(skills, 'sql')
4. update profiles set skills = skills || array['sql']
5. update profiles set skills = array_append(skills, 'sql') where not 'sql' = any(skills)

Выбран 5 ответ.


Вопрос 17.
В чём потенциальная проблема этого запроса?

select count(*)
from orders o
join order_items i on o.id = i.order_id

Ответы:
1. Таблицы нужно объединить через подзапрос
2. COUNT(*) требует DISTINCT по умолчанию
3. JOIN не нужен при подсчёте заказов
4. COUNT(*) может посчитать дубликаты
5. Нельзя использовать JOIN без LIMIT

Выбран 4 ответ.


Вопрос 18.
Что произойдёт при выполнении этого запроса?

select *
from products
where id not in (select product_id from archive)

Ответы:
1. Вернёт только архивные товары
2. Вернёт товары, не попавшие в архив
3. Вернёт только товары с NULL
4. Удалит дубликаты из обеих таблиц
5. Ошибка: NOT IN не поддерживается

Выбран 2 ответ.


Вопрос 19.
Вы поддерживаете таблицу events (10 млн строк), в которой часто выполняются запросы:

select * from events where category = 'system' and created_at > now() - interval '1 day'

Какой индекс лучше всего применить, чтобы ускорить эти запросы?

Ответы:
1. create unique index on events (id)
2. create index on events (category, created_at)
3. create index on events using hash (category)
4. create index on events (created_at, category)
5. create index on events (created_at)

Выбран 2 ответ.


Вопрос 20.
Выберите верное утверждение о запросе:

create materialized view some_view as select * from some_table order by id desc with no data

Ответы:
1. Представление перезапишется
2. Запрос выполнится и обновит базовую таблицу
3. Чтение возможно сразу после создания представления some_view
4. Произойдёт дублирование записей
5. INSERT будет транслирован в базу через RULE

Выбран 1 ответ.


Вопрос 21.
Что произойдёт при попытке вставить данные в представление?

insert into view_active_users (name, email) values ('Anna', 'a@example.com');

Ответы:
1. Представление перезапишется
2. Запрос выполнится и обновит базовую таблицу
3. Ошибка: представление только для чтения
4. Произойдёт дублирование записей
5. INSERT будет транслирован в базу через RULE

Выбран 3 ответ.


Вопрос 22.
Вы добавляете внешний ключ в таблицу orders, но операция ALTER TABLE выполняется медленно:

alter table orders
add constraint fk_customer
foreign key (customer_id) references customers(id);

Какой способ поможет оценить, почему операция занимает много времени?

Ответы:
1. Создать индекс на orders.customer_id и повторить команду
2. Временно удалить все данные из таблицы customers
3. Изменить тип customer_id на text
4. Удалить constraint и выполнить VACUUM
5. Использовать EXPLAIN (ANALYZE, VERBOSE) перед SELECT * FROM orders JOIN customers ON customer_id = id

Выбран 1 ответ.


Вопрос 23.
Какой риск возникает, если пользователь создаёт выраженный индекс на поле, к которому у него нет прав?

CREATE INDEX idx_lower_email ON users (lower(email));

Ответы:
1. Индекс будет создан, но использоваться не сможет
2. Индекс создастся, но выдаст ошибку при использовании функции
3. Запрос завершится ошибкой из-за отсутствия доступа к полю
4. Индекс создастся, но выдаст ошибку при обращении
5. PostgreSQL создаст индекс без проверки прав

Выбран 3 ответ.


Вопрос 24.
Вы настраиваете потоковую репликацию PostgreSQL. Какую строку конфигурации необходимо добавить в postgresql.conf на мастере?

Ответы:
1. replica_mode = on
2. enable_replication = true
3. hot_standby = yes
4. wal_level = replica
5. replication = streaming

Выбран 4 ответ.


06.10 (12 правильных ответов из 15)
Вот дополнительные вопросы и ответы по PostgreSQL:

**Вопрос: 25**
Какая разница между `TRUNCATE` и `DELETE FROM table`?

**Варианты ответов:**
- TRUNCATE быстрее и сбрасывает sequences
- DELETE можно откатить, TRUNCATE нельзя
- TRUNCATE работает только с пустыми таблицами
- DELETE освобождает место на диске, TRUNCATE нет
- Никакой разницы нет

**Правильный ответ:** TRUNCATE быстрее и сбрасывает sequences

---

**Вопрос: 26**
Что произойдет при выполнении этого запроса?

```sql
SELECT * FROM users
WHERE email LIKE '%@gmail.com'
ORDER BY created_at DESC
LIMIT 1000;
```

**Варианты ответов:**
- Индекс на email будет использован эффективно
- Index scan по created_at
- Full table scan, индекс на email не поможет
- Ошибка синтаксиса
- Запрос использует bitmap scan

**Правильный ответ:** Full table scan, индекс на email не поможет

---

**Вопрос: 27**
Для чего используется команда `VACUUM FULL`?

**Варианты ответов:**
- Освобождает место на диске, возвращая его ОС
- Обновляет статистику для планировщика
- Удаляет только dead tuples
- Создает резервную копию
- Перестраивает все индексы

**Правильный ответ:** Освобождает место на диске, возвращая его ОС

---

**Вопрос: 28**
Что делает следующая конфигурация?

```
work_mem = 256MB
```

**Варианты ответов:**
- Устанавливает общий лимит памяти для всех соединений
- Устанавливает лимит памяти на каждую операцию сортировки/хеширования
- Устанавливает размер shared_buffers
- Ограничивает размер временных таблиц
- Устанавливает максимальный размер запроса

**Правильный ответ:** Устанавливает лимит памяти на каждую операцию сортировки/хеширования

---

**Вопрос: 29**
В каком случае использование `UNION ALL` предпочтительнее `UNION`?

**Варианты ответов:**
- Когда нужно удалить дубликаты
- Когда дубликаты допустимы и важна производительность
- Когда объединяются более 2 таблиц
- UNION ALL всегда лучше
- Разницы нет

**Правильный ответ:** Когда дубликаты допустимы и важна производительность

---

**Вопрос: 30**
Что означает параметр `FILLFACTOR = 70` при создании таблицы?

**Варианты ответов:**
- Таблица будет заполнена на 70% случайными данными
- В каждой странице будет оставлено 30% свободного места для HOT updates
- Индексы будут занимать 70% от размера таблицы
- Автовакуум запустится при 70% заполнении
- Это коэффициент сжатия данных

**Правильный ответ:** В каждой странице будет оставлено 30% свободного места для HOT updates

---

**Вопрос: 31**
Какой из запросов эффективнее для проверки существования записи?

**Варианты ответов:**
- `SELECT COUNT(*) FROM users WHERE id = 1`
- `SELECT * FROM users WHERE id = 1`
- `SELECT EXISTS(SELECT 1 FROM users WHERE id = 1)`
- `SELECT id FROM users WHERE id = 1 LIMIT 1`
- Все одинаково эффективны

**Правильный ответ:** `SELECT EXISTS(SELECT 1 FROM users WHERE id = 1)`

---

**Вопрос: 32**
Что делает `ANALYZE` команда?

**Варианты ответов:**
- Удаляет dead tuples
- Обновляет статистику для планировщика запросов
- Показывает план выполнения запроса
- Проверяет целостность индексов
- Дефрагментирует таблицу

**Правильный ответ:** Обновляет статистику для планировщика запросов


06.10 (12 правильных ответов из 15)

**Вопрос: 33**
Вы добавили триггер на таблицу employees, чтобы логировать каждое изменение зарплаты:
create or replace function log_salary_update() returns trigger as $$
begin
   insert into salary_log(emp_id, old_salary, new_salary, changed_at)
   values (OLD.id, OLD.salary, NEW.salary, now());
   return NEW;
end;
$$ language plpgsql;
create trigger trg_salary_update
after update on employees
for each row
when (OLD.salary is distinct from NEW.salary)
execute function log_salary_update();

Как проверить, что триггер действительно сработал после выполнения:
update employees set salary = salary + 100 where department_id = 2;

1. Проверить таблицу employees_log
2. Посмотреть журнал ошибок PostgreSQL
3. Использовать pg_stat_statements
4. Выполнить explain update...
5. Выполнить select * from salary_log where changed_at > now() - interval '1 minute';

Выбрал ответ 1.


**Вопрос: 34**
В системе при удалении пользователя:
delete from users where id = 123;
наблюдается задержка. В таблице orders задано:
foreign key (user_id) references users(id) on delete cascade
Какой способ поможет оценить влияние каскадного удаления на производительность?

1. Использовать VACUUM FULL на обеих таблицах
2. Временно удалить каскадный внешний ключ
3. Выполнить EXPLAIN ANALYZE delete from users where id = 123
4. Перевести таблицу orders в UNLOGGED
5. Добавить ON DELETE SET NULL вместо CASCADE

Выбрал ответ 3.


**Вопрос: 35**
Нужно посчитать сумму зарплат по каждому отделу среди активных сотрудников. Какой запрос подойдёт?

1. select department, sum(salary) from employees where active = true group by department
2. select department, sum(salary) from employees group by salary
3. select department, sum(salary) from employees order by department
4. select department, sum(salary) group by department where active = true
5. select department, salary from employees group by department where active = true

Выбрал ответ 1.


**Вопрос: 36**
Какой параметр нужно включить в postgresql.conf на реплике, чтобы разрешить подключение в режиме только чтения?

1. read_only = true
2. hot_standby = on
3. standby_mode = on
4. slave_read = enable
5. stream_only = true

Выбрал ответ 2.


**Вопрос: 37**
Разработчик сообщает, что следующая команда INSERT в таблицу users(id primary key, name) иногда "подвисает" в продакшене:
insert into users (id, name) values (1, 'Ivan')
Какая команда подходит для анализа причины задержки выполнения?

1. analyze verbose users
2. select * from pg_stat_activity
3. explain analyze insert into users (id, name) values (1, 'Ivan')
4. vacuum analyze users
5. show transaction_isolation

Выбрал ответ 3.


**Вопрос: 38**
Что вернёт запрос?

select department, count(*)
from employees
group by department
having count(*) > 1;

1. Все департаменты
2. Ничего, если count(*) не указан в SELECT
3. Только NULL-записи
4. Только департаменты, где 1 сотрудник
5. Только департаменты, где 2 и более сотрудников

Выбрал ответ 5.


**Вопрос: 39**
Вы проектируете процедуру issue_payment(user_id int, amount numeric(5,2)), которая вносит запись в таблицу payouts(amount numeric(5,2)).
При высоких нагрузках в журнале стали появляться ошибки: numeric field overflow. Анализ показал, что иногда в amount передаётся 999.999. 
Какая доработка обеспечит устойчивое поведение при сохранении точности и отказоустойчивости?

1. Разрешить округление через set extra_float_digits = 0
2. Перед вызовом процедуры фильтровать значения на клиенте
3. Добавить в процедуру amount := round(least(amount, 999.99), 2) и логировать изменения
4. Обернуть INSERT в BEGIN ... EXCEPTION WHEN OTHERS THEN RAISE NOTICE
5. Изменить тип поля в таблице на numeric(7,4)

Выбрал ответ 5.


**Вопрос: 40**
Почему при уровне Repeatable Read может произойти ошибка сериализации?

BEGIN;
SELECT * FROM stock WHERE product_id = 1;
-- в другом сеансе UPDATE той же строки
SELECT * FROM stock WHERE product_id = 1;
COMMIT

1. Потому что другой сеанс изменил строку, нарушив консистентность
2. Потому что строки были удалены
3. Потому что product_id стал NULL
4. Потому что SELECT возвращает дубликаты
5. Потому что SELECT внутри транзакции вызывает COMMIT

Выбрал ответ 1.


**Вопрос: 41**
Какое влияние окажет добавление индекса на поле created_at в следующем запросе?
select * from logs where created_at >= now() - interval '1 day'

1. Ускорит выборку при большом объеме данных
2. Приведет к ошибке времени
3. Уменьшит размер таблицы
4. Увеличит количество возвращаемых строк
5. Увеличит количество операций записи

Выбрал ответ 1.


**Вопрос: 42**
Когда BRIN-индекс предпочтительнее B-Tree, несмотря на его меньшую точность?

1. Когда индекс используется для join'ов
2. Когда данные хранятся в jsonb
3. Когда нужно обеспечить уникальность значений
4. Когда выполняется поиск по точным строковым значениям
5. Когда таблица содержит большие объёмы данных, отсортированных по индексу

Выбрал ответ 2.


**Вопрос: 43**
Что вернёт запрос?

select name
from products
where price > (select avg(price) from products)

1. Ошибка: AVG нельзя использовать в подзапросе
2. Возвращает товары дороже среднего
3. Возвращает только товары с NULL
4. Сравнивает строки, а не числа
5. Возвращает товары дешевле всех

Выбрал ответ 2.


**Вопрос: 44**
У вас есть таблица users, где поле tags имеет тип text[]. В поле хранятся ключевые слова для фильтрации.
Вам нужно добавить новый тег vip только тем пользователям, у кого еще нет в массиве.
Какая из вставок выполнит задачу правильно?

1.update users set tags = array_cat(tags, vip)
2. update users set tags = tags || vip
3. update users set tags = tags + vip where vip not in tags
4. update users set tags = array_append(tags, vip) where not vip = any(tags)
5. update users set tags = vip where tags is null

Выбрал ответ 4.


**Вопрос: 45**
Что вернёт этот запрос?

select region, count(*)
from clients
group by region
having count(*) > 10

1. Все регионы без фильтрации
2. Только регионы с более чем 10 клиентами
3. Только регионы с NULL
4. Только 10 первых клиентов
5. Ошибка из-за HAVING

Выбрал ответ 2.


06.10 (12 правильных ответов из 15)
**Вопрос: 46**
Вы работаете над аналитическим отчётом. Нужно сгруппировать данные по категориям товаров и посчитать среднюю цену в каждой категории. Ваш коллега предложил следующий код:

select product, avg(price)
from goods
group by category

Однако этот код не выполняется. Какую доработку следует внести, чтобы получить корректный результат?

Варианты ответа:

1. select category, avg(price) from goods group by category
2. select product, avg(price) from goods
3. select avg(price) from goods group by price
4. select category, avg(price) from goods group by price
5. select product, price from goods group by category

Выбрал ответ 1.


**Вопрос: 47**
В таблице customers есть поле interests типа text[]. В некоторых строках уже есть значения вроде '{music, travel}'. Вам нужно добавить тег 'sports' только тем клиентам, у кого его нет. Ваш коллега предложил код:

update customers
set interests = interests || 'sports'
where not 'sports' = any(interests);

Какой из вариантов корректнее и безопаснее реализует задачу?

1. update customers set interests = array_append(interests, 'sports') where not 'sports' = any(interests)
2. update customers set interests = interests || 'sports' where interests is null
3. update customers set interests = 'sports' where interests @> array['sports']
4. update customers set interests = array_prepend('sports', interests)
5. update customers set interests = interests || array['sports'] where interests != 'sports'

Выбрал ответ 1.


**Вопрос: 48**
Почему следующий запрос может вернуть больше строк, чем таблица employees?

select *
from employees e
left join salaries s on e.id = s.emp_id

Варианты ответа:
1. Запрос должен содержать DISTINCT
2. LEFT JOIN всегда возвращает строки дважды
3. Нельзя использовать ON с LEFT JOIN
4. Только INNER JOIN гарантирует уникальность
5. В таблице salaries могут быть дубликаты по emp_id

Выбрал ответ 5.


**Вопрос: 49**
Почему следующий запрос может вернуть больше строк, чем таблица employees?

select *
from employees e
left join salaries s on e.id = s.emp_id

Варианты ответа:
1. Запрос должен содержать DISTINCT
2. LEFT JOIN всегда возвращает строки дважды
3. Нельзя использовать ON с LEFT JOIN
4. Только INNER JOIN гарантирует уникальность
5. В таблице salaries могут быть дубликаты по emp_id

Выбрал ответ 5.


**Вопрос: 50**
Вы хотите разделить таблицу users на два шарда по регионам. Какой шаг необходим при использовании PostgreSQL c Citus?

Варианты ответа:
1. Настроить шард-каталог вручную
2. Установить расширение citus
3. Создать индекс по колонке region
4. Выполнить select create_distributed_table('users', 'region')
5. Переместить все таблицы в новую базу

Выбрал ответ 4.

**Вопрос: 51**
Почему в PostgreSQL по умолчанию индекс по полю deleted_at не помогает ускорить запрос:
select * fren users where deleted at is null

Варианты ответа:
1. deleted at нужно делать PRIMARY KEY
2. Индекс работает только с числовыми полями
3. IS NULL нельзя использовать в WHERE
4. B-Tree индекс не включает NULL значения
5. NULL B PostgreSQL обрабатывается как О

Выбрал ответ 4.


**Вопрос: 52**
Вы добавили следующий триггер к таблице users, чтобы автоматически заполнять поле created_at, если оно не указано:

create or replace function fill_created_at() returns trigger as $$
begin
if NEW.created_at is null then
NEW.created_at := now();
end if;
return NEW;
end;
$$ language plpgsql;
create trigger trg_fill_created_at
before insert on users
for each row
execute function fill created_at();

Как убедиться, что триггер работает корректно?

Варианты ответа:
1. Удалить колонку created_at
2. Вставить запись с future timestamp
3. Посмотреть структуру таблицы через \d users
4. Выполнить ANALYZE на таблице
5. Вставить пользователя без указания created_at и проверить, что поле заполнено

Выбрал ответ 5.


**Вопрос: 53**

Разработчик применяет такие команды через интерфейс PostgreSQL, не отключая автокоммит:
1 update orders set status 'shipped' where id = 101;
2 update inventory set quantity - quantity
1 where item_id = 55;
На втором шаге происходит ошибка (например, отрицательное количество на складе).
К чему приведёт автокоммит в такой ситуации?

Варианты ответа:
1. Возникнет блокировка таблицы
2. Обе команды зафиксируются
3. Первая команда будет зафиксирована, вторую придётся корректировать вручную
4. Обе команды будут отменены
5. Только вторая команда не выполнится, первая откатится

Выбрал ответ 4.


**Вопрос: 54**
Почему запрос с != может не использовать индекс?
select * from payments where status != 'confirmed'

Варианты ответа:
1. Индексы не работают с текстовыми значениями
2. != приводит к полному сканированию таблицы
3. Запрос содержит ошибку
4. Индексы только для чисел
5. Индекс работает только с = и N

Выбрал ответ 2.