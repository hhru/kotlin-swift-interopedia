## Sealed class

| Статус          | Ожидание                                                                                               | Реальность                                                                      |
| --------------- | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------- |
| :no_entry_sign: | Корректно конвертируется в структуру, которую можно передать в switch-конструкцию и сделать exhaustive | Генерируется класс с наследниками. Передав в switch нет подсказок об exhaustive |

### Пояснения

В Kotlin-е sealed-классы могут использоваться в `when`-выражениях, которые могут подсказывать программисту 
о забытых ветках:

```kotlin
sealed class MySealed {
    object Object : MySealed()

    class Simple(val param1: String) : MySealed()

    data class Data(val param1: String, val param2: Boolean) : MySealed()
}

private fun example(s: MySealed) {
    when (s) {
        MySealed.Object -> TODO()
        is MySealed.Simple -> TODO()
        is MySealed.Data -> TODO()
    }
}
```

Но в Swift такой класс сконвертируется как обычный класс с наследниками, который бесполезен при подстановке в `switch`:

```switch
func example(s: MySealed) {
    switch s {
    default:
        print("Sad")
    }
}
```

В Swift-е роль sealed-классов выполняют enum-ы, и можно было бы написать специальный bridge-код для конвертации 
sealed-классов в Swift-овый enum.

См. [moko-kswift overview](/docs/moko-kswift/Overview.md)

---
[Оглавление](/README.md)