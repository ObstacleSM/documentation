# Types

## Basic types

There are 9 different types in ManiaScript: `Void`, `Integer`, `Real`, `Boolean`, `Text`, `Vec2`, `Vec3`,`Int3` and `Ident`.

| Type | Description |
| :--- | :--- |
| Void | `Void` is a type that means empty. You cannot create variables of that type, it is used to declare functions that returns nothing. |
| Integer | An `Integer` variable is an integer number \($$\mathbb{Z}$$ in mathematics\) between $$-2147483648$$ \($$-2^{31}$$\) and $$2147483647$$\($$2^{31}-1$$\). |
| Real | A `Real` variable is a real number \($$\mathbb{R}$$ in mathematics\). It can represent values much higher than Integer. |
| Boolean | A `Boolean` variable can be either `True` or `False`. |
| Text | `Text` represents a string of characters. |
| Vec2 | `Vec2` is a two dimensional vector \($$\mathbb{R^2}$$ in mathematics\). The two values can be accessed with `X` and `Y` respectively. |
| Vec3 | `Vec3` is a three dimensional vector \($$\mathbb{R^3}$$ in mathematics\). The third value can be accessed with the `Z` property. |
| Ident | `Ident` is the type of an Id. Every class in ManiaScript has a unique `Id` property that can be used to identify it. |

## Lists and Arrays

### List

A List is a type that can store multiple values. You can declare list by adding two square brackets after a type.

```maniascript
declare Integer[] MyList;
```

There are several basic functions to manipulate them, and you can access one element by its index. The indexes start at 0, so the first index is `0` and the last one is `MyList.count-1`. Accessing an invalid index will result in an `Out of bounds` error.

```maniascript
// Access an element
declare FirstElement = MyList[0];

// Basic functions
declare Size = MyList.count;
declare SortedList = MyList.sort();
MyList.add(42);
MyList.removekey(0); // Remove the element at the index 0
MyList.remove(38);
declare DoesExist1 = MyList.existskey(58); // equivalent to 0 <= 58 < MyList.count
declare DoesExist2 = MyList.exists(12);
declare Index = MyList.keyof(28); // such as List[Index] == 28
MyList.clear();
```

### Array

An array is similar to a list, except that you can specify a type for the index.

```maniascript
declare Text[Integer] MyArray;
```

The array above is not a list! There is no `add` function for arrays, instead you directly assign a value for the given key.

```maniascript
MyArray[1] = "One";
```

You can even nest them!

```maniascript
declare Text[Text][] UsersData;
UsersData = [
    [ "login" => "me",
      "name" => "still me"
    ],
    [ "login" => "you",
      "name" => "still you"
    ]
];
log(UsersData[0]["login"]); // prints "me"
```



