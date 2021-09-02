## Usual class val property (readonly)

| Статус             | Ожидание                                                     | Реальность                                  |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------- |
| :white_check_mark: | Доступ к свойству есть из объекта класса / свойство readonly | Реальность совпадает с ожиданием :thumbsup: |

### Пояснения

Объявим простой класс на стороне Kotlin-кода:

```kotlin
class MyClass(
    val param: String
) {
    
    val property: String get() = "123"
    
}
```

На стороне Swift-а мы можем получить доступ и к полям, объявленным в конструкторе, и к свойствам, 
описанных внутри класса:

```swift
func example() {
    let myClass = MyClass(param: "123")
    
    let _ = myClass.param
    let _ = myClass.property
}
```

---
[Оглавление](/README.md)