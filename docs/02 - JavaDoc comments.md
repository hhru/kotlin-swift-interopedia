## JavaDoc comments

| Статус фичи | Ожидание                  | Реальность                                                            |
| ----------- | ------------------------- | --------------------------------------------------------------------- |
| :warning:   | Комментарии видны в XCode | Комментарии видны, если добавить специальный аргумент для компилятора |

[С Kotlin 1.5.20 есть возможность пробрасывать JavaDoc комментарии](https://kotlinlang.org/docs/whatsnew1520.html#opt-in-export-of-kdoc-comments-to-generated-objective-c-headers).
Для этого нужно включить генерацию комментариев в настройке multiplatform-модуля:

```kotlin
kotlin {

    targets.withType<org.jetbrains.kotlin.gradle.plugin.mpp.KotlinNativeTarget> { 
        // Для включения документации  
        compilations["main"].kotlinOptions.freeCompilerArgs += "-Xexport-kdoc"  
    }

}
```

После этого на стороне XCode-а в автодополнениях можно видеть комментарии к классу и методам. 
Если переходить к определению функций (в `.h`-файл), то можно увидеть комментарии к @param / @return и т.д.

---
[01 - Internal modifier](/docs/01%20-%20Internal%20modifier.md) | [Оглавление](/README.md) | [03 - Top-level properties, functions](/docs/03%20-%20Top-level%20properties,%20functions.md)
