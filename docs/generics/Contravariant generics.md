## Contravariant generics

| Статус          | Ожидание                                                                                                            | Реальность                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| :no_entry_sign: | При указании ключевого слова in на generic-е, сгенерируется generic со схожим поведением (контравариантный generic) | Не работает как ожидается, приходится использовать приведение типов |

### Пояснения

В Kotlin-е `in T` - это *контравариантный* generic.

```kotlin
open class SuperClass  
class Child : SuperClass()  
  
class InGenericItem<in T>
  
private fun example(example: InGenericItem<SuperClass>) {  
    val y: InGenericItem<Child> = example // без in - не скомпилируется
}
```

В objective-c `in` нам сгенерировал generiс с указанием на его contravariant:

```objective-c
__attribute__((objc_subclassing_restricted))
__attribute__((swift_name("InGenericItem")))
@interface HHMSInGenericItem<__contravariant T> : HHMSBase
- (instancetype)init __attribute__((swift_name("init()"))) __attribute__((objc_designated_initializer));
+ (instancetype)new __attribute__((availability(swift, unavailable, message="use object initializers instead")));
@end;
```

И по идее, аналогичный код в Swift должен работать:

```swift
open class SuperClass {}
class ChildClass : SuperClass {}

private func inGenericUsage(generic: InGenericItem<SuperClass>) {
	let _: InGenericItem<ChildClass> = generic
}
```

Но он не компилируется с ошибкой:

```
Cannot assign value of type 'InGenericItem<HHMobileSdkExperiment.SuperClass>' to type 'InGenericItem<HHMobileSdkExperiment.ChildClass>'
```

Через приведение типа - работает:

```swift
inGenericUsage(
	generic: InGenericItem<ChildClass>() as! InGenericItem<SuperClass>
)

private func inGenericUsage(generic: InGenericItem<SuperClass>) {
	let _: InGenericItem<ChildClass> = generic as! InGenericItem<ChildClass>
	print("inGenericUsage - ok")
}
```

---
[Оглавление](/README.md)