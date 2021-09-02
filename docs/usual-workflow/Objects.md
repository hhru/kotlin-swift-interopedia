## Objects 

| Статус    | Ожидание                                                                   | Реальность                                      |
| --------- | -------------------------------------------------------------------------- | ----------------------------------------------- |
| :warning: | Доступ к свойствам и функциям, объявленным в object-е, аналогичен Kotlin-у | Доступ есть через вспомогательный объект shared |

### Пояснения

В Kotlin-е работа с object-ом напоминает работу со статическими методами и константами в Java. То есть:

```kotlin
object ObjectExample {

    const val CONST_VAL_EXAMPLE = "ObjectExample.CONST_VAL_EXAMPLE"

    val someVal = DataClassExample(
        param1 = "someVal.param1",
        param2 = 200,
        param3 = false
    )

    fun functionExample(): String {
        return "ObjectExample.functionExample()"
    }

    fun paramFunctionExample(funcParam1: String): String {
        return "ObjectExample.paramFunctionExample($funcParam1)"
    }

}

private fun example() {
    ObjectExample.CONST_VAL_EXAMPLE
    ObjectExample.someVal
    ObjectExample.functionExample()
    ObjectExample.paramFunctionExample("123")
}
```

В Swift-е для доступа к внутренностям object-а [появляется объект `shared`](https://kotlinlang.org/docs/whatsnew1530.html#improved-swift-objective-c-mapping-for-objects-and-companion-objects), 
к которому можно получить доступ через класс:

```kotlin
func usage() {
    ObjectExample.shared.CONST_VAL_EXAMPLE
    ObjectExample.shared.someVal
    ObjectExample.shared.functionExample()
    ObjectExample.shared.paramFunctionExample("123")
}
```

И объект, кстати, даже если его создавать через `init`, будет являться синглетоном.

---
[Оглавление](/README.md)