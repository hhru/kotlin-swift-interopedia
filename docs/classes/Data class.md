## Data class

| Статус    | Ожидание                                                    | Реальность                                                             |
| --------- | ----------------------------------------------------------- | ---------------------------------------------------------------------- |
| :warning: | Data class-ы сохраняют свои свойства после перехода в Swift | Не все возможности data class-ов сохраняются / есть особенности с copy |

### Пояснения

Опишем обычный data class в Kotlin-е:

```kotlin
data class DataClassExample(
    val param1: String,
    val param2: Int,
    val param3: Boolean
)
```

#### Метод `copy`

Метод `copy` переносится в Swift с названием `doCopy`, работает аналогично методу в Kotlin, но
есть неудобство [с необходимостью указывать все аргументы функции](/docs/usual-workflow/Function%20with%20default%20arguments.md).

#### Метод `equals`

Сравнение двух экземпляров data class-а работает аналогично Kotlin-у, включая сравнение коллекций.

#### Метод `toString`

При использовании объекта data class-а в строчке вывод такой же, как в Kotlin:

```swift
let dc = DataClassExample(param1: "123", param2: 10, param3: true)
print("dc = \(dc)")
```

#### Destructuring

Эта фича Kotlin-а не работает. Но функции `component1()`, `component2`, ... `componentN()` доступны, 
и при желании можно описать свой метод для деструктуризации:

```swift
extension DataClassExample {
    func destruct() -> (String, Int32, Bool) {
        return (component1(), component2(), component3())
    }
}

func example() {
    val (param1, param2, param3) = DataClassExample("", 100, true).destruct()
}
```

---
[Оглавление](/README.md)