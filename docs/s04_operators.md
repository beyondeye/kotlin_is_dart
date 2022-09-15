# Operators
## Arithmetic Operators
They are the same (``+ - * / %`` ) except for the **divide and return integer operator** ``~/``
```kotlin title="Kotlin"
//Divide two operands and give integer output
println((10.1).toInt() / 3); //3
```
```dart title="Dart"
//Divide two operands and give integer output
print(10.1~/3); //3
```
## Equality and Relational Operators
They are the same (``== != < <= > >= ``) 

## Reference equality
In **Dart** in order to check if two variables refers to the same class instance use ``identical``. 

In **Kotlin** use ``===``.
```kotlin title="Kotlin"
  var a = Point(1,1)
  var b = a
  assert(a===b)
```
```dart title="Dart"
  var a = Point(1,1);
  var b = a;
  assert(identical(a,b));
```
## Type Test and Type Cast Operators
The are the same except for  ``is!`` in **Dart** that is ``!is`` in **Kotlin**.
**Kotlin** has also the [safe cast operator ``as?``](https://kotlinlang.org/docs/null-safety.html#safe-casts)
```kotlin title="Kotlin"
//type cast
val pp:Any = 1
println(pp as Int + 2) //3

//type check
println(pp is Int) //true
println(pp !is Int) //false
```
```dart title="Dart"
//type cast
Object pp = 1;
print((pp as int) + 2); //3

//type check
print(pp is int); //true
print(pp is! int); //false

```
??? info "``is!`` instead of ``!is``"
    in **Dart** ``is!`` is the operator for testing if an object is NOT of a type. In **Kotlin**  it is ``!is`` which is actually the ``is`` operator, prefixed by the logical not ``!`` operator

## Assignment Operators
They are the same except for [assigment operator](https://dart.dev/guides/language/language-tour#assignment-operators) based on **Dart** bitwise operators `` << >> >>> ~ & |``  and the divide and return integer operator ``~/`` which [are not supported](https://kotlinlang.org/docs/operator-overloading.html#augmented-assignments) in **Kotlin** 
```kotlin title="Kotlin"
var a = 1
a+=1
println(a) //2
a-=1
println(a) //1
```
```dart title="Dart"
var a = 1;
a+=1;
print(a); //2
a-=1;
print(a); //1
```
## Logical Operator
They are the same (``&& || !`` )

## Bitwise and shift operators
**Kotlin** is known to use non-standard notations for bitwise and shift operators. So they are all different from **Dart** 
```kotlin title="Kotlin"
fun toHex(num:Int) = num.toString(16)

//bitwise AND
println(toHex(0xffff and 0xff)) //ff

//bitwise OR
println(toHex(0xfff0 or 0x0fff)) //ffff

//bitwise XOR
println(toHex(0xfff0 xor 0x0fff)) //f00f
  
//bitwise signed shift left
println(1 shl 2) //4      

//bitwise signed shift right
println(4 shr 2) //1      

//bitwise unsigned shift right
println(4 ushr 2) //1
  
//bitwise not
println(toHex(0xff00ff00.toInt().inv()) ) //ff00ff
```
```dart title="Dart"
String toHex(int number) => number.toRadixString(16);

//bitwise AND
print(toHex(0xffff & 0xff)); //ff

//bitwise OR
print(toHex(0xfff0 | 0x0fff)); //ffff

//bitwise XOR
print(toHex(0xfff0 ^ 0x0fff)); //f00f
  
//bitwise signed shift left
print(1 << 2); //4      

//bitwise signed shift right
print(4 >> 1); //1      
//bitwise unsigned shift right
print(4 >>> 1); //1      
  
//bitwise not
print(toHex(~0xff00ff00) ); //ff00ff
```
## Conditional expressions
**Dart** has the [conditional operator](https://dart.dev/guides/language/language-tour#conditional-expressions) **Kotlin**  has instead [if-else expression](https://kotlinlang.org/docs/control-flow.html#if-expression)
```kotlin title="Kotlin"
//conditional (ternary) operator
var smaller_than_ten=5
var bigger_than_ten=11
println (if(smaller_than_ten<10)  "smaller" else "bigger") //"smaller"
println (if(bigger_than_ten<10)  "smaller" else "bigger") //"bigger"
```
```dart title="Dart"
//conditional (ternary) operator
var smaller_than_ten=5;
var bigger_than_ten=11;
print (smaller_than_ten<10 ? "smaller": "bigger"); //"smaller"
print (bigger_than_ten<10 ? "smaller": "bigger"); //"bigger"
```
## Null coalescing operator (elvis operator)
**Dart** uses the [``??`` syntax](https://dart.dev/guides/language/language-tour#conditional-expressions) **Kotlin** uses the [``?:`` syntax](https://kotlinlang.org/docs/null-safety.html#elvis-operator).
```kotlin title="Kotlin"
var a:String?=null
var b="b"
println(a?:b); //"b"
a="a"
println(a?:b); //"a"
```
```dart title="Dart"
var a=null;
var b='b';
print(a??b); //'b'
a='a';
print(a??b); //'a'
```

## Member Access Operators
They are the same (``. ?.``)

## Cascade notation
In **Dart** [Cascades (.., ?..)](https://dart.dev/guides/language/language-tour#cascade-notation) allow you to make a sequence of operations on the same object.

in **Kotlin** there are instead the [``with`` and ``apply``](https://kotlinlang.org/docs/idioms.html#call-multiple-methods-on-an-object-instance-with) idioms.
```kotlin title="Kotlin"
var paint = Paint().apply {
  color = Colors.black
  strokeCap = StrokeCap.round
  strokeWidth = 5.0
}
```
```dart title="Dart"
var paint = Paint()
  ..color = Colors.black //no semicolon here!!
  ..strokeCap = StrokeCap.round //no semicolon here!!
  ..strokeWidth = 5.0;
```

## Not Null assertion operator
In **Dart** the [not null assertion operator](https://dart.dev/guides/language/language-tour#other-operators) is `!`. In **Kotlin** [it is ``!!``](https://kotlinlang.org/docs/null-safety.html#the-operator)
## Indexed access operator
It is the same (``[]``)

In **Dart** there is also the [conditional indexed access operator ``?[]``](https://dart.dev/guides/language/language-tour#other-operators). In **Kotlin** ``?[]`` is not supported, but the indexed operator can [specify more than one index](https://kotlinlang.org/docs/operator-overloading.html#indexed-access-operator).
## Invoke (function call) operator
It is the same ``()``.

In **Kotlin** when overridden is [``invoke``](https://kotlinlang.org/docs/operator-overloading.html#invoke-operator) while in **Dart** is [``call``](https://dart.dev/guides/language/language-tour#callable-classes)


