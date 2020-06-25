# MultiThreadedUI-UWP

Demonstrates creating a second UI thread in UWP.

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
