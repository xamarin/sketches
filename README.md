Xamarin Sample Sketches
=======================

[Xamarin Sketches](http://developer.xamarin.com/guides/cross-platform/sketches/)
are a new interactive way to try out the C# language and the APIs provided by
Xamarin. You can see results alongside each line of code, and even test UI code
right in the simulator, all without even creating a project.

Sketches are still an early preview. Please see [the documentation](http://developer.xamarin.com/guides/cross-platform/sketches/)
for install instructions and known issues and limitations.

This repository contains a few fun samples to demonstrate the power of interactive
coding.

Loading Projects or Third-Party Assemblies
-----------------------------------------

Call `LoadAssembly (pathToAssembly)` to bring any arbitrary library into
the Sketch runtime. Keep in mind that this code runs on the target platform,
so if you're on Android, the path should point to a file on the emulator's
file system.

Loading Resources
-----------------

You can bundle resources into your sketch, but there is currently no UI for it.

Create a folder next to your sketch file with a name like
"mysketch.sketchcs.Resources", and any files placed within will be available
for use in your code.

On iOS and Mac, they can be accessed through `NSBundle.MainBundle`, so you can
use API like `NSImage.ImageNamed(resourceName)` and
`UIImage.FromBundle(resourceName)`.

There is also a more general method available on all platforms called
`GetResourcePath(resourceName)`. This is currently the only way to get access
to bundled resources on Android.

See the samples in this repository for working examples.

Modifying Live UI
-----------------

Please see [the documentation](http://developer.xamarin.com/guides/cross-platform/sketches/)
for some examples. Sketches work by evaluating your code live in an "agent" app
running on the target platform. Each app provides its own way to modify the UI:

* iOS (Unified): A `RootView` static property is exposed to your Sketch. This
  is the UIView of the main UIViewController.
* iOS (Classic) and Android (Xamarin.Forms): A `RootPage` static property is
  exposed to your Sketch. This is a `Xamarin.Forms.TabbedPage` that is the
  main page of the app. You can add new Pages to `RootPage.Children`.
* Android (Android): A `RootActivity` static property is exposed to your Sketch.
  This represents the agent's running Activity.
* Mac: A `RootWindow` static property is exposed to your Sketch. When accessed,
  an NSWindow will be created that lets you add views like
  `RootWindow.ContentView.AddSubView(...)`.

For Android (Android), the following convenience method is provided:

	public static int DimToPixels (int dip, Android.Util.ComplexUnitType type = Android.Util.ComplexUnitType.Dip)
	{
		return (int)Android.Util.TypedValue.ApplyDimension (
			type, dip, RootActivity.Resources.DisplayMetrics);
	}

Reporting Issues
----------------

Please report issues in [Xamarin bugzilla](https://bugzilla.xamarin.com/enter_bug.cgi?product=Xamarin%20Studio&component=Sketches),
or stop by [our forums](http://forums.xamarin.com/categories/sketches).
