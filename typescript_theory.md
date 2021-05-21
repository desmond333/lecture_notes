## Июнь 2021 года
# Коспект по теории TypeScript для подготовки к собеседованию на позицию junior frontend
## Основы
### Базовые типы
В TypeScript имеются следующие базовые типы:  
1. boolean: логическое значение true или false  
2. number: числовое значение (любой тип)  
3. string: строки  
4. Array: массивы  
`let list: number[] = [1, 2, 3];`  
`let list: Array<number> = [1, 2, 3]; //Generic type`  

5. Typle: А что если массив содержит различные типы данных? На помощь приходит тип данных Typle

5. Enum: перечисления  
6. Any: произвольный тип  
7. Symbol  
8. null и undefined, отличия от js
//javascript  
typeof null это object  
typeof undefined это undefined  

//typescript  
const u: null = null  
const u: undefined = undefined  

9. Void: Это — тип, использование которого сообщает программисту о том, что соответствующие функции и методы при их вызове ничего не возвращают.  
`const greetUser = (): void => {`  
`  alert(Hello, world!);`  
`};`

Такой синтаксис для void использовать нельзя, получим ошибку, так как таким образом мы определяем тип константы, а не тип возращаемого функцией результата
`const greetUser: void = () => {`  
`  alert(Hello, world!);`  
`};`

10. Never: также представляет отсутствие значения и используется в качестве возвращаемого типа функций, которые генерируют или возвращают ошибку

Большинство из этих типов соотносятся с примитивными типами из JavaScript.
### Interface


## TypeScript + React
### Определение типа react-компонента
#### FunctionComponent
`const App: React.FunctionComponent = () => {`  
`  return <div>Hello, world!</div>;`  
`};`  

Важное:
1.) `React.FunctionComponent` можно сократить до `React.FC`
2.) Функциональные react-компоненты всегда должны что-то возращать

