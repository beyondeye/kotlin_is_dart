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
??? info "no ``public``, ``protected``, ``private`` in Dart"
    **Dart** doesn’t have the keywords ``public``, ``protected``, and ``private``. If an identifier starts with an underscore (_), it’s [private to its library](https://dart.dev/guides/language/language-tour#libraries-and-visibility).
??? check "string interpolation works the same"
    **Dart** [see docs](https://dart.dev/guides/language/language-tour#strings). **Kotlin**  [see docs](https://kotlinlang.org/docs/strings.html#string-templates)
??? check "var works the same"
    **Dart** is strongly typed with support for type inference like **Kotlin** 

## 

Try a link [here](other.md#abcd) 

