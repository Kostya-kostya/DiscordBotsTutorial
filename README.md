# discordbotstut
Начнём. Ссылка на мой [youtube канал.](https://www.youtube.com/channel/UCHHBv4pqQWIMUuXIirVWmjg?view_as=subscriber) 
~~Если вы читаете это, то скорее всего первая часть туториала уже вышла.~~ Ещё не вышла.
### Discord bot туториал #1. Сделано к части туториала 1. (текстовый вариант)
###### Creation date : 06.12.2019

#### Установка [node.js](https://nodejs.org/en/).
Давайте начнём создание бота. Если у вас установлена node.js, то пропустите сделающие 2 строчки.
Заходим на сайт [node.js](https://nodejs.org/en/), скачиваем, устанавливаем. Скриншотов процесса установки нету, тк переустанавливать node.js нету желания. Но там всё интуитивно понятно.

#### Создание файлов, инициализация проекта, установка библиотек.
Создаём папку bot. Желательно не использовать кирилицу, юникод и т. п. в названии.
Сразу же создаём файл index.js или bot.js. Это не несёт особого смысла. Можно назвать как угодно, но принятно index.js / bot.js.
Это будет главный файл бота, т.е. первым запускается, в нём основной код бота.
Далее открываем консоль / терминал если у вас linux.
Для быстрого открытия консоли на windows можно нажать WIN + R, ввести cmd.
Далее переходим в папку бота, думаю как это сделать через консоль всем понятно. Пишим :
npm init - инициализация проекта.
Жмём enter до конца. Если ошибка в package name, то напишите bot.
npm i discord.js - установка библиотеки discord.js.
<br />
#### Редакторы кода.
Далее рекомендую установить один из следующих редакторов кода :
##### [Atom](https://atom.io/).
##### [VScode](https://code.visualstudio.com/).
Если очень слабый компьюер можете поставить [notepad++](https://notepad-plus-plus.org/downloads/), но это для постоянной основы не самый хороший вариант.
Лично я использую Atom.

#### Аккаунт бота.
Вы можете зарегистрировать его на сайте [discord developers](https://discordapp.com/developers/).
Жмём кнопку "New Application". Вводим название бота. Жмём "Create".
Переходим во вкладку "Bot", нажимаем "Add Bot", затем "Yes, do it!"
Находим строку "token", немного ниже есть кнопка "Copy", нажимаем. Теперь в вашем буфере обмена есть токен бота.

#### Код.
##### Начало.
Создадим первый код. Пишем : 
```javascript
const Discord = require("discord.js"); //Подключаем discord.js для дальнейшего использования.
const client = new Discord.Client(); 
client.login("token"); //Где token пишем токен бота.
```
##### Запуск.
Открываем консоль, переходим в папку проекта и пишем : 
```
node название-файла-с-кодом.js
```
в зависимости от названия файла. 
Если у вас windows, то вы можете создать файл start.bat с текстом 
```
node название-файла-с-кодом.js
pause
```
Это будет запускать бота. Далее я не буду говорить про запуск. Делайте это сами.
##### Конфиг.
После строк кода // обозначает комментарий. Текст после //Никак не влияет на код. Это пояснения для вас.
Ссоздадим переменную с конфигом бота.
```javascript
let config = { //Создаём литеральный объект.
version : "1.0", //Версия бота.
prefix : "!" //Префикс бота.
};
```
##### Реагирование на сообщение.
Теперь давайте делать что-то когда приходит новое сообщение.
Например логировать его текст.
```javascript
client.on("message", message => { //Пришло сообщение.
console.log(message.content); //console.log логирует в консоль, message - объект сообщения, message.content - строка объекта с текстом сообщения.
})
```
##### Получение информации о авторе сообщения (отправителе).
Давайте залогируем тег автора.
```javascript
client.on("message", message => { //Пришло сообщение.
console.log(message.author.tag); //message.author.tag содержит в себе тег автора.
})
```
##### Команда !ping
Давайте в ответ на сообщение !ping отправлять такое сообщение : "@user, мой пинг равен " далее пинг.
```javascript
client.on("message", message => { //Пришло сообщение.
if(message.content==config.prefix + "ping") //Если текст сообщения равен префиксу плюс ping, то происходит код в {}
{
message.reply("мой пинг равен " + client.ping) //message.reply отвечает на сообщение.
//Также можно использовать message.channel.send(message.author + ", мой пинг равен " + client.ping);
}
})
```
##### Об отправке сообщений.
Теперь рассмотрим message.channel.send();
Когда я только начинал программировать я не понимал смысл этой фразы, но сейчас понимаю и могу рассказать вам. message - объект сообщения, в нём есть channel - канал в который было отправлено, то есть с помощью message.channel мы получаем канал, а .send() отправляет туда сообщение.
```javascript
client.on("message", message => { //Пришло сообщение.
if(message.content==config.prefix + "test")
{
message.channel.send("I am working now!");
}
})
```
Также можно отправлять сообщение по ID канала.
Делается это так :
```
//some code...
client.channels.get('ID канала').send("Hi!");
```
client.channels - все каналы которые есть на серверах с ботом._
.get('ID') получает канал из них по ID._
.send("Text"); Отправляет сообщение._
Id канала можно получить используя [devepoer mode](https://discordia.me/en/developer-mode)

#### В разработке..
