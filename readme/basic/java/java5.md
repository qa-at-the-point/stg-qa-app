# Step 5: Java Specific

[< Prev](./java4.md) | [General Step Instructions](../step5.md) | [Next >](./java5.md)

---

[TOC]

## Summary

In this lab we'll introduce the Page Object Model. 


#### TestBase.java
```java
package base;

import io.github.bonigarcia.wdm.WebDriverManager;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.annotations.AfterSuite;
import org.testng.annotations.BeforeSuite;

import java.time.Duration;

public class TestBase {

    public static WebDriver driver;
    public static WebDriverWait wait;

    @BeforeSuite
    public void init() {
        WebDriverManager.chromedriver().setup();
        driver = new ChromeDriver();
        wait = new WebDriverWait(driver, Duration.ofSeconds(10));
    }

    @AfterSuite
    public void tearDown() {
        if (driver != null) {
            driver.quit();
        }
    }
}
```

#### GooglePage.java

```java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.support.PageFactory;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class GooglePage {

    private final WebDriver driver;

    public GooglePage(WebDriver driver) {
        PageFactory.initElements(driver, this);
        this.driver = driver;
    }

    private final By searchBar = By.name("q");
    private final By searchBtn = By.name("btnK");

    public void searchGoogle(WebDriverWait wait, String searchTerm) {
        driver.findElement(searchBar).sendKeys(searchTerm);
        wait.until(ExpectedConditions.elementToBeClickable(searchBtn));
        driver.findElement(searchBtn).click();
    }
}
```

#### Using @FindBy Annotation

```java
package pages;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.FindBy;
import org.openqa.selenium.support.PageFactory;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class GooglePage {

    private final WebDriver driver;

    public GooglePage(WebDriver driver) {
        PageFactory.initElements(driver, this);
        this.driver = driver;
    }

    @FindBy(name = "q")
    static WebElement searchBar;

    @FindBy(name = "btnK")
    static WebElement searchBtn;

    public void searchGoogle(WebDriverWait wait, String searchTerm) {
        searchBar.sendKeys(searchTerm);
        wait.until(ExpectedConditions.elementToBeClickable(searchBtn));
        searchBtn.click();
    }
}
```

#### SeleniumTests.java
```java
import base.TestBase;
import org.openqa.selenium.By;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.testng.Assert;
import org.testng.annotations.Test;
import pages.GooglePage;

public class SeleniumTests extends TestBase {

    @Test
    public void testOne() {
        driver.navigate().to("https://www.google.com");
        
        GooglePage googlePage = new GooglePage(driver);
        String searchTerm = "testing";
        googlePage.searchGoogle(wait, searchTerm);

        By results = By.id("search");
        wait.until(ExpectedConditions.visibilityOfAllElementsLocatedBy(results));

        Assert.assertTrue(driver.findElement(results).getText().contains(searchTerm),
                String.format("The search results should contain the term '%s'.", searchTerm));
    }

}
```

## Documentation
- [Page Object Model](https://www.selenium.dev/documentation/test_practices/encouraged/page_object_models/)
- [@FindBy Annotation](https://www.selenium.dev/selenium/docs/api/java/org/openqa/selenium/support/FindBy.html)
- [The _final_ Keyword](https://www.baeldung.com/java-final)
