When creating a WPF application, the first thing you will meet is the Window class

It serves as the root of a window and provides you with the standard border, title bar and maximize, minimize and close buttons

A WPF window is a combination of a XAML (.xaml) file, where the `<Window>` element is the root, and a `CodeBehind` (.cs) file

```xml
<Window x:Class="WpfApplication1.Window1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Window1" Height="300" Width="300">
    <Grid>

    </Grid>
</Window>
```

The `x:class` attribute tells the XAML file which class to use

By default, it looks like this

```cs
using System;
using System.Windows;
using System.Windows.Controls;
//…more using statements

namespace WpfApplication1
{
    /// <summary>
    /// Interaction logic for Window1.xaml
    /// </summary>
    public partial class Window1 : Window
    {
        public Window1()
        {
            InitializeComponent();
        }
    }
}
```

`Window1` class is defined as partial, because it's being combined with your XAML file in runtime to give you the full window

This is what the call to `InitializeComponent()` does

# Important Window Properties

WPF Window class has a bunch of interesting attributes that you may set to control the look and behaviour of your application window

Icon - Allows you to define the icon of the window, which is usually shown in the upper left corner, to the left of the window title.

`ResizeMode` - This controls whether and how the end-user can resize your window. The default is CanResize, which allows the user to resize the window like any other window, either by using the maximize/minimize buttons or by dragging one of the edges. CanMinimize will allow the user to minimize the window, but not to maximize it or drag it bigger or smaller. NoResize is the strictest one, where the maximize and minimize buttons are removed and the window can't be dragged bigger or smaller.

`ShowInTaskbar` - The default is true, but if you set it to false, your window won't be represented in the Windows taskbar. Useful for non-primary windows or for applications that should minimize to the tray.

`SizeToContent` - Decide if the Window should resize itself to automatically fit its content. The default is Manual, which means that the window doesn't automatically resize. Other options are Width, Height and WidthAndHeight, and each of them will automatically adjust the window size horizontally, vertically or both.

`Topmost` - The default is false, but if set to true, your Window will stay on top of other windows unless minimized. Only useful for special situations.

`WindowStartupLocation` - Controls the initial position of your window. The default is Manual, which means that the window will be initially positioned according to the Top and Left properties of your window. Other options are CenterOwner, which will position the window in the center of it's owner window, and CenterScreen, which will position the window in the center of the screen.

`WindowState` - Controls the initial window state. It can be either Normal, Maximized or Minimized. The default is Normal, which is what you should use unless you want your window to start either maximized or minimized

# Working with `App.xaml`

`App.xaml` is the declarative starting point of your application

Visual Studio will automatically create it for you when you start a new WPF application, including a Code-behind file called `App.xaml.cs`

The two files are partial classes, working together to allow you to work in both markup (XAML) and Code-behind

`App.xaml.cs` extends the Application class, which is a central class in a WPF Windows application. .NET will go to this class for starting instructions and then start the desired Window or Page from there. This is also the place to subscribe to important application events, like application start, unhandled exceptions and so on

## Structure

When creating a new application, the automatically generated `App.xaml` will look something like this:

```xml
<Application x:Class="WpfTutorialSamples.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             StartupUri="MainWindow.xaml">
    <Application.Resources>

    </Application.Resources>
</Application>
```

The main thing to notice here is the `StartupUri` property. This is actually the part that instructs which Window or Page to start up when the application is launched. In this case, `MainWindow.xaml` will be started

## `App.xaml.cs` structure

The matching `App.xaml.cs` will usually look like this for a new project:

```cs
using System;
using System.Collections.Generic;
using System.Windows;

namespace WpfTutorialSamples
{
	public partial class App : Application
	{

	}
}
```

You will see how this class extends the Application class, allowing us to do stuff on the application level

For instance, you can subscribe to the `Startup` event, where you can manually create your starting window.

Here's an example:

```xml
<Application x:Class="WpfTutorialSamples.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
			 Startup="Application_Startup">
    <Application.Resources></Application.Resources>
</Application>
```

Notice how the `StartupUri` has been replaced with a subscription to the `Startup` event (subscribing to events through XAML is explained in another chapter). In Code-Behind, you can use the event like this:

```cs
using System;
using System.Collections.Generic;
using System.Windows;

namespace WpfTutorialSamples
{
	public partial class App : Application
	{

		private void Application_Startup(object sender, StartupEventArgs e)
		{
			// Create the startup window
			MainWindow wnd = new MainWindow();
			// Do stuff here, e.g. to the window
			wnd.Title = "Something else";
			// Show the window
			wnd.Show();
		}
	}
}
```