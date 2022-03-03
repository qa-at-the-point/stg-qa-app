# Step 2 - Story: Home Page

[<Prev](./step1.md) | [Main](../../README.md) | [Next>](./step3.md)

---

[TOC]

## Story

-   As a user I should see a "welcome" splash page upon navigating to the app, with the banner "Welcome, QA Engineers!" along with a navigation/utility bar at the top of the page.

### Acceptance Criteria

-   Can navigate to the home page.
-   The home page has a banner, "Welcome, QA Engineers!"
-   There is a navigation/utility bar at the top of the page.

### Technical Acceptance Criteria

-   This should be a brand new test file.

## General Instructions

We'll be hooking into the app itself here, and validating the home page.

1. Use the basic framework you have set up to navigate to the home page.

    - (see the [README.md](../../../README.md) for instructions on setup/launching the app)

1. Locate the right elements and use one or more assertions to verify the requirements are met.
1. You may need to "wait" for the page to load fully before making your assertions.

## Keep In Mind

> **Planning Automated Tests:**
>
> -   How would you test the application manually?
>
> This is the question to ask yourself as you're automating the tests. It often means writing more tests; but we're coding our tests so that they will run faster and whenever we want.
>
> Don't forget - even on a 'happy path', there are decisions our users can make, even just clicking the submit button, or hitting the enter key. Do what you can to cover those scenarios.

> **Proof of Competence:**
>
> Real tests are much more effective in building and showing proficiency than just showing you can iterate through a list, or interact with a page. This certification isn't to make your Account Manager happy with your skills. It's to prove to TWO people that you have what it takes as a QA Automation Engineer.
>
> 1. You
> 2. The Client
>
> Treat this project professionally, keeping your code clean, and realistic, and at the end of the cert you'll have code you can be confident showing off, and you'll know that you can go back and do the same thing on your next project.

## Language/Framework Specific Instructions

-   [JavaScript](./js/js2.md)
-   [Python](./python/p2.md)
-   [C#](./CSharp/CSharp2.md)
-   [Cypress.io](./cypress/cy2.md)

## General Links

-   Selenium WebDriver Page:
    -   [Locating elements](https://www.selenium.dev/documentation/en/webdriver/locating_elements/)
    -   [Web element](https://www.selenium.dev/documentation/en/webdriver/web_element/)
    -   [Waits](https://www.selenium.dev/documentation/en/webdriver/waits/)
-   [10 Gotchas for Automation Code Reviews](https://automationpanda.com/2017/05/08/10-gotchas-for-automation-code-reviews/)
    -   Basically a broad guide to maintaining clean automation
    -   Automation Panda is AWESOME. Pandy knows his stuff.
-   Good Locator Links
    -   [Xpath Diner](https://topswagcode.com/xpath/)
    -   [Xpath cheatsheet](http://devhints.io/xpath)
    -   [CSS cheatsheet](http://devhints.io/css)
-   [Difference between Selenium visibility methods](https://developers.perfectomobile.com/display/TT/Difference+between+Selenium+visibility+methods)
    -   Note: The code fragments are NOT language agnostic.
