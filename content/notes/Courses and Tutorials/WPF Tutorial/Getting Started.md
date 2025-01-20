# Hello World


📁`MainWindow.xaml`
```xml
<Window x:Class="WpfApplication1.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="350" Width="525">
    <Grid>
        <TextBlock HorizontalAlignment="Center" VerticalAlignment="Center" FontSize="72">
            Hello, WPF!
        </TextBlock>
    </Grid>
</Window>
```

# What is XAML

eXtensible Application Markup Language - Microsoft's variant of XML for describing a GUI

A Window or Page will consist of a XAML document and a CodeBehind file, which together creates the Window/Page

```xml
<Button FontWeight="Bold" Content="A button" />
```

We set the FontWeight property, giving us bold text, and then we set the Content property, which is the same as writing the text between the start and end tag. However, all attributes of a control may also be defined like this, where they appear as child tags of the main control, using the Control-Dot-Property notation:

```xml
<Button>
    <Button.FontWeight>Bold</Button.FontWeight>
    <Button.Content>A button</Button.Content>
</Button>
```

The result is exactly the same as above, so in this case, it's all about syntax and nothing else. However, a lot of controls allow content other than text, for instance other controls. Here's an example where we have text in different colors on the same button by using several TextBlock controls inside of the Button:

```xml
<Button>
    <Button.FontWeight>Bold</Button.FontWeight>
    <Button.Content>
        <WrapPanel>
            <TextBlock Foreground="Blue">Multi</TextBlock>
            <TextBlock Foreground="Red">Color</TextBlock>
            <TextBlock>Button</TextBlock>
        </WrapPanel>
    </Button.Content>
</Button>
```

The Content property only allows for a single child element, so we use a WrapPanel to contain the differently colored blocks of text. Panels, like the WrapPanel, plays an important role in WPF and we will discuss them in much more details later on - for now, just consider them as containers for other controls.

The exact same result can be accomplished with the following markup, which is simply another way of writing the same:

```xml
<Button FontWeight="Bold">
    <WrapPanel>
        <TextBlock Foreground="Blue">Multi</TextBlock>
        <TextBlock Foreground="Red">Color</TextBlock>
        <TextBlock>Button</TextBlock>
    </WrapPanel>
</Button>
```

# Events in XAML

All of the controls, including the Window (which also inherits the Control class) exposes a range of events that you may subscribe to

On most controls you will find events like `KeyDown`, `KeyUp`, `MouseDown`, `MouseEnter`, `MouseLeave`, `MouseUp` and several others

```xml
<Window x:Class="WpfTutorialSamples.XAML.EventsSample"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="EventsSample" Height="300" Width="300">
	<Grid Name="pnlMainGrid" MouseUp="pnlMainGrid_MouseUp" Background="LightBlue">        
		
    </Grid>
</Window>
```

Notice how we have subscribed to the `MouseUp` event of the Grid by writing a method name. This method needs to be defined in code-behind, using the correct event signature. In this case it should look like this:

```c#
private void pnlMainGrid_MouseUp(object sender, MouseButtonEventArgs e)
{
	MessageBox.Show("You clicked me at " + e.GetPosition(this).ToString());
}
```

`MouseUp` event uses a delegate called `MouseButtonEventHandler`, which you subscribe to
- It has two parameters, a sender (the control which raised the event) and a `MouseButtonEventArgs` object that will contain useful information

Several events may use the same delegate type - for instance, both `MouseUp` and `MouseDown` uses the `MouseButtonEventHandler` delegate, while the `MouseMove` event uses the `MouseEventHandler` delegate
- When defining the event handler method, you need to know which delegate it uses 

Visual Studio can help us to generate a correct event handler for an event. The easiest way to do this is to simply write the name of the event in XAML

![[Images/vs_new_event.png]]

When you select `<New Event Handler>` Visual Studio will generate an appropriate event handler in your Code-behind file

# Subscribing to an event from Code-behind

There may be times where you want to subscribe to the event directly from Code-behind instead. This is done using the += C# syntax, where you add an event handler to event directly on the object

```c#
using System;
using System.Windows;
using System.Windows.Input;


namespace WpfTutorialSamples.XAML
{
	public partial class EventsSample : Window
	{
		public EventsSample()
		{
			InitializeComponent();
			pnlMainGrid.MouseUp += new MouseButtonEventHandler(pnlMainGrid_MouseUp);
		}

		private void pnlMainGrid_MouseUp(object sender, MouseButtonEventArgs e)
		{
			MessageBox.Show("You clicked me at " + e.GetPosition(this).ToString());
		}

	}
}
```

