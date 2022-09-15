# Functions
## Simple functions
```kotlin title="Kotlin"
//standard syntax for function definition
fun addTwo(cur:Int):Int {
  return cur+2
}

println(addTwo(0)) //2

//omitting function return type is not allowed unless it is Unit
fun addArgs(arg1:Int,arg2:Int):Int {
  return arg1+arg2 //return Int
}

println(addArgs(1,2))  // 3

//if a function don't return a value, the type of the return value is Unit
fun returnUnit() {
  
}

println(returnUnit()) //Unit

//syntax for function that contains just an expression (no need to return type)
fun isEvent(number:Int) = number%2==0

println(isEvent(2)) //true

```

```Dart title="Dart"
//standard syntax for function definition
int addTwo(int cur) {
  return cur+2;
}

print(addTwo(0)); //2


//omitting function return type and/or argument types is allowed
// although not recommended for public APIs
// if types are not specified they are consider of type "dynamic"
addArgs(arg1,arg2) {
  return arg1+arg2;
}

print(addArgs("1","2")); //"12"
print(addArgs(1,2));  // 3



//All functions return a value. If no return value is specified
// the statement return null; is implicitly appended to the function body.
int? returnNull() {
  
}

print(returnNull()); //null


//syntax for function that contains just an expression
bool isEvent(int number) => number%2==0;

print(isEvent(2)); //true
```
??? info "function default return value is null"
    in **Dart** [default return value](https://dart.dev/guides/language/language-tour#return-values) is ``null`` . In **Kotlin** default return value is ``Unit``
??? info "it is possible to omit parameters types and/or return value"
    in **Dart** function parameters [with no specified type](https://dart.dev/guides/language/language-tour#functions) are considered ``dynamic``, and return type if not specified is considered ``dynamic``. In **Kotlin** parameter types must be specified, and also return value unless using the ``fun function(<params>) = <calculation>`` syntax


## Lambda functions

```kotlin title="Kotlin"

//lambda functions and functions as objects
val loudify = {msg:String -> "!!! ${msg.uppercase()} !!!"}

println(loudify("hello")) // "!!! HELLO !!!"



// lambda functions and functions as objects (with explicit return statement)
// remember that if types of arguments are not specified, they are considered
// of type "dynamic"
val joinArgs = { a:String,b:String,c:String -> a+b+c }

println(joinArgs("a","b","c")) //abc


/// Lexical closures:
/// Returns a function that adds [addBy] to the
/// function's argument.
fun makeAdder(addBy:Int):(Int)->Int {
  return {i:Int -> addBy + i}
}

var adder=makeAdder(2)
println(adder(2)) //4
```

```dart title="Dart"
//lambda functions and functions as objects
final loudify = (String msg) => '!!! ${msg.toUpperCase()} !!!';

print(loudify("hello")); // "!!! HELLO !!!"



// lambda functions and functions as objects (with explicit return statement)
// remember that if types of arguments are not specified, they are considered
// of type "dynamic"
final joinArgs = (a,b,c) { return a+b+c; };

print(joinArgs("a","b","c")); //abc


/// Lexical closures:
/// Returns a function that adds [addBy] to the
/// function's argument.
Function makeAdder(int addBy) {
  return (int i) => addBy + i;
}

var adder=makeAdder(2);
print(adder(2)); //4
```

## Named Arguments, Optional Positional Parameters

```Dart title="Dart"
// - A function can have any number of REQUIRED POSITIONAL parameters.
//   These can be followed either by NAMED parameters or by OPTIONAL 
//   POSITIONAL parameters (but not both).
// - Wrapping parameters in [] marks them as OPTIONAL POSITIONAL.
// - Wrapping parameters in {} marks them as (optional) NAMED parameters:
// - NAMED parameters annotated with "required" become mandatory parameters.
// - If a parameter is optional but can’t be null, provide a default value.
//   use the syntax: <Param> = <Value> to define default values. 
//   Default values must be compile-time constants.
//   If no default value is provided, the default value is null
int addWithNamedParameters(int a, {required int b, int c=0}) {
    var res=a+b+c;
      return res;
}

int addWithOptionalPositionalParameters(int a, [int b=0, int c=0]) {
    var res=a+b+c;
      return res;
}

print(addWithNamedParameters(1,b:2,c:3)); //6
print(addWithOptionalPositionalParameters(1)); //1
```

```kotlin title="Kotlin"
//actually in Kotlin any parameter can be a named parameter
fun addWithNamedParameters(a:Int, b:Int, c:Int=0):Int {
    var res=a+b+c
    return res
}

fun addWithOptionalPositionalParameters(a:Int, b:Int=0, c:Int=0):Int {
    var res=a+b+c
    return res
}

println(addWithNamedParameters(1,b=2,c=3)) //6
println(addWithOptionalPositionalParameters(1)) //1
```

