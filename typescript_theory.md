## Июнь 2021 года
# Коспект по теории TypeScript для подготовки к собеседованию на позицию junior frontend
## Основы
### Типы данных
В TypeScript имеются следующие типы данных:  
#### 1. number: числовое значение (любой тип)  
#### 2. boolean: логическое значение true или false  
#### 3. string: строки  
#### 4. Symbol  
#### 5. null и undefined, отличия от js
//javascript  
typeof null это object  
typeof undefined это undefined  

//typescript  
const u: null = null  
const u: undefined = undefined  

#### 6. Array: массивы  
`let list: number[] = [1, 2, 3];`  
`let list: Array<number> = [1, 2, 3]; //Generic type`  

Массивы определяются с помощью выражения [] и также являются строго типизированными. То есть если изначально массив содержит строки, то в будущем он сможет работать только со строками.
`let list: number[] = [10, 20, 30];`  
`let colors: string[] = ["red", "green", "blue"];`  
`console.log(list[0]);`  
`console.log(colors[1]);`  

Как и в JavaScript, с помощью индексов можно обращаться к элементам массива.  

Альтернативный способ определения массивов представляет применение типа Array<>, где в фигурных скобках указывается тип элементов массива:  
`let names: Array<string> = ["Tom", "Bob", "Alice"];`  
`console.log(names[1]);  // Bob`  

Но фактически такие формы массивов, как number[] или string[] являются сокращением соответственно типов Array<number> или Array<string>  
В остальном массивы в TypeScript поддерживают все те же операции, что и массивы в JavaScript.  

#### 7. Typle или кортежи
А что если массив содержит различные типы данных? На помощь приходит тип данных Typle  

#### 8. Generic или общие типы

#### 9. Enum
Перечисления  

#### 10. Any
произвольный тип  

#### 11. Void
Это — тип, использование которого сообщает программисту о том, что соответствующие функции и методы при их вызове ничего не возвращают.  
`const greetUser = (): void => {`  
`  alert(Hello, world!);`  
`};`  

Такой синтаксис для void использовать нельзя, получим ошибку, так как таким образом мы определяем тип константы, а не тип возращаемого функцией результата  
`const greetUser: void = () => {`  
`  alert(Hello, world!);`  
`};`  

#### 12. Never  
Означает отсутствие значения и используется в качестве возвращаемого типа функций, которые генерируют или возвращают ошибку  

#### 13. Псевдонимы Типов (Type Aliases)
TypeScript позволяет определять псевдонимы типов с помощью ключевого слова type:
`type id = number | string;`  
`let userId : id = 2;`  
`console.log(`Id: ${userId}`);`  
`userId = "qwerty";`  
`console.log(`Id: ${userId}`);`  

Здесь для объединения number|string определяется псевдоним id. Далее мы можем использовать этот псевдоним для определения переменных.  


#### 14. Interface  
Интерфейс определяет свойства и методы, которые объект должен реализовать. Другими словами, интерфейс - это определение кастомного типа данных, но без реализации. В данном случае интерфейсы в TS похожи на интерфейсы в языках Java и C#. Интерфейсы определяются с помощью ключевого слова interface. Для начала определим простенький интерфейс:  
`interface IUser {`  
`    id: number;`  
`    name: string;`  
`}`  

Интерфейс в фигурных скобках определяет два свойства: id, которое имеет тип number, и name, которая представляет строку. Теперь используем его в программе:  
`let employee: IUser = {`  
`    id: 1, `  
`    name: "Tom"`  
`}`  
`console.log("id: ", employee.id);`  
`console.log("name: ", employee.name);`  

По сути employee - обычный объект за тем исключением, что он имеет тип IUser. Если правильнее говорить, то employee реализует интерфейс IUser. Причем эта реализация накладывает на employee некоторые ограничения. Так, employee должен реализовать все свойства и методы интерфейса IUser, поэтому при определении employee данный объект обязательно должен включать в себя свойства id и name.  

### typeof
В TypeScript typeof, в отличие от JavaScript, означает содержимое переменной. Например:  
`const INITIALIZED_SUCCESSED = 'INITIALIZED_SUCCESSED';`
`type InitializedSuccessedActionType = {`  
`  type: typeof INITIALIZED_SUCCESSED;`  
`};`  

то есть `type: 'INITIALIZED_SUCCESSED'`  

## TypeScript + React
### Определение типа react-компонента
#### FunctionComponent
`const App: React.FunctionComponent = () => {`  
`  return <div>Hello, world!</div>;`  
`};`  

Важное:  
1.) `React.FunctionComponent` можно сократить до `React.FC`  
2.) Функциональные react-компоненты всегда должны что-то возращать  

