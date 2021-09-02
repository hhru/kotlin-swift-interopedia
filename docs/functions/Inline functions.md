## Inline functions

| Статус             | Ожидание                                         | Реальность                       |
| ------------------ | ------------------------------------------------ | -------------------------------- |
| :white_check_mark: | Инлайн-функции есть в .h-файле, их можно вызвать | Реальность совпадает с ожиданием |

### Пояснения

Опишем inline-функцию в Kotlin-е:

```kotlin
// Functions.kt

inline fun inlineFunction(action: () -> Unit) {
    println("FunctionsExample.inlineFunction() begin")
    action.invoke()
    println("FunctionsExample.inlineFunction() end")
}
```

В Swift эта функция тоже доступна, её можно вызвать без проблем:

```swift
FunctionsKt.inlineFunction {
    print("I'm inside inline!!!")
}
```

---
[Оглавление](/README.md)