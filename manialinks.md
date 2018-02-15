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
| :---- | :----- |
| `<quad />` | Displays image-type content. <br/> Supported file-types are: .png, .jpg and .dds <br/>Supported protocols are: file:// , http:// and https:// |
| `<label />` | Displays text content. |
| `<audio />` | Play audio content.<br/>Supported formats: .ogg, .wav and .mux |
| `<video />` | Displays video content.<br/>Supported types:  .webm |
| `<graph />` | Display line graphics.<br/>The element, needs to be filled using maniascript.|
| `<gauge />` | Display progress bar.<br/>Progress can be updated with maniascript. |
| `<entry />` | Display entry-inputbox.<br/> Depending on which scope the manialink is used, the text can be retrieved using http post, dedicated server callback or maniascript accessors. 
| `<fileentry />` | Displays inputbox for file with local file browser.<br/>Note: Works same as entry, but returns relative path to file. |
| `<textedit />` | Displays multiline text editor.<br/>This element can be used as multiline entry or maniascript editor with syntax highlighting. Works same as entry for returning the contents. |

`<frame>`
`</frame>`	This is different from the previous elements, as this itself doesn't show anything, but it can be used to group contents to a container. The grouped contents then can be then easily moved / repositioned.
`<framemodel>`
`</framemodel>`	This element defines a model container for the frame instances, works same as frames. By default the frame model is not shown at ui, you display the model using frame instaces.
`<frameinstance/>`	This element is used to display contents defined with frame model.



## Client side script

## Casting

## net variables

## Casting
