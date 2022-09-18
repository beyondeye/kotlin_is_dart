# Enums
For **Dart** see [here](https://dart.dev/guides/language/language-tour#enumerated-types). For **Kotlin** see [here](https://kotlinlang.org/docs/enum-classes.html)
```kotlin title="Kotlin"
//a simple enum
enum class Color { red, green, blue }


// an "enhanced" enum (an enum whose instances are more like classes)
// note that a semicon is required at the end of the list of possible 
// enum values, before definitions of enum fields and methods. 
enum class Vehicle(
    val tires:Int,
    val passengers:Int,
    val carbonPerKilometer:Int) : Comparable<Vehicle> {
    car(tires= 4, passengers= 5, carbonPerKilometer= 400),
    bus(tires= 6, passengers= 50, carbonPerKilometer= 800),
    bicycle(tires= 2, passengers= 1, carbonPerKilometer= 0); //SEMICOLON HERE!

    val carbonFootprint:Int get() =
        Math.round(carbonPerKilometer.toDouble() / passengers).toInt()

    //cannot override compareTo in enums in Kotlin(Java)
    // so we define a custom method
    fun compare(other:Vehicle):Int =
        carbonFootprint - other.carbonFootprint
}

//enum index 
// (the index of the corresponding enum label in the enum definition)
// This is also the index of the value in the "values" list.
// prints  "0,1,2"
println ("${Color.red.ordinal}, ${Color.green.ordinal}, ${Color.blue.ordinal}")
  
//list of all enum labels (List<Color)
// values() returns an array 
// array does not have a proper toString() implementation, 
// so we convert it to list for printing it
println(Color.values().toList()) //[red,green,blue]
  
//the name for some enum label  
println(Color.blue.name);  //blue
```
```dart title="Dart"
//a simple enum
enum Color { red, green, blue }

//an "enhanced" enum (enum that are more like classes)
enum Vehicle implements Comparable<Vehicle> {
  car(tires: 4, passengers: 5, carbonPerKilometer: 400),
  bus(tires: 6, passengers: 50, carbonPerKilometer: 800),
  bicycle(tires: 2, passengers: 1, carbonPerKilometer: 0);

  const Vehicle({
    required this.tires,
    required this.passengers,
    required this.carbonPerKilometer,
  });

  final int tires;
  final int passengers;
  final int carbonPerKilometer;

  int get carbonFootprint => (carbonPerKilometer / passengers).round();

  @override
  int compareTo(Vehicle other) => carbonFootprint - other.carbonFootprint;
}

//enum index 
// (the index of the corresponding enum label in the enum definition)
// This is also the index of the value in the "values" list.
print ("${Color.red.index}, ${Color.green.index}, ${Color.blue.index}"); //0,1,2
  
// list of all enum labels (List<Color>)
print(Color.values); //[Color.red, Color.green, Color.blue]
  
// the name for some enum label  
print(Color.blue.name);  //blue
```

