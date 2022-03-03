# Step 7: Cypress Specific

[< Prev](./cy6.md) | [General Step Instructions](../step7.md) | [Next >](./cy8.md)

---

[TOC]

## Summary

Step 7 is basically Step 6 with an extra detail or two. Adding works almost exactly the same way as editing, and movies work much the same way as people.

Looping through your tests will likely be your biggest difficulty.

### Simple Examples

Just about the only wrinkle here when it comes to functionality are a few elements you might not have interacted with before:

-   **Date Inputs**
    -   Some apps need more detail... This one should just work if you type the date without punctuation, as works in many apps.
    -   `cy.type('2021-07-04')` should fill in 7/4/21 regarldess of browser/local
    -   Stick to the `yyyy-MM-dd` format.
-   **Dropdowns/Selects**
    -   This is easier than you'd think. Get the select, then select your option(s) by their text/value/index.
    -   `cy.get('select').select('option 1')`
    -   `cy.get('select').select([5,12,57])`

Defining your test data and then iterating through it might be something new for you, though similar to working with the table(s) in step 6.

1. Declare an array of your data.
2. Iterate through the array.

This is something we can show readily by using the `search` custom command we created for our Google testing.

#### `iteratingTest.js`

```Cypress
let tests = [
    { term: "puppies", result: "adopt" },
    { term: "NBA", result: "basketball" },
    {
        term: "Millions of Peaches",
        result: "The Presidents of the United States of America",
    },
];

describe("iterating searches", () => {
    beforeEach(() => {
        cy.visit("https://google.com");
    });
    tests.forEach(({ term, result }) => {
        it(`Searches for "${term}" and finds "${result}"`, () => {
            cy.search(term);
            cy.get("#search").should("contain.text", result);
        });
    });
});
```

## Tutorials/Docs

-   Official Docs
    -   [Date Inputs](https://docs.cypress.io/api/commands/type#Date-Inputs)
    -   [Commands: select](https://docs.cypress.io/api/commands/select)
