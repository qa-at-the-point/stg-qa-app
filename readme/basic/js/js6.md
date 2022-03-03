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

### Simple Table Example

Testing against the table in W3School's [HTML Tables](https://www.w3schools.com/html/html_tables.asp) page should show roughly what I mean.

I'll start with the basic test boilerplate, in a new file, `table.test.js`

```javascript
const { expect } = require("chai");
const { until, By } = require("selenium-webdriver");
const { driverBuilder } = require("./driverBuilder");
require("chromedriver");

describe("testing tables", () => {
    var driver;
    before(async () => {
        driver = await driverBuilder();
        await driver.get("https://www.w3schools.com/html/html_tables.asp");
    });
    after(async () => {
        await driver.quit();
    });
});
```

This will load into w3 school's table page.

![](./screencaps/w3schoolstable.png)

The following example does a few things with tables; you should be able to find something to help you along your way working with the entity tables in the test application.

#### table.test.js

```javascript
const { expect } = require("chai");
const { until, By } = require("selenium-webdriver");
const { driverBuilder } = require("./driverBuilder");
require("chromedriver");

describe("testing tables", () => {
    var driver;
    before(async () => {
        driver = await driverBuilder();
        await driver.get("https://www.w3schools.com/html/html_tables.asp");
    });
    after(async () => {
        await driver.quit();
    });
    it("can check the contents of a whole table", async () => {
        let table = await driver.wait(until.elementLocated(By.id("customers")));
        let text = await table.getText();
        expect(text).to.contain("Canada");
    });
    it("can verify that a specific row is present", async () => {
        let table = await driver.wait(until.elementLocated(By.id("customers")));
        let rows = await table.findElements(By.css("tr"));
        // rows is now an array (since we used 'findElements' instead of 'findElement')

        // Note that array.find() doesn't work with async functionality,
        // and .forEach is finnicky the same way.

        // We'll loop through using for...of, which will automatically run against each value in rows,
        // passing it into the loop as "row"
        for (var row of rows) {
            let cells = await row.findElements(By.css("td"));
            if (
                cells.length > 0 &&
                (await cells[0].getText()) === "Island Trading"
            ) {
                expect(await cells[1].getText()).to.equal("Helen Bennett");
                expect(await cells[2].getText()).to.equal("UK");
                console.log("found our matching row!");
                // the break statement stops the loop from continuing on.
                break;
            }
        }
    });
    it("can find all unique countries", async () => {
        let table = await driver.wait(until.elementLocated(By.id("customers")));
        let countries = [];
        // xpath can be handy to cut to the chase. We know that "Countries" is the 3rd column of the table,
        // so let's just grab all of the 3rd cells.
        let countryCells = await table.findElements(By.xpath("//tr/td[3]"));

        // now we'll loop through what we found and add new values into the countries array
        for (var cell of countryCells) {
            let country = await cell.getText();
            if (countries.indexOf(country) === -1) countries.push(country);
        }
        // this list is up to date for the table as of 7/7/21
        let expectedCountries = [
            "Austria",
            "Canada",
            "Germany",
            "Italy",
            "Mexico",
            "UK",
        ];
        for (var expected of expectedCountries) {
            expect(countries).to.include(expected);
        }
    });
});
```

#### Some things to notice:

Don't stress if this takes you a bit longer: you are applying processes you've used before, sure, but this application is a bit different, and longer.

<!-- ## Tutorials/Docs

- [Node.js Modules (Node.js official)](https://nodejs.org/api/modules.html)
- [Understanding module.exports and exports in Node.js (Sitepoint)](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) -->
