# Built-in types

## supertypes for all types
??? info "``Object`` instead of ``Any``"
    in **Dart** the supertype of all  types is [``Object``](https://dart.dev/null-safety/understanding-null-safety#top-and-bottom). In **Kotlin** it is [``Any``](https://kotlinlang.org/spec/type-system.html#kotlin.any-typesystem). For nullable types it is ``Object?`` and ``Any?`` respectively
??? info "``Enum`` is the supertype of all Enums"
    in **Dart** there is also a special supertype for all enums
??? info "``num`` is the supertype of all numerical types"
    in **Dart** ``int`` and ``double`` has [``num`` as supertype](https://api.dart.dev/stable/2.18.0/dart-core/num-class.html)    
## Numbers
??? info "``int`` (64 bit integer) instead of ``Int`` and ``Long``"
    in **Dart** there is no 32bit integer type. Also on the web platform [``int``](https://api.dart.dev/stable/dart-core/int-class.html) is mapped to Javascript number  (64-bit floating-point values with no fractional part) and can be from -2^53 to 2^53 - 1.
??? info "``double`` (64 bit floating point) instead of ``Float`` and ``Double``"
    in **Dart** there is [no 32bit floating point type](https://dart.dev/guides/language/language-tour#numbers)
## Strings
```kotlin title="Kotlin"
var s = "a string"
var sraw =
"""
a raw
string
"""
```
```dart title="Dart"
var s1 = `a string`;
var s2= "another string";
var smulti1 = '''
You can create
multi-line strings like this one.
''';
var smulti2 = """This is also a
multi-line string.""";
var sraw = r'In a raw string, not even \n gets special treatment.';
```

??? info "``string`` instead of ``String``"
    in **Dart** [``string``](https://dart.dev/guides/language/language-tour#strings) are a sequence of UTF-16 code units. in **Kotlin** [``String``](https://kotlinlang.org/docs/strings.html) also are internally [encoded in utf-16](https://github.com/JetBrains/kotlin-native/issues/1185)
??? info "single quotes for strings"
    **Dart** allows both single and double quotes for defining string literals. In **Kotlin** [double quotes are required](https://kotlinlang.org/docs/strings.html#string-literals) while single quotes define [character literals](https://kotlinlang.org/docs/characters.html)
??? check "string interpolation works the same way"
    **Dart** [see docs](https://dart.dev/guides/language/language-tour#strings). **Kotlin**  [see docs](https://kotlinlang.org/docs/strings.html#string-templates)




## Booleans
??? info "``bool`` instead of  ``Boolean``"
    see  **Dart** [bool documentation](https://dart.dev/guides/language/language-tour#booleans). see **Kotlin** [Boolean documentation](https://kotlinlang.org/docs/booleans.html)


## Lists
```kotlin title="Kotlin"
var a_mutable_list = mutableListOf(1,2,3)
a_mutable_list.add(4)
val a_final_list = listOf(1,2,3)

//the proper type annotation for list type
var another_list:List<Int> = listOf(4,5,6)

// kotlin does not have the list spread operator
var joined_list = a_final_list + another_list
println(joined_list); //print [1,2,3,4,5,6]


// kotlin does not have the collection_if syntax
var promoActive= true;
var nav = listOfNotNull("Home", "Furniture", "Plants",
                        if(promoActive) "Outlet" else null)
println(nav); //print [Home, Furniture, Plants, Outlet] 
```

```dart title="Dart"
var a_mutable_list= [1,2,3];
a_mutable_list.add(4);
//cannot add elements to this list and it is a compile time constant
var const_list= const [1,2,3];

//the same as writing const [1,2,3]: cannot add elements
// to this list and it is also a compile time constant
const const_list2= [1,2,3];

//the proper type annotation for list type
List<int> another_list=[4,5,6];

//usage of the spread operator   
var joined_list = [0, ...const_list, ...another_list];
print(joined_list); //print [0,1,2,3,4,5,6]
  
//a null list: in Dart null variables are automatically initialized to null
List<int>? null_list;

//usage of the null-aware spread operator
var joined_list2 = [...const_list, ...?null_list];
print(joined_list2); //print [1,2,3]

//collection_if operator
var promoActive= true;
var nav = ['Home', 'Furniture', 'Plants', if (promoActive) 'Outlet'];
print(nav); //print [Home, Furniture, Plants, Outlet]

//collection_for operator
var listOfInts = [1, 2, 3];
var listOfStrings = ['#0', for (var i in listOfInts) '#$i'];  
print(listOfStrings); //print [#0, #1, #2, #3]

```
??? info "supported ``List`` operations are similar (but more limited) to ``Collection`` operations in **Kotlin** "
    see  **Dart** [List documentation](https://api.dart.dev/dart-core/List-class.html). see **Kotlin** [Collections operations](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-collection/)

??? info "lists has the collection spread operator ``...``, and the null-aware collection spread operator ``...?`` "
    see  **Dart** [List documentation](https://dart.dev/guides/language/language-tour#spread-operator). see also the [spread operator proposal](https://github.com/dart-lang/language/blob/master/accepted/2.3/spread-collections/feature-specification.md).
     **Kotlin** does not have the collection spread operator.

??? info "lists has the ``collection_if`` construct"
    see  **Dart** [List documentation](https://dart.dev/guides/language/language-tour#lists). see also the [control flow collections proposal](https://github.com/dart-lang/language/blob/master/accepted/2.3/control-flow-collections/feature-specification.md).
     **Kotlin** does not have the collection if syntax.

??? info "lists has the ``collection_for`` construct"
    see  **Dart** [List documentation](https://dart.dev/guides/language/language-tour#lists). see also the [control flow collections proposal](https://github.com/dart-lang/language/blob/master/accepted/2.3/control-flow-collections/feature-specification.md).
     **Kotlin** does not have the collection_for syntax.

https://dart.dev/guides/language/language-tour#collection-operators

## Sets
```kotlin title="Kotlin"
// a set
var halogens = 
    mutableSetOf("fluorine", "chlorine", "bromine", "iodine", "astatine")

// a set with the proper type annotation
var letters:MutableSet<String> = mutableSetOf("a","b","c")
  
// an empty set
var emptySet= mutableSetOf<String>()
  
// an immutable set
val constSet = setOf("a","b","c")
//the following line will cause a compilation error
//constSet.add('d');
```

```dart title="Dart"
// a set
var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};

 // a set with the proper type annotation
Set<String> letters = {'a','b','c'};
  
// an empty set
var emptySet= <String>{};

//this create a map not a set!
var emptyMap = {};
  
// a constant set
const constSet = {'a','b','c'};
//the following operation will throw an exception  
//constSet.add('d');
```
??? info "see the supported [``Set`` operations](https://dart.dev/guides/libraries/library-tour#sets)"
    see also the **Kotlin** supported [``Set`` operations](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-set/)

??? info "sets has the collection spread operator ``...``, and the null-aware collection spread operator ``...?`` "
    see  **Dart** [spread operator documentation](https://dart.dev/guides/language/language-tour#spread-operator). see also the [spread operator proposal](https://github.com/dart-lang/language/blob/master/accepted/2.3/spread-collections/feature-specification.md).
     **Kotlin** does not have the collection spread operator.

??? info "sets has the ``collection_if`` construct"
    see  **Dart** [collection_if documentation](https://dart.dev/guides/language/language-tour#lists). see also the [control flow collections proposal](https://github.com/dart-lang/language/blob/master/accepted/2.3/control-flow-collections/feature-specification.md).

     **Kotlin** does not have the collection if syntax.

??? info "sets has the ``collection_for`` construct"
    see  **Dart** [collection_for documentation](https://dart.dev/guides/language/language-tour#lists). see also the [control flow collections proposal](https://github.com/dart-lang/language/blob/master/accepted/2.3/control-flow-collections/feature-specification.md).
     **Kotlin** does not have the collection_for syntax.


## Maps
```kotlin title="Kotlin"
//a Map<Int,String> object  
var nobleGases = mutableMapOf(
  2 to "helium",
  10 to "neon",
  18 to "argon",
)

//a map with explicit type annotation
var nobleGases2:MutableMap<Int, String> = mutableMapOf()

//an immutable map
val constantMap = mapOf(
  2 to "helium",
  10 to "neon",
  18 to "argon",
)

//constantMap[2] = 'Helium'; // This line will not compile

```

```dart title="Dart"
//a Map<Int,String> object  
var nobleGases = {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};

//a map with explicit type annotation
Map<int, String> nobleGases2 = {};

//a constant map
final constantMap = const {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};

 constantMap[2] = 'Helium'; // This line will throw an exception.  
```

??? info "see the supported [``Map`` operations](https://dart.dev/guides/libraries/library-tour#maps)"
    see also the **Kotlin** supported [``Map`` operations](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-map/#kotlin.collections.MutableMap)

??? info "maps has the collection spread operator ``...``, and the null-aware collection spread operator ``...?`` "
    see  **Dart** [spread operator proposal](https://github.com/dart-lang/language/blob/master/accepted/2.3/spread-collections/feature-specification.md).
     **Kotlin** does not have the collection spread operator.

??? info "sets has the ``collection_if`` construct"
    see  **Dart** [control flow collections proposal](https://github.com/dart-lang/language/blob/master/accepted/2.3/control-flow-collections/feature-specification.md).
     **Kotlin** does not have the collection if syntax.

??? info "sets has the ``collection_for`` construct"
    see  **Dart** [control flow collections proposal](https://github.com/dart-lang/language/blob/master/accepted/2.3/control-flow-collections/feature-specification.md).
     **Kotlin** does not have the collection_for syntax.
