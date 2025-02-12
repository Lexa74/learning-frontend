# Задачки по JavaScript

### Задача 1. Четное\нечетное
<details>
  <summary>Раскрыть</summary>
    <h3>Написать функцию, которая принимает массив чисел и возвращает объект с массивом четных и нечетных чисел</h3>
<i>Пример вывода:</i> { even: [2, 4, 6], odd: [1, 3, 5] }

<details>
    <summary>Ответ</summary>

Если ответ получился с вложенным циклом, то лучше подумать над оптимизацией
```javascript
function splitEvenOdd(arr) {
    const odd = []
    const even = []

    arr.forEach((el) => {
        if(el % 2 === 0) {
            odd.push(el)
        } else {
            even.push(el)
        }
    })

    return {odd, even}
}
```
</details>

</details>

### Задача 2. Вложенные массивы
<details>
  <summary>Раскрыть</summary>
    <h3>Есть массив [0, [1, 2], [3], [[4, 5], 6, 7], [8,[[9]]]]. <br>Создайте функцию, которая преобразовывает массив к виду 
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
и возвращает его</h3>

```javascript
Вход: [0, [1, 2], [3], [[4, 5], 6, 7], [8,[[9]]]] 
Выход: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```
<details>
    <summary>Ответ</summary>

```javascript
function flatArray(arr) { 
    return arr.flat(Infinity)
}
```
</details>

</details>


### Задача 3. Средний возвраст
<details>
  <summary>Раскрыть</summary>
    <h3>Дан массив. Необходимо найти средний возвраст всех пользователей</h3>

```javascript
const users = [
    {
      name: 'Alex',
      age: 35,
    },
    {
      name: 'Misha',
      age: 18,
    },
    {
      name: 'Tania',
      age: 66,
    }
]
```

<details>
    <summary>Ответ</summary>

```javascript
function averageAge(arr) {
    return arr.reduce((acc, cur) => acc + cur.age, 0) / arr.length; // 39.6
}
```
</details>

</details>

### Задача 4. Сравнить объекты
<details>
  <summary>Раскрыть</summary>
    <h3>Даны 2 объекта. Как их проверить на идентичность?</h3>

```javascript
const obj1 = {
    id: 1,
    name: 'Example',
    gender: 'male'
}

const obj2 = {
    id: 1,
    name: 'Example',
    gender: 'male'
}
```
<details>
    <summary>Ответ</summary>

```javascript
// Ненадежный способ, но рабочий. Поверхностное сравниние
console.log(String(obj1) === String(obj2));
```

```javascript
//Глубокое сравнение
function deepEqual(obj1, obj2) {
    // Если оба объекта — это один и тот же объект
    if (obj1 === obj2) return true;

    // Если один из объектов null или не объект
    if (obj1 === null || typeof obj1 !== 'object' || obj2 === null || typeof obj2 !== 'object') {
        return false;
    }

    // Получаем ключи объектов
    const keys1 = Object.keys(obj1);
    const keys2 = Object.keys(obj2);

    // Если количество ключей разное
    if (keys1.length !== keys2.length) return false;

    // Рекурсивно сравниваем значения каждого ключа
    for (const key of keys1) {
        if (!keys2.includes(key) || !deepEqual(obj1[key], obj2[key])) {
            return false;
        }
    }

    return true;
}

console.log(deepEqual(obj1, obj2));

```
</details>

</details>

### Задача 5. Найти уникальные объекты
<details>
  <summary>Раскрыть</summary>
    <h3>Дан массив. Необходимо написать функцию, которая будет возвращать только уникальные значения из этого массива</h3>

```javascript
const cars = [
    { model: 'Opel', year: 2015, isNew: true },
    { model: 'Nissan', year: 2002, isNew: false },
    { model: 'Nissan', year: 2002, isNew: false },
    { model: 'Subaru', year: 1999, isNew: false },
    { model: 'BMW', year: 1900, isNew: true },
    { model: 'BMW', year: 1900, isNew: true },
    { model: 'Subaru', year: 1999, isNew: false },
    { model: 'Subaru', year: 1999, isNew: false },
    { model: 'Nissan', year: 2002, isNew: false },
];
```
<details>
    <summary>Ответ</summary>

```javascript
function getUniqValues(arr) {
    const uniqArr = arr.filter((el, indexEl) => {
        // Ищем индекс элемента, который совпадает c перебираемым элементом (el)
        const firstIndex = arr.findIndex((item) => {
            return item.model === el.model && item.year === el.year && item.isNew === el.isNew
        })
        // Сравниваем индексы перебираемого элемента и индекс первого элемента, который идентичен перебираемому
        // Если индексы равны, то массив наполняется (1 === 1)
        // Например, Nissan indexEl = 2, но firstIndex = 1, то элемент не добавится
        return indexEl === firstIndex
    })

    return uniqArr
}
```
</details>

</details>

