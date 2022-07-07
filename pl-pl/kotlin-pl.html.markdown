---
language: kotlin
contributors:
    - ["S Webber", "https://github.com/s-webber"]
filename: LearnKotlin.kt
translators:
    - ["Kamil Kołodziej", "https://github.com/spacenough"]
lang: pl-pl
---

Kotlin to statycznie typowany jezyk programowania dzialajacy na JVM, Android i przegladarce. Jest w 100% interoperacyjny z Java.
[Przeczytaj wiecej.](https://kotlinlang.org/)

```kotlin
// Pojedyncze komentarze zaznaczamy znakami //
/*
Tak wygląda komentarz wielolinijkowy.
*/

// Słowo "package" działa na takiej samej zasadzie jak w Javie.
package com.learnxinyminutes.kotlin

/*
Startowym punktem programu jest funkcja o nazwie "main".
Funkcji przekazywana jest tablica zawierająca wszelkie argumenty wiersza poleceń.
Wraz z Kotlin 1.3 funkcja "main" moze byc wykonana bez parametrow.
*/
fun main(args: Array<String>) {
    /*
    Zmienna deklarujemy za pomoca słów kluczowych "var" lub "val".
    Zmienna z nazwa "val" nie moze zostac nigdzie nadpisana, natomiast "vars" moze.
    */
    val fooVal = 10 // Nie mozemy zamienic później wartosci fooVal na inna.
    var fooVar = 10
    fooVar = 20 // fooVar może byc nadpisana (możemy zmienic jej wartosc w późniejszym etapie programu)

    /*
    Możemy zauważyć, że Kotlin sam domyśla sie jakiego typu ma byc nasza zmienna
   , dzieki temu nie ma potrzeby deklarować jej typu za każdym razem.
    Co prawda możemy wykonac robote za kotlina, ale nie jest to wymagane:
    */
    val foo: Int = 7

    /*
    Wartosci typu string maja takie wlasciwosci jak w Javie.
    */
    val fooString = "My String Is Here!"
    val barString = "Printing on a new line?\nNo Problem!"
    val bazString = "Do you want to add a tab?\tNo Problem!"
    println(fooString)
    println(barString)
    println(bazString)

    /*
   	Pusty (surowy) string przypisujemy za pomocą (""").
    Puste stringi moga zawierac nowa linie (\n) itp.
    */
    val fooRawString = """
fun helloWorld(val name : String) {
   println("Hello, world!")
}
"""
    println(fooRawString)

    /*
    Stringi mogą zawierać szablonowe wyrażenia.
    Wyrażenie szablonu zaczyna się od znaku dolara ($).
    */
    val fooTemplateString = "$fooString has ${fooString.length} characters"
    println(fooTemplateString) // => My String Is Here! has 18 characters

    /*
    Aby zmienna miała wartość null musi być jawnie określona jako nullable.
    Zmienna może być określona jako nullable poprzez dodanie ? do jej typu.
    Dostęp do zmiennej nullable możemy uzyskać za pomocą operatora ?.
    Możemy użyć operatora ?: aby określić alternatywną wartość do użycia
    jeśli zmienna ma wartość null.
    */
    var fooNullable: String? = "abc"
    println(fooNullable?.length) // => 3
    println(fooNullable?.length ?: -1) // => 3
    fooNullable = null
    println(fooNullable?.length) // => null
    println(fooNullable?.length ?: -1) // => -1

    /*
    Funkcje można deklarować za pomocą słowa kluczowego "fun".
    Argumenty funkcji podawane są w nawiasach po nazwie funkcji.
    Argumenty funkcji mogą opcjonalnie mieć wartość domyślną.
    Slowo kluczowe return, jeśli jest wymagane, jest określane po argumentach.
    */
    fun hello(name: String = "world"): String {
        return "Hello, $name!"
    }
    println(hello("foo")) // => Hello, foo!
    println(hello(name = "bar")) // => Hello, bar!
    println(hello()) // => Hello, world!

    /*
    Parametr funkcji może być oznaczony słowem kluczowym "vararg"
    aby umożliwić przekazanie zmiennej liczby argumentów do funkcji.
    */
    fun varargExample(vararg names: Int) {
        println("Argument has ${names.size} elements")
    }
    varargExample() // => Argument has 0 elements
    varargExample(1) // => Argument has 1 elements
    varargExample(1, 2, 3) // => Argument has 3 elements

    /*
    Gdy funkcja składa się z pojedynczego wyrażenia, wówczas nawiasy klamrowe można
    pominąć. Ciało funkcji jest określane po symbolu =.
    */
    fun odd(x: Int): Boolean = x % 2 == 1
    println(odd(6)) // => false
    println(odd(7)) // => true

    // Jeśli typ zwrotu może być wywnioskowany to nie musimy go określać.
    fun even(x: Int) = x % 2 == 0
    println(even(6)) // => true
    println(even(7)) // => false

    // Funkcje mogą przyjmować funkcje jako argumenty i zwracać funkcje.
    fun not(f: (Int) -> Boolean): (Int) -> Boolean {
        return {n -> !f.invoke(n)}
    }
    // Funkcje nazwane mogą być określone jako argumenty za pomocą operatora ::.
    val notOdd = not(::odd)
    val notEven = not(::even)
    // Wyrażenia lambda mogą być określone jako argumenty.
    val notZero = not {n -> n == 0}
    /*
    Jeśli lambda ma tylko jeden parametr
    to jego deklaracja może zostać pominięta (wraz z ->).
    Nazwą pojedynczego parametru będzie "it".
    */
    val notPositive = not {it > 0}
    for (i in 0..4) {
        println("${notOdd(i)} ${notEven(i)} ${notZero(i)} ${notPositive(i)}")
    }

    // Słowo kluczowe "class" służy do deklarowania klas.
    class ExampleClass(val x: Int) {
        fun memberFunction(y: Int): Int {
            return x + y
        }

        infix fun infixMemberFunction(y: Int): Int {
            return x * y
        }
    }
    /*
    Aby stworzyć nową instancję wywołujemy konstruktor.
    Zauważ, że Kotlin nie posiada słowa kluczowego "new".
    */
    val fooExampleClass = ExampleClass(7)
    // Funkcje członkowskie mogą być wywoływane przy użyciu notacji kropkowej.
    println(fooExampleClass.memberFunction(4)) // => 11
    /*
    Jeśli funkcja została oznaczona słowem kluczowym "infix", to można ją wywołać używając notacji infiksowej.
    wywoływana przy użyciu notacji infiksowej.
    */
    println(fooExampleClass infixMemberFunction 4) // => 28

    /*
    Klasy danych są zwięzłym sposobem tworzenia klas, które po prostu przechowują dane.
    Metody "hashCode"/"equals" i "toString" są generowane automatycznie.
    */
    data class DataClassExample (val x: Int, val y: Int, val z: Int)
    val fooData = DataClassExample(1, 2, 4)
    println(fooData) // => DataClassExample(x=1, y=2, z=4)

    // Klasy danych posiadają funkcję "copy".
    val fooCopy = fooData.copy(y = 100)
    println(fooCopy) // => DataClassExample(x=1, y=100, z=4)

    // Obiekty mogą być destrukturyzowane na wiele zmiennych.
    val (a, b, c) = fooCopy
    println("$a $b $c") // => 1 100 4

    // destrukturyzacja w pętli "for"
    for ((a, b, c) in listOf(fooData)) {
        println("$a $b $c") // => 1 2 4
    }

    val mapData = mapOf("a" to 1, "b" to 2)
    // Map.Entry jest również zniszczalna
    for ((key, value) in mapData) {
        println("$key -> $value")
    }

    // Funkcja "with" jest podobna do instrukcji JavaScript "with".
    data class MutableDataClassExample (var x: Int, var y: Int, var z: Int)
    val fooMutableData = MutableDataClassExample(7, 4, 9)
    with (fooMutableData) {
        x -= 2
        y += 2
        z--
    }
    println(fooMutableData) // => MutableDataClassExample(x=5, y=6, z=8)

    /*
    Listę możemy stworzyć za pomocą funkcji "listOf".
    Lista będzie niezmienna - elementy nie mogą być dodawane ani usuwane.
    */
    val fooList = listOf("a", "b", "c")
    println(fooList.size) // => 3
    println(fooList.first()) // => a
    println(fooList.last()) // => c
    // Elementy listy mogą być dostępne przez ich indeks.
    println(fooList[1]) // => b

    // Zmienną listę można utworzyć za pomocą funkcji "mutableListOf".
    val fooMutableList = mutableListOf("a", "b", "c")
    fooMutableList.add("d")
    println(fooMutableList.last()) // => d
    println(fooMutableList.size) // => 4

    // Zbiór możemy stworzyć za pomocą funkcji "setOf".
    val fooSet = setOf("a", "b", "c")
    println(fooSet.contains("a")) // => true
    println(fooSet.contains("z")) // => false

    // Mapę możemy stworzyć za pomocą funkcji "mapOf".
    val fooMap = mapOf("a" to 8, "b" to 7, "c" to 9)
    // Map values can be accessed by their key.
    println(fooMap["a"]) // => 8

    /*
    Sekwencje reprezentują leniwie oceniane kolekcje.
    Sekwencję możemy stworzyć za pomocą funkcji "generateSequence".
    */
    val fooSequence = generateSequence(1, { it + 1 })
    val x = fooSequence.take(10).toList()
    println(x) // => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

    // Przykład wykorzystania ciągu do generowania liczb Fibonacciego:
    fun fibonacciSequence(): Sequence<Long> {
        var a = 0L
        var b = 1L

        fun next(): Long {
            val result = a + b
            a = b
            b = result
            return a
        }

        return generateSequence(::next)
    }
    val y = fibonacciSequence().take(10).toList()
    println(y) // => [1, 1, 2, 3, 5, 8, 13, 21, 34, 55]

    // Kotlin zapewnia funkcje wyższego rzędu do pracy z kolekcjami (z javy Builder'y).
    val z = (1..9).map {it * 3}
                  .filter {it < 20}
                  .groupBy {it % 2 == 0}
                  .mapKeys {if (it.key) "even" else "odd"}
    println(z) // => {odd=[3, 9, 15], even=[6, 12, 18]}

    // Pętla "for" może być używana ze wszystkim, co zapewnia iterator.
    for (c in "hello") {
        println(c)
    }

    // Pętle "while" działają w taki sam sposób jak w innych językach.
    var ctr = 0
    while (ctr < 5) {
        println(ctr)
        ctr++
    }
    do {
        println(ctr)
        ctr++
    } while (ctr < 10)

    /*
    "If" może być użyte jako wyrażenie, które zwraca wartość.
    Z tego powodu trójdzielny ?: operator nie jest potrzebny w Kotlinie.
    */
    val num = 5
    val message = if (num % 2 == 0) "even" else "odd"
    println("$num is $message") // => 5 is odd

    // "When" może być używane jako alternatywa dla łańcuchów "if-else if".
    val i = 10
    when {
        i < 7 -> println("first block")
        fooString.startsWith("hello") -> println("second block")
        else -> println("else block")
    }

    // "when" może być użyte z argumentem.
    when (i) {
        0, 21 -> println("0 or 21")
        in 1..20 -> println("in the range 1 to 20")
        else -> println("none of the above")
    }

    // "when" może być używane jako funkcja, która zwraca wartość.
    var result = when (i) {
        0, 21 -> "0 or 21"
        in 1..20 -> "in the range 1 to 20"
        else -> "none of the above"
    }
    println(result)

    /*
    Możemy sprawdzić czy obiekt jest określonego typu używając operatora "is".
    Jeśli obiekt przejdzie kontrolę typu, to może być używany jako ten typ bez
    jawnego rzutowania.
    */
    fun smartCastExample(x: Any) : Boolean {
        if (x is Boolean) {
            // x is automatically cast to Boolean
            return x
        } else if (x is Int) {
            // x is automatically cast to Int
            return x > 0
        } else if (x is String) {
            // x is automatically cast to String
            return x.isNotEmpty()
        } else {
            return false
        }
    }
    println(smartCastExample("Hello, world!")) // => true
    println(smartCastExample("")) // => false
    println(smartCastExample(5)) // => true
    println(smartCastExample(0)) // => false
    println(smartCastExample(true)) // => true

    // Smartcast działa również w przypadku blokady
    fun smartCastWhenExample(x: Any) = when (x) {
        is Boolean -> x
        is Int -> x > 0
        is String -> x.isNotEmpty()
        else -> false
    }

    /*
    Rozszerzenia są sposobem na dodanie nowej funkcjonalności do klasy.
    Jest to podobne do metod rozszerzających w języku C#.
    */
    fun String.remove(c: Char): String {
        return this.filter {it != c}
    }
    println("Hello, world!".remove('l')) // => Heo, word!
}

// Klasy enum są podobne do typów enum w Javie.
enum class EnumExample {
    A, B, C // Enum constants are separated with commas.
}
fun printEnum() = println(EnumExample.A) // => A

// Ponieważ każdy enum jest instancją klasy enum, można je zainicjować jako:
enum class EnumExample(val value: Int) {
    A(value = 1),
    B(value = 2),
    C(value = 3)
}
fun printProperty() = println(EnumExample.A.value) // => 1

// Każdy enum ma właściwości pozwalające uzyskać jego nazwę i ordinal(pozycję) w deklaracji klasy enum:
fun printName() = println(EnumExample.A.name) // => A
fun printPosition() = println(EnumExample.A.ordinal) // => 0

/*
Słowo kluczowe "object" może być użyte do tworzenia obiektów singletonowych.
Nie możemy go zainicjować, ale możemy odwoływać się do jego unikalnej instancji przez jego nazwę.
Jest to podobne do obiektów singletonowych w Scali.
*/
object ObjectExample {
    fun hello(): String {
        return "hello"
    }

    override fun toString(): String {
        return "Hello, it's me, ${ObjectExample::class.simpleName}"
    }
}


fun useSingletonObject() {
    println(ObjectExample.hello()) // => hello
    // W Kotlinie "Any" jest korzeniem hierarchii klas, tak jak "Object" jest w Javie
    val someRef: Any = ObjectExample
    println(someRef) // => Hello, it's me, ObjectExample
}


/* Operator asercji not-null (!!) konwertuje dowolną wartość na typ non-null i
rzuca wyjątek, jeśli wartość jest null.
*/
var b: String? = "abc"
val l = b!!.length

data class Counter(var value: Int) {
    // przeciążenie Counter += Int
    operator fun plusAssign(increment: Int) {
        this.value += increment
    }

    // przeciążenie Counter++ i ++Counter
    operator fun inc() = Counter(value + 1)

    // przeciążenie Counter + Counter
    operator fun plus(other: Counter) = Counter(this.value + other.value)

    // przeciążenie Counter * Counter
    operator fun times(other: Counter) = Counter(this.value * other.value)

    // przeciążenie Counter * Int
    operator fun times(value: Int) = Counter(this.value * value)

    // przeciążenie Counter in Counter
    operator fun contains(other: Counter) = other.value == this.value

    // przeciążenie Counter[Int] = Int
    operator fun set(index: Int, value: Int) {
        this.value = index + value
    }

    // przeciążenie Wywołanie instancji licznika
    operator fun invoke() = println("The value of the counter is $value")

}
/* Można również przeciążać operatory poprzez metody rozszerzające */
// przeciążenie -Counter
operator fun Counter.unaryMinus() = Counter(-this.value)

fun operatorOverloadingDemo() {
    var counter1 = Counter(0)
    var counter2 = Counter(5)
    counter1 += 7
    println(counter1) // => Counter(value=7)
    println(counter1 + counter2) // => Counter(value=12)
    println(counter1 * counter2) // => Counter(value=35)
    println(counter2 * 2) // => Counter(value=10)
    println(counter1 in Counter(5)) // => false
    println(counter1 in Counter(7)) // => true
    counter1[26] = 10
    println(counter1) // => Counter(value=36)
    counter1() // => The value of the counter is 36
    println(-counter2) // => Counter(value=-5)
}
```

### Dalsze materiały

* [Kotlin tutorials (Poradniki do kotlina)](https://kotlinlang.org/docs/tutorials/)
* [Spróbuj kotlina w przeglądarce](https://play.kotlinlang.org/)
* [Lista zasobów Kotlina](http://kotlin.link/)

**Oficjalne kursy JetBrains**
* [JetBrains Academy: Kotlin](https://hyperskill.org/tracks?_gl=1%2a1jvkce8%2a_ga%2aMjEzODM2MDI2My4xNjU2MTY1ODY4%2a_ga_9J976DJZ68%2aMTY1NzIyODE3MC40LjAuMTY1NzIyODE3MC4w&_ga=2.17741177.1710735186.1657228171-2138360263.1656165868&category=4)

**Kursy po polsku**
* [Kanał o Wszystkim - Kurs Kotlin - Programowanie](https://www.youtube.com/watch?v=RfiY8RKhV3U&list=PL6aekdNhY7DB2lhRDfePL6owvAC9hfMv3)
