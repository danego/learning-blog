# A learning blog for mostly new and new to **Javascript** coders

_a blog post brought to you by HypnoToad_

# Part One - _Comments and the Console_

**Learning how to comment:**

<span style="color:green">//This is a comment. Just use // to start one </span>

***
<span style="color:green"> /* </span>

<span style="color:green"> Or you can comment multiple lines at a time by surrounding your code with /* */ </span>

<span style="color:green"> */ </span>


**The Console**

* The console is the message/testing center for you as the code developer and it allows you to interact with the program. 

* You can log different values, variables, or strings to help you code your project.

* If you're logging strings, you can use single or double quotes or string literals:

<pre><code>console.log('Hello there!');

console.log("But double quotes allow you to use apostrophes. You're welcome.");

console.log(`Or even string literals, which allow you to access variables like this: ${var_name}.`);
</code></pre>

# Part Two - _Manipulating the variable_

**Declaring Variables:** In JavaScript we can declare variables with three different keywords: var, let, and const. 

* _var_ is function scoped and can be hoisted (called before it's initialized).

* _let_ is block scoped (like C++ and Java variables) and cannot be hoisted (will throw an error instead). **CAN YOU RE-DECLARE A LET VAR???**

* _const_ is block scoped, but can only be set once (cannot be re-assigned) and must be declared and initialized at same time. 

_Note: We will return to hoisting and scope in Part 6 for a more in-depth discussion._

***

**Naming Conventions:** Variable names in JavaScript should be camel cased, eg variableNameExample, where each new word is capitalized. JavaScript variable names also have several rules:

* names must start with either an underscore (_) or a letter, no numbers to start. 

* The rest of the varName can have numbers, but no spaces, punctuation, or other symbols. 

* Variable names are case sensistive: varname != varName.

* You cannot use JavaScript's reserved words (such as "if", "case", "super") and JavaScript keywords (such as "java", "image", "function") should be avoided, even though they're not reserved.

***

**Inititalization:** Let's create some variables! 

    var helloCount = 0;

The variable is the container and we give it a value. Let's change its value a bit:

    console.log(helloCount++);

Outputs <span style="color:green"> 0 </span> but now helloCount equals 1 (the ++ means add 1 to current value) because the JavaScript engine logs the value before increasing it.

    console.log(++helloCount);

Outputs <span style="color:green"> 2 </span> now because it's a prefix increment, which means it adds one to helloCount **before** helloCount is outputted. 

***

**Dynamically vs Statically Typed:**

One thing you may have noticed if you're coming from a language like C++ or Java is that we declared a number value with _var_. Unlike those other languages, we didn't have to pick our keyword based on the type of number, like int, double, or float. 

This is because JavaScript is dynamically typed meaning it checks variables's values at runtime, not at compile time like in statically typed languages. 

_Note: JavaScript is also weakly typed which we will cover with coercion towards the end of Part 3._

But not only can we assign different types of number to the same keyword, we can also change the **type of value** completely! Even after we've initialized it as a number.  Let's re-assign a string to our variable:

    helloCount = "hi there, now I'm a string!";

***

**Variable Attributes:**  In addition to their value, JavaScript variables have attributes, such as properties and methods, that give us access to more info or allow us to perform changes on the variable. Specifically, properties and methods are stored on the variable's prototype, but we'll get more into that in Part 7?.

* Properties: We access these using dot notation. One property is "length", which tells us how long the variable value is.

    `console.log('checking length: ' + helloCount.length);`

    The output for this is <span style="color:green">checking length: 27</span>. 

    _Note: We logged the length of our variable by using a plus sign to combine it with our string message ('checking length '). This is called concatenation._

* Methods: Variables also have methods attached to them--like "toUpperCase" which changes our string temporarily to all uppercase--which we call using parentheses ().

    `console.log('changing to uppercase: ' + helloCount.toUpperCase());`

    Our output for this is: <span style="color:green">changing to uppercase: HI THERE, NOW I'M A STRING!</span>

***


# Part Three - _Primitives and Wrappers_

Values and data in JavaScript are either Primitives or Objects. There are 6 value types (7 with EC6 - the current JavaScript version) that are primitive:

### Primitive Types**
1. number
2. boolean
3. string
4. undefined (lack of existence)
5. null (lack of exitence, or no value set & technically a special object)
6. bigInt 
7. symbol 

Primitives, unlike objects, are _immutable_, which means the values can't be changed or altered once they're set. Unlike objects, primitive values are the basic blocks so when we reassign a variable a new value, a whole new primitve ... REVIEW They also have no methods attached to them. 

_Note: **null** is considered a primitive even though it's technically an object because it's a longstanding JavaScript error (and changing it could cause fresh problems in old code)._

_Note: **bigInt** (used for arbitrarily large numbers, like in cryptography) and **symbol** (used to create unique object identifiers) are uncommon and not necessary to be familiar with as of yet._

All other value types are objects: 

### Object Types**
* Function _(see Part 5 for an in-depth look)_
* Object
* Number
* String
* and many more ...

Now you may be wondering why number/Number and string/String are on both the primitive and Object lists ... the reason is that they're different! 

    Every primitive value, except for _null_ and _undefined_, have an object equivalent that wraps around the primitive value. They are used as constructors for primitives and also attached to these objects are multiple methods (like toUpperCase()) and properties (like .length). To access the actual primitive value, use the valueOf() property. 


Wrappers - creating them vs actual primitives, what they provide, and implict wrappers (but not for nums IFIRC)

* Pros: 
* Cons: "doesn't work on numbers ... === or == ???"

### Coercion & Wrappers ^

The other big thing about wrappers to keep in mind is how they coerce (coerce means to force in to a new shape). Normally use === but good to know.

    var helloCount = 2;
    var helloCountWrapper = new Number(2);

    console.log(typeof helloCount);  // is "number"
    console.log(typeof helloCountWrapper);  // is "object"

And now some type coercion with the same variables:

    console.log(helloCount == helloCountWrapper);  //true
    console.log(helloCount === helloCountWrapper); //false

***


### Calling a Function and Passing by Value

Passing by value means that the argument is copied into the function. So any changes made to the value _inside_ the function will not carry over to the original value once the function is finished. 

Passing by reference means that the actual argument, and not a copy, is passed into the function (specifically its memory address). So any changes made to the value **will** carry over after the function.

_Note:_
* _Parameter refers to a variable in a function declaration._ 
* _Argument refers to the value you call that function with. So the arguments are the actual values passed into the parameters._

_All functions in JavaScript pass parameters by value, not by reference. This is easiest to see with primitive values:_   

**Passing by Value**

    function reveal(value) {
        value = 5;
        console.log("Value within func: " + value);
    }

    var value = 2;
    reveal(value);
    console.log('Our value after func call: ' + value);

Output is:

> <code>Value within func:  5

> Our value after func call: 2 </code>

Because our variable _value_ is passed by value it still equals 2 even after we set it to 5 in _reveal()_;

***

_Up above we said that all JavaScript functions pass by value, but you might hear that JavaScript passes non-primitives by reference. So which is correct?_

Well, both are partly correct. For objects passed into functions, it looks like JavaScript passes them by reference, meaning we can make lasting changes to our values. Which is true--we can alter the properties of objects, like arrays, and keep those changes after the function.

But if we try to reassign the value to an entirely new array or object, then this change will not carry over. Let's see:

**Passing by "Reference"**

    function revealArray(dessertArray) {
        dessertArray[1] = 'spaghetti';
        dessertArray = new Array(2).fill('fruit');
        console.log(dessertArray);
    }

    var dessertArray = new Array(3).fill('Mango rice');
    revealArray(dessertArray);
    console.log(dessertArray); 

Output is the two arrays: 

> <code> ["fruit", "fruit"]

> ["Mango rice", "spaghetti", "Mango rice"] </code>

1. First we create an array _dessertArray_ of size 3 and fill it with the string, 'Mango rice'. Then we call our function revealArray(). 

2. Inside revealArray(), we change the second element of the array to the string 'spaghetti'. 

3. Then we assign _dessertArray_ to a whole new array of size 2 filled with the string 'fruit'. This array is the first one we log. 

4. After revealArray(), we log _dessertArray_ again ... and find that what we did in **step 4** did not carry over! Instead we see our original array of 'Mango rice' strings with its second entry updated (from **step 2**).

The explanation for all this is that only the _memory address of objects_ are passed by value in JavaScript. This means we can make lasting changes to any part of the object _except_ what value it points to. 



# Part Four - _Conditionals and Defaults_ #

Conditional statements, like _if, else if, else_, are the same in JavaScript as other major languages. Likewise, JavaScript uses many of the same logical operators you've probably seen before (operators take an operand(s) and returns a value):

> **&&** and operator

> **||** or operator

> **!** bang operator (not)

Comparison operators are similar, but with more options in JavaScript because it's dynamically typed--as we saw in _Coercion and Wrappers_ in Part Three. Generally it is best practice to stick with the three equal sign version unless you specifically want to coerce types:

> **===** is equal to

> **!==** is ***not*** equal to

***

### Truthy / Falsy Values ###

It is expected for boolean valuables to evaluate to true or false, but so do other values. Knowing these can be useful for testing input and many other cases, but they will also be necessary to understand our next mini-topic--defaults and short circuit evaluation.

Falsy Values: 
* 0
* empty strings ""
* null
* undefined
* NaN (not a number)

So if we set a variable to an empty string and pass into an _if_ statement, it should evaluate to false and run _else_ instead. 

    var dog = "";
    if (dog) {
        conosle.log('Dog type: ' + dog);
    }
    else {
        console.log('Dog variable not set');
    }

Output:

<code>Dog variable not set</code>

And we get the same behavior if we do not set _dog_'s value at all (i.e. not initialized).

***

### Defaults ###

Let's say we want to set up a function that has two parameters, one of which we want to provide a default value if none is passed in (note: if you're wondering why we can pass in a changing number of arguments into the same function, good, and we'll cover that in Part Five.). 

Default Default Way:

    function createPerson(name, occupation) {
        this.name = name; 
        this.occupation = occupation || 'coder'; 
    }

What this means is that if "occupation" is passed in to createPerson(), then it will use that value. But if no value is set, then it will set it to the default. This works becasue of the "or" operator, ||. If the first expression returns true then it doesn't read the second value.  

EC6 way:

    function createPerson(name, occupation = 'coder') { //do stuff }

*Firs of all, a binary operator takes two operands and returns a value. Like SUCH AND SUCH. A ternary does the same but with three inputs.  
ternary operators


# Part Five - _Functions and Execution Contexts_ #

In Part Three we've talked about functions and passing by value, but now let's talk about 

Call, apply, bind here?
IIFEs?? (if IIFEs must do hoisting first ...)

maybe bonus section on 3.5 different ways to create ... (would protoype be its own section?)

    would need object literals before this somewhere ...

# Part Six - _Scope, Var, Let, and Beyond!_ #

* Hoisting --> brief explanation of global exec context

* global vs block vs function

Scope chain (lexical placement)

# Part Seven - _Callbacks and Promises_ #











***
***
<span style="color: green">some *blue* text</span>  **//html code to be exact** _!doesn't work in code block!_


### testing ###

I'm a Header
------------
I'm Bigger
==========
# im a header?
## yes i am 

> this is a blockquote
>
> > var x = y;

>still am blocky

* list one /* emphasis shown? /*

    still one

*  two

***

--------

