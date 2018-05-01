# Event Handling
To listen for events, your program in some way needs to contain a endless loop so you don't miss an event. Scripts like game-modes usually provide label-entry-points into their event handling.
```c#
main() {
    while (True) {
        // wait a bit each iteration to not block the game
        yield;
    }
}
```
In this loop we ask for the `PendingEvents`, the events that happend since the last time we asked. Keep in mind that we can't react to events immediately like that but rather within a few milliseconds.
As `PendingEvents` may (but rarely does) contain multiple events, we usually iterate over these events and check whether their `Type` identifies them as an event we want to react to.
To look at a more concrete example, the following section looks at events in ManiaLinks.

## ManiaLink Events
Usually you want your ManiaLink to be interactive in some way. Pre-ManiaPlanet we were limited to loading different pages via the `manialink` XML-attribute or open the external browser with the `url`-attribute.
As ManiaLinks are now everywhere in the user interface, we want to trigger ManiaScript actions. For a ManiaLink-element to be able to trigger an event, we need to enable `scriptevents` as XML-attribute, setting it to a truthy value, e.g. `1` or `true`.

ManiaLink are in the `CMlScript` context and elements thus fire [`CMlScriptEvent`](https://maniaplanet.github.io/maniascript-reference/struct_c_ml_script_event.html)-events in various types.

### Mouse-Events
One of the most common use cases are mouse events, e.g. clicking a button, of showing a tooltip when moving the cursor over an element. We will look at these use cases in the following example.
```xml
<manialink version="3">
    <label
        class="btn"
        data-action="showContainer"
        data-container="container1"
        data-tooltip="Will show Container 1"
        scriptevents="1"
        text="Show Container 1"
        />
    <label
        class="btn"
        data-action="showContainer"
        data-container="container2"
        data-tooltip="Will show Container 2"
        scriptevents="1"
        text="Show Container 2"
        />
    <frame id="container1"><!-- ... --></frame>
    <frame id="container2" visible="false"><!-- ... --></frame>
    <label id="tooltip" visible="false" />
    <script><![CDATA[
    main() {
        declare CMlControl CurrentContainer;
        declare CMlLabel TooltipLabel = (Page.GetFirstChild("tooltip") as CMlLabel);
        while (True) {
            yield;
            foreach (Event in PendingEvents) {
                // handle mouse click events
                if (Event.Type == CMlScriptEvent::Type::MouseClick) {
                    // to avoid checking for certain elements for example by their id,
                    // we look for a common data-* attribute
                    if (Event.Control.HasClass("btn") && Event.Control.DataAttributeExists("action")) {
                        declare Action = Event.Control.DataAttributeGet("action");
                        if (Action == "showContainer") {
                            declare ContainerId = Event.Control.DataAttributeGet("container");
                            declare Container = Page.GetFirstChild(ContainerId);
                            // if the specified container is available and not already shown,
                            // we hide the previous one and show the new one.
                            if (Container != Null && Container != CurrentContainer) {
                                CurrentContainer.Hide();
                                CurrentContainer = Container;
                                CurrentContainer.Show();
                            }
                        }
                    }
                }
                if (Event.Type == CMlScriptEvent::Type::MouseOver) {
                    // elements which should trigger a tooltip have the data-tooltip attribute
                    // containing the text to be displayed
                    if (Event.Control.DataAttributeExists("tooltip")) {
                        TooltipLabel.Value = Event.Control.DataAttributeGet("tooltip");
                        TooltipLabel.Show();
                    }
                }
                if (Event.Type == CMlScriptEvent::Type::MouseOut) {
                    if (Event.Control.DataAttributeExists("tooltip")) {
                        TooltipLabel.Hide();
                    }
                }
            }
        }
    }
    ]]></script>
</manialink>
```
Eventhough some event handling code seems similar and we only *expect* a certain type of events, it is important to check for the event type, as all events have the same fields, but your script will break, if it tries to work with the `Control` of a key-event, which will be `Null`.

### Input events
`CMlEntry` elements may trigger a `CMlScriptEvent::Type::EntrySubmit` event when pressing the submit button.

### Custom events
Within a manialink it is not possible to fire and handle custom events. (`SendCustomEvent()` sends an event to the surrounding `CManiaApp`.) However there are certain possibilities to achieve the result of events:
* Mimic the behaviour of `PendingEvents` and keep an array on your own where you push event data and every loop iteration after checking for your custom events, clear the array.
* Use label-entry-points where you would trigger your event and then implement the behaviour once somewhere else.
* Call handler-functions where you would trigger your event. This comes with the pros and cons of having an own scope and limits to modifying the state.