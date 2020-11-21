# My JavaScript Best Practice Guide
## 1. Наименование переменных
---
 __Название переменной должно иметь ясный и понятный смысл, говорить о том, какие данные в ней хранятся.__
+ Используйте легко читаемые имена, такие как `userName` или `shoppingCart`.
+ Избегайте использования аббревиатур или коротких имён, таких как `a`, `b`, `c`, за исключением тех случаев, когда вы точно знаете, что так нужно.
+ Делайте имена максимально описательными и лаконичными. Примеры плохих имён: `data` и `value`. Такие имена ничего не говорят. Их можно использовать только в том случае, если из контекста кода очевидно, какие данные хранит переменная.


__Bad__
``` js
let a = 10;
let string = 'Привет, мир!';
```
__Good__
``` js
let minSum = 10; //Минимальная сумма
let greeting = 'Привет, мир!'; //Приветствие
```

## 2. Наименование функций
---
При выборе имён в `function` применяют те же правила, что и когда выбирают имена переменной. Однако следует помнить, что именем должен быть __глагол__, ведь функция — это __действие__. Как правило, в качестве имени используют глагольные префиксы, плюс уточнения.

Примеры, каким именем можно назвать функцию:
```js
showMessage(..)     // "показать" сообщение
getAge(..)          // get, "получает" возраст
calcD(..)           // calc, "вычисляет" дискриминант
createForm(..)      // create, "создаёт" форму
checkPermission(..) // check, "проверяет" разрешение, возвращает true/false
```
+ Таким же образом следует именовать и аргументы функции.

__Bad__
``` js
// Функция возвращает рандомное число из диапазона от min до max
function func (a, b) {
  const d = b - a + 1;
  const c = a + Math.floor(Math.random() * d);
  return c;
}
 console.log( func(1, 100) );
```
__Good__
``` js
// Функция возвращает рандомное число из диапазона от min до max
function getRandom (min, max) {
  const d = max - min + 1;
  const result = min + Math.floor(Math.random() * d);
  return result;
}
 console.log( getRandom(1, 100) );
```
## 3. Длина строки
---
+ Если в одну строку писать длинные выражения, то это является плохой практикой. 
+ Для удобства чтения избегайте строк длиннее 80.
+ Хорошая практика, если длинное выражение разделить на такие части, которые можно присвоить новой переменной, и потом обращаться уже к этой переменной.
+ Если оператор JavaScript не помещается на одной строке, лучшее место для разрыва это, после оператора или запятой.

__Bad__
``` js
function getRandom (min, max) {
  return min + Math.floor(Math.random() * max - min + 1);
}
 document.getElementById("demo").innerHTML = `Рандомное число - ${getRandom(1, 100)}`;
```
__Good__
``` js
function getRandom (min, max) {
  const d = max - min + 1;
  const result = min + Math.floor(Math.random() * d);
  return result;
}
 document.getElementById("demo").innerHTML =
    `Рандомное число - ${getRandom(1, 100)}`;
```

## 4. Глобальные переменные
---
+ Объявляйте переменные либо с помощью `const`, либо с помощью `let`. Ключевое слово `var` не должно использоваться.
+ Хорошая практика, если по умолчанию использовать `const` , если только переменная не нуждается в переназначении. 
+ Уменьшите глобальные переменные

__Bad__
``` js
let name = 'Michael';
var age = 20;
const nationality = 'Russian';

console.log('His name is ' + name);
console.log('He is ' + age);
```
__Good__
``` js
const user {
  name: 'Michael',
  age: 20,
  nationality: 'Russian',
} 

console.log('His name is ' + user.name);
console.log('He is ' + user.age);
```

## 5. Объявление объектов, массивов и др. типов данных
---
+ Плохая практика объявлять данные с помощью `new`.
+ Используйте {} вместо new Object()
+ Используйте "" вместо new String()
+ Используйте 0 вместо new Number()
+ Используйте false вместо new Boolean()
+ Используйте [] вместо new Array()
+ Используйте /()/ вместо new RegExp()
+ Используйте function (){} вместо new Function()

__Bad__
``` js
const user = new Object();
user.name = 'Michael';
user.books = new Array();
user.books[0] = 'book1';
user.book[1] = 'book2';
user.getName = () => console.log(this.name);
```
__Good__
``` js
const user = {
  name: 'Michael',
  books: ['book1', 'book2'],
  getName: () => console.log(this.name),
}
```

## 6. Производительность циклов for..
---
При выполнении длинных операторов `for` не заставляйте выполнять цикл дольше, чем он должен. Чтобы ускорить производительность и время работы цикла можно:
+ объявлять переменные вне оператора `for`
+ ограничить доступ к свойствам или переменным в цикле

Таким образом, на некоторые действия или свойства будут ссылаться один раз за цикл, а не обращаются к нему на каждой итерации.


__Bad__
``` js
for (let i = 0; i < someArray.length; i++) {
   const container = document.getElementById('container');
   container.textContent = 'my number: ' + i;
   console.log(i);
}
```
__Good__
``` js
const container = document.getElementById('container');
length = someArray.length;
for (let i = 0; i < length; i++) {
   container.textContent = 'my number: ' + i;
   console.log(i);
}
```

## 7. Не передавайте строку в "SetInterval" или " SetTimeOut"
---
Если передавать само выражение функции в`SetInterval` или `SetTimeOut`, то это снижает эффективность и читабельность кода. Поэтому следует передавать только имя функции

__Bad__
``` js
setInterval(
"document.getElementById('container').textContent = 'Добро пожаловать!'", 3000
);
```
__Good__
``` js
const writeContext = function() {
  const container = document.getElementById('container');
  container.textContent = 'Добро пожаловать!'
}
setInterval(writeContext, 3000);
```
## 8. Прокомментируйте Свой Код
---
Пишите хорошую документацию к своему коду — тогда тот, кто столкнётся с ним в будущем, поймёт, что и почему в этом коде делается.

__Bad__
``` js
const isPositive = arr.every(item => item > 0);
console.log(isPositive(arr));
```
__Good__
``` js
//функция проверяет все ли элементы массива положительные
const isPositive = arr.every(item => item > 0);
console.log(isPositive(arr));
```

## 9. Не используйте Short-Hand

+ Тело функций, циклов и операторов всегда нужно писать внутри фигурных скобок `{}`.
+ Если тело состоит из одной операции, то можно опустить фигурные скобки. Но это является плохой практикой, если писать тело на следующей строке.

__Bad__
``` js
if (result > 0) 
  result--;
  calcSum();
```
Такой пример является ужасной практикой, которой следует обязательно избегать. В данном случае, можно тело условия написать внутри `{}` или само условие полностью написать в одну строку.

__Good__
``` js
if (result > 0) {
  result--;
}
calcSum();
```


## 10. Операторы сравнения
---
+ Используйте === и !== (строгое сравнение ), вместо == и != (нестрогое сравнение).

Если использовать неявное сравнение, то могут возникнуть проблемы из-за 
 неявного преобразования типов данных, поэтому использование строгого сравнения является хорошей практикой. 

__Bad__
``` js
a == b
result == 0
result == true
result == undefined
```
__Good__
``` js
a === b
result === 0
result === true
result === undefined
```
Исключения:
+ сравнение двух литеральных значений:
+ вызов typeof;
+ сравнение с nullю