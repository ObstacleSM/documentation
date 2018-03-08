# Manialinks

## What is manialink

Manialink is a XML-document with certaint types of tags with parameters.
You should be able to learn the basics here by an example, but for more detailed overiview please refer W3C XML tutorial: https://www.w3schools.com/xml/xml_whatis.asp

So, manialinks are XML-files should be encoded with UTF-8 without bom-header.
 
To start manialink you need basically the xml header and define manialink with the version you would like to use. This tutorial will use version 3.

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes" ?>

<manialink version="3">
	<!-- this is comment -->
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
| `<fileentry/>` | Displays inputbox for file with local file browser.<br/>Note: Works same as entry, but returns relative path to file. |
| `<textedit/>` | Displays multiline text editor.<br/>This element can be used as multiline entry or maniascript editor with syntax highlighting. Works same as entry for returning the contents. |
| `<frame>`<br/>`</frame>` | This is different from the previous elements, as this itself doesn't show anything, but it can be used to group contents to a container. The grouped contents then can be then easily moved / repositioned. |
|`<framemodel>`<br/>`</framemodel>` | This element defines a model container for the frame instances, works same as frames. By default the frame model is not shown at ui, you display the model using frame instaces. |
| `<frameinstance/>` | This element is used to display contents defined with frame model. |
| `<dico>` | Creates dictionary for multilingual label messages |
| `<include>` | Includes a local or remote manialink file |
 
 
## Manialink positioning system

Manialink uses currently positioning system which is optimized for 16:9 displays.
The origo is defined to the center at the screen, at position `0.0, 0.0` Depending the proportions and the size of the screen, then contents are streched and scaled to always have same relative size and positions on the screen. The viewport total width is 320 units and total height is 180 units. Illutration below shows how the coordinate system works in practise.

![](/assets/manialink.png)

## Defining attributes for elements

Each element has many different attributes which they operate, but they all share some common ones. Attributes are always written inside the tag and after the basic element, see example with an attribute defined with value.

```xml
<label attribute=”value” />
```

Each element normally are defined with multiple attributes, to add more just separate the attributes with space, the order of attribute doesn't count.

```xml
<frame attribute1=”value” attribute2=”value2”></frame>
```

## Basic attributes for all manialink elements

| XML tag | Description |
| :---: | :--- |
| pos=”X.x Y.y” | Sets the position of the element at coordinates system, see the coordinate system defined below. You can use integers or floats to define the absolute position. |
| z-index=”Z.z” | Z-index defines the elements layers position.Indicies are always calculated within the container they are bound.<br/>You can think the z-index as pile papers. First one is 1 and second one is 2... and so on, so if you define indexes 1 and 2, the bigger value will overlap the smaller one, like the papers would overlap on your desk. |
| scale=”i.i” | Sets the scale of the element, number must be zero or positive interger or float. |
| rot=”i.i” | Set the rotation of the element in degrees. Positive goes clockwice and negative the other way. Number can be integer or float. |
| hidden=”1” | You can set hidden attribute to hide the element from the view.<br/>Values: 0 – shown , 1 – hidden |
| id=”value” | You can define name for the element. This id works kinda same as id in html. The values should be unique per manialink, normally you would search the element by its id using maniascript. |
| class=”class1 class2” | Classes works same as html. You can define multiple classes for one element and use maniascript to access them. |

### Quad

##### Common attributes

| XML tag | Description |
| :---: | :--- |
| size=”W.w H.h” | Sets the size of the element.<br/>Width:  W.w<br/>Height: H.h |
| halign=”alignement” | Sets horizontal alignement of the element:<br/>left, center, right |
| valign=”alignement” | Sets vertical alignement of the element:<br/>top, center, center2, bottom |
| opacity=”1” | Sets the tranparency, 1 = fully visible, 0 = invisible.<br/>Notice: the element links and scriptevents are still active, to disable use hidden feature or hide() with maniascript. |
| scriptevents=”1” | Sets if the element is registered for emitting events for maniascript. |
| action=”value” | Sets the action to be used with dedicated server callback system. |
| url=”url” | Sets redirect to url when clicked. |
| manialink=”uri” | Sets redirect to manialink when clicked |

##### Quad specific

| XML tag | Description |
| :---: | :--- |
| image="uri" | Set the image used for the element.<br/><br/>Supported file-types are: .png, .jpg and .dds<br/>Supported protocols are: file:// , http:// and https:// |
| imagefocus="uri" | Set the image used when mouse is being hovered upon the element.<br/><br/>Supported file-types are: .png, .jpg and .dds<br/>Supported protocols are: file:// , http:// and https:// |
| style="style" | Defines predefined style to be used as image, you need to define also substyle.<br/><br/>Refer: manialink://styles for full preview
| substyle="substyle" | Defines predefined substyle to be used as image, you need also define style.<br/><br/>Refer: manialink://styles for full preview |
| styleselected="1" | If the style has mousehover state, use that.<br/>bgcolor="rrggbbaa" Sets background color. <br/>You can use following color syntaxes: <br/>RGB, RGBA, RRGGBB, or RRGGBBAA syntax |
| colorize="rrggbb" | Sets colorize value for the element, this is very useful. You can change the green-colored contents to color of your choosing, all other colors are left intact. |
| modulatecolor="rrggbb" | Sets modulate color: this modulates the hue of the image. <br/>For best results use grayscale images. |
| autoscale="0" | To disable automatic scaling. |
| keepratio="value" | Sets the behaviour on resizeing:<br/>values here are following, notice the capital letters: "Inactive", "Fit", "Clip" |

### Label

##### Common attributes

| XML tag | Description |
| :---: | :--- |
| size="W.w H.h" | Sets the size of the element.<br/>Width:  W.w<br/>Height: H.h |
| halign="alignement" | Sets horizontal alignement of the element:<br/>left, center, right |
| valign="alignement" | Sets vertical alignement of the element:<br/>top, center, center2, bottom |
| scriptevents="1" | Sets if the element is registered for emitting events for maniascript. |
| opacity="1" | Sets the tranparency, 1 = fully visible, 0 = invisible. <br/><br/>Notice: the element links and scriptevents are still active, to disable use hidden feature or hide() with maniascript. |
| action="value" | Sets the action to be used with dedicated server callback system. |
| url="url" | Sets redirect to url when clicked. |
| manialink="uri" | Sets redirect to manialink when clicked |

##### Text style Common attributes
| XML tag | Description |
| :---: | :--- |
| style="value" | Sets style/font of the label.<br/><br/>Refer: manialink://styles for valid styles. |
| textfont="value" | Sets embed font to be used, usable on titlepacks. |
| textsize="f"| Sets text size, float numbers can be used.|
| textcolor="rrggbbaa" | Set text color. |
| focusareacolor1="rrggbbaa" | Sets text background color, when scriptevents="1"|
| focusareacolor2="rrggbbaa" | Sets text mouse hover background color, when scriptevents="1"|

##### Label attributes
| XML tag | Description |
| :---: | :--- |
| text="value"| Sets the text to be displayed|
| textprefix="value"| Sets the prefix for text to be displayed |
| textemboss="b"| Sets text emboss, values can be "1" or "0"|
| autonewline="b" | Sets if new lines should be applied when text doesn't fit on the bounding box, "1" or "0"|
| maxline="i" | Sets maximum lines to be used, use integer numbers|
|
| translate="b"| Sets if the text should use translations. In this case use Dico-element for defining multilingual messages, instead of using text="value", use textid="id"|
| textid="id"| Sets multilingual textid for looking up translation from Dico-element, note this is used as XML-tag in Dico.|

### Dico

Creates a dictionary for multilingual support, example shown below:

```xml
<dico>
  <language id="fr">
   <example1>Salut</example1>
  </language>
  <language id="en">
   <example1>Hello</example1>
  </language>
</dico>

<label textid="example1" />
```

The last defined language will be used as the default one, when no matching language is found for game client.

### Entry

##### Common attributes

| XML tag | Description |
| :---: | :--- |
| size="W.w H.h" | Sets the size of the element.<br/>Width:  W.w<br/>Height: H.h |
| halign="alignement" | Sets horizontal alignement of the element:<br/>left, center, right |
| valign="alignement" | Sets vertical alignement of the element:<br/>top, center, center2, bottom |
| scriptevents="1" | Sets if the element is registered for emitting events for maniascript. |

##### Text style Common attributes
| XML tag | Description |
| :---: | :--- |
| style="value" | Sets style/font of the label.<br/><br/>Refer: manialink://styles for valid styles. |
| textfont="value" | Sets embed font to be used, usable on titlepacks. |
| textsize="f"| Sets text size, float numbers can be used.|
| textcolor="rrggbbaa" | Set text color. |
| focusareacolor1="rrggbbaa" | Sets text background color, when scriptevents="1"|
| focusareacolor2="rrggbbaa" | Sets text mouse hover background color, when scriptevents="1"|

##### Entry attributes
| XML tag | Description |
| :---: | :--- |
| default="value" | Sets default value |
| name="value" | Set name for the entry. Name will be used for returning the value back (for http get string or dedicated server as xmlrpc array). |
| selecttext="b" | Sets if the text is automaticly selected when element gets focus. use "1" or "0" |
| textformat="value"| Sets the format used: values can be "Basic", "Password", "Newpassword", notice capital letters|


### Textedit


##### Common attributes

| XML tag | Description |
| :---: | :--- |
| size="W.w H.h" | Sets the size of the element.<br/>Width:  W.w<br/>Height: H.h |
| halign="alignement" | Sets horizontal alignement of the element:<br/>left, center, right |
| valign="alignement" | Sets vertical alignement of the element:<br/>top, center, center2, bottom |
| scriptevents="1" | Sets if the element is registered for emitting events for maniascript. |

##### Text style Common attributes
| XML tag | Description |
| :---: | :--- |
| style="value" | Sets style/font of the label.<br/><br/>Refer: manialink://styles for valid styles. |
| textfont="value" | Sets embed font to be used, usable on titlepacks. |
| textsize="f"| Sets text size, float numbers can be used.|
| textcolor="rrggbbaa" | Set text color. |
| focusareacolor1="rrggbbaa" | Sets text background color, when scriptevents="1"|
| focusareacolor2="rrggbbaa" | Sets text mouse hover background color, when scriptevents="1"|

##### Textedit attributes
| XML tag | Description |
| :---: | :--- |
| default="value" | Sets default value |
| name="value" | Set name for the entry. Name will be used for returning the value back (for http get string or dedicated server as xmlrpc array). |
| showlinenumbers="b" | Show line numbers. Use "1" or "0" |
| autonewline="b" | Sets if new lines should be applied when text doesn't fit on the bounding box, use "1" or "0"|
| maxline="i" | Set max lines |
| linespacing="i" | Set spacing between lines | 
| textformat="value"| Sets the format used: values can be "Basic", "Script", "Password", "Newpassword", notice capital letters|


### Fileentry

##### Common attributes

| XML tag | Description |
| :---: | :--- |
| size="W.w H.h" | Sets the size of the element.<br/>Width:  W.w<br/>Height: H.h |
| halign="alignement" | Sets horizontal alignement of the element:<br/>left, center, right |
| valign="alignement" | Sets vertical alignement of the element:<br/>top, center, center2, bottom |
| scriptevents="1" | Sets if the element is registered for emitting events for maniascript. |

##### Text style Common attributes
| XML tag | Description |
| :---: | :--- |
| style="value" | Sets style/font of the label.<br/><br/>Refer: manialink://styles for valid styles. |
| textfont="value" | Sets embed font to be used, usable on titlepacks. |
| textsize="f"| Sets text size, float numbers can be used.|
| textcolor="rrggbbaa" | Set text color. |
| focusareacolor1="rrggbbaa" | Sets text background color, when scriptevents="1"|
| focusareacolor2="rrggbbaa" | Sets text mouse hover background color, when scriptevents="1"|

##### Fileentry attributes
| XML tag | Description |
| :---: | :--- |
| default="value" | Sets default value |
| name="value" | Set name for the entry. Name will be used for returning the value back (for http get string or dedicated server as xmlrpc array). |
| selecttext="b" | Sets if the text is automaticly selected when element gets focus. use "1" or "0" |
| type="value"| Sets the type used: values can be "skin", "challenge", "map", "replay", "image", "audio", "video", "text", "zip"|
| folder="value"| Sets main folder at user files usually (my documents/Maniaplanet) |

### Audio

##### Common attributes

| XML tag | Description |
| :---: | :--- |
| size="W.w H.h" | Sets the size of the element.<br/>Width:  W.w<br/>Height: H.h |
| halign="alignement" | Sets horizontal alignement of the element:<br/>left, center, right |
| valign="alignement" | Sets vertical alignement of the element:<br/>top, center, center2, bottom |
| scriptevents="1" | Sets if the element is registered for emitting events for maniascript. |

##### Media attributes

| XML tag | Description |
| :---: | :--- |
| data="uri" | file://, http:// or https:// starting uri. Supports .mux or .ogg|
| play="b" | Sets autoplay, can be "1" or "0" |
| loop="b" | Sets loop, can be "1" or "0" |
| music="b" | Sets the audio to be as music, can be "1" or "0" |
| volume="f" | Sets volume, 0 for max |

### Video

##### Common attributes

| XML tag | Description |
| :---: | :--- |
| size="W.w H.h" | Sets the size of the element.<br/>Width:  W.w<br/>Height: H.h |
| halign="alignement" | Sets horizontal alignement of the element:<br/>left, center, right |
| valign="alignement" | Sets vertical alignement of the element:<br/>top, center, center2, bottom |
| scriptevents="1" | Sets if the element is registered for emitting events for maniascript. |

##### Media attributes

| XML tag | Description |
| :---: | :--- |
| data="uri" | file://, http:// or https:// starting uri. Supports .webm |
| play="b" | Sets autoplay, can be "1" or "0" |
| loop="b" | Sets loop, can be "1" or "0" |
| music="b" | Sets the audio to be as music, can be "1" or "0" |
| volume="f" | Sets volume, 0 for max |


### Graph

##### Common attributes

| XML tag | Description |
| :---: | :--- |
| size="W.w H.h" | Sets the size of the element.<br/>Width:  W.w<br/>Height: H.h |
| halign="alignement" | Sets horizontal alignement of the element:<br/>left, center, right |
| valign="alignement" | Sets vertical alignement of the element:<br/>top, center, center2, bottom |
| scriptevents="1" | Sets if the element is registered for emitting events for maniascript. |


