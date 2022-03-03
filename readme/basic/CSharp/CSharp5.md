# Step 5: C# Specific

[< Prev](./CSharp4.md) | [General Step Instructions](../step5.md) | [Next >](./CSharp6.md)

---

[TOC]

## Summary

Organizing your code into page objects, or just abstracting a method out to a different file is not going to be *too* different from the coding we've done so far.

### Abstracting Driver Creation

A good practice for page object model in C# is to create a top level file known as your "Test Base". You can then "inherit" from the test base in each of your test classes (aka your test fixtures). This allows you to establish set up and tear down methods that apply to all tests easily. 

#### TestBase.cs

Create this new file at the same level as your project file:
````C#
using NUnit.Framework;
using OpenQA.Selenium;
using OpenQA.Selenium.Chrome;
using OpenQA.Selenium.Support.UI;
using System;

namespace UnitTestProject1
{
    public class TestBase
    {
        public IWebDriver driver;
        public WebDriverWait wait;

        [SetUp]
        public void DriverSetup()
        {
            driver = new ChromeDriver();
            wait = new WebDriverWait(driver, TimeSpan.FromSeconds(10));
        }

        [TearDown]
        public void DriverTearDown()
        {
            if (driver != null)
            {
                driver.Quit();
            }
        }
    }
}
````

1. Because the `DriverSetup` and `DriverTearDown` methods are tagged as "SetUp" and "TearDown" methods, these will be performed before (setup) and after (teardown) _EACH_ test. This makes it easy since you know that every time each test executes you are starting with a brand new browser and a brand new session. Meaning you would need to navigate to the page and log in to the application in each test. If you want the browser to stay open and you are willing to keep track of the state of the browser between tests, you can make these "OneTimeSetUp" and "OneTimeTearDown" methods which will cause them to run once before and once after ALL tests. 
2. Then you will need to change your test file's class declaration to inherit from your test base. To do this you will place a colon after your class name, and then put your test base class name. 
   1. example: `public class UnitTest1 : TestBase`
   2. Make sure both the test base and the test classes are in the same namespace.
   3. This grants access to all public variables that exist in the TestBase class to the UnitTest1 class.
3. You can then remove the driver and wait variable declarations and your test specific set up and tear down methods since you are already performing these tasks in your test base. Every new test that is added can then inherit from the test base and their `driver` and `wait` variables will already exist.

#### UnitTest1.cs

Your test file should now look like this:

    ````C#
    using System;
    using NUnit.Framework;
    using OpenQA.Selenium;
    using OpenQA.Selenium.Support.UI;
    using OpenQA.Selenium.Chrome;
    using Utilities;

    namespace UnitTestProject1
    {
        [TestFixture]
        public class UnitTest1 : TestBase
        {
            [Test]
            public void TestMethod1()
            {
                // declare the string you wish to use throughout the 
                // test up front so you only have to update it once
                // in the event it needs to change
                string searchTerm = "puppies";
                
                // here we are using our new function, placing the
                // class name first, then calling the method off of it
                // it will find the search bar and click search
                SeleniumUtilities.Search(driver, searchTerm);

                // then we wait for results to appear, and verify them
                By results = By.Id("search");
                wait.Until(SeleniumExtras.WaitHelpers.ExpectedConditions.ElementIsVisible(results));

                // using the $ before a string allows you to use variables
                // within strings like this.
                Assert.That(Driver.FindElement(results).Text.Contains(searchTerm), $"The search results should contain '{searchTerm}'");
            }
        }
    }
    ````

### Creating your first page object

Creating your first page object is very similar to how you created a separate file for your login method and included it in your test. In my example I will be making a "Google" page object. Page objects include a list of the elements, as well as methods that perform basic, repeatable functionality that is availalbe on the given page. My page object will be replacing my utilites file we spoke of earlier. Utility files should apply to functionality that is applicable to all tests. Page object variables and methods should only pertain to the given page. 

#### GooglePageObject.cs

I would recommend placing all of your page object in a folder or something that will group them together. Here is my example of the Google page object:
````C#
using OpenQA.Selenium;
using OpenQA.Selenium.Support.UI;
using System;

// i created a separate namespace for page objects
namespace PageObjects
{
    public class Google_Page
    {
        public static By GoogleSearchInput = By.Name("q");
        public static By GoogleSearchButton = By.Name("btnK");

        public static void Search(IWebDriver driver, string searchTerm)
        {
            WebDriverWait wait = new WebDriverWait(driver, TimeSpan.FromSeconds(10));

            driver.FindElement(GoogleSearchInput).SendKeys(searchTerm);

            wait.Until(SeleniumExtras.WaitHelpers.ExpectedConditions.ElementIsVisible(GoogleSearchButton));
            driver.FindElement(GoogleSearchButton).Click();
        }
    }
}
````
1. The class should be public.
2. Start by listing out the elements (as `By` objects) first so that you only have to declare these elements a single time. They are static variables so you can reference the variables as needed in your tests. _You should never declare an element inside your test!_ All elements should belong to a page object. (This is where you will declare your 'username' and 'password' elements for your login page.)
3. After the elements, you can then create methods that perform basic functionality specific to this page. In this case we have a "Search" method. (This is where you will place your 'login' method that should use the element variables declared.)



### Using your page object

Your test file should now look something like this:
````C#
    using System;
    using NUnit.Framework;
    // here we are referencing the page object namespace
    using PageObjects;

    namespace UnitTestProject1
    {
        [TestFixture]
        public class UnitTest1 : TestBase
        {
            [Test]
            public void TestMethod1()
            {
                string searchTerm = "puppies";

                // here we are referencing the page object method
                Google_Page.Search(driver, searchTerm);

                // here we are referencing the page object element
                // by using Google_Page.GoogleResults
                wait.Until(SeleniumExtras.WaitHelpers.ExpectedConditions.ElementIsVisible(Google_Page.GoogleResults));

                // here again we are referencing a page object element
                Assert.That(driver.FindElement(Google_Page.GoogleResults).Text.Contains(searchTerm), $"The search results should contain '{searchTerm}'");
            }
        }
    }
````

#### Some things to remember

1. Because I made my page object variable and methods 'static', I can just reference them directly in a static manner wihtout creating an instance of the class. If you wanted to create instances of your page objects in your tests you could totally do that by removing the static keyword and adding a constructor to your page object class. You would then need to create a variable in your test file that creates an instance of your page object class.
2. Remember: the purpose of page object model is to declare each element a single time. If you find yourself creating a page element multiple times you are doing something wrong. Create the elements and methods in your page object and reference them everywhere else. 
3. If there are red underlined variables, use the "Quick Actions and Refactorings..." menu.


## Tutorials/Docs

- [Static vs Non-Static](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members)