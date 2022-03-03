# STG QA Certifications

[TOC]

## Overview

Our QA certification process has been designed to help you to, from start to finish, develop an automation solution for a real application.

-   The focus is on developing/showing your skills for REAL solutions, not completing toy problems.

The app is not perfect, nor is it used in production currently, but it is true to something you might be testing against in the industry.

> **Important**
> This was developed for internal use at STG. We're happy to share, but it's not going to be perfect for your use. ALSO, it was written for Bitbucket's readme markdown processing... Github's is better, but the end result is a bit clunky.

#### Certifications Offered

We offer both Automation and Advanced Automation certifications for the following. Note, several are in "beta" and are not as well supported.

-   C# and Webdriver (beta)
-   Java and Webdriver
-   JavaScript and Webdriver
-   Python and Webdriver
-   Cypress.io (a JS tool, beta)

### The Certification Process

1. Fork the [stg-qa-app](https://github.com/qa-at-the-point/stg-qa-app) repository, and clone it to your computer.
    - [How to fork in Bitbucket](https://confluence.atlassian.com/bitbucket/forking-a-repository-221449527.html)
    - [How to clone a git repo](https://support.atlassian.com/bitbucket-cloud/docs/clone-a-git-repository/)
1. [Get the test application running](#host) on your machine.
1. Follow the instructions for the [basic](#basic) or [advanced](#advanced) certification.
    - See the task specific docs for some FAQs about each, as well as links to tutorials/documentation that will be helpful for each language.

**Ask if you have questions!!!**

---

## Hosting the Application

##### Prerequisite:

Fork and clone the [stg-qa-app](https://github.com/qa-at-the-point/stg-qa-app) repository.

-   [How to fork in Bitbucket](https://confluence.atlassian.com/bitbucket/forking-a-repository-221449527.html)
-   [How to clone a git repo](https://support.atlassian.com/bitbucket-cloud/docs/clone-a-git-repository/)

Set up your BitBucket account for Git authentication. There are two methods you can choose from when using a Google Account for Atlassian.

-   [Use an App Password](https://support.atlassian.com/bitbucket-cloud/docs/app-passwords/)
-   [Use SSH](https://support.atlassian.com/bitbucket-cloud/docs/set-up-an-ssh-key/)

#### 1. Install Dependencies

1. Install Docker
    - Download [Docker Desktop](https://www.docker.com/products/docker-desktop)
    - Login or Register a user on [Docker Hub](https://hub.docker.com)
    - Make sure to login using the CLI: `docker login`
1. Install Node / NPM (Optional)
    - Download [node.js](https://nodejs.org/en/download/)
    - **If not installing**, you'll need to use the manual `docker` commands provided.
1. Open a terminal to the project's root directory.

#### 2. Start the App

1. Launch the `Docker Desktop` application
1. Open a terminal to the project's root directory.
1. Start Server: `npm run docker-up`
    1. To run without NPM:
        1. `docker compose -f src/main/docker/app.yml pull`
        1. `docker compose -f src/main/docker/app.yml up -d`
1. Open Browswer: [localhost:8080](http://localhost:8080)

#### 3. Monitor the App (optional)

1. View the server logs: `npm run docker-log` or `docker compose -f src/main/docker/app.yml logs`
1. To tail the server logs: `npm run docker-tail` or `docker compose -f src/main/docker/app.yml logs -f`

### 4. Shut Down the Application

1. Stop the Server, in a terminal: `npm run docker-stop`
    1. Stop without NPM: `docker compose -f src/main/docker/app.yml stop`

### 5. Remove the Application

1. Remove the application and database containers, including all data, in a terminal: `npm run docker-down`
    1. Remove without NPM: `docker compose -f src/main/docker/app.yml down`

> The application will take up a good amount of processing power on your machine - shutting it down when not working on the certification is a good idea.

> Using the `npm run docker-down` or `docker compose -f src/main/docker/app.yml down` command(s) will remove all data from the database. To restore the default data, start the application with the `up` commands.

---

## Automation Certification

This is used at STG for the following certifications, based on the language/framework you use to complete the Automation Engineer steps:

-   C#/Webdriver Automation Certification
-   Java/Webdriver Automation Certification
-   JS/Webdriver Automation Certification
-   Python/Webdriver Automation Certification
-   Cypress.io Automation Certification

> **Note**: Each of the following steps has a general set of instructions and acceptance criteria, and then a link to language/framework specific instructions if you would like more guidance for your work.
>
> JavaScript, Python, C#, and Cypress.io currently have language/framework specific instructions, Java is still pending.

**Ask if you have any questions, or if anything is unclear.**

**The Steps**

-   [Step 1 - Task: Initialize Framework](/readme/basic/step1.md)
-   [Step 2 - Story: Home Page](/readme/basic/step2.md)
-   [Step 3 - Story: Log In as User](/readme/basic/step3.md)
-   [Step 4 - Story: Log In as Admin](/readme/basic/step4.md)
-   [Step 5 - Task: Page Objects and other Models](/readme/basic/step5.md)
-   [Step 6 - Story: Viewing/Editing Person Records](/readme/basic/step6.md)
-   [Step 7 - Story: Adding/Removing Movie Records](/readme/basic/step7.md)
-   [Step 8 - Story: Searching Movies](/readme/basic/step8.md)
-   [Step 9 - Task: Pull Request](/readme/basic/step9.md)

Remember to save your work often - [commit](https://www.atlassian.com/git/tutorials/saving-changes) and [push](https://www.atlassian.com/git/tutorials/syncing/git-push) your code to your repository regularly.

---

## Advanced Automation Certification (Beta)

This is used at STG for the following certifications, based on the language/framework you use to complete the Advanced Automation Engineer steps:

-   C#/Webdriver Advanced Automation Certification
-   Java/Webdriver Advanced Automation Certification
-   JS/Webdriver Advanced Automation Certification
-   Python/Webdriver Advanced Automation Certification
-   Cypress.io Advanced Automation Certification

Pre-requisites:

-   You must have completed the Automation Engineer certification for the same language
-   OR have specific permission on skipping ahead from a member of QA Leadership.
-   You are expected to have a deeper understanding and more experience than the Automation Engineer certification requires.
-   You should have your code ready from the Automation Engineer certification to build on going forward.

> **Note**: Each step for the Advanced Automation Engineer certification has a set of instructions and acceptance criteria, but _does not_ have language/framework specific instructions.
>
> Feel free to come to us with questions, but know that you are expected to either already understand the process, or be able to do much of your own research for this level of certification.

**Ask if you have any questions, or if anything is unclear.**

**The Steps**

-   [Step 1 - Task: Cleaner Tests Using APIs](/readme/advanced/step1.md)
-   [Step 2 - Task: Reading and Writing Files](/readme/advanced/step2.md)
-   [Step 3 - Task: Reporting](/readme/advanced/step3.md)
-   [Step 4 - Task: Cross-Environment Testing](/readme/advanced/step4.md)
-   [Step 5 - Task: CI/CD Pipeline Testing](/readme/advanced/step5.md)
-   [Step 6 - Task: Submission for Code Review](/readme/advanced/step6.md)

---

## Old Certification Documents

-   [C#](https://docs.google.com/document/d/1y4aIeOmWgGc-wVlcG4UxoVgBL_ZeFRFvDjHIT0UBJo4/edit#heading=h.dunli9k39ffv)
-   [Java](https://docs.google.com/document/d/1QaNU7VYzyhO6ZPXfcQJw-mysO1gc3QC4sgLFgKnvOvc/edit#heading=h.dunli9k39ffv)
-   [JavaScript](https://docs.google.com/document/d/1QSldT355ljXtEmUSDgEumT3EbO7ml5sMuUIznIQhlaE/edit#heading=h.26hfj3wbnqqy)
-   [Python](https://docs.google.com/document/d/1eK36p1qRrS_DkG_sMuRxO_iYm_QMlLLbn3msb4hq9Fo/edit)
