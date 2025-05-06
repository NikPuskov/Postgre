# Postgre

Цель домашнего задания: 

Научиться настраивать репликацию и создавать резервные копии в СУБД PostgreSQL

-------------------------------------------------------------------------------

Описание домашнего задания:

1. настроить hot_standby репликацию с использованием слотов

2. настроить правильное резервное копирование

-------------------------------------------------------------------------------

Выполнение домашнего задания:

- Создаем три виртуальные машины с настройками с помощью ansible:

`vagrant up` 

- Подключаемся к barman:

`vagrant ssh barman`

- Проверяем возможность подключения к postgres-серверу:

`psql -h 192.168.56.11 -U barman -d postgres`

- Проверяем репликацию:

`psql -h 192.168.56.11 -U barman -c "IDENTIFY_SYSTEM" replication=1`

![Image alt](https://github.com/NikPuskov/Postgre/blob/main/postgres1.jpg)

- Проверим работу barman:

`barman switch-wal node1`

`barman cron`

`barman check node1`

![Image alt](https://github.com/NikPuskov/Postgre/blob/main/postgres2.jpg)

- Запускаем резервную копию:

`barman backup node1`

![Image alt](https://github.com/NikPuskov/Postgre/blob/main/postgres3.jpg)

Проверка восстановления из бекапов:

- На хосте node1 в psql удаляем базы Otus:

![Image alt](https://github.com/NikPuskov/Postgre/blob/main/postgres4.jpg)

- На хосте barman запустим восстановление:

![Image alt](https://github.com/NikPuskov/Postgre/blob/main/postgres5.jpg)

- На хосте node1 потребуется перезапустить postgresql-сервер и снова проверить список БД. Базы otus должны вернуться обратно:

![Image alt](https://github.com/NikPuskov/Postgre/blob/main/postgres6.jpg)
