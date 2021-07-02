# 10bestpracticeJS
JavaScript Best Practice Guide

## Содержание

1. [Переменные, функции, классы](#переменные)
    - [Правило №1](#правило-1)
    - [Правило №2](#правило-2)
    - [Правило №3](#правило-3)
    - [Правило №4](#правило-4)
2. [Функции](#функции)
    - [Правило №5](#правило-5)
    - [Правило №6](#правило-6)
3. [Создание объекта](#создание-объекта)
    - [Правило №7](#правило-7)
    - [Правило №8](#правило-8)
4. [Пробелы](№пробелы)
    - [Правило №9](#правило-9)
5. [Скобки](#скобки)
    - [Правило №10](#правило-10)


## Переменные, функции, классы

### Правило №1
1) Должны быть простыми и понятными имена переменных, функций и классов.
Названия функций должны быть краткими и содержательными. Например, если мы хотим создать переменную для хранения чьего-то дня рождения, она должна иметь имя, явно указывающее на это.
Это означает, что не должно быть имён типа b, также как и не должно быть излишне громоздкое и перенасыщенное посторонними словами.

Плохо 👎 :
```soVeryUselessLongBirthdayVariable ```

Хорошо :wink:  :
```birthday```

2) Кроме этого, лучше избегать комбинирования имени с функциональностью в названии переменной. Например, если мы хотим написать функцию по проверке достижения пользователем совершеннолетия, мы должны назвать её чем-то вроде isAdult(), а не isOverEighteen().

Плохо 👎 :
```isOverEighteen()```

Хорошо :wink:  :
``` isAdult()```

Это также имеет больше смысла, так как не в каждом месте возраст 18 лет является возрастом совершеннолетия.
Мы также можем рассмотреть венгерскую нотацию для именования переменных и функций. Нотация объединяет в себе тип возврата, и имя в одно название. Поскольку JavaScript-функция не имеет определённого типа возврата, мы можем добавить префикс типа для функции.
Например, если переменная возвращает булево значение с помощью функции isAdult(), мы можем написать bIAdult() с указанием b, что она является булевым значением.

3)  Рекомендуется хранить имена на английском языке, так как это сохраняет консистентность стиля в соответствии с остальным кодом. Все зарезервированные слова, такие как function и new - всё на английском языке, так что всё остальное должно быть на английском.
Английский также более интернациональный язык, так что вероятность больше, что разработчики знают английский язык, и смогут прочитать ваш код.

Плохо 👎 :
```vzroslyi() / взрослый()```

Хорошо :wink:  :
 ```isAdult()```
 
4) Классы - это функции, которые создают другие объекты, поэтому их названия должны отражать это. Например, если у нас есть класс, который создаёт объект человека, то он должны быть названы как Person.

Плохо 👎 :
```
class FirstObject
```
Хорошо :wink:  :
```
class Person
```
5) Имена классов должны быть в верхнем регистре и указывать, какой именно объект мы из него создаём.

Плохо 👎 :
```
class thistest
```
Хорошо :wink:  :
```
class ThisTest
```
6) Избегать частого использования глобальных переменных и функций.

Плохо 👎 :
```
var num = 5;
 
function foo() {
  console.log(num);
}
var num = 8;
foo();                // 5
console.log(num);     // 5
{
  console.log(num);   // 5
}
var num = 10;
```
Хорошо :wink:  :
```
var num = 5;
 
function foo() {
  console.log(num);
}
 
foo();                // 5
console.log(num);     // 5
{
  console.log(num);   // 5
}
```
В JavaScript всё запускается в одной и той же области видимости. И это реальная проблема, потому что некоторые данные могут быть случайно изменены в одной части кода, которая повлияет на другой код, использующий эти же данные.
К счастью, начиная с ES6, JavaScript имеет несколько возможностей для решения этой проблемы. Одна из них - использование модулей. С модулями, только то, что мы явно экспортируем, доступно для использования другими модулями.

7) Также должен быть включен строгий режим JavaScript, чтобы предотвратить случайное объявление глобальных переменных. При строгом режиме что-то вроде x = 1 приведет к ошибке без ключевых слов var, let или const перед ней.

```const strictFunction = ()=>{
  'use strict';
  const nestedFunction = ()=>{
    // эта функция тоже использует строгий режим
  }
}
```

8) Также let и const являются ключевыми словами для объявления локальных переменных и констант соответственно, поэтому мы не можем случайно ссылаться на них за пределами видимости блока, в котором они были объявлены.

Например, с var, если мы пишем следующий код:
```
if (true) {
  var x = 1;
}
console.log(x);
```
Выполнив этот пример, вызвав console.log, мы увидим результат 1. Это всё из-за того, что объявление переменной через var применяется к глобальной области видимости.

В другом же случае, если мы используем let вместо var:
```
if (true) {
  let x = 1;
}
console.log(x);
```
В результате мы получаем ошибку 'Uncaught ReferenceError: x is not defined'.
Как мы видим, мы не можем обращаться к переменным, которые доступны только в ограниченной области видимости (в данном случае, области видимости функции).

 Альтернативным способом решения этой проблемы - можно обернуть в вызов функции код, который мы хотим сделать приватным.

Например, мы можем написать:
```
(function() {
  var x = 1;
})();
console.log(x);
```
И тут мы также мы получим ошибку 'Uncaught ReferenceError: x is not defined'. Функция, которая запускается сразу же после объявления, как показано выше, называется IIFE (Immediately Invoked Function Expression) "Функция немедленного вызова".
Если мы хотим вернуть что-то из этой функции другому коду, который у нас есть выше, мы можем просто вернуть данные следующим образом:
```
let foo = (function() {
  var x = 1;
  return {
    bar: 2
  }
})();
console.log(foo.bar);
```
Мы вернули объект со свойством bar и присвоили его переменной foo. И, в результате, мы должны получить 2 из вывода console.log.

9) Следовать строгому стиль программирования.
Каждый разработчик в команде будет иметь свой индивидуальный стиль кодинга, которому пожелает следовать, при стилизации своего кода. Это означает, что код будет иметь разные стили в разных местах, где работали разные программисты, что усложняет чтение кода другими разработчиками. В связи с этим, неплохо было бы следовать какому-то общему формату стилей. Мы можем стилизовать наш код автоматически с помощью таких программ, как ESLint или JSLint, которые осуществляют статическую проверку нашего кода, чтобы убедиться, что он соответствует установленному стилю.
Есть также такие инструменты, как Prettier, для последовательного форматирования кода посредством стиля кода нашего приложения.

10) Комментарий при необходимости
В то время как большинство кода понятно, некоторый код нуждается в уточнении или объяснении. Например, если код является частью сложной системы, то может потребоваться некоторое уточнение в виде комментариев. Нужно правильно комментировать код, для объяснения сложных и неочевидных моментов разработчикам, которые будут работать с вашим кодом.
Простая функция, которая состоит из нескольких строк, наверное, не нуждается в больших пояснениях.
Если мы пишем комментарии, то следует использовать многострочные комментарии /* */ вместо однострочных //, так как они более универсальны.

Один из удобных приемов комментирования заключается в том, что перед закрытием многострочных комментариев нужно добавить двойной слеш следующим образом:
```
/*
  function foo(){
    return 1
  };  
// */
```
Таким образом, мы можем раскомментировать код, поставив слеш перед открывающим слешем в первой строке. И, чтобы раскомментировать код, достаточно:
```
//*
  function foo(){
    return 1
  };  
// */
```
Вышеуказанный код раскомментирован.

Многие текстовые редакторы также должны быть достаточно умны, чтобы автоматически распознавать и подсвечивать закомментированный и раскомментированный JavaScript-код.
