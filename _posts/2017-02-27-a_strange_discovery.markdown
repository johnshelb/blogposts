---
layout: post
title:  "A strange discovery"
date:   2017-02-26 20:04:34 -0500
---

I was working on a lab, coding an app for simulated e-commerce site.  As I was googling around trying to solve some problem that was vexing me, I saw something that really confused me.

There was a class variable that was assigned to an array keeping track of all the products that the store had for sale.
Here is a simplified view of the class, stripped down for purposes of this illustration:

```
class Products
  attr_accessor :item, :price
 
  @@products=[]
	 
	 def intitialize(name, price)
	    
			@name=name
			
			@price=price
			
			@@products << self

   end

end
```

The goal was to write some code that would allow a user to try to put an item into a virtual shopping cart.  The hitch was that the code had to make sure that the product was actually available.  If the product was being offered for sale, the code should return the price.  If the item was not available, the return value shoule be a string informing the customer of that fact.

Here is (something like) the code that I found:
```
def check_for_product(desired_item)

   if item = @@products.find{|p| p.name == desired_item}
       
			 item.price
   
	 else 
        
				"Item not found"

end
```


What blew my mind about this was that the variable `item`  does not appear earlier in the code.  To me, it seemed as if the conditional could never evaluate to `true`,  but instead, the line would always throw an error as a result of referencinging an unassigned variable.

And yet, it worked.

I dropped into irb and played around with various permutations of the idea until the simplicity of what was going on finally hit me.  To be sure, a big stumbling block in my understanding was a recurring issue that I have, forgetting that there is a vast difference between `=` and `==`.   I had been misreading the conditional as saying that if `item` was the same as the name of a product that was found when iterating through all of the available products, then return the price.

What I finally realized was actually happening, however, was that  the iteration was either going to find a product with the name attribute that the customer wanted, or it wouldn't.  If there is no product with that name, the `find` method will return `nil`.  Since, 'nil' is a falsey value in Ruby, the  statement `item = nil`  evaluates to `nil` and therefore `false` and the conditional is not fulfilled, so the program will move on to the `else` statement.  If, however, the `find` method does successfully return a truthy value (and here's where the magic comes in), `item`, a previously unassigned variable, will be assigned to that value and the conditional evaluates to true. Then we can use `item` to represent the object, making its `price` attribute accessible through dot notation (`item.price`)!


I guess a longer way to write out the conditional would be:
```
if @@products.find{|p| p.name == desired_item}
  item=@@products.find{|p| p.name == desired_item}
```


	
To be fair, this only involves one extra line of code, but it does seem particularly ugly to have to repeat the whole iteration, especially if one were to be dealing with a store with a large number of products to enumerate through.

The point is, it turns out that using an `if` statement, you can both check to see if a value exists and, if it does, assign it to a variable in one step, instead of having to check first and then making the assignment.
