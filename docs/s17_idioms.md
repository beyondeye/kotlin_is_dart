# Idioms

## Copying a ``list``, a ``set``, a ``map``

```kotlin title="Kotlin" hl_lines="3 10 14"
var aList=listOf(1,2,3)
//also toList() work, but then the copy is immutable
var listCopy = aList.toMutableList()
listCopy.add(4)
println(aList) //1,2,3
println(listCopy) //1,2,3,4

var aMap = mapOf("a" to 1,"b" to 2,"c" to 3)
// also .toMap() works, but then the copy is immutable
var mapCopy = aMap.toMutableMap()

var aSet = setOf("a","b","c")
// also .toSet() works, but then the copy is immutable
val setCopy = aSet.toMutableSet() 

```

```dart title="Dart" hl_lines="2 8 11"
var aList=[1,2,3];
var listCopy = [...aList];
listCopy.add(4);
print(aList); //1,2,3
print(listCopy); //1,2,3,4

var aMap = {"a":1,"b":2,"c":3};
var mapCopy = {...aMap};
  
var aSet = {"a","b","c"};
var setCopy = {...aSet};
```

## checking parameters validity and assigning fields in constructor

```dart title="Dart" hl_lines="7"
class Rectangle {
  final double width;
  final double height;
  final double area;
  Rectangle(
    this.width,this.height
  ): assert(width>0),assert(height>0),area=width*height;
}
```
# copying a class with one or more modified fields

```kotlin title="Kotlin"
class Rectangle(val width:Double,val height:Double)
{
  fun copy(width:Double?=null, height:Double?=null) =
    Rectangle(
      width ?: this.width, 
      height ?: this.height
    )  
}

// in kotlin you can simply define a data class to have 
// the copy method automatically generated
data class Rectangle(val width:Double,val height:Double)
```


```dart title="Dart"
class Rectangle {
  final double width;
  final double height;
  Rectangle(this.width,this.height);
  
  Rectangle copy({double? width, double? height}) =>
    Rectangle(
      width ?? this.width, 
      height ?? this.height
    );
}
```

