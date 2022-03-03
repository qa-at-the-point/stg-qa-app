# Step 6: JavaScript Specific

[< Prev](./js5.md) | [General Step Instructions](../step6.md) | [Next >](./js7.md)

---

[TOC]

## Summary

We have here a story about viewing and editing a record. We also have our acceptance criteria about all of the different places the information (original or edited) should be visible, so designing tests to meet this criteria should be pretty simple.

Coding your tests should also be fairly straightforward, given that you will be using actions you have already utilized.

-   Navigating between pages
-   Getting text from elements
-   Clearing/Setting inputs
-   Clicking buttons

Don't forget you do need to abstract shared functionality from your tests.

-   Create multiple page objects to house your functionality
-   Use functions/objects with methods to house your functionality

Arguably, verifying content in a table might seem complicated, but you can break it down:

1. Get the rows in your table
1. Find the row in question using the record's ID
    - (find the row with the correct value in the correct column)
1. Verify the other cells in that row match the values expected

I would recommend looking at XPath as a means of targetting hard to find elements in the DOM. [Here](https://www.w3schools.com/xml/xpath_intro.asp) is an XPath tutorial on W3Schools.

### Simple Table Example

Testing against the table in W3School's [HTML Tables](https://www.w3schools.com/html/html_tables.asp) page should show roughly what I mean.

I'll start with the basic test boilerplate, in a new file, `TablesTest`

```C#
    [TestFixture]
    public class TablesTest : TestBase
    {
        [Test]
        public void TablesTest1()
        {
            driver.Navigate().GoToUrl("https://www.w3schools.com/html/html_tables.asp");
        }
    }
```

This will load into w3 school's table page.

![](./screencaps/w3schoolstable.png)

The following example does a few things with tables; you should be able to find something to help you along your way working with the entity tables in the test application.

#### TableTest.cs

```C#
    [TestFixture]
    public class TablesTest : TestBase
    {
        [SetUp]
        public void SetUp()
        {
            driver.Navigate().GoToUrl("https://www.w3schools.com/html/html_tables.asp");
        }

        // verifying the contents of an entire table
        [Test]
        public void EntireTableVerification()
        {
            wait.Until(SeleniumExtras.WaitHelpers.ExpectedConditions.ElementIsVisible(By.Id("customers")));
            string text = driver.FindElement(By.Id("customers")).Text;
            Assert.That(text.Contains("Canada"));
        }

        // verifying a specific row exists
        [Test]
        public void SpecificRowVerification()
        {
            wait.Until(SeleniumExtras.WaitHelpers.ExpectedConditions.ElementIsVisible(By.Id("customers")));
            IWebElement table = driver.FindElement(By.Id("customers"));
            // if you don't know the difference between a list and an array
            // please look it up. Lists are great.
            IList<IWebElement> rows = table.FindElements(By.CssSelector("tr"));

            // now we loop through each row and validate the data shown
            foreach (IWebElement row in rows)
            {
                IList<IWebElement> cells = row.FindElements(By.CssSelector("td"));
                if (cells.Count > 0 && cells[0].Text == "Island Trading")
                {
                    Assert.That(cells[1].Text.Equals("Helen Bennett"));
                    Assert.That(cells[2].Text.Equals("UK"));
                    Console.WriteLine("Found our matching row!");
                    // now we break out of our for loop
                    break;
                }
            }
        }

        // finding unique countries
        [Test]
        public void FindUniqueCountries()
        {
            wait.Until(SeleniumExtras.WaitHelpers.ExpectedConditions.ElementIsVisible(By.Id("customers")));
            IWebElement table = driver.FindElement(By.Id("customers"));
            List<string> countries = new List<string>();
            // here we are using xpath to be explicit in our selector
            // we are grabbing every 3rd cell in every row that exists
            // in the table and adding it to the list
            IList<IWebElement> countryCells = table.FindElements(By.XPath("//tr/td[3]"));

            // now we'll loop through what we found and add new values into the countries List
            foreach (IWebElement cell in countryCells)
            {
                string country = cell.Text;
                if (countries.IndexOf(country) == -1)
                {
                    countries.Add(country);
                }
            }

            // this list is up to date for the table as of 7/7/21
            List<string> expectedCountries = new List<string>()
            {
                "Austria",
                "Canada",
                "Germany",
                "Italy",
                "Mexico",
                "UK",
            };

            foreach (string expected in expectedCountries)
            {
                Assert.That(countries.Contains(expected));
            }
        }
    }
```

#### Some things to notice:

Don't stress if this takes you a bit longer: you are applying processes you've used before, sure, but this application is a bit different, and longer.
