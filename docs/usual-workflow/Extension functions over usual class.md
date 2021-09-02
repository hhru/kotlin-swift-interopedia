## Extension function over usual class

| Статус             | Ожидание                                     | Реальность                                  |
| ------------------ | -------------------------------------------- | ------------------------------------------- |
| :white_check_mark: | Функцию можно использовать на объекте класса | Реальность совпадает с ожиданием :thumbsup: |

### Пояснения

Объявим в Kotlin-коде extension-функцию над кастомным типом:

```kotlin
// UsualClassExt.kt

fun UsualClass.extensionFunction() {
    // do something
}

```

На стороне Swift-а мы сможем использовать эту функцию аналогично Kotlin-у, на объекте нужного класса:

```swift
func example() {
   UsualClass().extensionFunction()
}
```

---
[Оглавление](/README.md)