---
layout: post
title:  "Handlebars for Beginners"
date:   2017-03-11 22:17:16 -0500
---


I had a very difficult time last week when I was trying to get through the Handlebars template lessons on Learn.  The words just swam before me as I tried to read through the examples and I ended up skipping the lab.  I was then mightily displeased to find that several subsequent labs required the use of the template.  It was a bad week all around.  But somehow, over the weekend, I found some tutorials and it became much clearer.  In fact, it's really not that bad at all.  So, here's hoping that this blog post reaches someone who, like me, has struggled to find something that puts the use of Handlebars templates into a clear and easy-to-understand guide.

The concept of a template is simple enough:  It allows the creation of dynamic html which can be reused in different places, substituting the dynamic variables into the rest of the text.  There are some procedural requirements for using Handlebars, but if you just follow the steps, the rest is pretty straightforward.  Here is what is needed:


--download Handlebars from handlebarsjs.com.  Place the handlebars.js file in In the js folder of your project's directory.
In your html file:
--you'll need a place to render your template.  A div with an id attribute will do nicely.
--include a reference to handlebars by adding the following tag to the body of your html file:  `<script src="js/handlebars.js</script>`
--also in the body of your html file, create your handlbars template inside another script tag with the following attributes:  `<script id="templateId" type ="text/x-handlebars-template> your template goes here </script>`
--your template can consist of whatever html you need.  For the parts that you want to be dynamic, simply choose a variable name and surround that variable with the trademark double curly brackets like this: {{variable}}
In your main .js file, such as index.js file:
--establish a variable and assign your template script to it (e.g. `var template = document.getElementById("templateId").innerHTML`
--establish a variable to which will be assigned the function that compiles your your template (a good name for this is `compiled`):  
`var compiled = Handlebars.compile(template)`  
Now establish a variable that will hold the information that you want to be rendered in the template.  The information must be formatted into an object in which your Handlebars variables are the keys and the text you want those variables to be replaced with are the values. For example, var info = {name: "Bob", birthday:"1/2/1995"}
Then, to place the templated html into the spot on the page where you want it to appear, use document.getElementById("idOfElementYouWantToHoldTheText").innerHTML = template(info)
Now, if you want to put the name and birthday of a different person into another spot of your document, you can establish another object, such as var info2 = {name: "Betty", birthdate: "12/21/02"} and call document.getElementById("anotherDiv").innerHTML=template(info2).  

Handlebars also comes with some nice built-in helpers, and also gives you the ability to build your own custom helpers.  One of the most useful helpers is an `each` method.  If your `var info ={teacher:[{name:"Steven"},{name:"Jess"},{name:"Niky"}"]`Within a template you can have something like this:
```
<ul>
{{#each teacher}}
  <li> {{name}}</li>
	{{/each}}
</ul>
```
This will iterate through an array established in the var info, producing a list item for each element of the array:
Steven
Jess
Niky

