**Tags:** [[Programming]]

Everything in ruby is an object. `self` tells you what object the current context belongs to. The default, if there is no specified object, is `main`.

`.methods` on an object returns an array of all the methodsthat can be applied to that object (they are preceded by a column but it can be ignored).

Interpolation in Ruby happens using "some string#{variable}". However, single-quoted strings do *not* support string interpolation (and escae sequence).

Methods that end with `?` return boolean values, like `.include?('some string')` which returns true if the string on which it is called contains the string passed in argument.
Methods that contain 2 words are spearated by `_`, like `.start_with?('some string')`.

`String_Object1 << String_Object2` appends the second string to the first one by applying the change to the first object and not creating a new string object (as opposed to using the `+` operator).

`.sub(str1,str2)` replaces the first substring by the second, but only the first occurence. `.gsub` does the same thing but to all occurences. The first substring can be a regex match if surrounded by forward slashes (without any quotation).

In Ruby, ? and ! can be used to replace then and else , respectively.

One way to do loops in Ruby is:
```
loop do
	 some block of code
	 break if condition
end
```

`[1,2,3,5][x]` returns the element at index `x` in the array. `.push` method appends the argument to the array. `<<` operator does the same as well.

`.map` method on an array followed by a `{}` or `do end` block that contains something of the form `|element| instruction` (with only one instruction) maps every result of the instruction (operation on the element) to a new array.

`.select` method returns a new array containing only the elements of the array that satisfy the condition specified in the block.

`.each` is the most used iteration method in Ruby. Contrary to `.map`, it can have as many instruction as you want, related or unrelated to the arguments, because it is a replacement to `for` loops.

Hashes are defined like this `hash = { "key" => value, ...}`. Values are accessed this way `hash["key"]`.

When iterating over hashes, the arguments between `|key_variable,value_variable|` are used to store the key then value of the hash for each iteration, meaning each iteration happens on the key-value pair.

When using the Hash.new() function, the argument you pass will be the default value no matter what other elements you add, meaning it will be the displayed valu for a key lookup that doesn't exist.

Another way to create a hash is `hash=Hash[:key,value,:key,value]`.

greater_than = ->(x,y) { y > x }.curry
lambda expression in ruby: function_name = -> (arguments) {block of code}

Curried Functions:
The first call (e.g., curried_add(1)) takes the first argument (x) and returns a new function that expects the remaining arguments (y and z).
The second call (e.g., result1(2)) takes the second argument (y) and returns another new function that expects the final argument (z).
The third call (e.g., result2(3)) takes the final argument (z) and finally executes the original add function with all the arguments, returning the result.
puts list.select(&greater_than.(5))
[6, 7, 8, 9, 10]
The select method expects a block not a curried function, so the & notation converts greater_than to a block
The dot . is used to "apply" the currying operation to the greater_than function with the argument 5. This creates a new function that is specifically designed to check for numbers greater than 5
puts "" puts list.select(&greater_than.(8))
[9, 10]

result = [1, 2, 3].map do |number| number * 2 end
the map method returns a new array with the result
|number| is the argument

puts ("")
puts("> Block result:",result) # Output: [2, 4, 6]
def greet
yield end greet { puts "Hello from the block!" }
When you call a function with yield inside of it, whatever code is inside the block between braces (or do / end) runs through the yield
You can pass arguments inside the yield which become the arguments of the block
puts "" def meth yield(10,1) end result=meth do |n,i| n-i end puts result
You can store the returned value inside a variable to use it later
.sort method returns a sorted array in ascending order

spaceship operator "<=>" compares two values abd returns -1 if the one on the left precedes the ine on the right (1<=>2 returns -1 , a<=>b returns -1), 1 if it's not in the right order and 0 if they are equal

"class << self" is a metaprogramming notation in ruby that allows to write a method of the class itself not of an instance of it

Safe Navigation Operator (&.):
The &. is the safe navigation operator. It prevents nil errors from occurring during method chaining.
If the object before &. is nil, the entire expression evaluates to nil instead of raising a NoMethodError.
If the object before &. is not nil, the first method is called on it.
Defining a class in ruby:

class myClass attr_accessor :name 
defines constructor and accessor with quick syntax def initialize(name) @name=name
method that initializes the object when calling myClass.new(arg) end end

The easiest way to think of a symbol is as a string that you can’t do anything interesting with: irb(main):021:0> :symbol.upcase NoMethodError: undefined method ‘upcase' for :symbol:Symbol from (irb):28 irb(main):022:0> :symbol.include?('sym') NoMethodError: undefined method ‘include?' for :symbol:Symbol from (irb):33 Using a symbol in your code signals a reader something about your intentions. You’re just using it to stand in for something else (like the name of an accessor you want Ruby to create).

when defining a self.methodname method inside of a class, it can be called for an instance by replacing self with the classname, classname.methodname

This can be used to initialize the object with special properties (classname.object_in_a_special_state) for example

In Ruby, `self.method_name` defines a method that belongs to the class itself, rather than to instances of the class. This means you can call `Maybe.unit(5)` directly on the `Maybe` class without first creating an object.

