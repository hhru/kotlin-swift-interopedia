## Function returns primitive type

| Статус             | Ожидание                                                   | Реальность                       |
| ------------------ | ---------------------------------------------------------- | -------------------------------- |
| :white_check_mark: | Функция, возвращающая примитивный тип, работает без ошибок | Реальность совпадает с ожиданием |

### Пояснения

Опишем функцию, возвращающую примитивный тип, на Kotlin-е:

```kotlin
// Functions.kt

fun simpleFunction(): String {
    return "FunctionsExample.simpleFunction()"
}

private fun example() {
    val result = simpleFunction()
}
```

На стороне Swift-а использование тоже выглядит удобным:

```swift
let _ = FunctionsKt.simpleFunction()
```

---
[Оглавление](/README.md)