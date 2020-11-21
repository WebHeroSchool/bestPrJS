# My JavaScript Best Practice Guide
## 1. ������������ ����������
---
 __�������� ���������� ������ ����� ����� � �������� �����, �������� � ���, ����� ������ � ��� ��������.__
+ ����������� ����� �������� �����, ����� ��� `userName` ��� `shoppingCart`.
+ ��������� ������������� ����������� ��� �������� ���, ����� ��� `a`, `b`, `c`, �� ����������� ��� �������, ����� �� ����� ������, ��� ��� �����.
+ ������� ����� ����������� ������������� � �����������. ������� ������ ���: `data` � `value`. ����� ����� ������ �� �������. �� ����� ������������ ������ � ��� ������, ���� �� ��������� ���� ��������, ����� ������ ������ ����������.


__Bad__
``` js
let a = 10;
let string = '������, ���!';
```
__Good__
``` js
let minSum = 10; //����������� �����
let greeting = '������, ���!'; //�����������
```

## 2. ������������ �������
---
��� ������ ��� � `function` ��������� �� �� �������, ��� � ����� �������� ����� ����������. ������ ������� �������, ��� ������ ������ ���� __������__, ���� ������� � ��� __��������__. ��� �������, � �������� ����� ���������� ���������� ��������, ���� ���������.

�������, ����� ������ ����� ������� �������:
```js
showMessage(..)     // "��������" ���������
getAge(..)          // get, "��������" �������
calcD(..)           // calc, "���������" ������������
createForm(..)      // create, "������" �����
checkPermission(..) // check, "���������" ����������, ���������� true/false
```
+ ����� �� ������� ������� ��������� � ��������� �������.

__Bad__
``` js
// ������� ���������� ��������� ����� �� ��������� �� min �� max
function func (a, b) {
  const d = b - a + 1;
  const c = a + Math.floor(Math.random() * d);
  return c;
}
 console.log( func(1, 100) );
```
__Good__
``` js
// ������� ���������� ��������� ����� �� ��������� �� min �� max
function getRandom (min, max) {
  const d = max - min + 1;
  const result = min + Math.floor(Math.random() * d);
  return result;
}
 console.log( getRandom(1, 100) );
```
## 3. ����� ������
---
+ ���� � ���� ������ ������ ������� ���������, �� ��� �������� ������ ���������. 
+ ��� �������� ������ ��������� ����� ������� 80.
+ ������� ��������, ���� ������� ��������� ��������� �� ����� �����, ������� ����� ��������� ����� ����������, � ����� ���������� ��� � ���� ����������.
+ ���� �������� JavaScript �� ���������� �� ����� ������, ������ ����� ��� ������� ���, ����� ��������� ��� �������.

__Bad__
``` js
function getRandom (min, max) {
  return min + Math.floor(Math.random() * max - min + 1);
}
 document.getElementById("demo").innerHTML = `��������� ����� - ${getRandom(1, 100)}`;
```
__Good__
``` js
function getRandom (min, max) {
  const d = max - min + 1;
  const result = min + Math.floor(Math.random() * d);
  return result;
}
 document.getElementById("demo").innerHTML =
    `��������� ����� - ${getRandom(1, 100)}`;
```

## 4. ���������� ����������
---
+ ���������� ���������� ���� � ������� `const`, ���� � ������� `let`. �������� ����� `var` �� ������ ��������������.
+ ������� ��������, ���� �� ��������� ������������ `const` , ���� ������ ���������� �� ��������� � ��������������. 
+ ��������� ���������� ����������

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

## 5. ���������� ��������, �������� � ��. ����� ������
---
+ ������ �������� ��������� ������ � ������� `new`.
+ ����������� {} ������ new Object()
+ ����������� "" ������ new String()
+ ����������� 0 ������ new Number()
+ ����������� false ������ new Boolean()
+ ����������� [] ������ new Array()
+ ����������� /()/ ������ new RegExp()
+ ����������� function (){} ������ new Function()

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

## 6. ������������������ ������ for..
---
��� ���������� ������� ���������� `for` �� ����������� ��������� ���� ������, ��� �� ������. ����� �������� ������������������ � ����� ������ ����� �����:
+ ��������� ���������� ��� ��������� `for`
+ ���������� ������ � ��������� ��� ���������� � �����

����� �������, �� ��������� �������� ��� �������� ����� ��������� ���� ��� �� ����, � �� ���������� � ���� �� ������ ��������.


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

## 7. �� ����������� ������ � "SetInterval" ��� " SetTimeOut"
---
���� ���������� ���� ��������� ������� �`SetInterval` ��� `SetTimeOut`, �� ��� ������� ������������� � ������������� ����. ������� ������� ���������� ������ ��� �������

__Bad__
``` js
setInterval(
"document.getElementById('container').textContent = '����� ����������!'", 3000
);
```
__Good__
``` js
const writeContext = function() {
  const container = document.getElementById('container');
  container.textContent = '����� ����������!'
}
setInterval(writeContext, 3000);
```
## 8. ���������������� ���� ���
---
������ ������� ������������ � ������ ���� � ����� ���, ��� ��������� � ��� � �������, �����, ��� � ������ � ���� ���� ��������.

__Bad__
``` js
const isPositive = arr.every(item => item > 0);
console.log(isPositive(arr));
```
__Good__
``` js
//������� ��������� ��� �� �������� ������� �������������
const isPositive = arr.every(item => item > 0);
console.log(isPositive(arr));
```

## 9. �� ����������� Short-Hand

+ ���� �������, ������ � ���������� ������ ����� ������ ������ �������� ������ `{}`.
+ ���� ���� ������� �� ����� ��������, �� ����� �������� �������� ������. �� ��� �������� ������ ���������, ���� ������ ���� �� ��������� ������.

__Bad__
``` js
if (result > 0) 
  result--;
  calcSum();
```
����� ������ �������� ������� ���������, ������� ������� ����������� ��������. � ������ ������, ����� ���� ������� �������� ������ `{}` ��� ���� ������� ��������� �������� � ���� ������.

__Good__
``` js
if (result > 0) {
  result--;
}
calcSum();
```


## 10. ��������� ���������
---
+ ����������� === � !== (������� ��������� ), ������ == � != (��������� ���������).

���� ������������ ������� ���������, �� ����� ���������� �������� ��-�� 
 �������� �������������� ����� ������, ������� ������������� �������� ��������� �������� ������� ���������. 

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
����������:
+ ��������� ���� ����������� ��������:
+ ����� typeof;
+ ��������� � null�