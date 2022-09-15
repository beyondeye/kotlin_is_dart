# Classes
??? check  "Use a dot ``.`` to refer to an instance variable or method."
    This is the same in **Dart** and in **Kotlin**

??? check " Use ``?.`` instead of ``.`` to avoid an exception when the leftmost operand is ``null``."
    This is the same in **Dart** and in **Kotlin**

## methods inherited from ``Object``
in **Dart** all types inherit from the supertype ``Object`` the methods ``operator ==``,  ``toString()`` and the property ``hashCode``. 

in **Kotlin** all types inherit from the supertype ``Any`` the methods ``equals()``, ``toString()`` and ``hashCode()``.
## Creating a  class instance
In **Dart** the ``new`` keyword before call to a class constructor is optional. In **Kotlin** the ``new`` keyword does not exist at all.
```kotlin title="Kotlin"
var p1 = Point(1,1)
var p2 = Point(2,2)
```
```dart title="Dart"
var p1 = Point(1,1);
var p2 = new Point(2,2);
```

## Constant Constructors
In **Dart** If your class produces objects that never change, you can make these objects compile-time constants. To do this, [define a *const constructor*](#const_constructor) and make sure that all class fields are final. Constructing two identical const class instances results in a single, canonical instance:

In **Kotlin** there is no such concept as const constructors. 
```dart title="Dart"
var a = const ImmutablePoint(1, 1);
var b = const ImmutablePoint(1, 1);
assert(identical(a, b)); // They are the same instance!
```
In **Dart** *const constructors* are "activated" by the ``const`` keyword before the call to the constructor. This define a *const context*: all const constructors used in the same line of code will be also activated, with no need to specifiy the ``const`` keyword before each of them.

```dart title="Dart"
// Lots of unneeded const keywords here.
const pointAndLine = const {
  'point': const [const ImmutablePoint(0, 0)],
  'line': const [const ImmutablePoint(1, 10), const ImmutablePoint(-2, 11)],
};

// the following line is equivalent to the previous one
// and define the same const instance
const pointAndLine2 = const {
  'point': [ ImmutablePoint(0, 0)],
  'line': [ ImmutablePoint(1, 10), ImmutablePoint(-2, 11)],
};
assert(identical(pointAndLine, pointAndLine2));

```
Note that if the ``const`` keyword is not added before the call to a *const constructor* (or an outer constructor calling a nested constructor as explained above), the constructor will **NOT** create a compile-time constant:

```dart title="Dart"
var a = const ImmutablePoint(1, 1); // Creates a constant
var b = ImmutablePoint(1, 1); // Does NOT create a constant

assert(!identical(a, b)); // NOT the same instance!
```
## Getting an object’s type
In **Dart** to get an object’s type at runtime, you can use the ``Object`` property ``runtimeType``, which returns a ``Type`` object.
In **Kotlin** instead you can use the syntax ``::class``

```kotlin title="Kotlin"
var a:Any=1
println(a::class) // class kotlin.Int
```
```dart title="Dart"
Object a=1;
print(a.runtimeType); //int
```
??? warning " Better use ``is`` than ``runtimeType`` to test an object’s type."
    In **Dart**, in production environments, using  ``is`` to test the object Type is more stable than using ``object.runtimeType == Type``.

## Basic Class declaration

```kotlin title="Kotlin"
class Point {
    var x:Double
    var y:Double
    constructor(x:Double,y:Double){
        this.x = x
        this.y = y
    }
}
```
```dart title="Dart"
class Point {
  double x=0; //initialization required for avoiding compilation error unless field is nullable
  double y=0; //initialization required for avoiding compilation error unless field is nullable

  Point(double x, double y) {
    this.x = x;
    this.y = y;
  }
}
```
## Constructors
### Initializing formal parameters

Both in **Dart** and **Kotlin** there are better ways to write the code above. in  **Kotlin** there is the concept of [primary constructor](https://kotlinlang.org/docs/classes.html#constructors), in **Dart** there is the concept of [initializing formal parameters](https://dart.dev/guides/language/language-tour#constructors) that allow for a much more concise syntax:
```kotlin title="Kotlin"
class Point(var x:Double, var y:Double) //primary constructor

class PointXY(var x: Double, var y: Double) {
    var z: Double
    init { //init blocks are executed in the order they are found in the class definition
        z = x * y
    }
}

//or even better
class PointXY(var x: Double, var y: Double) {
    var z: Double = x*y
}
```
```dart title="Dart" hl_lines="7 17"
class Point {
  double x,y;

  // initializing formal parameters: 
  // use the first parameter provided to the constructor to initialize this.x
  // use the second parameter provided to the constructor to initialize this.y
  Point(this.x, this.y);
}

class PointXY {
  double x,y;

  double xy=0; //initialization required for avoiding compilation error unless field is nullable
  
  // NOTE: this.x and this.y are set  
  // before the constructor body runs.
  PointXY(this.x, this.y) {
    xy=x*y;
  }
}
```
### Default constructors
In **Dart** If you don’t declare a constructor, a default constructor is provided for you. The default constructor has no arguments and invokes the no-argument constructor in the superclass. 

In **Kotlin**, [for the JVM platform](https://kotlinlang.org/docs/classes.html#secondary-constructors) a parameterless constructor will be also generated if all the primary constructor parameters have default values.
```kotlin title="Kotlin"
class Point {
    var x:Double=0.0
    var y:Double=0.0
}
var p = Point()
```
```dart title="Dart"
class Point {
  double x=0;
  double y=0;
}
var p = Point();
```
### Initializer list
In **Dart** if you want to initialize some fields in a constructor (with values not provided as parameters) there is a special syntax called ``initializer list``
This syntax is useful for example in [named constructors](#named_constr).

```dart title="Dart" hl_lines="5"
class Point {
  double x; //x not initialized here!
  double y; //y not initialized here!

  Point(): x=0, y=0; //initializer list
}
```
During development, you can validate inputs by using assert in the initializer list.
```dart title="Dart" hl_lines="6"
class Point {
  double x; //x not initialized here!
  double y; //y not initialized here!

  //named constructor with parameter validation in initializer list
  Point.withPositiveX(this.x,this.y): assert(x>0); //initializer list
}
```
Initializer lists are handy when setting up final fields. The following example initializes three final fields in an initializer list
```dart title="Dart" hl_lines="7 8 9"
class Point {
  final double x;
  final double y;
  final double distanceFromOrigin;

  Point(double x, double y)
      : x = x,
        y = y,
        distanceFromOrigin = sqrt(x * x + y * y);
}
```
### Named constructors <a name="named_constr"> </a>
In **Dart** [named constructor](https://dart.dev/guides/language/language-tour#constructors) are constructors with a name appended (after a dot).

In **Kotlin** an identical syntax at the constructor usage site, can be obtained with factory methods in the class companion object.
```kotlin title="Kotlin" hl_lines="3"
class Point(var x:Double,var y:Double) {
    companion object {
        fun origin() = Point(0.0,0.0)
    }
}
var p = Point.origin()
```
```dart title="Dart" hl_lines="8"
class Point {
  final double x;
  final double y;

  Point(this.x, this.y);

  // Named constructor
  Point.origin()
      : x = 0, y = 0; //this is called an initializer list
}

var p = Point.origin(); 
```
### Redirecting constructors
a constructor whose only purpose is to redirect to another constructor in the same class.
```kotlin title="Kotlin"
class Point(var x:Double,var y:Double) {
    // Delegates to the main constructor.
    constructor(x:Double): this(x,0.0)
}
```

```dart title="Dart"
class Point {
  double x, y;

  // The main constructor for this class.
  Point(this.x, this.y);

  // Delegates to the main constructor.
  Point.alongXAxis(double x) : this(x, 0);
}
```

### Constant constructors  <a name="const_constructor"> </a>
In **Dart** If your class produces objects that never change, you can make these objects compile-time constants. To do this, define a const constructor and make sure that all instance variables are final.
```dart title="Dart"
class ImmutablePoint {
  //all fields are final: it is 
  //possible to have a constant constructor
  final double x, y;
  //contant constructor
  const ImmutablePoint(this.x, this.y);
}
```
### Factory constructors
In **Dart**  use the factory keyword when implementing a constructor that doesn’t always create a new instance of its class. There are also [other reasons](https://dart.dev/guides/language/language-tour#constructors) to use a factory constructors. Factory constructors does not have access to ``this``.
In the following example, the Logger factory constructor returns objects from a cache, and the Logger.fromJson factory constructor initializes a final variable from a JSON object.
```dart title="Dart" hl_lines="10"
class Logger {
  final String name;
  bool mute = false;

  // _cache is library-private, thanks to
  // the _ in front of its name.
  static final Map<String, Logger> _cache = <String, Logger>{};

  //a factory constructor that create a new object only if not already present in _cache
  factory Logger(String name) {
    return _cache.putIfAbsent(name, () => Logger._internal(name));
  }
  //an internal named constructor
  Logger._internal(this.name);

  void log(String msg) {
    if (!mute) print(msg);
  }
}
```

## Operators
For **Dart** [see here](https://dart.dev/guides/language/language-tour#methods),  for  **Kotlin** [see here](https://kotlinlang.org/docs/operator-overloading.html)

```kotlin title="Kotlin" hl_lines="2"
class Vector( var x:Double, var y:Double) {
    operator fun plus(other:Vector):Vector {
        return Vector(x+other.x,y+other.y)
    }
    override fun toString():String ="x:$x, y:$y"
}

var a=Vector(2.0,0.0)
var b=Vector(0.0,3.0)
var c= a+b
println(c) //x:2.0, y:3.0
```

```dart title="Dart" hl_lines="4"
class Vector {
  final double x, y;
  Vector(this.x, this.y);
  Vector operator+(Vector other) {
    return Vector(x+other.x,y+other.y);
  }
  @override
  String toString() => "x:$x, y:$y";
}

var a=Vector(2.0,0.0);
var b=Vector(0.0,3.0);
var c = a+b;
print(a+b); //x:2, y:3
```
## Getters and Setters
For **Dart** [see here](https://dart.dev/guides/language/language-tour#methods) for **Kotlin** [see here](https://kotlinlang.org/docs/properties.html#getters-and-setters)

```kotlin title="Kotlin" hl_lines="3 4"
class Square(var side:Double) {
  var area:Double 
    get() = side*side
    set(value) { side = Math.sqrt(value) }
}

var sq=Square(10);
print(sq.area); //100 
sq.area=81;
print(sq.side); //9
```

```dart title="Dart" hl_lines="4 5"
class Square {
  double side;
  Square(this.side);
  double get area { return side*side; }
  set area(double newArea) { side = sqrt(newArea); }
}

var sq=Square(10);
print(sq.area); //100 
sq.area=81;
print(sq.side); //9
```

## Static Variables and Methods
For **Dart** [see here](https://dart.dev/guides/language/language-tour#class-variables-and-methods). For **Kotlin** [see here](https://kotlinlang.org/docs/object-declarations.html#companion-objects)

```kotlin title="Kotlin" hl_lines="3 4"
class Point(val x:Double, val y:Double) {
    companion object {
        val origin = Point(0.0,0.0)
        fun distanceBetween(a:Point, b:Point):Double {
            val dx = a.x - b.x
            val dy = a.y - b.y
            return sqrt(dx * dx + dy * dy)
        }  
    }
}
var a = Point.origin
var b = Point(3.0, 4.0)
var distance = Point.distanceBetween(a, b)
println(distance); //5
```

```dart title="Dart" hl_lines="5 6"
class Point {
  final x, y;
  Point(this.x, this.y);

  static final Point origin = Point(0.0,0.0);
  static double distanceBetween(Point a, Point b) {
    var dx = a.x - b.x;
    var dy = a.y - b.y;
    return sqrt(dx * dx + dy * dy);
  }
}
var a = Point.origin;
var b = Point(3, 4);
var distance = Point.distanceBetween(a, b);
print(distance); //5
```