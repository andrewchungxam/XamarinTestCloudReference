# XamarinTestCloudReference

//Note - smart quotes will not work in Repl/XTC

<ul>Common repl commands:
<li>tree</li>
<li>app.Flash("myButton");</li>
<li>app.Flash(x=>x.All("*"));</li>
<li>app.Flash(x => x.All("*").Class("UITextFieldLabel").Text("User ID"));</li>
<li>app.TapCoordinates(153, 86);</li>
<li>app.Repl ();</li>
<li>copy
</ul>
<ul>
Common UI commands:
<li>app.DismissKeyboard ();</li>
<li>app.Screenshot ("User enters phone number");</li>
<li>app.EnterText (x => x.Id ("edit_phone"), "5555555555");</li>
<li>app.ScrollDownTo ("CREATE", "linear_item");</li>
<li>app.SwipeRightToLeft (c => c.Id ("txt_title"));</li>
<li>app.DragCoordinates (200, 400, 200, 800); // (from X, from Y, to X, to Y)</li>
<li>app.Query(x=>x.Class("FormsTextView").Index(0)) </li>
</ul>
<ul>
Common Queries:
<li>app.Query("UITextFieldLabel");
<li>app.Query(); 
<li>app.Query(x => x.All());
<li>app.Query(x => x.All("*"));
<li>app.Query(x => x.All("*").Class("UITextFieldLabel"));
<li>app.Query(x => x.All("*").Class("UITextFieldLabel").Text("User ID"));
</ul>
<ul>
Complex Combinations:
<li>app.Tap (x => x.Text ("Eating Healthy").Sibling ("TheClassName")
<li>app.Tap (x => x.Text ("Eating Healthy").Sibling ("*").Id ("send_segment"));
</ul>
<ul>
Common Assertions:
<li>Assert.IsTrue(app.Query(q => q.Marked("logoutButton")).Any());
<li>Assert.IsFalse(app.Query(q => q.Marked("logoutButton")).Any());
<li>			Assert.IsNotNull(app.Query(x => x.Text(firstHospitalName)).Any());
<li>app.WaitForElement(q => q.Marked("logoutButton"));
</ul>
<ul>
System C# + UITest:
<li>var joinedUsername = string.Format ("myemail_{0}@microsoft.com", deviceNumber);
<li>var joinedUsername = $"myemail_{deviceNumber}@microsoft.com";
</ul>
<ul>
Sleep/Wait:
<li>Thread.Sleep (3000); //this would be 3 seconds
<li>Thread.Sleep (TimeSpan.FromMinutes (4));
<li>app.WaitForElement (x => x.Text ("Community Terms of Use"));
</ul>
<ul>
Device Numbers:
<li>var deviceNumber = Environment.GetEnvironmentVariable ("XTC_DEVICE_INDEX");
</ul>

App Configuration:<br/>
//On iOS - Simulator<br/>
return ConfigureApp
.iOS<br/>
.AppBundle ("../../../iOS/bin/iPhoneSimulator/Debug/XamarinForms.iOS.app")<br/>
.DeviceIdentifier ("KJ23d-45648-55D3E-WEF784F0") // Your simulator device ID<br/>
.AppBundle("/Users/USERNAME/Projects/MyFavorite.app")<br/>

//On iOS - Device<br/>
return ConfigureApp<br/>
.iOS<br/>
.DeviceIdentifier ("e2342asdfa8asdofhiaesd932h3")<br/>
.DeviceIp ("10.0.9.33")<br/>
.InstalledApp ("com.myfavoriteapp")<br/>
.StartApp();<br/>

//On Android<br/>
return ConfigureApp<br/>
.Android<br/>
.ApkFile("com.myfavoriteapp.apk") // example implies file is in SolutionFolder > bin > Debug<br/>
.StartApp ();<br/>

<ol>
Setup Issues:
<li>SetUp : System.Exception : Unable to start CalabashHostStrategyProxy
- Close down your Terminal/Repl then try running the test again</li>
<li> Unable to Instrument app:
- iOS - make sure to add the Calabash Test Server to your app - and make start it in your app delegate</li>
</ol>

------------------------------------------------
Command Line:<br/>
Windows:<br/>
packages\Xamarin.UITest.[version]\tools\test-cloud.exe submit yourAppFile.apk thePRIVATENotRealAPINumber00071 --devices 4b1b0c03 --series "master" --locale "en_US" --app-name "SimpleUITestApp" --user myemail@xamarin.com --assembly-dir pathToTestDllFolder

Example:
(From here)
C:\Users\Administrator\Desktop\CreditCardValidator.Droid (1)\CreditCardValidator.Droid\packages\Xamarin.UITest.2.0.0\tools
(Run this)
test-cloud.exe submit "C:\Users\Administrator\Desktop\CreditCardValidator.Droid (1)\CreditCardValidator.Droid\CreditCardValidator.Droid\bin\Release\com.xamarin.example.creditcardvalidator.apk" aasd_THIS_IS_WHERE_YOUR_API_KEY_GOES_34341 --devices=8c67ffb4  --assembly-dir "C:\Users\Administrator\Desktop\CreditCardValidator.Droid (1)\CreditCardValidator.Droid\CreditCardValidator.Droid.UITests\bin\Release" --user my.email.addy@xamarin.com

OS X:<br/>
mono packages/Xamarin.UITest.[version]/tools/test-cloud.exe submit yourAppFile.apk thePRIVATENotRealAPINumber00071 --devices 4b1b0c03 --series "master" --locale "en_US" --app-name "SimpleUITestApp" --user myemail@xamarin.com --assembly-dir pathToTestDllFolder

Run the command from the directory that contains the NuGet packages directory. Also, make sure you update your app name and the directory of tests. If your app file is not in the same directory as the NuGet packages, please include a direct path to the file.

Example:</br>
from here:</br>
/Users/myusername/SimpleUITestApp

Run:</br>
mono packages/Xamarin.UITest.1.3.15/tools/test-cloud.exe submit Droid/bin/Debug/com.minnick.simpleuitestapp.apk ceMYAPIKEY31dd3FD3234371 --devices 4b1b0c03 --series "master" --locale "en_US" --app-name "SimpleUITestApp" --user MyEmail@xamarin.com --assembly-dir UITests/bin/Debug

Categories:
--category "myFavorite"

------------------------------------------------------------
<ul>
<li>Cross Platform Properties you can Access:</li>
<li>Marked will access Id, label, and text:</li>
<li>so you'll be looking for on Android/iOS -> "label", “id" respectively</li>
<li>Android -> “contentDescription" => label on repl </li>
<li>iOS -> “accessibilityLabel” or "accessibilityIdentifier" => Id on Repl</li>
</ul>


Setting “AutomationID" Xamarin.Forms in iOS & Android assign the contentDescription and accessibilityIdentifier
XAML:
 `< Button x:Name="b" AutomationId="MyButton" Text="Click me" /> ` 

C#:
    `< var l = new Label { `
        `Text = "Hello, Xamarin.Forms!",`
        `AutomationId = "MyLabel"`
    `};`

Then in your test: `app.Query(x=>x.Marked("theGoodWord"));`
By using ‘Marked' - you’ll pick up all of the above on iOS / Android

Simplest way to do cross platform tests is to name the controls the same on iOS and Android

"Cross Platform Readiness"
using Query = System.Func<Xamarin.UITest.Queries.AppQuery, Xamarin.UITest.Queries.AppQuery>;

    namespace MySampleApplication
    {
        public class HomePage: BasePage
        {
        readonly Query TitleBar;
        readonly Query SearchBtn;

            public HomePage()
            {
        
                if (OnAndroid)
                {
                TitleBar = x => x.Id("toolbar_title");
                SearchBtn = x => x.Id("fab_button");
                }

                if (OniOS)
                {
                TitleBar = x => x.Marked("Hello");
                }
            }
        }
    }

^ Use the above in a test (ex.  app.Tap(TitleBar);   )

Clearing App instead of Deleting it (latest version of UITest)
`app = ConfigureApp`
               ` .Android`
               ` .ApkFile("app_path")`
                `.StartApp(Xamarin.UITest.Configuration.AppDataMode.Clear);`

ADDING MULTIPLE USERS

`			var deviceNumber = Environment.GetEnvironmentVariable ("XTC_DEVICE_INDEX");`

`			var joinedUsername = string.Format ("myemail_{0}@microsoft.com", deviceNumber);`

CROSS-PLATFORM DIVERGENCE:
``` 
readonly Query AddTaskButtonUsingIds; 
readonly Query AddTaskButton; 
```


``` 
  public HomeScreen(IApp app, Platform platform) : base(app, platform)
        {
            AddTaskButtonUsingIds = x => x.Marked("AddButton");

            if (platform == Platform.iOS)
                AddTaskButton = x => x.Class("UIBarButtonItem").Index(0);
            else
                AddTaskButton = x => x.Class("Button").Index(0);
        } 
```


ANDROID : SETUP
```  
<Button
        android:id="@+id/AddButton"
        android:text="Add Task"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:contentDescription="AddButton" /> 
```
        
IOS : SETUP
``` 
protected void Initialize()
        {
            var barButton = new UIBarButtonItem(UIBarButtonSystemItem.Add)
            {
                AccessibilityIdentifier = "AddButton"
            };
            NavigationItem.SetRightBarButtonItem (barButton, false);
            NavigationItem.RightBarButtonItem.Clicked += (sender, e) => { ShowTaskDetails(new TodoItem()); };
        } 
```        

-----
WEBVIEW SHORTCUT:
The below will get you the URL which you'll need to inspect
 a. iOS: app.Query(x => x.WebView().Invoke("request").Invoke("URL").Invoke("absoluteString"))
 b. Android: app.Query(x => x.WebView().Invoke("getUrl"))
 
 NOW INSPECT THAT URL
 You can view the CSS of that webview - you can do this with Chrome for example:
 Chrome > View > Developer > Developer Tools
 
 On the right panel - you'll see the HTML/CSS.  On the upper left of that panel - you'll see a toggle-able icon (a square with an arrow in it).  Toggling that icon will switch between allowing you to navigate through the webpage -- or clicking a specific element and inspecting it.  You'll need to do both.
 
 One you find an element you care about you can interact with it.  
 As an example - let's say you care about this element:
```
<span class="thing that I am interested in">
 ```
 Then you can interact with it, like this:
 ```
 app.Tap(x=>x.CSS(".thing.that.I.am.interested.in"));  //note how . marks preceed the entry and fill in the spaces as well.
 ```
 You preceeded the class with a "."
 If it were an ID, you can preceed it with a "#" mark.
 
 
 
 c. If HTML is embedded on an internal resource - try this: app.Query(x => x.Css("body"));

ENTER TEXT (need for certain Hybrid situations):
```
app.Tap("searchButtonBackground");
app.Query(x => x.Class("android.widget.EditText").Invoke("setText", "The Text I want to Enter"));
app.PressEnter();
```     
-----        





SOMETMES YOU NEED TO DOWNLOAD THE ANDROID APP ON YOUR DEVICE (FOR EXAMPLE TO ACCESS AN APP FROM THE GOOGLE PLAY STORE):
Connect your device to your Mac.
Open Terminal:
Go here:
cd ~/Library/Developer/Xamarin/android-sdk-macosx/platform-tools

NOTE // 
Do not go here (use adb tools above):
(NOT THIS) cd ~/Library/Android/sdk/platform-tools (NOT THIS)

Look for your package:
(notice the use of the "./" before command to use a local command vs a global command).

List your 3rd-party packages 
./adb shell pm list packages -f -3

Or skip ahead and use this:
./adb shell pm path your-package-name.
./adb shell pm path com.myCompanyApp.android

OUTPUT WILL LOOK LIKE THIS:
package:/data/app/XX.XX.XX.apk=YY.YY.YY
FROM ABOVE - YOU WANT THIS:
/data/app/XX.XX.XX.apk

FOR ANDROID VERSIONS BELOW 7.0//
THEN THIS:
(GENERAL COMMAND) ./adb pull full/directory/of/the.apk
(Example of SPECIFIC COMMAND) ./adb pull /data/app/com.myCompanyApp.android-1/mybase.apk 

FOR ANDROID VERSIONS BELOW 7.0+
(GENERAL COMMAND)adb shell cp /data/app/com.theCompanyName.android-1/base.apk /storage/emulated/0/Download
(GENERAL COMMAND)adb pull /storage/emulated/0/Download/base.apk

NOW YOUR APK FILE WILL DOWNLOAD THE DIRECTORY WHERE YOU ARE RUNNING YOUR COMMANDS:
In this case - it will be called base.apk

IN TERMINAL - you can type the following to open a FINDER WINDOW and then copy your new file base.apk to the directory of your choosing:
open .

-----
SITUATIONS WHERE WARNINGS MAY OR MAY-NOT POP-UP

```   
[Test]
public void MyImportantMethod ()
{
//ADD THE BELOW TO YOUR METHOD
	try 
	{
	//DISMISS POP-UP HERE
	//IT IS IMPORTANT TO NOT HAVE SCREENSHOTS HERE OR YOUR SCREENSHOTS WILL BE OUT OF SYNC WHICH WILL TRIGGER ERRORS
    	app.WaitForElement (x => x.Id ("welcome1"));
	app.Tap (x => x.Id ("welcome"));
	} 
	catch (Exception e) 
	{
	Console.WriteLine ("{0} Exception caught.", e);
	}
//ADD THE ABOVE TO YOUR METHOD

// here is where you do the rest of your method
   app.Tap("Sign-in");
   }
```   
-----
IF STATEMENTS
You should in general not sure IF statements - you want deterministic tests:

if(!app.Query(x=>x.Marked("foo")).Any())
{
//DO THIS
}
-------
# Date Picker

First - click into the date field to bring up the spinner:
```app.Tap("the_date_spinner_object");

Second - you'll see something like this:

```
            [DatePicker] id: "the_datePicker"
              [LinearLayout] id: "pickers"
                [NumberPicker] id: "month"
                  [NumberPicker$MyCustomEditText] id: "the_numberpicker_input" text: "Jun"
                [NumberPicker] id: "year"
                  [NumberPicker$MyCustomEditText] id: "the_numberpicker_input" text: "2017"
        [LinearLayout] id: "buttonPanel"
          [AppCompatButton] id: "cancel_button" text: "Cancel"
          [AppCompatButton] id: "ok_button" text: "OK"
```

```
//pick the Month spinner
app.Tap("the_numberpicker_input");
app.EnterText("May");
//pick the Year spinner
app.Tap(x=>x.Marked("the_numberpicker_input").Index(1));
app.EnterText("2016");
app.Tap(x=>x.Marked("ok_button"));
```


-------

TUTORIAL ON ADDING Calabash to Swift/Objective-C projects:
https://github.com/calabash/calabash-ios/wiki/Tutorial%3A-How-to-add-Calabash-to-Xcode
Calabash for iOS Github page:
https://github.com/calabash/calabash-ios

Xamarin Documentation has a more in-depth Cheat Sheet:
https://developer.xamarin.com/guides/testcloud/uitest/cheatsheet/

Guide created for TFS/VSTS with a lot of simple guides:
https://www.visualstudio.com/en-us/docs/build/steps/test/xamarin-test-cloud
-------

Thank you to JWhite, Mahdi, Brandon, June, Mike Watson, Brad, AdamB, and Ian Leatherbury
