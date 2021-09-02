## Collections with primitive types

| Статус    | Ожидание                                                                     | Реальность                                   |
| --------- | ---------------------------------------------------------------------------- | -------------------------------------------- |
| :warning: | Коллекции с элементами примитивных типов не требуют дополнительных маппингов | Маппинги не требуются только для String-типа |

### Пояснения

Примитивные типы Kotlin-а, указанные в generic-ах, 
[превращаются в специальные обёртки](https://kotlinlang.org/docs/apple-framework.html#kotlin-numbers-and-nsnumber) 
над примитивными типами:

- `List<Byte>` -> `[KotlinByte]`
- `List<UByte>` -> `[KotlinUByte]`
- `List<Short>` -> `[KotlinShort]`
- `List<UShort>` -> `[KotlinUShort]`
- `List<Int>` -> `[KotlinInt]`
- `List<UInt>` -> `[KotlinUInt]`
- `List<Long>` -> `[KotlinLong]`
- `List<ULong>` -> `[KotlinULong]`
- `List<Float>` -> `[KotlinFloat]`
- `List<Double>` -> `[KotlinDouble]`
- `List<Boolean>` -> `[KotlinBoolean]`

И два исключения ([аналогично optional-ам](/docs/types/Optional%20(nullable)%20primitive%20types.md):

- `List<String>` -> `[String]`
- `List<Char>` -> `[Any]`

Чтобы передать Swift-типы (не литералы) в качестве аргументов в Kotlin-функции, придётся писать маппинги:

```swift
func collectionsExample(intList: [Int]) {
    let _: [KotlinInt] = types.intList(list: [1,2,3])					// ok
    let _: [KotlinInt] = [1, 2, 3] + types.listType(list: [1, 3, 4])	// ok
    
    // Маппинг
    let li2: [KotlinInt] = types.listType(
	    list: intList.map({ p in KotlinInt(value: p) })
	)
}
```

---
[Оглавление](/README.md)