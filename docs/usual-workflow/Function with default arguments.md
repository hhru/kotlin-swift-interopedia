## Function with default arguments

| Статус          | Ожидание                                                              | Реальность                                        |
| --------------- | --------------------------------------------------------------------- | ------------------------------------------------- |
| :no_entry_sign: | Работа с функциями, имеющими дефолтные аргументы, аналогична Kotlin-у | Всегда приходится указывать все аргументы функции |

### Пояснения

В Kotlin-е можно опускать указание значений аргументов функции, если у них имеются дефолтные значения:

```kotlin
class MyClass {

    fun defaultParamsFunction(funcParam1: String, funcParam2: Int = 30): String {
        return "123"
    }
    
}

private fun example() {
    // funcParam2 имеет default-значение
    MyClass().defaultParamsFunction(funcParam1 = "1")
}
```

После перехода в Swift эта фича пропадает, и требуется указывать все аргументы при вызове функции:

```swift
func example() {
    MyClass().defaultParamsFunction(funcParam1: "1", funcParam2: 100)
}
```

moko-kswift это [пока не чинит](https://github.com/icerockdev/moko-kswift/issues/8).

---
[Оглавление](/README.md)