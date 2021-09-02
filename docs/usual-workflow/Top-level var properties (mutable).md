## Top-level var properties (mutable)

| Статус      | Ожидание                                                                                    | Реальность                                                             |
| ----------- | ------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| :warning:   | Доступ к свойству можно получить напрямую после импорта, аналогично Kotlin-у / поле mutable | Появляется класс-обёртка для доступа к свойству: UtilityKt.propertyVar |

### Пояснения

Опишем top-level var свойство в Kotlin в файле `Utils.kt`:

```kotlin
var topLevelProperty = "Some value"
```

В Kotlin-е подобный код можно вызывать напрямую, без указания названия файла, достаточно сделать `import` нужного
свойства.

На стороне Swift [мы получаем класс-обёртку `UtilsKt`](https://kotlinlang.org/docs/native-objc-interop.html#top-level-functions-and-properties) (название файла в Kotlin-е + суффикс `Kt`),
с помощью которого можно получить доступ к нужному property:

```swift
func example() {
    let _ = UtilsKt.topLevelProperty
}
```

Свойство является изменяемым:

```swift
func example() {
    UtilsKt.topLevelProperty = "Changed from Swift"
}
```

---
[Оглавление](/README.md)