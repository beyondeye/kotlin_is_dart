# Typedefs
For **Dart** see [here](https://dart.dev/guides/language/language-tour#typedefs). For **Kotlin** see [here](https://kotlinlang.org/docs/type-aliases.html)

```kotlin title="Kotlin"
typealias IntList = List<Int>

typealias ListMapper<X> = Map<X, List<X>>

typealias Compare<T> = (a:T,b:T) -> Int

var il:IntList = listOf(1, 2, 3)
var m2:ListMapper<String>  = mapOf()

val sort:Compare<Int> = { a,b -> a-b }
  
// in Kotlin I cannot check the following,
// because kotlin generics has type erasure,
// in other words we cannot check if 
// sort is Compare<String> or Compare<Int>
// or any other type parameter  
 
 /* print(sort is Compare<String>); // false */

 print(sort is Compare<Int>) // true

```

```dart title="Dart"
typedef IntList = List<int>;

typedef ListMapper<X> = Map<X, List<X>>;

typedef Compare<T> = int Function(T a, T b);

int sort(int a, int b) => a - b;

IntList il = [1, 2, 3];
ListMapper<String> m2 = {};
print(sort is Compare<String>); // false

print(sort is Compare<int>); // true
```

??? info "Don't overuse ``typedef`` for function types"
    in **Dart** 1.0 if you wanted to use a function type for a field, variable, or generic type argument, you had to first define a typedef for it.
    From [Dart 2.0 this is no more required](https://dart.dev/guides/language/effective-dart/design#prefer-inline-function-types-over-typedefs)