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

@extends('layouts.app')

@section('title', 'Список задач')

@section('content')
    <h1>Список задач</h1>

    @foreach ($tasks as $task)
        <div>
            <h3>{{ $task['title'] }}</h3>
            <p>Статус: {{ $task['status'] }}</p>
            <a href="{{ route('tasks.show', $task['id']) }}">Посмотреть задачу</a>
        </div>
    @endforeach
@endsection

### show.blade.php:

@extends('layouts.app')
@section('title', 'Задача: {{ $task["title"] }}')
@section('content')
    <h1>{{ $task['title'] }}</h1>
    <p>Описание: {{ $task['description'] }}</p>
    <p>Статус: {{ $task['status'] }}</p>
    <p>Дата создания: {{ $task['created_at'] }}</p>
    <p>Дата обновления: {{ $task['updated_at'] }}</p>
    <p>Приоритет: {{ $task['priority'] }}</p>
    <p>Исполнитель: {{ $task['assigned_to'] }}</p>
@endsection
@extends('layouts.app')
@section('title', 'Задача: {{ $task["title"] }}')
@section('content')
    <x-task :task="$task"></x-task>
@endsection
