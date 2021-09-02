## Suspend functions

| Статус             | Ожидание                                                     | Реальность                                                                                                                                      |
| ------------------ | ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| :white_check_mark: | Suspend-функции развернулись в удобную для Swift-конструкцию | Транслируется в callback, экспериментально - в async / await. Но для использования в реактивных фреймворках требуются дополнительный bridge-код |

### Пояснения

Опишем класс, использующий suspend-функции Kotlin-а:

```kotlin
data class Thing(val item: Int)

class ThingRepository {

    suspend fun getThing(succeed: Boolean): Thing {
        delay(100)
        if (succeed) {
            return Thing(0)
        } else {
            error("oh no!")
        }
    }

}
```

На стороне Swift-а suspend-функция [превращается в completion handler](https://kotlinlang.org/docs/native-objc-interop.html#suspending-functions).

```swift
// suspend function
ThingRepository().getThing(succeed: true, completionHandler: { thing, error in
    // do something
})
```

С Kotlin 1.5.30 [появилась экспериментальная возможность мапить suspend-функции в вид async/await](https://kotlinlang.org/docs/whatsnew1530.html#experimental-interoperability-with-swift-5-5-async-await). 
Но, вероятно, iOS-команда не будет использовать эту фичу в ближайшее время, 
потому что она будет нормально доступна только с iOS 15.

Про маппинг suspend-функций для реактивных фреймворков можно почитать серию статей:

- [Статья: Использование suspend в Swift - про неудобство с RxSwift](https://dev.to/touchlab/working-with-kotlin-coroutines-and-rxswift-24fa)
- [Статья: Использование suspend в Swift в 2021 году](https://touchlab.co/kotlin-coroutines-swift-revisited/)
- [Github: Пример работы корутин с RxSwift / Combine на основе статей от Touchlab](https://github.com/touchlab/SwiftCoroutines)

---
[Оглавление](/README.md)