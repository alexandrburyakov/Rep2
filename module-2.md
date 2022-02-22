# 5.1. Введение в виртуализацию. Типы и функции гипервизоров. Обзор рынка вендоров и областей применения.
### 1. Опишите кратко, как вы поняли: в чем основное отличие полной (аппаратной) виртуализации, паравиртуализации и виртуализации на основе ОС.
Основное отличие различных типов виртуализации заключается в уровне "независимости" гостевых операционных систем: 
```TEXT
а. При аппаратной виртуализации гостевые ОС остаются неизменными.
б. При паравиртуализации требуется модификация ядра (драйверов).
в. При виртуализации на основе ОС, гостевая ОС вообще использует ядро хоста.
```
### 2. Выберите один из вариантов использования организации физических серверов, в зависимости от условий использования.
#### а. Высоконагруженная база данных, чувствительная к отказу.
```TEXT
Физические сервера:
Такое размещение дает более высокий отклик и сокращает точки отказа в виде гипервизора хостовой машины.
Позволяет максимально использовать ресурсы хоста (не разделяя их с другими ВМ). 
```
#### б. Различные web-приложения.
```TEXT
Виртуализация уровня ОС:
Требуется меньше ресурсов, высокая скорость масштабирования при необходимости расширения.
Относительно невысокие затраты на администрирование.
```
#### в. Windows системы для использования бухгалтерским отделом.
```TEXT
Паравиртуализация:
Повышение отказоустойчивости. Возможность расширения на уровне ВМ.
Нет жестких требований по доступу к аппаратным ресурсам.
```
#### г. Системы, выполняющие высокопроизводительные расчеты на GPU.
```TEXT
Физические сервера:
Очень важна производительность, а любой слой виртуализации - это ее потеря.
```
### 3. Выберите подходящую систему управления виртуализацией для предложенного сценария. Детально опишите ваш выбор.
```TEXT
Сценарий 1
100 виртуальных машин на базе Linux и Windows, общие задачи, нет особых требований. 
Преимущественно Windows based инфраструктура, требуется реализация программных
балансировщиков нагрузки, репликации данных и автоматизированного механизма создания резервных копий.

Решение
Hyper-V или vSphere.  Хорошо поддерживают ВМ с Windows и Linux. 
Балансировка, репликация, создание резервных копий - встроены. 
Можно создавать кластер гипервизоров - это необходимо для работы 100 ВМ.
```
```TEXT
Сценарий 2
Требуется наиболее производительное бесплатное open source решение для виртуализации небольшой 
(20-30 серверов) инфраструктуры на базе Linux и Windows виртуальных машин.

Решение
Proxmox VE (гипервизор KVM). Оpen source решение, хорошо поддерживает Windows гостей,
Возможности по управлению сравнимы с коммерческими гипервизорами.
```
```TEXT
Сценарий 3
Необходимо бесплатное, максимально совместимое и производительное решение для виртуализации 
Windows инфраструктуры.

Решение
Hyper-V Server. Максимально совместимое (т.к. от Microsoft) и бесплатное решение.
 ```
```TEXT
Сценарий 4
Необходимо рабочее окружение для тестирования программного продукта на нескольких дистрибутивах Linux.

Решение
LXD. Содержит большую библиотеку с разными дистрибутивами
в образах.
 ```
### 4. Опишите возможные проблемы и недостатки гетерогенной среды виртуализации (использования нескольких систем управления виртуализацией одновременно) и что необходимо сделать для минимизации этих рисков и проблем. Если бы у вас был выбор, то создавали бы вы гетерогенную среду или нет? Мотивируйте ваш ответ примерами.
К основным проблемам относятся: необходимость в наборе специалистов различного профиля, кроме того, данный способ виртуализации
инфраструктуры является дорогостоящим и неэффективным в долгосрочной перспективе, поскольку, по мере развития
технологий, компании стремятся обеспечить легкость в управлении, совместимость различных систем и масштабируемость инфраструктуры. 
Лучшее решение, конечно, мигрировать на одну платформу, но это может быть не всегда возможно. В таких ситуациях лучше, по возможности,
использовать гипервизоры с более низким порогом входа для инженеров.
Если бы выбор был за мной, то старался бы делать максимально единообразную систему с минимумом разнообразия используемых технологий.
При этом не отказываясь, в определенных случаях, от использования нескольких систем виртуализации одновременно. Например, использование докер-контейнеров для микросервисов на базе ВМ. 

# 5.2. Применение принципов IaaC в работе с виртуальными машинами
### Задача 1
```TEXT
Опишите своими словами основные преимущества применения на практике IaaC паттернов.

Ответ:
Возможность быстро конфигурировать инфраструктуру. Удобное масштабирование. Централизованное внесение изменений,
используя систему контроля версий, а так же возможность отката на предыдущие версии. Возможность быстрого восстановления
инфраструктуры после выхода из строя в аварийных случаях.

 ```
```TEXT
Какой из принципов IaaC является основополагающим?

Ответ:
Основополагающим принципом является идемпотентность. Гарания достижения необходимого состояния конфигурации.
 ```
### Задача 2
```TEXT
Чем Ansible выгодно отличается от других систем управление конфигурациями?

Ответ:
Ansible использует существующую SSH инфраструктуру, в то время как другие инструменты требуют установки
специального PKI-окружения.
 ```
```TEXT
Какой, на ваш взгляд, метод работы систем конфигурации более надёжный push или pull?

Ответ:
Push надежнее, т.к. управляет конфигурацией централизованно. Если не удастся доставить конфигурацию на сервер,
он оповестит об этом. При методе pull возможна ситуация, когда сервер по какой-либо причине не запросит и
не обновит конфигурацию.  
 ```
### Задача 3
```TEXT
Установить на личный компьютер:
  VirtualBox
  Vagrant
  Ansible
Приложить вывод команд установленных версий каждой из программ, оформленный в markdown.
 ```
Ответ:
```bash
~$ vboxmanage --version
6.1.28r147628
~$ vagrant --version
Vagrant 2.2.19
~$ ansible --version
ansible 2.9.27
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/home/user/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.17 (default, Feb 27 2021, 15:10:58) [GCC 7.5.0]
```
# 5.3. Введение. Экосистема. Архитектура. Жизненный цикл Docker контейнера
### Задача 1
Ссылка на образ: https://hub.docker.com/r/alexandrburyakov/netology_nginx 
### Задача 2
```TEXT
Сценарий 1
Высоконагруженное монолитное java веб-приложение.

Решение
Физический сервер. Так как приложение монолитное - невозможно реализовать в микросерверах без изменения кода, 
а так как высоконагруженное - то желательно не тратить ресурсы на виртуализацию. Однако, при возможности 
масштабирования - докер.
 ```
```TEXT
Сценарий 2
Nodejs веб-приложение.

Решение
Докер. Можно быстро разворачивать приложение со всеми зависимостями и масштабировать.
 ```
```TEXT
Сценарий 3
Мобильное приложение c версиями для Android и iOS.

Решение
Виртуальная машина. Для создания (эмуляции) окружения.
 ```
```TEXT
Сценарий 4
Шина данных на базе Apache Kafka.

Решение
Докер. К тому же будет легко организовать кластер с использованием какого-либо оркестратора.
 ```
```TEXT
Сценарий 5
Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, 
два logstash и две ноды kibana.

Решение
Докер либо ВМ. Докер подойдёт лучше, так как он будет удобнее для кластеризации - меньше оверхед.
 ```
```TEXT
Сценарий 6
Мониторинг-стек на базе Prometheus и Grafana.

Решение
Докер. Быстро разворачивать, плюс возможность масштабирования под разные задачи. Кроме того,
мониторинг не подразумевает высокую нагруженность.
 ```
```TEXT
Сценарий 7
MongoDB, как основное хранилище данных для java-приложения.

Решение
Докер. Есть официальный образ на DockerHub. Однако, если приложение высоконагружено, то лучше физический сервер.
 ```
```TEXT
Сценарий 8
Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry.

Решение
Виртуальная машина. Не требуется масштабирования и частого обновления. Удобно делать бэкапы.
 ```
### Задача 3
Запустите первый контейнер из образа centos c любым тэгом в фоновом режиме, подключив папку /data из
текущей рабочей директории на хостовой машине в /data контейнера.
```bash
user@user-Aspire-F5-573G:~$ docker run -it -d --name centos -v ~/data:/data centos
d101125b2cd12e33e399446190d9d89372fd794a4fa3e5dcf8689d744d5e18a0
```
Запустите второй контейнер из образа debian в фоновом режиме, подключив папку /data из текущей рабочей
директории на хостовой машине в /data контейнера.
```bash
user@user-Aspire-F5-573G:~$ docker run -it -d --name debian -v ~/data:/data debian
92f8f35de22d4fd5a3579addceb92b981e4c2248ac5946e9ddde4bcb28ec878f
```
Подключитесь к первому контейнеру с помощью docker exec и создайте текстовый файл любого содержания в /data.
```bash
user@user-Aspire-F5-573G:~$ docker exec -it centos /bin/bash
[root@d101125b2cd1 /]# echo "centos" > /data/centos.txt
[root@d101125b2cd1 /]# exit
exit
```
Добавьте еще один файл в папку /data на хостовой машине.
```bash
user@user-Aspire-F5-573G:~$ echo "host" > ~/data/host.txt
```
Подключитесь во второй контейнер и отобразите листинг и содержание файлов в /data контейнера.
```bash
user@user-Aspire-F5-573G:~$ docker exec -it debian /bin/bash
root@92f8f35de22d:/# ls -l /data
total 8
-rw-r--r-- 1 root root 7 Jan 26 19:15 centos.txt
-rw-rw-r-- 1 1000 1000 5 Jan 26 19:15 host.txt
root@92f8f35de22d:/# cat /data/centos.txt
centos
root@92f8f35de22d:/# cat /data/host.txt
host
root@92f8f35de22d:/# exit
exit
```
# 5.4. Оркестрация группой Docker контейнеров на примере Docker Compose
### Задача 1
Созданный с помощью Packer образ операционной системы.
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/CLOUD_img_cli.png)
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/CLOUD_img_adm.png)
### Задача 2
Скриншот страницы свойств созданной ВМ.
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/CLOUD_VM.png)
### Задача 3
Скриншот работающего веб-интерфейса Grafana с текущими метриками.
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/CLOUD_grafana.png)

# 5.5. Оркестрация кластером Docker контейнеров на примере Docker Swarm
### Задача 1
Ответы на вопросы:
```TEXT
В чём отличие режимов работы сервисов в Docker Swarm кластере: replication и global?

Ответ:
В режиме `replication` на кластере запускается заданное пользователем количество экземпляров (реплик) сервиса.
При этом на одной ноде может быть как более одной реплики сервиса, так и ни одной. В режиме `global` на каждой 
ноде обязательно запускается по одному экземпляру сервиса. 
 ```
```TEXT
Какой алгоритм выбора лидера используется в Docker Swarm кластере?

Ответ:
В Docker Swarm для выбора Leader-ноды из управляющих нод используется Raft-алгоритм.
 ```
```TEXT
Что такое Overlay Network?

Ответ:
Overlay Network служит для соединения нескольких демонов Docker между собой, позволяя docker-swarm
службам взаимодействовать друг с другом.
```
### Задача 2
Создан Docker Swarm кластер в Яндекс.Облаке

Скриншот из терминала (консоли), с выводом команды: `docker node ls`
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/swarm-nodes.png)
### Задача 3
Создан готовый к боевой эксплуатации кластер мониторинга, состоящий из стека микросервисов.

Скриншот из терминала (консоли), с выводом команды: `docker service ls`
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/swarm-services.png)

# 6.1. Типы и структура СУБД
### Задача 1
Выберите подходящие типы СУБД для каждой сущности и объясните свой выбор.
```TEXT
Электронные чеки в json виде.

Ответ:
Документо-ориентированная. Классический подход для хранения документов в json. 
 ```
```TEXT
Склады и автомобильные дороги для логистической компании.

Ответ:
Графовая NoSQL БД. Склады и дороги удобно представлять в виде узлов и ребер.
 ```
```TEXT
Генеалогические деревья.

Ответ:
Иерархическая. Идеально подходит для данной задачи.
 ```
```TEXT
Кэш идентификаторов клиентов с ограниченным временем жизни для движка аутентификации.

Ответ:
Ключ-значение. Например Redis. Классический продход для данного примера.
 ```
```TEXT
Отношения клиент-покупка для интернет-магазина.

Ответ:
Реляционная БД. Для создания отношений (зависимостей) между сущностями.
 ```
### Задача 2
Классификация реализаций согласно CAP, PACELC.
```TEXT
Данные записываются на все узлы с задержкой до часа (асинхронная запись): CA (PC/EL)
При сетевых сбоях, система может разделиться на 2 раздельных кластера: AP (PA/EL)
Система может не прислать корректный ответ или сбросить соединение: CP (PC/EC)
 ```
### Задача 2 (доработка)
```TEXT
1. Если подразумевается, что система всегда доступна, но узлы могут ответить не одинаково
(данные не согласованы), т.к. долго не общаются (устойчивы к разделению), то по CAP: AP.
По PACELC - (PA/EL), т.к., действимтельно, подсознательно ближе Latency. 
2. Если система все таки отвечает, хотя и не корректно (или даже сбрасывает соединение),
всячески избегая дать несогласованные данные, то по CAP - это СА, по PACELC - (PC/EC), т.к. 
приоритет - согласованность. 
```
### Задача 3
Могут ли в одной системе сочетаться принципы BASE и ACID? Почему?
```TEXT
Не могут, т.к. это два противоречащих друг другу принципа. (По ACID - данные согласованы, по BASE - нет.) 
 ```
### Задача 4
Ответ:
```TEXT
Redis - key-value хранилище, которое имеет механизм Pub/Sub. В данном случае установка ключей с ttl +
подписка на нотификацию о просроченных ключах.
Минусы: Ограничение хранилища (все данные должны поместиться в оперативной памяти). Redis предлагает
только базовую безопасность (нет механизма ролей). Нет языка запросов (как SQL) - теряется гибкость. 
 ```
# 6.2. SQL
### Задача 1
docker-compose манифест:
```yaml
version: "3.1"
services:
  postgres:
    image: postgres:12
    environment:
      POSTGRES_DB: "netology"
      POSTGRES_USER: "netology"
      POSTGRES_PASSWORD: "test123"
      PGDATA: "/var/lib/postgresql/data/pgdata"
    container_name: netology_psql
    volumes:
      - ./backup:/backup
      - .:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    restart: always
```
Запускаем и заходим в БД
```bash
docker-compose up -d
docker exec -it netology_psql psql -U netology -W netology
```
### Задача 2
Cоздайте пользователя test-admin-user и БД test_db.
```
CREATE DATABASE test_db;
CREATE USER "test-admin-user" WITH PASSWORD 'test1';
```
В БД test_db создайте таблицу orders и clients.
```
CREATE TABLE orders (id SERIAL PRIMARY KEY, naim VARCHAR(255), price INT);
CREATE TABLE clients (id SERIAL PRIMARY KEY, last_name VARCHAR(30), country VARCHAR(30), 
                      order_id INT, FOREIGN KEY (order_id) REFERENCES orders (id));
CREATE INDEX index_country ON clients (country);
```
Предоставьте привилегии на все операции пользователю test-admin-user на таблицы БД test_db.
```
GRANT CONNECT ON DATABASE test_db to "test-admin-user";
GRANT ALL ON ALL TABLES IN SCHEMA public to "test-admin-user";
```
Создайте пользователя test-simple-user.
```
CREATE USER "test-simple-user";
```
Предоставьте пользователю test-simple-user права на SELECT/INSERT/UPDATE/DELETE данных таблиц БД test_db.
```
GRANT CONNECT ON DATABASE test_db to "test-simple-user";
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public to "test-simple-user";
```
Итоговый список БД после выполнения пунктов выше:
```
test_db=# \l
                                     List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |       Access privileges       
-----------+----------+----------+------------+------------+-------------------------------
 netology  | netology | UTF8     | en_US.utf8 | en_US.utf8 | 
 postgres  | netology | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | netology | UTF8     | en_US.utf8 | en_US.utf8 | =c/netology                  +
           |          |          |            |            | netology=CTc/netology
 template1 | netology | UTF8     | en_US.utf8 | en_US.utf8 | =c/netology                  +
           |          |          |            |            | netology=CTc/netology
 test_db   | netology | UTF8     | en_US.utf8 | en_US.utf8 | =Tc/netology                 +
           |          |          |            |            | netology=CTc/netology        +
           |          |          |            |            | "test-admin-user"=c/netology +
           |          |          |            |            | "test-simple-user"=c/netology
(5 rows)
```
Описание таблиц (describe):
```
test_db=# \d orders
                                    Table "public.orders"
 Column |          Type          | Collation | Nullable |              Default               
--------+------------------------+-----------+----------+------------------------------------
 id     | integer                |           | not null | nextval('orders_id_seq'::regclass)
 naim   | character varying(255) |           |          | 
 price  | integer                |           |          | 
Indexes:
    "orders_pkey" PRIMARY KEY, btree (id)
Referenced by:
    TABLE "clients" CONSTRAINT "clients_order_id_fkey" FOREIGN KEY (order_id) REFERENCES orders(id)
```
```
test_db=# \d clients
                                     Table "public.clients"
  Column   |         Type          | Collation | Nullable |               Default               
-----------+-----------------------+-----------+----------+-------------------------------------
 id        | integer               |           | not null | nextval('clients_id_seq'::regclass)
 last_name | character varying(30) |           |          | 
 country   | character varying(30) |           |          | 
 order_id  | integer               |           |          | 
Indexes:
    "clients_pkey" PRIMARY KEY, btree (id)
    "index_country" btree (country)
Foreign-key constraints:
    "clients_order_id_fkey" FOREIGN KEY (order_id) REFERENCES orders(id)
```
SQL-запрос для выдачи списка пользователей с правами над таблицами test_db:
```
SELECT 
    grantee, table_name, privilege_type 
FROM 
    information_schema.table_privileges 
WHERE 
    grantee LIKE 'te%';
```
Список пользователей с правами над таблицами test_db:
```
test_db=# SELECT grantee, table_name, privilege_type FROM information_schema.table_privileges 
WHERE grantee LIKE 'te%';
     grantee      | table_name | privilege_type 
------------------+------------+----------------
 test-admin-user  | orders     | INSERT
 test-admin-user  | orders     | SELECT
 test-admin-user  | orders     | UPDATE
 test-admin-user  | orders     | DELETE
 test-admin-user  | orders     | TRUNCATE
 test-admin-user  | orders     | REFERENCES
 test-admin-user  | orders     | TRIGGER
 test-admin-user  | clients    | INSERT
 test-admin-user  | clients    | SELECT
 test-admin-user  | clients    | UPDATE
 test-admin-user  | clients    | DELETE
 test-admin-user  | clients    | TRUNCATE
 test-admin-user  | clients    | REFERENCES
 test-admin-user  | clients    | TRIGGER
 test-simple-user | orders     | INSERT
 test-simple-user | orders     | SELECT
 test-simple-user | orders     | UPDATE
 test-simple-user | orders     | DELETE
 test-simple-user | clients    | INSERT
 test-simple-user | clients    | SELECT
 test-simple-user | clients    | UPDATE
 test-simple-user | clients    | DELETE
(22 rows)
```
### Задача 3
Используя SQL синтаксис - наполните таблицы следующими тестовыми данными:
```
INSERT INTO orders (naim, price) VALUES ('Шоколад', 10), ('Принтер', 3000), 
('Книга', 500), ('Монитор', 7000), ('Гитара', 4000);
```
```
test_db=# SELECT * FROM orders;
 id |  naim   | price 
----+---------+-------
  1 | Шоколад |    10
  2 | Принтер |  3000
  3 | Книга   |   500
  4 | Монитор |  7000
  5 | Гитара  |  4000
(5 rows)
```
```
INSERT INTO clients (last_name, country) VALUES ('Иванов Иван Иванович', 'USA'), 
('Петров Петр Петрович', 'Canada'), ('Иоганн Себастьян Бах', 'Japan'), 
('Ронни Джеймс Дио', 'Russia'), ('Ritchie Blackmore', 'Russia');
```
```
test_db=# SELECT * FROM clients;
 id |      last_name       | country | order_id 
----+----------------------+---------+----------
  1 | Иванов Иван Иванович | USA     |         
  2 | Петров Петр Петрович | Canada  |         
  3 | Иоганн Себастьян Бах | Japan   |         
  4 | Ронни Джеймс Дио     | Russia  |         
  5 | Ritchie Blackmore    | Russia  |         
(5 rows)
```
Вычислите количество записей для каждой таблицы:
```
test_db=# SELECT count(*) FROM orders;
 count 
-------
     5
(1 row)

test_db=# SELECT count(*) FROM clients;
 count 
-------
     5
(1 row)
```
### Задача 4

Часть пользователей из таблицы clients решили оформить заказы из таблицы orders.
Используя foreign keys свяжите записи из таблиц, согласно таблице.

Приведите SQL-запросы для выполнения данных операций.
```
UPDATE clients SET order_id = (SELECT id FROM orders WHERE naim = 'Книга') 
WHERE last_name = 'Иванов Иван Иванович';
UPDATE clients SET order_id = (SELECT id FROM orders WHERE naim = 'Монитор') 
WHERE last_name = 'Петров Петр Петрович';
UPDATE clients SET order_id = (SELECT id FROM orders WHERE naim = 'Гитара') 
WHERE last_name = 'Иоганн Себастьян Бах';
```
Приведите SQL-запрос для выдачи всех пользователей, которые совершили заказ, а также вывод данного запроса.
```
test_db=# SELECT c.id, c.last_name, o.naim FROM clients AS c INNER JOIN orders AS o ON o.id = c.order_id;
 id |      last_name       |  naim   
----+----------------------+---------
  1 | Иванов Иван Иванович | Книга
  2 | Петров Петр Петрович | Монитор
  3 | Иоганн Себастьян Бах | Гитара
(3 rows)
```
### Задача 5
Получение полной информации по выполнению запроса выдачи всех пользователей из задачи 4.
```
test_db=# EXPLAIN SELECT c.id, c.last_name, o.naim FROM clients AS c INNER JOIN orders AS o ON o.id = c.order_id;
                               QUERY PLAN                                
-------------------------------------------------------------------------
 Hash Join  (cost=13.15..28.47 rows=420 width=598)
   Hash Cond: (c.order_id = o.id)
   ->  Seq Scan on clients c  (cost=0.00..14.20 rows=420 width=86)
   ->  Hash  (cost=11.40..11.40 rows=140 width=520)
         ->  Seq Scan on orders o  (cost=0.00..11.40 rows=140 width=520)
(5 rows)
```

Эта команда выводит план выполнения, генерируемый планировщиком PostgreSQL.
По каждой операции (итерации) видно стоимость запуска и общую стоимость выполнения.
Ожидаемое количсество строк и среднюю длину строки в байтах. 
Cтроки одной таблицы записываются в хеш-таблицу в памяти, после чего сканируется другая таблица
и для каждой её строки проверяется соответствие по хеш-таблице

### Задача 6
Приведите список операций, который вы применяли для бэкапа данных и восстановления.
```
pg_dump -U netology -W test_db > /backup/test_db.sql
psql -U netology -W test_db < /backup/test_db.sql
```
