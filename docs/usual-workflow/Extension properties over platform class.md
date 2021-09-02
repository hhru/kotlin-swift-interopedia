## Extension properties over platform class

| Статус    | Ожидание                                                                 | Реальность                                                            |
| --------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------- |
| :warning: | Доступ к свойству можно получить с помощью объекта платформенного класса | Появляется класс-обёртка с методом, принимающим объект нужного класса |

### Пояснения

Платформенный класс - это, например, какой-то примитивный тип, или же класс, специфичный
для определённой платформы (`Bundle` для Android, `UILabel` для iOS, etc.).

В Kotlin-е нет разницы в использовании extension-а над обычным или платформенным классом:

```kotlin
// StringExt.kt

val String.myExtensionProperty: String get() = "123"

private fun example() {
    val result = "123".myExtensionProperty
}
```

После перехода в Swift разница проявляется в появлении класса-обёртки для вызова функции, 
совпадающей по имени с именем свойства:

```swift
func example() {
    let _ = StringExtKt.myExtensionProperty(receiver: "123")
}
```

Плагин [moko-kswift](https://github.com/icerockdev/moko-kswift) умеет решать эту проблему 
с помощью [фичи](https://github.com/icerockdev/moko-kswift/blob/master/kswift-gradle-plugin/src/main/kotlin/dev/icerock/moko/kswift/plugin/feature/PlatformExtensionFunctionsFeature.kt):

```kotlin
kswift {
	install(
		dev.icerock.moko.kswift.plugin.feature.PlatformExtensionFunctionsFeature
	)
}
```

Но есть некоторые особенности, см. [moko-kswift overview](/docs/moko-kswift/Overview.md)

---
[Оглавление](/README.md)