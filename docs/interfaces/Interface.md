## Interface

| Статус             | Ожидание                                                    | Реальность                                                                |
| ------------------ | ----------------------------------------------------------- | ------------------------------------------------------------------------- |
| :white_check_mark: | При реализации интерфейса, IDE подставит заглушки для всего | Интерфейс стал @protocol-ом. Но почему-то val-свойство превратилось в var |

### Пояснения

Создадим интерфейс на стороне Kotlin-а:

```kotlin
interface InterfaceExample {

    val id: String

    fun simpleFunction(): String
    fun functionWithParam(param1: String): String
    fun defaultParams(param1: String, param2: Int = 400): String

}

class MyInt : InterfaceExample {
    // Можно руками заменить на var, но изначально сгенерировался val
    override var id: String = "1"

    override fun simpleFunction(): String {
        TODO("Not yet implemented")
    }

    override fun functionWithParam(param1: String): String {
        TODO("Not yet implemented")
    }

    override fun defaultParams(param1: String, param2: Int): String {
        TODO("Not yet implemented")
    }

}
```

На стороне Swift-а интерфейс превратился в `protocol`, и при попытке его реализовать, IDE генерирует нужные заглушки:

```swift
class SwiftInterface : InterfaceExample {
    func defaultParams(param1: String, param2: Int32) -> String {
        return "param1: \(param1) ; param2: \(param2)"
    }
    
    func functionWithParam(param1: String) -> String {
        return "functionWithParam: \(param1)"
    }
    
    func simpleFunction() -> String {
        return "simpleFunction()"
    }
    
    // Из странного -- `val id: String` по умолчанию превратился в `var`. 
    // Но это можно руками заменить на `let`
    let id: String = "default"
}
```

---
[Оглавление](/README.md)