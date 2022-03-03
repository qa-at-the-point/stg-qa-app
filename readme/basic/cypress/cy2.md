# Step 2: Cypress Specific

[< Prev](./cy1.md) | [General Step Instructions](../step2.md) | [Next >](./cy3.md)

---

[TOC]

## Summary

You've been tasked to verify the home page of our new application. You've been given your story -- and it shouldn't be too hard to verify.

1. You need to navigate to the page.
    - When you are running the application locally, you can load the home page with `cy.visitt("http://localhost:9000")`
1. You need to locate and assert on the proper criteria.
    - You can use jQuery locators
    - You can use the built in assertions (Chai, Sinon, and jQuery assertions)

### Simple Example

We'll update the test for visiting Google to add one more test verifying that the search bar is visible, and a few other things.

1. First, I'll add a `beforeEach()` method to our `describe` block to visit Google before each test runs...

2. Then I'll add the second test! Here is the code you can see, where I find/verify a few different things on Google's homepage.

**firstTest.js**

```js
/// <reference types="Cypress" />

describe("visiting google", () => {
    beforeEach(() => {
        cy.visit("https://google.com");
    });
    it("shows 'Google' as the page title", () => {
        // I'm simplifying here, since the chained assertion is easiest
        // for most situations.
        cy.title().should("equal", "Google");
    });
    it("has a valid UI", () => {
        cy.visit("https://google.com");
        cy.get("input[name=q]")
            .should("be.visible")
            // should assertions yield the subject of their assertion
            // to the next method, so we can keep chaining.
            .should("have.attr", "title", "Search")
            .should("have.value", "");
        // There are TWO input buttons with the name "btnK"
        // cy.get("[name=btnK]") will yield both
        // the `.eq(0)` method picks the first from the results
        // just like in jQuery.
        // The first is hidden on the autocomplete popup, but
        // the second, at index 1, is visible right away.
        cy.get("[name=btnK]").eq(1).should("be.visible");
        // We could also chain a .find() off of a .get() to sort of
        // "search within" a previous element or elements. Here I
        // will get the autocomplete popout, and find the Google Search
        // button within it.
        cy.get("[jsaction*=mouseout]")
            .find("[name=btnK]")
            .should("not.be.visible")
            .should("have.value", "Google Search")
            .should("have.attr", "type", "submit");
        // cy.contains(someText) will search the whole page, or chain
        // off of a previous .get() or .find()
        cy.contains("I'm Feeling Lucky").should(
            "have.attr",
            "aria-label",
            "I'm Feeling Lucky"
        );
    });
});
```

## Tutorials/Docs

-   Official Docs:
    -   Commands:
        -   [get](https://docs.cypress.io/api/commands/get)
        -   [find](https://docs.cypress.io/api/commands/find)
        -   [eq](https://docs.cypress.io/api/commands/eq)
        -   [should](https://docs.cypress.io/api/commands/should)
    -   [Using Mocha's bdd syntax](https://docs.cypress.io/guides/references/bundled-tools#Mocha)
