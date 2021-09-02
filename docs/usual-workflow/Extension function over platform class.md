## Extension function over platform class

| Статус    | Ожидание                                                    | Реальность                                                            |
| --------- | ----------------------------------------------------------- | --------------------------------------------------------------------- |
| :warning: | Функцию можно использовать на объекте платформенного класса | Появляется класс-обёртка с методом, принимающим объект нужного класса |

### Пояснения

Платформенный класс - это, например, какой-то примитивный тип, или же класс, специфичный 
для определённой платформы (`Bundle` для Android, `UILabel` для iOS, etc.).

В Kotlin-е нет разницы в использовании extension-а над обычным или платформенным классом:

```kotlin
// StringExt.kt

fun String.myExtensionFunction() {
    // do something
}

private fun example() {
    "123".myExtensionFunction()
}
```

После перехода в Swift разница проявляется в появлении класса-обёртки для вызова функции:

```swift
func example() {
    StringExtKt.myExtensionFunction(receiver: "123")
}
```

См. [moko-kswift overview](/docs/moko-kswift/Overview.md)

---
[Оглавление](/README.md)