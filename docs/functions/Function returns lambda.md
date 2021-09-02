## Function returns lambda

| Статус             | Ожидание                                                             | Реальность                       |
| ------------------ | -------------------------------------------------------------------- | -------------------------------- |
| :white_check_mark: | Функция, вернувшая лямбду, работает без крашей; лямбду можно вызвать | Реальность совпадает с ожиданием |

### Пояснения

Опишем функцию, возвращающую какую-нибудь лямбду, на Kotlin-е:

```kotlin
// Functions.kt

fun returnLambda(): () -> Unit {
    println("Function that returns lambda")

    return {
        println("Lambda inside return")
    }
}

fun returnParametrizedLambda(): (String) -> Unit {
    println("Function that returns parametrized lambda")

    return {
        println("returnParametrizedLambda | it: $it")
    }
}

private fun example() {
    FunctionsKt.returnLambda().invoke()
    FunctionsKt.returnParametrizedLambda().invoke("123")
}
```

На стороне Swift-а использование тоже выглядит удобным:

```swift
functionsExample.returnLambda()()
let _ = functionsExample.returnParametrizedLambda()("123")
```

---
[Оглавление](/README.md)