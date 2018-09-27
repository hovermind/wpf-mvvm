## BindableBase (MVVM Light => ViewModelBase )
*Implements `INotifyPropertyChanged` to simplify ViewModel property change notification process.*

**Vanilla WPF:**    
The ViewModel should implement the `INotifyPropertyChanged` interface and should raise it whenever a property changes
```
public class MyViewModel : INotifyPropertyChanged
{
    private string _firstName;

    public event PropertyChangedEventHandler PropertyChanged;

    public string FirstName
    {
        get { return _firstName; }
        set
        {
            if (_firstName == value) return;

            _firstName = value;
            PropertyChanged(this, new PropertyChangedEventArgs("FirstName"));
        }
    }
}

```
In above approach, you have to write same code for every property. **So, to simplify things, you can create [Custom BindableBase](https://www.danrigby.com/2012/04/01/inotifypropertychanged-the-net-4-5-way-revisited/)**:
```
public class MyViewModel : BindableBase
{
    private string _firstName;
    private string _lastName;

    public string FirstName
    {
        get { return _firstName; }
        set { SetProperty(ref _firstName, value); }
    }

}
```
**[Prism provides `BindableBase` for us](https://github.com/PrismLibrary/Prism/blob/master/Source/Prism/Mvvm/BindableBase.cs)**. Prism Bindablebase (Abstract) Class:
```
namespace Prism.Mvvm
{

    public abstract class BindableBase : INotifyPropertyChanged
    {

        public event PropertyChangedEventHandler PropertyChanged;

		protected virtual bool SetProperty<T>(ref T storage, T value, [CallerMemberName] string propertyName = null)
		{
			if (EqualityComparer<T>.Default.Equals(storage, value)) return false;

			storage = value;
			RaisePropertyChanged(propertyName);

			return true;
		}

		protected virtual bool SetProperty<T>(ref T storage, T value, Action onChanged, [CallerMemberName] string propertyName = null)
		{
			if (EqualityComparer<T>.Default.Equals(storage, value)) return false;

			storage = value;
			onChanged?.Invoke();
			RaisePropertyChanged(propertyName);

			return true;
		}

		protected void RaisePropertyChanged([CallerMemberName]string propertyName = null)
		{
            OnPropertyChanged(new PropertyChangedEventArgs(propertyName));
        }

		protected virtual void OnPropertyChanged(PropertyChangedEventArgs args)
		{
			PropertyChanged?.Invoke(this, args);
		}

    }
}
```
