## Covariant generics

| Статус          | Ожидание                                                                                                         | Реальность                                                          |
| --------------- | ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| :no_entry_sign: | При указании ключевого слова out на generic-е, сгенерируется generic со схожим поведением (ковариантный generic) | Не работает как ожидается, приходится использовать приведение типов |

### Пояснения

В Kotlin–е ключевое слово `out` определяет *ковариантный* generic, который может производить данные.

```kotlin
class OutGeneric<out T>(data: T) {  
    val myState = data  
    fun pullState(): T = myState  
}  
  
private fun example(param: OutGeneric<String>) {  
    val t: OutGeneric<Any> = param    // без out-а не компилируется  
}
```

В Objective-C есть указание на то, что generic - ковариантный:

```objective-c
__attribute__((objc_subclassing_restricted))
__attribute__((swift_name("OutGeneric")))
@interface HHMSOutGeneric<__covariant T> : HHMSBase
- (instancetype)initWithData:(T _Nullable)data __attribute__((swift_name("init(data:)"))) __attribute__((objc_designated_initializer));
- (T _Nullable)pullState __attribute__((swift_name("pullState()")));
@property (readonly) T _Nullable myState __attribute__((swift_name("myState")));
@end;
```

Но в Swift-е эта ковариантность теряется, приходится использовать приведение типов:

```swift
private func outGenericUsage(generic: OutGeneric<NSString>) {
	let _: OutGeneric<AnyObject> = generic as! OutGeneric<AnyObject>
}
```

---
[Оглавление](/README.md)