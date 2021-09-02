## Extension properties over usual class

| Статус             | Ожидание                                             | Реальность                                  |
| ------------------ | ---------------------------------------------------- | ------------------------------------------- |
| :white_check_mark: | Доступ к свойству можно получить через объект класса | Реальность совпадает с ожиданием :thumbsup: |

### Пояснения

Объявим в Kotlin-коде extension-свойство для кастомного типа:

```kotlin
// UsualClassExt.kt

val UsualClass.extensionProperty: String get() = "123" 
```

На стороне Swift-а мы сможем использовать это свойство аналогично Kotlin-у, на объекте нужного класса:

```swift
func example() {
   let _ = UsualClass().extensionProperty
}
```

---
[Оглавление](/README.md)