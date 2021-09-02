## Generic classes

| Статус    | Ожидание                                                          | Реальность                                     |
| --------- | ----------------------------------------------------------------- | ---------------------------------------------- |
| :warning: | Сгенерируется класс с generic-ом, пользоваться можно как в Kotlin | Есть некоторые особенности использования типов |

### Пояснения

Опишем generic-класс в Kotlin-е:

```kotlin
class StateHolderWithoutAny<T>(data: T) {
    val myState = data
    fun pullState(): T = myState
}
```

[Нельзя сделать generic над примитивными типами](https://stackoverflow.com/questions/51196984/objective-c-generic-containing-a-scalar/51197180#51197180). 
Интероп ведётся через Objective-c, который не даёт это сделать.

Какие типы нельзя подставить:

- `Int` / `Int8` / `Int16` / `Int32` / `Int64`
- `Float` / `Double`
- `String`
- `Bool`

Но можно обойтись `NSNumber`, `NSString`

Ещё одна особенность связана с nullability - аналогично generic-функциям. 
Тип `T` интерпретируется как `Any?`, из-за этого приходится вводить дополнительные приведения типов:

```swift
let _: Int = GenericFunctionExampleKt.convert(data: 12) as! Int
let _: String = GenericFunctionExampleKt.convert(data: "'222'") as! String
let _: NotPrimitiveType = GenericFunctionExampleKt.convert(
	data: NotPrimitiveType(item: "122")
) as! NotPrimitiveType
```

Чтобы Swift увидел, что тип точно является not null, нужно использовать boundary-синтаксис на Kotlin-стороне:

```kotlin
class StateHolderWithAny<T : Any>(data: T) {
    val myState = data
    fun pullState(): T = myState
}
```

---
[Оглавление](/README.md)