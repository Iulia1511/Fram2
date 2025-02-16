# Лабораторная работа №2
## Цель
* Изучить основные принципы работы с HTTP-запросами в Laravel и шаблонизацию с использованием Blade на основе веб-приложения To-Do App для команд — приложения для управления задачами внутри команды.
Приложение предназначено для команды, которая хочет управлять своими задачами, назначать их участникам, отслеживать статус и приоритет задач (похоже на Github Issues).
## Условие
### №1. Подготовка к работе, установка Laravel
Откройте терминал и создайте новый проект Laravel с именем todo-app (имя проекта может быть любым) с помощью Composer: bash composer create-project laravel/laravel:^10 todo-app

![image](https://github.com/user-attachments/assets/07650063-d853-4a75-9915-9a370691f18b)

Перейдите в директорию проекта: bash cd todo-app

![image](https://github.com/user-attachments/assets/cc424298-7dbd-4871-b282-96b8f3bc2df2)

Запустите встроенный сервер Laravel: bash php artisan serve

![image](https://github.com/user-attachments/assets/08105535-39a6-4254-9d71-b42d7ba47a63)

Вопрос: Что вы видите в браузере, открыв страницу http://localhost:8000?

![image](https://github.com/user-attachments/assets/cb9d6f1f-ce6e-4f4a-83de-a5c8fd6fa95a)

### №2. Настройка окружения
Откройте файл .env и укажите следующие настройки приложения: ini APP_NAME=ToDoApp APP_ENV=local APP_KEY= APP_DEBUG=true APP_URL=http://localhost:8000

![image](https://github.com/user-attachments/assets/a91e6962-0461-4409-8995-118d4f88a384)

Сгенерируйте ключ приложения, который будет использоваться для шифрования данных: bash php artisan key:generate 

![image](https://github.com/user-attachments/assets/60d0bf5d-016e-4786-8d3d-a161de77e55a)

 Вопрос: Что будет, если данный ключ попадет в руки злоумышленника?

 #### Это может привести к:
* Доступу к зашифрованным данным (сессии, токены, данные в БД).
* Подделке данных (манипуляция куками, сессиями).
* Нарушению аутентификации пользователей.



