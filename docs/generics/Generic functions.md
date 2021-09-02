## Generic functions

| Статус          | Ожидание                                                       | Реальность                                               |
| --------------- | -------------------------------------------------------------- | -------------------------------------------------------- |
| :no_entry_sign: | Обычная функция-generic позволяет принять аргумент любого типа | Нет автоматического вывода типа, особенности nullability |

### Пояснения

Напишем простую generic-функцию, которая принимает generic на вход и возвращает его же.

```kotlin
fun <T> convert(data: T): T {  
    return data  
}

private fun example() {
    val s: String = convert("322")
    val p: Int = convert(122)
    val l: Long = convert(122L)
}
```

На стороне Swift-а тип `T` интерпретируется как `Any?`, из-за этого приходится вводить дополнительные приведения типов:

```swift
let _: Int = GenericFunctionExampleKt.convert(data: 12) as! Int
let _: String = GenericFunctionExampleKt.convert(data: "'222'") as! String
let _: NotPrimitiveType = GenericFunctionExampleKt.convert(
	data: NotPrimitiveType(item: "122")
) as! NotPrimitiveType
```

Чтобы Swift увидел, что тип точно является not null, нужно использовать boundary-синтаксис на Kotlin-стороне:

```kotlin
fun <T : Any> strictedGeneric(data: T): T {  
    return data  
}
```

Тогда функция `strictedGeneric` на стороне Swift-а возвращает уже `Any`, а не `Any?`.

Но автоматический вывод типа отсутствует.

---
[Оглавление](/README.md)