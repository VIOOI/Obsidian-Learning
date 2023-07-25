---
tags: [ JavaScript ]
---
## Кратко

`Map` — коллекция для хранения данных любого типа в виде пар `[ключ, значение]`, то есть каждое значение сохраняется по _уникальному_ ключу, который потом используется для доступа к этому значению. Причём в качестве ключей тоже принимаются значения любого типа.

Основные методы для работы с коллекцией `Map`:

- `set(ключ, значение)` — устанавливает значение;
- `get(ключ)` — возвращает значение;
- `has(ключ)` — проверяет наличие переданного ключа;
- `values()` — возвращает [итератор](https://doka.guide/js/iterator/) всех значений коллекции;
- `keys()` — возвращает [итератор](https://doka.guide/js/iterator/) всех ключей коллекции;
- `entries()` — возвращает [итератор](https://doka.guide/js/iterator/) пар `[ключ, значение]`;
- `delete(ключ)` — удаляет конкретное значение;
- `clear()` — полностью очищает коллекцию;
- `forEach(колбэк)` — перебирает ключи и значения коллекции.

Содержит свойство `size` для получения количества значений в коллекции.

## Пример

```javascript
const someData = new Map()

someData.set('1', 'Значение под строковым ключом 1')
someData.set(1, 'Значение под числовым ключом 1')
someData.set(true, 'Значение под булевым ключом true')

console.log(someData.size)
// 3

console.log(someData.get(1))
// Значение под числовым ключом 1

console.log(someData.get('1'))
// Значение под строковым ключом 1

console.log(someData.has(true))
// true

someData.clear()

console.log(someData.size)
// 0

```

## Как понять

### Создание коллекции

Коллекция создаётся при помощи конструктора. Можно создать пустой `Map`:

```javascript
const map = new Map()

console.log(map.size)
// 0
```

А можно сразу передать начальные значения. Для этого в конструктор нужно передать массив, состоящий из других массивов. Эти массивы должны состоять из двух элементов: первый элемент — ключ, а второй — значение:

```javascript
const map = new Map([['js', 'JavaScript'], ['css', 'Cascading Style Sheets']])

console.log(map.size)
// 2

console.log(map.get('js'))
// JavaScript
```

### Работа с коллекцией

`Map` предоставляет небольшой набор удобных методов для работы с данными.

Чтобы сохранить значение в коллекции, нужно использовать метод `set()`. Первым аргументом передаём ключ, а вторым - значение:

```javascript
const map = new Map()

map.set('js', 'JavaScript')
```

Получить значение можно при помощи метода `get()` единственным аргументом которого передаём ключ, данные которого хотим получить. Если в коллекции нет значения для переданного ключа, `get()` вернёт [`undefined`](https://doka.guide/js/undefined/).

```javascript
const map = new Map()
map.set('js', 'JavaScript')

console.log(map.get('js'))
// JavaScript
```  

Узнать, есть ли в коллекции значение с конкретным ключом, можно с помощью метода `has()`:

```javascript
const map = new Map()
map.set('js', 'JavaScript')

console.log(map.has('js'))
// true

console.log(map.has('css'))
// false
``` 

Удалять конкретное значение можно методом `delete()`, который также принимает ключ в качестве аргумента. `delete()` возвращает `true`, если элемент для переданного ключа _существовал и был удалён_. Полностью очищает коллекцию метод `clear()`:

```javascript
const map = new Map()

map.set('html', 'HTML')
map.set('css', 'CSS')
map.set('js', 'JavaScript')

console.log(map.size)
// 3

map.delete('css')

console.log(map.size)
// 2

map.clear()

console.log(map.size)
// 0
```

### Обход значений

`Map` предоставляет встроенный итератор для обхода значений:

```javascript
const map = new Map()

map.set('html', 'HTML')
map.set('css', 'CSS')
map.set('js', 'JavaScript')

for (let [key, value] of map) {
  console.log(`${key} - ${value}`)
}
// html - HTML
// css - CSS
// js - JavaScript
```

А ещё можно сделать то же самое при помощи метода `forEach()`:

```javascript
const map = new Map()

map.set('html', 'HTML')
map.set('css', 'CSS')
map.set('js', 'JavaScript')

map.forEach((value, key) => {
  console.log(`${key} - ${value}`)
})
// html - HTML
// css - CSS
// js - JavaScript

```

> [!warning] Обратите внимание: когда вызывается метод `forEach()`, в колбэк передаются текущий ключ и соответствующее ему значение — индексов в `Map` нет.

При обходе значений `Map` всегда выводит их в том порядке, в котором они были добавлены.

### Отличия от объектов

Обычные объекты тоже подходят для хранения данных. Однако ключи в них могут быть только [строками](https://doka.guide/js/string/) или [символами](https://doka.guide/js/symbol/):

```javascript
const obj = {
  1: 'String',
  '2': 'Number',
  true:'Bool',
}

console.log(Object.keys(obj))
// [ '1', '2', 'true' ]
```

`Map` же позволяет использовать в качестве ключа любое значение: объект, функцию, примитивные значения и даже [`null`](https://doka.guide/js/null-primitive/), [`undefined`](https://doka.guide/js/undefined/) и [`NaN`](https://doka.guide/js/number/#specialnye-znacheniya). Для сравнения ключей используется алгоритм _SameValueZero_.

```javascript
const func = (name) => `Hello, ${name}`
const obj = { foo: 'bar' }

const map = new Map()
map.set(func, 'func value')
map.set(obj, 'object value')
map.set(undefined, 'undefined value')
map.set(NaN, 'NaN value')
map.set(null, 'null value')

console.log(map.get(func))
// func value

console.log(map.get(obj))
// object value

console.log(map.get(undefined))
// undefined value

console.log(map.get(NaN))
// NaN value

console.log(map.get(null))
// null value
```

При использовании SameValueZero для сравнения ключей, приведение типов не происходит. Поэтому, число и строковое представление этого же числа будут являться двумя разными ключами:

```javascript
const map = new Map()

map.set(1, 'numeric 1')
map.set('1', 'string 1')

console.log(map.size)
// 2

console.log(map.get(1))
// numeric 1

console.log(map.get('1'))
// string 1
```

При использовании непримитивных типов в качестве ключей стоит помнить, что они [хранятся по ссылке](https://doka.guide/js/ref-type-vs-value-type/), поэтому для доступа к заданному с помощью объекта ключу, необходимо передавать _тот же самый объект_.

Создадим две переменные, которые указывают на один и тот же объект и добавим их ключами в Map:

```javascript
const dataObject = { position: 'left' }
const sameObject = dataObject

console.log(dataObject === sameObject)
// true

const map = new Map()
map.set(dataObject, 'value for dataObject')
map.set(sameObject, 'value for sameObject')

console.log(map.size)
// 1

console.log(map.get(dataObject))
// value for sameObject

console.log(map.get(sameObject))
// value for sameObject
```

А вот если мы возьмём два отдельных объекта с одинаковым содержимым, то мы получим два разных ключа:

```javascript
const playerOne = { position: 'left' }
const playerTwo = { position: 'left' }

console.log(playerOne === playerTwo)
// false

const map = new Map()
map.set(playerOne, 'player 1')
map.set(playerTwo, 'player 2')

console.log(map.size)
// 2

console.log(map.get(playerOne))
// player 1

console.log(map.get(playerTwo))
// player 2
```