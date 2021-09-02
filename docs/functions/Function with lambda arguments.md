## Function with lambda arguments

| Статус             | Ожидание                                                                                     | Реальность                       |
| ------------------ | -------------------------------------------------------------------------------------------- | -------------------------------- |
| :white_check_mark: | Функция, принимающая в аргументах одну или несколько лямбд, нормально конвертируется в Swift | Реальность совпадает с ожиданием |

### Пояснения

Опишем несколько функций, использующих лямбды из своих аргументов, на Kotlin-е:

```kotlin
// Functions.kt

fun funcWithLambda(calculation: () -> Int): Int {
    return 100 + calculation.invoke()
}

fun funcWithSeveralLambdas(
    calculation: () -> Int,
    formatting: (String) -> String
): String {
    val calculationResult = calculation.invoke()
    return formatting.invoke(calculationResult.toString())
}

fun funcWithParametrizedLambda(parametrizedLambda: (String) -> String): String {
    return "FunctionsExample.funcWithParametrizedLambda(resultFromLambda: ${parametrizedLambda.invoke("paramForLambda")})"
}

fun funcWithUnitLabmda(unitLambda: () -> Unit) {
    println("FunctionsExample.funcWithUnitLabmda() begin")
    unitLambda.invoke()
    println("FunctionsExample.funcWithUnitLabmda() end")
}

private fun example() {
    funcWithLambda {
        20
    }
    funcWithSeveralLambdas(
        calculation = { 400 },
        formatting = { "formatted $it" }
    )
    funcWithParametrizedLambda {
        "parametrized $it"
    }

    funcWithUnitLabmda {
        // do something
    }
}
```

На стороне Swift-а использование тоже выглядит удобно:

```swift
// Lambda with result usage
let result1 = FunctionsKt.funcWithLambda(calculation: {
    print("FunctionsKt.funcWithLambda | inside lambda --> ")
    return 2
})
let result2 = FunctionsKt.funcWithLambda {
    return 30
}
print("result1: \(result1) , result2: \(result2)")


// Parametrized lambda example
let result3 = FunctionsKt.funcWithParametrizedLambda(parametrizedLambda: { arg in
    return "funcWithParametrizedLambda | arg: \(arg)"
})
let result4 = FunctionsKt.funcWithParametrizedLambda { arg in
    return "funcWithParametrizedLambda | arg: \(arg)"
}
let result5 = FunctionsKt.funcWithParametrizedLambda {_ in
    return "funcWithParametrizedLambda | skip argument using"
}
print("result3: \(result3) , result4: \(result4), result5: \(result5)")

// Unit lambda in args
FunctionsKt.funcWithUnitLabmda {
    // do some stuff
}

// Several lambdas in args
let _ = FunctionsKt.funcWithSeveralLambdas(
    calculation: {
        return 2
    }, formatting: { arg in
        return "Some \(arg)"
    }
)
```

---
[Оглавление](/README.md)