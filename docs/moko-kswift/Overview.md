## moko-kswift overview

[moko-kswift](https://github.com/icerockdev/moko-kswift) - Gradle-плагин, разработанный 
командой [IceRock](https://icerockdev.com/), для генерации Swift-friendly кода для Kotlin/Native.

### Проверка работы плагина

| Фича Kotlin-а                          | Ожидание                                            | Статус             | Комментарий                                                    |
| -------------------------------------- | --------------------------------------------------- | ------------------ | -------------------------------------------------------------- |
| sealed-класс                           | Сгенерируется bridge-код для перевода класса в enum | :white_check_mark: | Всё ок :thumbsup:                                              |
| sealed-класс с глубокой иерархией      | Сгенерируется bridge-код для перевода в один enum   | :warning:          | Генерируется по enum-у для каждого sealed-класса вместо одного |
| sealed-интерфейс                       | Сгенерируется bridge-код для перевода в enum        | :white_check_mark: | Всё ок (y)                                                     |
| extension function over platform class | Сгенерируется extension на стороне Swift-а          | :warning:          | Платформенные классы - это классы из пакета `platform.*`       |

#### Sealed class with deep hierarchy

Допустим, была вот такая иерархия классов:

```kotlin
sealed class SealedWithDeepHierarchy {  
  
    abstract val param: String  
  
    sealed class LocalTrigger : SealedWithDeepHierarchy() {  
        object First : LocalTrigger() {  
            override val param: String = "first"  
 		}  
    }  
  
    sealed class RemoteTrigger : SealedWithDeepHierarchy() {  
        class Second(override val param: String) : RemoteTrigger()  
        data class Third(override val param: String) : RemoteTrigger()  
    }  
  
}
```

На стороне Kotlin-а такие классы очень удобно разворачивать внутри when-выражения:

```kotlin
private fun example(s: SealedWithDeepHierarchy) {  
    when (s) {  
        SealedWithDeepHierarchy.LocalTrigger.First -> TODO()  
        is SealedWithDeepHierarchy.RemoteTrigger.Second -> TODO()  
        is SealedWithDeepHierarchy.RemoteTrigger.Third -> TODO()  
    }  
}
```

С moko-swift сгенерировался вот такой swift-код:

```swift
public enum SealedWithDeepHierarchyLocalTriggerKs {  
  
  case first  
  
  public init(_ obj: SealedWithDeepHierarchy.LocalTrigger) {  
    if obj is HHMobileSdk.SealedWithDeepHierarchy.LocalTriggerFirst {  
      self = .first  
    } else {  
      fatalError("SealedWithDeepHierarchyLocalTriggerKs not syncronized with SealedWithDeepHierarchy.LocalTrigger class")  
    }  
  }  
  
}  
  
public enum SealedWithDeepHierarchyRemoteTriggerKs {  
  
  case second(SealedWithDeepHierarchy.RemoteTriggerSecond)  
  case third(SealedWithDeepHierarchy.RemoteTriggerThird)  
  
  public init(_ obj: SealedWithDeepHierarchy.RemoteTrigger) {  
    if let obj = obj as? HHMobileSdk.SealedWithDeepHierarchy.RemoteTriggerSecond {  
      self = .second(obj)  
    } else if let obj = obj as? HHMobileSdk.SealedWithDeepHierarchy.RemoteTriggerThird {  
      self = .third(obj)  
    } else {  
      fatalError("SealedWithDeepHierarchyRemoteTriggerKs not syncronized with SealedWithDeepHierarchy.RemoteTrigger class")  
    }  
  }  
  
}  
  
public enum SealedWithDeepHierarchyKs {  
  
  case localTrigger(SealedWithDeepHierarchy.LocalTrigger)  
  case remoteTrigger(SealedWithDeepHierarchy.RemoteTrigger)  
  
  public init(_ obj: SealedWithDeepHierarchy) {  
    if let obj = obj as? HHMobileSdk.SealedWithDeepHierarchy.LocalTrigger {  
      self = .localTrigger(obj)  
    } else if let obj = obj as? HHMobileSdk.SealedWithDeepHierarchy.RemoteTrigger {  
      self = .remoteTrigger(obj)  
    } else {  
      fatalError("SealedWithDeepHierarchyKs not syncronized with SealedWithDeepHierarchy class")  
    }  
  }  
  
}
```

И соответственно, использовать это можно вот так:

```swift
func mokoKswiftUsage(c: SealedWithDeepHierarchy) {
        switch SealedWithDeepHierarchyKs(c) {
        
        case let .localTrigger(tr):
            switch SealedWithDeepHierarchyLocalTriggerKs(tr) {
            case .first:
                <#code#>
            }
            
            
        case let .remoteTrigger(tr):
            switch SealedWithDeepHierarchyRemoteTriggerKs(tr) {
            case .second(_):
                <#code#>
            case .third(_):
                <#code#>
            }
        }
    }
```

Для большего удобства хорошо бы иметь единый enum.

#### Extension function over platform class
Ожидал, что это сработает для любого платформенного класса. 
Мы считаем платформенными классами любые классы типов (String / Int / Boolean / etc) + какие-то специфичные платформенные 
(тот же `platform.UIKit.UILabel` для iOS). 

Но оказалось, что учитываются только платформенные, у которых в package name-е 3 части, 
[первая из которых равна `platform`](https://github.com/icerockdev/moko-kswift/blob/master/kswift-gradle-plugin/src/main/kotlin/dev/icerock/moko/kswift/plugin/feature/PlatformExtensionFunctionsFeature.kt#L89-L110).

Поэтому для `fun String.myExtensionFunction()` маппинг не сработал.
