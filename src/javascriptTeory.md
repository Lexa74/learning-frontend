# JavaScript

1. ### Какие типы данных есть в JavaScript?
<details>
  <summary>Ответ</summary>
    <ul>
        <li>Примитивные типы: <i>Boolean, number, string, undefuned, null, BigInt, Symbol.</i> <br> (Для запоминания можно использовать только первые буквы. Например: BBS NUN)</li>
        <li>Не примитивы: <i>Objects</i></li>
    </ul>
</details>
    

2. ### В чем отличия между var, let, const?
<details>
  <summary>Ответ</summary>
    <ul>
        <li>Главное отличие var от let в их области видимости. У var область видимости функциональная. Область видимости let – блочная, проще говоря ограничена фигурными скобками, в котором она объявлена.</li>
        <li>Также если мы попытаеся обратиться к переменной до ее инициализации с var мы получим <i>undefined</i>, с let/const <i>Ошибку</i></li>
        <li>Отличия let и const в том, что мы можем переприсвоить(мутировать) let, а const – нет</li>
    </ul>

```javascript
function someFn() {
    if(true) {
        var x = 0
    }
    console.log(x) // Выведет 0
}

function someFn() {
    if(true) {
        const x = 0
    }
    console.log(x) // Выведет ошибку, т.к. область видиvости только внутри if
}
```
```javascript
a = 5;
var a; // Ошибки не будет

b = 5; // Будет ошибка, b is not defined
let b; 
```

   
</details>


3. ### Что такое замыкание
<details>
    <summary>Ответ</summary>
    <ul>
        <li>Замыкание – это комбинация функции и лексического окружения, в котором эта функция была определена. Другими словами, замыкание даёт вам доступ к Scope внешней функции из внутренней функции.</li>
        <li>Замыкание – возвращаемая функция внутри функции, которая помнит\знает об окружении (Scope) своей родительской функции</li>
        <li>Нужно для оптимизации кода, т.к. родительская функция будет выполняться только один раз</li>
    </ul>

```javascript
function counter() {
    let x = 0;
    for (let i = 0; i < 100000; i++) {
        // Я ресурсозатратный код и выполнюсь 1 раз
    }
    const increment = () => {
        return x++
    }
    
    return increment
}

const result = counter() // Функция вызовется единожды
// А вот внутреннюю можем вызывать сколько угодно
console.log(result()) // 1
console.log(result()) // 2
console.log(result()) // 3
```
</details>


4. ### В чем отличия Function expression и Function declaration

<details>
    <summary>Ответ</summary>
    <ul>
        <li>Function declaration можно вызвать <b>до</b> ее инициализации (hoisting)</li>
        <li>Function expression можно вызывать только <b>после</b> инициализации</li>
        <li>FD имеет <i>локальный контекст</i>, а FE – <i>глобальный</i></li>
    </ul>

```javascript
declareFn()

function declareFn() {
    console.log('Я функция, которую можно вызвать до инициализации')
}

const expressFn = () => {
    console.log('А меня можно вызввать только ниже')
}

expressFn()
```

```javascript
const obj = {
    name: 'Alex',
    age: 20,
    getAge: () => {
        return this.age 
    } 
}

console.log(obj.getAge()) // Вернет undefined, т.к. не знает где ее вызывают (глоабльное окружение)

const obj = {
    name: 'Alex',
    age: 20,
    getAge: function () {
        return this.age
    }
}

console.log(obj.getAge()) // Вернет 20, т.к. знает где ее вызывают (локальное окружение)
```
</details>

5. ### В чем разница между null и undefined

<details>
    <summary>Ответ</summary>
    <ul>
        <li>null – пустое значение (явно присваивается)</li>
        <li>undefined - неприсвоенное значение (по-умолчанию)</li>
        <li>null - это тип <b>объект</b>, а undefined и имеет тип <b>undefined</b></li>
    </ul>
</details>

