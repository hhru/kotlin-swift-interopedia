## Optional (nullable) primitive types

| Статус    | Ожидание                                                                                                              | Реальность                                                                                |
| --------- | --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| :warning: | Тип, объявленный как Nullable, является таковым и на стороне Swift / Пользоваться nullable-типами можно без изменений | Для примитивных типов требуется маппинг в специальные optional-типы / особенности с Char? |

### Пояснения

Напишем код, использующий nullable-типы в Kotlin-е:

```kotlin
class NullableExample(
    val optionalByte: Byte?,
    val optionalShort: Short?,
    val optionalInt: Int?,
    val optionalLong: Long?,
    val optionalFloat: Float?,
    val optionalDouble: Double?,
    val optionalString: String?,
    val optionalBoolean: Boolean?
) {

    fun optionalByteType(b: Byte?): Byte? {
        return b
    }

    fun optionalShortType(s: Short?): Short? {
        return s
    }

    fun optionalIntType(i: Int?): Int? {
        return i
    }

    fun optionalLongType(l: Long?): Long? {
        return l
    }

    fun optionalCharType(c: Char?): Char? {
        return c
    }

    fun optionalStringType(s: String?): String? {
        return s
    }

    fun optionalBooleanType(b: Boolean?): Boolean? {
        return b
    }

    fun optionalCustomClassType(customClass: OptionalDataHolder?): OptionalDataHolder? {
        return customClass
    }
    
}
```

На стороне Swift-а nullable-типы Kotlin-а (за исключением `String?` и `Char?`) 
представлены [специальными типами данных](https://kotlinlang.org/docs/apple-framework.html#kotlin-numbers-and-nsnumber):

- `Byte?` -> `KotlinByte?`
- `UByte?` -> `KotlinUByte?`
- `Short?` -> `KotlinShort?`
- `UShort?` -> `KotlinUShort?`
- `Int?` -> `KotlinInt?`
- `UInt?` -> `KotlinUInt?`
- `Long?` -> `KotlinLong?`
- `ULong?` -> `KotlinULong?`
- `Float?` -> `KotlinFloat?`
- `Double?` -> `KotlinDouble?`
- `Boolean?` -> `KotlinBoolean?`

И есть два отдельных кейса с `String?` и `Char?`:

- `String?` -> `String?`
- `Char?` -> `Any?`

#### Использование литералов и nil-значений

При передаче в аргументах литералов или nil-значений использование этих типов не отличается от Kotlin-а:

```swift
func optionalTypesExample3() {
    let _ = OptionalParamsConstructorClass(
        optionalByte: 1,
        optionalShort: 1,
        optionalInt: 1,
        optionalLong: 1,
        optionalFloat: 1.0,
        optionalDouble: 1.0,
        optionalParam: "123",
        optionalBoolean: true
    )
}
```

Так как `Char?` превратился в `Any?`, можно передать в качестве значения всё что угодно, 
и это НЕ сломает программу.

#### Использование not-null Swift-типов

При использовании Swift-овых типов данных требуется дополнительный маппинг:

```swift
func optionalTypesExample2(
    byteType: Int8,
    shortType: Int16,
    intType: Int32,
    longType: Int64,
    floatType: Float,
    doubleType: Double,
    stringType: String,
    booleanType: Bool
) {
    let _ = OptionalParamsConstructorClass(
        optionalByte: KotlinByte(value: byteType),
        optionalShort: KotlinShort(value: shortType),
        optionalInt: KotlinInt(value: intType),
        optionalLong: KotlinLong(value: longType),
        optionalFloat: KotlinFloat(value: floatType),
        optionalDouble: KotlinDouble(value: doubleType),
        optionalParam: stringType,
        optionalBoolean: KotlinBoolean(value: booleanType)
    )
}
```

#### Использование optional Swift-типов

При использовании optional-типов Swift-а маппинг становится более громоздким за счёт проверки на nil:

```swift
func optionalTypesExample(
    optionalByte: Int8?,
    optionalShort: Int16?,
    optionalInt: Int32?,
    optionalLong: Int64?,
    optionalFloat: Float?,
    optionalDouble: Double?,
    optionalString: String?,
    optionalBoolean: Bool?
) {
    let _ = OptionalParamsConstructorClass(
        optionalByte: (optionalByte != nil) ? KotlinByte(value: optionalByte!) : nil,
        optionalShort: (optionalShort != nil) ? KotlinShort(value: optionalShort!) : nil,
        optionalInt: (optionalInt != nil) ? KotlinInt(value: optionalInt!) : nil,
        optionalLong: (optionalLong != nil) ? KotlinLong(value: optionalLong!) : nil,
        optionalFloat: (optionalFloat != nil) ? KotlinFloat(value: optionalFloat!) : nil,
        optionalDouble: (optionalDouble != nil) ? KotlinDouble(value: optionalDouble!) : nil,
        optionalString: optionalString,
        optionalBoolean: (optionalBoolean != nil) ? KotlinBoolean(value: optionalBoolean!) : nil,
    )
}
```

---
[Оглавление](/README.md)