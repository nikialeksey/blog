---
layout: post
title: "Я знаю, почему ваши программы приносят вам проблемы"
lang: ru
image: /assets/imgs/skeletons.jpg
description: "История о наиболее частой причине всех проблем в программах"
tags: 
  - oop
  - data types
---

...

![Image by Paul Brennan from Pixabay]({{ site.url }}{{ page.image }})

<!--more-->

На сегодня мы имеем "замечательную" статистику по наиболее встречающимся 
исключениям в языках программирования.

### Java
![Top 10 Exception types by Frequency in 1000+ Applications]({{ site.url }}/assets/imgs/top-10-java-exceptions.png)
[Top 10 Exception types by Frequency in 1000+ Applications](https://blog.overops.com/the-top-10-exceptions-types-in-production-java-applications-based-on-1b-events/)
1. NullPointerException – 70% of Production Environments
2. NumberFormatException – 55% of Production Environments
3. IllegalArgumentException – 50% of Production Environments
4. RuntimeException – 23% of Production Environments
5. IllegalStateException – 22% of Production Environments
6. NoSuchMethodException – 16% of Production Environments
7. ClassCastException – 15% of Production Environments
8. Exception – 15% of Production Environments
9. ParseException – 13% of Production Environments
10. InvocationTargetException – 13% of Production Environments

### JS
[Top 10 JavaScript errors from 1000+ projects](https://rollbar.com/blog/top-10-javascript-errors/)
1. Uncaught TypeError: Cannot read property
2. TypeError: ‘undefined’ is not an object 
3. TypeError: null is not an object 
4. (unknown): Script error
5. TypeError: Object doesn’t support property
6. TypeError: ‘undefined’ is not a function
7. Uncaught RangeError
8. TypeError: Cannot read property ‘length’
9. Uncaught TypeError: Cannot set property
10. ReferenceError: event is not defined

### RubyOnRails
![Top 10 errors from 1000+ Ruby on Rails projects]({{ site.url }}/assets/imgs/top-10-ror-errors.png)
[https://rollbar.com/blog/top-10-ruby-on-rails-errors/](https://rollbar.com/blog/top-10-ruby-on-rails-errors/)
1. ActionController::RoutingError
2. NoMethodError: undefined method '[]' for nil:NilClass
3. ActionController::InvalidAuthenticityToken
4. Net::ReadTimeout
5. ActiveRecord::RecordNotUnique: PG::UniqueViolation
6. NoMethodError: undefined method 'id' for nil:NilClass
7. ActionController::ParameterMissing
8. ActionView::Template::Error: undefined local variable or method
9. ActionController::UnknownFormat
10. StandardError: An error has occurred, this and all later migrations canceled

Эта проблема реальна. Я не первый, кто ее заметил, поэтому уже придумано 
множество инструментов для борьбы с ней:

- https://en.wikipedia.org/wiki/Pyramid_of_doom_(programming)
- https://en.wikipedia.org/wiki/Safe_navigation_operator
- https://en.wikipedia.org/wiki/Null_coalescing_operator
- @NonNull, @Nullable + static analysers

## Интересно, были ли языки программирования без `null`?

Возмем свежий список популярных языков программирования из https://www.tiobe.com/tiobe-index/:

- Java (null)
- C (NULL)
- Python (None)
- C++ (NULL)
- ...

Все они имеют так или иначе языковую конструкцию, которая несет смысл 
"отсутствует какое либо значение" у переменной. JavaScript имеет даже несколько 
таких  конструкций `null`, `undefined`. Неужели нет ни одного популярного 
языка без `null`? Оказалось, что есть, и не один, только в другом времени.

До 1964 года ни в одном языке программрования не было `null`. И да, языки 
программирования до 1964 года были, вот их список:

- Algol 60
- Fortran

В 1960 году в компанию Elliot Brothers пришел программист Тони, 26 лет. Тони 
начал свою карьеру с обычной задачи: ему поручили разработать новый язык 
проограммирования. Как и мы с вами, Тони тоже был ~~ленивым~~ умным 
программистом, он не стал придумывать все с нуля, он взял за основу язык 
Algol 60 и решил его доработать. Чтобы вы могли окунуться в проблематику тех 
времен, я должен сказать, что большинство софта тогда было написано машинным 
кодом. А Тони делал язык высокого уровня. Этот язык должен был помогать 
человеку писать код. Например, ошибки должны были появляться в виде читаемых 
сообщений, а не шестнадцатиричным дампом памяти. Нужно было защитить программистов
от деталей реализации языка. Например, ему 
пришлось сделать рантайм проверку на индексы в массивах, это занимало и место
в программе компилятора и время при выполнении, но в языке высокого уровня 
это было нужно сделать, потому что отсутсвие такой проверки могло привести к
перезаписи кода программы во время выполнения (тогда ведь не было 
виртуальной памяти!). Далее, Тони ввел ООП в свой язык и начал придумывать, 
как работать с указателями и типами указателей. Ведь должны быть рантайм 
проверки типов. Указатель может ссылаться в никуда и тогда тоже должна быть 
проверка в языке программрования, которая выкинет ошибку при использовании 
указателя без данных. Нужно было вводить null типы, он предполагал иметь 
много различных null типов, по одному для каждого класса, было предложение 
заставить программистов писать для каждого класса описание пустого объекта, 
но в итоге Тони выяснил, что проще всего будет сделать один тип null, 
принадлежащий каждому классу.

После выхода в свет языка от Тони - Algol W - все другие языки переняли этот 
опыт с значением null и стали использовать у себя. Фактически, после
1964 года языков без null становилось все меньше и меньше. Сейчас вы их 
практически не найдете. Спустя 40 лет, Тони признался, что он тогда придумал 
ошибочную концепцию, которая плохо повлияла на весь мир программирования. 
Кстати, его друг, Эдсгер, уже тогда говорил Тони, что null - это плохая идея. 

Тони - это знаметитый Тони Хоар, придумавший быструю сортировку. Эдсгер - не 
менее знаменит, Эдсгер Дейкстра.  

https://www.infoq.com/presentations/Null-References-The-Billion-Dollar-Mistake-Tony-Hoare

## 

Проблемы, которые решал Тони в то время, недостаток опыта объектного 
программрования, смогли сузить сузить его взгляд. Ему так и не пришла 
мысль, что можно писать ООП код без использования null.  