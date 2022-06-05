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
# 6.3. MySQL
### Задача 1
Используя docker поднимите инстанс MySQL (версию 8). Данные БД сохраните в volume.
```bash
$ docker run --name mysql-netology -v /home/user/netology/6.3/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=test123 -p 3306:3306 -d mysql:8
```
Изучите бэкап БД и восстановитесь из него.
```bash
$ docker exec -i mysql-netology sh -c 'exec mysql -uroot -ptest123 test_db' < ./test_dump.sql
```
Перейдите в управляющую консоль mysql внутри контейнера.
```bash
$ docker exec -it mysql-netology mysql -u root -p
```
Найдите команду для выдачи статуса БД и приведите в ответе из ее вывода версию сервера БД.
```bash
mysql> \s
--------------
mysql  Ver 8.0.28 for Linux on x86_64 (MySQL Community Server - GPL)
...
```
Подключитесь к восстановленной БД и получите список таблиц из этой БД.
```bash
mysql> use test_db
...
Database changed
mysql> show tables;
+-------------------+
| Tables_in_test_db |
+-------------------+
| orders            |
+-------------------+
1 row in set (0.01 sec)
```
Приведите в ответе количество записей с price > 300.
```bash
mysql> SELECT count(*) FROM orders WHERE price > 300;
+----------+
| count(*) |
+----------+
|        1 |
+----------+
1 row in set (0.00 sec)
```
### Задача 2
Создайте пользователя test в БД c паролем test-pass.
```TEXT
mysql> CREATE USER 'test'@'localhost' 
    -> IDENTIFIED WITH mysql_native_password BY 'test-pass'
    -> WITH MAX_QUERIES_PER_HOUR 100
    -> PASSWORD EXPIRE INTERVAL 180 DAY
    -> FAILED_LOGIN_ATTEMPTS 3 PASSWORD_LOCK_TIME 2
    -> ATTRIBUTE '{"fname":"James", "lname":"Pretty"}';
Query OK, 0 rows affected (0.15 sec)
```
Предоставьте привелегии пользователю test на операции SELECT базы test_db.
```TEXT
mysql> GRANT SELECT ON test_db.* TO 'test'@'localhost';
Query OK, 0 rows affected, 1 warning (0.06 sec)
```
Используя таблицу INFORMATION_SCHEMA.USER_ATTRIBUTES получите данные по пользователю test
и приведите в ответе к задаче.
```TEXT
mysql> SELECT * FROM INFORMATION_SCHEMA.USER_ATTRIBUTES WHERE USER='test';
+------+-----------+---------------------------------------+
| USER | HOST      | ATTRIBUTE                             |
+------+-----------+---------------------------------------+
| test | localhost | {"fname": "James", "lname": "Pretty"} |
+------+-----------+---------------------------------------+
1 row in set (0.00 sec)
```
### Задача 3
Исследуйте, какой engine используется в таблице БД test_db и приведите в ответе.
```TEXT
mysql> SELECT table_schema,table_name,engine FROM information_schema.tables WHERE table_schema="test_db";
+--------------+------------+--------+
| TABLE_SCHEMA | TABLE_NAME | ENGINE |
+--------------+------------+--------+
| test_db      | orders     | InnoDB |
+--------------+------------+--------+
1 row in set (0.00 sec)

Используется InnoDB.
```
Измените engine и приведите время выполнения и запрос на изменения из профайлера в ответе.
```TEXT
mysql> SET profiling = 1
    -> ;
Query OK, 0 rows affected, 1 warning (0.00 sec)

mysql> ALTER TABLE orders ENGINE = MyISAM;
Query OK, 5 rows affected (1.67 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> ALTER TABLE orders ENGINE = InnoDB;
Query OK, 5 rows affected (1.11 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> SHOW PROFILES;
+----------+------------+------------------------------------+
| Query_ID | Duration   | Query                              |
+----------+------------+------------------------------------+
|        1 | 1.67945925 | ALTER TABLE orders ENGINE = MyISAM |
|        2 | 1.11124950 | ALTER TABLE orders ENGINE = InnoDB |
+----------+------------+------------------------------------+
2 rows in set, 1 warning (0.00 sec)
```
### Задача 4
Изучите файл my.cnf в директории /etc/mysql. Измените его согласно ТЗ (движок InnoDB).
```TEXT
[mysqld]
pid-file        = /var/run/mysqld/mysqld.pid
socket          = /var/run/mysqld/mysqld.sock
datadir         = /var/lib/mysql
secure-file-priv= NULL

# Custom config should go here
!includedir /etc/mysql/conf.d/

innodb_flush_log_at_trx_commit = 2
innodb_file_per_table = ON
innodb_log_buffer_size = 1M
# 30% RAM
innodb_buffer_pool_size = 680M
innodb_log_file_size = 100M
```
# 6.4. PostgreSQL
### Задача 1
Используя docker поднимите инстанс PostgreSQL (версию 13).
```yaml
version: "3.1"
services:
  postgres:
    image: postgres:13
    environment:
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
```bash
docker-compose up -d
```
Подключитесь к БД PostgreSQL используя psql.
```bash
docker exec -it netology_psql psql -U postgres -W
```
Найдите и приведите управляющие команды:
```TEXT
- вывода списка БД: \l
- подключения к БД: \c
- вывода списка таблиц: \d 
- вывода описания содержимого таблиц: \d 'table name'
- выхода из psql: \q
```
### Задача 2
Используя psql создайте БД test_database.
```TEXT
postgres=# CREATE DATABASE test_database;
CREATE DATABASE
```
Восстановите бэкап БД в test_database.
```TEXT
root@ed608da00cc1:/# cd /backup
root@ed608da00cc1:/backup# ls
test_dump.sql
root@ed608da00cc1:/backup# psql -U postgres -d test_database -f test_dump.sql
```
Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.
```TEXT
test_database=# ANALYZE orders;
ANALYZE
```
Используя таблицу pg_stats, найдите столбец таблицы orders с наибольшим средним значением размера элементов в байтах.
```TEXT
test_database=# SELECT attname, avg_width FROM pg_stats WHERE tablename = 'orders' ORDER BY avg_width DESC LIMIT 1;
 attname | avg_width 
---------+-----------
 title   |        16
(1 row)
```
### Задача 3
Вам предложили провести разбиение таблицы на 2 (шардировать на orders_1 - price>499 и orders_2 - price<=499).
Предложите SQL-транзакцию для проведения данной операции.
```TEXT
 BEGIN;
 CREATE TABLE orders_1 (CONSTRAINT price CHECK (price > 499)) INHERITS (orders);
 CREATE TABLE orders_2 (CONSTRAINT price CHECK (price <= 499)) INHERITS (orders);
 INSERT INTO orders_1 SELECT * FROM orders where price > 499;
 INSERT INTO orders_2 SELECT * FROM orders where price <= 499;
 COMMIT;
```
Можно ли было изначально исключить "ручное" разбиение при проектировании таблицы orders?
```TEXT
При проектировании таблицы orders можно было изначально сделать её секционированной.
CREATE TABLE orders (     
    id integer NOT NULL,
    title character varying(80) NOT NULL,
    price integer DEFAULT 0
    ) PARTITION BY RANGE (price);
CREATE TABLE orders_1 PARTITION OF orders FOR VALUES FROM (500) TO (MAXVALUE);
CREATE TABLE orders_2 PARTITION OF orders FOR VALUES FROM (MINVALUE) TO (500);
```
### Задача 4
Используя утилиту pg_dump создайте бекап БД test_database.
```TEXT
root@ed608da00cc1:/backup# pg_dump -U postgres -d test_database > test_dump_new.sql
```
Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца title для таблиц test_database?
```TEXT
ALTER TABLE orders ADD UNIQUE (title);
ALTER TABLE orders_1 ADD UNIQUE (title);
ALTER TABLE orders_2 ADD UNIQUE (title);
```
# 6.5. Elasticsearch
### Задача 1
Текст Dockerfile манифеста.
```TEXT
FROM centos:7

ENV ES_DISTR="/opt/elasticsearch"
ENV ES_HOME="${ES_DISTR}/elasticsearch-7.17.1"
ENV ES_DATA_DIR="/var/lib/data"
ENV ES_LOG_DIR="/var/lib/logs"
ENV ES_BACKUP="/opt/elasticsearch/snapshots"                                                                                                                                                               $
ENV ES_JAVA_OPTS="-Xms512m -Xmx512m"

WORKDIR "${ES_DISTR}"

RUN yum install wget -y

RUN yum install perl-Digest-SHA -y

RUN wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.17.1-linux-x86_64.tar.gz && \
    wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.17.1-linux-x86_64.tar.gz.sha512 && \
    shasum -a 512 -c elasticsearch-7.17.1-linux-x86_64.tar.gz.sha512 && \
    tar -xzf elasticsearch-7.17.1-linux-x86_64.tar.gz

COPY elasticsearch.yml ${ES_HOME}/config

ENV ES_USER="elasticsearch"

RUN useradd ${ES_USER}

RUN mkdir -p "${ES_DATA_DIR}" && \
    mkdir -p "${ES_LOG_DIR}" && \
    mkdir -p "${ES_BACKUP}" && \
    chown -R ${ES_USER}: "${ES_DISTR}" && \
    chown -R ${ES_USER}: "${ES_DATA_DIR}" && \
    chown -R ${ES_USER}: "${ES_BACKUP}" && \
    chown -R ${ES_USER}: "${ES_LOG_DIR}"

USER ${ES_USER}

WORKDIR "${ES_HOME}"

EXPOSE 9200
EXPOSE 9300

ENTRYPOINT ["./bin/elasticsearch"]
```
```TEXT
discovery.type: single-node

cluster.name: netology_elasticsearch

node.name: netology_test

path.data: /var/lib/data

path.logs: /var/lib/logs

path.repo: /opt/elasticsearch/snapshots

network.host: 0.0.0.0
```
Cсылка на образ в репозитории dockerhub: https://hub.docker.com/r/alexandrburyakov/nelology_elasticsearch

Ответ elasticsearch на запрос пути / в json виде.
```TEXT
$ curl localhost:9200/
{
  "name" : "netology_test",
  "cluster_name" : "netology_elasticsearch",
  "cluster_uuid" : "EFdc4HD8SJSGqvbWmLf-7A",
  "version" : {
    "number" : "7.17.1",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "e5acb99f822233d62d6444ce45a4543dc1c8059a",
    "build_date" : "2022-02-23T22:20:54.153567231Z",
    "build_snapshot" : false,
    "lucene_version" : "8.11.1",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```
### Задача 2
```TEXT
curl -X PUT "localhost:9200/ind-1?pretty" -H 'Content-Type: application/json' -d'
{
  "settings": {
    "number_of_shards": 1,
    "number_of_replicas": 0
  }
}
'
...
```
Получите список индексов и их статусов, используя API и приведите в ответе на задание.
```TEXT
$ curl -X GET 'http://localhost:9200/_cat/indices?v'
health status index            uuid                   pri rep docs.count docs.deleted store.size pri.store.size
green  open   .geoip_databases YD8KrFPSQTWhj6ctc7Vuuw   1   0         41            0     39.5mb         39.5mb
green  open   ind-1            SVP0iPgiSEKBz25loNfCmw   1   0          0            0       226b           226b
yellow open   ind-3            Ub-phIL9T6uoRQFbKpVBlQ   4   2          0            0       904b           904b
yellow open   ind-2            x1t4trJdQ9CNVmtdR6D2uQ   2   1          0            0       452b           452b
```
Получите состояние кластера elasticsearch, используя API.
```TEXT
curl -XGET localhost:9200/_cluster/health/?pretty=true
{
  "cluster_name" : "netology_elasticsearch",
  "status" : "yellow",
  "timed_out" : false,
  "number_of_nodes" : 1,
  "number_of_data_nodes" : 1,
  "active_primary_shards" : 10,
  "active_shards" : 10,
  "relocating_shards" : 0,
  "initializing_shards" : 0,
  "unassigned_shards" : 10,
  "delayed_unassigned_shards" : 0,
  "number_of_pending_tasks" : 0,
  "number_of_in_flight_fetch" : 0,
  "task_max_waiting_in_queue_millis" : 0,
  "active_shards_percent_as_number" : 50.0
}
```
Как вы думаете, почему часть индексов и кластер находится в состоянии yellow?
```TEXT
Два индекса находятся в состоянии yellow, так как у них есть реплики, а учитывая, что в нашем кластере
всего одна нода - эти реплики некуда размещать.
```
```TEXT
curl -X DELETE 'http://localhost:9200/ind-1?pretty'
...
```

### Задача 3
Приведите в ответе запрос API и результат вызова API для создания репозитория.
```TEXT
$ curl -X PUT "localhost:9200/_snapshot/netology_backup?pretty" -H 'Content-Type: application/json' -d'
> {
>   "type": "fs",
>   "settings": {
>     "location": "/opt/elasticsearch/snapshots"
>   }
> }
> '
{
  "acknowledged" : true
}
```
Создайте индекс test с 0 реплик и 1 шардом и приведите в ответе список индексов.
```TEXT
$ curl -X PUT "localhost:9200/test?pretty" -H 'Content-Type: application/json' -d'
> {
>   "settings": {
>     "number_of_shards": 1,
>     "number_of_replicas": 0
>   }
> }
> '
{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "test"
}
$ curl -X GET 'http://localhost:9200/_cat/indices?v'
health status index            uuid                   pri rep docs.count docs.deleted store.size pri.store.size
green  open   .geoip_databases p1rfLFs1RJOET0RNOVh6NQ   1   0         41            0     39.5mb         39.5mb
green  open   test             DiPLU5ZTS9m64LHU0ara8g   1   0          0            0       226b           226b
```
Создайте snapshot состояния кластера elasticsearch.
```TEXT
curl -X PUT "localhost:9200/_snapshot/netology_backup/my_snapshot?wait_for_completion=true&pretty"
```
Приведите в ответе список файлов в директории со snapshotами.
```TEXT
$docker exec netology_elasticsearch ls -l /opt/elasticsearch/snapshots
total 48
-rw-r--r-- 1 elasticsearch elasticsearch  1423 Mar  7 21:29 index-0
-rw-r--r-- 1 elasticsearch elasticsearch     8 Mar  7 21:29 index.latest
drwxr-xr-x 6 elasticsearch elasticsearch  4096 Mar  7 21:29 indices
-rw-r--r-- 1 elasticsearch elasticsearch 29277 Mar  7 21:29 meta-E6Fo2m1yRzOM_iTatPJgPA.dat
-rw-r--r-- 1 elasticsearch elasticsearch   710 Mar  7 21:29 snap-E6Fo2m1yRzOM_iTatPJgPA.dat
```
Удалите индекс test и создайте индекс test-2. Приведите в ответе список индексов.
```TEXT
$curl -X DELETE 'http://localhost:9200/test?pretty'
{
  "acknowledged" : true
}
$ curl -X PUT "localhost:9200/test-2?pretty" -H 'Content-Type: application/json' -d'
$ curl -X GET 'http://localhost:9200/_cat/indices?v'
health status index            uuid                   pri rep docs.count docs.deleted store.size pri.store.size
green  open   .geoip_databases p1rfLFs1RJOET0RNOVh6NQ   1   0         41            0     39.5mb         39.5mb
green  open   test-2           4jS_RrJBSwqbmcHSIxzMuw   1   0          0            0       226b           226b
```
Приведите в ответе запрос к API восстановления и итоговый список индексов.
```TEXT
$ curl -X POST localhost:9200/_snapshot/netology_backup/my_snapshot/_restore?pretty -H 'Content-Type: application/json' -d'                              
> {
>   "indices": "test",
>   "include_global_state":true
> }
> '
{
  "accepted" : true
}
$ curl -X GET 'http://localhost:9200/_cat/indices?v'
health status index            uuid                   pri rep docs.count docs.deleted store.size pri.store.size
green  open   .geoip_databases 0WcC_W1UQTatrDoRc9K6lA   1   0         41            0     39.5mb         39.5mb
green  open   test-2           4jS_RrJBSwqbmcHSIxzMuw   1   0          0            0       226b           226b
green  open   test             N1BunjXoQJSVNWKoZLQNTw   1   0          0            0       226b           226b
```
# 6.6. Troubleshooting
### Задача 1 (MongoDB)
Напишите список операций, которые вы будете производить для остановки запроса пользователя.
```TEXT
Найти запрос: db.currentOp({ "active" : true, "secs_running" : { "$gt" : 180 }})
Завершить запрос по opid: db.killOp(opid)
```
Предложите вариант решения проблемы с долгими (зависающими) запросами в MongoDB.
```TEXT
Добавить или переделать соответствующий индекс.
Использовать метод maxTimeMS.
```
### Задача 2 (Redis)
Как вы думаете, в чем может быть проблема?
```TEXT
Думаю, что превышен лимит оперативной памяти, соответственно блокируются операции записи.
```
### Задача 3 (MySQL)
Как вы думаете, почему это начало происходить и как локализовать проблему?
```TEXT
Вероятно, что ошибки начали возникать из-за роста нагрузки.
```
Какие пути решения данной проблемы вы можете предложить?
```TEXT
Увеличить значение параметров : connect_timeout, interactive_timeout, wait_timeout.
Добавить индексы для оптимизации и ускорения запросов.
Оптимизировать запросы.
```
### Задача 4 (PostgreSQL)
Как вы думаете, что происходит?
```TEXT
Причина в недостатке памяти. OOM-Killer завершает процессы, чтобы предотвратить падение системы.
```
Как бы вы решили данную проблему?
```TEXT
Для решения проблемы можно увеличить объем памяти, поменять настройки ядра: `vm.overcommit_memory`.
```
### Доработка по д/з "6.6. Troubleshooting"
```TEXT
Задача 2
Возможно, что проблема связана с настройкой (Allow writes only with N attached replicas), при которой Redis
блокирует запись, если количество доступных реплик недостаточно.
Такая ситуация может возникнуть, например, если добавленные реплики расположены на других хостах и общение
с репликами происходит по сети, а при дублировании данных на все реплики, их объём превышает ширину канала. 
Тогда могут теряться пакеты, и Redis будет считать, что реплик у него недостаточно и заблокирует запись.
```
```TEXT
Задача 4
Если не помогает настройка параметров `vm.overcommit_memory` и `vm.overcommit_ratio`, то можно попробовать
настроить swap, которым управляет переменная cat /proc/sys/vm/swappiness. Значение этой переменной указывают ядру,
как обрабатывать подкачку страниц. Чем больше значение, тем меньше вероятности, что OOM завершит процесс,
но из-за операций ввода-вывода это негативно сказывается на базе данных. И наоборот — чем меньше значение,
тем выше вероятность вмешательства OOM-Killer, но и производительность базы данных тоже выше. Поэтому, чтобы уменьшить
вероятность срабатывания OOM-Killer, можно увеличить значение вышеуказанной переменной (максимальное значение - 100, 
значение по умолчанию - 60).
```
### Доработка #2 по д/з "6.6. Troubleshooting"
```TEXT
Для решения проблемы нехватки оперативной памяти (при отсутствии ресурсов для увеличения оп и масштабирования сервиса)
необходимо усилить ограничения в настройках PG на использование оперативной памяти: shared_buffers, work_mem, 
hash_mem_multiplier, а так же в настройке подключений: max_connections.
```

# 7.1. Инфраструктура как код
### Задача 1
Какой тип инфраструктуры будем использовать для этого проекта: изменяемый или не изменяемый?
```TEXT
Не изменяемый, на основе образов, подготовленных с помощью Packer.
```
Будет ли центральный сервер для управления инфраструктурой?
```TEXT
Нет. Так как будем использовать инструменты, которые не требуют сервера: Packer, Terraform, Ansible.
Однако, код инфраструктуры будет хранится на сервере (git).
```
Будут ли агенты на серверах?
```TEXT
Нет. Можно использовать ssh.
```
Будут ли использованы средства для управления конфигурацией или инициализации ресурсов?
```TEXT
Да. Terraform, который уже используется.
```
Какие инструменты из уже используемых вы хотели бы использовать для нового проекта?
```TEXT
Packer, Terraform, Ansible, Docker, Kubernetes.
```
Хотите ли рассмотреть возможность внедрения новых инструментов для этого проекта?
```TEXT
Да. Рассмотрел бы внедерение Jenkins.
```
### Задача 2
```bash
~$ terraform --version
Terraform v1.1.7
on linux_amd64
```
### Задача 3
Скачал и распаковал бинарник более ранней версии 1.0.11
```bash
user@user-Aspire-F5-573G:~/Загрузки/terraform_1.0.11_linux_amd64$ terraform --version
Terraform v1.1.7
on linux_amd64
user@user-Aspire-F5-573G:~/Загрузки/terraform_1.0.11_linux_amd64$ terraform_1011 --version
Terraform v1.0.11
on linux_amd64

Your version of Terraform is out of date! The latest version
is 1.1.7. You can update by downloading from https://www.terraform.io/downloads.html
```
# 09.02 CI\CD
### Знакомство с SonarQube
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/sonar_qube.png)
### Знакомство с Nexus
[maven-metadata.xml](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/maven-metadata.xml)
### Знакомство с Maven
[pom.xml](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/pom.xml)

# Доработка по д/з "09.02 CI\CD"
### Знакомство с SonarQube (подробно по шагам)
Запускаем контейнер из скачанного с докерхаб образа sonarqube:
```bash
user@user-Aspire-F5-573G:~/netology/9.2$ docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:8.7-community
af1deb07a0cba2a6259445641d0b7670070ca16b1bdd0841607d6cefcfba8d31
user@user-Aspire-F5-573G:~/netology/9.2$ docker ps -a
CONTAINER ID   IMAGE                     COMMAND                  CREATED         STATUS         PORTS                                       NAMES
af1deb07a0cb   sonarqube:8.7-community   "bin/run.sh bin/sona…"   2 minutes ago   Up 2 minutes   0.0.0.0:9000->9000/tcp, :::9000->9000/tcp   sonarqube
```
Проверяем готовность сервиса через браузер, входим под admin/admin, меняем пароль, создаем новый проект (netology), получаем токен,
cкачиваем пакет sonar-scanner, который нам предлагает скачать сам sonarqube:
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/Sonar_qube_1.png)
Делаем так, чтобы binary был доступен через вызов в shell (меняем переменную PATH), проверяем:
```bash
user@user-Aspire-F5-573G:~/netology/9.2$ sonar-scanner --version
INFO: Scanner configuration file: /home/user/sonarscan/sonar-scanner-4.7.0.2747-linux/conf/sonar-scanner.properties
INFO: Project root configuration file: NONE
INFO: SonarScanner 4.7.0.2747
INFO: Java 11.0.14.1 Eclipse Adoptium (64-bit)
INFO: Linux 5.4.0-109-generic amd64
```
Скачиваем предлагаемый в задании файл кода в рабочую директорию:
```bash
user@user-Aspire-F5-573G:~/netology/9.2$ wget https://raw.githubusercontent.com/netology-code/mnt-homeworks/master/09-ci-02-cicd/example/fail.py
--2022-05-18 17:22:09--  https://raw.githubusercontent.com/netology-code/mnt-homeworks/master/09-ci-02-cicd/example/fail.py
Распознаётся raw.githubusercontent.com (raw.githubusercontent.com)… 2606:50c0:8001::154, 2606:50c0:8003::154, 2606:50c0:8002::154, ...
Подключение к raw.githubusercontent.com (raw.githubusercontent.com)|2606:50c0:8001::154|:443... ошибка: Сеть недоступна.
Подключение к raw.githubusercontent.com (raw.githubusercontent.com)|2606:50c0:8003::154|:443... ошибка: Сеть недоступна.
Подключение к raw.githubusercontent.com (raw.githubusercontent.com)|2606:50c0:8002::154|:443... ошибка: Сеть недоступна.
Подключение к raw.githubusercontent.com (raw.githubusercontent.com)|2606:50c0:8000::154|:443... ошибка: Сеть недоступна.
Подключение к raw.githubusercontent.com (raw.githubusercontent.com)|185.199.110.133|:443... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа… 200 OK
Длина: 255 [text/plain]
Сохранение в: «fail.py»

fail.py             100%[===================>]     255  --.-KB/s    за 0s      

2022-05-18 17:22:10 (2,71 MB/s) - «fail.py» сохранён [255/255]
```
Запускаем анализатор против скачанного кода с дополнительным ключом -Dsonar.coverage.exclusions=fail.py
```bash
user@user-Aspire-F5-573G:~/netology/9.2$ sonar-scanner \
>   -Dsonar.projectKey=netology \
>   -Dsonar.sources=. \
>   -Dsonar.host.url=http://localhost:9000 \
>   -Dsonar.login=f1f8e966a3fabb2a0da5cb43c2024b14c4460a78\
>   -Dsonar.coverage.exclusions=fail.py
INFO: Scanner configuration file: /home/user/sonarscan/sonar-scanner-4.7.0.2747-linux/conf/sonar-scanner.properties
INFO: Project root configuration file: NONE
INFO: SonarScanner 4.7.0.2747
INFO: Java 11.0.14.1 Eclipse Adoptium (64-bit)
INFO: Linux 5.4.0-109-generic amd64
INFO: User cache: /home/user/.sonar/cache
INFO: Scanner configuration file: /home/user/sonarscan/sonar-scanner-4.7.0.2747-linux/conf/sonar-scanner.properties
INFO: Project root configuration file: NONE
INFO: Analyzing on SonarQube server 8.7.1
INFO: Default locale: "ru_RU", source code encoding: "UTF-8" (analysis is platform dependent)
INFO: Load global settings
INFO: Load global settings (done) | time=216ms
INFO: Server id: BF41A1F2-AYDXlqtv7eTjZ9n7QXfV
INFO: User cache: /home/user/.sonar/cache
INFO: Load/download plugins
INFO: Load plugins index
INFO: Load plugins index (done) | time=150ms
INFO: Load/download plugins (done) | time=827ms
INFO: Process project properties
INFO: Process project properties (done) | time=9ms
INFO: Execute project builders
INFO: Execute project builders (done) | time=2ms
INFO: Project key: netology
INFO: Base dir: /home/user/netology/9.2
INFO: Working dir: /home/user/netology/9.2/.scannerwork
INFO: Load project settings for component key: 'netology'
INFO: Load project settings for component key: 'netology' (done) | time=62ms
INFO: Load quality profiles
INFO: Load quality profiles (done) | time=158ms
INFO: Load active rules
INFO: Load active rules (done) | time=2674ms
WARN: SCM provider autodetection failed. Please use "sonar.scm.provider" to define SCM of your project, or disable the SCM Sensor in the project settings.
INFO: Indexing files...
INFO: Project configuration:
INFO:   Excluded sources for coverage: fail.py
INFO: 7 files indexed
INFO: Quality profile for py: Sonar way
INFO: Quality profile for xml: Sonar way
INFO: ------------- Run sensors on module netology
INFO: Load metrics repository
INFO: Load metrics repository (done) | time=103ms
INFO: Sensor Python Sensor [python]
INFO: Starting global symbols computation
INFO: 2 source files to be analyzed
INFO: Load project repositories
INFO: Load project repositories (done) | time=71ms
INFO: Starting rules execution
INFO: 2 source files to be analyzed
INFO: 2/2 source files have been analyzed
INFO: 2/2 source files have been analyzed
INFO: Sensor Python Sensor [python] (done) | time=5572ms
INFO: Sensor Cobertura Sensor for Python coverage [python]
INFO: Sensor Cobertura Sensor for Python coverage [python] (done) | time=8ms
INFO: Sensor PythonXUnitSensor [python]
INFO: Sensor PythonXUnitSensor [python] (done) | time=1ms
INFO: Sensor CSS Rules [cssfamily]
INFO: No CSS, PHP, HTML or VueJS files are found in the project. CSS analysis is skipped.
INFO: Sensor CSS Rules [cssfamily] (done) | time=0ms
INFO: Sensor JaCoCo XML Report Importer [jacoco]
INFO: 'sonar.coverage.jacoco.xmlReportPaths' is not defined. Using default locations: target/site/jacoco/jacoco.xml,target/site/jacoco-it/jacoco.xml,build/reports/jacoco/test/jacocoTestReport.xml
INFO: No report imported, no coverage information will be imported by JaCoCo XML Report Importer
INFO: Sensor JaCoCo XML Report Importer [jacoco] (done) | time=2ms
INFO: Sensor C# Properties [csharp]
INFO: Sensor C# Properties [csharp] (done) | time=1ms
INFO: Sensor JavaXmlSensor [java]
INFO: 3 source files to be analyzed
INFO: Sensor JavaXmlSensor [java] (done) | time=361ms
INFO: 3/3 source files have been analyzed
INFO: Sensor HTML [web]
INFO: Sensor HTML [web] (done) | time=3ms
INFO: Sensor XML Sensor [xml]
INFO: 3 source files to be analyzed
INFO: Sensor XML Sensor [xml] (done) | time=171ms
INFO: Sensor VB.NET Properties [vbnet]
INFO: 3/3 source files have been analyzed
INFO: Sensor VB.NET Properties [vbnet] (done) | time=1ms
INFO: ------------- Run sensors on project
INFO: Sensor Zero Coverage Sensor
INFO: Sensor Zero Coverage Sensor (done) | time=21ms
INFO: SCM Publisher No SCM system was detected. You can use the 'sonar.scm.provider' property to explicitly specify it.
INFO: CPD Executor Calculating CPD for 2 files
INFO: CPD Executor CPD calculation finished (done) | time=10ms
INFO: Analysis report generated in 82ms, dir size=97 KB
INFO: Analysis report compressed in 41ms, zip size=17 KB
INFO: Analysis report uploaded in 105ms
INFO: ANALYSIS SUCCESSFUL, you can browse http://localhost:9000/dashboard?id=netology
INFO: Note that you will be able to access the updated dashboard once the server has processed the submitted analysis report
INFO: More about the report processing at http://localhost:9000/api/ce/task?id=AYDXtT-z7eTjZ9n7Qceh
INFO: Analysis total time: 12.703 s
INFO: ------------------------------------------------------------------------
INFO: EXECUTION SUCCESS
INFO: ------------------------------------------------------------------------
INFO: Total time: 17.604s
INFO: Final Memory: 7M/30M
INFO: ------------------------------------------------------------------------
```
Смотрим результат в интерфейсе
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/sonar_qube_2.png)
Исправляем файл
```TEXT
def increment(index):
    index_new = index + 1
    return index_new
def get_square(numb):
    return numb*numb
def print_numb(numb):
    print("Number is {}".format(numb))

index = 0
while (index < 10):
    index = increment(index)
    print(get_square(index))
```
Ещё раз запускаем анализатор и смотрим результат в интерфейсе:
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/sonar_qube_3.png)
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/sonar_qube_4.png)

# 09.01 Жизненный цикл ПО
### В рамках основной части необходимо создать собственные workflow для двух типов задач: bug и остальные типы задач.
#### Workflow for bug
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/bug_workflow.png)
#### Workflow для остальных типов задач
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/workflow.png)
### Проведение задач по статусам в kanban
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/desk_kanban.png)
### Проведение задач по статусам в scrum
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/desk_sprint.png)
### Если всё отработало в рамках ожидания - выгрузить схемы workflow для импорта в XML. Файлы с workflow приложить к решению задания.
[bug_workflow.xml](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/bug_workflow.xml)

[workflow.xml](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/workflow.xml)
