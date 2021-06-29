## Июль 2021 года
## Коспект по общим знаниям для frontend разработки

### HTTP-запрос
HTTP — широко распространённый протокол передачи данных, изначально предназначенный для передачи гипертекстовых документов (то есть документов, которые могут содержать ссылки, позволяющие организовать переход к другим документам).  

Аббревиатура HTTP расшифровывается как HyperText Transfer Protocol, «протокол передачи гипертекста». В соответствии со спецификацией OSI, HTTP является протоколом прикладного (верхнего, 7-го) уровня.

Протокол HTTP предполагает использование клиент-серверной структуры передачи данных. Клиентское приложение формирует запрос и отправляет его на сервер, после чего серверное программное обеспечение обрабатывает данный запрос, формирует ответ и передаёт его обратно клиенту. После этого клиентское приложение может продолжить отправлять другие запросы, которые будут обработаны аналогичным образом.  

Задача, которая традиционно решается с помощью протокола HTTP — обмен данными между пользовательским приложением, осуществляющим доступ к веб-ресурсам (обычно это веб-браузер) и веб-сервером. На данный момент именно благодаря протоколу HTTP обеспечивается работа Всемирной паутины.  

#### Из чего состоит
HTTP запрос состоит из трех основных частей, которые идут в нем именно в том порядке, который указан ниже. Между заголовками и телом сообщения находится пустая строка (в качестве разделителя), она представляет собой символ перевода строки.


1. строка запроса (Request Line)  

2. заголовки (Message Headers)  

Пустая строка (разделитель)  

3. тело сообщения (Entity Body) – необязательный параметр  

Строка запроса – указывает метод передачи, URL-адрес, к которому нужно обратиться и версию протокола HTTP.  

Заголовки – описывают тело сообщений, передают различные параметры и др. сведения и информацию.  

Тело сообщения  - это сами данные, которые передаются в запросе.  Тело сообщения – это необязательный параметр и может отсутствовать.  

### Cookie
Cookie (куки) — небольшой фрагмент данных, который отправляется веб-сервером и хранится на компьютере пользователя.  

Принцип работы достаточно простой. Когда вы заходите на сайт, сервер отправляет не только данные о странице, но и файл куки. Он записывается непосредственно на ваш компьютер, как правило, в рабочих файлах самого браузера. По мере того, как вы ходите по сайту, файл дополняется различной информацией. Если вы повторно зайдете на этот сайт, браузер отправит серверу cookie, благодаря чему сайт «узнает» вас.  