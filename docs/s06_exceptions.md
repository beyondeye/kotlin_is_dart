# Exceptions
[**Dart**](https://dart.dev/guides/language/language-tour#exceptions) like [**Kotlin**](https://kotlinlang.org/docs/exceptions.html) does not have checked Exception.

In **Kotlin** only objects derived from [Throwable](https://kotlinlang.org/docs/exceptions.html#exception-classes) can be throwed.  **Dart** [can throw any object](https://dart.dev/guides/language/language-tour#exceptions), but it is recommended to always use [``Exception``](https://api.dart.dev/stable/dart-core/Exception-class.html), [``Error``](https://api.dart.dev/stable/dart-core/Error-class.html) and their subclasses. 

**Dart** ``Exception`` class contains ony a message, while ``Error`` has a message and a stack trace.
In **Kotlin** the base exception class ``Throwable`` has both a message and a stack trace.

[in **Dart**](https://dart.dev/guides/language/language-tour#throw) like [in **Kotlin**](https://kotlinlang.org/docs/exceptions.html#the-nothing-type)  throwing and exception is an expression, and can be placed anywhere where an expression can be placed.

```kotlin title="Kotlin"
class Exception1:Throwable()
class Exception2:Throwable()
class Exception3:Throwable()

//when an exception occurs in a try-block, the exception type is checked
//against each handler and the first one that matches is executed.
//the finally block is executed always, both if an exception occurred or not.
//There may be zero or more catch blocks, and the finally block may be omitted.
// However, at least one catch or finally block is required.
try {
    throw Exception3()
} catch (e1:Exception1) { //handler for Exception1
    println("Exception1 catched")
} catch (e2:Exception2) {  //handler for Exception2
    println("Exception2 catched")
} catch (e2:Exception3) {  //handler for Exception3
    println("Exception3 catched")    
} catch(e: Throwable) { //handler for all Throwable objects
    println("${e::class} catched")
    throw e //propagate the exception further
} finally {
    println("in finally block")
}
```

```dart title="Dart"
class Exception1 extends Error {}
class Exception2 extends Error {}
class Exception3 extends Error {}

try {
    throw Exception3();
} on Exception1 catch (e1,s1) { //handler for Exception1
    //[catch (e1) can be omitted] s1 is the stack trace
    print("Exception1 catched");
} on Exception2 catch (e2) {  //handler for Exception2
    //[catch (e2) can be omitted]
    print("Exception2 catched");
} on Exception3  {  //handler for Exception3
    print("Exception3 catched");
} catch(e) { //handler for all Throwable objects
    print("${e.runtimeType} catched");
    rethrow; //propagate the exception further
} finally {
    print("in finally block");
}
```
for more information on **Dart** exception handling see [library-tour](https://dart.dev/guides/libraries/library-tour#exceptions)