# Advanced features

## Aliases

When dealing with API arrays (arrays already defined) like `Players` in game modes or `Frame.Controls` in manialinks, it is often better to use aliases. Aliases are a special kind of variables that only work with API arrays, it works like this:

```maniascript
// Imagine that they are two players
// Player A has 5 points
// Player B has 0 points

declare FirstPlayer = Players[0];
declare FirstPlayerAlias <=> Players[0];

// The players array is sorted by scores automatically
// So both FirstPlayer and FirstPlayerAlias refer to Player A

Players[1].Score.Points += 10;

// FirstPlayer still refers to Player A as you would expect
// FirstPlayerAlias is now referring to Player B, the current Players[0]
```

In a nutshell, an alias is like a pointer in C, it points to the first player of the `Players` array.
The advantages of aliases over regular assignations is that aliases are faster and consume less ressources.

```maniascript
declare Frame\_Content = (Page.GetFirstChild("Frame\_Content") as CMlFrame);
declare Frame\_Content <=> (Page.GetFirstChild("Frame\_Content") as CMlFrame);
```

Getting an element from a manialink like this is pretty common, the two lines above do the exact same thing but the line with an alias instead of an equal sign is better!

### Extension variables




### Net variables



### Persistant variables





