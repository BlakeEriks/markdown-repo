# Javascript

All data in javascript is either a primitive or an object.

**Primitives** represent actual data.  
* numbers
* strings
* booleans

**Objects** represent containers for data so when you store an object in a variable you are actually storing a reference to where the container exists in the computer's memory.
* Objects
* Functions
* Arrays
* Maps
* Sets
* Everything not a primitive

**Variables** can be declared in three ways which will effect whether the variable can change values and where does it exist.
* Const
    * Can't be reassigned
    * Block scoped
* Let
    * Can be reassigned
    * Block scoped
* Var
    * Can be reassigned
    * Global scoped unless function scoped

**Falsey Expressions**
* 0
* ""
* false
* null
* undefined
* NaN

**Arrays** store data in a set order, accessible via a numerical index starting with the number 0.

* Push() : add element to the end of the array
* Unshift() : add element to the beginning of the array.
* Pop() : remove last element from the array.
* Shift() : remove first element from the array.
* Splice(x,y,z) : starting at index x, remove y number of elements, and replace them with z
* Slice(start, end) : returns shallow copy of portion of an array selected from the start to end (end not included), where start and end are indexes in the array
* Join(delimiter) : creates and returns new string concatenating all elements in an array, separated by commas by default unless provided a different delimiter.

**Loops** are used to repeat the same block of code.

* For Loop
    * `for (let i = 0; i < pokemon.length; i++) {}`
* While Loop
    * `while (condition)`
* For Of Loop
    * Iterates through array elements
    * `for (poke of pokemon)`
* For in loop
    * Iterates through array indices
    * `for (poke in pokemon)`

**Functions** are like a spell. It can be used at any time and does magical things like add numbers, create objects and more.

#### Declaring a function:

##### Classic Function Notation  
>`function helloWorld() {}`

##### Anonymous Function
>`const helloWorld2 = function() {}`  

##### Arrow Function
>`const helloWorld3 = () => {}`

##### Default Parameters
``` 
const helloWorld = (name = "Blake") => {
   console.log('name');
}
 ```

 ##### Implicit Return

 `const sum = (x,y) => x + y`

 **Objects**  can store anything.

 ```
 const key = 'weapon';

 const robot = {
     name : 'BleepBlop',
     serial : 1,
     isEvil : false,
     'Gas Tank' : 'full',
     [key] : 'lazers'
 }
 ```

* Notice keys with spaces need to be in quotes.
* Can set dynamic keys with brackets -> see [key]

**Object Methods** are functions inside of an object
```
const obj = {
    prop: "Hello World",
    myFunc : () => console.log(`can i use this... ${this.prop}`),
    myFunc2 : function() {console.log(`can i use this... ${this.prop}`)},
    myFunc3() {console.log(`can i use this... ${this.prop}`)}
}

obj.myFunc();
obj.myFunc2();
obj.myFunc3();
```
This outputs:
```
can i use this... undefined
can i use this... Hello World
can i use this... Hello World
```
Arrow functions cannot use the **this** keyword!

**Object Oriented Programming** is built around:

* *Encapsulation*: abstracting an idea into a defined construct
* *Inheritance*: being able extend constructs to add functionality
* *Polymorphism*: The idea that on construct can be used in many ways 

A **class** allows use to pre-define an object before it's created and the kind of variables and functions that object can use.

```
class Animal {
    constructor(sound, ears, legs){
        this.sound = sound
        this.ears = ears
        this.legs = legs
    }
    makeSound(){
        console.log(this.sound)
    }
}
```

You can take advantage of inheritance and create a child class using the extends keyword.

```
class Pig extends Animal {
    constructor(name){
        super("oink", 2, 4)
        this.name = name
    }
    rollInMud(){
        console.log(`${this.name} rolls in mud and says ${this.sound}`)
    }
}
```

**Static** properties or methods belong to the class, not the instance.

```
class Pig extends Animal {

    static count = 0;

    constructor(){
        Pig.count++
    }

    static countPigs(){
        return Pigs.count
    }
}
```

Notice how **count** is referenced by the Class name, not the instance name. Static methods are required in order to access static properties.