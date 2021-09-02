## Companion object 

| Статус    | Ожидание                                                                             | Реальность                                         |
| --------- | ------------------------------------------------------------------------------------ | -------------------------------------------------- |
| :warning: | Доступ к свойствам и функциям, объявленным в companion object-е, аналогичен Kotlin-у | Доступ есть через вспомогательный объект companion |

### Пояснения

В Kotlin-е работа с companion object-ом напоминает работу со статическими методами и константами в Java. То есть:

```kotlin
class MyClass {
	companion object {
		const val CONST_VAL_EXAMPLE = "123"
	}
}

fun usage() {
	printn(MyClass.CONST_VAL_EXAMPLE)
}
```

В Swift-е для доступа к внутренностям companion [появляется объект `companion`](https://kotlinlang.org/docs/whatsnew1530.html#improved-swift-objective-c-mapping-for-objects-and-companion-objects), 
к которому можно получить доступ через класс:

```kotlin
func usage() {
	MyClass.companion.CONST_VAL_EXAMPLE
}
```

---
[Оглавление](/README.md)