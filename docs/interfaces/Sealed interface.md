## Sealed interface

| Статус          | Ожидание                                                        | Реальность                                                    |
| --------------- | --------------------------------------------------------------- | ------------------------------------------------------------- |
| :no_entry_sign: | При использовании в switch IDE поможет рассмотреть все варианты | Сгенерировались отдельные протоколы, не связанные между собой |

### Пояснения

Опишем sealed interface на стороне Kotlin-а, в выражении when есть автодополнение с рассмотрением всех вариантов:

```kotlin
sealed interface SealedInterfaceExample {

    interface First : SealedInterfaceExample {
        fun firstFunctionExample(): String
    }

    interface Second : SealedInterfaceExample {
        fun secondFunctionExample(): String
    }
}

private fun example(sie: SealedInterfaceExample) {
    when (sie) {
        is SealedInterfaceExample.First -> {
            sie.firstFunctionExample()
        }
        is SealedInterfaceExample.Second -> TODO()
    }
}
```

На стороне Swift-а сгенерировались отдельные протоколы, которые не наследуются друг от друга, 
это видно из `.h`-файла с Objective-C: 

```objective-c
__attribute__((swift_name("SealedInterfaceExample")))
@protocol HHMSSealedInterfaceExample
@required
@end;

__attribute__((swift_name("SealedInterfaceExampleFirst")))
@protocol HHMSSealedInterfaceExampleFirst <HHMSSealedInterfaceExample>
@required
- (NSString *)firstFunctionExample __attribute__((swift_name("firstFunctionExample()")));
@end;

__attribute__((swift_name("SealedInterfaceExampleSecond")))
@protocol HHMSSealedInterfaceExampleSecond <HHMSSealedInterfaceExample>
@required
- (NSString *)secondFunctionExample __attribute__((swift_name("secondFunctionExample()")));
@end;
```

Соответственно, при подстановке в выражение `switch` IDE не предлагает рассмотреть все варианты веток.
В Swift-е роль sealed-интерфейсов выполняют enum-ы, и можно было бы написать специальный bridge-код для конвертации
sealed-интерфейса в Swift-овый enum.

Плагин [moko-kwift](https://github.com/icerockdev/moko-kswift/) умеет генерировать такой маппинг
[с помощью фичи](https://github.com/icerockdev/moko-kswift/blob/master/kswift-gradle-plugin/src/main/kotlin/dev/icerock/moko/kswift/plugin/feature/SealedToSwiftEnumFeature.kt).

```kotlin
kswift {
    install(dev.icerock.moko.kswift.plugin.feature.SealedToSwiftEnumFeature)
}
```

Но есть некоторые особенности, см. [moko-kswift overview](/docs/moko-kswift/Overview.md)

---
[Оглавление](/README.md)