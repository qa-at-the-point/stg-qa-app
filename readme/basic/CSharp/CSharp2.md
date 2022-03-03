# Step 2: C# Specific

[< Prev](./CSharp1.md) | [General Step Instructions](../step2.md) | [Next >](./CSharp3.md)

---

[TOC]

## Summary

You've been tasked to verify the home page of our new application. You've been given your story -- and it shouldn't be too hard to verify.

1. You need to navigate to the page.
   - When you are running the application locally, you can load the home page with `driver.get("http://localhost:9000")`
1. You need to locate and assert on the proper criteria.
   - You'll need to use `Bys`, AKA locators... CSS or XPath selectors, IDs, element names...
2. You may also need to know how to handle a wait.
   - You will want to use `driver.WaitFor`.


### Simple Example

To add this test to my old `visiting google` test, I had to update what I was requiring, but it shows waiting for, locating, and using an element in an assertion.

    ```C#
    using System;
    using NUnit.Framework;
    using OpenQA.Selenium;
    using OpenQA.Selenium.Support.UI;
    using OpenQA.Selenium.Chrome;

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
                driver.Navigate().GoToUrl("https://www.google.com");

                By search = By.Name("q");

                wait.Until(SeleniumExtras.WaitHelpers.ExpectedConditions.ElementIsVisible(search));

                Assert.AreEqual(Driver.FindElement(search).GetAttribute("type"), "text", "The search bar should have a type of 'text'");
            }

            [TearDown]
            public void TearDown()
            {
                driver.Quit();
            }
        }
    }
    ```

    ## Tutorials/Docs

- Official Docs:
    - [By](https://www.selenium.dev/selenium/docs/api/dotnet/html/T_OpenQA_Selenium_By.htm)
    - [WebElement](https://www.selenium.dev/selenium/docs/api/dotnet/html/T_OpenQA_Selenium_IWebElement.htm)
    - [WebDriverWait](https://www.selenium.dev/selenium/docs/api/dotnet/html/T_OpenQA_Selenium_Support_UI_WebDriverWait.htm)
- Selenium WebDriver Page:
    - [Locating elements](https://www.selenium.dev/documentation/en/webdriver/locating_elements/)
    - [Web element](https://www.selenium.dev/documentation/en/webdriver/web_element/)
    - [Waits](https://www.selenium.dev/documentation/en/webdriver/waits/)
    - See the CSharp tabs