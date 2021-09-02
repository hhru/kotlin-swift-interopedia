## Inner class

| Статус    | Ожидание                                                                                     | Реальность                              |
| --------- | -------------------------------------------------------------------------------------------- | --------------------------------------- |
| :warning: | Можно создать инстанс inner-класса / прямого доступа к родительским свойствам и функциям нет | Небольшие отличия в синтаксисе создания |

### Пояснения

Создадим небольшой inner-класс на Kotlin-е:

```kotlin
class InnerClassExample(
    val param: String
) {

    fun parentFunc() {}

    inner class MyInnerClass {
        fun useSomeFunction() {
            println("this@InnerClassExample.param == ${this@InnerClassExample.param}")
        }
    }
}

private fun example() {
    val inner = InnerClassExample("12").MyInnerClass()
}
```

В Swift-е немного меняется синтаксис создания экземпляра inner-класса, нужно явно передавать родительский класс в конструктор:

```swift
let _ = InnerClassExample.MyInnerClass(InnerClassExample(param: "1323"))
```

---
[Оглавление](/README.md)