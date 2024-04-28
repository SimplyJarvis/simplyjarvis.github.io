# How to use the Tool Tip Scripts #

### ToolTip.cs ###
* Place this on any 2D gameobject to enable a tooltip.
* Enter in a string of what the tooltip will display.
* A 2D collider is required for it to be picked up by the raycast. (Only if its not a UI Element)

### ToolTipController.cs ###
* Controls the ToolTip UI, use the "ToolTipParent" prefab to see how its structured
* A calculation is done to see which side of the display the mouse is on, this is then used to flip the side of the tooltip