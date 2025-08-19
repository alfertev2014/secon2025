---
# You can also start simply with 'default'
theme: default
# some information about your slides (markdown enabled)
title: Ныряем в теорию типов для лучшего понимания TypeScript
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
---

# Ныряем в теорию типов

для лучшего понимания TypeScript

---
level: 2
hideInToc: true
---

# Приятно познакомиться

- Василий Алфертьев
- Frontend разработчик (React + TypeScript)
- Компания: Открытые решения
- Telegram: @alfertev2012
- GitHub: alfertev2014

<!--
Сперва, кто я такой. Я Василий Алфертьев, в настоящее время работаю frontend-разработчиком в компании Открытые решения, пишу на React-е, активно использую TypeScript в работе. Ничего особенного, делаю интерфейсы различных одностраничных приложений.
-->

---
layout: two-cols-header
level: 2
hideInToc: true
---

# Чем ещё владею

::left::

- 5+ лет в **С++**:
  - системное программирование в Linux
  - UI на Qt
- ~6 лет в **Java**:
  - backend на Spring
  - базы данных
  - монолиты, микросервисы…

::right::

- Увлекаюсь
  - дизайном языков программирования
  - best practices и архитектурой ПО
  - математической логикой
- **Фанат систем типов**
- Тянет разбираться в
  - компиляторах и оптимизациях
  - "кишках" runtime разных языков
  - IDE и инструментах
  - LISP, Prolog, OCaml, Haskell, Scala…

<!--
Когда-то занимался системным программированием на C++, писал UI на Qt, прошёл через backend-разработку на Java. Параллельно увлекался изучением вопросов дизайна языков программирования, математическими основами, которые за ними стоят... Фанат систем типов. Люблю поинтересоваться, как устроены компиляторы, IDE и другие инструменты.

И вот с этим опытом я пришёл во frontend-разработку, возлагая на TypeScript определённые надежды. Какое-то время я просто наблюдал за его развитием, а потом решил, что всё, пора.
-->
---
layout: section
---

# Коротко про TypeScript

И его систему типов

<!--
Вспомним быстро, что из себя представляет TypeScript
-->
---
layout: default
dragPos:
  ts_logo: 640,113,220,_
  microsoft: 648,383,209,_
---

# Коротко про TypeScript

- Язык программирования
- Синтаксис основан на JavaScript
- Транспиляция в JavaScript
- Проверка типов
- Поддержка IDE (language server)

<img v-drag="'ts_logo'" src="./images/ts_logo.png" />
<img v-drag="'microsoft'" src="./images/microsoft.png" />

<!--
Итак, TypeScript - это язык программирования с синтаксисом, основанным на JavaScript, он транспилируется в JavaScript с минимальными изменениями кода (в идеале - происходит просто "стирание" типов). Основной фишкой его фишкой выступает тайпчекер, выполняющий вывод и проверку типов, а также, с ним идёт language-server для поддержки языка в IDE, автокомпилита и различных рефакторингов.
-->
---
layout: image-right
image: /images/smiling_cat.png
---

# TypeScript хвалят за

- Предотвращение runtime-ошибок (TypeError)
- Продуктивность разработки (поддержка в IDE)
- Документируемость кода и API
- Прививание хорошего стиля кода
- Избавление от лишних проверок в runtime

<!--
Собственно, мы любим его за то, что он помогает нам отлавливать ошибки типизации и повышает продуктивность при написании и редактировании кода. Код получается более самодокументированным, и сам компилятор нас вынуждает писать такой код в более строгом и ясном стиле, который получается ещё и эффективным, потому что в нём не приходится вставлять runtime-проверок.
-->
---
layout: image-right
image: /images/angry_cat.png
---

# TypeScript ругают за

- Ненадёжная система типов
- Слабо типизированная стандартная библиотека JavaScript
- Неактуальные “.d.ts”-файлы для библиотек из NPM
- Высокий порог входа (“трёх-этажные типы”)
- Борьба с ошибками компиляции

<!--
И в то же время всем должно быть уже известно, что его система типов не надёжна, а взаимодействие с JavaScript вызывает ещё больше проблем. 

И надо сказать, что TypeScript не самый простой язык. Даже некоторые простые повседневные с точки зрения JavaScript приёмы программирования могут потребовать написания сложных трёх-этажных типов. И если в них запутаться, это всё может вылиться в непродуктивную борьбу с компилятором по устранению ошибок, при которой так и хочется влепить any или принудительно привести тип через as.
-->

---
layout: image-right
image: /images/tapl.png
---

# Теория

- Теория множеств
- Теория доказательств
- Теория формальных языков и грамматик
- Лямбда-исчисление
- Операционная семантика

---
layout: default
---

# План доклада

1. Семантика языков программирования
1. Система типов и семантика языка
1. Полиморфизм и системы типов
1. Строгость и “уровень” языков программирования
1. Соображения про методологии разработки

---
layout: section
---

# Семантика языков программирования

Формальные системы, спецификация и реализации языка

---
layout: default
---

# Формальная система

- Совокупность **абстрактных объектов**
- **Правила** оперирования множеством символов
- В строго синтаксической трактовке без учёта смыслового содержания

Состоит из

- **Язык** выражений
- Множество **формул**
- **Правила** преобразования формул

---
layout: default
---

# Язык

- **Алфавит** - конечное или счётное множество символов
- **Синтаксис** - правила построения *выражений*
- **Семантика** - правила определения *смысла* выражений

---
layout: default
---

# Пример: арифметические выражения

Синтаксические правила

```
Цифра ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
Число ::= Цифра Цифра*
Выражение ::=
  | Число
  | -Число
  | +Число
  | Выражение + Выражение
  | Выражение - Выражение
  | Выражение * Выражение
  | Выражение / Выражение
  | ( Выражение )
```

---
layout: default
---

# Пример: арифметические выражения

Семантика

```ts
2             // --> 2
4             // --> 4
2 + 2         // --> 4
2 + 2 * 2     // --> 6
(2 + 2) * 2   // --> 8
```

---
layout: default
---

# Пример: арифметические выражения

Операционная семантика

````md magic-move
```ts
(2 + 2 * 2) * ((2 + 2) * 2)
```
```ts
(2 + 4) * ((2 + 2) * 2)
```
```ts
6 * ((2 + 2) * 2)
```
```ts
6 * (4 * 2)
```
```ts
6 * 8
```
```ts
40
```
````

---
layout: default
---

# Пример: Базовые типы JavaScript

````md magic-move
```ts
2 + "2"     // --> ?
true + null // --> ?
```
```ts
2 + "2"     // --> ?
true + null // --> ?
[] + {}     // --> ?
```
```ts
2 + "2"     // --> "22"
true + null // --> 1
[] + {}     // --> "[object Object]"
```
````

---
layout: default
---

# Абстракция

````md magic-move
```ts
function f() {
  return (1 + 2 + 3) * (1 + 2 + 3) + ((1 + 2 + 3) * (1 + 2 + 3)) * ((1 + 2 + 3) * (1 + 2 + 3))
}
```
```ts
function f() {
  const a = 1 + 2 + 3
  return a * a + (a * a) * (a * a)
}
```
```ts
function f() {
  const a = 1 + 2 + 3
  const b = a * a
  return b + b * b
}
```
```ts

function f() {
  const a = 1 + 2 + 3
  const square = (x: number) => x * x
  const b = square(a)
  return b + square(b)
}
```
```ts
const square = (x: number) => x * x

function f() {
  const a = 1 + 2 + 3
  const b = square(a)
  return b + square(b)
}
```
```ts
const square = (x: number) => x * x

function f(a: number) {
  const b = square(a)
  return b + square(b)
}

f(1 + 2 + 3)
```
````

---
layout: image
image: /images/ecmascript_spec.png
backgroundSize: contain
title: ECMAScript
---

---
layout: default
---

# Общие черты языков программирования

- Базовые типы данных и операции над ними
- Составные типы данных (объекты и массивы)
- Древовидные выражения
- Переменные с лексической областью видимости
- Функции и процедуры
- Замыкания
- Модули

---
layout: default
---

# Лямбда-исчисление

- Теоретический каркас языков программирования
- Два правила:
  - правило области видимости символов ("альфа-конверсия")
  - правило подстановки значений вместо символов ("бета-редукция")

---
layout: default
---

# Редукция

````md magic-move
```ts {8}
const square = (x: number) => x * x

function f(a: number) {
  const b = square(a)
  return b + square(b)
}

f(1 + 2 + 3)
```
```ts {8}
const square = (x: number) => x * x

function f(a: number) {
  const b = square(a)
  return b + square(b)
}

f(6)
```
```ts {3-6}
const square = (x: number) => x * x

((a: number) => {
  const b = square(a)
  return b + square(b)
})(6)
```
```ts {3,4}
const square = (x: number) => x * x

const b = square(6)
b + square(b)
```
```ts
const b = ((x: number) => x * x)(6)
b + ((x: number) => x * x)(b)
```
```ts
const b = 6 * 6
b + b * b
```
```ts
const b = 36
b + b * b
```
```ts
36 + 36 * 36
```
```ts
36 + 1296
```
```ts
1332
```
````

---
layout: default
---

# Ошибки типизации

```ts twoslash
const a = 2 + "2"

const b = [] + {}
```

---
layout: default
---

# Реализация и инструменты

<img src="./images/implementation.svg" />

---
layout: default
---

# TypeScript и Node.js

<img src="./images/implementation_ts.svg" />

<br />

- или использовать `tsx` (или аналоги)
- или запускать `*.ts` нативно на `Node.js`

---
layout: default
---

# Ошибки

- Синтаксические ошибки
- Ошибки времени исполнения
  - Ошибки среды исполнения
  - Необработанные исключения
  - stack overflow, out of memory, зацикливания
  - Логические ошибки

---
layout: default
---

# TypeError

<br />

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypeError]

A `TypeError` may be thrown when:

- an operand or argument passed to a function is incompatible with the type expected by that operator or function; or
- when attempting to modify a value that cannot be changed; or
- when attempting to use a value in an inappropriate way.

---
layout: default
---

# Статический анализ

- Рассуждения об исполнении программы без её реального запуска
- Доказательство свойств программ
  - Обнаружение потенциальных ошибок или **доказательство** их отсутствия

---
layout: default
---

# Формальная верификация

<img src="./images/verification.svg" />

---
layout: section
---

# Системы типов и семантика

Что такое типы, свойства систем типов

---
layout: default
---

# Система типов

- Система доказательства подмножества (ослабленных) утверждений
- Исходит из семантики языка
- Является "упрощённой версией" (проекцией) семантики

Система типов предназначена для доказательства *отсутствия* определённого рода ошибок при исполнении программы - **ошибок типизации**.

---
layout: statement
---

# Типы - это не только типы данных!

---
layout: default
---

# Типы как раскладка данных в памяти

```c
struct S {
  int a;
  bool b;
  const char* c;
  unsigned char d[4];
  // ...
};
```

---
layout: statement
---

# Типы - это утверждения о выражениях

---
layout: default
---

# Правила типизации

- Правила "приписывания" типов выражениям
- Задаются для синтаксических конструкций языка
- Не должны противоречить семантике
- Определены только для корректно типизированных выражений
- Используются в алгоритмах проверки и вывода типов

---
layout: default
---

# Примеры: литеральные выражения

````md magic-move
```ts
42            // number
100500.5      // number
"The Answer"  // string
true          // boolean
false         // boolean
```
```ts
let a1 = 42            // number
let a2 = 100500.5      // number
let a3 = "The Answer"  // string
let a4 = true          // boolean
let a5 = false         // boolean
```
```ts
const a1 = 42            // 42
const a2 = 100500.5      // 100500.5
const a3 = "The Answer"  // "The Answer"
const a4 = true          // true
const a5 = false         // false
```

```ts
const a1 = 42            // 42
const a2 = 100500.5      // 100500.5
const a3 = "The Answer"  // "The Answer"
const a4 = true          // true
const a5 = false         // false

const a6 = null          // null
const a7 = undefined     // undefined
```
````

---
layout: statement
---

# Тип - это множество допустимых значений

---
layout: default
---

# Примеры: составные выражения

````md magic-move
```ts
let a1 = []            // never[]
let a2 = {}            // {}
let a3 = () => {}      // () => void
```
```ts
let a1 = [42, 100500.5]                  // number[]
let a2 = { a: "The Answer", b: false }   // { a: string, b: boolean }
let a3 = (arg: string): number => {
  return arg.length
}                                        // (arg: string) => number
```
```ts
const a1 = [42, 100500.5] as const                  // readonly [42, 100500.5]
const a2 = { a: "The Answer", b: false } as const   // { readonly a: string, readonly b: boolean }
const a3 = (arg: string): number => {
  return arg.length
}                                                   // (arg: string) => number
```
````

---
layout: default
---

# Аннотации типов

````md magic-move
```ts
const f: (arg: string) => number   =  (arg: string): number => {
  const arr: string[] = arg.split(' ');
  return arr.length
}
```
```ts {2}
const f: (arg: string) => number   =  (arg: string): number => {
  const arr: string[] = (arg as string).split(' ');
  return arr.length
}
```
```ts {2}
const f: (arg: string) => number   =  (arg: string): number => {
  const arr: string[] = (arg.split as (sep: string) => string[])(' ');
  return arr.length
}
```
```ts {3}
const f: (arg: string) => number   =  (arg: string): number => {
  const arr: string[] = arg.split(' ');
  return arr.length as number
}
```
```ts {2,3}
const f: (arg: string) => number   =  (arg: string): number => {
  const arr: string[] = (arg.split satisfies (sep: string) => string[])(" ");
  return arr.length satisfies number
}
```
````

---
layout: default
---

# Проверка типов

- Проверка выражений на соответствие правилам типизации
- Проверка совместимости типов при
  - инициализации переменных
  - присваиваниях
  - передаче аргументов в функцию

---
layout: default
---

# Проверка типов

```ts twoslash
const a: string = 42;        // Инициализация

let b: boolean = false
b = null                     // Присваивание

const c: { prop: string } = { prop: 42}   // Ожидаемый тип объекта

c.prop = false             // Присваивание property

const f = (arg: string) => { }
f(42)                   // Передача аргумента в функкцию
```

---
layout: default
---

# Вывод типов

- Реконструкция отсутствующих аннотаций типов
- Выполняется на основе правил типизации
- Исходные данные:
  - Типы литеральные выражений и встроенных операций
  - Явные аннотации типов


---
layout: section
---

# Свойства систем типов

---
layout: default
---

# Свойства систем типов

- **Надёжность** (soundness)
- **Полнота** (completeness)
- **Разрешимость** (resolvability)

---
layout: default
---

# Надёжность системы типов

Система типов **надёжна** (*sound*), если выведенные типы **_гарантированно_** соответствуют семантике (поведению в runtime).

*Вычисление корректно типизированного выражения либо зациклится, либо гарантированно даст в результате значение, удовлетворяющее выведенному типу.*

---
layout: default
---

# Множества программ, считающихся корректными

<img src="./images/soundness.svg" />

---
layout: statement
---

# Надёжность - это если программа корректно типизирована, то она корректна с точки зрения семантики

---
layout: default
---

# Надёжность системы типов TypeScript

[https://github.com/Microsoft/TypeScript/wiki/TypeScript-Design-Goals]

- **Non-goals**:
  - Apply a **sound** or "**provably correct**" type system. Instead, strike a balance between correctness and productivity.

---
layout: image-right
---

# И как с этим жить?

<v-clicks>

- Мы **_хотим_**, чтобы типы в коде были верными
- Просто *ответственность за это ложится на разработчика*
- Type checker - просто инструмент
- Для обеспечения гарантий нужны *best practices* и *соглашения*

</v-clicks>

---
dragPos:
  first_time: -58,0,0,0
  cpp: -58,0,0,0
---

<img v-drag="'first_time'" src="./images/first_time.png" />
<div v-drag="'cpp'" style="background-color: white;text-alignment: center">
<b>C++</b>
</div>

---
layout: default
---

# Полнота системы типов

Система типов может считать ошибочными программы, которые с точки зрения семантики считаются валидными.

Чем "гибче" система типов, тем больше валидных программ могут быть типизированы.

Полнота - это покрытие системой типов множества валидных программ.

---
layout: statement
---

# Если программа корректна с точки зрения семантики, то она должна быть корректно типизирована

---
layout: default
---

# "Гибкость" системы типов

<img src="./images/completeness.svg" />

---
layout: default
---

# Надёжная и полная система типов

<img src="./images/sound_complete.svg" />

---
layout: default
---

# Надёжность и полнота TypeScript

<img src="./images/completeness_ts.svg" />

---
layout: default
---

# Разрешимость системы типов

Система типов **разрешимая**, если задачи проверки и вывода типов *алгоритмически разрешимы*.

С неразрешимой системой типов:

- проверка типов может зациклиться
- можно "программировать на типах"

---
layout: default
---

# Разрешимость системы типов

<img src="./images/resolvability.svg" />

---
layout: default
---

# Разрешимость системы типов TypeScript

<img src="./images/resolvability_ts.svg" />
