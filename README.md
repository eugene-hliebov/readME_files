__Кроки встанолення:__
1. Створюємо будь-де папку, в ній відкриваємо PowerShell (Shift+RMB і там буде "Відкрити вікно PowerShell тут".
2. Клонуємо
    _Основна гілка main і додвання гілки і початку main_
   ```
   git clone https://github.com/NTU-KhPI/safeua.git
   ```
   ```
   git branch your-branch
   ```
   _ скрізь замість your-branch пишите вашу вигадану гілку наприклад прізвище і група - hliebov-kn1020b, Щоб інші розуміли чия гілка_  
   ```
   git checkout your-branch
   ```
   _!!!Коміти робити тільки в своїй гілці!!!_  
   _+ якщо ви хочете продовжити працю із моїми змінами, треба запулить мою гілку і об'єднати зі своїю гілкою гілку hliebov-branch, команди навдено нижче_  
   _якщо ви хочете з нуля, не пишіть ці команди, а просто переходьте далі по крокам_
   ```
   git checkout main
   ```
   ```
   git pull origin hliebov-kn1020b
   ```
   ```
   git checkout your-branch
   ```
   ```
   git merge main
   ```
   </br>
   </br>  
   
   _Коли зробили ви зміни, щось добавили і хочете загрузи зміни в свою гілку на github_  
   _не забудьте про крапку після add_  
   ```
   git checkout your-branch
   ```
   ```
   git add .
   ```
   ```
   git commit -m "тут пишете дію або зміну, яку ви зробили бажано на англійському і англійскьми літерами"
   ```
   ```
   git push --set-upstream origin your-branch
   ```
   </br>
   </br>
   </br>
3. В папках safeua і .docker копіювати файли .env.example в .env
4. В папці .docker відкриваємо PowerShell і вводимо команду:
   ```
   docker compose up 
   ```
   _Якщо у вас відкривається вікно, що наведнео нижче, нажимайте Share it_  
   ![This is an image](https://github.com/eugene-hliebov/readME_files/blob/main/Docker%20Desktop%20Filesharing.png)
5. Після завершення, відкриваємо термінал в контейнері app:
   Якщо у вас встановлено в VSCode плагін Docker:  
   ![This is an image](https://github.com/eugene-hliebov/readME_files/blob/main/docker_app_attach_shell.png)  
   Якщо ні, то в Docker Desktop, open terminal:  
   ![This is an image](https://github.com/eugene-hliebov/readME_files/blob/main/docker_app_open_terminall.png)  
6. Вводимо команди:  
   ```
   npm i
   ```
   ```
   composer i   
   ```
7. В кореневій папці safeua:
   ```
   npm install
   ```
   ```
   npm run build
   ```
   ```
   npm run dev
   ```
8. Міграція таблиц, знову відкриваємо термінал в контейнері app і пишемо:  
   ```
   php artisan migrate
   ```
   
   
   
Веб-застосунок -> http://localhost/  
phpMyAdmin -> http://localhost:8888/
</br>
</br>
</br>
__Що, де і як можна змінювати!!!__
1. php сторінки: resource/views бажано створити свою папку для своїх сторінок. Файл обов'язково з роширенням .blade.php  
   нарпиклад media.blade.php і бажана верстка (загалом в таких файлах лежать main контенти):  
   _Сторінки для не авторизованих, гостей_
   ```blade
   <x-guest-layout>
      Ваш hmtl, що в лежить в тегі main
   </x-guest-layout>
   ```
   _Для авторизованих_
   ```blade
   <x-app-layout>
      Ваш hmtl, що в лежить в тегі main
   </x-app-layout>
   ```
   _!!!але якщо в php-сторікнах у вас будуть умови, що перевіряють чи авторизованих чи ні, то різниця у використанні практично не буде між x-app-layout і x-quest-layout!!!_

   в app і quest шаблони (/resources/views/layouts/), тут можна підключати header, footer і нші php шаблони 
   ```blade
   <!DOCTYPE html>
   <html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
      <head>
         <meta charset="utf-8">
         <meta name="viewport" content="width=device-width, initial-scale=1">
         <meta name="csrf-token" content="{{ csrf_token() }}">

         <title>{{ config('app.name', 'Laravel') }}</title>
         //бажано підключити bootstrap 4, щб не посипалась верстка, на тих сторінках де написано на bootstrap
         <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.1/dist/css/bootstrap.min.css">
         

         <!-- Scripts -->
         @vite(['resources/css/app.css', 'resources/js/app.js'])
      </head>
      <body class="font-sans antialiased">
         <div class="min-h-screen bg-gray-100">
               @include('tmp.header')

               <!-- Page Content -->
               <main>
                  {{ $slot }} // якраз буде підставлятись ваш php
               </main>
         </div>
         
         //бажано підключити bootstrap 4, щб не посипалась верстка, на тих сторінках де написано на bootstrap
         <script src="https://cdn.jsdelivr.net/npm/jquery@3.6.0/dist/jquery.slim.min.js"></script>
         <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js"></script>
         <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.1/dist/js/bootstrap.bundle.min.js"></script>
      </body>
   </html>
   ```
   потім цим php-сторінками підключаємо власні під-посилання в route/wep.php:
   ```blade
   // media для прикладу
   Route::get('/media', function () {
      return view('media');
      // у view ім'я файлю без розширення .blade.php
      // якщо сторінка в своїй папці у resource/views, то перед ім'я пишіть вашу папку
   });
   ```
   
3. Стилі css: в resource/css бажано створити свою папку і в файл app.css в resource/css робити імпортування ваших стилів. Наприклад:
   ```css
   @import "home/styles.css";
   ```
4. Js: в resource/js бажано створити свою папку і в файл app.js в resource/css робити імпортування ваших js. Наприклад:
   ```js
   import './ваша_папка/ваш_js';
   // js файл в імпорті без .js
   ```
5. _P.S. можливо я неправильно зрозумів, куди кидати img, але мій варіант все ж таки також працює_  
   Img: в public/img бажано створити свою папку і туди можливо закидувати ваші img. Приклад підключення зображень:
   ```html
   <img src="../img/ваша_папка/ваше_зображення.розширення" alt="">
   ```
</br>
</br>
</br>  

Мій приклад створення таблиці на основі PhotoArchives (УВАЖНО):  
1. Створення моделі файлу та налаштування міграцій (відкрити термінал в контейнері app)
    ```
    php artisan make:model PhotoArchives -m
    ```
2. Далі відкрийте файл міграції для визначення значень таблиці в базі даних для зберігання інформації про завантажений файл. Перейдіть до файлу database/migrations/......_create_photo_archives_table і визначте значення таблиці.
    ```php
    <?php

    use Illuminate\Database\Migrations\Migration;
    use Illuminate\Database\Schema\Blueprint;
    use Illuminate\Support\Facades\Schema;

    return new class extends Migration
    {
        /**
         * Run the migrations.
         *
         * @return void
         */
        public function up()
        {
            Schema::create('photo_archives', function (Blueprint $table) {
                $table->id();
                $table->timestamps();
                $table->integer('user_id');
                $table->string('filename');
                $table->string('origin');
                $table->text('description')->nullable();
                $table->text('region')->nullable();
                $table->integer('count_likes')->nullable();
                $table->integer('count_complains')->nullable();
                $table->boolean('shadow_ban')->default(false);
            });
        }

        /**
         * Reverse the migrations.
         *
         * @return void
         */
        public function down()
        {
            Schema::dropIfExists('photo_archives');
        }
    };
    ```
3. Тепер додайте властивість $fillable у модель File. Відкрийте файл app/Models/PhotoArchives.php і розмістіть наступний код.
    ```php
    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Factories\HasFactory;
    use Illuminate\Database\Eloquent\Model;

    class PhotoArchives extends Model
    {
        use HasFactory;
        protected $fillable = [
            'user_id',
            'filename',
            'origim',
            'description',
            'region',
            'count_likes',
            'count_complains',
            'shadow_ban'
        ];
    }
    ```
4. Тепер ви готові до запуску міграції. Ви також можете побачити оновлення в базі даних mysql.
    ```
    php artisan migrate
    ```
5. Створимо контролер завантаження файлів.В папці app/Http/Controllers створимо свою паппу в PhotoArchives. Далі Виконайте команду для створення контролера.
    ```
    php artisan make:controller PhotoArchives/PhotoUploadController --resource
    ```
    Відкрийте файл app/Http/Controllers/FileUpload.php , і нам потрібно визначити логіку для завантаження, зберігання, редагування, оновлення і видалення данних:
    -   Підключаємо модель
        ```php
        use App\Models\PhotoArchives;
        ```
    -   в index()
        ```php
        public function index()
        {
            $photos = PhotoArchives::all();
            return view('/test', compact('photos'));
        }
        ```
    -   в store() (для вашої таблиці, те в функції може бути інше, все залежить, що ви хочете завантажити у таблицю)
        ```php
        public function store(Request $request)
        {
            $request->validate([
                'image' => 'required|image|mimes:png,jpg,jpeg|max:1024',
                'user_id' => 'required|numeric',
                'description' => 'required|max:255',
                'region' => 'required|max:255'
            ]);

            $imageRequest = $request->image;
            $file_path = $imageRequest->hashName();
            $imageRequest->move(public_path('img/test'), $imageRequest->hashName());
            // $file_path = $imageRequest->hashName();


            $image = new PhotoArchives();
            $image->user_id = $request->user_id;
            $image->filename = $file_path;
            $image->origin = $imageRequest->getClientOriginalName();
            $image->description = $request->description;
            $image->region = $request->region;
            $image->save(); 

            return back()->with('success', 'Image uploaded Successfully!');
        }
        ``` 
6. Додаємо наступний код у файл routes/web.php:
    ```php
    use App\Http\Controllers\PhotoArchives\PhotoUploadController;
    Route::resource('test', PhotoUploadController::class);
    ```
7. Запустити наступну команду в констайнері app, щоб створити різні маршрути для нашої програми CRUD.
    ```
    php artisan route:list
    ```
8. Створюємо test.blade.php і додаємо приблизно такий код:
    ```blade
    <x-guest-layout>
        <div class="container">
            <h1>test photos</h1>
            @if (Route::has('login')) // перевірка чи авторизований користувач
                @auth
                    <p>your ID: {{ Auth::user()->id }}</p> // вивід ID user
                    <div>
                            // в input name пишемо ті значення, що записали в валідації
                            //$request->validate([
                            //    'image' => 'required|image|mimes:png,jpg,jpeg|max:1024',
                            //    'user_id' => 'required|numeric',
                            //    'description' => 'required|max:255',
                            //    'region' => 'required|max:255'
                            //]);
                        <form method="POST" action="{{ route('test.store') }}" enctype="multipart/form-data"> // запускається функція store()
                            @csrf
                            
                            
                            <label for="image">Завантажити фото</label>
                            <input type="file" class="form-control" name="image" /> <br>
                            <label for="user_id">User Id</label>
                            <input type="number" class="form-control " name="user_id" value="{{ Auth::user()->id }}" readonly/><br>
                            <label for="user_id">Description</label>
                            <input type="text" class="form-control" name="description" /><br>
                            <label for="user_id">Region</label>
                            <input type="text" class="form-control" name="region" /><br>
                            <button type="submit" class="btn btn-sm">Upload</button>
                        </form>        
                    </div>
                    <div>
                        @if ($photos->count())
                            <div>
                                @foreach ($photos as $image)
                                    <img height="30" src="{{ asset('img/test/'.$image->filename) }}" /></br>
                                @endforeach
                            </div>
                        @else
                            <p class="text-center">No images yet. Please check back later.</p>
                        @endif
                    </div>
                @endauth
            @endif
        </div>
    </x-guest-layout>
    ```
9. Якщо зображення або файл не заваньажується і видає помилку 413 Request Entity Too Large, то .docker/nginx/conf.d/default.conf додати змінну client_max_body_size,яка може змінювати розмір завантажуваного файлу в Nginx. (наприклад збільшити до 100M)
    ```php
    server {
    client_max_body_size 100M;
    ...
    ...
    }
    ```



