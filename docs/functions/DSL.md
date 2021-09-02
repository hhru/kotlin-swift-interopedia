## DSL

| Статус    | Ожидание                                                | Реальность                                                                      |
| --------- | ------------------------------------------------------- | ------------------------------------------------------------------------------- |
| :warning: | Надеемся, что DSL в Kotlin-е превратится в DSL на Swift | Сгенерировались функции с receiver-ами, выглядит не так удобно, как хотелось бы |

### Пояснения

В Kotlin-е есть возможность создать DSL на основе множества extension-функций, 
которые нужно передавать внутрь других функций. Для примера - [DSL для UI-тестов](https://habr.com/ru/company/hh/blog/455042/).

```kotlin
@DslMarker
annotation class DslMarkerExample

interface Experiment {
    val key: String
    val description: String
}

@DslMarkerExample
class ExperimentsDsl {

    val list = mutableListOf<Experiment>()

    fun enable(experiment: Experiment) {
        list += experiment
    }

}

@DslMarkerExample
class Dsl {
    val experiments = ExperimentsDsl()

    fun experiments(block: ExperimentsDsl.() -> Unit = {}) {
        experiments.block()
    }
}

private fun example() {
    Dsl().apply {
        experiments {
            enable(object : Experiment {
                override val key: String get() = "key1"
                override val description: String  get() = "desc1"
            })
        }
    }
}
```

Но при переходе в Swift extension-функции в аргументах превращаются в функции с параметрами, 
что выглядит не так, как хотелось бы:

```swift
dslBlock { dsl in
    dsl.experiments { experimentsDsl in
        experimentsDsl.enable(...)
    }   
}

private func dslBlock(block: (Dsl) -> Dsl) -> Dsl {
    var dsl = Dsl()
    dsl = block(dsl)
    return dsl
}
```

[В Swift-е можно статейка на Habr-е про DSL в Swift](https://habr.com/ru/company/tinkoff/blog/455760/), 
а ещё есть [github-репозиторий со списком Swift-библиотек, построенных на DSL](https://github.com/carson-katri/awesome-result-builders).

---
[Оглавление](/README.md)