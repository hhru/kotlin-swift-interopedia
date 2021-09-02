## Annotation class

| Статус          | Ожидание                             | Реальность                    |
| --------------- | ------------------------------------ | ----------------------------- |
| :no_entry_sign: | Аннотации можно использовать в Swift | Аннотации не попали в .h-файл |

### Пояснения

Добавим аннотации в Kotlin-е:

```kotlin
@Target(AnnotationTarget.CLASS)
annotation class AnnotationClassExample

@Retention(AnnotationRetention.BINARY)
@Target(AnnotationTarget.CLASS)
annotation class BinaryClassExample

@Retention(AnnotationRetention.RUNTIME)
@Target(AnnotationTarget.CLASS)
annotation class RuntimeAnnotationClass

@Retention(AnnotationRetention.SOURCE)
@Target(AnnotationTarget.CLASS)
annotation class SourceAnnotationClass
```

Вне зависимости от указанных retention-ов, аннотации не попали в `.h`-файл, и их нельзя использовать в Swift.  

В Swift-е нет аннотаций в том смысле, в котором они присутствуют в Kotlin, но 
[есть атрибуты](https://docs.swift.org/swift-book/ReferenceManual/Attributes.html), которые используются для 
определённых целей.

---
[Оглавление](/README.md)