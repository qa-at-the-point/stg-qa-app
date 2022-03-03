# Step 3 - Story: Log In as User

[<Prev](./step2.md) | [Main](../../README.md) | [Next>](./step4.md)

---

[TOC]

## Story

As a user with the following account details, I should be able to log in as a user, with access to the Movies page, the various Entities, and Account Settings. If I'm prompted to sign in to access a page, I am redirected to that page after signing in. There is also a contextualized message on the home page.

-   Username: `user`
-   Password: `user`

I should also be able to log out.

### Acceptance Criteria

-   As a user I can sign in with those credentials anywhere the sign in modal is accessed.
-   The following pages are only accessible when logged in:
    -   Movies
    -   Entities Pages (the option doesn't exist in the menu if not logged in)
    -   Account settings (also not present until logged in)
    -   When logging in, the page remembers the context. (i.e. logging in to get the "Movies" page, I'm redirected to that page after logging in successfully)
-   When logged in the home page message is present, `You are logged in as user "user".`
-   As a user I can log out

### Technical Acceptance Criteria

-   You should be logging in using a function or method. That function for now can be in the same file as the test.
-   This test should be in a separate file from the home page test.

## General Instructions

There are three main technical skills you'll use in this step:

1. Interacting with elements.
    - Typing/Sending keystrokes
    - Clicking on elements
2. Handling changes to the site.
    - Waiting for elements to show/disappear.
        - You can also wait for text to change.
        - Just make sure what you were waiting for isn't already on the page BEFORE you start waiting.
    - Handling state
        - You'll be logged in at the end of some tests, but need to be logged out to try again in the next test.
        - One option: Use your setup/teardown hooks to kill the original driver and get a new one before each test.
3. Using a function or method.
    - Abstracting out repeated steps into functions or methods is important - most of your tests will require you to be logged in; having a function to reference instead of copying the same code everywhere is SMART.

To start, you should be able to copy the structure or "boilerplate" of your homepage test to a new test. Once you know _how_ to test the acceptance criteria, then it's time to get coding.

I'd also recommend breaking this up into several smaller tests within your test file.

## Keep In Mind

> **Organizing Automated Testing:**
>
> I tend to prefer bigger manual tests that check more and require less documentation maintenance. That is, if I document my tests beyond a few bullet points even...
>
> When it comes to automation, I prefer the opposite.
>
> -   If you or I see a bug when testing manually, we know we can keep looking at the rest of the test for possible issues.
> -   Automation will just stop.
>
> Keep your tests smaller - each will usually cover a single (or part of a single) acceptance criteria.

> **Functional Testing & Functions:**
>
> Functional testing is all about making sure our applications can do the things we want them to. It means that much of the time, we're following the same steps with minor differences in inputs/decisions -- this is the perfect time for a function or method in our code.
>
> We can reuse our method/function over and over with those minor differences, and get several, or even hundreds of executions FAR faster than we can execute them manually.
>
> This is what can make automation worth spending time on!
>
> **BUT** - don't get so obsessed with making the perfect function, getting it "just right" and supremely flexible, that you spend more time than it could ever save you.

## Language/Framework Specific Instructions

-   [JavaScript](./js/js3.md)
-   [Python](./python/p3.md)
-   [C#](./CSharp/CSharp3.md)
-   [Cypress.io](./cypress/cy3.md)

## General Links

-   Selenium WebDriver Page
    -   [Keyboard](https://www.selenium.dev/documentation/en/webdriver/keyboard/)
    -   [Waits](https://www.selenium.dev/documentation/en/webdriver/waits/)
-   [What does abstraction mean in programming?](https://stackoverflow.com/a/21220945)
    -   Awesome (if long-ish) Stack Overflow answer about abstraction and functions...
