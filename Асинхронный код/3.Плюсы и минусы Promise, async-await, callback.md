# Callback-функции, Promise и async/await: сравнение, преимущества и недостатки

**Асинхронное программирование** в JavaScript предлагает три основных подхода: **callback-функции**, **Promise** и **async/await**. Каждый из них имеет свои сильные и слабые стороны. Рассмотрим их особенности и подходящие случаи применения.

---

## 1. Callback-функции

### Преимущества:
1. **Простота использования**: callback-функции легко начать использовать, особенно для небольших задач.
2. **Широкая поддержка**: работают во всех версиях JavaScript и совместимы с большинством старых библиотек.

### Недостатки:
1. **Callback Hell**: вложенные callback-и создают «лесенку» кода, что усложняет его чтение и поддержку.
2. **Проблемы с обработкой ошибок**: необходимо вручную обрабатывать ошибки, передавая их через аргументы, что делает код громоздким.
3. **Ограниченная масштабируемость**: при увеличении сложности приложения callback-и становятся трудными для поддержки.

#### Пример:

```javascript
function fetchData(callback) {
  setTimeout(() => {
    const error = Math.random() > 0.7; // Генерируем ошибку с вероятностью 30%
    if (error) {
      callback("Ошибка загрузки данных", null);
    } else {
      callback(null, "Данные успешно получены!");
    }
  }, 1000);
}

// Использование callback
fetchData((error, data) => {
  if (error) {
    console.error("Произошла ошибка:", error);
  } else {
    console.log(data);
  }
});
```

---

## 2. Promise

### Преимущества:
1. **Читаемость**: Promises позволяют избежать «callback hell», делая код более линейным.
2. **Управление ошибками**: метод `.catch()` обеспечивает централизованную обработку ошибок.
3. **Композиция**: легко комбинируются, поддерживая последовательное или параллельное выполнение задач.

### Недостатки:
1. **Сложность для новичков**: синтаксис Promises может быть непонятен для тех, кто только начинает изучать JavaScript.
2. **Неявное поведение ошибок**: если пропустить вызов `.catch()`, ошибка может остаться необработанной.
3. **Долгие цепочки**: при последовательных действиях код может выглядеть менее компактно.

#### Пример:

```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const success = Math.random() > 0.5;
      success ? resolve("Данные получены!") : reject("Ошибка загрузки данных");
    }, 1000);
  });
}

// Использование Promises
fetchData()
  .then(data => console.log(data)) // Обработка успеха
  .catch(error => console.error("Произошла ошибка:", error)); // Обработка ошибки
```

---

## 3. Async/Await

### Преимущества:
1. **Похож на синхронный код**: async/await делает асинхронный код более понятным и читаемым.
2. **Обработка ошибок**: используется стандартный механизм `try/catch`, что упрощает обработку исключений.
3. **Легкость в отладке**: стек вызовов сохраняет читаемость, упрощая поиск ошибок.

### Недостатки:
1. **Блокировка кода**: неправильное использование `await` может замедлить выполнение других операций.
2. **Совместимость**: поддерживается только в современных версиях JavaScript (ES2017+), что требует полифиллов для старых браузеров.

#### Пример:

```javascript
async function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const success = Math.random() > 0.5;
      success ? resolve("Данные успешно получены!") : reject("Ошибка загрузки данных");
    }, 1000);
  });
}

async function getData() {
  try {
    const data = await fetchData(); // Ожидание результата
    console.log(data);
  } catch (error) {
    console.error("Произошла ошибка:", error);
  }
}

getData();
```

---

## Сравнительная таблица

| Подход         | Преимущества                          | Недостатки                                   | Подходит для                                                         |
|----------------|---------------------------------------|----------------------------------------------|----------------------------------------------------------------------|
| **Callback**   | Простота, поддержка всех версий JS    | Callback Hell, сложная обработка ошибок      | Простейшие задачи, работа с устаревшим кодом                         |
| **Promise**    | Читаемость, централизованная обработка ошибок | Неявные ошибки, сложнее для новичков | Средние и сложные задачи, последовательное и параллельное выполнение |
| **Async/Await**| Лаконичность, синхронный стиль        | Совместимость, возможные блокировки          | Современные приложения, читаемый код                                 |

---

## Итог

- **Callback-функции** — хороший выбор для простых задач, но с ростом сложности кода они теряют свою привлекательность.
- **Promises** предлагают мощный инструмент для работы с асинхронным кодом, улучшая читаемость и поддержку.
- **Async/await** — лучший выбор для современных приложений, так как он упрощает написание и понимание кода.

Каждый подход имеет свои сильные стороны. Выбор зависит от задач проекта, целевой платформы и предпочтений разработчиков.

---

## ЗАДАЧИ
Задачи по теме "Callback-функции, Promise и async/await"

---

### Задача 1: Преобразование callback-функции в Promise

У вас есть функция, использующая callback для обработки результата. Перепишите её, чтобы она использовала `Promise`.

```javascript
function fetchData(callback) {
  setTimeout(() => {
    const error = Math.random() > 0.5; // Генерируем ошибку с вероятностью 50%
    if (error) {
      callback("Ошибка загрузки данных", null);
    } else {
      callback(null, "Данные успешно получены!");
    }
  }, 1000);
}
```

<details>
<summary>Решение</summary>

```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const error = Math.random() > 0.5;
      error ? reject("Ошибка загрузки данных") : resolve("Данные успешно получены!");
    }, 1000);
  });
}
```

</details>

---

### Задача 2: Сравнение подходов (Callback vs Promise)

Перепишите код ниже с использованием Promise. Заметьте, как изменяется читаемость.

```javascript
function fetchData(callback) {
  setTimeout(() => {
    const error = Math.random() > 0.5;
    if (error) {
      callback("Ошибка загрузки данных", null);
    } else {
      callback(null, "Данные успешно получены!");
    }
  }, 1000);
}

fetchData((error, data) => {
  if (error) {
    console.error("Произошла ошибка:", error);
  } else {
    console.log(data);
  }
});
```

<details>
<summary>Решение</summary>

```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const error = Math.random() > 0.5;
      error ? reject("Ошибка загрузки данных") : resolve("Данные успешно получены!");
    }, 1000);
  });
}

fetchData()
  .then(data => console.log(data))
  .catch(error => console.error("Произошла ошибка:", error));
```

</details>

---

### Задача 3: Преобразование Promise в async/await

Перепишите код, использующий Promise, на `async/await`.

```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const success = Math.random() > 0.5;
      success ? resolve("Данные получены!") : reject("Ошибка загрузки данных");
    }, 1000);
  });
}

fetchData()
  .then(data => console.log(data))
  .catch(error => console.error("Произошла ошибка:", error));
```

<details>
<summary>Решение</summary>

```javascript
async function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const success = Math.random() > 0.5;
      success ? resolve("Данные получены!") : reject("Ошибка загрузки данных");
    }, 1000);
  });
}

(async () => {
  try {
    const data = await fetchData();
    console.log(data);
  } catch (error) {
    console.error("Произошла ошибка:", error);
  }
})();
```

</details>

---

### Задача 4: Обработка ошибок с Promise

Напишите код, который при ошибке выводит сообщение "Ошибка: что-то пошло не так", используя `.catch()`.

```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const success = Math.random() > 0.5;
      if (success) {
        resolve("Данные успешно получены!");
      } else {
        reject("Ошибка загрузки данных");
      }
    }, 1000);
  });
}

fetchData()
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

<details>
<summary>Решение</summary>

```javascript
fetchData()
  .then(data => console.log(data))
  .catch(() => console.error("Ошибка: что-то пошло не так"));
```

</details>

---

### Задача 5: Переписывание с async/await

Перепишите код, использующий `Promise`, на `async/await`.

```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const success = Math.random() > 0.5;
      success ? resolve("Данные успешно получены!") : reject("Ошибка загрузки данных");
    }, 1000);
  });
}

fetchData()
  .then(result => console.log(result))
  .catch(error => console.error(error));
```

<details>
<summary>Решение</summary>

```javascript
async function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const success = Math.random() > 0.5;
      success ? resolve("Данные успешно получены!") : reject("Ошибка загрузки данных");
    }, 1000);
  });
}

(async () => {
  try {
    const result = await fetchData();
    console.log(result);
  } catch (error) {
    console.error(error);
  }
})();
```

</details>

---

### Задача 6: Использование всех подходов (Callback, Promise, Async/Await)

Напишите функцию, которая использует callback, а затем перепишите её на Promise и async/await.

**Условие:** Если результат операции больше 50, возвращаем успех, иначе — ошибку.

<details>
<summary>Решение</summary>

#### Callback:
```javascript
function fetchData(callback) {
  setTimeout(() => {
    const value = Math.random() * 100;
    value > 50 ? callback(null, value) : callback("Ошибка: значение меньше 50");
  }, 1000);
}
```

#### Promise:
```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const value = Math.random() * 100;
      value > 50 ? resolve(value) : reject("Ошибка: значение меньше 50");
    }, 1000);
  });
}
```

#### Async/Await:
```javascript
async function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const value = Math.random() * 100;
      value > 50 ? resolve(value) : reject("Ошибка: значение меньше 50");
    }, 1000);
  });
}

(async () => {
  try {
    const data = await fetchData();
    console.log("Успех:", data);
  } catch (error) {
    console.error(error);
  }
})();
```

</details>

---

Эти задачи помогут вам закрепить знания о различных подходах в асинхронном программировании в JavaScript.

---