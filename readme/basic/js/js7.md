# Step 7: JavaScript Specific

[< Prev](./js6.md) | [General Step Instructions](../step7.md) | [Next >](./js8.md)

---

[TOC]

## Summary

Step 7 is basically Step 6 with an extra detail or two. Adding works almost exactly the same way as editing, and movies work much the same way as people.

Looping through your tests will likely be your biggest difficulty.

### Simple Examples

Just about the only wrinkle here when it comes to functionality are a few elements you might not have interacted with before:
* **Date Inputs**
    * Some apps need more detail... This one should just work if you type the date without punctuation, as works in many apps.
    * `element.sendKeys('07042021')` should fill in 7/4/21.
* **Dropdowns/Selects**
    * This is easier than you'd think. Click the `option` in the `select` directly.
    * `await driver.findElement(By.xpath("//select/option[text()='some text']")).click()`
* **Scrollable Multi-Select**
    * Do like with the prior select; just send multiple clicks to all the elements you want to select!
    ```
    await driver.findElement(By.xpath("//select/option[text()='item1']")).click()
    await driver.findElement(By.xpath("//select/option[text()='item2']")).click()
    await driver.findElement(By.xpath("//select/option[text()='item3']")).click()
    ```

Google is your friend if you need some more guidance.

Defining your test data and then iterating through it might be something new for you, though similar to working with the table(s) in step 6.

1. Declare an array of your data.
2. Iterate through the array.

This is something we can show readily by using the `search` method we created for our Google testing.

#### iterating.test.js

```javascript
const { expect } = require("chai");
const { until, By } = require("selenium-webdriver");
const { driverBuilder } = require("./driverBuilder");
const { search } = require("./search");

// here is our list of test data
let tests = [
    { term: "puppies", result: "adopt" },
    { term: "NBA", result: "basketball" },
    {
        term: "Millions of Peaches",
        result: "The Presidents of the United States of America",
    },
];

describe("iterating searches", () => {
    var driver;
    before(async () => {
        driver = await driverBuilder();
    });
    // note, we need to reset our testing environment before each test (reload Google)
    beforeEach(async () => {
        await driver.get("https://www.google.com");
    });
    after(async () => {
        await driver.quit();
    });

    // we can actually loop through, automatically adding a new test for every item we add
    // to the array 'tests'
    for (const test of tests) {
        it(`a search for "${test.term}" will find "${test.result}"`, async () => {
            await search(driver, test.term);
            let results = await driver.wait(
                until.elementLocated(By.id("search"))
            );
            expect(await results.getText()).to.include(test.result);
        });
    }
});
```

<!-- ## Tutorials/Docs

-  -->