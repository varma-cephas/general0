# 1.22.25, ES6
Arrow Functions
One difference between regular functions and arrow function expressions is thatarrow functions are always expressions infact, their full name is actually“arrow function expressions”, this mean that they can only be used where an expression is valid, which includes being:
stored in a variable
passed as an argument to a function.
stored in a object's property
const greet = name => `Hello ${name}!`;
when there's only one parameter in a function, you can write only that parameter name and exculde the parentheses..
some devs prefer to use underscore \_ instead of an empty bracket when to declare arrow functions that are not going to take any parameter.
when an arrow function is written in one line to return something, it is called the concise body syntax .
this syntax has no curly bracket around the function body
it automatically returns the expression.
when more than a single line of code is needed, the block body syntaxcan be used.
this syntax uses curly braces to wrap the function body
a return statement is needed to return someting from the array.
although arrow functions are useful, they should not be used when you have the following conditions:
this (a dynamic value depending on how a function is called) doesn't work normally as it should in arrow functions.
when this is used in arrow functions it depends on where the value(this) is called.
arrow functions are only `expressions`
arrow function declaration does not exist.

this and regular functions
the value of this depends completely on how it's function is called in regular functions
const mySundae = new Sundae('Chocolate', ['Sprinkles', 'Hot Fudge']);
in the above example, the value of this inside the Sundae contructor function is a new object cause it was called with new. (new object)

const result = obj1.printName.call(obj2);
in the example above, the value of this inside the printName() will refer to obj2 since the first parameter of call( ) is explicitly set to which ever this refers to. (specified object)

data.teleport()
in the example above, this refers to data

teleport( )
in the example above, the value of this refers to either the global object or if in strict mode, it's undefined .
this and Arrow Function
the value of this is based on the function's surrounding context in arrow functions. (meaning that the value of this inside an arrow function is the same value outside the function)

Default function paramenter
default parameters were introduced to es6 with the hope to help easy the task of writing default parameter. They can be written by:
function greet(name = 'Student', greeting = 'Welcome') {
return `${greeting} ${name}!`;
}

greet(); // Welcome Student!
greet('James'); // Welcome James!
greet('Richard', 'Howdy'); // Howdy Richard!
Defaults and destructuring arrays
combining default function function parameters with destructuring is a great way to create some powerful functions
function createGrid([width = 5, height = 5]) {
return `Generates a ${width} x ${height} grid`;
}

createGrid([]); // Generates a 5 x 5 grid
createGrid([2]); // Generates a 2 x 5 grid
createGrid([2, 3]); // Generates a 2 x 3 grid
createGrid([undefined, 3]); // Generates a 5 x 3 grid
from the above example, the function expects any array to be apssed to it, it then uses destructuring to set the first item to the width, and the second to the height.
when the createGrid() function is called without an argument, we can an error: `Uncaught TypeError:Cannot read property 'Symbol(Symbol.iterator)' of undefined`
this is because our functions expects an array which will then be destructured, since we called the function without an argument, the error is thrown. to fix this look at the code below.
function createGrid([width = 5, height = 5] = []) {
return `Generates a ${width} x ${height} grid`;
}
here we're using =[] to use an empty array as the default if the function is passed without an argument. which will allow our code to work.
Defaults and destructuring objects.
just like we can have default array parameters, we can have an object as a default parameter of a function and use object destructuring
function createSundae({scoops = 1, toppings = ['Hot Fudge']}) {
const scoopText = scoops === 1 ? 'scoop' : 'scoops';
return `Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.`;
}
as our previous function with default parameter throw an error when we tried to call it without a parameter before, this will also throw an error when it is called without an argument. We'll get an error as we did before, this time it is going to be `Uncaught TypeError:Cannot match against 'undefined' or 'null`. to fix, take a look at the code below:
function createSundae({scoops = 1, toppings = ['Hot Fudge']} = {}) {
const scoopText = scoops === 1 ? 'scoop' : 'scoops';
return `Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.`;
}
here we are adding ={} as an empty object, in the case no argument is provided, the function still works.

Default function parameter conclusion.
adding a default paramter to your functions is going to make your life much easier, one benefit of object defaults over array defaults is how they handle sktipped options. If you only want to use one of the dafault parameter, and assigned a value to the other, this is possible with object defaults.
However with arrays, you have to passed undefined to the position where you the default parameter to be used or skip over arguments.
unless you have a strong reason to use array defaults with array destructuring, it is recommended to always use object defaults with object destructuring. (javascript classes are a thin mirage of regular functions and prototypical inheritance)

Class preview
class, super, extend
javascript is `not a class based language` and it uses functions to create objects, and links objects together by prototypical inheritence.
What is prototypical inheritence?

Previous way to create a class in ES5
function Plane(numEngines) {
this.numEngines = numEngines;
this.enginesActive = false;
}

// methods "inherited" by all instances
Plane.prototype.startEngines = function () {
console.log('starting engines...');
this.enginesActive = true;
};

var richardsPlane = new Plane(1);
richardsPlane.startEngines();

var jamesPlane = new Plane(4);
jamesPlane.startEngines();
rewrite the entire hero section, you don't have to poke a stick in the dark, the webpage is right there, look at the properties. put the work in.


# 1.23.25, ES6
with the knowledge that classes are just a mirage to hide the fact that prototypal inheritence is actually going on, this is how classes were created back then in ES5
function Plane(numEngines) {
this.numEngines = numEngines;
this.enginesActive = false;
}

// methods "inherited" by all instances
Plane.prototype.startEngines = function () {
console.log('starting engines...');
this.enginesActive = true;
};

var richardsPlane = new Plane(1);
richardsPlane.startEngines();

var jamesPlane = new Plane(4);
jamesPlane.startEngines();
in the code above, the Plane function is a constructor function that will create new Plane objects.  
methods that are inherited by each Plane object are placed on the Plane.prototype object.
while richardsPlane is created with one engine, and jamesPlane is created with two, they both use te same method startEngines method to turn on their engines.
things to consider:
the constructor function is called with the new keyword.
the constructor function name starts with a capital letter
the constructor function controls the setting of data on the objects that will be created.
inherited methods placed on the constructor function's prototype object.
it is worth noting that ES6 classes are made of all the things mentioned above.

here's how the same Plane class would look like in the ES6 class syntax
class Plane {
constructor(numEngines) {
this.numEngines = numEngines;
this.enginesActive = false;
}

startEngines() {
console.log('starting engines…');
this.enginesActive = true;
}
}
in the above code, the startEngine method is on the prototype of the Plane class, while the constructor method is a new special method that exists in the class that is used to initialize new object.
the class syntax is just a nicer way that was introduced to be used, instead of using functions as constructors.

Classes are just functions.
class Plane {
constructor(numEngines) {
this.numEngines = numEngines;
this.enginesActive = false;
}

startEngines() {
console.log('starting engines…');
this.enginesActive = true;
}
}

typeof Plane; // function
it's just a function dawg, there's no new type of class in ES6 or JS in general.

Static methods
to add a static method, add the static keyword in front of the class name.
class Plane {
constructor(numEngines) {
this.numEngines = numEngines;
this.enginesActive = false;
}

static badWeather(planes) {
for (plane of planes) {
plane.enginesActive = false;
}
}

startEngines() {
console.log('starting engines…');
this.enginesActive = true;
}
}
to add the badWeather() method directly to the Plane class, the static keyword should be used.
big update boys, the functions or variables or objects declared with the static keyword in a class means that you can only access that function, variable, or object on the class itself, and not the instance of that that class, say using the new keyword to instantiate an instace.
Benefits of classes
there is lesss code that you need to write to create a function.
you can clearly define the constructor function inside of the class definition.
all the code that is needed for a particular class is contained in the class declaration, instead of having one constructor function in one place, and adding methods to the prototype at a time, you can do everything at once.

Things to consider when using classes
they are not magic, the classes keyword brings with it a lot of mental construct from other class based language. it doesn't add this functionality to JS classes.
class is just a mirage over prototypal inheritance. under the hood, JS classes JS classes just uses prototypal inheritance(which is object inheriting from other objects)
using classes always requires the use of the new keyword, that is when creating a new instance of a JS class, the new keyword must be used.
class Toy {
...
}

const myToy1 = Toy(); // throws an error
const myToy2 = new Toy(); // this works!

Subclasses with ES6
now that you understand how classes are created, look at the use of the super and extend keyword to extend a class.
class Tree {
constructor(size = '10', leaves = {spring: 'green', summer: 'green', fall: 'orange', winter: null}) {
this.size = size;
this.leaves = leaves;
this.leafColor = null;
}

changeSeason(season) {
this.leafColor = this.leaves[season];
if (season === 'spring') {
this.size += 1;
}
}
}

class Maple extends Tree {
constructor(syrupQty = 15, size, leaves) {
super(size, leaves);
this.syrupQty = syrupQty;
}

changeSeason(season) {
super.changeSeason(season);
if (season === 'spring') {
this.syrupQty += 1;
}
}

gatherSyrup() {
this.syrupQty -= 3;
}
}

const myMaple = new Maple(15, 5);
myMaple.changeSeason('fall');
myMaple.gatherSyrup();
myMaple.changeSeason('spring');
the code above, both classes are JS classes. the Maple class however is a subclass of Treeand uses the extendskeyword to set itself as a subclass.
to get from subclass to parent class, the super keyword isused.
super is used two ways though, in the Maple's constructor method, super is used as a function. In the Maple 's changeSeason() method, superis used as an object.
ES5 Subclasses with the same functionality above as subclasses in es6
function Tree(size, leaves) {
this.size = (typeof size === "undefined")? 10 : size;
const defaultLeaves = {spring: 'green', summer: 'green', fall: 'orange', winter: null};
this.leaves = (typeof leaves === "undefined")? defaultLeaves : leaves;
this.leafColor;
}

Tree.prototype.changeSeason = function(season) {
this.leafColor = this.leaves[season];
if (season === 'spring') {
this.size += 1;
}
}

function Maple (syrupQty, size, leaves) {
Tree.call(this, size, leaves);
this.syrupQty = (typeof syrupQty === "undefined")? 15 : syrupQty;
}

Maple.prototype = Object.create(Tree.prototype);
Maple.prototype.constructor = Maple;

Maple.prototype.changeSeason = function(season) {
Tree.prototype.changeSeason.call(this, season);
if (season === 'spring') {
this.syrupQty += 1;
}
}

Maple.prototype.gatherSyrup = function() {
this.syrupQty -= 3;
}

const myMaple = new Maple(15, 5);
myMaple.changeSeason('fall');
myMaple.gatherSyrup();
myMaple.changeSeason('spring');

Working with subclasses
like most of the new stuff in ES6, a lot less code isrequired to set up some code, and the syntax is alot cleaner to create subclasses using the class , super , and extend keywords.
remember though that under the hood, the same connections are made between functions and prototypes
super must be called before this
in a subclass constructor function, before this can be used, a call on the super or parent class must be made.
class Apple {}
class GrannySmith extends Apple {
constructor(tartnessLevel, energy) {
this.tartnessLevel = tartnessLevel; // `this` before `super` will throw an error!
super(energy);
}
}
objects that are instantiated from classes, that are also sub classes of other parent classes, are also instances of those objects.

Directions:
Create aBicyclesubclass that extends theVehicleclass. TheBicyclesubclass should overrideVehicle's constructor function by changing the default values forwheelsfrom4to2andhornfrom'beep beep'to'honk honk'.
class Vehicle {
constructor(color = 'blue', wheels = 4, horn = 'beep beep') {
this.color = color;
this.wheels = wheels;
this.horn = horn;
}

    honkHorn() {
    	console.log(this.horn);
    }

}

// your code goes here
class Bicycle extends Vehicle{
constructor(color="blue", wheels=2, horn="honk honk"){
super(color, wheels, horn)
this.wheels = wheels;
this.horn = horn;
this.color=color;
}
}
///_ tests
const myVehicle = new Vehicle();
myVehicle.honkHorn(); // beep beep
const myBike = new Bicycle();
myBike.honkHorn(); // honk honk
//_/

1. work only on codewars exercises that has something to do with the concepts that you are learning
   write the name of the topic that you'll on and add exercises github.com to the title to get good quality exercises to work on. e.g. class exercises: github.com
   look at things like padding and margin on the original website to make stuff responsive.


# 1.24.25, ES6
dude waait, sets maps and promises are all built in!!!! these built-ins make it more easy to execute tasks that were once more difficult in ES5. there's also appropriate time to use them and not to.
Symbols
symbols are a latest addition to a list of primitive data types in js.
symbols are basically just a unique identifier, it is most often used to indentify properties within an object. (in my own words, I think they help when you have multiple objects properties that has the same name and you uniquely want to identify them.)  
by def: a symbol is a unique and immutable data type that is used to identify object properties.
to create one: use Symbol() , it's optional to pass a string as it's description.
const sym1 = Symbol('apple');
console.log(sym1);
//logs Symbol(apple)
the above code will create a unique symbol and store it in the variable sym1 . The description apple is just a way to describe the symbol, but it's can't be used to access the symbol itself.
const sym2 = Symbol('banana');
const sym3 = Symbol('banana');
console.log(sym2 === sym3);
//logs false
the above code proves that because the description is only used to describe the symbol, and it's not a part of the symbol itself.

const bowl = {
'apple': { color: 'red', weight: 136.078 },
'banana': { color: 'yellow', weight: 183.151 },
'orange': { color: 'orange', weight: 170.097 },
'banana': { color: 'yellow', weight: 176.845 }
};
console.log(bowl);
consider that we want to add another banana to the code above, if we do, we'll basically be overriding the previous banana. To fix this however, we can introduce symbols.
const bowl = {
[Symbol('apple')]: { color: 'red', weight: 136.078 },
[Symbol('banana')]: { color: 'yellow', weight: 183.15 },
[Symbol('orange')]: { color: 'orange', weight: 170.097 },
[Symbol('banana')]: { color: 'yellow', weight: 176.845 }
};
console.log(bowl);

//logs Object {Symbol(apple): Object, Symbol(banana): Object, Symbol(orange): Object, Symbol(banana): Object}
in the above code, we're chaning the bowl's properties to use symbols. Each one of the property is a unique Symbol and the first banana does not overwrite the second one.
Iteration and iterable protocols
these protocols are not directly built-ins, but they help to understand the concept of iteration in ES6, and also show a use case for symbols.
iterable protocol
used for definiing and customizing the iteration behavior of objects... in order words, we now have the flexibility of specifying a way for interating through values in object in ES6.
some objects already come with this built-in behaviour. e.g. strings and arrays are examples of built-in iterables.
How it works
for a object to be iterable, it must implement the iterable interface first (which basically mean that, "for an object to be iterable, it must contain a default iterator method"). This method will then define how the object should be iterated.
the iterator method, which is available via the constant [Symbol.iterator] ,is a zero argument function that returns an iterator object. An iterator object is an object that conforms to the iterator protocol.
iterator or iteration protocol
used to define a standard way that an object produce a sequence of values.... in other words, we now have a process for defining how an object will iterate. This is done by implementing the .next() method.
how it really works
an object becomes an iterator when it uses or implement the .next() method. the .next() method is a zero argument function that returns an object with two properties:
value - refers to the data representing the next value in the sequence of values within the object.
done - refers to a boolean if the iterator is done goign through the sequence of values.
when done is true, the iterator has reached the end of the sequence of values.
Example combining both iterator and iterable protocol.
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
const arrayIterator = digits[Symbol.iterator]();

console.log(arrayIterator.next());
console.log(arrayIterator.next());
console.log(arrayIterator.next());

//logs Object {value: 0, done: false}
//logs Object {value: 1, done: false}
//logs Object {value: 2, done: false}

Sets
def: in mathematics, set is a collection of distinct items. e.g. {2,4,5,6} is a set because each number is unique and only occur once. {1,2,2,5} is not a set cause it contain duplicate items(two appears more than once)
in JS, we can represent something similar to a mathematical set using an array.
const nums = [2, 4, 5, 6];
nums.push(2);
console.log(nums);
//logs: [2, 4, 5, 6, 2]
in the code above, nums started as an mathematical set, but pushing stuff to it removed that fact.
in ES6, we have a new built-in object which acts like a mathematical set and works very closely to an array, which is called Set. The main differences between set and arrays are:
Sets are not indexed based. meaning that you can't refer to an item in a Set based on their position in Set.
items in a Set can't be accessed individually.
to put it simply, a Set is an object that let's you store unique items.
you can either add items to a Set, remove items from a Set, or loop over a Set.
Creating sets
there are multiple ways to create a Set:
const games = new Set();
console.log(games)
//logs Set {}
the code above creates an empty set

const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);
console.log(games);
//logs Set {'Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart'}
in the above example, the duplicate entry is removed when the Set is created. AWESOME.
Modifying Sets
after a set has been created, we would probably want to modify it by adding and removing elements. this can be done with the .add() and .delete() methods.
const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);

games.add('Banjo-Tooie');
games.add('Age of Empires');
games.delete('Super Mario Bros.');

console.log(games);
//logs Set {'Banjo-Kazooie', 'Mario Kart', 'Banjo-Tooie', 'Age of Empires'}

games.clear()
console.log(games);
//logs Set {}
in the above code, we're using the .add() and .delete() method to add and remove items from our Sets.
.add() returns a Set if the item is successfully added.
note that you can only add one item to a Set at a time.
.delete() on the other hand will return Boolean(true or false) depending on graceful deletion.
to delete all items for a Set, the .clear() method is happy to serve us.
one thing to remember is that, if we try to use .add() to add a duplicate item to our Set, we won't recieve an error, but that item is not going to be added. .delete() also works similarly, if we try to delete an item that doesn't exists in a Set, we won't get an error, but the Set will remain unchanged.




# 1.24.25, ES6
Working with sets
to check the length of a Set, we can summon the .size property which is going to return the number of items in a Set, you can think of it as array.length is to getting the length of an array .
const months = new Set(['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']);
console.log(months.size);
//logs 12
to check if an item is included or exists in a Set, we can use the .has() method. This method returns a boolean, true if it's inlcuded, or false if it's not.
console.log(months.has('September'));
//logs true
to return the values in a Set, we can use the .values() method which happily gives us back has a SetIterator object.
console.log(months.values());
//log SetIterator {'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'}
do note that .key() method behaves the exact way that .value() does by returning values in the Set within a new iterator object .
Looping over Sets
first thing to note is that Sets are built-in iterables. Which means we have two good news,
we can use the Set's default iterator to go through each item in Set one step at a time.
we can use the freshly baked for...of loop to loop through each every item in a Set.
Making use of the SetIterator.
the fact that the .values() method is going to give us aback a new iterator object called (SetIterator) we can store that iterator object in a variable, and loop through each item in that Set using .next() .
const iterator = months.values();
iterator.next();
//logs Object {value: 'January', done: false}
when we run .next() again, we get:
iterator.next();
Object {value: 'February', done: false}
the done key is going to continue to be false until we reach the end of the Set.
Finally, the for...of for Sets
the more easier way to loop through items in a Set is through the usuage of the for...of loop.
const colors = new Set(['red', 'orange', 'yellow', 'green', 'blue', 'violet', 'brown', 'black']);
for (const color of colors) {
console.log(color);
}
//logs
/_
red
orange
yellow
green
blue
violet
brown
black
_/
Working with WeakSet?
a WeakSet works like a normal Set, but there are a couple differences:
WeakSets can only contain object
WeakSets is not iterable by default, meaning we can't gracefully loop through them
WeakSets doesn't have a .clear() method.
to create a WeakSet , we can follow the same syntax as we would when creating a Set, the major difference is that we use the WeakSet constructor instead.
let student1 = { name: 'James', age: 26, gender: 'male' };
let student2 = { name: 'Julia', age: 27, gender: 'female' };
let student3 = { name: 'Richard', age: 31, gender: 'male' };

const roster = new WeakSet([student1, student2, student3]);
console.log(roster);
//logs
/_
WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'Richard', age: 31, gender: 'male'}, Object {name: 'James', age: 26, gender: 'male'}}
_/
however, when we try adding something other than an object, we're going to get rejected by our darling, the WeakSet
roster.add('Amanda');
//logs Uncaught TypeError: Invalid value used in weak set(…)
this is to be expected however be WeakSets can only contain objects.
one reason to use WeakSets over the regular Set is that WeakSet don't have a .clear() method.
Garbage collection
in JS, memory is allocated when new values are created, and automatically freed up when those values are no longer needed. The process of freeing up memory when is no longer needed is called garbage collection.
WeakSets takes advantage of this only working with objects. Whenever you set an object to null , we're basically deleting that object.
when the JS garbage collector runs, the memory that object previously occupied will then be freed or opened up to be used later in your program.
student3 = null;
console.log(roster);
//logs WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'James', age: 26, gender: 'male'}}
in the code above, setting an object that already exists in a WeakSet to null removes that object from the WeakSet.
in essence, this is useful because we don't have to worry about deleting references in order to delete objects from our WeakSet, we can simply set that object to null, and JavaScript does it for us. When an object is deleted, that object will also be deleted from the WeakSet when the garbage collector run. This makes them incredibly convenient in situtations where we want an efficient, lightweight solution for creating groups of objects.
it will also be eye opening to check MDN's documentation to learn about the algorithms used to handle garbage collection in JS: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management#Garbage_collection



# 1.27.25, ES6
Creating and Modifying Maps
if Sets are similar to Arrays, Maps similar to Objects cause they are able store values in key-value pairs, similarly to how objects do.
basically a Map is an object that lets you store key-value pairs, where both the keys and values can be objects, primitive values, or the combination of two;
to create one, use:
const employees = new Map();
console.log(employees);
//logs
//Map {}
the above code is used to create an empty Map employee with no key-value pairs.
Maps Modification
not like Sets, we can't create Maps from a list of value, we have to add key-values by using Map's .set() method.
const employees = new Map();

employees.set('james.parkes@udacity.com', {
firstName: 'James',
lastName: 'Parkes',
role: 'Content Developer'
});
employees.set('julia@udacity.com', {
firstName: 'Julia',
lastName: 'Van Cleve',
role: 'Content Developer'
});
employees.set('richard@udacity.com', {
firstName: 'Richard',
lastName: 'Kalehoff',
role: 'Content Developer'
});

console.log(employees);
//logs
//Map {'james.parkes@udacity.com' => Object {...}, 'julia@udacity.com' => Object {...}, 'richard@udacity.com' => Object {...}}
in the above code, the .set() method takes two arguments, first in line is a key, which is mostly used to reference the second argument, the value.
the .set() method when used to set a key-value pair to a Map that already exists with the same key-value pair, we won't recieve an error, but rather the existing key value pair will be overwritten by the new one.
.set() is going to return the map object itself.
to remove key-value pairs,we can use the .delete() method.
employees.delete('julia@udacity.com');
employees.delete('richard@udacity.com');
console.log(employees);
//logs
//Map {'james.parkes@udacity.com' => Object {firstName: 'James', lastName: 'Parkes', role: 'Course Developer'}}
in the code above, we're using the .delete() method to remove key-value pairs from the Map
when you call .delete() method on a key-value pair that doesn't exists in a Map, no error is going to be recieved, and the Map shall remain unchanged.
the .delete() method is going to return trueif the key-value pair is sucessfully deleted from the Map object, and false if the operatoin is unsuccessful.
to remove all items from a set, we can use the .clear() method to remove all the key-value pairs from the set because their rent is finished. see example below:
employees.clear()
console.log(employees);
//logs Map {}
the .has() method can be used to check if a key-vaue pair exists in a Map.
const members = new Map();

members.set('Evelyn', 75.68);
members.set('Liam', 20.16);
members.set('Sophia', 0);
members.set('Marcus', 10.25);

console.log(members.has('Xavier'));
console.log(members.has('Marcus'));
//logs
//true
//false
We can use the .get() method to obtain values from a Map
console.log(members.get('Evelyn'));
//logs 75.68

Looping through Maps
After we have created Maps, added key-value pairs to them, the next thing that we would want to do is loop through the Map.
we have three different items on the menu when it comes to that:
Map's default iterator
with the help of both the .keys() and .value() method, we can use them to return a new iterator object called MapIterator .
We can then store that iterator object into a new variable, and use the .next() method to loop through each key or value pair. note that which method you use will determine if the iterator has access to the Map's keys or values
let iteratorObjForKeys = members.keys();
iteratorObjForKeys.next();
//logs Object {value: 'Evelyn', done: false}
iteratorObjForKeys.next();
//logs Object {value: 'Liam', done: false}

//we can basically do the same for values
let iteratorObjForValues = members.values();
iteratorObjForValues.next();
//logs Object {value: 75.68, done: false}

using the for...of loop, which returns an array of the Map key value pairs
for (const member of members) {
console.log(member);
}
//logs
/_
['Evelyn', 75.68]
['Liam', 20.16]
['Sophia', 0]
['Marcus', 10.25]
_/
to fix this, we can use destructuring to return the key, value pairs as they are.
using the forEach loop, by using the .forEach method
members.forEach((value, key) => console.log(key, value));
//logs
/_
'Evelyn' 75.68
'Liam' 20.16
'Sophia' 0
'Marcus' 10.25
_/
in the above code, we're basically adding the value and key to the callback and logging that out.
WeakMaps introduction
a WeakMap works very similarly to a normal Map, but there are sevreal differences,
they contain only objects as keys.
they are not iterable, which means that they can't be looped through.
they don't have a .clear() method.
to create a WeakMap we can use the same procedure as we would for a Map except would use the WeakMap constructor.
const book1 = { title: 'Pride and Prejudice', author: 'Jane Austen' };
const book2 = { title: 'The Catcher in the Rye', author: 'J.D. Salinger' };
const book3 = { title: 'Gulliver’s Travels', author: 'Jonathan Swift' };

const library = new WeakMap();
library.set(book1, true);
library.set(book2, false);
library.set(book3, true);

console.log(library);
//logs
/_
WeakMap {Object {title: 'Pride and Prejudice', author: 'Jane Austen'} => true, Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver’s Travels', author: 'Jonathan Swift'} => true}
_/
in the above code, we're creating a couple objects and using the .set() method to add them to the WeakMap.4
if we try to add anything other than an object as a key, we're going to get an error. Remember both WeakMaps and WeakSets leverage garbage collection for ease of use and maintainability.
Weakmaps take advantage for this by working with objects as keys. Again, setting an object to null is like saying we want to delete that object, this is because when the garbage collector runs, the memory that object occupied previously will be freed up to be later used in your program.
this is useful becuase we don't have to wrry about deleting keys that are refrencing a deleted object in WeakMaps, because JavaScript does it for us.
library.set('The Grapes of Wrath', false);
//logs an error: Uncaught TypeError: Invalid value used as weak map key(…)

book1 = null;
console.log(library);

//logs
//WeakMap {Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {tit



# 1.28.25, ES6
Promises
promises helps solve some tricky problems in JS. using promises is a way to handle asyncronous request.
it's an improvement to the way that code was structured in the past.
going back and forth from making a request for something, to the downtime to when that request is fulled, and then doing work while that request is being fulfilled and being notified, when that request is finally fufilled, is what promises do for us in JS.
in short, we're saying do this thing now and notify me when it's done, so that I don't have to stop work to wait for the thing I asked for.
last example, say we're at a coffee shop and working, the barista might approach us to ask us for which coffee we would like, let's say we pick a black ice coffee. in this instance, the barista is not immediately giving us the coffee, but instead giving us the promise that we might get our coffee. this is beautiful because we don't have to sit there and wait for the barista to bring the coffee, that would be a might waste of time, we can instead continue working, and whenever the barista returns with the coffee, that orginal promise that the barista gaved us has been gracefully fufilled.
A Promise is created with the Promise constructor function - new Promise() , basically a promise will allow you to start some work that will done asynchronously and let you get back to your regular work as the barista would.
when one is created, we must give it some code thta will run asyncronously, which can be provided as an argument to the constructor function.
new Promise(function () {
window.setTimeout(function createSundae(flavor = 'chocolate') {
const sundae = {};
// request ice cream
// get cone
// warm up ice cream scoop
// scoop generous portion into cone!
}, Math.random() _ 2000);
});
in the code above, we are creating promise that will start in a few after the request is made.
Was the coffe request resolved or Reject!
when our code is done executing, JS has to let us know that it is actually done, in two ways, was the promise gracefully resolved or reject.
the function which we passed to the Promise constructor, can have two functions: you guessed it, resolve and reject.
new Promise(function (resolve, reject) {
window.setTimeout(function createSundae(flavor = 'chocolate') {
const sundae = {};
// request ice cream
// get cone
// warm up ice cream scoop
// scoop generous portion into cone!
resolve(sundae);
}, Math.random() _ 2000);
});
in the above code, when the sundae is successfully created, it calls the resolve method and passes the data we want to return.
in short, resolve is used to indicate that the request was successfully completed.

when there is a problem, say there was an shortage of coffee at the coffee shop, and the promise made by the barista could not be successfully fufilled, then we could use the second identifier function reject .
new Promise(function (resolve, reject) {
window.setTimeout(function createSundae(flavor = 'chocolate') {
const sundae = {};
// request ice cream
// get cone
// warm up ice cream scoop
// scoop generous portion into cone!
if ( / _iceCreamConeIsEmpty(flavor)_ / ) {
reject(`Sorry, we're out of that flavor :-(`);
}
resolve(sundae);
}, Math.random() \* 2000);
});
in the code above, we are using the reject method to let us know that the promise will not be fulfilled so that we are not infinitely waiting. simply, when the request fails, we can still return data. i
in the current case we're just returning a text that says that the desired flavor is not available.
IN CONCLUSION: a promise constructor will take a function that will run and after some time, either complete successfully our request, (uisng the resolve method) or (reject using the reject method).
when the outcome has been finalized, the promise is now fufilled and we will be notified so we can decide what to do, in this case, either leave the coffee shop or order something doordash and use their wifi for free 😂.
Promises return immediately
it is important to understand that a promise will immediately return an object.
const myPromiseObj = new Promise(function (resolve, reject) {
// sundae creation code
});j
that object has a .then() method attached to it that we can use to notify us if the request we made was successful or failed.
we can use that then()method to notify us if the request that we made in the promise failed or was successful. the .then() method takes two functions:
the function that will run if the request is finished successfully
the function to run if the request fails
mySundae.then(function(sundae) {
console.log(`Time to eat my delicious ${sundae}`);
}, function(msg) {
console.log(msg);
self.goCry(); // not a real method
});
in the above code, the first function is passed to the .then() method that will be called and the data will be passed that the promise resolve function called, assuming that the function recieves the sundae object.
the second function will be called and passed the data that the promise reject function was called with. Here, our function recieves the error message and says that are request was not successful, and that the rejectfunction was called.

Proxies
proxies basically let one object stand in for another object, to handle for the interactions for that object.
the proxie can handle request directly, pass data back and forth to the target object, and do a lot more.
on thing that keeps recurring is that most builtins are built into a constructor.
to create a proxy, we can use the Proxy constructor, which takes about two item.
the object that it will be a proxy for
an object that will contain the list of methods that will be handled for the proxied object.
the second object is called a handler btw.
the easiest way to create a proxy is to provide an object and an empty handler object.
var richard = {status: 'looking for work'};
var agent = new Proxy(richard, {});

agent.status; // returns 'looking for work'
the code above, we're basically ceating a an object richard, a variable agent, then creating an instance of the Proxy constructor, to point to the richard object, which is the source of of our proxy instace. not much!
what if we wanted the proxy object to intercept the request, that's what the handler object is for.
the key to making proxies useful is the handler object that is passed as a second object to the Proxy constructor. The handler object is made up of special methods that will be used for property access.
Get Trap
get trap is used to "block" calls to the properties
const richard = {status: 'looking for work'};
const handler = {
get(target, propName) {
console.log(target);
console.log(propName);
return target[propName];
}
};
const agent = new Proxy(richard, handler);
agent.status; // (1)logs the richard object, (2)logs the property being accessed, (3)returns the text in richard.status
in the code above, take a look at the return statement, we added return target[propName] as the lsat line of the get trap. this is going to access the property of the target object and return it.

we can the proxy return stuff directly by:
const richard = {status: 'looking for work'};
const handler = {
get(target, propName) {
return `He's following many leads, so you should offer a contract as soon as possible!`;
}
};
const agent = new Proxy(richard, handler);
agent.status; // returns the text `He's following many leads, so you should offer a contract as soon as possible!
in the code above, the Proxy is not going to check the target object, but rather just directly respond calling code.
in order words the get trap will take over when any property on the when the proxy is called. if we want to intercept calls to specific propertie, then we weed to use the set trap
Set Trap
the set trap is used for intercepting code that will change a property. the set trap recieves the following parameters:
the object it proxies, the property that is being set, and the new value for the proxy.
const richard = {status: 'looking for work'};
const handler = {
set(target, propName, value) {
if (propName === 'payRate') { // if the pay is being set, take 15% as commission
value = value \* 0.85;
}
target[propName] = value;
}
};
const agent = new Proxy(richard, handler);
agent.payRate = 1000; // set the actor's pay to $1,000
agent.payRate; // $850 the actor's actual pay
in the above code, the set trap looks to see if the payRate property is being set. If that is the case, the proxy takes 15% off the top for their own. In summary when the actor's pay is set to one thousand dollars, and since the payRate property was used, the code took 15% off the top and set the actual payRate to 850

So far, we've seen the get and set traps, but there are many more different traps, actually 13 different traps that can be used in a handler. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy

Proxies vs. ES5 Getter/Setter
at first. it can seem like it's non beneficial to use proxies when you already have the getter and setter methods that is given by ES5.
the catch is before using ES5 getter and setter methods, you'll first need to know beforehand which or what properties are going to be get/set
var obj = {
\_age: 5,
\_height: 4,
get age() {
console.log(`getting the "age" property`);
console.log(this.\_age);
},
get height() {
console.log(`getting the "height" property`);
console.log(this.\_height);
}
};
in the code above, notice that we have to set get age() and get height() when initializing the object, so when the code is called, we can get the following result
obj.age; // logs 'getting the "age" property' & 5
obj.height; // logs 'getting the "height" property' & 4
consider that we added a new property to the object:
obj.weight = 120; // set a new property on the object
obj.weight; // logs just 120
take note that our new weight property that was added to the object was not displayed like the ageand height property
However with ES6 Proxies, we do not need the property before hand:
const proxyObj = new Proxy({age: 5, height: 4}, {
get(targetObj, property) {
console.log(`getting the ${property} property`);
console.log(targetObj[property]);
}
});

proxyObj.age; // logs 'getting the age property' & 5
proxyObj.height; // logs 'getting the height property' & 4
everything looks good so far, just like our previous getter and setter from ES5, but see what happens when we add a new property:
proxyObj.weight = 120; // set a new property on the object
proxyObj.weight; // logs 'getting the weight property' & 120
in the code above, we notice that we the weight property was added to the proxy object, and when it was later retrieved, it logged a log message.
although some functionality of proxy objects may seem similar to the existing getter/setter methods, we don't need to initialize the object with getters and setters for each property when the object is initialized.
IN CONCLUSION: a proxy object sits between a real object and the calling code. The calling code iteracts with the proxy instead of the real object.
to get started with them:
use the new Proxy() constructor.
pass the object being proxied as the first item to the constructor
the second object is a handler object.
the handler object has 13 different "traps"
a trap is a function that will intercept calls to properties to let you run code.
if a trap is not defined, the default behavior is sent to the target object.
Proxies are a beautiful way to create and manage the interactions between objects.




# 1.29.25, Generators
when a function get's invoked, the JS engine starts from the top of the function, and runs every line until it get's to the bottom. There's no way to stop the execution of that function in the middle to pick up again at some point later on. This run to completion is how things have always been.
function getEmployee() {
console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        console.log(name);
    }

    console.log('the function has ended');

}

getEmployee();
running the code above logs the following:
the function has started
Amanda
Diego
Farrin
James
Kagure
Kavita
Orit
Richard
the function has ended
what if we wanted to first log out the first 3 employee names and stop for a bit, then pick up the function again from where we left off, and print out more of employee names. There's currently no way to do this with regular functions.
Pausable Functions
if we want to be able to pause a function in a middle, while it's executing, we can use a new type of function available to use in ES6 - generator function! take a peek at one below, and make it long:
function\* getEmployee() {
console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        console.log( name );
    }

    console.log('the function has ended');

}
while you were taking a peek, I'm sure you noticed that you noticed that there's an asterick (\*) right after the function keyword. that asterick is indicating to us that the function is actually a generator.
note that the asterisk can be placed anywhere between the function, and the name of the function. keeping the asterisks is goin gto be prescribed for us.
this is what happens when we run the function:
getEmployee();

// this is the response I get in Chrome:
getEmployee {[[GeneratorStatus]]: "suspended", [[GeneratorReceiver]]: Window}
when we call the code above, we actually get something interesting, and iterator object.
Generators & Iterators
when generator functions are invoked, they don't immediately any of the code inside of the function, instead they create and return an iterator.  
const generatorIterator = getEmployee();
generatorIterator.next();
the code above logs the following:
the function has started
Amanda
Diego
Farrin
James
Kagure
Kavita
Orit
Richard
the function has ended
the first time the iterator's .next() method was called, it ran all the code that was placed in the generators.
The Yield keyword
the yield keyword was newly introduced in ES6, it can only be used in a generator function. yeild is what causes our gene

Exporting and Importing in ES6:
In ES6, you can export variables or functions using Default or Named Exports.
Default Export:

- const greetings = "Hi there"
  export default greetings

Named Export:
export const greetings = "Hi there baby"

Additionally:
Default Imports:

- import greetings from `./greeetings.js`
  console.log(greetings) //logs "Hi there"

Named Import:
import { greetings } from `./greeetings.js`
console.log(greetings) //logs "Hi there baby"

class File {
// Write your code here :D
constructor(fullName,content, filename, extension){
this.\_fullName = fullName;
this.\_filename = filename;
this.\_extension = extension;
this.\_content = content;
}

get fullName(){
return `${this._fullName}`
}

getFileNameExtension(){
const fullNameArr=this.fullName.split("");
let fileExtension=[];
for(let i=fullNameArr.length;i>0;i--){
if(fullNameArr[i]==="."){
fullNameArr.splice(i, 1);
break;
}else{
fileExtension.push(fullNameArr.splice(i, 1))
}
}
fileExtension.reverse();
return {"fileName":fullNameArr.join(""), "fileExt":fileExtension.join("")}
}

get filename(){  
 const fileNameExtensionObj=this.getFileNameExtension();
this.\_filename=fileNameExtensionObj.fileName;
return this.\_filename
}

get extension(){
const fileNameExtensionObj=this.getFileNameExtension();
this.\_extension=fileNameExtensionObj.fileExt
return this.\_extension
}

get content(){
return this.\_content
}

getContents(){
return this.content
}

set content(str){
this.\_content=str
}

    write(str){
    let newStr=this.content.length > 0?`\n${str}`:`${str}`
    return this.content+=newStr;

}

\*getGeneratorFunc(){
const arrOfContent=this.content.split("\n")
for(const arrItem of arrOfContent){
return arrItem
}
}

get(){
let arrCont = this.getGeneratorFunc();
let arrItem=arrCont.next();
console.log(arrItem)
return arrItem.value
}

gets(){

}

}

var myFile = new File("example.txt", "Line 1\nLine 2\nLine 3\nLine 4\nLine 5");
console.log(myFile.gets()); // "Line 1"
console.log(myFile.gets()); // "Line 2"
console.log(myFile.gets()); // "Line 3"
console.log(myFile.gets()); // "Line 4"
console.log(myFile.gets()); // "Line 5"
console.log(myFile.gets()); // undefined
console.log(myFile.gets()); // undefined
console.log(myFile.gets()); // undefined





# 1.30.25, Generators
    - the `yield` keyword is lowkey new and was introduced in ES6, and it can only be used inside of generator function. `yield` the main culprit behind the generator pausing, take a look at how to use the `yeild` keyword below.
        
        ```js
        function* getEmployee() {
        console.log('the function has started');

        const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

        for (const name of names) {
            console.log(name);
            yield;
        }

        console.log('the function has ended');
    }
        ```

    - notice that in the code above, we're using `yield` inside of the `for...of` loop. When the generator is invoked, (which produces an iterator) and call next, we're going to get the following output.

    ```js
    const generatorIterator = getEmployee();
    generatorIterator.next();
    //logs The function has started
    //Amanda
    ```
    - it paused, but to be sure, check out the next iteration.

    ```js
    generatorIterator.next();
    //logs
    //Diego
    ```
    - it resumed and took off from where we left of in the last iteration. everytime we hit the `yield` keyword the code get's paused. now this is all fun, but what if we actually want to send data from the generator to the outside world, we can also do this with yield, ensentially replacing the need for a return keyword
        - here's an example
        ```js
        function* getEmployee() {
        console.log('the function has started');

        const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

        for (const name of names) {
            yield name;
        }

            console.log('the function has ended');
        }
        ```
    - now that we have done that, we can now use use the .value property to get the value from our generator
        ````js
        const generatorIterator = getEmployee();
        let result = generatorIterator.next();
        result.value // is "Amanda"
        
        generatorIterator.next().value // is "Diego"
        generatorIterator.next().value // is "Farrin"
        ````

    #### Sending data in/out of a generator
        - We can also send data into the generator by uisng the `.next()` method.
        ```js
        function* displayResponse() {
        const response = yield;
        console.log(`Your response is "${response}"!`);
        }

        const iterator = displayResponse();

        iterator.next(); // starts running the generator function
        iterator.next('Hello Udacity Student'); // send data into the generator
        // the line above logs to the console: Your response is "Hello Udacity Student"!
        ```

        - We can also send data into the generator function. the yield keyword in summary is used to pause the generator, and send data outside of the generator. and the next method is used to pass data into the generator. take a look at another example below:
        ```js
            function* getEmployee() {
            const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];
            const facts = [];

            for (const name of names) {
                // yield *out* each name AND store the returned data into the facts array
                facts.push(yield name); 
            }

                return facts;
            }

            const generatorIterator = getEmployee();

            // get the first name out of the generator
            let name = generatorIterator.next().value;

            // pass data in *and* get the next name
            name = generatorIterator.next(`${name} is cool!`).value; 

            // pass data in *and* get the next name
            name = generatorIterator.next(`${name} is awesome!`).value; 

            // pass data in *and* get the next name
            name = generatorIterator.next(`${name} is stupendous!`).value; 

            // you get the idea
            name = generatorIterator.next(`${name} is rad!`).value; 
            name = generatorIterator.next(`${name} is impressive!`).value;
            name = generatorIterator.next(`${name} is stunning!`).value;
            name = generatorIterator.next(`${name} is awe-inspiring!`).value;

            // pass the last data in, generator ends and returns the array
            const positions = generatorIterator.next(`${name} is magnificent!`).value; 

            // displays each name with description on its own line
            positions.join('\n'); 
        ```

        - a usecase for generators is that they are great for iterating over a list of items one at a time so that we can handle each item on it's own before moving on to the next. let's say theere's an app that needs to get a list of all repositories and number of times they have starred. before we can get the humber of stars for each repository, we need to get the user's information. After then recieviing the profile of the user, the code can then take that info to find all the reppositories.

        - there are some browsers not are not quite caught up with the es6 syntax, so you need to make your research before chosing to build out a specific feature in es6.









        - end of day session
            - tailwindcss
            - planning day
            - advanced speaking muscles
            - anki flashcards
            - codewars
            - diving into es6 generators
            - talk about what you have planned after the end of say session.

    #### Professional Dev-Fu
        - as new tech rolls out like es6 for example, it won't be supported by older browsers
        - the code we've been working on this whole time is not supported by older browsers, that is older browsers that we develped prior to the release of ES6, if we try running any ES6 code in an older browser, it won't work.
            - for example, attempting to use an arrow function in Safari 9 is just not going to work.
            - it is really difficult for browswer vendors to keep up with these updates and changes because languages like HTML, CSS, and JS are always improving.
        - Just as HTML, CSS, and SVG  has a standard body the WSC, **Ecma internation** is an industry association that develops and oversees standards like JS and JSON
