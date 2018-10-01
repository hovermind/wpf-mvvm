| kit   | Prism | MVVM Light |
|-------|-------|------------|
|ViewModelBase|`BindableBase`|`ViewModelBase` (`ViewModelBase` entends `ObservableObject` & `ObservableObject` implements `INotifyPropertyChanged`)|
|Command (`ICommand`)|`DelegateCommand`|`RelayCommand`|
|Communication|`EventAggregator`|`Messenger`|
|Validation|`IDataErrorInfo` / Annotation for WPF, (`BindableValidator` + `ValidatableBindableBase`) for UWP or Core| |
