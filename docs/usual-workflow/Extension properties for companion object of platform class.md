## Extension properties for companion object of platform class

| Статус          | Ожидание                                                         | Реальность                                                       |
| --------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| :no_entry_sign: | Доступ к свойству можно получить с помощью платформенного класса | В .h-файле свойство есть, а в Swift-е не получается использовать |


### Пояснения

На стороне Kotlin-а объявили extension–свойство для companion object-а платформенного класса:

```kotlin
val String.Companion.MY_CONST_VAL: String get() = "123"
```

Из Swift-а не удаётся получить доступ к этому свойству. При этом в Objective-C `.h`-файла эту
константу видно:

```objective-c
@interface HHMSKotlinStringCompanion (Extensions)
@property (readonly) NSString *MY_CONST_VAL __attribute__((swift_name("MY_CONST_VAL")));
@end;
```

---
[Оглавление](/README.md)