# Working with UI Layers
Everytime you want to create a user interface (UI) for pretty much anything, you are probably in the context of `CManiaApp` and can use [UILayer](https://maniaplanet.github.io/maniascript-reference/struct_c_u_i_layer.html)s. This chapter will focus on how to communicate with your UI.

## Creating a Layer
Layers should be regarded as what the name suggests: if you have a UI with multiple views, consider putting every view in it's own layer. A layer will retain it's state e.g. if you it is a title menu and you leave the layer to play a map. Knowing that it is convenient to keep "logical" layers like *main menu* > *solo* > *campagin* on different layers.
```c#
CUILayer GetView() {
    declare Data = ["Line 1", "Line 2", "Line 3"];
    declare View = UILayerCreate();
    View.ManialinkPage = "<manialink version=\"3\" name=\"view\">";
    foreach (I => Line in Data) {
        View.ManialinkPage ^= """<label pos="0 {{{I * -5}}}" size="10 5" text="{{{Line}}}" />""";
    }
    View.ManialinkPage ^= "</manialink>";
    return View;
}
```
In this example we initialized the view with data from our application's context. In a real program that would likely be some data like file- or player information.

## Updating Data on a Layer
If data in our application context changes we could simply initialize a new layer and replace the old one. However we would be losing any state displayed in the layer.
An alternative is to send our variables to the layer:
```c#
// in our application
LayerCustomEvent(View, "UpdateData", ["Some", "new", "data"]);
// in the script-tag in the layer's manialink code
while (True) {
    yield;
    foreach (Event in PendingEvents) {
        if (Event.Type == CMlScriptEvent::Type::PluginCustomEvent) {
            if (Event.CustomEventType == "UpdateData") {
                UpdateView(Event.CustomEventData);
            }
            else if (Event.CustomEventType == "UpdateOtherData") {
                // ...
            }
        }
    }
}
```
This example assumes the function `UpdateView` to be defined in the layer's manialink script and to be able to handle the incoming data.

While that may work for simple data (like text), you might want to transfer more "complex" data like player objects to then access and display their properties in your UI.
```c#
// in our application
declare CTmPlayer[] Players for View.LocalPage as LayerData;
LayerData = GetPlayers();
// in the layer's script
declare CTmPlayer[] Players for Page as ApplicationData;
UpdateView(ApplicationData);
```
Note that declaring an alias for the variables is not necessary and only for demonstration purposes. Like that you should keep in mind that your data could probably be named better than `Players` 😉
Also this code assumes the functions `GetPlayers()` and `UpdateView()` to exist and be type conformant. They are not standard functions.

With that our layer now can access the new data. Lastly we have to tell the layer that it has new data to access. Like before we would submit an event from the application and listen for it in the layer's maniascript, e.g. send an event with "type" `PlayersDataUpdated` and react to it by loading the variable and handling the new data.

## Updating the Application
It is equally important to react to user interaction on the UI by e.g. loading new data into the UI. We have two ways of doing this.

### The XML-Way
If you don't really need any maniascript in your layer, you might want to use the simple way to e.g. just trigger displaying a different view:
```xml
<label class="btn" text="Solo Campaign" scriptaction="loadView'solo" />
<label class="btn" text="Multiplayer" scriptaction="loadView'multiplayer" />
<label class="btn" text="Quit" scriptaction="exit" />
```
The `scriptaction`-attribute is comprised of the event type and further (optional) data, each separated by `'`.

### The Script-Way
Achieving the above of course is a lot more troublesome using the "tarnditional" way but some types of interaction require a bit more work as shown with the `entry`-element.
```xml
<label class="btn btn-loadView" text="Solo Campaign" data-view="solo" scriptevents="1" />
<entry id="search" scriptevents="1" />
<script><![CDATA[
main() {
    while (True) {
        yield;
        foreach (Event in PendingEvents) {
            if (Event.Type == CMlScriptEvent::Type::MouseClick) {
                if (Event.Control.HasClass("btn-loadView")) {
                    SendCustomEvent("loadView", [Event.Control.DataAttributeGet("view")]);
                }
            }
            else if (Event.Type == CMlScriptEvent::Type::EntrySubmit) {
                if (Event.ControlId == "search") {
                    SendCustomEvent("search", [(Event.Control as CMlEntry).Value]);
                }
            }
        }
    }
}
]]></script>
```


On the application-side you usually have some kind of [`CManiaAppEvent`](https://maniaplanet.github.io/maniascript-reference/struct_c_mania_app_event.html) and can react to that like you usually would:
```c#
foreach (Event in PendingEvents) {
    if (Event.Type == CManiaAppEvent::EType::LayerCustomEvent) {
        if (Event.CustomEventType == "loadView") {
            LoadView(Event.CustomEventData[0]);
        }
    }
}
```
Different contexts may have different types of event, but the EType `LayerCustomEvent` is inherited and should work all the same.