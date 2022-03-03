# Step 4: C# Specific

[< Prev](./CSharp3.md) | [General Step Instructions](../step4.md) | [Next >](./CSharp5.md)

---

[TOC]

## Summary

Referencing code from an external source in C# is quite simple. Remeber the "Namespaces" that we talked about in step 1? All you need to do to reference code in another class is place a "using" stagement at the beginning of your file with the namespace of that class after it. This topic also exposes the difference between a 'static' and an 'instanced' class. Static variables or methods can only exist once, you cannot create multiple instances. Non-static variables or methods can be "instantiated" and multiple instances can exist. 

For example, lets say you have a class called "Bear". In the world more than one bear can exist at a given time. So in our code, if we were to make this class and associated variables non-static, we could create multiple instances of a bear. The reason we may want to create multiple of the same class in this case is to set the "Name" variable for one bear to "Baloo" and the other to "Smoky". Both are bears and both have "Name" properties but we are able to create separate "instances" of the same class (or object). Now lets say we created a 2nd class in a separate file named "Feed". Within the "Feed" class we have an "Eat" method that accepts 2 arguments; an animal object and the type of food the animal will be eating (as a string). The "Feed" class applies to more than just a bear, does not need to exist more than once and does not need to maintain instanced variables. It simply needs information passed in, and performs a simple task. In this case we could set the "Feed" class and "Eat" method as "static" since it performs a simple, repeatable action. This will make more sense by the end of this lesson.

### Simple Example

In this example, I barely had to edit the tests in my test file at all. I just moved the search function to a separate file and included the "using" statement with the new file's namespace.

#### `Utilities.cs`

1. First, create a new file at the same level as your current test file. I would recommend calling it your "Utilities" file or something similar.
    * Right click your project in the project explorer -> Add -> New Item -> Class
2. Then make sure you name the new file's namespace and class something you will remember. You will also have to add "public" before "class" in the class declaration to make it publicly accessible.
3. Now, cut and paste the function into your new class. _Make this method static._
4. Check the function to see if you'll need to import anything in this separate file.
    * There will be "red squigglies" under object that have not been added yet. If you right click these keywords that are red underlined, there is a "Quick Actions and Refactorings..." option. Select this option and it will give you the option to automatically add the using statements into your file. You'll need selenium files and NUnit for the assert.
    * You will probably need to create a new "wait" variable in this class. Place the "WebDriverWait wait = new WebDriverWait(driver, TimeSpan.FromSeconds(10));" line into the beginning of your method.
    * You will not need NUnit tags in this class since you will simply be using the methods as tools within your tests. 

    ```C#
    using OpenQA.Selenium;
    using OpenQA.Selenium.Support.UI;
    using System;

    namespace Utilities
    {
        public class SeleniumUtilities
        {
            
            public static void Search(IWebDriver driver, string searchTerm)
            {
                By search = By.Name("q");
                WebDriverWait wait = new WebDriverWait(driver, TimeSpan.FromSeconds(10));
                
                driver.Navigate().GoToUrl("https://www.google.com");

                driver.FindElement(search).SendKeys(searchTerm);

                // The button you see on login is hidden when you start typing, and
                // a new search button then appears. We need to find that one.
                // first, set the By locator to the 'searchButton' variable...
                By searchButton = By.Name("btnK");

                // now, wait for it to show up, then click.
                // (note: I prefer to create By variables and instantiate the
                // IWebElement when I need it using driver.FindElement())
                wait.Until(SeleniumExtras.WaitHelpers.ExpectedConditions.ElementIsVisible(searchButton));
                driver.FindElement(searchButton).Click();
            }
        }
    }
    ```

#### Calling External Search Method

If the namespace you set in your new file is "Utilities", then in your test file add "using Utilities" to your list of using statements. Then call the method using the following format: ClassName.MethodName(arguments);

    ````C#
    using System;
    using NUnit.Framework;
    using OpenQA.Selenium;
    using OpenQA.Selenium.Support.UI;
    using OpenQA.Selenium.Chrome;
    // here we are granting this file access to the new class
    using Utilities;

    namespace UnitTestProject1
    {
        [TestFixture]
        public class UnitTest1
        {
            IWebDriver driver;
            WebDriverWait wait;
            
            [SetUp]
            public void SetUp()
            {
                driver = new ChromeDriver();
                wait = new WebDriverWait(driver, TimeSpan.FromSeconds(10));
            }

            [Test]
            public void TestMethod1()
            {
                // declare the string you wish to use throughout the 
                // test up front so you only have to update it once
                // in the event it needs to change
                string searchTerm = "puppies";
                
                // here we're using our new function, placing the
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

            [TearDown]
            public void TearDown()
            {
                driver.Quit();
            }
        }
    }
    ````

## Tutorials/Docs

- [Static vs Non-Static](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members)