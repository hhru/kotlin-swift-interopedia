## Star projection

| Статус          | Ожидание                                                           | Реальность                                                          |
| --------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------- |
| :no_entry_sign: | Сгенерируется generic со схожим поведением (in Nothing / out Any?) | Не работает как ожидается, приходится использовать приведение типов |

### Пояснения

В Kotlin-е `Star projection` - совмещение концепций `in` и `out`:

```kotlin
class MyGeneric<T : Any>(val data: T) {  
    val state: T get() = data  
  
 	fun someStarProjection(myGeneric: MyGeneric<*>) {  
        println("myGeneric: ${myGeneric}")  
    }  
}

private fun myGenericExample() {  
    val myGeneric = MyGeneric(1)  
      
    myGeneric.someStarProjection(myGeneric)  
    myGeneric.someStarProjection(MyGeneric("11"))  
}
```

В Objective-C мы получаем вот такой заголовок:

```objective-c
__attribute__((objc_subclassing_restricted))
__attribute__((swift_name("MyGeneric")))
@interface HHMSMyGeneric<T> : HHMSBase
- (instancetype)initWithData:(T)data __attribute__((swift_name("init(data:)"))) __attribute__((objc_designated_initializer));
- (void)someStarProjectionMyGeneric:(HHMSMyGeneric<id> *)myGeneric __attribute__((swift_name("someStarProjection(myGeneric:)")));
@property (readonly) T data __attribute__((swift_name("data")));
@property (readonly) T state __attribute__((swift_name("state")));
@end;
```

На стороне Swift-а используем приведения типов:

```kotlin
private func starGenericProjecton() {
	let starProj = MyGeneric(data: NSNumber(12))

	starProj.someStarProjection(myGeneric: starProj as! MyGeneric<AnyObject>)
	starProj.someStarProjection(
		myGeneric: MyGeneric<AnyObject>(data: NSString("111"))
	)
}
```

---
[Оглавление](/README.md)