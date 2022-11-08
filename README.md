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
   - Якщо у вас встановлено в VSCode плагін Docker:  
     ![This is an image](https://github.com/eugene-hliebov/readME_files/blob/main/docker_app_attach_shell.png)
   - Якщо ні, то в Docker Desktop, open terminal:  
     ![This is an image](https://github.com/eugene-hliebov/readME_files/blob/main/docker_app_open_terminall.png)
6. Вводимо команди:  
   ```
   npm i
   composer i
   
   ```
7. В кореневій папці safeua:
   ```
   npm install
   npm dev
   ```
8. Там же вводимо:
   ```
   npm run build
   ```
9. Далі знову відкриваємо термінал в контейнері app і пишемо:
   _Для перевірки_  
   ```
   php artisan migrate:rollback
   ```
   ```
   php artisan migrate
   ```
   
