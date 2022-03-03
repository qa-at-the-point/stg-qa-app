# Step 7: C# Specific

[< Prev](./CSharp6.md) | [General Step Instructions](../step7.md) | Next >

---

[TOC]

## Summary

Step 7 is basically Step 6 with an extra detail or two. Adding works almost exactly the same way as editing, and movies work much the same way as people.

Looping through your tests will likely be your biggest difficulty.

### Simple Examples

Just about the only wrinkle here when it comes to functionality are a few elements you might not have interacted with before:
* **Date Inputs**
    * Some apps need more detail... This one should just work if you type the date without punctuation, as works in many apps.
    * `element.SendKeys('07042021')` should fill in 7/4/21.
* **Dropdowns/Selects**
    * This is easier than you'd think. Click the `option` in the `select` directly.
    * `driver.FindElement(By.XPath("//select/option[text()='some text']")).Click()`
* **Scrollable Multi-Select**
    * Do like with the prior select; just send multiple clicks to all the elements you want to select!
    ```
    driver.FindElement(By.XPath("//select/option[text()='item1']")).Click()
    driver.FindElement(By.XPath("//select/option[text()='item2']")).Click()
    driver.FindElement(By.XPath("//select/option[text()='item3']")).Click()
    ```

Google is your friend if you need some more guidance.

Defining your test data and then iterating through it might be something new for you, though similar to working with the table(s) in step 6.

1. Declare an array of your data.
2. Iterate through the array.

This is something we can show readily by using the `search` method we created for our Google testing.

#### IteratingTest.cs

````C#
[TestFixture]
public class UnitTest1 : TestBase
{
    // in C# you can create custom objects by creating
    // a subclass like the one below. This will allow 
    // you to reference the properties in your code later
    class SearchTerm
    {
        public string term { get; set; }
        public string result { get; set; }
    }

    // now we make a list of the custom objects
    List<SearchTerm> tests = new List<SearchTerm>()
    {
        new SearchTerm(){term = "puppies", result = "adopt"},
        new SearchTerm(){term = "NBA", result = "basketball"},
        new SearchTerm(){term = "Millions of Peaches", result = "The Presidents of the United States of America"},
    };

    [Test]
    public void IteratingTest1()
    {
        // now we loop through the list and use the properties
        // set in our objects to perform the test
        foreach (SearchTerm test in tests)
        {
            Google_Page.Search(driver, test.term);

            wait.Until(SeleniumExtras.WaitHelpers.ExpectedConditions.ElementIsVisible(Google_Page.GoogleResults));
            Assert.That(driver.FindElement(Google_Page.GoogleResults).Text.Contains(test.result));
        }
    }
}
````