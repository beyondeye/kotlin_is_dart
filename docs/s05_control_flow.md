# Control Flow

## ``if`` and ``else``
They are the same. But **Kotlin** support also [if-else expression](https://kotlinlang.org/docs/control-flow.html#if-expression)
## ``while`` and ``do-while``, ``break`` and ``continue``
They are the same: for **Dart** [see here](https://dart.dev/guides/language/language-tour#while-and-do-while). For **Kotlin** [see here](https://kotlinlang.org/docs/control-flow.html#while-loops)

## ``for`` loops
### standard loop

```kotlin title="Kotlin"
//standard for loop    
for (i in 1..3 step 1) {
    println(i) //1 2 3
}

//standard for loop: step 1 can be omitted
for (i in 1..3) {
    println(i) //1 2 3
}

//standard reversed loop (note that the step is POSITIVE!)
for (i in 6 downTo 0 step 2) {
    println(i) //6 4 2 0
}

//standard reversed loop: step 1 can be omitted
for (i in 6 downTo 0) {
    println(i) //6 5 4 3 2 1 0
}
```
```dart title="Dart"
//standard for loop    
for (var i=1; i<=3; ++i) {
    print(i); //1 2 3
}

//standard reversed loop
for (var i=6; i>=0; i-=2) {
    print(i); //6 4 2 0
}
```
### loop variable captured in closure
```kotlin title="Kotlin"
//Closures inside of Kotlins’s for loops capture the value of the index
var callbacks = mutableListOf<()->Unit>()
for (i in 0..2) {
  callbacks.add({ println(i)})
}
// print 0 and then 1
callbacks.forEach{ c-> c() }
```
```dart title="Dart"
//Closures inside of Dart’s for loops capture the value of the index
var callbacks = [];
for (var i = 0; i < 2; i++) {
  callbacks.add(() => print(i));
}
// print 0 and then 1
callbacks.forEach((c) => c()); 

```


### loop over iterable 
For **Dart** see [iteration in library-tour](https://dart.dev/guides/libraries/library-tour#iteration). For **Kotlin** see [for loops](https://kotlinlang.org/docs/control-flow.html#for-loops) and [iterable in stdlib](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-iterable/)

```kotlin title="Kotlin"
var cities = listOf("Rome","Paris","London")
//iterate over elements of iterable
// the same as in Dart see 
// see also 
for(city:String in cities) //the String type annotation can be omitted
{
    println(city)    
}
```
```dart title="Dart"
  //iterate over elements of iterable
//see 
var cities=["Rome","Paris","London"];
for(final city in cities) //instead "final" we can specify "var" or the explicit type (String)
{
    print(city);    
}

```

### iterable.forEach()
For **Dart** see [forEach](//https://api.dart.dev/stable/dart-core/Iterable/forEach.html). For **Kotlin** see [forEach in stdlib](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/for-each.html)
```kotlin title="Kotlin"
//iterable has also a forEach method for iterating over the elements
cities.forEach { city-> println(city) }
  
//or more simply
cities.forEach{ println(it) }
```
```dart title="Dart"  
//Iterable classes also have a forEach() method as another option:

cities.forEach((city) {print(city);});

//or more simply
cities.forEach(print);
```  

## ``switch`` and ``case``
```kotlin title="Kotlin"
```
```dart title="Dart"
```  
**Kotlin** support also [when expression](https://kotlinlang.org/docs/control-flow.html#when-expression)
## ``assert``
```kotlin title="Kotlin"
```
```dart title="Dart"
```  
