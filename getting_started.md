# Getting Started

Here is a little script written in ManiaScript. As you can see, ManiaScript uses a C-like syntax: there are blocks delimited by curly braces `{}` , and each instruction ends with a semicolon `;`.

```maniascript
Text Hello() {
    return "Hello World!";
}

main() {
    declare Text Nothing;
    declare Sentence = Hello();
    log(Sentence);
}
```

This script prints "Hello World!" to the console output. Let's try to understand the script bit by bit. Each script starts with a `main` function, it means that the code within the `main` function is executed first.

```maniascript
declare Text Nothing;
```

The first line declares a new **variable**. A variable is used to hold some data. It starts with a declare keyword, then the type and the name of the variables are indicated. We have not set any value for the `Nothing` variable, consequently its value is an empty text.

```maniascript
declare Sentence = Hello();
```

This line is similar  to the first one, we declare a new variable named `Sentence` and assign a value. The value of `Sentence` is `Hello()`. Did you notice the two parenthesis? They are here because `Hello()` is a  **function call**, so we need to read the `Hello` function to know the value of `Sentence`.

```maniascript
Text Hello() {
    return "Hello World!";
}
```

Here is the code for the function `Hello`.
A **function declaration** begins with a type that indicates what kind of value it returns. It is followed by the name of the function. You can declare variables and call functions in the body of the function declaration, but you have to return a value with the `return` keyword.  
This function is named `Hello`, returns a value of type `Text` which is "Hello World!".

In the declaration of the variable `Sentence`, no type was specified. That's because when you assign a value to a variable in the same line as the declaration, the compiler can guess the type of that value.

```maniascript
log(Sentence);
```

And finally the last line of the script!
Did you notice the two parenthesis again? This line is also a function call.
`log` is a function that takes one argument and print it to the output console. Here it prints the value of `Sentence`, so "Hello World!" is printed.
