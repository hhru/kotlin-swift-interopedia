## Open class

| Статус             | Ожидание                                                                                              | Реальность                          |
| ------------------ | ----------------------------------------------------------------------------------------------------- | ----------------------------------- |
| :white_check_mark: | Можно наследоваться от open-класса / есть доступ к protected-полям / можно переопределять open-методы | Можно переопределять и final-методы |

### Пояснения

Опишем open class на Kotlin:

```kotlin
open class OpenClassWithConstructorParams(
    val param1: String,
    val param2: Boolean
) {

    protected val someField: String get() = "14"

    fun finalMethodInClass() {
        println("Final method in open class")
    }

    open fun methodCanBeOverride() {
        println("OpenClassWithConstructorParams | methodCanBeOverride")
    }

}
```

На стороне Swift-а мы можем наследоваться от этого класса, использовать его protected-свойства,
переопределять open и даже переопределять **final**-методы:

```swift
class OpenSwiftClass : OpenClassWithConstructorParams {
    override func methodCanBeOverride() {
        print("methodCanBeOverride in SwiftOpen2")
    }
    
    override func finalMethodInClass() {
        print("I can override final method")
    }
}

func example() {
    let osc = OpenSwiftClass(param1: "123", param2: true)
    let _ = osc.someField
}
```

---
[Оглавление](/README.md)