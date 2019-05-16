# Functions

A function is a piece of code that can be executed with parameters to avoid duplicating some functionality in your program.

## Defining a function

A function always has a _return-type_ - the type of the data that will be returned by the function -, a name and a list of zero or more arguments - each with a type and a name. The _function-body_ describes the behaviour of the function.

```text
Integer Sum(Integer _A, Integer _B) {
    return _A + _B;
}
```

Among the usual datatypes functions can have the return-type `Void`, indicating that the function will not return a value. Returning a value none-the-less will not compile. The same goes for not returning a value \(or a value of wrong type\) if a return-type is set.

## Calling a function

To execute a function with given arguments, you simply call them like this:

```text
declare Result = Sum(23, 19);
```

Expressions passed as arguments to a function are evaluated before calling the function.

To call a function it has to be defined prior to your call in the code. That means you can't call a function not yet defined and thus can't circularly call functions \(e.g. fn1 calls fn2, which calls fn1\). Functions may however call themselves.

## Overriding a function

The combination of name and argument types makes the function's _signature_. No two functions with the same signature may be present in your program. However there can be multiple functions with the same name but varying in number and or type of their arguments. The compiler will choose the fitting function from the given arguments. This is called _polymorphism_.

```text
Integer Sum(Integer _A, Integer _B) { return _A + _B; }
Real Sum(Real _A, Real _B) { return _A + _B; }
main() {
    declare Result1 = Sum(34, 8);
    declare Result2 = Sum(2.8, .34);
}
```

This way you would implement optional arguments as well. Only keep in mind that the most generic function has to be declared first.

```text
Void doSomething(CMlControl _Control, Boolean _Flag) { /* ... */ }
Void doSomething(CMlControl _Control) {
    doSomething(_Control, True);
}
```

## The `main`-function

The `main`-function is a special case as it does not have a return-type, no arguments and cannot be re-declared. It is the entrance into your program.

