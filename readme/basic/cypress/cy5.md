# Step 5: Cypress Specific

[< Prev](./cy4.md) | [General Step Instructions](../step5.md) | [Next >](./cy6.md)

---

[TOC]

## Summary

Page objects are considered something of an *anti*pattern for Cypress, and it makes a decent amount of sense too. The framework is really lightweight when it comes to the tests themselves, and we don't need to be spending five or ten lines of code every file or even every test to initialize things.

Enter "Custom Commands"

## Custom Commands

Commands in Cypress are the methods that can chain from the `cy` command, or from other commands.

_Custom_ commands are methods YOU add that don't ship with Cypress.

1. We write a function.
2. Add the function to `cypress/support/commands.js`
3. Use the new command!

#### 1. Creating a Function

Piece of cake, we've already got one! Let's use our search function that's already sitting in `cypress/support/search.js".

Really though, almost any function would do, check out the links at the bottom for more about custom commands and cool things to do.

#### 2. `Cypress.Commands.add(name, callbackFn)`

Now to add the search command so that Cypress knows where to find it, we use a method on the global `Cypress` object.

`Cypress.Commands.add()` takes two arguments, minimum:

-   `name` - a string that will be the name of the method on the `cy` object.
-   `callbackFn` - the function that we're calling.

If we're getting technical and chaining commands deeper, there's a third `options` argument that let's us specify things like using a command that chains off of a `get` or `find` to act on an element found, that sort of thing.

We would either need to add this in our search.js file and import that into `cypress/support/commands.js`, or just add it straight to the `commands.js` file. I'll do the latter.

**`commands.js`**

```javascript
// first we import the function
import { search } from "./search";
// then we add it to Cypress's command list
Cypress.Commands.add("search", search);
```

And that's it! All that's left is implementation...

#### 3. Use the new command!

Now we can utilize the command. Let's try it out in our existing `firstTest.js` where we'd been using the `search` function already.

**`firstTest.js`** update:

```javascript
it("can search for puppies", () => {
    cy.search("puppies");
    cy.get("#rso").should("contain", "Puppies");
});
```

-   For this test I even stopped importing the search function at all -- this is 100% coming through as a Cypress command.

### Using Custom Commands

It's up to you exactly how you want to use these. Common implementations I've seen:

1. `cy.login(username, password)`
1. `cy.uploadFile(name, fileContent, mimeType)`
1. `cy.populateMyForm(formdata)`
1. `cy.scrapeScreen().should('deep.equal', myJsonOfExpectedResults)`
1. `cy.getMyCustomElement(someIdentifier).then(myElementWrappedInATestHarness=>/*...*/)`
    - Read on for this one!

### Using "Test Harnesses"

Page objects are certainly a bit heavy for Cypress' style, _but_ I use test harnesses on a regular basis still.

Consider an application that has custom components, like the data tables in our QA App.

1. You _could_ use a bunch of custom commands to test your component.
    ```javascript
    cy.withComponentADoX();
    cy.withComponentADoY();
    cy.withComponentADoZ();
    cy.withComponentBDoX();
    cy.withComponentBDoY();
    cy.withComponentBDoZ();
    ```
    - It works, it's just not my favorite, and then you have a whole bunch of custom commands that aren't necessarily related to each other, but are available everywhere.
1. I like to go for a happy medium. Create a sort of 'mini' page object as a test harness for the custom component, and use that.
    ```javascript
    cy.getComponentA().then((a) => {
        a.sortByColumn("X");
    });
    ```

**`exampleHarness.js`**

```javascript
class Component{
   public locator:string;
   constructor(locator:string){
       this.locator = locator
   }
   public getComponent(){
       return cy.get(this.locator)
   }
   public sortByColumn(columnName){
       cy.get(this.locator).find('th').contains(columnName).click()
   }
   // etc...
}
Cypress.Commands.add("getComponent", (locator:string)=>cy.wrap(new Component(locator)))
```

-   You'd just need to import this file in your `cypress/support/commands.js` file and you'd be set to go!
-   Any methods you add on your class would be available in your tests `cy.getComponent().then(myComponent=>myComponent.doSomeOtherThing())`

## To consider

At the end of the day, sort your tests in a way that makes sense to you! A smaller test library probably wouldn't use the harnesses. A larger one, it might make great sense, especially when shared with other QA engineers.

Try some different things out. Contrary to popular opinion, there is no _right_ way to automate something. But on the flip side, there are a lot of pretty bad ideas out there! Feel free to experiment and see where you get.

---

## Tutorials/Docs

-   Official Documentation
    -   [Custom Commands](https://docs.cypress.io/api/cypress-api/custom-commands)
    -   [TypeScript Support for Custom Commands](https://docs.cypress.io/guides/tooling/typescript-support#Types-for-custom-commands)
-   Tod Gentille-gitconnected: (Navigating Cypress Custom Commands)[https://levelup.gitconnected.com/navigating-cypress-custom-commands-412a817b088]
-   TutorialsPoint: (Cypress - Custom Commands)[https://www.tutorialspoint.com/cypress/cypress_custom_commands.htm]
