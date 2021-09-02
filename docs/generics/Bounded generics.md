## Bounded generics

| Статус          | Ожидание                                                              | Реальность               |
| --------------- | --------------------------------------------------------------------- | ------------------------ |
| :no_entry_sign: | Ограничение типа generic-а, объявленное в Kotlin, сработает и в Swift | Ограничение не сработало |

### Пояснения

Опишем ограниченный определённым классом generic-класс в Kotlin-е:

```kotlin
open class ForStricted  
  
class ChildStricted : ForStricted()  
  
  
class StrictedGeneric<T : ForStricted>(val data: T) {  
    fun fetch(): T {  
        return data  
 	}  
}  
  
private fun example() {  
    val s1 = StrictedGeneric(ForStricted())  
    val s2 = StrictedGeneric(ChildStricted())  
	
	// val s3 = StrictedGeneric("123") // не компилируется
}
```

В Objective-C `.h`-файле нет информации об ограничении generic-а:

```objectivec
__attribute__((objc_subclassing_restricted))
__attribute__((swift_name("StrictedGeneric")))
@interface HHMSStrictedGeneric<T> : HHMSBase
- (instancetype)initWithData:(T)data __attribute__((swift_name("init(data:)"))) __attribute__((objc_designated_initializer));
- (T)fetch __attribute__((swift_name("fetch()")));
@property (readonly) T data __attribute__((swift_name("data")));
@end;
```

Поэтому в Swift-е мы можем скомпилировать и вот такой код:

```swift
private func boundedGeneric() {
	class MyStricted : ForStricted {}

	let _ = StrictedGeneric(data: MyStricted())
	let _ = StrictedGeneric(data: NSString("1122")) // компилируется.
}
```

---
[Оглавление](/README.md)