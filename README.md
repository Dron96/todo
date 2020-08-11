# API для To-Do List

### Стек
1. PHP 7.4.3
2. Laravel 7.21
3. PostgreSQL 12.3

###Как начать:
1. Установка PHP 7.4: <br>
```
sudo apt install php7.4
```
2. Установка зависимостей: <br>
```
sudo apt install php-mysql php-mbstring php-tokenizer php-xml php-json php-common
```
3. Установка Composer: <br>
```
sudo apt install composer
```
4. Переместимся в папку, где храняться веб-сайты: <br>
```
cd /var/www/sites
```
5. Установим проект из репозитория: <br>
```
git clone https://github.com/Dron96/todo.git
```
6. Изменим владельца директории: <br>
```
sudo chown -R www-data:www-data todo
```
7. Настроим базу данных: <br>
Подключитесь к базе данных и создайте новую таблицу: <br>
```
$ sudo mysql -u root -p
> CREATE DATABASE laravel;
```
Затем создайте пользователя для этой базы данных и дайте ему все права на неё: <br>
```
> CREATE USER `laravel_user`@`localhost` IDENTIFIED BY 'password';
> GRANT ALL ON laravel.* TO `laravel_user`@`localhost`;
```
Далее обновите таблицу привилегий: <br>
```
> FLUSH PRIVILEGES;
```
По умолчанию Laravel настроен на использование  нужной нам базы данных, но вам надо указать правильные
 параметры доступа к ней. Откройте файл config/database.php и найдите там секцию mysql: <br>
```shell
vi config/database.php
```
![](https://losst.ru/wp-content/uploads/2019/04/Snimok-ekrana-ot-2019-04-07-21-20-37.png)
7. Запуск проекта:
```shell
php artisan serve
```
`ГОТОВО!`

### Описание:

#### Операции над списком списков:
|#  | Описание операции                            | URL             | Метод запроса | Параметры                 |
|---|----------------------------------------------|-----------------|:-------------:|---------------------------|
|1. | Получение списка всех списков списков        | /api/lists      | GET / HEAD    | Нет параметров            |
|2. | Создание списка списков                      | /api/lists      | POST          | name - имя списка списков |
|3. | Изменение имеющегося списка списков          | /api/lists/{id} | PUT / PATCH   | name - имя списка списков |
|4. | Получение списков, входящих в список списков | /api/lists/{id} | GET / HEAD    | Нет параметров            |
|5. | Удаление списка списков со всеми вложениями  | /api/lists/{id} | DELETE        | Нет параметров            |

#### Операции над списком дел:
|#    | Описание операции                              | URL            | Метод запроса | Параметры                 |
|:---:|------------------------------------------------|----------------|:-------------:|---------------------------|
|1.   | Получение всех списков дел                     | /api/list      | GET / HEAD    | Нет параметров            |
|2.   | Создание списка дел                            | /api/list      | POST          | <ol><li>name - имя списка</li> <li>list_id - ID списка, к которому относится дело </li></ol>|
|3.   | Изменение имеющегося списка дел                | /api/list/{id} | PUT / PATCH   | <ol><li>name - имя списка</li> <li>list_id - ID списка, к которому относится дело </li></ol>|
|4.   | Получение дел, входящих в список дел           | /api/list/{id} | GET / HEAD    | Нет параметров            |
|5.   | Удаление списка дел со всеми вложенными делами | /api/list/{id} | DELETE        | Нет параметров            |

#### Операции над делом:
|#    | Описание операции         | URL            | Метод запроса | Параметры                 |
|:---:|---------------------------|----------------|:-------------:|---------------------------|
|1.   | Получение всех дел        | /api/item      | GET / HEAD    | Нет параметров            |
|2.   | Создание дела             | /api/item      | POST          | <ol><li>name - имя дела</li> <li>description - описание дела</li> <li>complete - завершено или нет</li> <li>urgency - срочность дела</li> <li>list_id - ID списка дел, к которому относится дело </li></ol>|
|3.   | Изменение имеющегося дела | /api/item/{id} | PUT / PATCH   | <ol><li>name - имя дела</li> <li>description - описание дела</li> <li>complete - завершено или нет</li> <li>urgency - срочность дела</li> <li>list_id - ID списка дел, к которому относится дело </li></ol>|
|4.   | Получение дела            | /api/item/{id} | GET / HEAD    | Нет параметров            |
|5.   | Удаление дела             | /api/item/{id} | DELETE        | Нет параметров            |


