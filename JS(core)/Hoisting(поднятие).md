# Hoisting (Поднятие)

**Hoisting** — это механизм JavaScript, при котором объявления переменных, функций и классов "поднимаются" в верхнюю часть своей области видимости во время фазы компиляции. При этом поднимаются только сами **объявления**, а инициализация (присвоение значений) остается на месте.

---

## Как работает hoisting для функций?

Функции, объявленные с помощью **function declaration**, полностью поднимаются вместе с их определением. Это позволяет вызывать такие функции до их объявления в коде.

#### Пример:
```javascript
console.log(greet()); // Вывод: "Hello, World!"

function greet() {
    return 'Hello, World!';
}
```

Функция `greet` доступна до своей явной декларации, так как она поднимается в область видимости.

Однако **function expressions** (функциональные выражения) и **arrow functions** поднимаются только как объявления переменных, поэтому их нельзя вызвать до присвоения значения:
```javascript
console.log(sayHello); // Вывод: undefined
// console.log(sayHello()); // Ошибка: sayHello is not a function

var sayHello = function() {
    return 'Hello!';
};
```

---

## Как работает hoisting для переменных?

Hoisting для переменных зависит от способа их объявления: **var**, **let** или **const**.

#### Hoisting переменных, объявленных с `var`

Переменные, объявленные с помощью `var`, поднимаются, но их значение устанавливается в `undefined` до выполнения строки с присвоением.  
#### Пример:
```javascript
console.log(myVar); // Вывод: undefined
var myVar = 5;
console.log(myVar); // Вывод: 5
```

#### Hoisting переменных, объявленных с `let` и `const`

Переменные, объявленные с помощью `let` и `const`, также поднимаются, но остаются в так называемой **"временной мертвой зоне" (Temporal Dead Zone, TDZ)** до выполнения строки, где они инициализируются. Попытка доступа до инициализации вызывает ошибку.  
#### Пример:
```javascript
// console.log(myLet); // Ошибка: Cannot access 'myLet' before initialization
let myLet = 10;
console.log(myLet); // Вывод: 10

// console.log(myConst); // Ошибка: Cannot access 'myConst' before initialization
const myConst = 20;
console.log(myConst); // Вывод: 20
```

---

## Какие типы объявлений поднимаются?

1. **Объявления функций (Function Declarations):**  
   Полностью поднимаются с их телом.

   ```javascript
   sayHi(); // Вывод: "Hi!"
   function sayHi() {
       console.log('Hi!');
   }
   ```

2. **Переменные, объявленные с `var`:**  
   Поднимаются как объявление, но без инициализации.

   ```javascript
   console.log(a); // Вывод: undefined
   var a = 5;
   console.log(a); // Вывод: 5
   ```

3. **Переменные, объявленные с `let` и `const`:**  
   Поднимаются, но остаются в **TDZ**, пока не встретится строка их инициализации.

   ```javascript
   // console.log(x); // Ошибка: Cannot access 'x' before initialization
   let x = 10;
   ```

4. **Классы:**  
   Поднимаются, но находятся в **TDZ**, аналогично `let` и `const`. Попытка использовать их до объявления вызовет ошибку.

   ```javascript
   // const obj = new MyClass(); // Ошибка: Cannot access 'MyClass' before initialization
   class MyClass {
       constructor(name) {
           this.name = name;
       }
   }
   ```

---

### Отличия в поведении `var`, `let` и `const`

- **`var`:**
    - Переменные поднимаются и инициализируются значением `undefined`.
    - Переменные с `var` имеют функциональную область видимости или глобальную (если объявлены вне функции).

- **`let` и `const`:**
    - Переменные поднимаются, но остаются в TDZ до выполнения строки инициализации.
    - Имеют блочную область видимости.
    - Попытка использовать до объявления вызывает ошибку.

---

## Итог

**Hoisting** — это важный механизм JavaScript, который влияет на то, как интерпретатор читает и выполняет код. Понимание этого механизма помогает избежать ошибок и использовать функции и переменные корректно.

Ключевые моменты:
1. **Функции, объявленные через `function`, полностью поднимаются.**
2. **Переменные с `var` поднимаются, но инициализируются в `undefined`.**
3. **`let`, `const` и классы поднимаются, но остаются в TDZ.**
4. **Используйте `let` и `const` для предсказуемого поведения и избегайте проблем с hoisting.**  

---

## ЗАДАЧИ

Ниже приведены задачи для закрепления знаний о механизме **hoisting**. Вы можете попытаться решить их самостоятельно. Если не получается, в каждом разделе есть кнопка "Показать пример", чтобы посмотреть объяснение и правильное решение.

---

### Задача 1: Hoisting функций

**Что выведет следующий код? Объясните почему.**

```javascript
greet();

function greet() {
    console.log('Hello, World!');
}

// sayHi(); // Что произойдет, если эту строку раскомментировать?
var sayHi = function() {
    console.log('Hi!');
};
```

<details>
<summary>Показать пример</summary>

```javascript
// Функция greet поднимется (hoisted), и вызов greet() сработает.
greet(); // Выведет: Hello, World!

// sayHi поднимется только как переменная (var), а не как функция.
// Если раскомментировать строку sayHi(), будет ошибка TypeError: sayHi is not a function.
var sayHi = function() {
    console.log('Hi!');
};
```

</details>

---

### Задача 2: Hoisting переменных с `var`

**Определите, что выведется в консоль:**

```javascript
console.log(a);
var a = 10;
console.log(a);

function test() {
    console.log(b);
    var b = 20;
    console.log(b);
}

test();
```

<details>
<summary>Показать пример</summary>

```javascript
// Переменная a поднимается, но её значение будет undefined до строки присвоения.
console.log(a); // undefined
var a = 10;
console.log(a); // 10

function test() {
    console.log(b); // undefined (b объявлена, но не инициализирована)
    var b = 20;
    console.log(b); // 20
}

test();
```

</details>

---

### Задача 3: Hoisting переменных с `let` и `const`

**Попробуйте угадать результат выполнения данного кода. Если возникнет ошибка, объясните, почему.**

```javascript
console.log(x); 
let x = 5;

console.log(y);
const y = 10;

{
    console.log(z);
    let z = 15;
}
```

<details>
<summary>Показать пример</summary>

```javascript
// Ошибка ReferenceError, так как переменные, объявленные с let и const, поднимаются,
// но остаются недоступными до момента инициализации (находятся в TDZ - Temporal Dead Zone).
```

</details>

---

### Задача 4: Классы и hoisting

**Что произойдет при выполнении следующего кода?**

```javascript
const obj = new MyClass();

class MyClass {
    constructor(name) {
        this.name = name;
    }
}

console.log(obj);
```

<details>
<summary>Показать пример</summary>

```javascript
// Ошибка ReferenceError: Cannot access 'MyClass' before initialization.
// Классы также находятся в TDZ до момента их объявления.
```

</details>

---

### Задача 5: Смешанный hoisting

**Объясните поведение кода и определите, что будет выведено в консоль:**

```javascript
console.log(a);
var a = 10;

function demo() {
    console.log(b);
    let b = 20;
    console.log(c);
    var c = 30;
    console.log(d);
}

demo();
```

<details>
<summary>Показать пример</summary>

```javascript
// Переменная a поднимется, но будет undefined до присвоения.
console.log(a); // undefined
var a = 10;

// В функции demo:
function demo() {
    console.log(b); // Ошибка ReferenceError из-за TDZ для b.
    let b = 20;

    console.log(c); // undefined, var поднимается как undefined.
    var c = 30;

    console.log(d); // Ошибка ReferenceError, d не объявлена.
}
```

</details>

---

### Задача 6: Практическая задача на устранение ошибок

**Дан следующий код:**

```javascript
function calculateSum() {
    return x + y;
}

var x = 5;
let y = 10;

console.log(calculateSum());
```

1. Что произойдет при выполнении кода?
2. Исправьте ошибки, чтобы код работал корректно.

<details>
<summary>Показать пример</summary>

```javascript
// Ошибка ReferenceError: y is not defined при вызове calculateSum().
// Функция вызывает переменную y до её инициализации.

// Исправленный код:
var x = 5;
let y = 10;

function calculateSum() {
    return x + y;
}

console.log(calculateSum()); // 15
```

</details>

---

### Задача 7: Анализ TDZ

**Рассмотрите код ниже и опишите поведение:**

```javascript
{
    console.log(foo);
    let foo = 'bar';

    function testFunc() {
        console.log(foo);
        var foo = 'baz';
        console.log(foo);
    }

    testFunc();
}
```

<details>
<summary>Показать пример</summary>

```javascript
{
    console.log(foo); // Ошибка ReferenceError из-за TDZ для let foo.
    let foo = 'bar';

    function testFunc() {
        console.log(foo); // undefined (var foo поднят внутри testFunc).
        var foo = 'baz';
        console.log(foo); // 'baz'
    }

    testFunc();
}
```

</details>

---

### Задача 8: Правильный выбор способа объявления

**Прочитайте код ниже и перепишите его так, чтобы избежать проблем с hoisting.**

```javascript
function init() {
    console.log(value);
    if (!value) {
        var value = 100;
    }
    console.log(value);
}

init();
```

<details>
<summary>Показать пример</summary>

```javascript
// Проблема в том, что переменная value поднимается, но становится undefined.
// Чтобы избежать проблемы, используйте let или const:

function init() {
    let value; // Инициализируем value заранее.
    console.log(value); // undefined
    if (!value) {
        value = 100;
    }
    console.log(value); // 100
}

init();
```

</details>
```

---

### Задача 8: Правильный выбор способа объявления
Прочитайте код ниже и перепишите его так, чтобы избежать проблем с hoisting.

```javascript
function init() {
    console.log(value);
    if (!value) {
        var value = 100;
    }
    console.log(value);
}

init();
```

---

Эти задачи помогут вам глубже понять, как работает **hoisting** и как можно избежать типичных ошибок, связанных с этим механизмом.

---
