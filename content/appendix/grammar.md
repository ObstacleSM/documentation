# Grammar
simplified excerpt from the grammar
```
LineTerminator = [\n\r]

Program = Directive* (GlobalDeclaration|FunctionDefinition|LabelBlock)* MainFunction?

Identifier = IdentifierStart IdentifierPart*
IdentifierStart = [a-zA-Z_]
IdentifierPart = [a-zA-Z0-9_]

Statement = BlockStatement | LabelStatement | ForStatement | ForEachStatement | SwitchStatement | SwitchTypeStatement | IfStatement | DeclareStatement | AssignmentStatement | BuiltinFunctionStatement
BlockStatement = "{" Statement "}"
LabelStatement = ("+++" Identifier "+++")|("---" Identifier "---")
DeclareStatement = ("declare" ("persistent" | "netread" | "netwrite")? Type Identifier ("as" Identifier)? "for" Identifier ("=" Expression)? ";") | ("declare" Type? Identifier "=" Expression ";") | ("declare" Type Identifier ";");
IfStatement = "if" "(" Expression ")" Statement ElseIfStatement* ElseStatement?
ElseIfStatement = "else" "if" "(" Expression ")" Statement
ElseStatement = "else" Statement
ForStatement = "for" "(" Identifier "," Expression "," Expression ("," Expression)? ")" Statement
ForEachStatement = "foreach" "(" Identifier ("=>" Identifier)? ("in" | ",") Identifier ")" Statement
SwitchStatement = "switch" "(" Expression ")" "{" SwitchCaseStatement* DefaultStatement? "}"
SwitchCaseStatement = "case" Expression ":" Statement
DefaultStatement = "default" ":" Statement
SwitchTypeStatement = "switchtype" "(" Expression ")" "{" SwitchTypeCaseStatement* DefaultStatement? "}"
SwitchTypeCaseStatement = "case" ClassType ":" Statement
BuiltinFunctionStatement = "break" ";"|"continue" ";"|"yield" ";"|"log" "(" Expression ")" ";"|"assert" "(" Expression ")" ";"|"sleep" "(" Expression ")" ";"|"wait" "(" Expression ")" ";"|"tuning_start();"|"tuning_end();"

Text = "\"" ("\\["tnr]"|.) "\""
TemplateString = "\"\"\"" !("\"\"\"") . "\"\"\""

Integer = "-"? \d+

Real = "-"? (\d+\.\d*|\d*\.\d+)

Boolean = "True" | "False"

Vector2 = "<" Expression "," Expression ">"
Vector3 = "<" Expression "," Expression "," Expression ">"

List = "[" ListItems "]"
ListItems = (ListItem "," ListItems)|ListItem
ListItem = Expression

Array = "[" ArrayItems "]"
ArrayItems = (ArrayItem "," ArrayItems)|ArrayItem
ArrayItem = Expression "=>" Expression

UnderscoreFunction = "_(" Text ")"

Literal = Text | Integer | Real | Boolean | "Null" | "NullIdent" | Vector2 | Vector3 | List | Array | UnderscoreFunction | EnumValue

EnumValue = Identifier? "::" Identifier "::" Identifier

ClassType = Identifier
SimpleType = "Void" | "Integer" | "Real" | "Text" | "Boolean" | "Ident" | "Int3" | "Vec3" | "Vec2" | ClassType
Type = SimpleType ( "[" SimpleType? "]" )*

Directive = RequireContextDirective | IncludeDirective | ExtendsDirective | ConstDirective | SettingDirective
RequireContextDirective = "#RequireContext" Text LineTerminator
IncludeDirective = "#Include" Text "as" Identifier LineTerminator
ExtendsDirective = "#Extends" Text LineTerminator
ConstDirective = "#Const" Identifier Literal LineTerminator
SettingDirective "#Setting" Identifier Literal ("as" UnderscoreFunction|Text)? LineTerminator

FunctionBody = Statement*

GlobalDeclaration = "declare" Type Identifier ";"

FunctionDefinition = Type Identifier "(" FunctionArgumentList ")" "{" FunctionBody "}"
FunctionArgumentList = (FunctionArgument "," FunctionArgumentList)|FunctionArgument
FunctionArgument = Type Identifier

LabelBlock = "***" Identifier "***" "***" FunctionBody "***"

MainFunction = "main" "(" ")" "{" FunctionBody "}"
```