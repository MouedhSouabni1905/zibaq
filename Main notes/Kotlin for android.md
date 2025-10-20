**Tags:** [[Android]]

Using Jetpack Compose, you build your UI by defining sets of functions called composable functions to take in data and describe UI elements. Composable functions take input and generate it on the screen but they don't return anything in the code or program running.

Annotations (like `@Composable`) tell the compiler that the next function is a composable. Some annotations can take parameters, like `@Preview(showBackground=true)`. It can take multiple at once, ex: `@Preview(name="Preview",showSystemUi=true)`. Names of composable functions must use Pascal case (every word's first letter is capitalized) and be a noun (ex: `DoneButton()`).

- In **Kotlin** statements don't end with a semi-column.
- To specify an argument when calling a function, you use a variable affectation syntax (`x = a`).
- When declaring the function's arguments you specify the type after the column and you can specify a default value after that (`parameterName : Type = defaultValue`)

`Column`, `Row` and `Box` are composable functions that take composable content as arguments so you can place items inside these layout elements. ex: items in a `Row` composable are place horizontally next to each other. 

When a parameter is the last one in the function signature, you can use trailing lambda syntax. ex: `Row(content = {Text(...)})` becomes `Row{Text(...)}`.

To make the content be by default under the android system top bar, you need to add `.systemBarsPadding()` the main container's modifier in your application, like so:

```
@Composable
fun YourScreen() {
    Box(
        modifier = Modifier
            .fillMaxSize()
            .systemBarsPadding() // Adds padding to avoid overlapping status/navigation bars
    ) {
        // Your content here
    }
}
```

An `R` class is an automatically generated class by Android that contains the IDs of all resources in the project. 

The `Box` composable stacks your elements one over the other, by the order with which you placed the items in your code.

Layout arrangements:
![[android-verticalArrangement.png]]
![[android-horizontalArrangement.png]]

It is good code practices to take any string and turn it into a resource (would be an xml file in android) by highlighting it then clicking on the light bulb and clicking *extract string resource*. The `stringResource()` function which is the one that replaces the string, can take any number of arguments in good order, so you can extract even strings containing multiple variables.

Creating multiple Kotlin files to define different screens and components outside of the `MainActivity` file works and allows you to call them just like any composable function from the MainActivity.

For navigation you use a navigation library for jetpack commpose like NavHost, you create a navController variable that you pass as argument to all of the screens.

In kotlin `val name:type` declares an immutable variable and `var name:type` declares a mutable variable.
A class doesn't need its own file, you just define it like this: `class ClassName(params...) { [Class-Body] }` with the class body containing any number of functions including the `init{}` function.
An immutable variable is part of the object's state but can't be changed and can be used like a global variable. A mutable variable is passed as a parameter to the `init()` function.

Kotlin has function type declaration `([parameters]) -> [result type]`. The result type cannot be ommitted so if the function returns nothing you write `-> Unit`.
It is used: `val func1 = {FUNCTION-DECLARATION}` and can be used as an argument to a function like so `fun fff(f1 : FUNCTION-DECLARATION):Return-Type{Code-Block}`, with the function declaration being the same as the one we are gonna pass as argument whent calling the function.
A function call `function({ [lambda-function] })` can be abbreviated: `function { [lambda-function] }`.
A function call `function(par1, par2, ..., { [lambda-function] })` can be abbreviated: `function(par1, par2, ...) { [lambdafunction] }`.
To invoke a lambda function `[lambda_function].invoke([parameters])` or `[lambda_function]([parameters])`.

Kotlin contains iterating functions `forEach` and `forEachIndexed` which aren't language constructs. Meaning you can include them on a chain of operation like this:
```
originalCollection.
	filter([filter_function]).
	map([mapping_function]).
	take(37).
	forEach { elem ->
		...
	}
```

