_Docker з Laravel від https://github.com/NTU-KhPI/safeua_

__Кроки встанолення:__
1. Створюємо будь-де папку, в ній відкриваємо PowerShell (Shift+RMB і там буде "Відкрити вікно PowerShell тут".
2. Клонуємо
   ```
   git clone https://github.com/NTU-KhPI/safeua.git
   ```
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
   npm dev
   ```
8. Там же вводимо:
   ```
   npm run build
   ```
9. Далі знову відкриваємо термінал в контейнері app і пишемо:  
   ```
   php artisan migrate
   ```
   _Якщо вже робили міграцію, бажано запустити rollback і заново запустити міграцію_  
   ```
   php artisan migrate:rollback
   ```
   
   
   
__Приложение -> http://localhost/__  
__phpMyAdmin -> http://localhost:8888/__
   
   
   
__Що, де і як можна змінювати!!!__
1. php-html сторінки: resource/views бажано створити свою папку для своїх сторінок. Файл обов'язково з роширенням .blade.php  
   нарпиклад media.blade.php і бажана верстка (загалом в таких файлах лежать main контенти):  
   ```php
   @extends('layout')

   @section('content')
       //ваш main
       <main>

       </main>
   @endsection
   ```
   в layout шаблон, що буде на всіх сторінках, тут можна підключати header і footer
   потім цим php-сторінками підключаємо власні під-посилання в route/wep.php:
   ```php
   // media для прикладу
   Route::get('/media', function () {
      return view('media');
      // у view ім'я файлю без розширення .blade.php
      // якщо сторінка в своїй папці у resource/views, то перед ім'я пишіть вашу папку
   });
   ```
   
3. Стилі: в resource/css бажано створити свою папку і в файл app.css в resource/css робити імпортування ваших стилів. Наприклад:
   ```css
   @import "home/styles.css";
   ```
   






