## Reified functions

| Статус          | Ожидание                                                                     | Реальность                  |
| --------------- | ---------------------------------------------------------------------------- | --------------------------- |
| :no_entry_sign: | Функции с reified нормально вызываются из Swift + работают ожидаемым образом | В рантайме функция крашится |

### Пояснения

Опишем reified-функцию в Kotlin-е:

```kotlin
inline fun<reified T> reifiedExample(marks: Int): T {
    return when (T::class) {
        Int::class -> marks as T
        String::class -> "Congratulations! you scored more than 90%" as T
        else -> "Please enter valid type" as T
    }
}
```

Пытаемся вызвать из Swift-а:

```swift
private func reifiedExample() {
    let c = ReifiedExampleKt.reifiedExample(marks: 23)
    print("c = \(String(describing: c))")
}
```

При попытке вызова приложение падает с ошибкой:

```
Function doesn't have or inherit @Throws annotation and thus exception isn't propagated from Kotlin to Objective-C/Swift as NSError.
It is considered unexpected and unhandled instead. Program will be terminated.
Uncaught Kotlin exception: kotlin.IllegalStateException: unsupported call of reified inlined function `ru.hh.hh_mobile_sdk.generics.reifiedExample`
```

Добавляем на стороне Kotlin-а аннотацию `@Throws(IllegalStateException)`, получаем другую ошибку:

```
My error messasge 
Error Domain=KotlinException Code=0 "unsupported call of reified inlined function `ru.hh.hh_mobile_sdk.reifiedExample`" 
UserInfo={NSLocalizedDescription=unsupported call of reified inlined function `ru.hh.hh_mobile_sdk.reifiedExample`, 
KotlinException=kotlin.IllegalStateException: unsupported call of reified inlined function `ru.hh.hh_mobile_sdk.reifiedExample`, 
KotlinExceptionOrigin=}
```

---
[Оглавление](/README.md)