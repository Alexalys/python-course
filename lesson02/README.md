# Модуль 2. Управляющие конструкции. Исключения

```python
name = input("What is your name? ")
print(f"Hello {name}")
```

По-умолчанию в Python инструкции выполняются одна за одной сверху вниз.
В примере две инструкции, сначала выполнится `name = input("What is your name? ")`, потом `print(f"Hello {name}")`.

Последовательность выполнения выражений в программе называется «поток выполнения» (Flow of execution).

Программы, в которых все команды выполняются одна за одной называются *линейными программами*, пример выше &mdash; это линейная программа,
инструкции выполнятся все и строго по очереди.

В Python существует три способа управления потоком выполнения:

* условное выполнение &mdash; выполнения блока инструкций только при наступлении некоторого условия;
* циклы &mdash; повторение выполнения блока инструкций пока выполняется некоторое условие;
* исключения &mdash; выполнение блока инструкций в случае ошибки.

## Условное выполнение

```python
age = input("How old are you? ")

if int(age) >= 18:
    print("You are adult already.")
else:
    print("You are infant yet.")
```

В Python реализован оператор контроля выполнения (условный оператор) `if ... elif ... else`.

С помощью этого инструмента существует возможность контролировать поток выполнения (по-умолчанию все инструкции выполняются сверху вниз).
Оператор контроля исполнения позволяет выполнять блоки инструкций не всегда, а только тогда, когда будет выполнено условие.

Синтаксис условного оператора состоит из обязательного ключевого слова `if` и необязательных `elif`, `else`.

Условный оператор начинается с ключевого слова `if` за которым следует условие.

После условия ставится двоеточие и с новой строки с отступом идет блок инструкций, которые будут выполнены в
случае, когда условие выполняется.

После блока `if` может быть ноль или более блоков `elif`, интерпретатор последовательно будет проверять
все условия `elif` сверху вниз, пока не найдет то, которое выполняется, или они закончатся.

После блока(ов) `elif` может содержаться один блок `else`, который выполнится, если все предыдущие условия не выполняются.

```python
a = input('Введите число')
a = int(a)
if a > 0:
    print('Число положительное')
elif a < 0:
    print("Число отрицательное")
else:
    print('Это число - ноль')
```

Во время выполнения условного оператора интерпретатор Python проверяет условия сверху вниз пока не найдет то,
которое выполняется, затем выполнит выражение для этого условия и выйдет из проверки условий.

```python
a = input('Введите число')
a = int(a)
if a > 0:
    print('Число положительное')
elif a == 1:
    print('Число равно 1')
else:
    print("a <= 0")
```

В таком случае код для условия `a == 1` никогда не исполнится.

## Приведение типов

Python &mdash; это язык с динамической строгой типизацией. Это означает, что одна и та же переменная
может менять свой тип по мере выполнения новых инструкций, но автоматически интерпретатор не будет менять
тип данных.

```python
age = input("How old are you? ")
```

Функция `input` возвращает `str`, строку и сравнить значение `age` с числом `18`, нельзя, непонятно как должно происходить такое сравнение.

Но можно преобразовать тип переменной `age` в `int` при помощи встроенной функции `int` (функция называется точно также, как и тип):

```python
age = input("How old are you? ")
age = int(age)
```

Для преобразование строк в числа с дробной частью можно использовать функцию `float`:

```python
pi = float('3.14')
```

Также можно преобразовать практически любой Python объект в строку функцией `str`:

```python
pi_str = str(3.14)
age_str = str(29)
```

## Условия в Python

Условный оператор `if ... elif ... else` в Python в качестве условий может принимать переменные типа `bool`
или любое выражение, которое он выполнит и результат преобразует в `bool`.

Тип `bool` &mdash; подтип целых чисел, который может принимать только два значения: `True` и `False`.

### Создание переменных типа `bool`

Есть 3 способа создать переменную с типом `bool`:

* Присвоить переменной значение `True` или `False`

    ```python
    a = True
    b = False
    ```

* Присвоить переменной результат выполнения логического выражения:

  ```python
  age = 18
  adult1 = age >= 18    # True

  age = 15
  adult2 = age >= 18    # False
  ```

* Использовать функцию `bool` для приведения к типу `bool`
  
  ```python
  user_name = ""
  user_name_is_set = bool(user_name)
  ```

### Логические выражения

Когда в качестве условия в условный оператор мы передаем выражение, то выражение выполнится, а результат его выполнения будет преобразован в тип `bool`.

Для удобства в Python есть механизм неявного приведения любого типа к типу `bool`.
Правила приведения к `bool` &mdash; интуитивны:

* число `0` приводится к `False` (целое, дробное или комплексное);
  
    ```python
    money = 0
    if money:
        print(f"You have {money} on your bank account")
    ```

* `None` приводится к `False`;

    ```python
    result = None
    if result:
        print(result)
    else:
        print("Result is None, do something")
    ```

* пустой контейнер (пустой список, пустой словарь, пустая строка и т.п.) приводятся к `False`

    ```python
    user_name = input("Enter your name: ")

    if user_name:
        print(f"Hello {user_name}")
    else:
        print("Hi Anonym!")
    ```

* всё остальное приводится к `True`

Правила приведения к `bool` позволяют писать условные выражения в Python практически на литературном английском.
В любом случае, такой код становится очень понятным.

### Выражения сравнения

Для сравнения в Python есть операторы `<` (меньше), `<=` (меньше или равно), `>` (Больше), `>=` (больше или равно), `==` (равно), `!=` (Не равно).

```python
a = 3
b = 5
c = a < b   # True
d = a > b   # False
a == b      # False
a != v      # True
```

Определим является ли число, которое ввел пользователь, положительным (больше нуля).

```python
a = input('Введите число')
if int(a) > 0:
    print("Число положительное")
```

Также можно использовать интервальные сравнения в Python:

```python
t = input("Введите температуру воды")
t = int(t)
if t <= 0:
    print("Это - лед")
elif 0 < t < 100:
    print("Это - вода")
else:
    print("Это - пар")
```

### Булева алгебра

Но что делать, когда у нас сложное условие, которое сочетает в себе несколько вложенных условий? Например, чтобы пользователь мог
арендовать автомобиль надо чтобы у пользователя обязательно было указанно имя, пользователь был старше 18 и имелись водительские права.

```python
name = "Taras"
age = 22
has_driver_licence = True

if name and age >= 18 and has_driver_licence:
    print(f"User {name} can rent a car")
```

Для построения логических условий из нескольких используется булева алгебра.

__Булева алгебра &mdash; это раздел математической логики, в котором изучаются логические операции над высказываниями.__

В программировании применяют бинарную логику, возможные значения для бинарной логики могут быть `True` и `False`.

Булева алгебра строится на трёх основных операциях: "И", "ИЛИ", "НЕ". Есть ещё вспомогательные, но давайте пока рассмотрим основные.

В Python операторы булевой алгебры &mdash; это операторы `not`, `and`, `or`.

### and (И) выражение выполняется, если оба условия выполняются

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">A</th>
    <th class="tg-c3ow">B</th>
    <th class="tg-c3ow">A and B</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">True</td>
    <td class="tg-c3ow">True</td>
    <td class="tg-c3ow">True</td>
  </tr>
  <tr>
    <td class="tg-c3ow">True</td>
    <td class="tg-c3ow">False</td>
    <td class="tg-c3ow">False</td>
  </tr>
  <tr>
    <td class="tg-c3ow">False</td>
    <td class="tg-c3ow">True</td>
    <td class="tg-c3ow">False</td>
  </tr>
  <tr>
    <td class="tg-c3ow">False</td>
    <td class="tg-c3ow">False</td>
    <td class="tg-c3ow">False</td>
  </tr>
</tbody>
</table>

```python
a = True and False  # False
```

### or (ИЛИ) выражение выполняется, если хоть одно из условий выполняется

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">A</th>
    <th class="tg-c3ow">B</th>
    <th class="tg-c3ow">A or B</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">True</td>
    <td class="tg-c3ow">True</td>
    <td class="tg-c3ow">True</td>
  </tr>
  <tr>
    <td class="tg-c3ow">True</td>
    <td class="tg-c3ow">False</td>
    <td class="tg-c3ow">True</td>
  </tr>
  <tr>
    <td class="tg-c3ow">False</td>
    <td class="tg-c3ow">True</td>
    <td class="tg-c3ow">True</td>
  </tr>
  <tr>
    <td class="tg-c3ow">False</td>
    <td class="tg-c3ow">False</td>
    <td class="tg-c3ow">False</td>
  </tr>
</tbody>
</table>

```python
a = True or False  # True
```

#### not (НЕ) отрицание, выражение выполняется, если операнд - ложь

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">A</th>
    <th class="tg-c3ow">not A</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">True</td>
    <td class="tg-c3ow">False</td>
  </tr>
  <tr>
    <td class="tg-c3ow">False</td>
    <td class="tg-c3ow">True</td>
  </tr>
</tbody>
</table>

```python
a = not 2 < 0  # True
```

## Блоки инструкций

```python
x = input("X: ")
y = input("Y: ")

if x == 0:
    print("X can`t be equal to zero")
    x = input("X: ")

result = y / x
```

У Python особый синтаксис касательно выделения блоков инструкций. Чтобы интерпретатор воспринял набор инструкций как отдельный
блок достаточно выделить все инструкции этого блока одинаковым количеством отступов слева.
В Python рекомендуется для выделения одного уровня вложенности для блока инструкций использовать **4 пробела**.

Вы можете использовать символы табуляции для выделения блока инструкций, это не ошибка, но такой способ не рекомендуется.

Синтаксической **ошибкой** будет смешать в одном файле выделение блоков  при помощи **табуляций и пробелов одновременно**.

Вы также можете выделять несколько уровней вложенности добавляя ещё 4 пробела слева для всех инструкций блока:

```python
x = input("X: ")
y = input("Y: ")

if x == 0:
    print("X can`t be equal to zero")
    x = input("X: ")
    if x == 0:
        print("X can`t be equal to zero")
        x = input("X: ")
        if x == 0:
            print("X can`t be equal to zero")
            x = input("X: ")

result = y / x
```

В этом примере трижды повторяется проверка на неравенство `x` нулю и на каждую проверку блок инструкций выделяется дополнительными 4-мя пробелами.

Пример вложенности для определения четвертей для координатной плоскости.

```python
if x > 0:
    if y > 0:               # x>0, y>0
        print("Первая четверть")
    else:                   # x>0, y<0
        print("Четвертая четверть")
else:
    if y > 0:               # x<0, y>0
        print("Вторая четверть")
    else:                   # x<0, y<0
        print("Третья четверть")
```

## Циклы

Для того, чтобы повторить какой-то блок кода несколько раз или повторять пока выполняется некоторое условие в Python,
реализованны циклы. Есть два вида циклов:

* цикл `for`, который ещё называют итерирующим, он перебирает все элементы некоторой последовательности;
* цикл `while`, который выполняется пока выполняется некоторое условие.

__Итерация (лат. iteratio «повторение») &mdash; повторение какого-либо действия.__
Итерация в программировании &mdash; организация обработки данных, при которой действия повторяются многократно, не приводя при этом к вызовам самих себя.

Одна итерация &mdash; это одно повторение.

### Цикл for

В Python, цикл `for` используется для перебора всех элементов контейнеров, или итерируемых объектов, например, списков.
Инструкции, которые находятся в теле цикла будут выполнены столько раз, сколько элементов в списке.

При этом, на каждой итерации специальная переменная получает значение одного из элементов списка.

Работу цикла `for` можно сравнить с тем, что вы по очереди возьмете каждую букву из фразы и проговорите её.
Фразой будет выступать строка `'apple'`, а аналогом произнесения вслух будет выступать вывод соответствующей буквы в консоль.

```python
fruit = 'apple'
for char in fruit:
    print(char)
```

Синтаксис цикла `for`:

1. цикл начинается с ключевого слова `for`;
2. за которым обязательно идёт название переменной куда будет записываться значение получаемое из итерируемого объекта на каждой итерации;
3. далее следует ключевое слово `in`;
4. за которым обязательно идёт выражение или объект по которому собственно будет итерироваться `for`;
5. далее ставится `:`;
6. и с новой строки с отступом идёт набор выражений, которые будут повторятся на каждой итерации

### Цикл while

Цикл `while` позволяет выполнять инструкции, которые находятся в теле цикла до тех пор, пока выполняется условие, указанное в цикле.
Например, цикл `while`, который выводит числа от 1 до 5:

```python
a = 1
while a <= 5:
    print(a)
    a = a + 1
```

### «Бесконечные циклы» и `break`

Бывают ситуации, когда необходимо выйти из цикла до завершения итерации, не дожидаясь пока произойдет очередная проверка условия.
Для этого есть команда `break`. Команда `break` останавливает цикл в момент вызова и не завершает итерацию.

```python
a = 0
while True:
    print(a)
    if a == 20:
        break
    a = a + 1
```

В этом примере условие цикла будет выполнятся всегда, ведь `True` всегда будет `True`. Это пример бесконечного цикла. Но из-за проверки что `a == 20` этот цикл завершится как только в `a` будет значение `20`.

Бесконечные циклы часто применяются там где надо взаимодействовать с клиентом ожидая ввода от него и завершаться только при наступлении некоторого условия.

Например echo скрипт, который выводит в консоль то, что вы введете, пока вы не введете `exit`:

```python
while True:
    user_input = input()
    print(user_input)
    if user_input == "exit":
        break
```

### Завершение итерации с помощью continue

Также для того, чтобы сразу перейти к следующей итерации цикла без выполнения оставшихся выражений есть команда `continue`.
Вызов этой команды в теле цикла приводит к тому, что оставшиеся выражения этой итерации не будут выполнены,
а интерпретатор сразу перейдет к следующей итерации или проверке условия.

```python
a = 0
while a < 20:
    a = a + 1
    if a % 2 == 0:
        continue
    print(a)
```

Операторы `continue` и `break` работают только внутри одного цикла. В ситуации вложенных циклов нет способа выйти из всех циклов сразу.
Также использование `continue` или `break` вне цикла приводит к синтаксической ошибке.

В этом примере использовался оператор получения остатка от деления `%`, он возвращает такое число `p`,
что если его отнять от `r`, то выполнится условие `r / x == 0`.

## Исключения

Преобразовать в `int` или `float` можно не любую строку. Например, если пользователь введет `'a'`, то интерпретатор не сможет определить как преобразовать символ `a` в целое число и вызовет исключение `ValueError`.

```python
int("a")
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-6-d9136db7b558> in <module>
----> 1 int("a")

ValueError: invalid literal for int() with base 10: 'a'
```

Исключение в Python &mdash; это ошибка на уровне интерпретатора, вызванная невозможностью выполнить тот или иной оператор
по каким-либо причинам (переменная не существует, синтаксическая ошибка, отсутствует атрибут, операция деления на ноль и т.п.).

В данном случае программа прекратит свою работу и пользователь так и не узнает, что привело к этому сбою.

В нашем примере (ввели `'а'`) интерпретатор пытается преобразовать строку в тип `int` (целое число), но как переводится строка `'a'` в число &mdash; не определено и будет вызвано исключение по этому поводу.

### Механизм обработки исключений

Для обработки исключений существует оператор `try ... except ...`. Синтаксически, этот оператор начинается с ключевого слова `try:` (попробовать) и продолжается блоком кода на следующей строке, который выделен отступом.

Далее идет блок обработки исключений `except` (кроме), где можно указать одно, или более исключений, после которых выполнить следующий блок кода.
Этот блок не обязателен, но чаще всего нужен. Он выполнится если случится указанное исключение (одно из них, если их несколько).

Потом идёт необязательный блок кода, который начинается с ключевого слова `finally`, он выполнится в любом случае.

Последним идёт необязательный блок, который начинается с ключевого слова `else`. Этот код выполнится только если исключений не случилось.

В нашем примере обработка пользовательского ввода будет выглядеть следующим образом:

```python
val = 'a'
try:
    val = int(val)
except ValueError:
    print(f"val {val} is not a number")
else:
    print("Its ok")
finally:
    print("This will be printed anyway")
```

Исключения в Python &mdash; это очень мощный инструмент, который часто используется для управления потоком выполнения, а не
только для обработки ошибок. В динамических языках никогда нельзя быть на 100% уверенным в том, что пользователь
ввёл значение корректного типа или что другое приложение не вернуло `None` вместо `int`, например.

Наивным решением этой проблемы будет повсеместное использование проверок `if` на корректность введенного пользователем
или другим приложением значения. Более продвинутым, удобным и прозрачным решением является использование механизма
обработки исключений там, где они могут случиться из-за некорректных входных данных.  

```python
age = input("How old are you? ")
try:
    age = int(age)
    if age >= 18:
        print("You are adult.")
    else:
        print("You are infant")
except ValueError:
    print(f"{age} is not a number")
```

### Основные типы исключений в Python

`SyntaxError` синтаксическая ошибка.

`IndentationError` ошибка которая возникает если в выделении блоков инструкций пробелами допущена ошибка.

`TabError` возникает если в одном файле использовать пробелы и табуляции для выделения блоков инструкций.

`TypeError` возникает когда операция с переменной этого типа невозможна.

```python
2 / 'a'
```

`ValueError` возникает когда тип операнда подходящий, но значение таково, что операцию невозможно выполнить.

```python
int("a")
```

`ZeroDivisionError` деление на ноль.

## Домашнее задание

Напишите программу, которая будет выполнять простейшие математические операции с числами последовательно принимая
от пользователя операнды (числа) и оператор.

### Условия приёмки

* Приложение работает с целыми и дробными числами.
* Приложение умеет выполнять такие математические операции:
  * СЛОЖЕНИЕ (+)
  * ВЫЧИТАНИЕ (-)
  * УМНОЖЕНИЕ (*)
  * ДЕЛЕНИЕ (/)
* Приложение принимает один операнд или один оператор за один цикл запрос-ответ.
* Все операции приложение выполняет по мере поступления одну за одной.
* Приложение выводит результат вычислений когда получает от пользователя `=`.
* Приложение заканчивает свою работу после того, как выведет результат вычисления.
* Пользователь по очереди вводит числа и операторы.
* Если пользователь вводит оператор два раза подряд, то он получает сообщение об ошибке и может ввести повторно.
* Если пользователь вводит число два раза подряд, то он получает сообщение об ошибке и может ввести повторно.
* Приложение корректно обрабатывает ситуацию некорректного ввода.
