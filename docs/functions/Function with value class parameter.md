## Function with no return type

| Статус          | Ожидание                                                                         | Реальность                                                                     |
| --------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| :no_entry_sign: | Функция появится в .h-файле и её можно будет использовать, передавая value-класс | Функция появилась в .h-файле, но аргумент value-класса развернулся в примитивы |

### Пояснения

Опишем функцию, которая на вход принимает value-класс:

```kotlin
value class ValueClassExample(val t: Int)

fun valueClassUsageExample(v: ValueClassExample): String {
    return "Value class usage example | ${v.t}"
}
```

На стороне Swift-а функция `valueClassUsageExample` присутствует, 
но так как [сам value-класс в .h-файл не попал](/docs/classes/Value%20class.md), аргумент разворачивается 
в отдельные примитивы:

```swift
// тип для v : Int32
ValueClassExampleKt.valueClassUsageExample(v: 40)
```

---
[Оглавление](/README.md)