_Docker з Laravel від https://github.com/NTU-KhPI/safeua_

__Кроки встанолення:__
1. Створюємо будь-де папку, в ній відкриваємо PowerShell (Shift+RMB і там буде "Відкрити вікно PowerShell тут".
2. Клонуємо
   ```
   git clone git clone https://github.com/NTU-KhPI/safeua.git
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
   composer instal
   ```
   ```
   npm install
   ```
7. Відкриваємо термінал в папці safeua і вводимо:   
   ```
   npm run gulp-watch
   ```
   _Якщо не спрацьовує і виводиться текст - "gulp" не являєтся внутренной или внешенй командой..._  
   _то вводимо команду і повторюємо знову верхню команду_
   ```
   npm install --global gulp-cli
   ```
8. Відкриється в браузері сайт.  
   _Вітаю, у вас вийшло_  
     
   _Додадковий нюанс:_  
   Якщо ви зупиняєте докер і заново запускаєте, а при відкриванні сайту через localhost:3000 з'являється повідовленн "_Немає зв’язку із сайтом  
   Хост localhost відхилив запит на з’єднання._"  
   Слід повторити 7 крок.
