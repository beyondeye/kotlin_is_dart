# Generics
For **Dart** see [here](https://dart.dev/guides/language/language-tour#generics). For **Kotlin** see [here](https://kotlinlang.org/docs/generics.html)

??? check "The syntax for creating and using classes with type parameters is the same"

??? info "Generics are reified"
    In **Dart**  generic types are *reified*, which means that they carry their type information around at runtime.

    In **Kotlin**, like in Java, generics use type erasure, which means that generic type parameters are removed at runtime: you can test whether an object is a ``List``, but you can’t test whether it’s a ``List<String>``. But there is a work-around, that is [inline functions with reified type parameters](https://kotlinlang.org/docs/inline-functions.html#reified-type-parameters)  

## Generic types In collections

```kotlin title="Kotlin"
// note: the explicit type parameter here is actually redundant
var names = mutableListOf<String>("Seth", "Kathy", "Lars")

// note: the explicit type parameter here is actually redundant
var uniqueNames = mutableSetOf<String>("Seth", "Kathy", "Lars")

// note: the explicit type parameter here is actually redundant
var pages = mutableMapOf<String, String>(
  "index.html" to "Homepage",
  "robots.txt" to "Hints for web robots",
  "humans.txt" to "We are people, not machines"
  )
```
```dart title="Dart"
//define a List<String>
// note: the explicit type parameter here is actually redundant
var names = <String>['Seth', 'Kathy', 'Lars'];

//define a Set<String>
// note: the explicit type parameter here is actually redundant
var uniqueNames = <String>{'Seth', 'Kathy', 'Lars'};

//define a Map<String,String>
// note: the explicit type parameter here is actually redundant
var pages = <String, String>{
  'index.html': 'Homepage',
  'robots.txt': 'Hints for web robots',
  'humans.txt': 'We are people, not machines'
  };
}
```
## Restricting the generic type
```kotlin title="Kotlin"  hl_lines="6"
interface Animal 
class Dog(var name:String):Animal
class Cat(var name:String):Animal

//a pair of any objects that derive from the Animal base class
class PairOfAnimals<A : Animal>(var first:A, var second:A) 

var p1 = PairOfAnimals(Dog("Pluto"),Dog("Max")) //ok
var p2 = PairOfAnimals(Dog("Pluto"),Cat("Felix")) //ok
var p3 = PairOfAnimals(Cat("Tom"),Cat("Felix")) //ok

//compilation error! String is not an Animal
var p4 = PairOfAnimals("aa",Cat("Felix"))

```
```dart title="Dart" hl_lines="12"
class Animal {}
class Dog implements Animal {
  String name;
  Dog(this.name);
}
class Cat implements Animal {
  String name;
  Cat(this.name);
}

//a pair of any objects that derive from the Animal base class
class PairOfAnimals<A extends Animal> {
  A first,second;
  PairOfAnimals(this.first,this.second);
}

var p1 = PairOfAnimals(Dog("Pluto"),Dog("Max")); //ok
var p2 = PairOfAnimals(Dog("Pluto"),Cat("Felix")); //ok
var p3 = PairOfAnimals(Cat("Tom"),Cat("Felix")); //ok

//compilation error! String is not an Animal
var p4 = PairOfAnimals("aa",Cat("Felix"));

```
??? info "Handling bounds on generic type can be much more complex in Kotlin"
    see [**Kotlin** docs](https://kotlinlang.org/docs/generics.html#variance)

### Restricting to non-nullable type
```kotlin title="Kotlin"
// only non nullable type parameters allowed
// (Any is base type of all non-nullable types)
class SomeClass<T:Any>
```
```dart title="Dart"
// only non-nullable type parameters allowed
// (Object is base type of all non-nullable types)
class SomeClass<T extends Object>
```
## Instantiating generic class with no type parameter
In **Dart** it is possible to instantiate a generic class without specifying the type parameter. 
```dart title="Dart"
class SomeBaseType {}
class SomeClass<T extends SomeBaseType> {}
var foo = SomeClass(); //instance of SomeClass<SomeBaseType>
```
## Generic methods
```kotlin title="Kotlin"
fun  <T> extractFirstElement(ts:List<T>):T {
  // show that we can use the type parameter inside the function
  var tmp:T = ts[0];
  return tmp;
}
var cities = listOf("Rome","Paris","New York")
var first_city= extractFirstElement(cities)
print(first_city) //Rome
```
```dart title="Dart"
T extractFirstElement<T>(List<T> ts) {
  // show that we can use the type parameter inside the function
  T tmp = ts[0];
  return tmp;
}

var cities = ['Rome','Paris','New York'];
var first_city= extractFirstElement(cities);
print(first_city); //Rome
 
```



