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

## How to add proporties to the control?

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
        //Proporties here
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
        new PropertyMetadata(null));// keep the first parameter null, east this time
    
    public string Header
    {  
        get => (string)GetValue(HeaderProperty);
        set => SetValue(HeaderProperty, value);
    }
}
```

```xaml
<!--Header-->
<TextBlock  FontSize="21" Text="{TemplateBinding Header}"/>
```

If the output is showing error, F5 to run the program(it's for build the program).
