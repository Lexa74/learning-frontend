# Задачки по EvenLoop

### №1 (легко)
<details>
  <summary>Раскрыть</summary>
    <h3>Какая будет очередность вызова console</h3>

```javascript
console.log(1)

setTimeout(() => {
    console.log(2)
}, 1000)

setTimeout(() => {
    console.log(3)
}, 900)

console.log(4)
```
<details>
    <summary>Ответ</summary>
    
```javascript
1
4
3
2
```
</details>

</details>

### №2 (среднее)
<details>
  <summary>Раскрыть</summary>
    <h3>Какая будет очередность вызова console</h3>

```javascript
setTimeout(() => {
    console.log(1)
})

Promise.resolve().then(() => {
    console.log(2)
})

Promise.resolve().then(() => {
    console.log(3)

    setTimeout(() => {
        console.log(4)
    })
})

setTimeout(() => {
    console.log(5)
})

console.log(6)
```
<details>
    <summary>Ответ</summary>

```javascript
6
2
3
1
5
4
```
</details>

</details>


### №3 (жоска)
<details>
  <summary>Раскрыть</summary>
    <h3>Какая будет очередность вызова console</h3>

```javascript
Promise.resolve().then(() => {
    console.log(1)
})

setTimeout(() => console.log(2), 2)

new Promise(() => {
    console.log(3)
}).then(() => {
    console.log(4)
})

console.log(5)

Promise.resolve().then(() => {
    setTimeout(() => {
        console.log(6)
    })

    console.log(7)
})

setTimeout(() => {
    console.log(8)
}, 1)

console.log(9)
```
<details>
    <summary>Ответ</summary>

```javascript
3
5
9
1
7
2
8
6
```
</details>

</details>

### №4 (нереально)
<details>
  <summary>Раскрыть</summary>
    <h3>Какая будет очередность вызова console</h3>

```javascript
console.log(1)

Promise.resolve().then(() => console.log(2))

new Promise((resolve) => {
    const x = 3

    resolve(x + 1)
}).then((res) => {
    console.log(res)
})

Promise.resolve(() => setTimeout(() => console.log(5)))

console.log(6)

setTimeout(() => {
    console.log(7)

    Promise.resolve().then(() => {
        console.log(8)
    })
}, 10)

setTimeout(() => {
    console.log(9)
})

console.log(10)
```
<details>
    <summary>Ответ</summary>

```javascript
1
6
10
2
4
9
7
8

```
</details>

</details>

### №5 (Марк Цукерберг нервно курит в сторонке)
<details>
  <summary>Раскрыть</summary>
    <h3>Какая будет очередность вызова console</h3>

```javascript
const myPromise = (delay) => new Promise((res, rej) => { setTimeout(res, delay) })
setTimeout(() => console.log('in setTimeout1'), 1000);
myPromise(1000).then(res => console.log('in Promise 1'));
setTimeout(() => console.log('in setTimeout2'), 100);
myPromise(2000).then(res => console.log('in Promise 2'));
setTimeout(() => console.log('in setTimeout3'), 2000);
myPromise(1000).then(res => console.log('in Promise 3'));
setTimeout(() => console.log('in setTimeout4'), 1000);
myPromise(5000).then(res => console.log('in Promise '));
```
<details>
    <summary>Ответ</summary>

```javascript
// in setTimeout2
// in setTimeout1
// in Promise 1
// in Promise 3
// in setTimeout4
// in Promise 2
// in setTimeout3
// in Promise

```
</details>

</details>

