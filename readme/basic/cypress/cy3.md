# Step 3: Cypress Specific

[< Prev](./cy2.md) | [General Step Instructions](../step3.md) | [Next >](./cy4.md)

---

[TOC]

## Summary

Logging in using a function is a basic part of most automation setups; after all, it's something we need to do all the time in our applications.

The following example of adding a search function to a test should show how you might add a login function to your test file.

### Simple Example

I added a function and a new test into my `firstTest.test.js` file to search Google.

#### The function:

(I put this JS function at the bottom of my file)

```js
function search(term) {
    // .type(text:string) will type the text passed in INTO the
    // element yielded by the previous command.
    cy.get("[name=q]").type(term);
    // .click() will click the element yielded by the previous command!
    // go figure.
    cy.get("[name=btnK]").eq(0).click();
}
```

#### The test:

(I added this to my `firstTest.js` file's `describe("visiting google")` block.)

```js
it("can search for puppies", () => {
    // call the function
    search("puppies");
    // check the results element, cypress automatically retries locating
    // elements, and then the `should` will keep re-pulling `#rso` until
    // it passes, or times out.
    cy.get("#rso").should("contain", "Puppies");
});
```

## Gotchas

Cypress, to save time, will maintain sessionStorage between tests run in the open Test Runner.

**What does this mean?** Well, it means that your user stays logged in on this app.

### The Solution

I'm going to give you a freebie... There are other options, but this seems one of the simplest. It's a custom command (more on those later) to visit a page while clearing session storage.

1. Add the code to your `cypress/support/commands.js`
1. Call `cy.visitFresh()` in your beforeEach instead of `cy.visit()`
    - If you navigate directly to a page in the future after logging in, still use `cy.visit()`

`commands.js` update

```js
Cypress.Commands.add("visitFresh", (url, options?) => {
    return cy.visit(url, {
        ...options,
        onBeforeLoad: (win) => win.sessionStorage.clear(),
    });
});
```

`beforeEach()` update

```js
cy.visitFresh("http://localhost:8080");
```

## Tutorials/Docs

-   Official Docs:
    -   Commands
        -   [type](https://docs.cypress.io/api/commands/type)
    -   [Assertions/retries/timeouts on get](https://docs.cypress.io/api/commands/get#Assertions)
