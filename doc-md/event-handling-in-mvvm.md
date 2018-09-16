In MVVM design pattern, the view model is the component that is responsible for handling the application's presentation logic and state. 
This means that the view's code-behind file should contain no code to handle events that are raised from UI element nor should it contain any domain specific logic.

Ideally, the code-behind of a view (typically a `Window` or a `UserControl`) contains only a constructor that calls the `InitializeComponent` method and 
perhaps some additional code to control or interact with the view layer that is difficult or inefficient to express in XAML, e.g. complex animations.

In other words, an MVVM application should not have any code as below:
```
// MainWindow.xaml
<Button Content="Click here!" Click="btn_Click"/>
 

// MainWindow.xaml.cs
protected void btn_Click(object sender, RoutedEventArgs e)
{
  /* This is not MVVM! */
}
```

## Commands
In addition to providing properties to expose data to view, the ViewModel defines commands that respond to user actions.
A command is an object that implements the `System.Windows.Input.ICommand` interface and encapsulates the code for the action to be performed. 
It can be data bound to a UI control in the view to be invoked as a result of a mouse click, key press or any other input event. 
As well as the command being invoked as the user interacts with the UI, a UI control can be automatically enabled or disabled based on the command.

`ICommand` interface specifies three members:
* the method `Execute` is called when the command is actuated. It has one parameter, which can be used to pass additional information from the caller to the command
* the method `CanExecute` returns a Boolean. If the return value is true, it means that the command can be executed. The parameter is the same one as for the `Execute` method. 
When used in XAML controls that support the Command property, the control will be automatically disabled if CanExecute returns false
* the `CanExecuteChanged` event handler must be raised by the command implementation when the `CanExecute` method needs to be reevaluated
In XAML, when an instance of ICommand is bound to a control’s `Command` property through a data-binding, raising the `CanExecuteChanged` event will automatically call the `CanExecute` method, and the control will be enabled or disabled accordingly

WPF provides two implementations of the `ICommand` interface:
* `RoutedCommand`
* `RoutedUICommand` (sub-class of `RoutedCommand`, adds a Text property)

However, neither of these implementations are especially suited to be used in a view model as they search the visual tree from the focused element and up for 
an element that has a matching [CommandBinding](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/commanding-overview#commandbinding) object in its `CommandBindings` collection and then executes the Execute delegate for this particular `CommandBinding`. 
Since the command logic should reside in the view model, you don't want to setup a `CommandBinding` in the view in order to connect the command to a visual element. 
Instead, you can create your own command by creating a class that implements the `ICommand`.

### [RelayCommand](https://github.com/hovermind/wpf-ninja/blob/master/doc-md/data-binding/relay-command.md)
### [RelayCommand Using Commander.Fody](https://github.com/DamianReeves/Commander.Fody)
### [Interaction Triggers](https://github.com/hovermind/wpf-ninja/blob/master/doc-md/data-binding/interaction-triggers.md)
