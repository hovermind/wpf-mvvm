## ViewModel First Approach
The ViewModel-first approach accepts that a ViewModel shouldn't know anything about its View, but does not accept that the View should be responsible for constructing the ViewModel either. Instead, a third service is responsible for locating the correct View for a given ViewModel, and setting up its DataContext correctly.
```
public class FooModule : IModule{

  private IViewFoo _fooView;
  private IViewModelFoo _fooViewModel;
  
  public Initialize(IViewFoo fooview, IviewModelFoo fooViewModel){
    _fooView = fooview;
    _fooViewModel = fooViewModel;
    
    // set data context for foo view
    _fooview.DataContext = _fooViewModel;
  }
  
  
}
```

See: [ViewModel First Approach Details](https://github.com/canton7/Stylet/wiki/ViewModel-First)
