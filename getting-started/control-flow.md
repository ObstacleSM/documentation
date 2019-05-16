# Control Flow

Deciding on a "route" to take through your program is "controlling the flow" through your application. This can include both skipping parts of your code under certain circumstances or repeating instructions multiple times without actually writing them down multiple times.

## Choice

A program usually is only useful if it does different things based on conditions.

### If Else

Code following an `if`-statement only gets evaluated if the given expression evaluates to `True`. To handle the case that the condition evalutes to `False`, you can follow up with an `else`-statement without further arguments:

```text
if (List.count > 2) {
    doSomething(List);
} else {
    log("List has too few items");
}
```

When asking for an alternative condition, we don't have to nest if-else-statements in the respective else-blocks, but rather use as many `else if` constructs as we want:

```text
if (List.count == 0) {
    log("List has no items :(");
} else if (List.count <= 2) {
    log("List should have at least 3 items");
} else {
    doSomething(List);
}
```

### Switch case

To avoid a lot of `else if`-statements all checking for different values of a certain expression, we can use the `switch`-statement. In different _cases_ we ask if the given expression evaluated to this value.

```text
switch (Block.Direction) {
    case CBlock::CardinalDirections::North: {
        log("Facing north");
    }
    case CBlock::CardinalDirections::South: {
        log("Facing south");
    }
    default: {
        log("Facing east or west");
    }
}
```

The `default`-case will be executed when no other `case` is applicable. Cases are tested in their order of declaration so handling the default behaviour first would not execute the other cases. The compiler expects at least one `case`- \(or a `default`-\) block to be present.

A special version of the `switch`-statement is the `switchtype`-statement. It checks whether the given expression \(evaluating to a class instance\) matches one of the classes provided in the case statements.

```text
switchtype (Control) {
    case CMlEntry: log((Control as CMlEntry).Value);
    case CMlTextEdit: log((Control as CMlTextEdit).Value);
    default: log("not a input element");
}
```

## Loop

To do things repeatedly, programming languages use loops. ManiaScript has - like many other languages - three kinds of loops.

### While

A `while`-loop executes code as long as a given condition evaluates to `True`:

```text
declare ItemCount = 10;
while (ItemCount > 0) {
    ItemCount -= 1;
}
```

Be careful that your condition at some point evaluates to `False`, you `break;` out of the loop or call `yield;` to avoid an unterminated loop - ultimately having your script terminated for "consuming too many resources".

### For

To execute code a set number of times, you would use a `for`-loop:

```text
for (I, 2, 5) {
    log(I);
}
```

`I` will assume the values 2 to 5 \(inclusive\) throughout your code's execution. As you are probably iterating over lists or arrays a lot, keep in mind, that you can only run to `List.count - 1`.

### Foreach

When iterating over an array or a complete list, you might use the `foreach`-loop:

```text
declare MyList = ["foo", "bar", "baz"];
foreach (Item in MyList) {
    log(Item);
}
```

If you need to know the index of the item in your list \(or the key in an associative array\) you can get it like this:

```text
declare MyArray = [1 => "foo", 3 => "bar", 8 => "baz"];
foreach (Index => Item in MyArray) {
    log(Index ^ ": " ^ Item);
}
```

In every type of loop you can use the statements `break;` to exit the loop at the current statement and `continue;` to cancel further execution and start with the next iteration of the loop. You would use `break;` for example when looping over some data and want to stop the loop execution once you have found an item. `continue;` would be used if you checked some conditions on the current item and don't need to execute further code on that item.

```text
declare CMlControl Match;
foreach (Control in Page.MainFrame.Controls) {
    if (!(Control is CMlLabel))
        continue;
    declare Label = (Control as CMlLabel);
    if (Label.Value == "match") {
        Match = Label;
        break;
    }
}
```

