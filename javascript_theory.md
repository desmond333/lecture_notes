## Март 2022 года
## Коспект по теории Javascript для frontend разработки

## Введение
### ECMAScript
ECMAScript — это встраиваемый расширяемый не имеющий средств ввода-вывода язык программирования, используемый в качестве основы для построения других скриптовых языков. Стандартизирован международной организацией ECMA в спецификации ECMA-262. Расширения языка: JavaScript, JScript и ActionScript.  
Последняя версия - EcmaScript 10 (ES2019). Добавили `BigInt` для использования чисел произвольной точности и многое другое.

### JavaScript  
JavaScript — мультипарадигменный язык программирования. Поддерживает объектно-ориентированный, императивный и функциональный стили. Является реализацией спецификации ECMAScript (стандарт ECMA-262).  
JavaScript обычно используется как встраиваемый язык для программного доступа к объектам приложений. Наиболее широкое применение находит в браузерах как язык сценариев для придания интерактивности веб-страницам.  
Основные архитектурные черты: динамическая типизация, слабая типизация, автоматическое управление памятью, прототипное программирование, функции как объекты первого класса.

### Node.js
Node.js — программная платформа, основанная на движке V8 (транслирующем JavaScript в машинный код), превращающая JavaScript из узкоспециализированного языка в язык общего назначения. Node.js добавляет возможность JavaScript взаимодействовать с устройствами ввода-вывода через свой API, написанный на C++, подключать другие внешние библиотеки, написанные на разных языках, обеспечивая вызовы к ним из JavaScript-кода. Node.js применяется преимущественно на сервере, выполняя роль веб-сервера, но есть возможность разрабатывать на Node.js и десктопные оконные приложения (при помощи NW.js, AppJS или Electron для Linux, Windows и macOS) и даже программировать микроконтроллеры (например, tessel, low.js и espruino). В основе Node.js лежит событийно-ориентированное и асинхронное (или реактивное) программирование с неблокирующим вводом/выводом.  

### Строгий режим — "use strict"
Директива выглядит как строка: `"use strict"` или `'use strict'`. Когда она находится в начале скрипта, весь сценарий работает в «современном» режиме.  
Обратите внимание, что `use strict` в консоли по умолчанию выключен.  
Современный JavaScript поддерживает «классы» и «модули» — продвинутые структуры языка (и мы, конечно, до них доберёмся), которые автоматически включают строгий режим. Поэтому в них нет нужды добавлять директиву `"use strict"`.

## Основы
[Хорошее видео с теорией](https://www.youtube.com/watch?v=gV6eobXisYU&t=1102s&ab_channel=UlbiTV)

### Типы данных
В JavaScript есть 8 основных типов.
1.) `number` для любых чисел: целочисленных или чисел с плавающей точкой; целочисленные значения ограничены диапазоном ±(253-1).  
2.) `bigint` для целых чисел произвольной длины.  
3.) `string` для строк. Строка может содержать ноль или больше символов, нет отдельного символьного типа.  
4.) `boolean` для `true/false`.  
5.) `symbol` для уникальных идентификаторов.  
6.) `null` для неизвестных значений – отдельный тип, имеющий одно значение `null`.  
7.) `undefined` для неприсвоенных значений – отдельный тип, имеющий одно значение `undefined`.  
8.) `object` для более сложных структур данных.  

Оператор `typeof` позволяет нам увидеть, какой тип данных сохранён в переменной.  
• Имеет две формы: `typeof x` или `typeof(x)`.  
• Возвращает строку с именем типа. Например, "string".  
• Для `null` возвращается `"object"` – это ошибка в языке, на самом деле это не объект.  

### Операторы
Оператор ИЛИ  
При выполнении ИЛИ || с несколькими значениями:  
`result = value1 || value2 || value3;`  

Оператор || выполняет следующие действия:
1.) Вычисляет операнды слева направо.  
2.) Каждый операнд конвертирует в логическое значение. Если результат `true`, останавливается и возвращает исходное значение этого операнда.  
3.) Если все операнды являются ложными (`false`), возвращает последний из них.  

Значение возвращается в исходном виде, без преобразования.
Другими словами, цепочка ИЛИ "||" возвращает первое истинное значение или последнее, если такое значение не найдено.  
```javascript
let currentUser = null;    
let defaultUser = "John";   
let name = currentUser || defaultUser || "unnamed";    
alert( name ); // выбирается "John" – первое истинное значение  
```

Оператор && выполняет следующие действия:  
1.) Вычисляет операнды слева направо.  
2.) Каждый операнд преобразует в логическое значение. Если результат false, останавливается и возвращает исходное значение этого операнда.  
3.) Если все операнды были истинными, возвращается последний.  

Другими словами, И возвращает первое ложное значение. Или последнее, если ничего не найдено.  
Можно передать несколько значений подряд. В таком случае возвратится первое «ложное» значение, на котором остановились вычисления.  
`alert( 1 && 2 && null && 3 ); // null`    

Когда все значения верны, возвращается последнее  
`alert( 1 && 2 && 3 ); // 3`   

Приоритет операторов  
Приоритет 	Название 	Обозначение  
… 	… 	…  
17 	унарный плюс 	+  
17 	унарный минус 	-  
16 	возведение в степень 	**  
15 	умножение 	*  
15 	деление 	/  
13 	сложение 	+  
13  вычитание 	-  
… 	… 	…  
6  логическое И  &&  
5  логическое ИЛИ  ||  
3 	присваивание 	=  
… 	… 	…  

## Объекты
### Объекты
```javascript
let user = new Object(); // синтаксис "конструктор объекта"     
let user = {};  // синтаксис "литерал объекта"  
```  

Нет никаких ограничений к именам свойств. Они могут быть в виде строк, символов, специальных зарезервированных слов.  
Все другие типы данных будут автоматически преобразованы к строке. Например, если использовать число 0 в качестве ключа, то оно превратится в строку "0".  
// Имя свойства может состоять из нескольких слов, но тогда оно должно быть заключено в кавычки  
`"user age"`    
// присваивание значения свойству объекта через квадратные скобки  
`user["user age"] = true;`     
// удаление свойства объекта через квадратные скобки  
`delete user["user age"];`    

Объект, объявленный через `const`, может быть изменён. Определение `const` выдаст ошибку только если мы присвоим переменной другое значение:  
`user = 123 //ошибка`  

Вместо name:name мы можем написать просто name: 
```javascript
function makeUser(name, age) {   
  return {  
    name, // то же самое, что и name: name  
    age   // то же самое, что и age: age  
  };  
}  
``` 

Дополнительные операторы:  
• Удаление свойства: `delete obj.prop`  
• Проверка существования свойства: `"key" in obj. //вернет true or false`  
• Перебор свойств объекта с помощью цикла `for`, синтаксис: `for (let key in obj){}`  
```javascript
for (let key in user) {  
  // выведем все ключи объекта  
  alert( key );  // name, age, isAdmin  
  // выведем все значения ключей объекта  
  alert( user[key] ); // John, 30, true  
}  
```


### Копирование объектов и ссылки
Операторы равенства == и строгого равенства === для объектов работают одинаково.  
Два объекта равны только в том случае, если это один и тот же объект.  

Для «простого клонирования» объекта можно использовать `Object.assign`. Необходимо помнить, что `Object.assign` не делает глубокое клонирования объекта. Если внутри копируемого объекта есть свойство, значение которого не является примитивом, оно будет передано по ссылке. Для создания «настоящей копии» (полного клона объекта) можно воспользоваться методом из сторонней JavaScript-библиотеки cloneDeep(obj).  

### Сборка мусора
Мусор — это любой объект, к которому невозможно пройти по ссылке от «корня». К мусору относятся все «мертвые объекты», которые утратили связь с корневым.  
• Сборка мусора выполняется автоматически. Мы не можем ускорить или предотвратить её.  
• Объекты сохраняются в памяти, пока они достижимы.  
• Наличие ссылки не гарантирует, что объект достижим (от корня): несколько взаимосвязанных объектов могут стать недостижимыми как единое целое.  

Основной алгоритм сборки мусора – «алгоритм пометок» (англ. «mark-and-sweep»).  
Согласно этому алгоритму, сборщик мусора регулярно выполняет следующие шаги:  
• Сборщик мусора «помечает» (запоминает) все корневые объекты.  
• Затем он идёт по их ссылкам и помечает все найденные объекты.  
• Затем он идёт по ссылкам помеченных объектов и помечает объекты, на которые есть ссылка от них. Все объекты запоминаются, чтобы в будущем не посещать один и тот же объект дважды.  
• …И так далее, пока не будут посещены все ссылки (достижимые от корней).  
• Все непомеченные объекты удаляются. Вполне возможна ситуация, при которой целый «остров» связанных объектов может стать недостижимым и удалиться из памяти.  


### Методы объекта, "this"
Для доступа к информации внутри объекта метод может использовать ключевое слово `this`. Например, `this.state`. Значение `this` – это объект «перед точкой», который использовался для вызова метода. В JS "this" не является фиксированным, значение `this` вычисляется во время выполнения кода и зависит от контекста.  
Когда функция вызывается синтаксисом «метода» – `object.method()`, значением `this` во время вызова является объект перед точкой.  

`alert(this) //вызов this без объекта`  

В строгом режиме ("use strict") в таком коде значением `this` будет являться `undefined`. Если мы попытаемся получить доступ к `name`, используя `this.name` – это вызовет ошибку.  
В нестрогом режиме значением this в таком случае будет глобальный объект (window для браузера, мы вернёмся к этому позже в главе Глобальный объект). Это – исторически сложившееся поведение `this`, которое исправляется использованием строгого режима ("use strict").  

Некоторые хитрые способы вызова метода приводят к потере значения `this`, например:  
```javascript
let user = {  
  name: "Джон",  
  hi() { alert(this.name); },  
  bye() { alert("Пока"); }  
};  
user.hi(); // Джон (простой вызов метода работает хорошо)  
//попробуем вызывать user.hi или user.bye в зависимости от имени пользователя user.name  
(user.name == "Джон" ? user.hi : user.bye)();  
// Ошибка! Так уже не работает (так как вызываемый метод вычисляется). 
```
Стрелочные функции особенные: у них нет своего «собственного» this. Если мы используем this внутри стрелочной функции, то его значение берётся из внешней «нормальной» функции.  

### Конструкторы, создание объектов через "new"  
При помощи функции-конструктора и оператора "new" можно создать множество однотипных объектов, таких как пользователи, элементы меню и т.д.  

Функции-конструкторы являются обычными функциями. Но есть два соглашения:  
1.) Имя функции-конструктора должно начинаться с большой буквы.  
2.) Функция-конструктор должна вызываться при помощи оператора "new".  

Когда функция вызывается как `new User(...)`, происходит следующее:  
1.) Создаётся новый пустой объект, и он присваивается `this`.  
2.) Выполняется код функции. Обычно он модифицирует `this`, добавляет туда новые свойства.  
3.) Возвращается значение `this`.  

Другими словами, вызов `new User(...)` делает примерно вот что:  
```javascript
function User(name) {  
  // this = {};  (неявно)  
  // добавляет свойства к this  
  this.name = name;  
  this.isAdmin = false;  
  // return this;  (неявно)  
}  
```

То есть, результат вызова `new User("Вася")` – это тот же объект, что и:  
```javascript
let user = {  
  name: "Вася",  
  isAdmin: false   
}; 
```

## Типы данных
### Функция, которая ничего не возращает - по умолчанию возращает undefined

### Деструктурирующее присваивание
Деструктурирующее присваивание – это специальный синтаксис, который позволяет нам "распаковать» массивы или объекты в кучу переменных, так как иногда они более удобны.    

#### a.) Деструктуризация любого перебираемого объекта(массив, строка и т.д.):
```javascript
// у нас есть массив с именем и фамилией  
let arr = ["Ilya", "Kantor"]  
// деструктурирующее присваивание  
// записывает firstName=arr[0], surname=arr[1]  
let [firstName, surname] = arr;  
alert(firstName); // Ilya  
alert(surname);  // Kantor
```

Ненужные элементы массива также могут быть отброшены через запятую:   
```javascript
// второй элемент не нужен  
let [firstName, , title] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];  
alert( title ); // Consul  
```

Если мы хотим не просто получить первые значения, но и собрать все остальные, то мы можем добавить ещё один параметр, который получает остальные значения, используя оператор "остаточные параметры» – троеточие ("..."):  
```javascript
let [name1, name2, ...rest] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];  
alert(name1); // Julius  
alert(name2); // Caesar  
// Обратите внимание, что rest является массивом.  
```
#### b.) Деструктуризация объекта:
У нас есть существующий объект с правой стороны, который мы хотим разделить на переменные. Левая сторона содержит "шаблон» для соответствующих свойств. В простом случае это список названий переменных в {...}.  
Например:  
```javascript
let options = {  
  title: "Menu",  
  width: 100,  
  height: 200  
};  
let {title, width, height} = options; //Деструктуризация объекта  
alert(title);  // Menu  
alert(width);  // 100  
alert(height); // 200
```
  
Свойства `options.title`, `options.width` и `options.height` присваиваются соответствующим переменным. Порядок не имеет значения!  

Если мы хотим присвоить свойство объекта переменной с другим названием, например, свойство `options.width` присвоить переменной w, то мы можем использовать двоеточие:  
```javascript
let options = {  
  title: "Menu",  
  width: 100,  
  height: 200  
};  
// { sourceProperty: targetVariable }  
let {width: w, height: h, title} = options;  
// width -> w  
// height -> h  
// title -> title  
alert(title);  // Menu  
alert(w);      // 100  
alert(h);      // 200  
```
Двоеточие показывает "что : куда идёт". В примере выше свойство width сохраняется в переменную w, свойство height сохраняется в h, а title присваивается одноимённой переменной.  

## Объект Promise, async/await
### Promise
Объект `Promise` используется для отложенных и асинхронных вычислений.  
Чаще всего самостоятельно создавать промисы не нужно, так как мы будем работать с функциями или методами, которые будут их возращать.  
Описание промиса:  
Конструктор промисов принимимает в себя функцию "Экзекьютор" с двумя параметрами, являющимися функциями `resolve`(выполняется когда все прошло хорошо) и `reject` (это функция, которая говорит о том, что что-то пошло не так)  
```javascript
let promise = new Promise(function(resolve, reject) {  
  setTimeout(() => resolve("done!"), 1000);  
});  
// resolve запустит первую функцию, переданную в .then  
promise.then(  
  result => alert(result), // выведет "done!" через одну секунду  
  error => alert(error) // не будет запущена  
);  

let promise = new Promise(function(resolve, reject) {  
  setTimeout(() => reject(new Error("Whoops!")), 1000);  
});  
// reject запустит вторую функцию, переданную в .then  
promise.then(  
  result => alert(result), // не будет запущена  
  error => alert(error) // выведет "Error: Whoops!" спустя одну секунду  
);  
``` 

#### Step 0
• Создается некая функция в глобальной памяти akaFetch  
• В момент вызова этой функции создаётся объект `Promise`  
• Объект имеет ключ `value`, который имеет значение `undefined`, а также два массива  
![шаг 0](https://user-images.githubusercontent.com/67102520/123755618-c4178f00-d8c4-11eb-9998-f4a177d0252e.png)


#### Step 1
• Цепочки из `then`, `catch` наполняют объект `Promise`, а именно  
• Функция `then` при вызове передает свой параметр (то, что у нее в скобках) в массив `onFullfiled`  
• Функция `catch` при вызове передает свой параметр (то, что у нее в скобках) в массив `onRejected`  
![шаг 1](https://user-images.githubusercontent.com/67102520/123755648-cc6fca00-d8c4-11eb-9c91-9be77f7438ee.png)


#### Step 2
• В какой-то момент у объекта `Promise` вызывается `resolve` или `rejected`, и значит значение `value` меняется  
• Следовательно начинают вызываться функции либо в ветке массива `onFullfiled` (если был вызван `resolve`), либо в ветке массива `onRejected` (если был вызван `rejected`) 
![шаг 2](https://user-images.githubusercontent.com/67102520/123755718-ddb8d680-d8c4-11eb-86c5-48b275327df4.png)


#### Step N or chain (цепочка вызовов)
• сначала происходит все тоже самое  
• затем происходит цепочка вызовов `then` или `catch`  
• если вовремя этой цепочки был `return response + '!'`, то `value` этого `promise` меняется  
• затем начинает выполняться следующая функция с новым `value`  
• если после цепочки вызовов `then` не было вызова `rejected`, то `catch` не будет вызвана  
• метод `finally` выполняется в любом случае  
![шаг n1](https://user-images.githubusercontent.com/67102520/123755767-e9a49880-d8c4-11eb-9e6d-4ef1c9823022.png)


Чаще всего мы работаем с промисами таким образом:
fetch.

## Продвинутая работа с функциями
### Замыкание  
Замыкание – это функция вместе со всеми внешними переменными, которые ей доступны.
В JavaScript, все функции изначально являются замыканиями (есть только одно исключение, cинтаксис создания функции "new Function").  

В JS у каждой выполняемой функции, блока кода и скрипта есть связанный с ними внутренний (скрытый) объект, называемый лексическим окружением LexicalEnvironment.    
Объект лексического окружения состоит из двух частей:    
1.) Environment Record – объект, в котором как свойства хранятся все локальные переменные (а также некоторая другая информация, такая как значение this).    
2.) Ссылка на внешнее лексическое окружение – то есть то, которое соответствует коду снаружи (снаружи от текущих фигурных скобок). Эта ссылка устанавливается в значение [[Environment]] функции.  
"Переменная" – это просто свойство специального внутреннего объекта: Environment Record. "Получить или изменить переменную", означает, "получить или изменить свойство этого объекта".    

Функция называется «вложенной», когда она создаётся внутри другой функции.    
В процессе вызова функции у нас есть два лексических окружения: внутреннее (для вызываемой функции) и внешнее (глобальное), когда код хочет получить доступ к переменной – сначала происходит поиск во внутреннем лексическом окружении, затем во внешнем, затем в следующем и так далее, до глобального.  
Новое лексическое окружение функции создаётся каждый раз, когда функция выполняется, и если функция вызывается несколько раз, то для каждого вызова будет своё лексическое окружение, со своими, специфичными для этого вызова, локальными переменными и параметрами.  
Все функции «при рождении» получают скрытое свойство [[Environment]], которое ссылается на лексическое окружение места, где они были созданы (кроме синтаксиса "new Function", его свойство [[Environment]] всегда ссылается на глобальное лексическое окружение).  

«Понимать замыкания» в JavaScript означает понимать следующие вещи:  
1.) Все переменные и параметры функций являются свойствами объекта переменных LexicalEnvironment. Каждый запуск функции создаёт новый такой объект. На верхнем уровне им является "глобальный объект", в браузере – window.  
2.) При создании функция получает системное свойство [[Scope]], которое ссылается на LexicalEnvironment, в котором она была создана.  
3.) При вызове функции, куда бы её ни передали в коде – она будет искать переменные сначала у себя, а затем во внешних LexicalEnvironment с места своего "рождения".  

### Устаревшее ключевое слово "var"
Область видимости переменных var ограничивается либо функцией, либо, если переменная глобальная, то скриптом, так как var выходит за пределы блоков if, for и подобных. Это происходит потому, что на заре развития JavaScript блоки кода не имели лексического окружения.  

Объявления (инициализация) переменных var производится в начале исполнения функции (или скрипта для глобальных переменных), так как они подвержены хостингу (хостятся).  


## Остальное
### Hoisting 
Поднятие или hoisting — это механизм в JavaScript, в котором переменные и объявления функций, передвигаются вверх своей области видимости перед тем, как код будет выполнен.  

console.log(typeof variable); // Выводит: undefined
Первое заключение: необъявленной переменной при выполнении кода назначается значение undefined , а так же и тип undefined.  

console.log(variable); // Выводит: ReferenceError: variable is not defined
Второе заключение: ReferenceError появляется при попытке доступа к предварительно необъявленной переменной.  

var,Function Declaration vs let, const, Function Expression  
первая группа подвержена хостингу, когда мы вызываем var - выводит `undefined`, а когда функцию - то она выполняется  
вторая группа не подвержена хостингу, когда мы вызываем let, const - выводит `ReferenceError`, а когда функцию - `TypeError`  


## Введения в события
### Введение в браузерные события
Событие – это сигнал от браузера о том, что что-то произошло. Событию можно назначить обработчик, то есть функцию, которая сработает, как только событие произошло.  

Есть три способа назначения обработчиков событий:  
1.) Атрибут HTML: `<input value="Нажми меня" onclick="alert('Клик!')" type="button">`  
2.) Можно назначать обработчик, используя свойство DOM-элемента on<событие>, например, `elem.onclick = function.`    
Обработчик всегда хранится в свойстве DOM-объекта, а атрибут – лишь один из способов его инициализации.
Так как у элемента DOM может быть только одно свойство с именем `onclick`, то назначить более одного обработчика двумя этими способами не получится!  

Внутри обработчика события this ссылается на текущий элемент, то есть на тот, на котором, как говорят, «висит» (т.е. назначен) обработчик. В коде ниже button выводит своё содержимое, используя this.innerHTML:
`<button onclick="alert(this.innerHTML)">Нажми меня</button>`  

3.) Специальные методы:  
Синтаксис добавления обработчика `addEventListener`:  
`element.addEventListener(event, handler[, options]);`  
• `event` - имя события, например "click".  
• `handler` - ссылка на функцию-обработчик.  
• `options` - дополнительный объект со свойствами  

Для удаления обработчика следует использовать `removeEventListener`:  
`element.removeEventListener(event, handler[, options]);`  
• `event` - имя события, например "click".  
• `handler` - ссылка на функцию-обработчик.  
• `options` - дополнительный объект со свойствами  
Для удаления нужно передать именно ту функцию-обработчик которая была назначена (пишем именно название функции, а не код в ней)!  

Обработчики некоторых событий можно назначать только через `addEventListener`, например, событие `DOMContentLoaded`, которое срабатывает, когда завершена загрузка и построение `DOM` документа. 
Также `addEventListener` поддерживает объекты в качестве обработчиков событий. В этом случае вызывается метод объекта `handleEvent`.  

Первый или второй способ назначения обработчиков событий срабатывают независимо от `addEventListener`, поэтому вполне возможна ситуация, когда у элемента срабатывают сразу несколько обработчиков событий.  

Когда происходит событие, браузер создаёт объект события (`event`), записывает в него детали и передаёт его в качестве аргумента функции-обработчику.  
Пример ниже демонстрирует получение координат мыши из объекта события:  
```html
<input type="button" value="Нажми меня" id="elem">  
<script>  
  elem.onclick = function(event) {  
    // вывести тип события, элемент и координаты клика  
    alert(event.type + " на " + event.currentTarget);  
    alert("Координаты: " + event.clientX + ":" + event.clientY);  
  };  
</script>
```

### Всплытие и погружение
Стандарт `DOM Events` описывает 3 фазы прохода события:  
• Фаза погружения (`capturing phase`) – событие сначала идёт сверху вниз.  
• Фаза цели (`target phase`) – событие достигло целевого(исходного) элемента.    
• Фаза всплытия (`bubbling stage`) – событие начинает всплывать.  

Обработчики, добавленные через `on<event>`-свойство или через HTML-атрибуты, или через `addEventListener(event, handler)` с двумя аргументами, ничего не знают о фазе погружения, а работают только на 2-ой и 3-ей фазах.  

Хоть и формально существует 3 фазы, 2-ую фазу («фазу цели»: событие достигло элемента) нельзя обработать отдельно, при её достижении вызываются все обработчики: и на всплытие, и на погружение.  

Принцип всплытия очень простой.  
Когда на элементе происходит событие, обработчики сначала срабатывают на нём, потом на его родителе, затем выше и так далее, вверх по цепочке предков.  

Самый глубокий элемент, который вызывает событие, называется целевым элементом, и он доступен через `event.target`.  
Отличия от `this` (=`event.currentTarget`):  
• `event.target` – это «целевой» элемент, на котором произошло событие, в процессе всплытия он неизменен.  
• `this` – это «текущий» элемент, до которого дошло всплытие, на нём сейчас выполняется обработчик.  

При наступлении события – самый глубоко вложенный элемент, на котором оно произошло, помечается как «целевой» (`event.target`).  
• Затем событие сначала двигается вниз от корня документа к `event.target`, по пути вызывая обработчики, поставленные через `addEventListener(...., true)`, где `true` – это сокращение для `{capture: true}`.  
• Далее обработчики вызываются на целевом элементе.  
• Далее событие двигается от `event.target` вверх к корню документа, по пути вызывая обработчики, поставленные через `on<event>` и `addEventListener` без третьего аргумента или с третьим аргументом равным `false`.  

Каждый обработчик имеет доступ к свойствам события `event`:  
• `event.target` – самый глубокий элемент, на котором произошло событие.  
• `event.currentTarget` (=`this`) – элемент, на котором в данный момент сработал обработчик (тот, на котором «висит» конкретный обработчик)  
• `event.eventPhase` – на какой фазе он сработал (погружение=1, фаза цели=2, всплытие=3).  

Любой обработчик может остановить событие вызовом `event.stopPropagation()`, но делать это не рекомендуется, так как в дальнейшем это событие может понадобиться, иногда для самых неожиданных вещей.  
