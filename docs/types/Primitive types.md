## Primitive types

| Статус      | Ожидание                                                             | Реальность                                                                     |
| ----------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| :warning:   | Типы, объявленные в Kotlin, можно без изменений использовать в Swift | Может требоваться маппинг для целочисленных типов данных / маппинги для Char-а |

### Пояснения

Опишем Kotlin-класс, использующий различные примитивные типы Kotlin-а:

```kotlin
class PrimitiveTypesClass {

    fun byteType(b: Byte): Byte {
        return b
    }

    fun shortType(s: Short): Short {
        return s
    }

    fun intType(i: Int): Int {
        return i
    }

    fun longType(l: Long): Long {
        return l
    }

    fun floatType(f: Float): Float {
        return f
    }

    fun doubleType(d: Double): Double {
        return d
    }

    fun stringType(s: String): String {
        return s
    }

    fun booleanType(b: Boolean): Boolean {
        return b
    }

}
```

#### Целочисленные типы данных (Byte / Short / Int / Long)

Целочисленные типы данных Kotlin-а конвертируются в Swift-типы следующим образом:

- `Byte` -> `Int8`
- `UByte` -> `UInt8`
- `Short` -> `Int16`
- `UShort` -> `UInt16`
- `Int` -> `Int32`
- `UInt` -> `UInt32`
- `Long` -> `Int64`
- `ULong` -> `UInt64`

Если использовать литералы или же аргументы указанных Swift-овых типов, дополнительных усилий не требуется:

```swift
func integerTypesExample(
    byteType: Int8,
    shortType: Int16,
    intType: Int32,
    longType: Int64
) {
    let types = PrimitiveTypesClass()
    
    let _: Int8 = types.byteType(b: 1)
    let _: Int8 = types.byteType(b: byteType)
    
    let _: Int16 = types.shortType(s: 1)
    let _: Int16 = types.shortType(s: shortType)
    
    let _: Int32 = types.intType(i: 1)
    let _: Int32 = types.intType(i: intType)
    
    let _: Int64 = types.longType(i: 1)
    let _: Int64 = types.longType(l: longType)
}
```

Если же нужно использовать Swift-овый тип `Int`, потребуются дополнительные маппинги:

```swift
func swiftIntTypeExample(swiftIntType: Int) {
    let types = PrimitiveTypesClass()
    
    let _: Int = Int( types.byteType(b: Int8(swiftIntType)) )
    let _: Int = Int( types.shortType(s: Int16(swiftIntType)) )
    let _: Int = Int( types.intType(i: Int32(swiftIntType)) )
    let _: Int = Int( types.longType(l: Int64(swiftIntType)) )
}
```

#### Вещественные типы данных (Float / Double)

Вещественные типы Kotlin-а конвертируются в соответствующие вещественные типы 
Swift-а (`Float` -> `Float`, `Double` -> `Double`), дополнительные маппинги не требуются:

```swift
func realTypesExample(
    floatType: Float,
    doubleType: Double
) {
    let types = PrimitiveTypesClass()
    
    let _: Float = types.floatType(f: 1.0)
    let _: Float = types.floatType(f: floatType)
    
    let _: Double = types.doubleType(d: 1.0)
    let _: Double = types.doubleType(d: doubleType)
}
```

#### Символьный тип данных (Char)

Тип `Char` на стороне Swift-а конвертируется в тип `unichar`, с которым не очень удобно работать:

```swift
func charTypeExample(
    unicharType: unichar,
    stringType: String
) {
    let types = PrimitiveTypesClass()
    
    let _: unichar = types.charType(c:  ("a" as NSString).character(at: 0))
    let _: unichar = types.charType(c: unicharType)
    let _: unichar = types.charType(c: (stringType as NSString).character(at: 0))
}
```

#### Строки (String)

С типом данных `String` нет проблем, он конвертируется в Swift-овый тип `String` без дополнительных маппингов:

```swift
func stringTypeExample(stringType: String) {
    let types = PrimitiveTypesClass()
    
    let _: String = types.stringType(s: "123")
    
    let _: String = types.stringType(s: stringType)
}
```

#### Логический тип данных (Boolean)

С `Boolean`-ом нет проблем, он конвертируется в Swift-овый тип `Bool` без дополнительных маппингов:

```swift
func boolTypeExample(boolType: Bool) {
    let types = PrimitiveTypesClass()
    
    let _: Bool = types.booleanType(b: true)
    let _: Bool = types.booleanType(b: false)
    
    let _: Bool = types.booleanType(b: boolType)
}
```

---
[Оглавление](/README.md)