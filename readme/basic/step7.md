# Step 7 - Story: Adding/Removing Movie Records

[<Prev](./step6.md) | [Main](../../README.md) | [Next>](./step8.md)

---

[TOC]

## Story

As a standard user I should be able to add or remove Movies.

-   Movies are viewable from the main "Movies" option in the nav bar, but can only be added/removed from the movie page in the "Entities" dropdown.

When creating a new movie, I can enter the movie's:

-   Title
-   Overview
-   Release Date
-   Production Company
-   Director(s)
-   Cast Member(s)

The Director and Cast Member fields should allow me to select multiple People for each role.

I should be able to view/edit/delete existing, updated, or newly added movies.

### Technical Acceptance Criteria

Most of this testing should go the same way as step 6; you might even be able to use a lot of the same code with a few tweaks.

The biggest differences are:

-   You need to use some sort of stored test data (in a JSON, CSV, etc.)
-   Iterate over the stored data

## General Instructions

Some of you may have implemented Data Driven Testing in your Step 6 automation; no problem, you're ahead of the game.

Data Driven Testing is when you write your tests to consume external data; multiple movies, people, etc. This allows you to add/edit tests by updating your stored data instead of the test code, usually just by adding an item to an array, or a line to a CSV.

-   Add another movie
-   Add additional cast members

Generally, you will just import the external data, then iterate over the data for your test(s). External data is more easily reusable and maintainable, and keeps your testing clean.

## Keep In Mind

> **Iterating Tests**
>
> Using something like an array or a list can be a huge help when running the same steps with different data. Many testing frameworks allow you to put a test inside of a loop, which saves us a lot of time by looping through our test data, passing the data directly into the test.
>
> ```
> for(test in test_data){
>   test("testing x with " + test_data.name){
>     stepA(test_data.name)
>     // stepB(...)
>     // etc...
>   }
> }
> ```
>
> Even when your test framework doesn't allow tests in a loop, you can put your test steps in a function and use simple test declarations:
>
> ```
> test("first run"){
>   test_function(test_data[0])
> }
> test("second run"){
>   test_function(test_data[1])
> }
> ```

## Language/Framework Specific Instructions

-   [JavaScript](./js/js7.md)
-   [Python](./python/p7.md)
-   [C#](./CSharp/CSharp7.md)
-   [Cypress.io](./cypress/cy7.md)

## General Links

-   [An Introduction to Data-Driven Test Automation](https://nearshore.perficient.com/software-development/an-introduction-to-data-driven-test-automation/)
    -   An overview of data driven testing.
