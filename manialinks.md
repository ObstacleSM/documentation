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

| XML tag | |Description |
| :- | :- |
| <quad /> | Displays image-type content. 
Supported file-types are: .png, .jpg and .dds
Supported protocols are: file:// , http:// and https:// |
| <label /> | Displays text content. |
| <audio /> | Play audio content.
Supported formats: .ogg, .wav and .mux |
| <video /> | Displays video content. 
Supported types:  .webm |
| <graph /> | Display line graphics.
The element, needs to be filled using maniascript.|
| <gauge /> | Display progress bar.
Progress can be updated with maniascript. |


## Client side script

## Casting

## net variables

## Casting
