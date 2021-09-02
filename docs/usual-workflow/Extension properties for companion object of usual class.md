## Extension properties for companion object of usual class

| Статус    | Ожидание                                     | Реальность                                              |
| --------- | -------------------------------------------- | ------------------------------------------------------- |
| :warning: | Доступ к свойству можно получить через класс | Доступ к свойству можно получить через объект companion |

### Пояснения

На стороне Kotlin-а объявили extension–свойство для companion object-а обычного класса:

```kotlin
val UsualClass.Companion.EXT_PROP: String get() = "123"
```

Из Swift-а доступ к этому свойству есть через объект `companion`, к которому 
[можно получить доступ через класс](/docs/usual-workflow/Companion%20object.md):

```swift
UsualClassExample.companion.extensionOverCompanion()
```

---
[Оглавление](/README.md)