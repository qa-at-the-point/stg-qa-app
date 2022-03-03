# Step 4 - Story: Log In as Admin

[<Prev](./step3.md) | [Main](../../README.md) | [Next>](./step5.md)

---

[TOC]

## Story

As an admin user with the following credentials, I should have both the standard user access, as well as an administration menu with access to various pages listed below.

**Credentials**

-   Username: `admin`
-   Password: `admin`

**Administration Menu**

-   User management
-   User tracker
-   Metrics
-   Health
-   Configuration
-   Audits
-   Logs
-   API

I should also be able to log out.

### Acceptance Criteria

-   As an admin, I can log in.
-   I have access to everything a standard user has access to.
-   I also show the administration menu, and can access each of the pages listed above.

### Technical Acceptance Criteria

-   The function that was used to log in as a user should be moved to a separate file, and imported into the user login test file, and a new admin login test file.

## General Instructions

There is really only one new technical skill you'll be using in this step - using code from a different file.

1. You'll need to put your login function/method in a separate file.
1. Import it into your user login test, and make sure it works there.
1. Create a new test file verifying the acceptance criteria for admin login listed above.
    - Copying the "boilerplate" code from your user login test and tweaking it to suit your new test can make this easier. (Your import statements, the general structure, etc)

One other skill that you'll likely be exercising is waiting for new pages to load - some will be easy to wait for an element to appear, others, you might want to wait for the URL to change, etc.

## Keep In Mind

> **Files and Folders:**
>
> Leverage your file system. In our certification, you probably won't have TOO much code, so you might not get lost trying to figure out what goes where, or where a problem is.
>
> In practice, however, you might have thousands of lines of code. If that's all in one file, it can be easy to forget where something was, or even searching within you'll probably make an edit in the wrong spot. It's messy, and can be hard to understand if someone new comes on the project, or if you have to fix something in the future.
>
> Instead, keep your files pretty small. Split tests up across files wherever it makes sense. Keep your supporting code clean and organized too. We'll have page objects in the future, as well as other functionality, that should be stored separately from the tests themselves.
>
> There is no single perfect solution; figure out your happy spot!

## Language/Framework Specific Instructions

-   [JavaScript](./js/js4.md)
-   [Python](./python/p4.md)
-   [C#](./CSharp/CSharp4.md)
-   [Cypress.io](./cypress/cy4.md)

## General Links

-   [7 Steps for Building a Successful UI Automated Testing Framework](https://smartbear.com/resources/ebooks/steps-for-building-a-successful-ui-automated-test/)
    -   Step 1 specifically - note how broad it is.
    -   Step 5 - Your login function is an example of this
