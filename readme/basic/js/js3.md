# Step 3: JavaScript Specific

[< Prev](./js2.md) | [General Step Instructions](../step3.md) | [Next >](./js4.md)

---

[TOC]

## Summary

Logging in using a function is a basic part of most automation setups; after all, it's something we need to do all the time in our applications.

The following example of adding a search function to a test should show how you might add a login function to your test file.

### Simple Example

I added a function and a new test into my `firstTest.test.js` file to search Google.

#### The function:
(I put this at the bottom of my file)

```javascript
// async function search(driver, searchTerm) {
// search = async function(driver, searchTerm){
const search = async (driver, searchTerm) => {
    let search = await driver.wait(until.elementLocated(By.name("q")));
    await search.sendKeys(searchTerm);

    // The button you see on login is hidden when you start typing, and
    // a new search button then appears. We need to find that one.
    // first, locate the element...
    let popoutSearchButton = await driver.wait(
        until.elementLocated(By.name("btnK"))
    );
    // now, wait for it to show up, then click.
    // (note: until.elementIsVisible needs an element, not a By)
    await driver.wait(until.elementIsVisible(popoutSearchButton)).click();
};
```

Some things to notice:

* You can declare functions a few different ways in javascript. I like the "fat arrow" syntax for most things. `()=>{}`. It feels like less typingto me.

* I made the function `async` so that I can:
    1. `await` the driver to find elements etc.
    2. Have my test `await` the search function.

* I'll need to pass in the `driver` we use in the test so that the function knows how to interact with my browser.

* The search button on the little suggestions popout (`By.name("btnK")`) was PRESENT on the page, and could be located, even when the popout was not displayed.
    1. First I needed to locate the element.
    2. Then I could wait to click it until it was visible.
    * Trying to click on an element that isn't displayed on the page just won't work.

#### The test: 
(This was added after the `it("waits for the search bar to show up")` test.)

```javascript
it("can do a search", async () => {
    // here we're using our new function.
    await search(driver, "puppies");
    // it will find the search bar and click search,
    // then we wait for results to appear, and verify them
    let results = await driver.wait(until.elementLocated(By.id("search")));
    expect(await results.getText()).to.include("puppies");
});
```

* I `await`ed the search function to do the search.
* Waiting until the search results element was located was all I needed to do to handle Google popping open a new page.
    * WebDriver doesn't care that the page changed - it will just keep looking for the element I asked it to wait for.

## Tutorials/Docs

- Official Docs:
    - [Keyboard](https://www.selenium.dev/documentation/en/webdriver/keyboard/)
    - [Waits](https://www.selenium.dev/documentation/en/webdriver/waits/)
    - See the JavaScript tabs
- [JavaScript Functions (W3Schools)](https://www.w3schools.com/js/js_functions.asp)
- [Functions (javascript.info)](https://javascript.info/function-basics)