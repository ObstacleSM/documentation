# Variables

In variables you can store values for future use. Before using them, they have to be declared.

## Declaring variables

Variables can be declared in different ways.

### Local variables

In functions variables are declared using the `declare` keyword, a datatype and an identifier. Local variables can be declared with an initial value. If the datatype can be derived from this initial value, the type doesn't have to be explicitly declared.

```text
declare Text Var1;
declare Integer Var2 = 2;
declare Var3 = 3;
declare Something = []; // no type can be derived from this, it should be like this:
declare Text[] Something = [];
```

### Global variables

In the global scope \(alongside directives and function definitions\) variables can't be declared with an initial value. Thus a explicit datatype is mandatory.

### Extension variables

Variables can also be attached to existig objects and later read from these objects:

```text
declare Text SomeVar for LocalUser;
declare Integer SomeOtherVar for LocalUser = 42;
```

Setting a value as in the case of `SomeOtherVar` will not set the value of the variable but rather the default value for reading this variable from objects that don't have this variable initialized yet.

Such variables may be aliased. This comes is necessary when you have to objects of the same type with the same variables, e.g. two players:

```text
declare Integer CustomScore for Players[0] as CustomScore1;
declare Integer CustomScore for Players[1] as CustomScore2;
```

On top of that there are some modifiers that can be inserted between `declare` and the datatype:

#### persistent

Persistent variables are available when revisiting the script, so you could store settings in the user object or something like cookies in a ManiaLink's `Page` object and use them once the user comes back.

Note that you can only store a limited amount of data on an object.

Note that you cannot change the type of a persistent variable and have to use a new name;

#### netread

#### netwrite

## Using variables

You can write to a variable by assigning a value to it:

```text
declare Text SomeVar;
SomeVar = "foo";
SomeVar = "bar";
```

The type of a declared variable can't change and the values have to match the variable's type.

Reading a variable is as easy as using it's name in your program:

```text
declare Text Foo = "foo";
log(Foo);
declare MyPage = Page;
log(Page.MainFrame);
```

It is also possible to use something like pointers: variables that point to certain objects.

```text
declare CPlayer[] Players;
// ...
declare CPlayer FirstPlayer <=> Players[0];
while (True) {
    log(FirstPlayer.User.Name); // might change as `Players` changes
    yield;
}
```

