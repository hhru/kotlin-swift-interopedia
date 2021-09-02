## Top-level functions

| Статус      | Ожидание                                                               | Реальность                                             |
| ----------- | ---------------------------------------------------------------------- | ------------------------------------------------------ |
| :warning:   | Функцию можно использовать напрямую после импорта, аналогично Kotlin-у | Появляется класс-обёртка: UtilityKt.topLevelFunction() |

### Пояснения

Опишем top-level функцию в Kotlin в файле `Utils.kt`:

```kotlin
fun topLevelFunction() {
    println("Hello from top-level function")
}
```

В Kotlin-е подобный код можно вызывать напрямую, без указания названия файла, достаточно сделать `import` нужного
свойства.

На стороне Swift [мы получаем класс-обёртку `UtilsKt`](https://kotlinlang.org/docs/native-objc-interop.html#top-level-functions-and-properties) 
(название файла в Kotlin-е + суффикс `Kt`), с помощью которого можно получить доступ к нужной функции:

```swift
func example() {
    UtilsKt.topLevelFunction()
}
```

---
[Оглавление](/README.md)