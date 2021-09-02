## Unit and Nothing

| Статус             | Ожидание                                                                                                        | Реальность                                    |
| ------------------ | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| :white_check_mark: | Типы Unit и Nothing можно использовать так же, как в Kotlin: Unit как объект или void, Nothing - нельзя создать | Реальность соответствует ожиданиям :thumbsup: |

### Пояснения

Пусть у нас есть такой класс на Kotlin-е:

```kotlin
class UnitNothingExample {

    fun unitType(p: Unit) {

    }

    fun nothingType(n: Nothing) {

    }

    fun returnUnit(): Unit {

    }

    fun returnNothing(): Nothing {
        throw IllegalStateException()
    }

}
```

После перехода в Swift мы получаем из типов `Unit` и `Nothing` типы `KotlinUnit` и `KotlinNothing`.
При этом можно создать объект класса `KotlinUnit`, и нельзя создать объект типа `KotlinNothing`.

---
[Оглавление](/README.md)