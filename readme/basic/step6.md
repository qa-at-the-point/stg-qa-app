# Step 6 - Story: Viewing/Editing Person Records

[<Prev](./step5.md) | [Main](../../README.md) | [Next>](./step7.md)

---

[TOC]

## Story

As a standard user I should be able to view or edit a "Person" record.

-   These records are accessible from the "Entities" dropdown once logged in.

Visible in the "People" table, you can see the person's

-   ID
-   Name
-   Birthday
-   Biography
-   Profile Path
-   Homepage
-   Also Known As

By using the ID link, or the view button to the right, I can see the individual record page, which shows the same information in a different format.

The edit button from the "People" table or from the individual record page allows me to edit all fields except for the person's ID.

### Technical Acceptance Criteria

-   Verify data is correct in:
    -   The table view
    -   The individual record
    -   The edit page
-   Verify saved edits in these pages as well.
-   Verify navigation throughout the process:
    -   Links/buttons all work as expected
-   Leverage the model you started using in Step 5.

## General Instructions

Now we're getting into more of the regular use of the application. This is the sort of story that gives us testing that is perfect for automation; repetitive tasks that are core to the application's functionality.

-   Consider how the user in this story would use the application.
-   If there are multiple ways to accomplish something, test the different methods.
-   Abstract the steps you'll use more than once.
    -   Methods on a page object, or exported from another file are easier to maintain; there is only one spot to update when the application changes.
    -   It also keeps the tests themselves cleaner/easier to read.
-   Don't forget negative tests - inputting data that shouldn't work, or cancelling out of processes.

## Keep In Mind

> **Don't Over-Abstract**
>
> It's easy to get caught in the trap of making something OVERLY efficient. Sometimes it's not worth the effort -- don't spend so much time making one or two AMAZING functions that you could have finished your entire project instead of just this piece.
>
> For example: SpaceX did a lot of work developing stronger and more efficient carbon fiber capsule designs, only to realize that the final product was so finnicky that a classic stainless steel was much more cost efficient.

> **Smaller Tests > Bigger Tests**
>
> Creating more test files, or more tests within each file, is generally better than cramming too much into one. Generally, you'll want to do your best to check a small number of things per test. Ideally, only one.
>
> You may have heard of **defect masking** where one failure can make others harder to see...
>
> I.E. Your test checks _1. Editing a Record_, then _2. Viewing a Record_, and there is a bug in editing the record. Your test will stop there, and never check viewing the record. If that is the only place you test viewing a record, it may leave a simple bug undiscovered until the editing bug is fixed!

## Language/Framework Specific Instructions

-   [JavaScript](./js/js6.md)
-   [Python](./python/p6.md)
-   [C#](./CSharp/CSharp6.md)
-   [Cypress.io](./cypress/cy6.md)

## General Links

-   [An Introduction to Data-Driven Test Automation](https://nearshore.perficient.com/software-development/an-introduction-to-data-driven-test-automation/)
    -   An overview of data driven testing.
