## Mutable, immutable collections

| Статус    | Ожидание                                                                                                                                         | Реальность                                                                                                                       |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| :warning: | Сигнатуры List / MutableList / etc имеют значение в Swift-мире и тоже регулируют мутабельность ; Использование коллекций не отличается от Kotlin | Для регулировки мутабельности используются ключевые слова let, var / Для мутабельных коллекций требуются дополнительные маппинги |

### Пояснения

Вне зависимости от того, какую сигнатуру объявили на стороне Kotlin-а, мутабельную (`MutableList`) или нет (`List`), 
на стороне Swift-а можно передать и изменяемую, и неизменяемую коллекции.

Был вот такой код на стороне Kotlin-а:

```kotlin
fun listType(list: List<Int>): List<Int> {  
    return mutableListOf(1, 2, 3).also { it.addAll(list) }  
}  

fun mutableListType(list: MutableList<Int>): MutableList<Int> {  
    return mutableListOf(4, 5, 6).also { it.addAll(list) }  
}
```

В Swift регулировка мутабельности делается ключевыми словами `var` и `let`:

```swift
private func collectionsMutability() {
	let types = PrimitiveTypesClass()

	var mutableList: [KotlinInt] = [1, 2, 3]
	let notMutableList: [KotlinInt] = [1, 2, 3]

	mutableList = types.listType(list: mutableList)
	let _ = types.listType(list: notMutableList)
}
```

Кстати, если записать результат функции, возвращающей `List` в `var`-переменную, то можно спокойно изменять эту 
коллекцию, крашей не будет:

```swift
var list = typeClass.listType(list: [12, 34])
list.append(2)
```

#### List / MutableList

С мутабельными коллекциями уже другие правила и [другие типы](https://kotlinlang.org/docs/native-objc-interop.html#collections). 
`MutableList` превращается в `NSMutableArray`, но можно использовать простой способ превращения `[KotlinInt]` в `NSMutableArray`.

```swift
var mutableList: [KotlinInt] = [1, 2, 3]
let notMutableList: [KotlinInt] = [1, 2, 3]

let _ = types.mutableListType(list: NSMutableArray(array: notMutableList))
let _ = types.mutableListType(list: NSMutableArray(array: mutableList))
```

#### Set / MutableSet
Пусть на стороне Kotlin-а у нас будет объявлено две функции, использующие `Set` и `MutableSet`:

```kotlin
fun setType(set: Set<Int>): Set<Int> {  
    return mutableSetOf(1, 2, 3).also { it.addAll(set) }  
}  
  
fun mutableSetType(set: MutableSet<Int>): MutableSet<Int> {  
    return mutableSetOf(4, 5, 6).also { it.addAll(set) }  
}
```

С immutable-версией ничего примечательного, с mutable - на стороне Swift 
[потребуется приведение типов](https://kotlinlang.org/docs/native-objc-interop.html#collections) 
к `KotlinMutableSet`:

```swift
var mutableSet: Set<KotlinInt> = Set(arrayLiteral: 1, 2, 3)
let notMutableSet: Set<KotlinInt> = Set(arrayLiteral: 1, 2, 3)

mutableSet = types.setType(set: mutableSet)
let _ = types.setType(set: notMutableSet)

let _ = types.mutableSetType(set: KotlinMutableSet(set: mutableSet))
let _ = types.mutableSetType(set: KotlinMutableSet(set: notMutableSet))
```

Если нужно привести `KotlinMutableSet` к Swift-овому `Set`-у, нужно делать явный cast:

```swift
var mutableSet: Set<KotlinInt> = Set(arrayLiteral: 1, 2, 3)

mutableSet = types.mutableSetType(
	set: KotlinMutableSet(set: mutableSet)
) as! Set<KotlinInt>
```

Это возможно, потому что `KotlinMutableSet` == `NSMutableSet`.

#### Map / MutableMap
Пусть на стороне Kotlin-а у нас будет объявлено две функции, использующие `Map` и `MutableMap`:

```kotlin
fun mapType(map: Map<String, Int>): Map<String, Int> {  
    return mutableMapOf(  
        "1" to 1,  
		"2" to 2,  
		"3" to 3  
	).also { it.putAll(map) }  
}  
  
fun mutableMapType(map: MutableMap<String, Int>): MutableMap<String, Int> {  
    return mutableMapOf(  
        "1" to 1,  
		"2" to 2,  
		"3" to 3  
	).also { it.putAll(map) }  
}
```

С immutable-версией ничего примечательного, с mutable - на стороне Swift
[потребуется приведение типов](https://kotlinlang.org/docs/native-objc-interop.html#collections)
к `KotlinMutableDictionary`:

```swift
var mutableMap: Dictionary<String, KotlinInt> = Dictionary(dictionaryLiteral: ("1", 1), ("2", 2), ("3", 3))
var mutableMapLiteral: [String: KotlinInt] = [
	"1": 1,
	"2": 2,
	"3": 3
]
let notMutableMap: Dictionary<String, KotlinInt> = Dictionary(
	dictionaryLiteral: ("1", 1), ("2", 2), ("3", 3)
)
let notMutableMapLiteral: [String: KotlinInt] = [
	"1": 1,
	"2": 2,
	"3": 3
]

mutableMap = types.mapType(map: mutableMap)
mutableMapLiteral = types.mapType(map: mutableMapLiteral)
let _ = types.mapType(map: notMutableMap)
let _ = types.mapType(map: notMutableMapLiteral)

let _ = types.mutableMapType(
	map: KotlinMutableDictionary(dictionary: mutableMap)
)
let _ = types.mutableMapType(
	map: KotlinMutableDictionary(dictionary: mutableMapLiteral)
)
let _ = types.mutableMapType(
	map: KotlinMutableDictionary(dictionary: notMutableMap)
)
let _ = types.mutableMapType(
	map: KotlinMutableDictionary(dictionary: notMutableMapLiteral)
)
```

Если нужно привести `KotlinMutableDictionary` к Swift-овому `Dictionary`-у, нужно делать явный cast:

```swift
mutableMap = types.mutableMapType(
	map: KotlinMutableDictionary(dictionary: mutableMap)
) as! Dictionary<String, KotlinInt>
```

Это возможно, потому что `KotlinMutableDictionary` == `NSMutableDictionary`.

---
[Оглавление](/README.md)