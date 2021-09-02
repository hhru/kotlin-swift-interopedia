## Generic interfaces

| Статус          | Ожидание                                                       | Реальность                                 |
| --------------- | -------------------------------------------------------------- | ------------------------------------------ |
| :no_entry_sign: | Можно реализовать протокол с generic-ом после перехода в Swift | Generic-и на интерфейсах не поддерживаются |

### Пояснения

Опишем интерфейс с generic-ом на Kotlin-е:

```kotlin
interface SocketConverter<T : Any> {  
    fun convert(element: String): T  
}
```

При интеропе информация о generic-е на этом интерфейсе теряется, это видно из `.h`-файла:

```objective-c
__attribute__((swift_name("SocketConverter")))
@protocol HHMSSocketConverter
@required
- (id)convertElement:(NSString *)element __attribute__((swift_name("convert(element:)")));
@end;
```

Но generic-и на интерфейсах [пока не поддерживаются](https://kotlinlang.org/docs/native-objc-interop.html#generics). 
В самом Swift-е создать протокол с generic-ом можно.

---
[Оглавление](/README.md)