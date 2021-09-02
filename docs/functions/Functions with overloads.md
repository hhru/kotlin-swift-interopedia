## Functions with overloads

| Статус    | Ожидание                                                            | Реальность                                                    |
| --------- | ------------------------------------------------------------------- | ------------------------------------------------------------- |
| :warning: | Использование перегруженных функций ничем не отличается от Kotlin-а | Есть особенности при использовании одинаковых имён параметров |

### Пояснения

В Kotlin-е мы можем спокойно перегружать какие-то функции аргументами с тем же самым именем, никаких изменений в сигнатуре не будет:

```kotlin
// OverloadExample.kt

fun overloadFunction(param: Int) {  
    println("Utility.overloadFunction(param: Int) | $param")  
}  
  
fun overloadFunction(param: Long) {  
    println("Utility.overloadFunction(param: Long) | $param")  
}  
  
fun overloadFunction(param: Float) {  
    println("Utility.overloadFunction(param: Float) | $param")  
}  
  
fun overloadFunction(param: Double) {  
    println("Utility.overloadFunction(param: Double) | $param")  
}  
  
fun overloadFunction(param: String) {  
    println("Utility.overloadFunction(param: String) | $param")  
}  
  
fun overloadFunction(param: Boolean) {  
    println("Utility.overloadFunction(param: Boolean) | $param")  
}  
  
  
private fun example() {  
    overloadFunction(param = "1222")  
    overloadFunction(true)  
    overloadFunction(param = 2.0)  
    overloadFunction(1.0f)  
    overloadFunction(param = 1)  
    overloadFunction(2L)  
}
```

При компиляции в Swift для того, чтобы функции отличались друг от друга, к имени параметра 
добавляется нижнее подчёркивание. Для каждой последующей функции - добавляется ещё одно. 

```swift
OverloadExampleKt.overloadFunction(param: true)  // Bool
OverloadExampleKt.overloadFunction(param_: 2.0)  // Double
OverloadExampleKt.overloadFunction(param__: 2.0) // Float
OverloadExampleKt.overloadFunction(param___: 2)  // Int32
OverloadExampleKt.overloadFunction(param____: 4) // Int64
OverloadExampleKt.overloadFunction(param_____: "123")
```

Соответственно, если каждый раз использовать разные имена параметров, то всё будет в порядке.

В Kotlin-е:

```kotlin
fun anotherOverload(intParam: Int) {
    println("anotherOverloadsWithDifferNames.kt.anotherOverload(param: Int) | $intParam")
}

fun anotherOverload(longParam: Long) {
    println("anotherOverloadsWithDifferNames.anotherOverload(param: Long) | $longParam")
}

fun anotherOverload(floatParam: Float) {
    println("anotherOverloadsWithDifferNames.anotherOverload(param: Float) | $floatParam")
}

private fun example() {
    anotherOverload(intParam = 1)
    anotherOverload(longParam = 1L)
    anotherOverload(1.0f)
}
```

В Swift-е:

```swift
private funс example() {
    OverloadExampleKt.anotherOverload(intParam: 1)
    OverloadExampleKt.anotherOverload(longParam: 1)
    OverloadExampleKt.anotherOverload(floatParam: 1.0)
}
```

---
[Оглавление](/README.md)