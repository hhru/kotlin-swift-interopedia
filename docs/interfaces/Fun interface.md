## Fun interface

| Статус          | Ожидание                                                                  | Реальность                             |
| --------------- | ------------------------------------------------------------------------- | -------------------------------------- |
| :no_entry_sign: | С помощью такого протокола можно более простым синтаксисом описать лямбду | В Swift нельзя создать анонимный класс |

### Пояснения

В Kotlin-е при помощи `fun interface`-ов можно более удобным синтаксисом описывать создание анонимных лямбд:

```kotlin
fun interface FunInterfaceExample {
    fun singleFunctionInInterface(funInterfaceExample: String): String
}

interface NotFunInterface {
    fun singleFunctionInInterface(funInterfaceExample: String): String
}

private fun example() {
    val notFun = object : NotFunInterface {
        override fun singleFunctionInInterface(funInterfaceExample: String): String {
            return "return"
        }

    }

    val listener = FunInterfaceExample {
        println("it: ${it}")
        "some return value"
    }
}
```

В [Swift нет аналогичного синтаксиса для описания анонимных классов](https://stackoverflow.com/questions/24408068/anonymous-class-in-swift). 
Можно, конечно, делать как в одном из ответов на StackOverflow, но это кажется каким-то большим overhead-ом:

```swift
class EmptyClass {

    var someFunc: () -> () = { }

    init(overrides: EmptyClass -> EmptyClass) {
        overrides(self)
    }
}

// Now you initialize 'EmptyClass' with a closure that sets
// whatever variable properties you want to override:

let workingClass = EmptyClass { ec in
    ec.someFunc = { println("It worked!") }
    return ec
}

workingClass.someFunc()  // Outputs: "It worked!"
```

---
[Оглавление](/README.md)