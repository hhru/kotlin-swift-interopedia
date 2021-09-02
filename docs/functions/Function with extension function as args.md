## Function with extension function as args

| Статус    | Ожидание                                   | Реальность                                           |
| --------- | ------------------------------------------ | ---------------------------------------------------- |
| :warning: | Можно вызвать функцию так же, как в Kotlin | Extension-функция превращается в лямбду с параметром |

### Пояснения

В Kotlin мы можем легко [делать красивые API](https://youtu.be/A2LukgT2mKc?t=1645) вокруг неудобного Android API. 

```kotlin
// Functions.kt

fun funcWithExtension(extension: UsualClassExample.() -> Unit) {
    val someObject = UsualClassExample(
        param1 = "FunctionsExample.funcWithExtension",
        param2 = 500,
        param3 = 600L,
        param4 = 700.0f,
        param5 = 800.0,
        param6 = false
    )
    someObject.apply(extension)
}

private fun example() {
    funcWithExtension {
        this.publicMutableProperty = "changed"
    }
}
```

В Swift extension-функция превратилась в лямбду, где первым параметром идёт receiver:

```swift
let _ = FunctionsKt.funcWithExtension(extension: { usualClassExample in
    usualClassExample.publicMutableProperty = "5000"
})
```

---
[Оглавление](/README.md)