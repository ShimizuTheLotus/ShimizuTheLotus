#CS And UI
We can edit UI Elements in a C# file. But it's not as same as using the XAML.
***UI elements can be reached in C# by name, but only the UI defined in XAML!***

***If you defined a UI element in C#, please use this code to reach it:***

```csharp
UIElement uiElement = (UIElement)FindName("ElementName");
//UIElement could be replaced by the type of the UI element, such as TextBlock
//uiElement could be replaced with any name you want(in C# variable naming rules),
//but it's not the Name property of your UI element. FindName finds element having UIElement.Name the same value with the string.
//ElementName is the UIElement.Name property.
```
