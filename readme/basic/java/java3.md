# Step 3: Java Specific

[< Prev](./java2.md) | [General Step Instructions](../step3.md) | [Next >](./java4.md)

---

[TOC]

## Summary

Logging in using a function is a basic part of most automation setups; after all, it's something we need to do all the
time in our applications.

The following example of adding a search function to a test should show how you might add a login function to your test
file.

### Simple Example

We'll create a method (_function_) that will send a search term to the Google search box and then click the Search
button.

#### The Method

This method (the name used in Java for "function") will be placed at the bottom of our test class. Methods are not
typically used within test classes, we would typically put them either in a Page Object Model class or another utility
class, but for the sake of demonstration and simplicity we'll just add it to the bottom of our test class.

```java
public void searchGoogle(WebDriver driver,WebDriverWait wait,String searchTerm){
    By searchBar=By.name("q");
    By searchBtn=By.name("btnK");

    driver.findElement(searchBar).sendKeys(searchTerm);
    wait.until(ExpectedConditions.elementToBeClickable(searchBtn));
    driver.findElement(searchBtn).click();
}
```

Some things to take note of:

* Before our method name we use the words "public" and "void". The keyword _public_ means that the method is accessible
  to other classes, not just the class the method belongs to. _Void_ essentially means that the method is just
  performing an action, and is not returning any objects.
* This method will take three parameters: "driver", "wait" and "searchTerm". We need to pass it the _driver_ instance so
  that the method will be able to utilize it for finding our web elements. When we've made the driver available to the
  entire class (by declaring `Webdriver driver` at the top of the class) we typically would not need to send it again,
  but to demonstrate how we would use WebDriver in another class, this is how it would be done. The case for an instance
  of `driver` is the same for the instance of `WebDriverWait`. Our _searchTerm_ is simply the text string that we would
  use.

#### The Test

```java
@Test
public void testOne(){

    driver.navigate().to("https://www.google.com");

    String searchTerm="selenium automation";
    searchGoogle(driver,searchTerm);

    By results=By.id("search");
    wait.until(ExpectedConditions.visibilityOfAllElementsLocatedBy(results));

    Assert.assertTrue(driver.findElement(results).getText().contains(searchTerm),
        String.format("The search results should contain the term '%s'.",searchTerm));
}
```

Note the changes that we have made to our test code:

- We've replaced the `By` locator and `wait` with our new method
- Our method will perform the search independently
- A new `By` has been added to locate our search results
- We wait for the search results to be visible in the browser
- We run an _assertion_ to verify that the search results contain our search term, and we've also added a message that
  will display in the output if our search term is not found in the results

## Documentation

- Official Docs
    - [Java Methods](https://www.w3schools.com/java/java_methods.asp)
    - [Sending Keys to Keyboard](https://www.selenium.dev/documentation/en/webdriver/keyboard/)
    - [WebDriverWait](https://www.selenium.dev/selenium/docs/api/java/org/openqa/selenium/support/ui/WebDriverWait.html)
