# Step 6: Cypress Specific

[< Prev](./cy5.md) | [General Step Instructions](../step6.md) | [Next >](./cy7.md)

---

[TOC]

## Summary

We have here a story about viewing and editing a record. We also have our acceptance criteria about all of the different places the information (original or edited) should be visible, so designing tests to meet this criteria should be pretty simple.

Coding your tests should also be fairly straightforward, given that you will be using actions you have already utilized.

-   Navigating between pages
-   Getting text from elements
-   Clearing/Setting inputs
-   Clicking buttons

Don't forget you do need to abstract shared functionality from your tests.

-   Create multiple page objects to house your functionality
-   Use functions/objects with methods to house your functionality

Arguably, verifying content in a table might seem complicated, but you can break it down:

1. Get the rows in your table
1. Find the row in question using the record's ID
    - (find the row with the correct value in the correct column)
1. Verify the other cells in that row match the values expected

### Simple Table Example

Testing against the table in W3School's [HTML Tables](https://www.w3schools.com/html/html_tables.asp) page should show roughly what I mean.

I'll start with the basic test boilerplate, in a new file, `tableTest.js`

```Cypress
describe("testing tables", () => {
    beforeEach(() => {
        cy.visit("https://www.w3schools.com/html/html_tables.asp");
    });
    it("loads", () => {
        cy.title().should("contain", "HTML");
    });
});
```

This will load into w3 school's table page.

![](./screencaps/w3schoolstable.png)

The following example does a few things with tables; you should be able to find something to help you along your way working with the entity tables in the test application.

#### tableTest.js

```Cypress
describe("testing tables", () => {
    beforeEach(() => {
        cy.visit("https://www.w3schools.com/html/html_tables.asp");
    });
    it("can check within the contents of a whole table", () => {
        cy.get("#customers").should("contain.text", "Canada");
    });
    it("can verify that a specific row is present", () => {
        cy.get("#customers")
            .find("tr")
            .should((rows) => {
                let found = false;
                for (let i = 0; i < rows.length; i++) {
                    cy.wrap(rows[i])
                        .find("td")
                        .then((cells) => {
                            // you can use jQuery, remember?
                            cy.wrap(cells[0])
                                .invoke("text")
                                .then((text) => {
                                    if (text === "Island Trading") {
                                        cy.wrap(cells[1]).should(
                                            "have.text",
                                            "Helen Bennett"
                                        );
                                        cy.wrap(cells[2]).should(
                                            "have.text",
                                            "UK"
                                        );
                                        found = true;
                                    }
                                });
                        });
                    if (found) break;
                }
            });
    });
    it("can find all unique countries", () => {
        let countries = [];
        // this list is up to date for the table as of 1/19/22
        let expectedCountries = [
            "Austria",
            "Canada",
            "Germany",
            "Italy",
            "Mexico",
            "UK",
        ];
        cy.get("#customers")
            .find("tr")
            .each(($row, index, $list) => {
                if (index > 0)
                    //skip the header row
                    cy.wrap($row)
                        .find("td")
                        .eq(2)
                        .invoke("text")
                        .then((country) => {
                            if (!countries.includes(country))
                                countries.push(country);
                        });
            })
            .then(() => {
                cy.log("Found these countries...", countries);
                for (let expected of expectedCountries)
                    expect(countries).to.include(expected);
            });
    });
});
```

#### Some things to notice:

Don't stress if this takes you a bit longer: you are applying processes you've used before, sure, but this application is a bit different, and longer.

<!-- ## Tutorials/Docs

- [Node.js Modules (Node.js official)](https://nodejs.org/api/modules.html)
- [Understanding module.exports and exports in Node.js (Sitepoint)](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) -->
