---
layout: post
title:  "The Operator That Saved (many hours of) My Life"
date:   2017-02-12 19:13:17 -0500
---

In working through the prework labs in preparation for starting my coursework in web development at The Flatiron School, 
I often found myself stymied by the NoMethod on Nil Class error.  
 
For example, I would be building a hash and would want to add an element to an array which was the value for a particular key.  The problem was, that if this was the first element being added, the array did not yet exist!  So I was trying to shovel a value into a non-existent array.  Naturally, this would result in my maching telling me that there was no shovel method for a non-existent array.
 
In order to fix my code, I would laboriously add in conditional statements:

```
If hash[key]
    hash[key]<<new_element
else 
    hash[key]=[new_element]
end
```

Pretty code-smelly, right? But, hey, the tests passed, the light turned green, and I was a happy coder.

It was when searching through StackOverflow on an unrelated issue that I saw something that I didn't understand at all:  ||=
What *is* this? I wondered.  Some further googling, revealed that this was the operator that I had been needing for quite some time.  In hope that I may save other newbies from some serious loss of time, I would like to give a concise explanation of the "double pipe equals" a.k.a. "or equals" operator.
 
This handy operator turns the above smelly code into the sleek beast presented here:

```

hash[key] ||= []
```

```
hash[key] << new_element
```

From five lines of code down to two!


To be clear, about what is happening here in plain English:

If a value has already been assigned to the key for the hash in question, the first line does nothing--that value is left alone.  Then the second line shovels the new element into the array which is that value.

On the other hand, if this is the first time through the iteration, and no value has yet been assigned to that key for the hash, the value is set equal to an empty array.

In either case, the second line will shovel the new_element into the array.

This has been useful many times since then and has saved me countless hours.

Please realize that this is not only useful for hashes. The `||=` operator can be used on almost anything!  You can use it to maintain a variable that already exists OR to assign that variable if it hasn't been previously assigned, e.g.:




```
a ||=3
```
																			 
With this line of code, a will keep its value, if it has already been assigned one.  But, if a has not yet been assigned a value, it will now be set equal to 3.  No more undefined local variable or method!  Sweet relief.

I hope this has been useful to you.
