# Manialinks

## what is manialink

Manialink is a XML-document with certaint types of tags with parameters.
You should be able to learn the basics here by an example, but for more detailed overiview please refer W3C XML tutorial: https://www.w3schools.com/xml/xml_whatis.asp

So, manialinks are XML-files should be encoded with UTF-8 without bom-header.
 
To start manialink you need basically the xml header and define manialink with the version you would like to use. This tutorial will use version 3.

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes" ?>

<manialink version="3">
	// this is comment
</manialink>
```

## Manialink basic

Manialink elements consists of different basic XML-tags, which are introduced below.

| XML tag | Description |
| :---: | :--- |
| `<quad/>` | Displays image-type content. <br/> Supported file-types are: .png, .jpg and .dds <br/>Supported protocols are: file:// , http:// and https:// |
| `<label/>` | Displays text content. |
| `<audio/>` | Play audio content.<br/>Supported formats: .ogg, .wav and .mux |
| `<video/>` | Displays video content.<br/>Supported types:  .webm |
| `<graph/>` | Display line graphics.<br/>The element, needs to be filled using maniascript.|
| `<gauge/>` | Display progress bar.<br/>Progress can be updated with maniascript. |
| `<entry/>` | Display entry-inputbox.<br/> Depending on which scope the manialink is used, the text can be retrieved using http post, dedicated server callback or maniascript accessors. 
| `<fileentry />` | Displays inputbox for file with local file browser.<br/>Note: Works same as entry, but returns relative path to file. |
| `<textedit />` | Displays multiline text editor.<br/>This element can be used as multiline entry or maniascript editor with syntax highlighting. Works same as entry for returning the contents. |
| `<frame>`<br/>`</frame>` | This is different from the previous elements, as this itself doesn't show anything, but it can be used to group contents to a container. The grouped contents then can be then easily moved / repositioned. |
|`<framemodel>`<br/>`</framemodel>` | This element defines a model container for the frame instances, works same as frames. By default the frame model is not shown at ui, you display the model using frame instaces. |
| `<frameinstance/>` | This element is used to display contents defined with frame model. |

## Manialink positioning system

Manialink uses currently positioning system which is optimized for 16:9 displays.
The origo is defined to the center at the screen, at position <0.0, 0.0>
Depending the proportions and the size of the screen, then contents are streched and scaled to always have same relative size and positions on the screen. The viewport total width is 320 units and total height is 180 units. Illutration below shows how the coordinate system works in practise.

## Defining attributes for elements

Each above introduced elements has many different attributes which they operate, but they all share some common ones. Attributes are always written inside the tag and after the basic element, see example with an attribute defined with value.

```xml
<label attribute=”value” />
```

Each element normally are defined with multiple attributes, to add more just separate the attributes with space, the order of attribute doesn't count.

```xml
<frame attribute1=”value” attribute2=”value2”></frame>
```

## Basic attributes for all manialink elements

| XML tag | Description |
| :- | :- |
| pos=”X.x Y.y” | Sets the position of the element at coordinates system, see the coordinate system defined below. You can use integers or floats to define the absolute position. |
| z-index=”Z.z” | Z-index defines the elements layers position.Indicies are always calculated within the container they are bound.<br/>You can think the z-index as pile papers. First one is 1 and second one is 2... and so on, so if you define indexes 1 and 2, the bigger value will overlap the smaller one, like the papers would overlap on your desk. |
| scale=”i.i” | Sets the scale of the element, number must be zero or positive interger or float. |
| rot=”i.i” | Set the rotation of the element in degrees. Positive goes clockwice and negative the other way. Number can be integer or float. |
| hidden=”1” | You can set hidden attribute to hide the element from the view.<br/>Values: 0 – shown , 1 – hidden |
| id=”value” | You can define name for the element. This id works kinda same as id in html. The values should be unique per manialink, normally you would search the element by its id using maniascript. |
| class=”class1 class2” | Classes works same as html. You can define multiple classes for one element and use maniascript to access them. |

## Additional attributes for each elements

Quite meny of the elements share additional Size and Aligment attributes, these shared attributes are marked with grey background.


You should define either color, style or image for the quad:


You can also recolor / alter the colors of the image or style element.

## Client side script

## Casting

## net variables

## Casting
