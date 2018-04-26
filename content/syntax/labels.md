# Labels
Labels are "extension points" in your script. There are two variations of such extension points:
`+++ MyLabel +++` can be extended multiple times, `--- MyLabel ---` is only extended by the latest definition of extending code.

To define the code that should be executed at the position of this label, we define the code block like this:
```c#
*** MyLabel ***
***
// do something in the scope of the extension point
***
```
These blocks are only available in the global scope (alongside your directives, global variables and function definitions). The code in the block has the scope of the extension point, meaning that all variables and functions known at the your `+++ MyLabel +++` (or `--- MyLabel ---`) can be accessed.

Labels can be inserted multiple times (and in different contexts) so their scope is in fact the intersection of the scopes where they are inserted:
```c#
Void fn1() {
    declare V = 2;
    declare W = 3;
    +++ MyLabel +++
}
Void fn2() {
    declare V = 4;
    +++ MyLabel +++
}
*** MyLabel ***
***
log(V); // logs 2 and 4 respectively
// log(W); would not compile as W is not always defined
***
```

Extension points can only be used in the scope of a function. That means that you can only access function-level code in the label implementation and can't e.g. define functions.
Depending on your use case it might be good practice to wrap your extension point in curly braces: `{+++ MyLabel +++}`. This wraps your label in a new scope. While you can still read and write all variables available at that point, you can't leak (internal) variables from your label implementation.
Consider the following example:
```c#
*** MyLabel ***
***
declare Tmp = V;
// ...
***
Void fn1() {
    declare V = 3;
    +++ MyLabel +++
    declare Tmp = "tmp";
    // ...
}
```
Here the compiler would complain that the variable `Tmp` has already been declared before. Wrapping the extension point in braces will result in `Tmp` from `MyLabel` not being visible in `fn1` thus not causing further errors.