# Types

ManiaScript is a strongly typed language which means that every value has to be of a certain type and a value of different type will not be accepted in it's place.

## Primitive Types

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
| Int3 | `Int3` is a three dimensional vector \($$\mathbb{Z^3}$$ in mathematics\). |
| Ident | `Ident` is the type of an Id. Every class in ManiaScript has a unique `Id` property that can be used to identify it. |

## Lists and Arrays

### List

A List is a type that can store multiple values. You can declare list by adding two square brackets after a type.

```text
declare Integer[] MyList;
```

There are several basic functions to manipulate them, and you can access one element by its index. The indexes start at 0, so the first index is `0` and the last one is `MyList.count-1`. Accessing an invalid index will result in an `Out of bounds` error.

```text
// Access an element
declare FirstElement = MyList[0];

// Basic functions
declare Size = MyList.count;
declare SortedList = MyList.sort();
declare ReversedList = MyList.sortreverse();
declare SortKeys = MyArray.sortkey();
declare ReversedKeys = MyArray.sortkeyreverse();


MyList.add(42);  // adds to last element
MyList.addfirst() // adds to first element
MyList.removekey(0); // Remove the element at the index 0
MyList.remove(38);

declare DoesExist1 = MyList.existskey(58); // equivalent to 0 <= 58 < MyList.count
declare DoesExist2 = MyList.exists(12);
declare Index = MyList.keyof(28); // such as List[Index] == 28

MyList.containsonly();
MyList.containsoneof();
MyList.slice();

Declare Text json = MyList.tojson();
MyList.fromjson("{ "propery": "value"});

MyList.clear();
```

### Array

An array is similar to a list, except that you can specify a type for the index.

```text
declare Text[Integer] MyArray;
```

The array above is not a list! There is no `add` function for arrays, instead you directly assign a value for the given key.

```text
MyArray[1] = "One";
```

You can even nest them!

```text
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

### API Arrays

access by Integer or Ident

### Structs

```text
#Struct MyStruct {
//      {Type} {propertyname};
    Integer MyMember;
    Text MyTextMember;
}

main() {
    declare MyStruct MyVar;
    // declare MyStruct MyVar = MyStruct{MyMember = 1, MyTextMember = "Example"};
    log(MyVar.MyMember); //Output : 0

    MyVar.MyMember = 1;
    log(MyVar.MyMember); //Output : 1

    declare MyStruct MyCopy = MyVar;
    log(MyCopy.MyMember); //Output : 1

    MyVar.MyMember = MyVar.MyMember + 1;

    log(MyVar.MyMember); //Output : 2
    log(MyCopy.MyMember); //Output : 1
}
```

## Vectors

Vectors are declared with pointing angles: `declare Vec2 V = <1.0, 2.0>`.  
Vector-elements can be accessed either with `X`, `Y` and `Z` \(as `V.Y`\) or like an array with the indices `0` to `2` \(like `V[1]`\) \(depending on the vector having 2 or 3 elements\). Vectors are initialized with the initial value for `Integer` or `Real` respectively, e.g. `declare Vec3 V; log(V);` will log as `<0., 0., 0.>`.

