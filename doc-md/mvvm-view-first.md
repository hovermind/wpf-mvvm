## View First Approach
The ViewModel should know nothing about the View, but that View should be aware of the ViewModel. The obvious way to attach a View and ViewModel, then, you have the View constructs its ViewModel in its codebehind - something like this:
```
public MainWindow()
{
    InitializeComponent();
    this.DataContext = new EmployeeViewModel();
}
```

**In XAML**
`MainWindow.xaml`
```
<Window x:Class="SampleApplication.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:SampleApplication"
    Title="MainWindow" Height="350" Width="525">
	
    <Grid>
    
        <TextBox Grid.Column="1" Text="{Binding Id}" />
        <TextBox Grid.Column="1" Text="{Binding Name}" />
		
    </Grid>
	
</Window>
```
## Static Resource
```
<Window x:Class="SampleApplication.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:SampleApplication"
    Title="MainWindow" Height="350" Width="525">
	
    <Window.Resources>
        <local:EmployeeViewModel x:Key="EmployeeViewModel" />
    </Window.Resources>
	
    <Grid DataContext="{StaticResource EmployeeViewModel}">

        <TextBox Grid.Column="1" Text="{Binding Id}" />
        <TextBox Grid.Column="1" Text="{Binding Name}" />
		
    </Grid>
	
</Window>
```

## Element Tag
```
<Window x:Class="SampleApplication.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:SampleApplication"
    Title="MainWindow" Height="350" Width="525">
	
    <Window.DataContext>
        <local:EmployeeViewModel />
    </Window.DataContext>
	
    <Grid>

        <TextBox Grid.Column="1" Text="{Binding Id}" />
        <TextBox Grid.Column="1" Text="{Binding Name}" />
		
    </Grid>
	
</Window>
```
