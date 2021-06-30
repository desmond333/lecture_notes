## Июль 2021 года
## Коспект по практике Javascript для frontend разработки

## Обычные задачи
### Напишите функцию camelize(str), которая преобразует строки вида «my-short-string» в «myShortString»
```javascript
//на примере 'listStyleImage'
const camelize = (str) => {
  str = str.split('-') //превращаем строку в массив
  let result = str[0]  //result = list
  str.map((word, index) => { //перебираем массив
    if (index > 0) { // следующие слова после слова list
      result += word[0].toUpperCase() + word.slice(1) //добавляем первую букву и остальное слово
    }
  })
  return result //возращаем 'listStyleImage'
}

console.log(camelize('background-color')) //'backgroundColor'
console.log(camelize('list-style-image')) //'listStyleImage'
console.log(camelize('-webkit-transition')) //'WebkitTransition'
```

### Функция проверки палиндрома
```javascript
let palindrome = (str) => str.toLowerCase() === str.toLowerCase().split('').reverse().join('')  
//Возращаем функцией тип boolean, получаемый при сравнении изначальной строки и перевернутой (буквы приводим в один регистр).  

console.log(palindrome('racecar')) // true
console.log(palindrome('table')) // false
console.log(palindrome('Анна')) // true

//Более сложный вариант
let isPalindrome = (str) => {
  str = str.toLowerCase().split(' ').join('') //убираем пробелы и приводим все буквы к одному регистру в изначальной строке
  return str === str.split('').reverse().join('') //возвращаем результат сравнения
}

console.log(isPalindrome('А роза упала на лапу Азора')) // true
```


## Более сложные задачи
### Замыкание
```javascript
const arr = [10, 12, 15, 21];
for (var i = 0; i < arr.length; i++) {
  setTimeout(function() {
    console.log('Index: ' + i + ', element: ' + arr[i]);
  }, 3000);
}
```
В консоли выведет:
```javascript
Index: 4, element: undefined
Index: 4, element: undefined
Index: 4, element: undefined
Index: 4, element: undefined
```


Причина подобного заключается в том, что функция setTimeout создаёт функцию (замыкание), у которой есть доступ к внешней по отношению к ней области видимости, представленной в данном случае циклом, в котором объявляется и используется переменная i.

После того, как пройдут 3 секунды, функция выполняется и выводит значение i, которое, после окончания работы цикла, остаётся доступным и равняется 4-м. Переменная, в ходе работы цикла, последовательно принимает значения 0, 1, 2, 3, 4, причём, последнее значение оказывается сохранённым в ней и после выхода из цикла.

В массиве имеется четыре элемента, с индексами от 0 до 3, поэтому, попытавшись обратиться к arr[4], мы и получаем undefined. Как избавиться от undefined и сделать так, чтобы код выводил то, чего от него и ждут, то есть — значения элементов массива?  

Вот пара распространённых подходов к решению подобной задачи, а конкретно — к тому, чтобы организовать доступ к нужному значению переменной цикла внутри функции, вызываемой setTimeout. Первый предусматривает передачу необходимого параметра во внутреннюю функцию, второй основан на использовании возможностей ES6.  

Итак, вот первый вариант:  
```javascript
const arr = [10, 12, 15, 21];  
for (var i = 0; i < arr.length; i++) {  
  // передадим функции переменную i, в результате  
  // у каждой функции будет доступ к правильному значению индекса  
  setTimeout(function(i_local) {  
    return function() {  
      console.log('The index of this number is: ' + i_local);  
    }  
  }(i), 3000);  
}
```

Вот второй вариант:  
```javascript
const arr = [10, 12, 15, 21];  
for (let i = 0; i < arr.length; i++) {  
  // использование ключевого слова let, которое появилось в ES6,  
  // позволяет создавать новую привязку при каждом вызове функции  
  setTimeout(function() {  
    console.log('The index of this number is: ' + i);  
  }, 3000);  
}
```

### Сортировка массива объектов по дате
```javascript
/*
Есть массив операций.
Необходимо операции отсортировать по дате и сгруппировать их по году, а в качестве
значений представить массивы c датами в формате MM-DD.
Пример результата:
    result = {
            "2017": [
                "07-31",
                "08-22"
            ],
            "2018": [
                "01-01"
                "02-22"
            ]
        }
*/
const operations = [
    {"date": "2017-07-31", "amount": "5422"},
    {"date": "2017-06-30", "amount": "5220"},
    {"date": "2017-05-31", "amount": "5365"},
    {"date": "2017-08-31", "amount": "5451"},
    {"date": "2017-09-30", "amount": "5303"},
    {"date": "2018-03-31", "amount": "5654"},
    {"date": "2017-10-31", "amount": "5509"},
    {"date": "2017-12-31", "amount": "5567"},
    {"date": "2018-01-31", "amount": "5597"},
    {"date": "2017-11-30", "amount": "5359"},
    {"date": "2018-02-28", "amount": "5082"},
    {"date": "2018-04-14", "amount": "2567"}
];
```

Мое решение (не самое удачное):  
```javascript
const sortOperations = operations => {
    const result = {}
    const operationsSortByDate = operations.sort((a, b) => {
        return new Date(a.date) - new Date(b.date);
    });
    operationsSortByDate.forEach(operation=>{
        const dateArr = operation['date'].split('-')
        const year = dateArr[0]
        result[year] = []
    })
    operationsSortByDate.forEach(operation => {
        const dateArr = operation['date'].split('-')
        const year = dateArr[0]
        const month = dateArr[1] + '-' + dateArr[2]
        if ([year] in result) {
            result[year].push(month)
        }
    })
    return result
}
```

Лаконичное решение:  
```javascript
const sortOperations = operations => {
    operations.reduce((acc, cur) => {
    const dateSplit = cur.date.split(‘-’);
    const key = dateSplit[0];
    return {
      ...acc,
      [key]: [...(acc[key]? acc[key] : []), dateSplit.slice(1).join(‘-’)].sort()
    }
  } , {})
}
```
