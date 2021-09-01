## Internal modifier

| Статус фичи        | Ожидание                                   | Реальность                                                                           |
| ------------------ | ------------------------------------------ | ------------------------------------------------------------------------------------ |
| :white_check_mark: | Internal-функции и классы не видны в Swift | Так и есть, с iOS-разработчиками придётся обсуждать только публичное API общего кода |

### Пример

Если описать какой-нибудь internal-класс в Kotlin:

```kotlin
internal class InternalClassExample(
    val param1: Int,
    val param2: Float,
    val param3: Double
) {

    val someProperty: String
        get() {
            val calculated = someFunction()
            return "${calculated}123"
        }

    fun someFunction(): String {
        return "Internal Class example"
    }

}
```

То при попытке использовать этот класс в Swift-коде мы получаем ошибку, так как класс не может быть найден. 

---
[Оглавление](/README.md) | [02 - JavaDoc comments.md](/docs/02%20-%20JavaDoc%20comments.md)