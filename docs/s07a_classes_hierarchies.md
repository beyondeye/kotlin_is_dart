# Class Hierarchies

## Interfaces
```kotlin title="Kotlin"
interface IShapeWithArea {
  fun area():Double { return 0.0 } //default method implementation (optional)
}

interface IShapeWithPerimeter {
  fun perimeter():Double { return 0.0 }
}

//in Kotlin we must specify this interface explicitly
interface IRectangle {
    var w:Double
    var h:Double
}

class Rectangle(override var w:Double,override var h:Double)
 : IShapeWithArea,IShapeWithPerimeter,IRectangle 
{
  override fun area()= w*h
  override fun perimeter()=2*w+2*h
}

class Square(var side:Double) : IShapeWithArea,IShapeWithPerimeter,IRectangle
{
  //from IShapeWithArea
  override fun area() = side*side
  //from IShapeWithPerimeter
  override fun perimeter() = 4*side
  //from IRectangle
  override var w:Double 
    get() =side 
    set(value) {side=value } 
  //from IRectangle
  override var h:Double 
    get() =side 
    set(value) {side=value }     
}
```
```dart title="Dart"
// Every class in Dart* implicitly defines an interface 
// containing all fields and methods
// of the class and of any interfaces it implements.
class IShapeWithArea {
  double area() { return 0; }
}

class IShapeWithPerimeter {
  double perimeter() { return 0; }
}

// when using the "implements" keyword, we specify that we want
// to implement the implicit interface defined
// by the classes IShapeWithArea,IShapeWithPerimeter
class Rectangle implements IShapeWithArea,IShapeWithPerimeter {
  double w,h;
  Rectangle(this.w,this.h);
  @override
  double area() => w*h;
  @override
  double perimeter() => 2*w+2*h;    
}

class Square implements IShapeWithArea,IShapeWithPerimeter,Rectangle
{
  double side;
  Square(this.side);
  //from IShapeWithArea
  @override
  double area() => side*side; 
  //from IShapeWithPerimeter
  @override
  double perimeter() => 4*side; 
  //from Rectangle
  @override
  double get w => side;
  @override
  set w(double value) { side=value; }
  @override
  //from Rectangle
  double get h => side;
  @override
  set h(double value) { side=value; }
}
```
??? info " no ``interface`` keyword"
    In **Dart** every class [implicitly defines an interface](https://dart.dev/guides/language/language-tour#implicit-interfaces) containing all fields and methods of the class and of any interfaces it implements. 
    
    In **Kotlin** there are explicit [interfaces](https://kotlinlang.org/docs/interfaces.html).


## Abstract Classes
```kotlin title="Kotlin" hl_lines="4 5 6 7 8 18 25"
class Color(val r:Int,val g:Int, val b:Int)

//abstract classes can contains data fields (unlike interfaces)
abstract class ColoredShape(var fillColor:Color,var borderColor:Color) {
    abstract fun area():Double
    abstract fun perimeter():Double
    fun areaToPerimeterRation():Double = area()/perimeter()
}

interface IRectangle {
    var w:Double
    var h:Double
}

class Rectangle(
    override var w:Double,override var h:Double,
	fillColor:Color, borderColor:Color) 
: IRectangle,ColoredShape(fillColor,borderColor) {
  override fun area()= w*h
  override fun perimeter()=2*w+2*h
}

class Square(var side:Double,
            fillColor:Color, borderColor:Color) 
: IRectangle,ColoredShape(fillColor,borderColor)
{
  override fun area() = side*side
  override fun perimeter() = 4*side
  override var w:Double 
    get() =side 
    set(value) {side=value } 
  override var h:Double 
    get() =side 
    set(value) {side=value }     
}
```
```dart title="Dart" hl_lines="7 11 12 16 17 19 20 27 30 31"
class Color
{
  int r,g,b;
  Color(this.r,this.g,this.b);
}

abstract class ColoredShape 
{
  Color fillColor,borderColor;
  ColoredShape(this.fillColor,this.borderColor);
  double area(); //method with no implementation: abstract
  double perimeter(); //method with no implementation: abstract
  double areaToPerimeterRation() => area()/perimeter();
}

// use the "extends" keyword to extend another class (abstract or not)
class Rectangle extends ColoredShape {
  double w,h;
  //define in constructor also fields of parent class ColoredShape constructor
  Rectangle(this.w,this.h,super.fillColor,super.borderColor);
  @override
  double area() => w*h;
  @override
  double perimeter() => 2*w+2*h;    
}

class Square  extends ColoredShape implements Rectangle
{
  double side;
  //define in constructor also fields of parent class ColoredShape constructor
  Square(this.side,super.fillColor,super.borderColor);
  @override
  double area() => side*side; 
  @override
  double perimeter() => 4*side; 
  @override
  double get w => side;
  @override
  set w(double value) { side=value; }
  @override
  double get h => side;
  @override
  set h(double value) { side=value; }
}

```
??? info "all classes are open, all methods are open"
    In **Dart** all classes [can be extended (inherited from)](https://dart.dev/guides/language/language-tour#extending-a-class) not only abstract classes.
    In **Kotlin** only [open classes](https://kotlinlang.org/docs/inheritance.html) can be inherited from, and only [open methods](https://kotlinlang.org/docs/inheritance.html#overriding-methods) can be overridden.

## NoSuchMethod()
for ``dynamic`` types, **Dart** support [special handling of cases where a not existent method is invoked](https://api.dart.dev/stable/dart-core/Object/noSuchMethod.html) 
```dart title="Dart"
class A {
  // Unless you override noSuchMethod, using a
  // non-existent member results in a NoSuchMethodError.
  @override
  void noSuchMethod(Invocation invocation) {
    print('You tried to use a non-existent member: '
        '${invocation.memberName}');
  }
}
```




