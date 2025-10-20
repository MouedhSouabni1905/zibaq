# Constructors and destructor

- Automatic allocation: eg. `Point p(nom, x, y);`
- Dynamic allocation: eg. `Point * ptrP = new Point(nom,x,y);`. Don't forget the `delete ptrP;` or there will be a memory leak.
- `~Point()` function destroys the object and so you don't need to implement anything in there except maybe a log message.
- **Operator overloading:** in the .h file `T & operator=(T & t);` and in the .cpp file `T & T::operator=(const T & t) {}` and in that function we first delete the memory taken by the object in case there's an array and copy the parameter object's attributes to the current object's attributes (`this`). 
- Copy constructor: in the .h file `T(const T & t);` and in the .cpp file `T::T(const T & t) : [initialization of non-dynamically allocatable attributes] { [initialization of allocatable attributes like arrays] }`
- When copying an array, you dynamically allocate it (declare it with a length based on variables) and then memcpy it to the new object.
- Whenever we use composition on an object to put it as a member of another object, we have to free it (without destroying it) when we destroy the object it is a member of. To do that, it must first be composed into the object using a pointer not a reference or the object itself

# Particularities in c++
- A child object inheriting from its parent can use all of its parent's methods, even the constructor even though it has a different name
- In order for the child to be able to override the parent object's method, you need to specify `virtual` before its declaration in the parent and child methods and `override` after the arguments in the child method's definition
- Initializing a child object (`Obj obj(...) : [inits...] {}` syntax) can be done by calling the parent's constructor in the inits then adding additional attributes of the child object like any other basic constructor would
- The destructor destroys the child object directly, unlike the constructor's intermediary step in creating the parent object first
- When an object is dynamically allocated it can be passed as a reference directly (reference as in alias not pointer) without having to do any more work
- Getters should return references (`T & getT() const {}`)
- An array of objects for example can be anything except an array of references to the objects, like the objects themselves or pointers to the objects, const or not const doesn't matter
- When doing aggregation, the attribute is either a pointer or a reference to the object, as opposed to composition where the object itself is an attribute
- Operator overloading syntax: `T & T::operator=(const T & t)`
- Copy constructor syntax: `T::T(const T & t)`
- In the .h file we just remove the `T::` prefix

# Exceptions

```
try {
	...
} catch (char * const exception) {
	cout << exception << endl;
}
```

And inside the function called in the try block:
`throw("[message that will be affected to the 'exception' variable]")`

# Remarks

- `const` keyword is used on methods that shouldn't modify the object
- It's **not** used on private attributes that are not class constants
- Class constants are declared in the header file but initialized in the .cpp file (can also be initialized in the header file), like so `static const TYPE NAME;`
- `constexpr` keyword makes it so that constants are evaluated at compile time rather than runtime, optimizing the program
- In the .cpp file: `TYPE ObjectName::function(args,...) {}` to define methods on that object, but you don't need to specify the namespace (the `ObjectName::` part) in the .h file
- Initializing an argument to a default value in the constructor's declaration (in the header file) makes it so that if no value is given, the constructor takes the default value
- `stdin.ignore(256, '\n');` after using stdin makes sure you can utilize the entry as a pure int
- `static` keyword indicates that the variable is class-global, meaning belongs to all instances of the class
- With operator overloading where we overload the = sign, we first empty the `this` object, then copy the contents of the argument into it, then we return `*this`
- To create a template class we place this line `template <class T>` before the class declaration in the header file.
- Template methods are implemented in the header file, and are all preceded by the line mentioned in the previous point, and in vectors for example we replace whatever should indicate the type with `T`
- The `inline` keyword allows us to define methods inside of the header file
