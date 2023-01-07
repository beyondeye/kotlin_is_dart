# Introduction
Are you a Kotlin developer that wants to learn Dart, or a Dart developer that wants to learn Kotlin, with the least possible effort? Then you are in the right place!

**Important note**: info boxes that does not specify if they refer to Kotlin or Dart by default are referring to Dart. for example:
!!! info "semicolon at end of lines"

This document is based on 

- **Dart version 2.18.0**
- **Kotlin 1.7.10**

# Kotlin to Dart transpiler
If you are interested into a tool to help porting Kotlin code to Dart try our [kotlin2dart transpiler](https://github.com/beyondeye/kotlin2dart).


# Experimenting with code
You can experiment with **Dart** code online in [DartPad](https://dartpad.dev/?)

You can experiment with **Kotlin** code online in [Kotlin Playground](https://play.kotlinlang.org/)

## Hello World
The basic Dart syntax is very similar to Java. 

```kotlin title="Kotlin"
public fun main() { //public is optional
    var w = "world"
    print("Hello $w") //output "Hello world"
}
```
```dart title="Dart"
void main() {
    var w = 'world';
    print('Hello $w'); //output 'hello world'
}

```
??? info "semicolon at end of lines"
    **Dart** requires a semicolon (;) at the end of code lines. In **Kotlin** they are optional
??? info "single quotes for strings"
    **Dart** allows both single and double quotes for defining string literals. In **Kotlin** [double quotes are required](https://kotlinlang.org/docs/strings.html#string-literals) while single quotes define [character literals](https://kotlinlang.org/docs/characters.html)
??? info "no ``public``, ``protected``, ``private``"
    **Dart** doesn’t have the keywords ``public``, ``protected``, and ``private``. If an identifier starts with an underscore (_), it’s [private to its library](https://dart.dev/guides/language/language-tour#libraries-and-visibility).
??? check "string interpolation works the same way"
    **Dart** [see docs](https://dart.dev/guides/language/language-tour#strings). **Kotlin**  [see docs](https://kotlinlang.org/docs/strings.html#string-templates)
??? check "``var`` works the same way"
    **Dart** is strongly typed with support for type inference like **Kotlin** 

## Variables
```kotlin title="Kotlin"
    var a = 1               //variable, type inferred
    var aa:Int = 1          //variable, type explicit

    val b = 2               //Read-only variable, type inferred
    val bb:Int = 2          //Read-only variable, type explicit

    const val c = 3         //compile-time constant, type inferred
    const val cc:Int = 3    //compile-time constant, type explicit

    var str:String?= null    //nullable variable

    lateinit var d:String    //initialized later
```
```dart title="Dart"
    var a = 1;              //variable, type inferred
    int aa = 1;             //variable, type explicit

    final b = 2;            //Read-only variable, type inferred
    final int bb = 2;       //Read-only variable, type explicit

    const c = 3;            //compile-time constant, type inferred
    const int cc = 3;       //compile-time constant, type explicit

    String? str;            //nullable variable, by default initialized to null

    late String d;          //initialized later
```

??? info "``final`` instead of ``val``"
    **Dart** uses the [``final`` keyword](https://dart.dev/guides/language/language-tour#final-and-const) for identifying readonly variables. **Kotlin** uses the ``val`` keyword
??? info "``const`` instead of ``const val``"
    **Dart** uses the [``const`` keyword](https://dart.dev/guides/language/language-tour#final-and-const) for identifying compile-time constants. **Kotlin** uses the combination of keywords ``const val``
??? info "``const`` is a more extended concept"
    see [const variables](https://dart.dev/guides/language/language-tour#final-and-const) and [const constructors](https://dart.dev/guides/language/language-tour#constant-constructors) in **Dart** documentation.
??? info "nullable variable are by default initialized to null"
    **Dart**  [automatically initializes to null](https://dart.dev/guides/language/language-tour#default-value) nullable variables    
??? info "``late`` instead of ``lateinit``"
    **Kotlin** [``lateinit`` variables](https://kotlinlang.org/docs/properties.html#late-initialized-properties-and-variables) are called [```late``` variables](https://dart.dev/guides/language/language-tour#late-variables) in **Dart**



<!-- Try a link [here](other.md#abcd) 

## A subparagraph here <a name="abcd"> </a>

-->

