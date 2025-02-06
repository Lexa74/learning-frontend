# JavaScript

### 1. Какие типы данных есть в JavaScript?
<details>
  <summary>Ответ</summary>
    <ul>
        <li>Примитивные типы: <i>Boolean, number, string, undefuned, null, BigInt, Symbol.</i> <br> (Для запоминания можно использовать только первые буквы. Например: BBS NUN)</li>
        <li>Не примитивы: <i>Objects</i></li>
    </ul>
</details>
    

### 2. В чем отличия между var, let, const?
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


### 3. Что такое замыкание
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


### 4. В чем отличия Function expression и Function declaration

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

### 5. В чем разница между null и undefined

<details>
    <summary>Ответ</summary>
    <ul>
        <li>null – пустое значение (явно присваивается)</li>
        <li>undefined - неприсвоенное значение (по-умолчанию)</li>
        <li>null - это тип <b>объект</b>, а undefined и имеет тип <b>undefined</b></li>
    </ul>
</details>

### 6. Как достигается ассинхронность в JS? (EventLoop)

<details>
    <summary>Ответ</summary>
    JavaScript – это однопоточный язык, в котором ассинхронность достигается с помощью механизма EventLoop (цикл событий).
    У EventLoop есть 3 очереди:
    <ul>
        <li>CallStack (Стек вызовов)</li>
        <li>MicroTasks (микро задачи)</li>
        <li>MacroTasks (макро задачи)</li>
    </ul>
    Каждый этап – это итерация цикла и когда javaScript видит код, он его сразу делит на очереди. Очередность: 
    <ol>
        <li>Синхронный код</li>
        <li>MicroTasks</li>
        <li>MacroTasks</li>
    </ol>

   CallStack – в этот стек помещается любой код, который должен сейчас выполнится. Действует по прицнипу: первый вошел – первый вышел. Сюда сразу попадает весь синхронный код. 

```javascript
console.log('Я синхронный код')
alert('Я тоже, но я появлюсь вторым, после console')
```
MicroTasks – это выполнение ассинхронного кода (Promise).

```javascript
Promise.resolve().then(() => {
    console.log('Я ассинхронный код')
})
new Promise((resolve) => {
    console.log('Я необычная запись. Здесь синхронный код')
    resolve(); // Вызов этой функции обязателен, если хотим выполнить блок then
}).then(() => {
    console.log('А я уже ассинхронный')
})
```

MacroTasks – это тоже ассинхронный код, только с четко установленными врменем откладывания вызова. К ним относится setTimeout и setInterval

```javascript
setTimeout(() => {
    console.log('Ты меня увидишь через секунду')
}, 1000)
```
У каждой очереди есть своя очередность: 

Теперь перейдем к примерам, где будут все эти виды очередей:

```javascript
console.log(1) // Синхронный код. Выполнится на первой итерации

setTimeout(() => {
    console.log(2) // Ассинхронный код, макро-таска и выполнится на третей итерации цикла EventLoop
}) // Даже если секунду не указаны, вызов все равно откладывается

Promise.resolve().then(() => {
    console.log(3) // Ассинхронный код, микро-таска и выполнится на второй итерации цикла EventLoop
})

console.log(4) // Синхронный код. Выполнится на первой итерации
```

В данном случае вывод консолей будет таким: 1 4 3 2. 

Это достаточно объемная тема, поэтому рекомендую ознакомиться с видео:
https://www.youtube.com/watch?v=eiC58R16hb8
https://www.youtube.com/watch?v=zDlg64fsQow

</details>

### 7. В чем отличия === и == ?
<details>
    <summary>Ответ</summary>
    == это равеснтво срвнивает значения без типов <br>
    === это строго равенство и сравнивает не только значения, но и типы
    
```javascript
console.log("1" == 1) // Выдаст true, т.к. сравнивает значения
console.log("1" === 1) // Выдаст false, т.к. сравнивает значения и типы, а типы у них разные

```
</details>

### 8. Какие методы массивов ты знаешь?
<details>
    <summary>Ответ</summary>
   Самые популярные:
<ul>
    <li>map* – принимает колбек и возвращает новый массив. Применяет этот колбек к каждому элементу</li>
    <li>filter* – принимает колбек и возвращает новый массив элементов, которые отвечают возвращаемому условию из колбека</li>
    <li>find* – принимает колбек и возвращает первый элемент, который подошел под условие из колбека</li>
    <li>some* – принимает колбек и возвращает true или false. true - если хотя бы один элемент подходит под условие колбека, false – если ни один элемент не подошел</li>
    <li>every* – принимает колбек и возвращает true или false. true - если все элементы подходят под условие колбека, false – если хотя бы один элемент не подошел</li>
    <li>includes – принимает элемент и возвращает true или false. true - если элемент найден в массиве, false – если не найден</li>
    <li>sort** – принимает колбек. Колбек принимает 2 параметра – a, b. Позволяет отсортировать массив</li>
    <li>reduce – принимает колбек и изначальное значение. Колбек принимает 2 параметра – acc, cur, где acc – переменная, которая будет аккумулировать значение на каждой итерации, cur – пребираемый элемент. </li>
</ul>
    
```javascript
const users = [
    {
        name: 'Alex',
        age: 20,
        isAdmin: true,
    },
    {
        name: 'Misha',
        age: 50,
        isAdmin: false,
    },
    {
        name: 'Ira',
        age: 10,
        isAdmin: false,
    }
]

users.map((el) => el.age * 2) // Вернет массив только возрастов, умноженных на 2
// [ 40, 100, 20 ]

users.filter((el) => el.age > 18) // Вернет 2 юзера старше 18 лет
// [
//   { name: 'Alex', age: 20, isAdmin: true },
//   { name: 'Misha', age: 50, isAdmin: false }
// ]

users.find((el) => el.age > 18) // Вернет только Мишу
// { name: 'Alex', age: 20, isAdmin: true }

users.some((el) => el.isAdmin) // Вернет true, т.к. у Alex это значение true
// true

users.every((el) => el.isAdmin) // Вернет false, т.к. только у Alex это значение true
// false

users.sort((a, b) => a.age - b.age) // Вернет юзеров по возврастанию возрастов
// [
//    { name: 'Ira', age: 10, isAdmin: false },
//    { name: 'Alex', age: 20, isAdmin: true },
//    { name: 'Misha', age: 50, isAdmin: false }
// ]

users.reduce((acc, cur) => acc + cur.age, 0) // Посчитает сумму всех возрастов
// 80
```

<p>* - все эти методы принимают три аргумента в колбек: el – перебираемый элемент, index – индекс элемента, array – массив</p>
<p>** - мутирующий метод массива, т.е. изменяет изначальный массив</p>
</details>

