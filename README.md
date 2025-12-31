# java-selenium-automation-notes
WHERE Method Overloading Is Used in Selenium
Inside Selenium WebDriver APIs (Already Overloaded)
Same method name, different parameters (By.id, By.name, By.xpath).
In Selenium automation, method overloading is used to create reusable actions like click, sendKeys, and wait methods with different parameter types such as By locators and WebElements. It helps handle different scenarios using the same method name, improving readability and maintainability of the framework. Selenium WebDriver itself uses method overloading in APIs like findElement and sendKeys. This supports compile-time polymorphism and makes test scripts cleaner and flexible.
findElement:
driver.findElement(By.id("email"));
driver.findElement(By.name("email"));
driver.findElement(By.xpath("//input[@id='email']"));
sendKeys:
element.sendKeys("Hello");
element.sendKeys(Keys.ENTER);
element.sendKeys("User", Keys.TAB);
WebDriverWait.until():
wait.until(ExpectedConditions.visibilityOf(element));
wait.until(ExpectedConditions.elementToBeClickable(locator));
HOW USE Method Overloading in Automation Framework
Reusable Click Method (Very Common):
public class ActionUtil {

    public void click(By locator) {
        driver.findElement(locator).click();
    }

    public void click(WebElement element) {
        element.click();
    }
   }
Send Text With Optional Clear:
public void enterText(By locator, String value) {
    driver.findElement(locator).sendKeys(value);
}

public void enterText(By locator, String value, boolean clearFirst) {
    WebElement element = driver.findElement(locator);
    if (clearFirst) {
        element.clear();
    }
    element.sendKeys(value);
}
Real Selenium Framework Example (Interview GOLD ⭐) :
public void waitForElement(By locator) {
    new WebDriverWait(driver, Duration.ofSeconds(10))
        .until(ExpectedConditions.visibilityOfElementLocated(locator));
}

public void waitForElement(WebElement element) {
    new WebDriverWait(driver, Duration.ofSeconds(10))
        .until(ExpectedConditions.visibilityOf(element));
}

}

