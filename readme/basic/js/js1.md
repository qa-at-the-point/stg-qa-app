# Step 1: JavaScript Specific

< Prev | [General Step Instructions](../step1.md) | [Next >](./js2.md)

---

[TOC]

## Summary

Setting up for WebDriver automation with JavaScript isn't too hard. There are some super detailed step by step instructions to follow here (and they won't get quite this detailed again), but I'll add some links to documentation/tutorials if you want to try a different path.

- **Environment**: `NodeJS`
- **Test Runner**: `Mocha`
- **Assertion Library**: `Chai`

## Environment Setup

1. Install NodeJS
   - This had to be done already to launch the QA app; hopefully you've already done that.
   - Download [here](https://nodejs.org/en/download/)
   - Verify install was successful by executing this command in your terminal/command line/bash:
     - `npm -version`
     - You should get back something like `6.14.12`
1. Install Mocha
   - From the project's base directory, run the following command:
     - `npm i --save-dev mocha`
       - This installs mocha as a project dependency
     - `npm i -g mocha` will install Mocha globally, letting you use Mocha more easily from the command line, and in any other project on your machine.
1. Install Chai
   - From the project directory, in your terminal run:
     - `npm i --save-dev chai`
1. Install WebDriver
   - Still at the base directory, run the following command:
     - `npm i --save-dev selenium-webdriver`
1. Install Browser Specific Drivers
   - Once again in the base directory:
     - `npm i --save-dev chromedriver`
       or
     - `npm i --save-dev geckodriver`
   - You _can_ install these globally and make sure your global node_modules are on your Path. I'll just require `chromedriver` manually, as you'll see.

> **Note:** This project is already initialized for Node. When starting from scratch, go to your project's base folder and execute the following command to set up with default node configuration (a `package.json` and the ability to install dependencies).
>
> - `npm init -y`
>
> There is also already a `.gitignore` file to ignore the `/node_modules/` folder with all of your dependencies. In a brand new project, this probably would not exist.

## Your First Test

- Now it's time to make sure your setup went correctly.
- I recommend using [VS Code](https://code.visualstudio.com/download) for your JS automation, but you can use your IDE of choice.

1.  Add a test file to your automation directory. I called mine `firstTest.test.js`.
    - The `.test` portion of the name isn't required, it could've been `firstTest.js`, but this makes it easier for me to have config/support/model files in the same directory as my tests without breaking the execution.
2.  We use `describe` blocks to organize our tests. They can be nested. As I'm going to hit Google first, we'll describe that.
    ```javascript
    describe('visiting google', () => {
      // your test will go here
    });
    ```
3.  We use `it` blocks for the individual tests. This way the output will order:
    ```
    1. Thing you described
        1. It does x
        1. It does y
        1. It does z
    1. The other thing you described...etc.
    ```
    So in our test, we'll add that `it` block.
    ```javascript
    describe('visiting google', () => {
      it("shows 'Google' as the page title", () => {
        // the meat of the test goes here
      });
    });
    ```
    - With this you might still get some other chromedriver debugging messages, but otherwise if it works, when executed in your terminal, you'll get something like
    ```
        * visiting google
            * shows 'Google' as the page title
    ```
4.  Now it's time to actually set up and use the webdriver. First we need our `driver` (or `browser`, those are generally the two standard names)

    - We'll need to bring in `chromedriver` and `Builder` for this setup.
    - If you're using a nice IDE, it will give tooltips as you type, recommending imports, and when you hit TAB will autocomplete/autoimport!

      ```javascript
      const { Builder } = require('selenium-webdriver');
      require('chromedriver');

      describe('visiting google', () => {
        it("shows 'Google' as the page title", async () => {
          const driver = await new Builder().forBrowser('chrome').build();
          // this doesn't do anything yet, but now we have the harness...
        });
      });
      ```

    - **Important**: Notice the `async` callout on the `it` function, and that we `await` the new Builder()... You can use promise chains if you want. I find the syntax of async await is usually easier to pick up.
    - If you _don't_ use something like this, your test WILL NOT WORK. Not handling asynchronous code as cleanly as other languages is often considered a weakness of JavaScript.

5.  With that, we have our "test harness" at it's most basic level. We can drive our browser. Now we need to do something with it. We'll get our page, and make sure the driver closes when the test is done.
    ```javascript
    require('chromedriver');

         describe('visiting google', () => {
             it("shows 'Google' as the page title", async () => {
             const driver = await new Builder().forBrowser('chrome').build();
             await driver.get('https://www.google.com');
             await driver.quit();
             });
         });
         ```

    - This works to open, navigate, and close our browser, and we _could_ run it. There are, however, no assertions to make sure it _does_ work.

6.  We'll `expect` the outcome we're looking for using a `Chai` expect.
    ```javascript
    const { expect } = require('chai');
    const { Builder } = require('selenium-webdriver');
    require('chromedriver');

         describe('visiting google', () => {
             it("shows 'Google' as the page title", async () => {
             const driver = await new Builder().forBrowser('chrome').build();
             await driver.get('https://www.google.com');
             expect(await driver.getTitle()).to.equal('Google');
             await driver.quit();
             });
         });
         ```

    - Now, if anything shows up in the title except "Google", our test will fail!

7.  Execute your test with the `mocha` command and the path to your test file:

    - `mocha automation/firstTest.test.js`
    - You should get output something like...

      ```
      $ mocha automation/firstTest.test.js

      visiting google
          √ Has 'Google' as the page title (1068ms)

      1 passing (1s)
      ```

8.  Now a last bit of cleanup. We'll use the Mocha 'hooks' `before()` and `after()` to restructure our code a bit. This will allow us to add more tests to one file without setting things up late or tearing them down early.

    - We'll put the browser setup and page navigation in the `before` block.
    - The driver shut down will go in the `after` block, which runs after all tests in its `describe`.
    - `beforeEach()` and `afterEach()` will run before or after EACH test in their scope, which can be handy too.

    ```javascript
    const { expect } = require('chai');
    const { Builder } = require('selenium-webdriver');
    require('chromedriver');

    describe('visiting google', () => {
      // we keep the driver in the scope of our base describe, or even outside of it,
      // so once it's defined in the before, it's available everywhere.
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
    });
    ```

Congrats! You now have a solid foundation to build from!

## Tutorials/Docs

- [Official Docs: selenium-webdriver](https://www.selenium.dev/selenium/docs/api/javascript/index.html)
- [Mocha Docs](https://mochajs.org/#table-of-contents)
- [Chai Docs](https://www.chaijs.com/)
- [TAU: Introduction to Mocha](https://testautomationu.applitools.com/mocha-javascript-tests/)
- [JavaScript Selenium Mocha QuickStart](https://dev.to/stephencavender/javascript-selenium-mocha-quickstart-guide-5a5k)
- [Jest Tutorial For Selenium JavaScript Testing With Examples](https://www.lambdatest.com/blog/jest-tutorial-for-selenium-javascript-testing-with-examples/)
- [The Best Unit Testing Frameworks for NodeJS](https://blog.logrocket.com/the-best-unit-testing-frameworks-for-node-js/)
