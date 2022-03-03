# Step 2: JavaScript Specific

[< Prev](./js1.md) | [General Step Instructions](../step2.md) | [Next >](./js3.md)

---

[TOC]

## Summary

You've been tasked to verify the home page of our new application. You've been given your story -- and it shouldn't be too hard to verify.

1. You need to navigate to the page.
   - When you are running the application locally, you can load the home page with `driver.get("http://localhost:9000")`
1. You need to locate and assert on the proper criteria.
   - You'll need to use `Bys`, AKA locators... CSS or XPath selectors, IDs, element names...
   - Check out the [Chai API docs](https://www.chaijs.com/api/) for different things you can `expect()` or `assert()` to be true. Or false.
1. You may also need to know how to handle a wait.
   - You will want to use `driver.wait`, and then `until`, a separate utility.

> Note: Depending on your connection/hardware, you might run into Mocha's default timeout killing your tests before they are done. Try using the `--timeout` flag when you execute your test, followed by the number of milliseconds to allow a test to take.
>
>* i.e. `mocha --timeout 15000 automation/firstTest.test.js`

### Simple Example

To add this test to my old `visiting google` test, I had to update what I was requiring, but it shows waiting for, locating, and using an element in an assertion.

```javascript
const { expect } = require('chai');
// note the added 'until', and 'By'
const { Builder, until, By } = require('selenium-webdriver');
require('chromedriver');

describe('visiting google', () => {
  var driver;
  before(async () => {
    driver = await new Builder().forBrowser('chrome').build();
    await driver.get('https://www.google.com');
  });
  after(async () => {
    await driver.quit();
  });
  it("shows 'Google' as the page title", async () => {
    expect(await driver.getTitle()).to.equal('Google');
  });
  it('waits for the search bar to show up', async () => {
    // if you're waiting on an element to be located/visible, etc,
    // that element is returned by the wait
    let search = driver.wait(until.elementLocated(By.name('q')));
    // knowing what you can do with an element when you've found it can be very
    // useful -- though I rarely *actually* get the tag from it.
    expect(await search.getTagName()).to.equal('input', "The search bar should be an 'input'");
  });
});
```

## Tutorials/Docs

- Official Docs:
    - [By](https://www.selenium.dev/selenium/docs/api/javascript/module/selenium-webdriver/index_exports_By.html)
    - [WebElement](https://www.selenium.dev/selenium/docs/api/javascript/module/selenium-webdriver/index_exports_WebElement.html)
    - [until](https://www.selenium.dev/selenium/docs/api/javascript/module/selenium-webdriver/lib/until.html)
- Selenium WebDriver Page:
    - [Locating elements](https://www.selenium.dev/documentation/en/webdriver/locating_elements/)
    - [Web element](https://www.selenium.dev/documentation/en/webdriver/web_element/)
    - [Waits](https://www.selenium.dev/documentation/en/webdriver/waits/)
    - See the JavaScript tabs
    

