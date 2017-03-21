---
layout: post
title:  ".forEach() forBeginners"
date:   2017-03-11 22:17:16 -0500
---

In starting to tackle the learning of JavaScript, I have struggled with mastering the syntax, and with the vagueries of some of the documentation that I have consulted in trying to figure it out.  I think I have finally figured out how the Array.prototype.forEach property works and so I would like to try to explain it as clearly as possible, in the hope that a future struggling beginner will be able to come across this post and be able to grasp the concept with less pain than it cost me.

Like the `.each` method in Ruby, `.forEach()` can be used to iterate over each member of an array.  Once you understand the syntax, and how the arguments are passed, I think you will find it a very useful property.

I will try to illustrate the use of `.forEach()` with simple examples.  Let's start with a very simple array assigned to the variable `a`:
```
a = [1, 2, 3, 4]
```

Point 1:
`.forEach()` is called on array.  Using the dot notation, we can call forEach on our array like so:

```
a.forEach()
```

As written, however, this will throw an error, because `.forEach()` needs to be passed an argument between its parentheses.

Point 2:
The argument passed to `.forEach()` must be a function.  This will be the function that you want to act on each member of the array on which `.forEach()` is being called.  Let's start with a simple function that will simply log each element of the array:

```
a.forEach(function print(element){
  console.log(element)
	})
```

This will print out:
```
1
2
3
4
=>undefined
```
(Since there is no `return` value specified, the return value is given as undefined.)

Note that the argument of the function `print` is `element`.  This represents the element of the array that is being extracted with each iteration.

Point 3:
Although here the function that is given to `.forEach()` is fully written out and named `print`, it may also be an anonymous function:
```
a.forEach(function(element){
console.log(element)
})
```
Point 4: 
This function may also be written as an arrow function in several different formats:
```
a.forEach((element)=>{
console.log(element)
})
```

or, leaving out the curly brackets:

```
a.forEach((element)=>
console.log(element)
)
```

or, leaving out the parentheses around `element`, which is allowed when there is only one argument in the arrow function:

```
a.forEach(element=>
console.log(element)
)
```

Point 5:
The real power of `.forEach()` comes when the function argument passed into it is a callback function.  And here is where I encountered real difficulty in comprehension.

A callback function can be defined elsewhere in the code and then called back inside another function.  To keep our examples consistent, I will define my callback function like so:

```
cbk = function print(element){
console.log(element)
}
```

I can now call the function by passing in an argument to `cbk`, so that `cbk(27)` will print out:

```
27
=>undefined
```

Now, I can call `.forEach()` on our array using `cbk`:

```
a.forEach(cbk)
```

This will, as expected give the output:

```
1
2
3
4
=>undefined
```

Notice that in our expression `a.forEach(cbk)`, we do not explicitly pass in an argument to cbk.  cbk, representing the function `print()` was previously defined as taking in one argument, which we called, for convenience, 'element'.  This is where most of my confusion lay, so I want to be as explicit as possible here.

The secret magic of `.forEach()` is that is will automatically make up to three arguments available to the function being passed in.  Those arguments, in this order, are 1. the current element of the iteration, 2. the index of that element in the array, and 3. the entire array itself.

Since `cbk` represents the `print` function, which was defined as taking one argument, `.forEach()` will automatically pass in one argument, the current element, to `cbk`.

Now, for illustration, let's change the definition of `cbk` a little:

```
cbk = function print(e, i){
console.log(e,i)
}
```

Now, if we call `array.forEach(cbk)`, the output will be:
```
1 0
2 1
3 2
4 3
=>undefined
```

Printing out each element followed by its index.

Let's change `cbk` one more time:

```
cbk = function print(e, i,a){
console.log(e, i, a)
}
```

Now, if we call `a.forEach(cbk)`, the output will be:

```
1 0 >[1, 2, 3, 4]
2 1 >[1, 2, 3, 4]
3 2 >[1, 2, 3, 4]
4 3 >[1, 2, 3, 4]
=>undefined
```
printing out the element, its index, and the entire array for each iteration.

To be clear, the point that had me confused is that `.forEach()` will pass in as many of the arguments (element, index, array) *in that order* as the callback function requires.  If the callback only takes one argument, just the element will be passed in.  If the callback takes two arguments, the element and its index will be passed in, and if the callback takes three arguments, the element, its index, and the entire array will be passed in.
