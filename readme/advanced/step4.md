# Step 4 - Task: Cross Environment Testing

[<Prev](./step3.md) | [Main](../../README.md) | [Next>](./step5.md)

---

[TOC]

## Task

User bases vary widely. We need our tests to cover more than one browser. Even better if they cover a range of browsers and resolutions.

### Technical Acceptance Criteria

-   Your automation can be executed against more than one browser.
-   Your automation can be executed against more than one resolution.
-   You have implemented separate commands to trigger these runs leveraging:
    -   CLI commands for your test framework
    -   IDE/Language specific commands (configurations, package scripts, etc)
-   Your test reports indicate the environment testing was executed against.

## General Instructions

It may or may not shock you how often bugs occur in one browser, but not in another. Native components like data pickers tend to be handled quite differently between browsers, or one browser supports a new standard, while another is years behind.

You might find that you need to adapt how your tests find or interact with elements to be more stable across browsers, but this will be worth the time!

-   Remember if you tests works in one browser and fails in another, verify whether you can complete the test manually in that browser before you assume it's a bug in the web app.

Modern applications use reactive design, and change their format based on screen size. There are a couple of general solutions to this:

-   Write separate tests for full size vs. mobile
-   Use branching logic in your test methods.
    -   i.e. A method `addMovie(movieDetails)` might contain something like this:
    ```javascript
    addMovie:(movieDetails){
        if(env.isMobile){
            // opens the hidden menu on a smaller screen
            menu.openMenu()
        }
        menu.select("Entities", "Movie")
        driver.findElement(newMovieButton).click()
        // etc.
    }
    ```
    This same process can solve some browser issues too.

You don't have to get your tests running always/everywhere, but this is good practice, and your tests should be reliable with at least a couple of environments.

## Keep In Mind

> **Tests Should Be Reliable**
>
> Nothing kills confidence in automation like a slew of false positives, or huge bugs that slip by. You want your team to be able to rely on your tests, and not be concerned about their flakiness.
>
> It's generally better to have fewer _but stable_ tests vs more tests that are flakier.

> **Test For Your Users**
>
> Save yourself some time and effort; find out what _your_ users use in terms of browsers and devices. Spend more time working in those environments instead of the more limited environments, until you _have_ the time to spend there.

## General Links

-   [BrowserStack: Cross Browser Testing](https://www.browserstack.com/cross-browser-testing)
    -   The writeup is to sell you on using their service to accomplish your testing across multiple environments, and thus does a great job explaining why it's important, and how to prioritize your efforts!
-   [SoftwareTestingHelp: Responsive Web Design Testing Guide](https://www.softwaretestinghelp.com/responsive-web-design-testing-guide/)
    -   Good info on how responsive design can impact our testing efforts.
