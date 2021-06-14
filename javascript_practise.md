## Июнь 2021 года
# Коспект по практике Javascript для подготовки к собеседованию на позицию junior frontend

## Обычные задачи
### Напишите функцию camelize(str), которая преобразует строки вида «my-short-string» в «myShortString»
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

### Функция проверки палиндрома
let palindrome = (str) => str.toLowerCase() === str.toLowerCase().split('').reverse().join('')  
Возращаем функцией тип boolean, получаемый при сравнении изначальной строки и перевернутой (буквы приводим в один регистр).  

console.log(palindrome('racecar')) // true
console.log(palindrome('table')) // false
console.log(palindrome('Анна')) // true

//Более сложный вариант
let isPalindrome = (str) => {
  str = str.toLowerCase().split(' ').join('') //убираем пробелы и приводим все буквы к одному регистру в изначальной строке
  return str === str.split('').reverse().join('') //возвращаем результат сравнения
}

console.log(isPalindrome('А роза упала на лапу Азора')) // true

## Более сложные задачи
### Замыкание
const arr = [10, 12, 15, 21];  
for (var i = 0; i < arr.length; i++) {  
  setTimeout(function() {  
    console.log('Index: ' + i + ', element: ' + arr[i]);  
  }, 3000);  
}  
В консоли выведет:  
Index: 4, element: undefined  
Index: 4, element: undefined  
Index: 4, element: undefined  
Index: 4, element: undefined  

Причина подобного заключается в том, что функция setTimeout создаёт функцию (замыкание), у которой есть доступ к внешней по отношению к ней области видимости, представленной в данном случае циклом, в котором объявляется и используется переменная i. После того, как пройдут 3 секунды, функция выполняется и выводит значение i, которое, после окончания работы цикла, остаётся доступным и равняется 4-м. Переменная, в ходе работы цикла, последовательно принимает значения 0, 1, 2, 3, 4, причём, последнее значение оказывается сохранённым в ней и после выхода из цикла. В массиве имеется четыре элемента, с индексами от 0 до 3, поэтому, попытавшись обратиться к arr[4], мы и получаем undefined. Как избавиться от undefined и сделать так, чтобы код выводил то, чего от него и ждут, то есть — значения элементов массива?  

Вот пара распространённых подходов к решению подобной задачи, а конкретно — к тому, чтобы организовать доступ к нужному значению переменной цикла внутри функции, вызываемой setTimeout. Первый предусматривает передачу необходимого параметра во внутреннюю функцию, второй основан на использовании возможностей ES6.  

Итак, вот первый вариант:  
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

Вот второй вариант:  
const arr = [10, 12, 15, 21];  
for (let i = 0; i < arr.length; i++) {  
  // использование ключевого слова let, которое появилось в ES6,  
  // позволяет создавать новую привязку при каждом вызове функции  
  setTimeout(function() {  
    console.log('The index of this number is: ' + i);  
  }, 3000);  
}