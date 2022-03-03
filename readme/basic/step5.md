# Step 5 - Task: Page Objects and other Models

[<Prev](./step4.md) | [Main](../../README.md) | [Next>](./step6.md)

---

[TOC]

## Task

Get smart with your test organization - break your functionality out into shared methods/objects, like Page Objects, where you only need to write the code once and you can re-use it in multiple tests. - Start with functionality to: - Navigation - Logging In - You can also include the locators you need on each page.
Also abstract to a separate class/module the code needed to generate your webdriver.

### Technical Acceptance Criteria

-   Your code has been refactored/reorganized using Page Objects or a similar organizational model.
    -   You have functionality either as standalone (but organized) functions, or as a method on a page object that allows you to:
        -   Navigate
        -   Log In
    -   It is strongly recommended you create your own custom Page Objects rather than utilizing Selenium's Page Object Factory.
-   You are no longer building your `driver`, `browser`, or whatever you name your Webdriver instance, inside of your test file(s).
-   Your existing tests are all still executable.

## General Instructions

Love it, or hate it, the single most popular model when it comes to UI automation is the Page Object. Selenium's built in Page Object support usually isn't very performant. It's recommended that you define your own page object class or classes.

You CAN use a different model, or no model at all.

1. Abstract out the code to create your webdriver object.
1. Update your tests, and verify they still work.
1. Determine what functionality you need on your page object(s) or in file(s) of shared methods - only having one page object or external file is acceptable, though as you further expand your automation in later steps you might find more than one to be easier to keep organized.
    - You can leverage inheritance and create a base page object your other page objects will extend.
        - This can make waiting for page loads, typing into elements, etc, simpler.
        - A base page object won't usually have any page specific functionality.
    - Your page specific page object(s) need to include logging in and navigating the navbar.
1. Update your tests with your page object(s) and make sure they still work.

## Keep In Mind

> **Page Object Model: A tool, not a rule**
>
> Using something like POM (the Page Object Model) is intended to make your testing:
>
> -   Less messy
> -   More extendable
> -   Easier to maintain
>
> Saving time/hassle and making things easier is the whole purpose of test automation anyway. If you find that using the POM is more hassle than it's worth, you're either doing it wrong, or your project is probably pretty darn small. You could argue that our project here is too small to make the POM worth using -- and there's an argument to be made for that. However, this is such a commonly used practice in the industry, we want to see you use the model, or at least something similar so that our clients know you have the skills.

> **Sharing Functionality**
>
> Whether or not you use this chance ot explore a page object or just pull some of your functionality out, do your best to recognize when code will be used more than once AND is complicated enough to make abstraction worthwhile.
>
> **Generating the driver** is a great example of something you'll do multiple times, and might be handy to have abstracted out. This way, you have one spot to handle deciding what browser to use, settings, etc.
>
> **Verifying link destinations** is an example of something you'll also do more than once -- but the built in functionality is probably simple enough that a function will _usually_ be overkill.

## Language/Framework Specific Instructions

-   [JavaScript](./js/js5.md)
-   [Python](./python/p5.md)
-   [C#](./CSharp/CSharp5.md)
-   [Cypress.io](./cypress/cy5.md)

## General Links

-   Selenium WebDriver Page
    -   [Page object models](https://www.selenium.dev/documentation/en/guidelines_and_recommendations/page_object_models/)
-   [Page Object Model (POM) Design Pattern](https://medium.com/tech-tajawal/page-object-model-pom-design-pattern-f9588630800b)
    -   A pretty good Medium blog post
-   [UI Automation - Page Object Model and other Design Patterns](https://techcommunity.microsoft.com/t5/testingspot-blog/ui-automation-page-object-model-and-other-design-patterns/ba-p/992242)
    -   Blog post by the Microsoft Testing Team
    -   You'll find that these are mostly different flavors of the POM
-   [Stop using Page Objects](https://www.cypress.io/blog/2019/01/03/stop-using-page-objects-and-start-using-app-actions/)
    -   A pretty good argument for efficiency from the mind behind Cypress.io
    -   Also a pretty good overview of POM and its benefits.
