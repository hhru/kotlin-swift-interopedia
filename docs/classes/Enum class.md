## Enum class

| Статус    | Ожидание                                                                               | Реальность                                                                     |
| --------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| :warning: | Kotlin-овский enum class превратится в enum Swift-а, и можно будет использовать switch | Не работает как ожидается. Но сгенерировался объект со статическими элементами |

### Пояснения

Опишем обычный enum class в Kotlin-е:

```kotlin
enum class MyEnum(val type: String) {

    ENTRY_ONE("entry_one"),
    ENTRY_TWO("entry_two");

    companion object {
        fun findByType(type: String) = values().find { it.type == type }
    }

}
```

На стороне Swift-а не был сгенерирован enum, и как следствие, класс нельзя удобно использовать в 
выражении `switch`. Но доступ к элементам enum-а есть, есть доступ к функции внутри companion object-а, 
есть возможность вызвать метод `values()`.

```swift
func enumClassUsage() {
    let _ = MyEnum.entryOne
    let _ = MyEnum.entryTwo
    
    let _ = MyEnum.entryOne.name
    let _ = MyEnum.entryOne.type
    
    let _ = MyEnum.companion.findByType(type: "entry_two")
    let optionalResult = MyEnum.companion.findByType(type: "entry_two_trheee")
}

private func enumEntryUsage(enumClassExample: MyEnum) {
	switch enumClassExample {
	default:
		print("Sad")
	}
}
```

[Kotlin/Native пока что не поддерживает генерацию enum-а](https://youtrack.jetbrains.com/issue/KT-48068).

См. [moko-kswift overview](/docs/moko-kswift/Overview.md)

---
[Оглавление](/README.md)