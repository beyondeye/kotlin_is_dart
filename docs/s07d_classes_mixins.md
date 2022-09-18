# Mixins
For **Dart** see [here](https://dart.dev/guides/language/language-tour#adding-features-to-a-class-mixins). 
Mixins classes are not allowed to have a constructor.

**Kotlin** *does not have mixins*, but it has instead something similar that is called [delegation](https://kotlinlang.org/docs/delegation.html)
Also Kotlin [interfaces with method implementations](https://kotlinlang.org/docs/interfaces.html) can be used, in some cases, instead of mixins.

```kotlin title="Kotlin"
interface Person {
    val name:String
    val surname:String
}

// interface with method implentations and properties
// (but no actual data)
interface Musical : Person{
  var canPlayPiano:Boolean
  var canCompose:Boolean
  var canConduct:Boolean

  fun entertainMe() {
    println("${name} ${surname} is")
    if (canPlayPiano) {
      println("Playing piano")
    }
    if (canConduct) {
      println("Waving hands")
    }
    if (canCompose) {
      println("Humming to self")
    }
    println("")
  }
}

// MusicalImpl is the class  we will "delegate to" 
// for implementing the "Musical" interface.
// it is equivalent to the "Musical" mixin in Dart code
class MusicalImpl(
  override val name:String,override val surname:String):Musical {
  override var canPlayPiano:Boolean=false
  override var canCompose:Boolean=false
  override var canConduct:Boolean=false
}

// a class that has "Person" as superclass and
// delegate implementation of the "Musical" interface 
// to the MusicalImpl class
class Pianist(name:String, surname:String)
 : Musical by MusicalImpl(name,surname)
{
  init {
      canPlayPiano=true //from  "Musical" 
    }
}

// a class that has "Person" as superclass and
// delegate implementation of the "Musical" interface 
// to the MusicalImpl class
class Maestro(name:String, surname:String)
 : Musical by  MusicalImpl(name,surname)
{
  init {
    canConduct=true //from  "Musical"
  }
}

// a class that has "Person" as superclass and
// delegate implementation of the "Musical" interface 
// to the MusicalImpl class
class Composer(name:String, surname:String)
 : Musical by  MusicalImpl(name,surname)
{
  init {
    canCompose=true //from  "Musical" 
  }
}

var p=Pianist("Glenn","Gould")
var m=Maestro("Zubin","Mehta")
var c=Composer("Frédéric","Chopin")
c.canPlayPiano=true //chopin was also a virtuoso Pianist
  
p.entertainMe() //Glenn Gould is Playing piano
m.entertainMe() // Zubin Mehta is Waving hands
c.entertainMe() //Frédéric Chopin is Playing piano Humming to self
```

```dart title="Dart"
class Person {
  final String name;
  final String surname;
  Person(this.name,this.surname);
}

// a mixin in Dart
// defines a class that CANNOT BE instantiated, 
// but can be included in another class as a mixin
// with the "with" keyword
// the "on <class name>" class restricts the classes 
// that can use the mixin to only the classes that derives from
// some specific superclass, in this case "Person" 
// because the mixin implementation depends on
// the availability of fields and methods
// from that superclass
// All the mixin methods and fields will be available to the class that
// include it with the "with" keyword
mixin Musical on Person {
  bool canPlayPiano = false;
  bool canCompose = false;
  bool canConduct = false;

  void entertainMe() {
    print("${name} ${surname} is");
    if (canPlayPiano) {
      print('Playing piano');
    }
    if (canConduct) {
      print('Waving hands');
    }
    if (canCompose) {
      print('Humming to self');
    }
    print("");
  }
}



// a class that has "Person" as superclass and
// use the "Musical" mixin
class Pianist extends Person with Musical {
  Pianist(super.name,super.surname) {
      canPlayPiano=true; //from the "Musical" mixin
    }
}

// a class that has "Person" as superclass and
// use the "Musical" mixin
class Maestro extends Person  with Musical {
  Maestro(super.name,super.surname) {
    canConduct=true; //from the "Musical" mixin
  }
}

// a class that has "Person" as superclass and
// use the "Musical" mixin
class Composer extends Person  with Musical {
  Composer(super.name,super.surname) {
    canCompose=true; //from the "Musical" mixin
  }
}


var p=Pianist("Glenn","Gould");
var m=Maestro("Zubin","Mehta");
var c=Composer("Frédéric","Chopin");
c.canPlayPiano=true; //chopin was also a virtuoso Pianist
  
p.entertainMe(); //Glenn Gould is Playing piano
m.entertainMe(); // Zubin Mehta is Waving hands
c.entertainMe(); //Frédéric Chopin is Playing piano Humming to self
```

