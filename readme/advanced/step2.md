# Step 2 - Task: Reading and Writing Files

[<Prev](./step1.md) | [Main](../../README.md) | [Next>](./step3.md)

---

[TOC]

## Task

Tests may need to interact with files for any number of reasons -- testing upload/download, providing test data, or recording results.

Update your testing to incorporate both reading and writing files. See the general instructions for ideas of how to use this productively.

### Technical Acceptance Criteria

-   You have incorporated reading a file into at least one test.
-   You have incorporated writing a file into at least one test.
-   Your existing tests are all still executable.

## General Instructions

Many applications allow users to upload pdfs/images/other files, or a way to export search results. These would both be great opportunities to test whether or not you could upload/download something.

Regardless of what an application allows, however, there is always utility for utilizing files in our testing:

-   Importing test data
-   Saving test results
-   Scraping/saving data

There is a bit more information on why each of these is useful below; make sure to read and write your files in a way that adds value to your testing - if you find a way not mentioned here, go for it!

### Importing Test Data

Many testers or other stakeholders find it easier to organize test data using a spreadsheet application, where each column might be a different input/expected result, and each row is then a test case. Exported as a .csv, we can import this into our testing and iterate over the rows for thorough test coverage.

### Saving Test Results

There are many already existing tools for reporting results of tests, but sometimes it's simpler to implement our own, especially if we want the results to be readable by a certain tool, or if we want to incorporate screenshots into the results view. Most often these results are written to .xml, .csv, or .json files.

### Scraping/Saving Data

We can leverage automation for far more than a simple test case. Sometimes it's particularly useful to go out and grab information from the web for our use. I've known people who used Selenium automation to hit a number of Fantasy Football websites, grab statistics and performance projections, and aggregate it all into one data set they used to make their picks; others have used similar processes for comparison shopping.

## Keep In Mind

> **Using Files Should Be Easy**
>
> While it might take a minute for you to parse how to use your language's file system tools, or to find an easy library to utilize, once implemented, this should be a value added proposition.
>
> If you find yourself struggling to utilize the new tool you've provided, consider how you are using it, how things are formatted, etc.
>
> -   Would it be easy for you or a stakeholder to add more tests by editing a test data file?
> -   Is it easy to read/understand your test results or scraped information?
>
> It's generally worth it to put a little more effort into making your files easy to read or edit instead of keeping them purely functional; this is a space that we are likely to need to interact with regularly, and share with others outside of QA.

## General Links

-   [The Significance of Data Driven Automation Testing](https://www.testing-whiz.com/blog/significance-of-data-driven-automation-testing)
    -   This should be a review of what was covered in the earlier cert, but is a good reminder of what you can do with a good data file.
-   [Introduction to Web Scraping Using Selenium](https://medium.com/the-andela-way/introduction-to-web-scraping-using-selenium-7ec377a8cf72)
    -   While this is language specific, it reviews good general practices and benefits.
