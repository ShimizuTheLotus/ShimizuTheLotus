# Templated Controls

## What it can do?

Templated controls can make making a complex control more easily.

*If you just want to change the view of a control, refer to [Control Template](https://learn.microsoft.com/en-us/windows/apps/design/style/xaml-control-templates) rather than this.*

## How to create a Templated Control?

In your project, make sure you'll create the file at the root path of the project. Then, go to Project > Add New Item > C# > Templated COntrol, name it and then add it, you'll find a new file created, such as MyControl.md (The name is decided by yourself).

## How can I edit the view of the control?

Now you can edit how it looks like. You can also combine many controls to make it a complex control. Go to Solution Explorer, find Themes\Generic.xaml, you'll find a basic template is created automatically. Now you can place your control here:

```xaml
<!--Generic.xaml-->
<Style TargetType="local:MyControl" >
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="local:MyControl">
                <Border
                    Background="{TemplateBinding Background}"
                    BorderBrush="{TemplateBinding BorderBrush}"
                    BorderThickness="{TemplateBinding BorderThickness}">
                <!--Here to put your control in-->
                </Border>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```

*Generic.xaml is a place to put all the templates you made here. If there's too many templates, you can separate them to different .xaml files.*

Let's Create a control with a TextBlock and a Button, and add another TextBlock as header.

```xaml
<Border
     Background="{TemplateBinding Background}"
     BorderBrush="{TemplateBinding BorderBrush}"
     BorderThickness="{TemplateBinding BorderThickness}">
    <StackPanel>
        <!--Header-->
        <TextBlock FontSize="21"/>
        <!--Content-->
        <TextBlock/>
        <!--Button-->
        <Button/>
    </StackPanel>
</Border>
```

Now the view is finished. And the control is not functional yet.

## How to add properties to the control?

You can refer [this](https://learn.microsoft.com/en-us/windows/apps/winui/winui3/xaml-templated-controls-csharp-winui-3), it also works in UWP, or you want to check it in this file:

```cs
//MyControl.cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.InteropServices.WindowsRuntime;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Data;
using Windows.UI.Xaml.Documents;
using Windows.UI.Xaml.Input;
using Windows.UI.Xaml.Media;

// The Templated Control item template is documented at https://go.microsoft.com/fwlink/?LinkId=234235

namespace TemplatedControlTest
{
    public sealed class MyControl : Control
    {
        public MyControl()
        {
            this.DefaultStyleKey = typeof(MyControl);
        }
    }
}
```

Now I'll add some comments.

```cs
//MyControl.cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.InteropServices.WindowsRuntime;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Data;
using Windows.UI.Xaml.Documents;
using Windows.UI.Xaml.Input;
using Windows.UI.Xaml.Media;

// The Templated Control item template is documented at https://go.microsoft.com/fwlink/?LinkId=234235
// Ignore that, the document is not exist, at least now.

namespace TemplatedControlTest
{
    public sealed class MyControl : Control
    {
        //Properties here
        //Your codes should be in this part

        public MyControl()
        {
            this.DefaultStyleKey = typeof(MyControl);
        }

        //Or here.
    }
}
```

I'll add a Header property first.

```cs
//MyControl.cs
public sealed class MyControl : Control
{
    public MyControl()
    {
        this.DefaultStyleKey = typeof(MyControl);
    }

    public static readonly DependencyProperty HeaderProperty = DependencyProperty.Register(
        nameof(Header),//The name of property
        typeof(string),//The type of property
        typeof(MyControl),//The type of your control
        new PropertyMetadata(null));// the first parameter is the default value of this property
    
    public string Header
    {  
        get => (string)GetValue(HeaderProperty);
        set => SetValue(HeaderProperty, value);
    }
}
```

```xaml
<!--Generic.xaml-->
<!--Header-->
<TextBlock  FontSize="21" Text="{TemplateBinding Header}"/>
```

If the output is showing error, F5 to run the program(it's for build the program).

Now the Header part is finished, you can try to use it with code:

```xaml
<!--SomePage.xaml, yes, the page you wanto to use this control-->
<local:MyControl Header="This is the header"/>
```
*P.S., if you want you app fit globalization, there'll be some [problem](https://github.com/ShimizuTheLotus/ShimizuTheLotus/blob/main/Note/UWP/Templated%20Controls.md#why-my-content-was-replaced-when-i-tried-to-localization).*

## How to add event to the control?

If you want to add a event and you can use it like ```<MyControl Click="MyCOntrol_Click"/>```, check this:

Now we want to make MyControl.Click launch after the button was clicked.

Before everything, we should name the button:

```xaml
<--Generic.xaml-->
<!--Button-->
<Button x:Name="ResponceButton"/>
```

Then we'll edit the .cs file, add an EventHandler and override ```OnApplyTemplate()```:

```cs
//MyControl.cs
public sealed class MyControl : Control
{
    public MyControl()
    {
        this.DefaultStyleKey = typeof(MyControl);
    }

    public event EventHandler<RoutedEventArgs> responseButtonClicked;

    protected override void OnApplyTemplate()
    {
        base.OnApplyTemplate();
        Button button = GetTemplateChild("ResponceButton") as Button;
        if(button != null )
        {
            button.Click += (s, e) => responseButtonClicked?.Invoke(s, e);
        }
    }
}
```
Now it's finished, have a try!

## Why my content was replaced when I tried to localization?

Now the main part of MyControl looks like this:

```xaml
<!--Generic.xaml-->
<StackPanel>
    <!--Header-->
    <TextBlock FontSize="21" Text="{TemplateBinding Header}"/>
    <!--Content-->
    <TextBlock Text="{TemplateBinding Content}"/>
    <!--Button-->
    <Button x:Name="ResponceButton"/>
</StackPanel>
```

If we've set a Uid for MyControl and there's content for it like ``` <local:MyControl Uid="Id_1"/>, we'll find that the header block and content block show same text.

It is interesting. Our source code haven't mentioned anything about Uid. And I have a imagine. The text content of Uid will automatically be set to TextBlocks at the outer side, if we change our code a bit, it will be solved:

```xaml
<--Generic.xaml-->
<StackPanel>
    <!--Header-->
    <TextBlock FontSize="21" Text="{TemplateBinding Header}"/>
    <StackPanel>
        <!--Content-->
        <TextBlock Text="{TemplateBinding Content}"/>
        <!--Button-->
        <Button x:Name="ResponceButton"/>
    </StackPanel>
</StackPanel>
```

## Why the property dosen't work?

This is a sample the property can't be set:
```cs
public static new readonly DependencyProperty FontSizeProperty = DependencyProperty.Register(
    nameof(FontSize),//The name of property
    typeof(double),//The type of property
    typeof(Button),//The type of your control
    new PropertyMetadata(12.0));// the first parameter is the default value of this property

public new double FontSize
{
    get => (double)GetValue(FontSizeProperty);
    set => SetValue(FontSizeProperty, value);
}
```
``` xaml
FontSize="{TemplateBinding FontSize}"
```
Macically, if you rename the Fontsize like this:
```cs
public static new readonly DependencyProperty FontSizeProperty = DependencyProperty.Register(
    nameof(FontSize1),//The name of property
    typeof(double),//The type of property
    typeof(Button),//The type of your control
    new PropertyMetadata(12.0));// the first parameter is the default value of this property

public new double FontSize1
{
    get => (double)GetValue(FontSizeProperty);
    set => SetValue(FontSizeProperty, value);
}
```
``` xaml
FontSize="{TemplateBinding FontSize1}"
```
It will work.

**For the properties already exist that the complier suggest you to use "new" to hide the hide the origin keyword, you can code in this form in XAML**
```xaml
FontSize="{Binding FontSize,RelativeSource={RelativeSource TemplatedParent}}"
```

Then it'll work.
