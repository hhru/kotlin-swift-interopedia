## Collections with custom types data

| Статус             | Ожидание                                                                   | Реальность                       |
| ------------------ | -------------------------------------------------------------------------- | -------------------------------- |
| :white_check_mark: | Коллекции с элементами кастомных типов не требуют дополнительных маппингов | Маппинги не требуются :thumbsup: |

### Пояснения

Пусть на стороне Kotlin-а был объявлен следующий код:

```kotlin
data class NotPrimitiveType(
    val item: String
)

fun notPrimitiveTypeList(list: List<NotPrimitiveType>): List<NotPrimitiveType> {
    return list
}

fun notPrimitiveTypeSet(set: Set<NotPrimitiveType>): Set<NotPrimitiveType> {
    return set
}

fun notPrimitiveTypeMap(map: Map<String, NotPrimitiveType>): Map<String, NotPrimitiveType> {
    return map
}
```

На стороне Swift коллекции с кастомными типами данных можно использовать без специальных маппингов:

```swift
func notPrimitiveCollections(list: [NotPrimitiveType], set: Set<NotPrimitiveType>, map: [String: NotPrimitiveType]) {
    let myList: [NotPrimitiveType] = NotPrimitiveTypeKt.notPrimitiveTypeList(list: list)
    let mySet: Set<NotPrimitiveType> = NotPrimitiveTypeKt.notPrimitiveTypeSet(set: set)
    let myMap: [String: NotPrimitiveType] = NotPrimitiveTypeKt.notPrimitiveTypeMap(map: map)
}
```

---
[Оглавление](/README.md)