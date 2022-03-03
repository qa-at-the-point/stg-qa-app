# Step 3: C# Specific

[< Prev](./CSharp2.md) | [General Step Instructions](../step3.md) | [Next >](./CSharp4.md)

---

[TOC]

## Summary

Logging in using a function is a basic part of most automation setups; after all, it's something we need to do all the time in our applications.

The following example of adding a search function to a test should show how you might add a login function to your test file.

### Simple Example

I added a function and a new test into my test file to search Google.

#### The function:
(I put this at the bottom of my file but still within the class)

```C#
public void Search(IWebDriver driver, string searchTerm)
{
    By search = By.Name("q");

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
```

Some things to notice:

* Declaring the method "public" means you can call that method from within the current class, and a source that is outside of the current class if you ever needed to. Having a return type of "void" means you don't plan on returning anything during the method's execution. 

* Declaring "By" objects is usually better than declaring a full IWebElement. Some Selenium methods require a "By" to be passed, and if you ever have to pass an IWebElement you can construct it at that time. 

* I'll need to pass in the `driver` we use in the test so that the function knows how to interact with my browser.

* The search button on the little suggestions popout (`By.name("btnK")`) was PRESENT on the page, and could be located, even when the popout was not displayed.
    1. First I needed to locate the element.
    2. Then I could wait to click it until it was visible.
    * Trying to click on an element that isn't displayed on the page just won't work.

#### The test:

```C#
[Test]
public void TestMethod1()
{
    // declare the string you wish to use throughout the 
    // test up front so you only have to update it once
    // in the event it needs to change
    string searchTerm = "puppies";
    
    // here we're using our new function.
    Search(driver, searchTerm);
    // it will find the search bar and click search,
    // then we wait for results to appear, and verify them
    By results = By.Id("search");
    wait.Until(SeleniumExtras.WaitHelpers.ExpectedConditions.ElementIsVisible(results));

    // using the $ before a string allows you to use variables
    // within strings like this.
    Assert.That(Driver.FindElement(results).Text.Contains(searchTerm), $"The search results should contain '{searchTerm}'");
}
```

## Tutorials/Docs

- Official Docs:
    - [Keyboard](https://www.selenium.dev/documentation/en/webdriver/keyboard/)
    - [Waits](https://www.selenium.dev/documentation/en/webdriver/waits/)
    - See the C# tabs
- [C# Methods (W3Schools)](https://www.w3schools.com/cs/cs_methods.php)