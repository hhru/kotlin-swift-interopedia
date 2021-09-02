# Kotlin-Swift interopedia
[![Maven Central](https://img.shields.io/maven-central/v/org.jetbrains.kotlin/kotlin-maven-plugin.svg)](https://search.maven.org/#search%7Cga%7C1%7Cg%3A%22org.jetbrains.kotlin%22)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Мы создали этот репозиторий, чтобы помочь разработчикам, интересующимся технологией KMM, понять, как будет выглядеть
описанное ими публичное API общего модуля.

В сети есть [подробная документация от JetBrains](https://kotlinlang.org/docs/native-objc-interop.html)   
про интероп между Kotlin и Swift, однако в ней не рассматриваются подробно все возможности языка Kotlin.

Поэтому мы свели в единую табличку перечень возможностей Kotlin-а и отметили, какими возможностями можно пользоваться
без каких-либо проблем, а с какими потребуются те или иные доработки.

## Таблица интеропа

Как пользоваться таблицей:

- Знак :white_check_mark: означает, что указанной фичой Kotlin-а можно спокойно пользоваться, она генерирует
  Swift-friendly код без необходимости доработок;
- Знак :warning: означает, что либо для работы фичи требуются какие-то доработки, либо есть несоответствие между
  ожидаемым и реальным поведением фичи, которое не сильно мешает разработке;
- Знак :no_entry_sign: означает, что фичой нельзя пользоваться, она генерирует не Swift-friendly код, она работает
  совсем не так как ожидается, и это может стать помехой в разработке.

<br/>

<table>
	<thead>
		<th>Фича Kotlin-а</th>
		<th>Ожидание</th>
		<th>Статус</th>
		<th>Комментарий</th>
	</thead>
	<tbody>
		<tr>
			<td colspan="4" align="center">Common</td>
		</tr>
		<tr>
			<td><a href="/docs/common/Internal%20modifier.md">Internal modifier</a></td>
			<td>Internal-функции и классы не видны в Swift</td>
			<td>:white_check_mark:</td>
			<td>Так и есть, с iOS-разработчиками придётся обсуждать только публичное API общего кода</td>
		</tr>
		<tr>
			<td><a href="/docs/common/JavaDoc%20comments.md">JavaDoc comments</a></td>
			<td>Комментарии видны в XCode</td>
			<td>:warning:</td>
			<td>Комментарии видны, если добавить специальный аргумент для компилятора</td>
		</tr>
		<tr>
			<td colspan="4" align="center">Data types</td>
		</tr>
		<tr>
			<td><a href="/docs/types/Primitive%20types.md">Primitive types</a></td>
			<td>Типы, объявленные в Kotlin, можно без изменений использовать в Swift</td>
			<td>:warning:</td>
			<td>Может требоваться маппинг для целочисленных типов данных / маппинги для Char-а</td>
		</tr>
		<tr>
			<td><a href="/docs/types/Optional%20(nullable)%20primitive%20types.md">Optional (nullable) primitive types</a></td>
			<td>Тип, объявленный как Nullable, является таковым и на стороне Swift / Пользоваться nullable-типами можно без изменений</td>
			<td>:warning:</td>
			<td>Для примитивных типов требуется маппинг в специальные optional-типы / особенности с Char?</td>
		</tr>
		<tr>
			<td><a href="/docs/types/Mutable,%20immutable%20collections.md">Mutable, immutable collections</a></td>
			<td>Сигнатуры List / MutableList / etc имеют значение в Swift-мире и тоже регулируют мутабельность ; Использование коллекций не отличается от Kotlin</td>
			<td>:warning:</td>
			<td>Для регулировки мутабельности используются ключевые слова let, var / Для мутабельных коллекций требуются дополнительные маппинги</td>
		</tr>
		<tr>
			<td><a href="/docs/types/Collections%20with%20primitive%20types.md">Collections with primitive types</a></td>
			<td>Коллекции с элементами примитивных типов не требуют дополнительных маппингов</td>
			<td>:warning:</td>
			<td>Маппинги не требуются только для String-типа</td>
		</tr>
		<tr>
			<td><a href="/docs/types/Collections%20with%20custom%20types%20data.md">Collections with custom types data</a></td>
			<td>Коллекции с элементами кастомных типов не требуют дополнительных маппингов</td>
			<td>:white_check_mark:</td>
			<td>Маппинги не требуются :thumbsup:</td>
		</tr>
		<tr>
			<td><a href="/docs/types/Unit%20and%20Nothing">Unit and Nothing</a></td>
			<td>Типы Unit и Nothing можно использовать так же, как в Kotlin: Unit как объект или void, Nothing - нельзя создать</td>
			<td>:white_check_mark:</td>
			<td>Реальность соответствует ожиданиям :thumbsup:</td>
		</tr>
		<tr>
			<td colspan="4" align="center">Usual workflow</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Top-level%20functions.md">Top-level functions</a></td>
			<td>Функцию можно использовать напрямую после импорта, аналогично Kotlin-у</td>
			<td>:warning:</td>
			<td>Появляется класс-обёртка: UtilityKt.topLevelFunction()</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Top-level%20val%20properties%20(readonly).md">Top-level val properties (readonly)</a></td>
			<td>Доступ к свойству можно получить напрямую после импорта, аналогично Kotlin-у / поле readonly</td>
			<td>:warning:</td>
			<td>Появляется класс-обёртка для доступа к свойству: UtilityKt.propertyVal</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Top-level%20var%20properties%20(mutable).md">Top-level var properties (mutable)</a></td>
			<td>Доступ к свойству можно получить напрямую после импорта, аналогично Kotlin-у / поле mutable</td>
			<td>:warning:</td>
			<td>Появляется класс-обёртка для доступа к свойству: UtilityKt.propertyVar</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Extension%20function%20over%20platform%20class.md">Extension function over platform class</a></td>
			<td>Функцию можно использовать на объекте платформенного класса</td>
			<td>:warning:</td>
			<td>Появляется класс-обёртка с методом, принимающим объект нужного класса</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Extension%20properties%20over%20platform%20class.md">Extension properties over platform class</a></td>
			<td>Доступ к свойству можно получить с помощью объекта платформенного класса</td>
			<td>:warning:</td>
			<td>Появляется класс-обёртка с методом, принимающим объект нужного класса</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Extension%20properties%20for%20companion%20object%20of%20platform%20class.md">Extension properties for companion object of platform class</a></td>
			<td>Доступ к свойству можно получить с помощью платформенного класса</td>
			<td>:no_entry_sign:</td>
			<td>В .h-файле свойство есть, а в Swift-е не получается использовать</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Extension%20function%20over%20usual%20class.md">Extension function over usual class</a></td>
			<td>Функцию можно использовать на объекте класса</td>
			<td>:white_check_mark:</td>
			<td>Реальность соответствует ожиданиям :thumbsup:</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Extension%20properties%20over%20usual%20class.md">Extension properties over usual class</a></td>
			<td>Доступ к свойству можно получить через объект класса</td>
			<td>:white_check_mark:</td>
			<td>Реальность соответствует ожиданиям :thumbsup:</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Extension%20properties%20for%20companion%20object%20of%20usual%20class.md">Extension properties for companion object of usual class</a></td>
			<td>Доступ к свойству можно получить через класс</td>
			<td>:warning:</td>
			<td>Доступ к свойству можно получить через объект companion</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Usual%20class%20constructor.md">Usual class constructor</a></td>
			<td>Работа с конструктором не отличается от Kotlin-а</td>
			<td>:white_check_mark:</td>
			<td>Реальность соответствует ожиданиям :thumbsup:</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Usual%20class%20val%20property%20(readonly).md">Usual class val property (readonly)</a></td>
			<td>Доступ к свойству есть из объекта класса / свойство readonly</td>
			<td>:white_check_mark:</td>
			<td>Реальность соответствует ожиданиям :thumbsup:</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Usual%20class%20var property%20(mutable).md">Usual class var property (mutable)</a></td>
			<td>Доступ к свойству есть из объекта класса / свойство mutable</td>
			<td>:white_check_mark:</td>
			<td>Реальность соответствует ожиданиям :thumbsup:</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Usual%20class%20functions.md">Usual class functions</a></td>
			<td>Работа с функциями, объявленными внутри класса, не отличается от Kotlin-а</td>
			<td>:white_check_mark:</td>
			<td>Реальность соответствует ожиданиям :thumbsup:</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Companion%20object.md">Companion object</a></td>
			<td>Доступ к свойствам и функциям, объявленным в companion object-е, аналогичен Kotlin-у</td>
			<td>:warning:</td>
			<td>Доступ есть через вспомогательный объект companion</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Objects.md">Objects</a></td>
			<td>Доступ к свойствам и функциям, объявленным в object-е, аналогичен Kotlin-у</td>
			<td>:warning:</td>
			<td>Доступ есть через вспомогательный объект shared</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Function%20with%20default%20arguments.md">Function with default arguments</a></td>
			<td>Работа с функциями, имеющими дефолтные аргументы, аналогична Kotlin-у</td>
			<td>:no_entry_sign:</td>
			<td>Всегда приходится указывать все аргументы функции</td>
		</tr>
		<tr>
			<td><a href="/docs/usual-workflow/Constructor%20with%20default%20arguments.md">Constructor with default arguments</a></td>
			<td>Работа с конструктором, имеющим дефолтные аргументы, аналогична Kotlin-у</td>
			<td>:no_entry_sign:</td>
			<td>Всегда приходится указывать все аргументы для конструктора</td>
		</tr>
		<tr>
			<td colspan="4" align="center">Classes</td>
		</tr>
		<tr>
			<td><a href="/docs/classes/Abstract%20class.md">Abstract class</a></td>
			<td>Можно отнаследоваться от абстрактного класса, IDE подсказывает какие методы надо переопределить</td>
			<td>:warning:</td>
			<td>В IDE нет подсказок о необходимости переопределить абстрактный метод</td>
		</tr>
		<tr>
			<td><a href="/docs/classes/Annotation%20class.md">Annotation class</a></td>
			<td>Аннотации можно использовать в Swift</td>
			<td>:no_entry_sign:</td>
			<td>Аннотации не попали в .h-файл</td>
		</tr>
		<tr>
			<td><a href="/docs/classes/Data%20class.md">Data class</a></td>
			<td>Data class-ы сохраняют свои свойства после перехода в Swift</td>
			<td>:warning:</td>
			<td>Не все возможности data class-ов сохраняются / есть особенности с copy</td>
		</tr>
		<tr>
			<td><a href="/docs/classes/Enum%20class.md">Enum class</a></td>
			<td>Kotlin-овский enum class превратится в enum Swift-а, и можно будет использовать switch</td>
			<td>:warning:</td>
			<td>Не работает как ожидается. Но сгенерировался объект со статическими элементами</td>
		</tr>
		<tr>
			<td><a href="/docs/classes/Inner%20class.md">Inner class</a></td>
			<td>Можно создать инстанс inner-класса / прямого доступа к родительским свойствам и функциям нет</td>
			<td>:warning:</td>
			<td>Небольшие отличия в синтаксисе создания</td>
		</tr>
		<tr>
			<td><a href="/docs/classes/Open%20class.md">Open class</a></td>
			<td>Можно наследоваться от open-класса / есть доступ к protected-полям / можно переопределять open-методы</td>
			<td>:white_check_mark:</td>
			<td>Можно переопределять и final-методы</td>
		</tr>
		<tr>
			<td><a href="/docs/classes/Sealed%20class.md">Sealed class</a></td>
			<td> Корректно конвертируется в структуру, которую можно передать в switch-конструкцию и сделать exhaustive</td>
			<td>:no_entry_sign:</td>
			<td>Генерируется класс с наследниками. Передав в switch нет подсказок об exhaustive</td>
		</tr>
		<tr>
			<td><a href="/docs/classes/Value%20class.md">Value class</a></td>
			<td>Класс попадёт в .h-файл, им можно будет пользоваться в Swift</td>
			<td>:no_entry_sign:</td>
			<td>Класс не попал в .h-файл, пользоваться нельзя</td>
		</tr>
		<tr>
			<td colspan="4" align="center">Interfaces</td>
		</tr>
		<tr>
			<td><a href="/docs/interfaces/Interface.md">Interface</a></td>
			<td>При реализации интерфейса, IDE подставит заглушки для всего</td>
			<td>:white_check_mark:</td>
			<td>Интерфейс стал @protocol-ом. Но почему-то val-свойство превратилось в var</td>
		</tr>
		<tr>
			<td><a href="/docs/interfaces/Sealed%20interface.md">Sealed interface</a></td>
			<td>При использовании в switch IDE поможет рассмотреть все варианты</td>
			<td>:no_entry_sign:</td>
			<td>Сгенерировались отдельные протоколы, не связанные между собой</td>
		</tr>
		<tr>
			<td><a href="/docs/interfaces/Fun%20interface.md">Fun interface</a></td>
			<td>С помощью такого протокола можно более простым синтаксисом описать лямбду</td>
			<td>:no_entry_sign:</td>
			<td>В Swift нельзя создать анонимный класс</td>
		</tr>
		<tr>
			<td colspan="4" align="center">Functions</td>
		</tr>
		<tr>
			<td><a href="/docs/functions/DSL.md">DSL</a></td>
			<td>Надеемся, что DSL в Kotlin-е превратится в DSL на Swift</td>
			<td>:warning:</td>
			<td>Сгенерировались функции с receiver-ами, выглядит не так удобно, как хотелось бы</td>
		</tr>
		<tr>
			<td><a href="/docs/functions/Function%20returns%20lambda.md">Function returns lambda</a></td>
			<td>Функция, вернувшая лямбду, работает без крашей; лямбду можно вызвать</td>
			<td>:white_check_mark:</td>
			<td>Реальность совпадает с ожиданием</td>
		</tr>
		<tr>
			<td><a href="/docs/functions/Function%20returns%20primitive%20type.md">Function returns primitive type</a></td>
			<td>Функция, возвращающая примитивный тип, работает без ошибок</td>
			<td>:white_check_mark:</td>
			<td>Реальность совпадает с ожиданием</td>
		</tr>
		<tr>
			<td><a href="/docs/functions/Function%20with%20extension%20function%20as%20args.md">Function with extension function as args</a></td>
			<td>Можно вызвать функцию так же, как в Kotlin</td>
			<td>:warning:</td>
			<td>Extension-функция превращается в лямбду с параметром</td>
		</tr>
		<tr>
			<td><a href="/docs/functions/Function%20with%20lambda%20arguments.md">Function with lambda arguments</a></td>
			<td>Функция, принимающая в аргументах одну или несколько лямбд, нормально конвертируется в Swift</td>
			<td>:white_check_mark:</td>
			<td>Реальность совпадает с ожиданием</td>
		</tr>
		<tr>
			<td><a href="/docs/functions/Function%20with%20no%20return%20type.md">Function with no return type</a></td>
			<td>Функции, которые ничего не возвращают, можно спокойно вызвать</td>
			<td>:white_check_mark:</td>
			<td>Реальность совпадает с ожиданием</td>
		</tr>
		<tr>
			<td><a href="/docs/functions/Function%20with%20value%20class%20parameter.md">Function with value class parameter</a></td>
			<td>Функция появится в .h-файле и её можно будет использовать, передавая value-класс</td>
			<td>:no_entry_sign:</td>
			<td>Функция появилась в .h-файле, но аргумент value-класса развернулся в примитивы</td>
		</tr>
		<tr>
			<td><a href="/docs/functions/Function%20with%20vararg%20parameter.md">Function with vararg parameter</a></td>
			<td>vararg смапился в Swift-овый variardic и используется аналогично</td>
			<td>:no_entry_sign:</td>
			<td>Не работает так, как ожидается</td>
		</tr>
		<tr>
			<td><a href="/docs/functions/Functions%20with%20overloads.md">Functions with overloads</a></td>
			<td>Использование перегруженных функций ничем не отличается от Kotlin-а</td>
			<td>:warning:</td>
			<td>Есть особенности при использовании одинаковых имён параметров</td>
		</tr>
		<tr>
			<td><a href="/docs/functions/Inline%20functions.md">Inline functions</a></td>
			<td>Инлайн-функции есть в .h-файле, их можно вызвать</td>
			<td>:white_check_mark:</td>
			<td>Реальность совпадает с ожиданием</td>
		</tr>
		<tr>
			<td><a href="/docs/functions/Suspend%20functions.md">Suspend functions</a></td>
			<td>Suspend-функции развернулись в удобную для Swift-конструкцию</td>
			<td>:warning:</td>
			<td>Транслируется в callback, экспериментально - в async / await. Но для использования в реактивных фреймворках требуются дополнительный bridge-код</td>
		</tr>
		<tr>
			<td colspan="4" align="center">Generics</td>
		</tr>
		<tr>
			<td><a href="/docs/generics/Generic%20classes.md">Generic classes</a></td>
			<td>Сгенерируется класс с generic-ом, пользоваться можно как в Kotlin</td>
			<td>:warning:</td>
			<td>Есть некоторые особенности использования типов</td>
		</tr>
		<tr>
			<td><a href="/docs/generics/Generic%20functions.md">Generic functions</a></td>
			<td>Обычная функция-generic позволяет принять аргумент любого типа</td>
			<td>:no_entry_sign:</td>
			<td>Нет автоматического вывода типа, особенности nullability</td>
		</tr>
		<tr>
			<td><a href="/docs/generics/Generic%20interfaces.md">Generic interfaces</a></td>
			<td>Можно реализовать протокол с generic-ом после перехода в Swift</td>
			<td>:no_entry_sign:</td>
			<td>Generic-и на интерфейсах не поддерживаются</td>
		</tr>
		<tr>
			<td><a href="/docs/generics/Bounded%20generics.md">Bounded generics</a></td>
			<td>Ограничение типа generic-а, объявленное в Kotlin, сработает и в Swift</td>
			<td>:no_entry_sign:</td>
			<td>Ограничение не сработало</td>
		</tr>
		<tr>
			<td><a href="/docs/generics/Contravariant%20generics.md">Contravariant generics</a></td>
			<td>При указании ключевого слова in на generic-е, сгенерируется generic со схожим поведением (контравариантный generic)</td>
			<td>:no_entry_sign:</td>
			<td>Не работает как ожидается, приходится использовать приведение типов</td>
		</tr>
		<tr>
			<td><a href="/docs/generics/Covariant%20generics.md">Covariant generics</a></td>
			<td>При указании ключевого слова out на generic-е, сгенерируется generic со схожим поведением (ковариантный generic)</td>
			<td>:no_entry_sign:</td>
			<td>Не работает как ожидается, приходится использовать приведение типов</td>
		</tr>
		<tr>
			<td><a href="/docs/generics/Star%20projection.md">Star projection</a></td>
			<td>Сгенерируется generic со схожим поведением (in Nothing / out Any?)</td>
			<td>:no_entry_sign:</td>
			<td>Не работает как ожидается, приходится использовать приведение типов</td>
		</tr>
		<tr>
			<td><a href="/docs/generics/Reified%20functions.md">Reified functions</a></td>
			<td>Функции с reified нормально вызываются из Swift + работают ожидаемым образом</td>
			<td>:no_entry_sign:</td>
			<td>В рантайме функция крашится</td>
		</tr>
	</tbody>
</table>

## Полезные ссылки
- Из документации Kotlin
    - [Документация: Что нового в Kotlin 1.5.30](https://kotlinlang.org/docs/whatsnew1530.html)
    - [Документация: интероп Swift <--> Kotlin](https://kotlinlang.org/docs/native-objc-interop.html).
    - [Документация: маппинг типов между C и Kotlin/Native](https://kotlinlang.org/docs/mapping-primitive-data-types-from-c.html)
    - [Документация: Туториал по использованию Ktor-а в multiplatorm](https://kotlinlang.org/docs/mobile/use-ktor-for-networking.html#set-up-an-http-client)
    - [Документация: Kotlin-идиомы](https://kotlinlang.org/docs/idioms.html)
    - [Документация: Concurrency в Kotlin/Native](https://kotlinlang.org/docs/mobile/concurrency-overview.html)
- [Документация Apple: Про completion handler-ы](https://developer.apple.com/documentation/swift/calling_objective-c_apis_asynchronously)
- [Документация Swift: про async / await](https://docs.swift.org/swift-book/LanguageGuide/Concurrency.html)
- [Доклад: Состояние интеропа в 2019 году (Некоторые вещи всё ещё актуальны)](https://www.youtube.com/watch?v=N1Xt-LuAR9A&ab_channel=JetBrainsTV)
- [Статья: Про Kotlin/Native generics в 2019 году (Всё ещё актуально)](https://medium.com/@kpgalligan/kotlin-native-interop-generics-15eda6f6050f)
- [Статья: Про построение более удобного кода на Swift при помощи gradle-плагина moko-kswift](https://habr.com/ru/post/571714/)
- [Статья: Построение DSL в Swift](https://habr.com/ru/company/tinkoff/blog/455760/).
- Серия статей про написание необходимых обёрток для взаимодействия между корутинами и RxSwift / Combine / OpenCombine
    - [Статья: Использование suspend в Swift - про неудобство с RxSwift](https://dev.to/touchlab/working-with-kotlin-coroutines-and-rxswift-24fa)
    - [Статья: Использование suspend в Swift в 2021 году](https://touchlab.co/kotlin-coroutines-swift-revisited/)
    - [Github: Пример работы корутин с RxSwift / Combine на основе статей от Touchlab](https://github.com/touchlab/SwiftCoroutines)
- Набор статей про Generic-и в Kotlin:
    - [Хорошая статья про ковариантность и контравариантность в Kotlin](https://typealias.com/guides/illustrated-guide-covariance-contravariance/)
    - [Хорошая статья про in и out в Kotlin](https://typealias.com/guides/ins-and-outs-of-generic-variance/)
    - [Хорошая статья про star projection](https://typealias.com/guides/star-projections-and-how-they-work/)
- [Github: Список DSL-библиотек на Swift](https://github.com/carson-katri/awesome-result-builders)
- [Плагин moko-kswift](https://github.com/icerockdev/moko-kswift/)