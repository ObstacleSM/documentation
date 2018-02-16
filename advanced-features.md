# Advanced features

## Aliases

When dealing with API arrays, it is often better to use aliases. Aliases are a special kind of variables that only work with API arrays, it works like this:

```maniascript
// Imagine that they are two players
// Player A has 5 points
// Player B has 0 points

declare FirstPlayer = Players[0];
declare FirstPlayerAlias <=> Players[0];

// This code doesn't work but imagine it working
// The players array is sorted by scores automatically
// So both FirstPlayer and FirstPlayerAlias refer to Player A

// Let's give some points to Player B
Players[1].Score.Points += 10;

// FirstPlayer is Player A, because we assigned the value of Players[0]
// However FirstPlayerAlias is now referring to Player B, the current Players[0]
// FirstPlayerAlias will always points to the first element of Players
```

In a nutshell, an alias is like a pointer in C, it points to the first player of the `Players` array.
The advantages of aliases over regular assignations is that aliases are faster and consume less resources.

```maniascript
declare Frame_Content = (Page.GetFirstChild("Frame_Content") as CMlFrame);
declare Frame_Content <=> (Page.GetFirstChild("Frame_Content") as CMlFrame);
```

Getting an element from a manialink like this is pretty common, the two lines above do the exact same thing but the line with an alias instead of an equal sign is better!

### Extension variables

You cannot create classes in ManiaScript, so what if you write a game mode and you want your players to have special properties? That's where you use extension variables.

An extension variable works like a variable, but instead of declaring a variable for the current scope, you **extend** an existing object. Here is an example:

```maniascript
// This code is in a SM game mode which needs to track how many times a player has respawned

//Somewhere in the PlayLoop
foreach (Event in PendingEvents) {
    if (Event.Type == CSmModeEvent::EType::OnPlayerRequestRespawn) {
        declare RespawnCounter for Event.Player = 0;
        RespawnCounter += 1;
    }
}
```

We declare extension variables like regular variables, the type is either explicitly stated or inferred from a value. There is a `for Event.Player`, it means that the variable `RespawnCounter` is now linked to that Player. You can access anywhere in the script by declaring it for that player again. Every player has now its own `RespawnCounter` variable.

Wait, you are maybe thinking that there is an error in the code above. Does the code above always set the variable to `0` and increment it by one after? Then every player should have `RespawnCounter` set to `1` no?

When you are assigning a value to an extension variable during its declaration, you are setting a **default value**. It means that if `RespawnCounter` was already set to something other than `0`, its value will not change. In other words, `RespawnCounter` will be set to `0` only if it is the first time that we declare `RespawnCounter`.

If you already have a local variable with the same name as your extension variable, or that you want to rename it locally, you can use the `as` keyword.

```maniascript
declare RespawnCounter = 12;
declare RespawnCounter as PlayerRSCounter for Player = 0;
RespawnCounter += PlayerRSCounter;
```

### Persistant variables


The keyword `persistent` can be added to a variable declaration to declare a persistant variable. Depending on where the variable is declared, it is stored either in the player's profile or in the server, and thus keep its value across different servers or server restart.


