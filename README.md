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

The ability to embed resources into your Sketch is not yet supported. For now,
you have a couple of options:

1. On iOS or Mac, simply provide absolute paths to the resources you want to
   load. On Android, use `adb push` to copy resources onto the `/sdcard/`.

2. Open a terminal, and `cd` to the directory that contains your resources.
   Then run `python -m SimpleHTTPServer 8000` to start a local HTTP server.
   Then in your Sketch, call `CreateLocalUri (relativePathToResource)` to get
   a `System.Uri` for the resource. This method accepts optional `host` and
   `port` arguments.

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

Please report issues in [Xamarin bugzilla](https://bugzilla.xamarin.com/enter_bug.cgi?product=Xamarin%20Studio&component=Sketches).
