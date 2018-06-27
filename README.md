## Learn JavaScript

- [Типы данных](#Типы-данных)
- [Строки](#Строки)
- [Числа](#Числа)
- [Массивы](#Массивы)
- [Методы массивов](#Методы-массивов)
- [Объекты](#Объекты)
- [Прототипы объектов](#Прототипы-объектов)
- [Циклы](#Циклы)
- [Функции](#Функции)
- [Параметры функции](#Параметры-функции)
- [Стрелочные функции](#Стрелочные-функции)
- [Сallback](#callback)
- [Классы](#Классы)
- [DOM](#DOM)
- [Замыкание](#Замыкание)
- [Get/Set](#getset)
- [Обработчики события](#Обработчики-события)
- [Объект событий](#Объект-событий)
- [this - контекст исполнения функции](#this---контекст-исполнения-функции)
- [Декораторы](#Декораторы)
- [Оператор разворота](#Оператор-разворота)
- [Шаблонные строки](#Шаблонные-строки)
- [Модули](#Модули)





## Типы данных
Примитивные типы данных (строки, числа,...) передаются по значению, а все остальное (объекты) по ссылке.
```javascript
// Простые типы данных
var myNumber = 2525
    myString = "Somestring"
    myBool = true
    myNull = null
    myUndef = undefined

// Объектные типы
var obj = {name: "sorax"}
    array = [1, 2, 3]
    regexp = /w+/g
    func = function(){}
```
## Строки
### Получаем длину строки
```javascript
var string = "terrible";
string.lenght; // 8

'42'.length;   // 2
```


### Экранирование запрещенных символов
```javascript
'it's my life';
'ist\'s my life';
```


### Строки vs. символы

в JS нет типа данных для символа. Символ это строка с одним символом.
```javascript
'abcdef'.charAt(2);    // 'c'
'abcdef'.charAt(200); // ''
'abcdef'.charAt(-1);  // ''
```


### Конкатенация
```javascript
'abcdef'.charAt(0) + 'abcdef'.charAt(2) + 'abcdef'.charAt(4); // 'ace' 

'together' + 'again'; // 'together again'

12 + 'or' + '20'; // '12 or 20' (при склеивании числа и строки мы получаем строку)
```


### Строки и числа
```javascript
12 + ' or ' + '20'; // '12 or 20' (в этом примере чило 12 интерпретируется как строка и на выходе мы получаем строку)

'12' / 2 + 1 // 7; (при математической операции не сложении, а например делении происходит обратная ситуация. Тут 12 интерпретируется как число и мы получаем число на выходе)

'day' * 2; // NaN 
```

### Перевод числа в строку. Для этого истользуется оператор toString();
```javascript
var a = 42; // 42
a.toString(); // '42'
a.toString().lenght; // 2 (так как длина это число мы получаем строку)
a.toString().length.toString(); // '2' (и теперь обратно переводим это число в строку)
```

Метод `toString` вызывается под капотом при неявном приведении типов, например: `42 + '' === '42'`.
Важно, что это работает для любых объектов, в том числе собственных:

```js
var a = {};
a.toString = function() {
	return 'foo';
};

// true
a + '' === 'foo';
```

### Работа со скобками
```javascript
'Blink ' + 182 // 'Blink 182' (так есть строка, у нас все склеивается и мы получаем строку)

'Blink ' + 182 + 1 // 'Blink 1811' (ситуация аналогичная, не смотря на то, что у нас два числа. Все равно все склеится, так как у нас есть строка)

'Blink ' + (181 + 1) // 'Blink 182' (тут мы получим нужный результат, так как мы выводим математическую операцию "сложение" в скобки. На выходе мы получаем склеивание строки с результатом замкнутой математической операции)
```

### Сравнение строк (как ни странно, но строки стравниваются в алфавитном порядке. Это касается не только единичных символов, но и целых строк. В них сравнение идет посимвольно)
```javascript
'a' < 'b'; // true
'c' < 'b'; // false

'abcd' < 'abcd'; // false (мы получим false, так как на самом деле строки равны)
'abcd' < 'abdc'; // true (а тут получим true третий символ и первой строки больше)


'toy' === 't' + 'o' + 'y' // true (конкатенацию строк JavaScript интерпретирует как строку поэтому мы получим true)
```



## Числа 
### Ошибочные числа

1/0 = infinity
-1/0 = - infinity
NaN = не числовые значения

1. Любая операция с NaN дает NaN
2. NaN != NaN
3. isNaN(...)

### Преобразование
```javascript
var y = 43.81327
y.toFixed(); // '44'
y.toFixed(1); // 43.8
y.toFixed(2); // 43.1

var n = 7432
n.toString(); // '7432'
```
## Массивы
Массивы нужны для упорядоченного набора данных.

* Напоминает объект список, который обладает некоторыми методами и свойствами.

* Ни размер, ни тип элементов массива не фиксированы.

* "Длинна" массива не является верхней гранцей

(Это значит, что во дном массиве мы можем хранить числа одновременно со строками, объектами, null, undefined и т.д.)

### Рекомендуемый способ
```javascript
var myArray = [];
var cities = ['Moscow', 'Almaty', 'Kiev', 'New York'];
```
### Как отличить массив от объекта
```javascript
console.log(Array.isArray(name))
```

### Создание с помощью конструктора функции Array
```javascript
var a = newArray();
var b = newArray('Hey', 'You', 'Me');
var c = newArray(3);
```

### Length
* Length - это индекс последнего элемента + 1
* Значение length можно изменять

Не совсем логичное поведение.
Допустим у нас есть массив
```javascript
var a = ['a', 'b', 'c'];
a.length; // 3

a[0] // 'a'
a[1] // 'b'
a[2] // 'c'
a[3] // undefined
```

Затем мы добавляем элемент с индексом 10
```javascript
a[10] = 'what?'
```

И длина нашего массива становится равной 11 (индекс последнего элемента + 1) не смотря на то, что у нас 
образовалось пропасть между элементами с индексами 2 и 10
```javascript
a.lenght; // 11
```


### Удаление

* delete
* splice
```javascript
массив[1].delete // удалит элемент с индексом 2 (не рекомендован к использованию так как по сути после удаления оставляет undefined)
```
```javascript
массив.splice(3, 1); // откуда начать, сколько удалить
```


### Перебирающие методы массива


### Через for
```javascript
for(var i=0; i < a.lenght; i++) {
  // выведет все элементы массива (рекомендуется использовать forEach)
}
```

### Через forEach (рекоммендуется)
- Позволяет итерироваться по массиву. 
- Принимает один аргумент - функцию обратного вызова.
- Функция принимает 3 параметра: элемент массива, индекс элемента, сам массив(не обязательный).

```javascript
let arr = ['first', 'second', 77, true, null];

arr.forEach(function(item, index, array){
  console.log(`Индекс: ${index}, элемент: ${item}`)
});
```

### some
Проверяет отвечает хотя бы один элемент в масcиве условиям и возвращает булевое значение **true** или **false**.

```javascript
const data = [7, 14, 5, 12, 25];

const value1 = data.some(i => i > 10);
const value2 = data.some(i => i < 3);
console.log(value1) // true;
console.log(value2) // false;
```

### every
Возвращает **true** только если каждый элемент массива отвечает условиям, иначе **false**
```javascript
const data = [7, 14, 5, 12, 25];

const value1 = data.every(i => i > 10);
const value2 = data.every(i => i > 3);
console.log(value1) // false;
console.log(value2) // true;
```

Вместо стрелочной функции можно сделать и развернутую запись, так же все методы итерирования по массивам, колбэк функция принимает 3 параметра: элемент, индекс и сам массив.

```javascript
const value3 = data.every(function(i, index, array){
	return i > 3;
});
```


### filter
Проходит по массиву и возвращает новый массив с элементами, которые удовлетворяют заданным условиям. В **filter** передается функция, с параметром **элемента** внутри.

```javascript
const users = [
	{ id: 1, name: 'John', isAdmin: true },
	{ id: 1, name: 'Smith', isAdmin: true },
	{ id: 1, name: 'David', isAdmin: true }
];

const filtred = users.filter(i => item.id == 2);
console.log(filtered);
```

### map
С помощью метода **map** мы можем пройтись по каждому элементу массива, произвести какие-то действия с этим элементом и затем вернуть копию массива с измененными элементами.

В **map** передается функция, которая будет производить действия с элементами с двумя параметрами это **элемент** и **index**

```javascript
var array = [1, 2, 3, 4],
var mapped = array.map(function(element, index){
	return element + index
});

console.log(mapped);
```

### reduce
Работает с каждым элементом массива и сводит всю работу с массивом к одному результирующему значению. Метод **reduce** принимает функцию как параметр (это еще называется callback функция), у которой в свою очередь есть несколько параметров, это **аккумулирующее значение**, **сам элемент** и **index**.

Функция проходится по массиву начиная со второго элемента, параметр **acc** хранит результат выполнения предыдущей итерации.

```javascript
var array = [1, 2, 3, 4],
var raducedValue = array.raduce(function(acc, element, index){
	return acc + element
});

console.log(raducedValue);
```

## Методы массивов

### push
Чтобы добавить элемент в конец массива, воспользуйтесь методом **push**. Введите **.push** после имени массива, а после в круглых скобках укажите элемент который нужно добавить.

```javascript
var animals = [],
animals.push('Кот');
animals.push('Пес');
animals.push('Лама');

console.log(animals.length) // 3
```

### pop
Убрать из массива последний элемент можно, добавив к его имени .pop(). Метод pop делает сразу два дела: удаляет последний элемент из массива и возвращает этот элемент в виде значения.
```javascript
var animals = ['Кот', 'Пес', 'Лама'];
animals.pop();
console.log(animals) // 'Кот', 'Пес'
```

### shift
Работает аналогично **pop**, но элемент берется из начала массива.
```javascript
var animals = ['Кот', 'Пес', 'Лама'];
animals.shift();
console.log(animals) // 'Пес', 'Лама'
```

### unshift
Добавляет элемент в начало массива.

```javascript
var animals = ['Кот', 'Пес', 'Лама'];
animals.unshift('Медведь');
console.log(animals) // 'Медведь', 'Кот', 'Пес', 'Лама'
```

### concat
Конкатенация массивов

```javascript
var str1 = "Hello ";
var str2 = "world!";
var res = str1.concat(str2);
```

### join
Превращает массив в строку, в качестве параметра указывается разделитель для элементов

```javascript
var planets = ['Меркурий', 'Венера', 'Земля', 'Марс'];
planets.join('+');
console.log(planets) // 'Медведь'+ 'Кот'+ 'Пес'+ 'Лама'
```

### reverse
Данный метод изменяет исходный массив. После его применения порядок элементов в массиве меняется на обратный

```javascript
var planets = ['Меркурий', 'Венера', 'Земля', 'Марс'];
planets.reverse();
console.log(planets) // 'Марс', 'Земля', 'Венера', 'Меркурий'
```

### sort
Сортировка происходит по алфавиту английского языка. Метод приемлем для работы со строковыми величинами. Числа будут группироваться по первой цифре.

```javascript
var planets = ['Меркурий', 'Венера', 'Земля', 'Марс'];
planets.sort();
console.log(planets) // 'Венера', 'Земля', 'Марс', 'Меркурий'
```

Любопытно, что массив чисел так же будет восприниматься как массив строк:

```js
var numbers = [1, 5, 10, 20];
numbers.sort();
console.log(numbers); // [1, 10, 20, 5]
```

`10 < 5`, потому что на самом деле сравниваются строки '10' и '5', а не числа.

Чтобы этого избежать нужно явно указать как именно мы сраниваем элементы:

```js
var numbers = [1, 5, 10, 20];
numbers.sort((a, b) => a > b);
console.log(numbers); // [1, 5, 10, 20]
```

## Объекты

* **Объект** - контейнер со свойствами;
* **Все** - объекты (кроме чисел, строк, true/false - переменных, null и undefined);
* **Функция** - объект, массив - объект, объект - объект;
* **Порядок** — традиционно на порядок следования ключей в объекте не закладываются (на прядок закладываются в массиве).



### Пример объекта
```javascript
var obj = {};

var person = {
	'name' : 'Alex',
	'age' : 25
}
```

### Обращение
```javascript
persone.name; // 'Alex'
persone.age; // 25
```

Идентификатор свойства может быть указан без кавычек, но если идентификатор свойства пустая строка, тогда нам необходимо поставить кавычки.

### Пример объекта
```javascript
var person = {
	name : 'Alex',
	age : 25
	'' : 'WEIRD!'
}
```
### Обращение (можно обращаться через квадратные скобочки)
```javascript
a['name']; // 'Alex'
a['age']; // 25
a[''];	// 'WEIRD!'
```


Названия индентификаторов объектов не всегда нужно оборачивать в кавычки, за исключением тех случаев, когда в названиях используются спецсимволы.
```javascript
var person = {
	name : 'Alex', // ок
	bad-thing : 22, // ошибка
	'good-thing' : 23, // ок
	':;;:' : 24 // ок
};
```


### Вложенность 

Значение свойства может содержать число, строку, но также ничего не мешает ему содержать другой объект.
```javascript
var persone = {
	name : 'Alex',
	wife : {
		name : 'Eve',	
		age : 29;
	}
	age : 25
};
```



### Обращение к вложенным данным
```javascript
person.wife; // Object
person.wife.age; // 29
person.wife.wife // undefined
```


### Обновление
```javascript
var person = {
	name : 'Alex',
	age : 25
}

person.height; // undefined (так как нет свойства height)

person.name = 'Peter'; (перезаписываем значение)
persone.height = 178; (добавляем свойство)

person.name; // 'Peter'
person.height; // 178
```

### Копирование одного объекта в другой
```javascript
var name = {
	first: 'Mike',
	second: 'Will'
};

var karma = {
	status: 'top',
	role: 'admin'
};

Object.assign(name, karma);  // Object.assign(target, ...sources)
```

### Можно пожно получить массив всех ключей объекта
```javascript
var name = {
	first: 'Mike',
	second: 'Will'
};

Object.луны(name);  // [first, second]
```

### Атрибуты свойств (Object.defineProperty)
...


## Get/Set
Геттеры и сеттеры в синтаксисе с get/set работают при обращении к свойству класса вместо вызова метода. Они вызываются обычно у публичных методов. Они и нужны только для внутреннего устройства класса. Не стоит их явно вызывать у объектов. (в другом синтаксисе: пишутся с подчеркиванием)

```javascript
class GetThings {
  constructor(size) {
    this.length = size;
  }
  
  get Length() {
    return this.length;
  }
  
  set Lenght(value) {
    this.length = value;
    console.log('Значение установленно');
  }  
}

/*
var thing = new GetThings(9);
thing.Length;
thing.Length = 10;
https://www.youtube.com/watch?v=nx6DFeNIXlA
*/
```



### ES6
В ES6 если название свойства совпадает со значением, то мы можем писать только значение.
Геттер и Сеттер записываются короче.
```javascript
let firstName = 'Bill',
    lastName = 'Gates',
    email = 'bill@microsoft.com';
    
let persone = {
	firstName,
	lastName,
	email,
	get fullName() {
		return this.firstName + ' ' + this.lastName;
	},
	set fullName(value) {
		this.firstName = value;
	}
}

console.log(persone);
```


## Прототипы объектов 
Объекты в JavaScript можно организовать в цепочки так, чтобы свойство, не найденное в одном объекте, автоматически искалось в другом.

Прототипом называется объект в котором осуществляется поиск, если не нашли в самом текущем объекте.

Связующим звеном выступает специальное свойство __proto__.

### Прототип proto

```javascript
Если один объект имеет специальную ссылку __proto__ на другой объект, то при чтении свойства из него, если свойство отсутствует в самом объекте, оно ищется в объекте __proto__.

Свойство __proto__ доступно во всех браузерах, кроме IE10-, а в более старых IE оно, конечно же, тоже есть, но напрямую к нему не обратиться, требуются чуть более сложные способы, которые мы рассмотрим позднее.

var e = {
  eat: 'fish'
}

function Animal(name) {
  this.name = name;
  this.__proto__ = e; 
}

var bear = new Animal('bear');
console.log(bear.eat); / fish
```

## Циклы 

### For

for (инициализация; тест; инкремент) {
  тело цикла
}
  
```javascript
for (i = 1; i < 10; i++) {
  console.log(i)
}
```

```javascript
for (i = 1=; i--) {
  console.log(i)
}
```

### While

```javascript
while (выражения) {
  инструкция
}
```

```javascript
var i = 10;
while(i--) {
  console.log(i)
}
```

### Do While

```javascript
do 
  инструкция; 
while 
  (выражение)
```

```javascript
  do 
    console.log(i);
  while
    (i < 10);
```


## Функции
Функция - это объект

* Со свойствами name, lenght и prototype;
* Может использоваться как любой другой объект: хранить в переменных, других объектах (Если функция находится внутри объекта, то мы называем эту функцию методом), передаваться как аргумент, возвращать как значение;
* Функциям можно задавать свойства и методы;
* В отличии от других объектов функцию можно вызвать.

### Общий вид функции
```javascript
зарезервированное_слово имя_функции(параметры) {
  тело функции // параметры внутри в теле функции являются переменными
}
```
### Анонимная функция
имя_функции - необязательно, если его нет то такую функцию мы называем анонимной.


## Стрелочные функции
Стрелка должна идти сразу после параметров, если спустить ее на строку ниже, то получим ошибку

### Функция с двумя параметрами
```javascript
/* Старый синтаксис */
function add(x, y){
	return x + y;
}

/* Новый синтаксис */
let add =(x, y) => x + y;
```


### Функция с одним параметром
Если функция принимает только один параметр, то нет необхоимости его заключать в круглые скобки
```javascript
/* Старый синтаксис */
let square = function(x){
	return x * x;
}

/* Новый синтаксис */
let square = x => return x * x;
```


### Функция, которая вообще не принимает параметров
```javascript
/* Старый синтаксис */
let givMeAnswer = function(){
	return 42;
}

/* Новый синтаксис */
let givMeAnswer = () => return 42;
```

### Функция, которая не возвращает ничего
```javascript
/* Старый синтаксис */
let log = function(){
	console.log('Logging');
}

/* Новый синтаксис */
let log = () => console.log('Logging');
```

### Функция, тело которой состоит из двух строк
Если в теле функции несколько строк, мы должны использовать фигурные скобки и также мы должны указать что функция возвращает.
```javascript
/* Старый синтаксис */
let multuply = function(x, y){
	var result = x * y;
	return result;
}

/* Новый синтаксис */
let multuply = (x, y) => {
	var result = x * y;
	return result;
}
```


### Функция, которая возвращает литерал объекта
Если функция возвращает литерал объекта, то нам нужно обернуть его в круглые скобки
```javascript
/* Старый синтаксис */
let getPersone = function(x, y){
	return { name : 'John' };
}

/* Новый синтаксис */
let getPersone = (x, y) => ({ name : 'John' });
```

### Функция, которая вызывается и тут же возвращается (IIFE)
IIFE - Immediately Invoked Function Expression

```javascript
/* Старый синтаксис */
(function(){
	console.log('IIFE');
})();

/* Новый синтаксис */
(() => console.log('IIFE'))();
```

/* Написать про практическое применение стрелочных функций с Массивами */


## Параметры функции
```javascript
function great(greating = "Hello" name="friend") {
	console.log(`{$greating}, {$name}`);
}

great('Hi', 'Bill');
great('Hi');
great('undefined', 'Bill');
great();
```

### Функция высшего порядка
Функция высшего порядка — это функция которая принимает другую функцию как аргумент или возвращает ее
```javascript
```

## Callback
### Что такое функция callback

Функцию, которая передается внутрь как аргумент называют callback функцией или функцией обратного вызова.

Это функция которую запустят позднее. Как пример callback-а можно привести обычный обработчик события.

Коллбэки нужны чтобы вы могли запустить функцию не прямо сейчас, а чтобы другая функция могла запустить ее позже. Например браузер может запустить функцию после того как выпонится событие (например клик). Либо вы сами можете запустить функцию, когда что-то произойдет.

Как пример функция вопрос. Допустим я хочу спросить пользователя о чем-нибудь. И в случае если он скажет свое имя мне нужно сделать какое-то одно действие (например doSomething). Иначе другое действие (handleError).

Зачем это может понадобиться? Представьте вам нужно 20 раз спросить имя человека вы же не будете 20 раз писать prompt. 
Если он не ввел значение вам нужно 20 раз обработать это как ошибку вы же не будете 20 раз ставить if.

Для этого вы делаете функцию, функцию Ask.

https://yadi.sk/i/ZNS6HDNr3EFgS3


## Классы
Классы нужны для того, чтобы штамповать объекты

Свои классы на прототипах. Используем ту же структуру, что JavaScript использует внутри себя, для объявления своих классов.

### Обычный конструктор

Вспомним, как мы объявляли классы ранее.

Например, этот код задаёт класс Animal в функциональном стиле, без всяких прототипов:

```javascript
function Animal(name) {
  this.speed = 0;
  this.name = name;

  this.run = function(speed) {
    this.speed += speed;
    alert( this.name + ' бежит, скорость ' + this.speed );
  };

  this.stop = function() {
    this.speed = 0;
    alert( this.name + ' стоит' );
  };
};

var animal = new Animal('Зверь');

alert( animal.speed ); // 0, начальная скорость
animal.run(3); // Зверь бежит, скорость 3
animal.run(10); // Зверь бежит, скорость 13
animal.stop(); // Зверь стоит
```

### Класс через прототип

А теперь создадим аналогичный класс, используя прототипы, наподобие того, как сделаны классы Object, Date и остальные.

Чтобы объявить свой класс, нужно:

Объявить функцию-конструктор. Записать методы и свойства, нужные всем объектам класса, в prototype.
Опишем класс Animal:

```javascript
// конструктор
function Animal(name) {
  this.name = name;
  this.speed = 0;
}

// методы в прототипе
Animal.prototype.run = function(speed) {
  this.speed += speed;
  alert( this.name + ' бежит, скорость ' + this.speed );
};

Animal.prototype.stop = function() {
  this.speed = 0;
  alert( this.name + ' стоит' );
};

var animal = new Animal('Зверь');

alert( animal.speed ); // 0, свойство взято из прототипа
animal.run(5); // Зверь бежит, скорость 5
animal.run(5); // Зверь бежит, скорость 10
animal.stop(); // Зверь стоит
```

В объекте animal будут храниться свойства конкретного экземпляра: name и speed, а общие методы – в прототипе.

Совершенно такой же подход, как и для встроенных классов в JavaScript.

Инстанс конструктора - это результат работы конструктора.

### Класс ES6
```javascript
class ItemClass {
	constructor () {
	
	}
}
```

Конструктор - это функция, которая создает объекты, давая им набор заранее определенных свойств и методов. Представьте себе что это машина по созданию объектов, вроде фабрики, которая штампует тысячи копий одно и того же товара. Задав конструктор вы сможете создавать с его помощью лобое количество одинаковых объектов.


Наследование нужно если мы хотим использовать какой-то другой класс, который будет обладать всеми теми же методами и еще какими-нибудь другими. Например для детских товаров. И в ES2015 нет ничего проще чем сделать это. Просто указать ключевое слово **extends**. По сути мы объявляем класс, который расширяет объявленный нами класс до этого. Но тут есть еще одно требование для того чтобы наследовать один конструктор от другого. И для этих целей в ES2015 есть ключевое слово **super()** которое нужно вызвать внутри этого конструктора (внутри конструктора в ‘супере’, содержится ссылка на конструктор родителя). В этот момент в него записываются все свойства объявленные внутри конструктора родителя.

```javascript
class ChildItemClass extends ItemClass {
	constructor () {
		super()
	}
}
```

Так же классу и его конструктору можно пробрасывать аргументы, если они есть

```javascript
class ChildItemClass extends ItemClass {
	constructor (…args) {
		super(…args)
	}
}
```

Статические методы это методы объявленные в неймспейcе самого конструктора, просто тупо записанные в функцию как свойства (пользуемся тем что функции в JS это объекты и пишем в них что захотим).

Публичные методы методы это методы ...


## Замыкание
Это идея в программировании очень старая и очень мощная и это одна из тех вещей, которая в JavaScript сделана хорошо.

Если мы в функции используем переменную находящуюся в глобальном объекте, то мы не можем гарантировать, что ничего не взорвется. К примеру туда может быть подключена либа, в которой переменные называются также и тогда будет конфликт.

Мы создаем переменную каждый раз когда вызываем функцию

```javascript
var getAnswer = fucnction(){
	var answer = 42;
	return answer;
};
```

/* Но если мы делаем замыкание, то мы имеем доступ к */

Мы создаем переменную getAnswer и задаем значение этой переменной тому что вернет внутренняя функция. Внутренняя функция имеет доступ к тому что находится вне ее. И на самом деле мы обращаемся к answer в тот момент когда его уже не существует так как мы обращаемся после того, как она завершила свою работу. Тем не менее мы имеем доступ к тому что было внутри функции в момент запуска - это и есть замыкание.

```javascript
var getAnswer = (function() {
	var answer = 42;

	return function inner(){
		returm answer;
	};
}());
```


Еще одна формулировка замыкания

Замыкание это когда мы из фунции можем вернуть функцию и у той функции, которую мы вернули мы можем иметь доступ к тем аргументам, которые мы передали в первый раз (https://youtu.be/t4AhK0oWd9I?t=421)



## DOM

### Дерево DOM
DOM нужен для того, чтобы манипулировать страницей. Дом это объектная модель документа. Любой узел является объектом и через JavaScript мы можем изменять его свойства

```javascript
document.body.backgroundColor = 'red'
```
Через JavaScript можно динамически создавать новые элементы, добавлять их на страницу, удалять их со страницы и т.д.
```javascript
document.documentElement // Соответствует тегу html
```
```javascript
document.body // Соответствует тегу body
```

Получив ссылку на элелемент, можно побродить по его потомкам.
```javascript
document.body.firstChild
```

```javascript
document.body.firstNodes[0]
```

```javascript
document.body.firstChild.nextSibling
```

```javascript
document.body.firstChild.nextSibling.nextSibling
```

Мотод для получения всех дочерних узлов исключая пробел. Children это псевдомассив, который содержит все узлы и элементы.
```javascript
document.body.children
```

Помимо универсальных навигационнах ссылок есть дополнительние. Например для форм, для таблиц.
```javascript
 table.rows[0].cells[1]
 ```
 
Свойство которое показывает тип узла. Сущетвует всего 12 типов узлов (узел элемент 1, текстовый узел 3).
```javascript
document.body.nodeType
```
Свойство, которое показывает имя узла (всегда большими буквами).
```javascript
document.body.nodeName
```

Свойство содержимого. C помощью него можно как получить содержимое, так присвоить (это свойство есть только у узлов элементов, у текстовых узлов его нет).
```javascript
document.body.innerHTML
```

Для текстовых узлов используется свойство data, оно так же позволяет получать и менять содержимое.
```javascript
document.body.firstChild.data // предположим что это текст
```
### Атрибуты и пользовательские свойства
Методы для работы с атрибутами.
```javascript
getAttribute(name)
setAttribute(name, value)
hasAttribute(name)
removeAttribute(name)
attributes(name) // коллекция котора все аттрибуты
```

```javascript
ol.getAttribute('data-description') // <ol data-description="Свойства и методы для работы с атрибутами">
```
Получается, что с одной стороны у DOM элементов есть свои свойтва, как у обычных элементов, с другой стороны есть атрибуты, которые можно устанавливать с помощью методов.


### Методы поиска
```javascript
document.getElementById(id)
document.getElementByName(name)
document.evaluate(xpath)
elem.getElementByTagName(tag)
elem.getElementByClassName(className)
elem.querySelectorAll(css)
elem.querySelector(css) // Современный способ
```



## Обработчики событий
### Обработка событий через атрибут (быстрый способ на коленке)

```html
<ul>
	<li onclick="alert('привет')"></li>
</ul>
```

### Обработка событий через свойство (хоть сколько-нибудь масштабируемый код, позволяет поставить обработчик только одного типа на элемент)

```javascript
var li = document.querySelector('li'); //получаем ссылку на элементы
li.onclick = function(){ // и ставим ему свойство
  alert('привет')l
}
```

### Современные методы назначения обработчиков, позволяют поставить несколько обработчиков на одно событие
Он получает имя сообытия например клик, функцию обработчик, третий аргумент который обычно равен false.

```javascript
var li = document.querySelector('li');

function sayHi(){
  alert('Привет!');
}

function sayHi2(){
  alert('Привет, еще раз!');
}

li.addEventListener('click', sayHi, false);
li.addEventListener('click', sayHi, false);
```


### Удаление обработчика
Для того чтобы удалить обработчик его сначало нужно куда-нибудь записать.
```javascript
var f = function sayHi(){
  alert('Привет');
}

li.addEventListener('click', f, false);
li.removeEventListener('click', f, false);
```


В обработчике события this это текущий элемент на котором сработал обработчик, доступ к нему можно получить следующим образом.
```javascript
var f = function sayHi(){
  alert(this);
}

li.addEventListener('click', f, false);
```
## Объект событий 
Для того чтобы обработать событие нам мало знать на каком элементе оно произошло, могут понадобиться дополнительные детали произошедшего и они находятся в специальном объекте event. Он передается первым аргументам в функцию обработчик событий. У него очень много свойств. Он содержит как свойства вообще любых событий, например:
- event.type (тип события)
- event.target (элемент на котором произошло собыитие)

Так и свойства, которые есть только у событий мыши. Например, свойства:
- clientX: 57
- clientY: 81

Однако у браузеров есть рассинхрон относительно свойств событий. Поэтому для работы с событиями лучше воспользоваться фреймворком, даже если вы предпочитаете работать на чистом JavaScript



## this - контекст исполнения функции 

This это переменная которая ссылается на текущий объект (ещё иногда говорят на текущий контекст)

### this Default Binding
**this будет ссылаться на Lexical scope в котором вызывается функция (в данном случае глобальный объект).**
```javascript
function foo() {
  console.log(this.a);
}

var a = 2;

foo();
```


### this Implicit Binding (скрытое связывание)
**this будет указывать на объект из которого вызывается функция.**
```javascript
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
  foo: foo
}

obj.foo;
```


### this Explicin Binding (явное связывание)
**Явно задаем объект (c помощью call или apply) на который будет указывать this.**
```javascript
function foo() {
  console.log(this.a);
}

var a = 'global';

var obj = {
  a: 2
}

foo.call( obj ) //2
foo.apply( obj ) //2
```

Чтобы указать контекст выполнения любой функций вы можете использовать три метода: **call**, **apply** и **bind**. При использовании первых двух методов происходит вызов функции «на месте», метод bind функцию не вызывает, вместо этого он возвращает новую функцию с заданным контекстом.


/* Тут написать пример для bind */


/* Тут написать пример для стрелочных функций. У стрелочных функций свое поведение */




### this New Binding (связывание при создание объекта через конструктор)
** Как работает конструктор:**
- На лету создается новый объект;
- Этот объект становится контекстом исполнения данной функции (именно в даный момент);
- Функция автоматически вернет это объект, даже если мы ничего не будем возвращать.

```javascript
function foo() {
  this.a = a;
}

var bar = new foo(2);

console.log( bar.a ); //2
```


## Декораторы
Декоратор позволяет мощно и гибко модифицировать поведение функции (обертка, которая модифицирует поведение функции).

Декоратор это функция, она получает другую функцию и какие-то параметры. Ее задача это вернуть обертку вокруг функции.
Это обертка иногда что-то делает потом возвращает функцию (и потом может опять что-то делает с результатом).

```javascript
// decorator(f, ...) = обертка вокруг f
```

Смысл обертки это модифицировать поведение f при этом синтаксис вызова как правило остается таким же

```javascript

function doubleDqecorator(f) {
	return function(){
		return 2*f.apply(this, arguments); /* f.apply(this, arguments) передаем все аргументы, которые получила обертка */
	}
}

function sum(a + b) {
	return a + b;
}

sum = doubleDecorator(sum);

alert( sum(1,2) ); //6
```


## Оператор разворота
Допустим имеется два массива и мы хоти перенести элементы первого массива во второй. Для этого мы и можем использовать оператор разворота, который развернет первый массив и вставит его значения во второй.

```javascript
let staticLanguages = ['C', 'C++', 'Java'];
let dynamicLanguages = ['Java', 'PHP', 'Ruby'];
let languages = [ ...staticLanguages, 'C#', ...dynamicLanguages, 'Python'];
console.log(languages);
```

Еще один пример, допустим имеется массив let array = [1,2,3] и есть функция doSomething (X,X,X), функция принимает три аргумента и у массива есть три элемента. Сам массив отправить в функцию мы не можем, но мы можем развернуть массив в аргуметы функции используя оператор разворота.

```javascript
function add(x, y, z) {
	console.log(x + y + z);
}

let numbers = [1, 2, 3];

add(...numbers);
```

## Шаблонные строки
Поддерживают многострочность, интерполяцию выражений и тегирование.
```javascript
function createEmail(to, from, subject, message) {
	console.log(` 
		To: ${to},
		From: ${to},
		Subject: ${subject},
		Message: ${message}
	`)
}

createEmail(meeq@yamoney.ru, mikhail@koloskov.kz, Привет!, Как дела?);
```
## Модули

Вы можете дробить код на отдельные модули. В JavaScript один модуль — это один файл.
Объединение кода, расположенного в разных модулях, происходит через:

1. Экспорт чего-то из модуля.
2. Импорт в другой модуль.

### Экспорт и два способа импорта

Поставьте **export** перед тем, что вы хотите экспортировать. Такая операция сделает это импортируемым куда угодно:

```javascript
export const pi = 3.14;
export const e = 2.718;

export const square = (x) => {
  return x * x;
};

export const surfaceArea = (r) => {
  return 4 * pi * square(r);
};
```

Импортируйте специфичные штуки таким способом:

```javascript
import { surfaceArea, square } from './math';

const surfaceOfMars = surfaceArea(3390);
const surfaceOfMercury = surfaceArea(2440);
const yearSquared = square(2017);
```

'./math' означает "из файла math.js, расположенного в той же (текущей) папке".

Или импортируйте всё:

```javascript
import * as mathematics from './math';

const surfaceOfMars = mathematics.surfaceArea(3390);
const surfaceOfMercury = mathematics.surfaceArea(2440);
const yearSquared = mathematics.square(2017);
```
Это значит: "импортировать весь модуль и назвать его mathematics в этом модуле". Вот почему к импортированным сущностям обращение происходит через mathematics вот так: mathematics.surfaceArea.

### Экспорт по умолчанию

Вы можете сделать одну позицию экспортируемой по умолчанию.

```javascript
const pi = 3.14;
const e = 2.718;

const square = (x) => {
  return x * x;
};

const surfaceArea = (r) => {
  return 4 * pi * square(r);
};

export default surfaceArea;
```

Можно также экспортировать функцию или константу без имени:

```javascript
const pi = 3.14;
const e = 2.718;

const square = (x) => {
  return x * x;
};

export default (r) => {
  return 4 * pi * square(r);
};
```

Импортирование чего-то, что было экспортировано по умолчанию:

```javascript
import surfaceArea from './math';

const surfaceOfMars = surfaceArea(3390);
```

При экспорте функции без имени, её имя в модуле будет определяться в момент импорта, т.е. один и тот же экспорт может иметь разные имена в разных модулях:


**math.js**

```javascript
export default () => {
  ///
};
```

**import1.js:**

```javascript
import something1 from './math';
```


**import2.js:**

```javascript
import something2 from './math';
```
