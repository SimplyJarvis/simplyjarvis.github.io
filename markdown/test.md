# Mutli-Page Text Box #
The multi page text box system is made up of a Prefab and Scriptable Object for content.
## MultiTextPanel.cs ##
Within the prefab you will see a component called:
```C#
Mutli Text Panel
```
This is the main interaction point of the text box, here you can set the content by passing it a "Page Collection". There are a few useful public functions that can be called to interact with it:

The following is a script on an object that needs to pass some content and open the text box. For example this could be an interactable object that the player could click on:
```C#
PageCollection  content; //You could serialize this field
MultiTextPanel  textPanel;
void  Activate()
{
	//Updates the content in the text box, this also updates the state of the box to "Start" which in turn
	//refreshes the buttons for example to show "next" instead of "Close" if its now on page 1
	textPanel.UpdateContent(content);

	//Opens the textbox by setting the Alpha to 1 and enabling blocking raycasts in the canvas group
	textPanel.Visible(true); 

	//The following are really intended for the buttons within the prefab, but could
	// be triggered by anything (Keyboard press for example)

	//Moves to the next page
	textPanel.NextText()
	//Moves back to the previous page
	textPanel.BackText()
}
```

### State Change Event
The state change event is used for anything that needs to be updated when the overall state of the text box changes.
The states are as follows:

 - Start (First page of the text box)
 - Middle (Any page that isn't first or last)
 - End (Last page)
 - Single (If only one page of content is provided, next and back buttons need to hide or change)
 - Close (When the box is closed)

You can use this event to hook into a state change, maybe you want music to change near the end of the text box for example. This also allows the buttons themselves handle their own behaviour depending on how they are configured.

## TextPanelButton.cs
The text panel buttons also have their own script, this allows for more complex behaviour. They have their own state and type enabling different behavior from one script. Their OnActivate event is applied to the normal Unity OnClick() at run time, this is mostly so it's all managed in one place, however you could also call their OnActivate on a keyboard arrow press for example.
#### Type:
```C#
//Next, Back or Quit. Set this in editor. Changes how it interacts with the text box
tPanelButtonType  buttonType; 

//Avoids being locked to only OnClick(), its automatically added to OnClick at run time for you anyway
public  UnityEvent  OnActivate;

//If you want a sound to play when activated
[SerializeField] AudioSource  clickSound;

```