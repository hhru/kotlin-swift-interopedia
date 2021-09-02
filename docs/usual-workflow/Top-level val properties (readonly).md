## Top-level val properties (readonly)

| Статус      | Ожидание                                                                                     | Реальность                                                             |
| ----------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| :warning:   | Доступ к свойству можно получить напрямую после импорта, аналогично Kotlin-у / поле readonly | Появляется класс-обёртка для доступа к свойству: UtilityKt.propertyVal |

### Пояснения

Опишем top-level val свойство в Kotlin в файле `Utils.kt`:

```kotlin
val topLevelProperty = "Some value"
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

Свойство является `readonly`, изменить его не получится.

---
[Оглавление](/README.md)