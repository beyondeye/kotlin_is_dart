# Dart Languange Cheat Sheet for Kotlin developers

## Introduction
Here we are going to point out the main differences between the Kotlin and Dart, that
a developer coming from a Kotlin background should focus on.
The basic Dart syntax is very similar to Java. We are not going too much to point out differences
between the two languages that are related to this.

## Hello World
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
??? info "semicolumn at end of lines"
    **Dart** requires a semicolumns (;) at the end of code lines. In **Kotlin** they are optional
??? info "single quotes for strings"
    **Dart** allows both single and double quotes for defining string literals. In **Kotlin** [double quotes are required](https://kotlinlang.org/docs/strings.html#string-literals) while single quotes define [character literals](https://kotlinlang.org/docs/characters.html)
??? info "no ``public``, ``protected``, ``private``"
    **Dart** doesn’t have the keywords ``public``, ``protected``, and ``private``. If an identifier starts with an underscore (_), it’s [private to its library](https://dart.dev/guides/language/language-tour#libraries-and-visibility).
??? check "string interpolation works the same"
    **Dart** [see docs](https://dart.dev/guides/language/language-tour#strings). **Kotlin**  [see docs](https://kotlinlang.org/docs/strings.html#string-templates)
??? check "var works the same"
    **Dart** is strongly typed with support for type inference like **Kotlin** 

## Variables
```kotlin title="Kotlin"
    var a = 1               //variable, type inferred
    var aa:Int = 1          //variable, type explicit
    val b = 2               //Read-only variable, type inferred
    val bb:Int = 2          //Read-only variable, type explicit
    const val c = 3         //compile-time constant, type inferred
    const val cc:Int = 3    //compile-time constant, type inferred
```
```dart title="Dart"
    var a = 1;              //variable, type inferred
    int aa = 1;             //variable, type explicit
    final b = 2;            //Read-only variable, type inferred
    final int bb = 2;       //Read-only variable, type explicit
    const c = 3;            //compile-time constant, type inferred
    const int cc = 3;       //compile-time constant, type inferred
```

??? info "``final`` instead of ``val``"
    **Dart** uses the ``final`` keyword for identifying readonly variables. **Kotlin** uses the ``val`` keyword
??? info "``const`` instead of ``const val``"
    **Dart** uses the ``const`` keyword for identifying compile-time constants. **Kotlin** uses the combination of keywords ``const val``


## 

Try a link [here](other.md#abcd) 

