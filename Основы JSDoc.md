---
tags: [JSDoc, JavaScript, groups]
---

> [!info]- Ссылки
> [[Теги]]

JSDoc - это стандарт, используемый для документирования JavaScript-кода. Он позволяет описывать структуру вашего кода, что может быть особенно полезно при работе в команде или для тех, кто будет использовать ваш код в будущем. Несмотря на то что мы используем TypeScript, JSDoc все еще может быть полезен для добавления дополнительной информации или описаний.

Основная структура комментария JSDoc выглядит так:

```typescript
/**
 * Описание функции
 *
 * @param {Тип} имя_параметра - Описание параметра
 * @returns {Тип} - Описание, что функция возвращает
 */
```

Скобки {} используются для обозначения типа переменных, а после @param и @returns следует краткое описание.

Например, представим функцию, которая суммирует два числа:

```typescript
/**
 * Возвращает сумму двух чисел
 *
 * @param {number} a - Первое слагаемое
 * @param {number} b - Второе слагаемое
 * @returns {number} - Сумма a и b
 */
const add = (a: number, b: number): number => {
	return a + b;
};
```

JSDoc также позволяет указывать типы для сложных структур данных, таких как объекты или массивы:

```typescript
/**
 * Возвращает объект, представляющий координаты точки
 *
 * @param {number} x - Координата x
 * @param {number} y - Координата y
 * @returns {Object} - Объект с полями x и y
 */
const createPoint = (x: number, y: number): {x: number, y: number} => {
	return { x, y };
};
```

```typescript
/**
 * Возвращает массив чисел, умноженных на два
 *
 * @param {number[]} nums - Массив чисел
 * @returns {number[]} - Массив чисел, умноженных на два
 */
const doubleNumbers = (nums: number[]): number[] => {
	return nums.map(num => num * 2);
};
```

JSDoc также позволяет использовать некоторые дополнительные теги для добавления информации:

- @throws {Тип} - описывает тип ошибки, которую может выдать функция
- @deprecated - указывает, что функция устарела
- @see - добавляет ссылку на другую функцию или внешнюю страницу

Пример:

```typescript
/**
 * Возвращает результат деления двух чисел
 *
 * @param {number} a - Числитель
 * @param {number} b - Знаменатель
 * @returns {number} - Результат деления a на b
 * @throws {TypeError} Если b равно 0
 * @deprecated Используйте функцию divideSafe вместо этой
 * @see {@link https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Error|Error MDN}
 */
const divide = (a: number, b: number): number => {
	if (b === 0) {
		throw new TypeError('Нельзя делить на ноль');
	}
	return a / b;
};
```

