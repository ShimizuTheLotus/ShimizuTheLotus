#CS And UI
We can edit UI Elements in a C# file. But it's not as same as using the XAML.
***UI elements can be reached in C# by name, but only the UI defined in XAML!***

***If you defined a UI element in C#, please use this code to reach it:***

```CSharp
UIElement uiElement = (UIElement)FindName("ElementName");
```
