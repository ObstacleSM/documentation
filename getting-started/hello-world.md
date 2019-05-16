# Hello World

In this part I am going to explain a basic script. If you already have some experience with programming and that you understand what the code below does, you can probably skip this part.

## Hello World!

ManiaScript uses a C-like syntax: there are code blocks delimited by curly braces `{}` , that contain several instructions, ending with a semicolon `;`.

```text
Text Hello() {
    return "Hello World!";
}

main() {
    declare Text Nothing;
    declare Sentence = Hello();
    log(Sentence);
}
```

This script prints "Hello World!" to the console output. Let's try to understand the script bit by bit.

In ManiaScript, every script starts with a `main` function, it means that the code within the `main` function is executed first. Let's start by reading the first line of the `main` function.

```text
declare Text Nothing;
```

The first line declares a new **variable**. A variable is used to hold some data. It starts with a declare keyword, then the type and the name of the variable are indicated. We have not set any value for the variable named `Nothing`, consequently its value is an empty text.

```text
declare Sentence = Hello();
```

This line is similar to the first one, we declare a new variable named `Sentence` and assign it a value with the equal sign `=`. The value of `Sentence` is `Hello()`. Did you notice the two parenthesis after `Hello`? They are here because `Hello()` is a **function call**, so we need to read the function named `Hello` to know the value of `Sentence`.

```text
Text Hello() {
    return "Hello World!";
}
```

Here is the code for the function `Hello`. This code is written above the `main` function because we call it from main and the ManiaScript compiler reads a file from the top to the bottom. A **function declaration** begins with a type that indicates what kind of value it returns. It is followed by the name of the function. You can declare variables and call functions in the body of the function declaration, but you have to return a value with the `return` keyword.  
This function is named `Hello`, returns a value of type `Text` which is "Hello World!".

In the declaration of the variable `Sentence`, no type was specified. That's because when you assign a value to a variable in the same line as the declaration, the compiler can guess the type of that value.

```text
log(Sentence);
```

And finally the last line of the script!  
Did you notice the two parenthesis again? This line is also a function call.  
`log` is a function that takes one argument and print it to the output console. Here it prints the value of `Sentence`, so "Hello World!" is printed.

In this example our function named `Hello` did not take any arguments, but it is possible to do so. Here is an example of another function named `Hello` that takes a name as argument:

```text
Text Hello(Text _Name) {
    return "Hello" ^ _Name ^ "!";
}
```

Note that there is only one argument in the code above, but your functions can have as many arguments as you want, just separe them with a comma. In ManiaScript, the operator `^` concatenates strings together. So if you call the function like this:

```text
log(Hello("you"));
```

It will print "Hello you!" to the console.

