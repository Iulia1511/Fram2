# Лабораторная работа №2
## Цель
* Изучить основные принципы работы с HTTP-запросами в Laravel и шаблонизацию с использованием Blade на основе веб-приложения To-Do App для команд — приложения для управления задачами внутри команды.
Приложение предназначено для команды, которая хочет управлять своими задачами, назначать их участникам, отслеживать статус и приоритет задач (похоже на Github Issues).
## Условие
### №1. Подготовка к работе, установка Laravel
* Откройте терминал и создайте новый проект Laravel с именем todo-app (имя проекта может быть любым) с помощью Composer: bash composer create-project laravel/laravel:^10 todo-app

![image](https://github.com/user-attachments/assets/07650063-d853-4a75-9915-9a370691f18b)

* Перейдите в директорию проекта: bash cd todo-app

![image](https://github.com/user-attachments/assets/cc424298-7dbd-4871-b282-96b8f3bc2df2)

* Запустите встроенный сервер Laravel: bash php artisan serve

![image](https://github.com/user-attachments/assets/08105535-39a6-4254-9d71-b42d7ba47a63)

* Вопрос: Что вы видите в браузере, открыв страницу http://localhost:8000?

![image](https://github.com/user-attachments/assets/cb9d6f1f-ce6e-4f4a-83de-a5c8fd6fa95a)

### №2. Настройка окружения
* Откройте файл .env и укажите следующие настройки приложения: ini APP_NAME=ToDoApp APP_ENV=local APP_KEY= APP_DEBUG=true APP_URL=http://localhost:8000

![image](https://github.com/user-attachments/assets/a91e6962-0461-4409-8995-118d4f88a384)

* Сгенерируйте ключ приложения, который будет использоваться для шифрования данных: bash php artisan key:generate 

![image](https://github.com/user-attachments/assets/60d0bf5d-016e-4786-8d3d-a161de77e55a)

*  Вопрос: Что будет, если данный ключ попадет в руки злоумышленника?

 #### Это может привести к:
* Доступу к зашифрованным данным (сессии, токены, данные в БД).
* Подделке данных (манипуляция куками, сессиями).
* Нарушению аутентификации пользователей.

### №3. Основы работы с HTTP-запросами
#### №3.1. Создание маршрутов для главной страницы и страницы "О нас"
Создайте класс-контроллер HomeController для обработки запросов на главную страницу.
![image](https://github.com/user-attachments/assets/c8db5cd7-0589-4f96-870a-586e0627a382)

* Добавьте метод index в HomeController, который будет отвечать за отображение главной страницы.

![image](https://github.com/user-attachments/assets/9121a3d2-57e4-4586-8a4f-a5bba033aa44)

* Создайте маршрут для главной страницы в файле routes/web.php. php public function index() { return view('home'); }

![image](https://github.com/user-attachments/assets/64f2a14a-575c-41cb-9af3-5dbf93fa1765)

* Откройте браузер и перейдите по адресу http://localhost:8000. Убедитесь, что загружается пустая страница, так как представление home.blade.php пока не создано.

![image](https://github.com/user-attachments/assets/9e343a8d-236f-4f7d-bbfd-bb4e66c71922)

 Показывает ошибку, так как такого представления еще нет

### При добавлении представления home.blade.php при запуске сервера будет выходить ее содержимое

![image](https://github.com/user-attachments/assets/70c683ec-a8f2-40fb-b953-50eb7d4b80ac)

* В этом же контроллере HomeController создайте метод для страницы "О нас".

![image](https://github.com/user-attachments/assets/8fcbdbf4-ee9e-46c8-96df-2f7b0ef4a7bb)

* Добавьте маршрут для страницы "О нас" в файле routes/web.php.

![image](https://github.com/user-attachments/assets/a9a66786-c2e8-4ae6-9207-914411cb88f2)

### Добавим представления,контент в них и переход между страницами.Теперь выглядит вот так: 

![image](https://github.com/user-attachments/assets/cc753366-33f7-4ed2-956a-469b0bd69bb8)

![image](https://github.com/user-attachments/assets/9fc0bd5f-fd76-4b2b-bb16-30b6c7752348)

#### №3.2. Создание маршрутов для задач

* Создайте класс-контроллер TaskController для обработки запросов, связанных с задачами, и добавьте следующие методы:

![image](https://github.com/user-attachments/assets/cd9a2d63-55ab-4c71-bb64-b12bbb494df4)

![image](https://github.com/user-attachments/assets/986b1d5b-e77b-45ab-a9a1-16165a78f5fd)

![image](https://github.com/user-attachments/assets/eb85dbf0-6dfe-4c2f-9765-81fca0205967)

* Используйте группирование маршрутов для контроллера TaskController с префиксом /tasks, чтобы упростить маршрутизацию и улучшить читаемость кода.
* Определите правильные имена маршрутов для методов контроллера TaskController, например:
tasks.index — список задач;
tasks.show — отображение отдельной задачи.
...
* Добавьте валидацию параметров маршрута id для задач. Убедитесь, что параметр id — это положительное целое число. Используйте метод where, чтобы ограничить значения для параметра id.

![image](https://github.com/user-attachments/assets/d59f484e-d763-4a2a-9c74-c1ca95998fdc)

* Вместо ручного создания маршрутов для каждого метода можно использовать ресурсный контроллер, который автоматически создаст маршруты для всех CRUD-операций:

![image](https://github.com/user-attachments/assets/ba9a78c1-2b50-480a-ad3e-6be3f8d8e9c5)

* Вопрос: Объясните разницу между ручным созданием маршрутов и использованием ресурсного контроллера. Какие маршруты и имена маршрутов будут созданы автоматически?
✅ Ручные маршруты дают полный контроль (можно настраивать URL, middleware и т. д.).
✅ Route::resource() удобен, когда нужны стандартные CRUD-маршруты.

* Проверьте созданные маршруты с помощью команды php artisan route:list.

![image](https://github.com/user-attachments/assets/3257c49f-7302-41a6-8d16-523b32c284cf)

## №4. Шаблонизация с использованием Blade
### 4.1. Создание макета страницы
*Создайте макет основных страниц layouts/app.blade.php с общими элементами страницы:
Используйте директиву @yield для определения области, в которую будут вставляться содержимое различных страниц.

![image](https://github.com/user-attachments/assets/f05b2590-0328-4312-83f2-a88919c399cd)

### №4.2. Использование шаблонов Blade
* Создайте представление для главной страницы home.blade.php с использованием макета layouts/app.blade.php в каталоге resources/views.

![image](https://github.com/user-attachments/assets/23b175d8-4f34-4d5d-98aa-874d3f8e63ad)

* Создайте представление для страницы "О нас" — about.blade.php с использованием макета layouts/app.blade.php в каталоге resources/views.

  ![image](https://github.com/user-attachments/assets/4ebd7198-9315-4cd6-bea4-e9209a950ec1)

* Создайте представления для задач со следующими шаблонами в каталоге resources/views/tasks:
### index.blade.php:

![image](https://github.com/user-attachments/assets/a31f2d06-c917-4642-9a91-5ea11ce4253f)

### show.blade.php:

![image](https://github.com/user-attachments/assets/93b67ebb-eac1-4924-a346-6e0defd4f022)


* Отрендерите список задач на странице index.blade.php с использованием статических данных, передаваемых из контроллера с помощью директивы @foreach.
![image](https://github.com/user-attachments/assets/fbbbcbee-4857-4c82-9772-e70184ab8c1d)

### №4.3. Анонимные компоненты Blade
 * Создайте анонимный компонент для отображения header. Используйте созданный компонент в макете layouts/app.blade.php.

   ![image](https://github.com/user-attachments/assets/0110bb3b-c9e3-48f9-b9bd-c83b115da8fb)

* Создайте анонимный компонент для отображения задачи
### app.blade.php:

```
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>@yield('title')</title> <!-- Здесь будет вставляться заголовок страницы -->
    <link rel="stylesheet" href="{{ asset('css/app.css') }}"> <!-- Подключаем стили -->
</head>
<body>
    <!-- Используем компонент header -->
    <x-header>{{ $title ?? 'To-Do App' }}</x-header> <!-- Заголовок страницы -->

    <!-- Меню навигации -->
    <header>
        <nav>
            <ul>
                <li><a href="{{ url('/') }}">Главная</a></li>
                <li><a href="{{ url('/about') }}">О нас</a></li>
                <li><a href="{{ route('tasks.index') }}">Список задач</a></li>
                <li><a href="{{ route('tasks.create') }}">Создать задачу</a></li>
            </ul>
        </nav>
    </header>

    <!-- Основной контент страницы -->
    <main>
        @yield('content') <!-- Здесь будет вставляться контент каждой страницы -->
    </main>

    <!-- Подвал -->
    <footer>
        <p>&copy; 2025 To-Do App. Все права защищены , я лично защищала.</p>
    </footer>
</body>
</html>
```
## Конечный результат 

![image](https://github.com/user-attachments/assets/038c62ed-4841-4fcc-925d-6690b6d9211d)

![image](https://github.com/user-attachments/assets/394e37cf-44fd-4f66-86dc-4e1748999f96)

![image](https://github.com/user-attachments/assets/e4833db7-cfbc-4a86-a3a6-4a56f817b3b9)

![image](https://github.com/user-attachments/assets/d9974323-fd5b-4277-b2c2-c0920a508682)

# Контрольные вопросы

#### Что такое ресурсный контроллер в Laravel и какие маршруты он создает?
* Ресурсный контроллер в Laravel — это контроллер, который автоматически создает стандартные методы для работы с CRUD-операциями (создание, чтение, обновление и удаление) для заданного ресурса. Ресурсный контроллер создает маршруты для следующих операций:
* index (GET) — отображение списка ресурсов.
* create (GET) — форма для создания нового ресурса.
* store (POST) — сохранение нового ресурса.
* show (GET) — отображение одного ресурса.
* edit (GET) — форма для редактирования ресурса.
* update (PUT/PATCH) — обновление ресурса.
* destroy (DELETE) — удаление ресурса.
#### Объясните разницу между ручным созданием маршрутов и использованием ресурсного контроллера.
* Ручное создание маршрутов подразумевает, что каждый маршрут нужно прописывать и связывать с конкретным методом контроллера. В случае с ресурсным контроллером, Laravel автоматически генерирует все необходимые маршруты для стандартных операций CRUD, упрощая работу разработчика и уменьшив количество кода.
#### Какие преимущества предоставляет использование анонимных компонентов Blade?
* Анонимные компоненты Blade позволяют создавать повторно используемые блоки кода, что помогает сократить дублирование. Это облегчает организацию кода и упрощает поддержку, так как компоненты можно легко внедрять и менять без необходимости изменять несколько файлов.
#### Какие методы HTTP-запросов используются для выполнения операций CRUD?
* Создание: POST
* Чтение: GET
* Обновление: PUT или PATCH
* Удаление: DELETE
