# Lecture 4
Тесты появятся позднее
## Выражения

### Дедлайн 04/04/21 00:01 - 30 баллов

Задание выполняется на Java.

1) Разработайте классы
   `Const`, `Variable`, `Add`, `Subtract`, `Multiply`, `Divide`
   для вычисления выражений с одной переменной в типе `int`. Классы нужно помесить в
   пакет `ru.ifmo.backend_2021.expressions`.
2) Классы должны позволять составлять выражения вида
    ```java
    new Subtract(
        new Multiply(
          new Const(2),
          new Variable("x")
        ),
        new Const(3)
    ).evaluate(5)
    ```
   При вычислении такого выражения вместо каждой переменной подставляется значение, переданное в качестве параметра
   методу `evaluate` (на данном этапе имена переменных игнорируются). Таким образом, результатом вычисления приведенного
   примера должно стать число 7.
3) Метод `toString` должен выдавать запись выражения в полноскобочной форме. Например
    ```java
    new Subtract(
        new Multiply(
          new Const(2),
          new Variable("x")
        ),
        new Const(3)
    ).toString()
    ```
   должен выдавать `((2 * x) - 3)`.
4) Метод `toMiniString` должен выдавать выражение с минимальным числом скобок. Например
    ```java
    new Subtract(
      new Multiply(
        new Const(2),
        new Variable("x")
      ),
      new Const(3)
    ).toMiniString()
    ```
   должен выдавать `2 * x - 3`.
5) Переопределите метод `equals`, проверяющий, что два выражения совпадают. Так же надо переопределить `hashCode`. Например,
    ```java
    new Multiply(new Const(2), new Variable("x"))
      .equals(new Multiply(new Const(2), new Variable("x")))
    ```
   должно выдавать `true`, а
    ```java
    new Multiply(new Const(2), new Variable("x"))
        .equals(new Multiply(new Variable("x"), new Const(2)))
    ```
   должно выдавать `false`.
6) При выполнении задания следует обратить внимание на:
    * Выделение общего интерфейса создаваемых классов.
    * Выделение абстрактного базового класса для бинарных операций.
7) Реализуйте парсер выражений из строки в ранее описанную структуру `ru.ifmo.backend_2021.ExpressionParser`.
    1) В записи выражения могут встречаться: умножение `*`, деление `/`, сложение `+`, вычитание `-`, унарный минус `-` (класс для него называется на ваше усмотрение),
       целочисленные константы (в десятичной системе счисления, которые помещаются в 32-битный знаковый целочисленный
       тип), круглые скобки, переменные, состоящие из любого количества букв (`testMe`), и произвольное число пробельных
       символов в любом месте (но не внутри констант).
    2) Приоритет операторов, начиная с самого высокого
        1) унарный минус;
        2) умножение и деление;
        3) сложение и вычитание.
    3) Разбор выражений рекомендуется производить
       методом [рекурсивного спуска](https://ru.wikibooks.org/wiki/%D0%A0%D0%B5%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D0%B8_%D0%B0%D0%BB%D0%B3%D0%BE%D1%80%D0%B8%D1%82%D0%BC%D0%BE%D0%B2/%D0%9C%D0%B5%D1%82%D0%BE%D0%B4_%D1%80%D0%B5%D0%BA%D1%83%D1%80%D1%81%D0%B8%D0%B2%D0%BD%D0%BE%D0%B3%D0%BE_%D1%81%D0%BF%D1%83%D1%81%D0%BA%D0%B0)
       . Алгоритм должен работать за линейное время.
8) Бонус(5): Реализуйте метод `evaluateWithVariables`, который принимает на вход `Map<String, Integer>`, содержащей
   соответствие названия переменной её значению. Если вы не планируете выполнять бонус, сделайте заглушку для этого
   метода всегда возвращающую -1.
