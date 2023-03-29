# Using the Array forEach Method

## Learning Goals

- Recognize that Arrays are Objects
- Learn how iterator methods in JavaScript work
- Use `forEach()` to iterate through an array
- Learn when to use `forEach()`

## Introduction

| Use Case                                                       | Method                |
| -------------------------------------------------------------- | --------------------- |
| ** Execute a provided callback on each element                 | `forEach()`           |
| Finding a single element that meets a condition                | `indexOf()`, `find()` |
| Finding and returning a list of elements that meet a condition | `filter()`            |
| Modifying each element and returning the modified array        | `map()`               |
| Creating a summary or aggregation of values in an array        | `reduce()`            |

In this lesson, we will learn how to use the first of the iterator methods
above: `forEach()`. We will also learn under what circumstances `forEach()` is
the right iterator method to use. But first, we're going to get a little more
context for these methods by learning more about JavaScript objects.

## A Deeper Look at Objects

We've seen that JavaScript has many built-in methods that we can use to make our
code more efficient and to avoid having to "reinvent the wheel." But what
exactly is a method? A method is nothing more than a function that belongs to an
Object. So what does that mean? Let's take a look at an example.

Let's create a `dog` object and give it a couple of properties:

```js
const dog = {
    name: "Spinach",
    breed: "Shiba Inu"
}
```

As you can see, this object represents a particular dog:

```js
dog.name;
// => "Spinach"
dog.breed;
// => "Shiba Inu"
```

In addition to having the `name` and `breed` properties, we might also want our
`dog` object to be able to `bark()`:

```js
function bark() {
    console.log("Woof woof!")
}
```

Now we can call our `bark()` function, but it isn't associated with our `dog`
object in any way. It would really make more sense for the `bark()` function to
_belong_ to our `dog` object somehow. Well, we can do that!

You may recall from an earlier lesson that, in JavaScript, functions are
considered _first class_. This means that, like data values, they can be
assigned to variables and used as arguments in other functions. It also means
you can store functions in Arrays and Objects. In order to make the `bark()`
function belong to our `dog`, we can simply add it to the `dog` object as
another property:

```js
const dog = {
    name: "Spinach",
    breed: "Shiba Inu",
    bark: function() {
        console.log("Woof woof!");
    }
}
```

Now that `bark()` belongs to an object, we refer to it as a `method` rather than
a `property`. A method in JavaScript is simply a function that belongs to an
object.

<details><summary><b>How do you think we would call the `bark()` method?</b></summary><p>
    <code>dog.bark();</code>
    <p>We call a method the same way we access a property: using the dot operator. If we just enter <code>dog.bark</code>, without the parentheses, the method itself will be returned:</p>
    <code>dog.bark</code><br/>
    <code>// => f () {</code><br/>
    <code>// console.log("Woof woof!");</code><br/>
    <code>// }</code>
    <p>Adding the parentheses (as always) <em>executes</em> the method.</p>
</p></details>

### Aside: A Brief Preview of Object Orientation

While JavaScript was originally developed as a [functional programming
language][], it can also be used to create object-oriented code. To be clear,
the "object" part of object orientation refers to the fact that the code is
usually organized around real-world "objects" — such as dogs, cars, coding
classes, etc. — not to the use of the Object data structure. In other
programming languages, object orientation will be implemented and structured in
different ways.

[functional programming language]: https://en.wikipedia.org/wiki/Functional_programming

We can say, though, that our `dog` object is heading in the direction of object
orientation: our `dog` object represents a real-world thing, and it has
properties and methods. However, it is limited because it represents a single,
specific dog. In object orientation, we can create a `Dog` _class_ (with a
capital "D") that represents dogs in general, and we can then create an
_instance_ of that class that represents an individual dog. Each dog instance
would have its own values of the `breed` and `name` properties, and each dog
instance would be able to `bark()`. The properties and methods of the Dog class
would be _inherited_ by each instance of the class.

Don't worry too much about functional vs. object-oriented programming at this
point. These are difficult concepts. We will delve more deeply into what they
mean later in the course.

## Arrays (and many other things in JavaScript) are Objects

So how does all this apply to JavaScript Arrays? Well, JavaScript Arrays are
actually objects! They have properties (e.g., `length`) and methods (`push()`,
`join()`, etc.). Their indexes are actually keys! JavaSCript includes code
"under the hood" that allows us to interact with Arrays in an array-like way.
Because all arrays have numeric keys, beginning with 0, that under-the-hood code
is able to simplify and streamline how we interact with arrays. And when we
create an array, it _inherits_ all the properties and methods that belong to the
`Array` object.

So what else in JavaScript is an Object? Lots of things, including strings and
even functions! In general, we don't need to concern ourselves too much with
this fact. However, noting the commonalities — e.g., calling methods using dot
notation — and understanding that instances of these objects inherit all the
properties and methods of their [object _prototype_][prototypes], can help us
understand how things work in JavaScript.

## Array Iterator Methods

So now let's return to our Array iterator methods. These are methods on the
`Array` Object prototype that are inherited by array instances. Therefore, we
can call any of these iterator methods on a specific array using dot notation.

Like a `for...of` loop, each of the methods _iterates_ through the elements in
an array in turn and performs some action on each of them. But that's really
where the similarities end. Unlike a loop, iterator methods:

1. are _called on_ an instance of an array, and
2. take a _callback function_ as an argument.

For `forEach`, the basic setup looks like this:

```js
<array>.forEach(callback);
```

For example, if we want to log the values of our array, we could do this:

```js
const myArray = [1, 2, 3];
myArray.forEach(function(el) {
    console.log(el);
});
```

So what's happening here? We are calling `forEach()` on `myArray` and passing an
anonymous function as the callback. The `forEach()` method iterates through
`myArray` and, in each iteration, _automatically passes_ the current element to
the callback function. (It actually automatically passes _three_ values, not
just one; more about that later.) The callback captures the element using the
`el` parameter then, in the body of the loop, logs it to the console. That's it!

**Challenge:** there are other ways we could code this. We could call
`forEach()` directly on the array rather than creating a variable, or we could
use an arrow function for our anonymous function. Take a few minutes to see if
you can code each of those before moving on. If you have difficulty with this
task, don't worry too much. The important thing is to keep practicing!

<details><summary><b>Calling `forEach()` directly on the array</b></summary><p>
    <code>[1, 2, 3].forEach(function(el) {</code><br/>
    <code>console.log(el);</code><br/>
    <code>});</code>
</p></details>

<details><summary><b>Passing an arrow function as the callback</b></summary><p>
    <code>[1, 2, 3].forEach((el) => console.log(el));</code>
</p></details>

Of course, we can also create the callback as a named function and pass it by
name. That would look like this:

```js
function logElements(value) {
    console.log(value);
}

[1, 2, 3].forEach(logElements);
```

Note that we don't need to explicitly pass the current element to the callback:
the `forEach()` method does that for us! We do, however, need to set up our
callback with a parameter, or maybe more than one...

## More on `forEach()`

We mentioned above that `forEach()` automatically passes _three_ values to our
callback in each iteration, not just the current element. The other two values
are the _index_ of the current element in the array and the array itself. We
access them by setting up additional parameters in our callback. For example, we
could log the contents of the array with a little more detail:

```js
const myArray = ["one", "two", "three"];

function logArrayContents(element, index) {
    console.log(`arr[${index}] = ${element}`);
}
myArray.forEach(logArrayContents);
// => 
// arr[0] = one
// arr[1] = two
// arr[2] = three
```

If we also want to use the array itself inside our callback, we would simply add
a third parameter.

**Note:** If we only use one parameter, the JavaScript engine will automatically
assign the first passed value, the element itself, to that parameter and ignore
the other passed values. If we use two parameters, it will automatically assign the
first two passed values to those parameters, respectively. What this means is
that, if we only need to use the index in our callback, we still need to use two
parameters so that the index is assigned to the correct parameter. The parameter
names, as always, are arbitrary: JavaScript will not know to assign the second
passed value to the parameter named `index`!

## When Should We Use `forEach()`?

`forEach()` is the most general of the iterator methods we'll be learning about.
But, as a result, it is also the least _expressive_. You can't tell anything
about what the code will do with each element of the array simply by noting that
`forEach()` is being used.

If you take a look back at the table at the top of the page, you'll see that all
the other methods are meant to accomplish something specific: finding an element
in an array that meets a certain condition, modifying each element in an array,
etc. If we see that the `find()` method is being called on an array, for
example, we immediately know that a single value that meets a condition
specified in the callback is going to be returned. (Well, usually. We'll learn
more about that in the next lesson.)

What this means is that **you should only use `forEach()` when none of the other
iterator methods are appropriate**! Not only because it makes your code less
expressive (although that's a good reason), but also because we don't want to
reinvent the wheel. We _could_ recreate the functionality of one of the other
methods in our callback function, but doing so adds unnecessary code to our
program. It is also likely to result in the need for more debugging and yield
less efficient code than if we use a built-in method that has been fine-tuned
and improved by multiple developers over time.

The example we used in this lesson is a good illustration of when using
`forEach()` is appropriate: we didn't need our callback to return a value, we
just logged values to the console. You could also use `forEach()` if you need to
make _in-place_ changes to the elements in the array (i.e., you want the changes
to be applied to the input array). This use is, of course, generally not
recommended: it's almost always better to create and return a _new_ array with
the changed elements and leave the original array unchanged — which is exactly
what the `map()` method does! We'll learn about `map()` a bit later in this
module.

## Conclusion

JavaScript's global `Array` object provides a number of iterator methods that
allow us to iterate through an array without having to write looping code. They
also give us a great deal of control over what we do with the elements of the
array by allowing us to pass a callback function as an argument.

In this lesson, we learned about the most general (and least expressive) of the
iterator methods: `forEach()`. In the lessons that follow, we'll learn about the
other iterator methods and practice using them.

## Resources

- [MDN: forEach()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
- [Object Prototypes][prototypes]
- [Prototypal Inheritance][inheritance]

[prototypes]: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes
[inheritance]: https://javascript.info/prototype-inheritance
