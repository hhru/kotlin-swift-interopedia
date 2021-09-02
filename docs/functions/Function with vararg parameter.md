## Function with vararg parameter

| Статус          | Ожидание                                                         | Реальность                     |
| --------------- | ---------------------------------------------------------------- | ------------------------------ |
| :no_entry_sign: | vararg смапился в Swift-овый variardic и используется аналогично | Не работает так, как ожидается |

### Пояснения

Опишем функцию, использующую `vararg`-аргументы, в Kotlin-е:

```kotlin
// Functions.kt

fun funcWithVararg(vararg item: String) {  
    println(item.joinToString { "$it | " })  
}

private fun example() {
    funcWithVararg("1", "2", "3")
}
```

В Swift-коде это превращается в функцию, которая на вход принимает `KotlinArray<NSString>`.

```swift
let arr = KotlinArray<NSString>(
	size: 10, 
	init: { index in "\(index)" as NSString }
)
FunctionsKt.funcWithVararg(item: arr)
```

[В YouTrack-е есть issue про эту проблему](https://youtrack.jetbrains.com/issue/KT-42925), но variardic-параметры 
в Objective-C являются compile time-аргументами, и Kotlin не может просто взять и преобразовать vararg.

---
[Оглавление](/README.md)