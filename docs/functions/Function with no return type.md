## Function with no return type

| Статус             | Ожидание                                                      | Реальность                       |
| ------------------ | ------------------------------------------------------------- | -------------------------------- |
| :white_check_mark: | Функции, которые ничего не возвращают, можно спокойно вызвать | Реальность совпадает с ожиданием |

### Пояснения

Опишем несколько функций, использующих лямбды из своих аргументов, на Kotlin-е:

```kotlin
// Functions.kt

fun noReturnFunction() {
    println("println -> noReturnFunction()")
}

private fun example() {
    noReturnFunction()
}
```

На стороне Swift-а использование тоже выглядит удобно:

```swift
FunctionsKt.noReturnFunction()
```

---
[Оглавление](/README.md)