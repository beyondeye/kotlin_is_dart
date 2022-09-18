# Extension Methods
For **Dart** see [here](https://dart.dev/guides/language/extension-methods), for **Kotlin** see [here](https://kotlinlang.org/docs/extensions.html)

```kotlin title="Kotlin"
fun String.parseInt():Int {
    //kotlin already have a similar extension method: redirect to it
    return this.toInt()
}
fun String.parseDouble():Double {
    //kotlin already have a similar extension method: redirect to it
    return this.toDouble()
}

fun <T> MutableList<T>.swap(index1: Int, index2: Int) {
    val tmp = this[index1] // 'this' corresponds to the list
    this[index1] = this[index2]
    this[index2] = tmp
}

println("123".parseInt()+1); //124
println("123.0".parseDouble()+0.5); //123.5
  
var list= mutableListOf(0,1,2,3)
list.swap(0,1);
println(list); //1,0,2,3
```

```dart title="Dart"
// extension method are defined as part of a named extension block
// it is used in Dart to help resolving conflicting extension method definitions
extension NumberParsing on String {
  int parseInt() {
    return int.parse(this);
  }
  double parseDouble() {
    return double.parse(this);
  }
  // ···
}

// it is possible to define extension methods on a generic type. 
// This is the syntax
extension ListSwap<T> on List<T> {
  void swap(int index1, int index2) {
    final tmp= this[index1];
    this[index1]=this[index2];
    this[index2]=tmp;
  }
}

// To create a local extension that’s visible only in the library 
// where it’s declared, either omit the extension name
// or give it a name that starts with an underscore (_)
extension on String {
  String wrappedWithA() {
    return "A${this}A";
  }
}

print('123'.parseInt()+1); //124
print('123.0'.parseDouble()+0.5); //123.5
 
var list= [0,1,2,3];
list.swap(0,1);
print(list); //1,0,2,3
print ('BB'.wrappedWithA()); //ABBA
```

??? info " extensions are resolved statically"
    Both in [**Dart**](https://dart.dev/guides/language/extension-methods#static-types-and-dynamic) and in [**Kotlin**](https://kotlinlang.org/docs/extensions.html#extensions-are-resolved-statically) extensions are resolved statically. In other words the dynamic type at runtime does not count. What counts is the resolved 
    static type at a compile time. 

## Extension Methods Visibility
There are several important details about extension methods visibility and disambiguation. For **Dart** see [here](https://dart.dev/guides/language/extension-methods#api-conflicts)
for **Kotlin** see [here](https://kotlinlang.org/docs/extensions.html#scope-of-extensions)  
