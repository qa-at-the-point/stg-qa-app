# Step 6 - Task: Submission for Code Review

[<Prev](./step5.md) | [Main](../../README.md) | [Next>]()

---

[TOC]

## Task

Get ready for your Code Review!

You need to commit and push your test solution, and create a pull request, just like you did for the earlier certification.

However, you should also spend time cleaning up, renaming things, adding comments, especially those that improve the quality of life in your IDE (tooltips, autocomplete, etc). Spend a little time now to make your code more understandable and maintainable.

### Technical Acceptance Criteria

Advanced Specific Criteria

-   Your code is formatted, named, and commented effectively.
-   You leverage a commenting solution enabling tooltips/prompts/explanations of key methods/functionality in your IDE.

The following criteria are identical to the submission criteria for the prior certification.

-   Your code for all previous steps is present in your forked repotisory.
-   Your project is configured so that we can clone, install dependencies, and execute your tests against the cert app without having to debug major problems specific to our machines.
-   You have submitted a pull request to merge your latest commit into the original repository, and submitted that link to qa.leadership@stgconsulting.com, letting us know your cert is ready for review.

## General Instructions

For details on the commit/push/pull request process, see the [previous certification's final step](../basic/step9.md).

Prepping for your code review isn't too crazy. Ask yourself this: if someone with knowledge of the language and tools came in and looked at your code, would they understand how and why it worked?

Your file structure, naming scheme, and comments should all support that understanding.

As for your documentation enabling IDE functions go, there are a number of formats that depend on the language/IDE you are using.

For Example most IDEs respect the following formats for each language:

-   Java - **JavaDoc**
-   JavaScript/TypeScript - **JSDoc**
-   C# - **XML Documentation**
-   Python - **Docstrings**
-   **DOxygen** and other tools might support multiple languages, or varying IDEs.

Take this example of a simple comment pulled from some production code:

```typescript
/** will search for a foo matching all provided filter(s) */
getFooFromSearch: (search: fooSearch) =>
    fooWsRequest("POST", "/foo/search", search);
```

The `/**` opening to the comment is a **JSDoc** convention that **VSCode** knows. If I start to use the `fooWsRequest` method from that example, I'll get a tooltip with the details `will search for a foo matching all provided filter(s)`. Add to that, the IDE can read my TypeScript definition file(s) and prompt me for the `search` parameter.

There are lots of things you can include in comments like these.

-   Parameters
-   Types
-   Examples
-   etc.

That said, don't spend too long working on this, but getting a minimum level of documentation in place will make your solution MUCH easier to maintain.

Know your audience. You aren't documenting for an end user, but for another automation engineer or developer; keep it simple! Put simply, this is just a chance to clean up your code for your code review.

## Keep In Mind

> **Good, Better, Best**
>
> You shouldn't spend more time than it's worth on cleanup/polish. At some point, if it works, well darn it, it works. That's still **good** enough.
>
> It's **better** if you can spend a few minutes now and then going through and renaming things effectively/adding comments where they're needed. Remembering or even understanding what you did six months ago can be challenging without the help!
>
> It's **best** if you have a plan/vision from the get-go and can lay everything out with names that make sense so that the code reads easily enough, and with comments already in place to make your test development that much easier, let alone maintenance.

## General Links

-   [Automation Panda: 10 Gotchas For Automation Code Reviews](https://automationpanda.com/2017/05/08/10-gotchas-for-automation-code-reviews/)
    -   One of the BEST writeups I've seen on cleaning up your automation. If you follow these practices, you'll have maintainable/understandable/clean code.
-   [TestProject: Automation Coding Practices to Adopt - Code Like a Developer](https://blog.testproject.io/2020/03/16/automation-coding-practices-adopt-code-like-a-developer/)
    -   More good practices on coding/commenting, also aimed at Automation Engineers.
