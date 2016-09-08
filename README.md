# XamarinTestCloudReference

<ul>Common repl commands:
<li>tree</li>
<li>app.Flash(“myButton”);</li>
<li>app.Flash(x=>x.All(“*”));</li>
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
</ul>
<ul>
Common Queries:
<li>app.Query("UITextFieldLabel");
<li>app.Query(x => x.All("*"));
<li>app.Query(x => x.All("*").Class("UITextFieldLabel"));
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
<li>Assert.IsTrue(app.Query(q => q.Marked("logoutButton”)).Any());
<li>Assert.IsFalse(app.Query(q => q.Marked(“logoutButton")).Any());
<li>app.WaitForElement(q => q.Marked("logoutButton"));
</ul>
<ul>
System C# + UITest:
<li>var joinedUsername = string.Format (“myemail_{0}@microsoft.com", deviceNumber);
<li>var joinedUsername = $”myemail_{deviceNumber}@microsoft.com”;
</ul>
<ul>
Sleep/Wait:
<li>Thread.Sleep (3000); //this would be 3 seconds
<li>Thread.Sleep (TimeSpan.FromMinutes (4));
<li>app.WaitForElement (x => x.Text (“Community Terms of Use"));
</ul>
<ul>
Device Numbers:
<li>var deviceNumber = Environment.GetEnvironmentVariable ("XTC_DEVICE_INDEX");
</ul>

App Configuration:
//On iOS - Simulator
return ConfigureApp
.iOS
.AppBundle ("../../../iOS/bin/iPhoneSimulator/Debug/XamarinForms.iOS.app")
.DeviceIdentifier (“KJ23d-45648-55D3E-WEF784F0”) // Your simulator device ID
.AppBundle("/Users/USERNAME/Projects/MyFavorite.app")

//On iOS - Device
return ConfigureApp
.iOS
.DeviceIdentifier (“e2342asdfa8asdofhiaesd932h3")
.DeviceIp ("10.0.9.33")
.InstalledApp (“com.myfavoriteapp")
.StartApp();

//On Android
return ConfigureApp
.Android
.ApkFile("com.myfavoriteapp.apk”) // example implies file is in SolutionFolder > bin > Debug
.StartApp ();

<ol>
Setup Issues:
<li>SetUp : System.Exception : Unable to start CalabashHostStrategyProxy
- Close down your Terminal/Repl then try running the test again</li>
<li> Unable to Instrument app:
- iOS - make sure to add the Calabash Test Server to your app - and make start it in your app delegate</li>
</ol>

Command Line:<br/>
Windows:<br/>
packages\Xamarin.UITest.[version]\tools\test-cloud.exe submit yourAppFile.apk thePRIVATENotRealAPINumber00071 --devices 4b1b0c03 --series "master" --locale "en_US" --app-name "SimpleUITestApp" --user myemail@xamarin.com --assembly-dir pathToTestDllFolder

OS X:<br/>
mono packages/Xamarin.UITest.[version]/tools/test-cloud.exe submit yourAppFile.apk thePRIVATENotRealAPINumber00071 --devices 4b1b0c03 --series "master" --locale "en_US" --app-name "SimpleUITestApp" --user myemail@xamarin.com --assembly-dir pathToTestDllFolder

Run the command from the directory that contains the NuGet packages directory. Also, make sure you update your app name and the directory of tests. If your app file is not in the same directory as the NuGet packages, please include a direct path to the file.

Categories:
--category "all"


<ul>
Cross Platform Properties you can Access:
Properties you can access:
Android/iOS -> “id"
Android -> “contentDescription"
iOS -> “accessibilityLabel” or "accessibilityIdentifier"
</ul>


Setting “AutomationID" Xamarin.Forms in iOS & Android assign the contentDescription and accessibilityIdentifier
XAML:
 `< Button x:Name="b" AutomationId="MyButton" Text="Click me" /> ` 

C#:
    `< var l = new Label { `
        `Text = "Hello, Xamarin.Forms!",`
        `AutomationId = "MyLabel"`
    `};`

Then in your test: `app.Query(x=>x.Marked(“theGoodWord”));`
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

Xamarin Documentation has a more in-depth Cheat Sheet:
https://developer.xamarin.com/guides/testcloud/uitest/cheatsheet/

-------

Thank you to Jwhite, Mahdi, Brandon, June, Mike Watson, Brad, and Ian Leatherbury
