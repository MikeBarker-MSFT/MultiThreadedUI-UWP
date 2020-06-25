# MultiThreadedUI-UWP

Demonstrates creating a second UI thread in UWP.

## Logic demonstrated
The primary logic demonstrated is implemented in MainPage.xaml.cs
```
  CoreApplicationView newView = CoreApplication.CreateNewView();
  int newViewId = 0;
  await newView.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
  {
      Frame frame = new Frame();
      frame.Navigate(typeof(Page2), null);
      Window.Current.Content = frame;
      // You have to activate the window in order to show it later.
      Window.Current.Activate();

      newViewId = ApplicationView.GetForCurrentView().Id;
  });
  bool viewShown = await ApplicationViewSwitcher.TryShowAsStandaloneAsync(newViewId);
```

## Threading in UWP
As per the documentation of [ApplicationView](https://docs.microsoft.com/en-us/windows/uwp/design/layout/application-view):
> An app view is the 1:1 pairing of a thread and a window that the app uses to display content. It's represented by a Windows.ApplicationModel.Core.CoreApplicationView object.

Therefore, by creating a new instance of `CoreApplicationView` a new UI thread is generated.
