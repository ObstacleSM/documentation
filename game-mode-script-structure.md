# Game mode script stucture

So you want to create a new game mode for your favourite game?
The first step is to understand how game mode scripts are structured.

## The header

The top of the file can contain some special instructions that start with a hash `#`.

### Common headers


```maniascript
#Const CompatibleMapTypes "ObstacleArena,ObstacleTitleArena,TimeAttackArena,ObstacleBetaArena"
#Const Version            "1.2"
#Const ScriptName         "Modes/ShootMania/Obstacle.Script.txt"
```

The `#Const` instruction is used to define constants. The keyword is followed by an identifier to access the value defined just after. The examples above are only `Text` but you can use other Types too.
These three constants are used by the game to have some informations about the mode.
`CompatibleMapTypes` indicates with wich maptypes the mode is compatible
`Version` defines, well, the version of your script. It can be anything, for example all Nadeo's script use a date format `"2013-11-14"`.

___

```maniascript
#Include "Libs/Nadeo/Message.Script.txt" as Message
#Include "TextLib" as TextLib
```

The `#Include` instruction allows you to use functions or constants from separate libraries.
In the first statement above, we include a library made by Nadeo to handle Message (you can see the code of Nadeo's libs in the in-game editor or in their [github repository](https://github.com/maniaplanet/game-modes/tree/master/Common/Scripts/Libs/Nadeo)). The first parameter is the path to the library and then an identifier to use it prefixed by `as`.
The second lib is special because you can see that there is no path. It's because you can import the TextLib from any scripts. It is also the case for the MathLib, TimeLib, AnimLib and MapUnits.

The syntax to use a function from a library or read a constant is :

```maniascript
declare One = TextLib::ToInteger("1");
declare MessageScriptVersion = Message::Version;
```

### Game mode specific headers


```maniascript
#Setting S_TimeLimit       600 as _("Time limit")      ///<   Time limit on a map
#Setting S_PointLimit      25  as _("Points limit")    ///<   Points limit on a map
#Setting S_HiddenSetting   25  as "<hidden>"           ///<   Invisible by the players
```

The `#Setting` is used to allow the server hoster and the players to change the rules of your mode. The examples only use the type Integer, but you can also use `Real`, `Boolean` and `Text`.
The server hoster can edit any script settings in the playlist file or with a server controller. The players can start a vote to change the value of the settings that are not hidden.


___


```maniascript
#Extends "Modes/ShootMania/Base/ModeShootmania.Script.txt"
or
#Extends "Modes/Trackmania/Base/ModeTrackmania.Script.txt"
```

The `#Extends` instruction is the most important header when writing a mode. It allows you to focus on writing the logic on your mode rather than its structure. `ModeShootmania` or `ModeTrackmania` contains everything you need to create a standard game mode: MatchMaking, Match, Map, Round and Turn logic.

## Extending the base modes with labels


I told you earlier that every scripts should have a `main` function. That is still the case I did not lie, but game modes are so complex that there some "base" scripts already define it. It allows you to put code during special events and at the beginning and end of each step with *labels*.

Here is the structure of a standard game mode(when extending `ModeShootmania` or `ModeTrackmania`): `Server -> Match -> Map -> Round -> Turn -> PlayLoop`.

This structure is flexible and allows you to:
    * Play a match on several maps.
    * Each maps can be divided into several rounds.
    * Each rounds can be further divided into several turns.


The list of some available labels:
- Yield (it's called every tick)

- Settings
- LoadLibrairies
- LogVersions
- InitServer
- Rules
- StartServer
	- InitMatch
	- StartMatch
		- InitMap
		- StartMap
			- InitRound
			- StartRound
				- InitTurn
				- StartTurn
					- PlayLoop
				- EndTurn
			- EndRound
		- EndMap
	- EndMatch
- EndServer

Here is an example of code to display the name of the map each time a map starts.

```maniascript
***Match_StartMap***
***
ModeStatusMessage = "Current map : "^Map.MapInfo.Name;
***
```

Note that the label name is not `StartMap` but `Match_StartMap`. It is because in fact, every label above exists in two version: `Lobby_` and `Match_`. They are used when the matchmaking is enabled to distinguish the code for the lobby server and for the match. When coding a game mode without lobby, you should use the `Match_` labels.

If you want more details on how labels work, read the Labels part of Advanced Features.

Now that you know the basic structure of a game mode, it is time to create one yourself!