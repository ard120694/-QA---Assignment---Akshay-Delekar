package Pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.Assert;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

public class LoginTest {

    private WebDriver driver;

    @BeforeTest
    public void setup() {
        // Set up the webdriver (assuming we are using ChromeDriver)
        System.setProperty("webdriver.chrome.driver", "path to chromedriver");
        driver = new ChromeDriver();
    }

    @Test(priority = 1)
    public void testLoginWithValidCredentials() {
        // Navigate to the login page of the web application
        String loginUrl = "url of Login Page";
        driver.get(loginUrl);

        // Find the username, password fields, and login button by inspecting the page 
        WebElement usernameField = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for user input box")));
        WebElement passwordField = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for user password input box")));
        WebElement loginButton = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for login button")));

        // Input valid credentials
        usernameField.sendKeys("Enter Your Username");
        passwordField.sendKeys("Enter Your Password");

        // Click on the login button
        loginButton.click();

        // Wait for the dashboard page to load
        new WebDriverWait(driver, 10)
                .until(ExpectedConditions.titleContains("Dashboard"));

        // Verify that the user has successfully logged in and accessed the system
        Assert.assertTrue(driver.getTitle().contains("Dashboard"), "Login unsuccessful");
    }

 @Test(priority = 2)
    public void testLoginWithInvalidCredentials() {
        // Navigate to the login page of the web application
        String loginUrl = "url of Login Page";
        driver.get(loginUrl);

        // Find the username, password fields, and login button by inspecting the page 
        WebElement usernameField = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for user input box")));
        WebElement passwordField = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for user password input box")));
        WebElement loginButton = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for login button")));

        // Input invalid credentials
        usernameField.sendKeys("Enter Your Invalid Username");
        passwordField.sendKeys("Enter Your Invalid Password");

        // Click on the login button
        loginButton.click();

        // Wait for the error message to be displayed
        WebElement errorMessage = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for error message")));

        // Verify that an error message is displayed
        Assert.assertEquals(errorMessage.isDisplayed(), true);
    }

     @Test(priority = 3)
    public void testRetainValuesAfterFailedLogin() {
        // Navigate to the login page of the web application
        String loginUrl = "url of Login Page";
        driver.get(loginUrl);

        // Find the username, password fields, and login button by inspecting the page 
        WebElement usernameField = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for user input box")));
        WebElement passwordField = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for user password input box")));
        WebElement loginButton = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for login button")));

        // Input invalid credentials
        usernameField.sendKeys("Enter Your Invalid Username");
        passwordField.sendKeys("Enter Your Invalid Password");

        // Click on the login button
        loginButton.click();

        // Verify that the entered values are retained
        Assert.assertEquals(usernameField.getAttribute("value"), "invalid_username", "Username not retained");
        Assert.assertEquals(passwordField.getAttribute("value"), "invalid_password", "Password not retained");
    }

    @Test(priority = 4)
    public void testRetainValuesAfterFailedLogin() {
        // Navigate to the login page of the web application
        String loginUrl = "url of Login Page";
        driver.get(loginUrl);

        // Find the username, password fields, and login button by inspecting the page 
        WebElement usernameField = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for user input box")));
        WebElement passwordField = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for user password input box")));
        WebElement loginButton = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for login button")));

        // Verify that the login button is disable
        Assert.assertFalse(loginButton.isEnabled(),"Login button is Disable");

        // Input invalid credentials
        usernameField.sendKeys("Enter Your Username");
        passwordField.sendKeys("Enter Your  Password");

        // Verify that the login button is Enable
        Assert.assertEquals(loginButton.isEnabled(),"Login Button is Enabled")
    }

     @Test(priority = 5)
    public void testForgotPasswordRedirect() {
        // Navigate to the login page of the web application
        String loginUrl = "url of Login Page";
        driver.get(loginUrl);

        // Find the 'Forgot Password' link by inspecting the page
        WebElement forgotPasswordLink = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for Forgot Password link")));

        // Click on the 'Forgot Password' link
        forgotPasswordLink.click();

        // Wait for the password recovery page to load
        new WebDriverWait(driver, 10)
                .until(ExpectedConditions.titleContains("Password Recovery"));

        // Verify that the user is redirected to the password recovery page
        Assert.assertTrue(driver.getTitle().contains("Password Recovery"), "Forgot Password link");
    }

    @Test(priority = 6)
    public void testForgotPasswordRedirect() {
        // Navigate to the login page of the web application
        String loginUrl = "url of Login Page";
        driver.get(loginUrl);

        // Find the 'Forgot Password' link by inspecting the page
        WebElement forgotPasswordLink = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for Forgot Password link")));

        // Click on the 'Forgot Password' link
        forgotPasswordLink.click();

         // Wait for the password recovery page to load
        new WebDriverWait(driver, 10)
                .until(ExpectedConditions.titleContains("Password Recovery"));

        // Find the email field, recovery button, and success message elements
        WebElement emailField = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for email field")));
        WebElement recoverButton = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for recover password field]")));

        // Enter a registered email address
        emailField.sendKeys("enter your register email id");

        // Click the 'Recover Password' button
        recoverButton.click();

        // Wait for the success message to be displayed
        WebElement successMessage = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for success message")));

        // Verify that a success message is displayed
        Assert.assertEquals(successMessage.isDisplayed(), true);

        // After sending mail id we will assume that password is recovered
        // Navigate to the login page of the web application
        String loginUrl = "url of Login Page";
        driver.get(loginUrl);

        // Find the username, password fields, and login button by inspecting the page 
        WebElement usernameField = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for user input box")));
        WebElement passwordField = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for user password input box")));
        WebElement loginButton = new WebDriverWait(driver, 10)
                .until(ExpectedConditions.visibilityOfElementLocated(By.xpath("enter xpath for login button")));

        // Input invalid credentials
        usernameField.sendKeys("Enter Your Invalid Username"); c
        passwordField.sendKeys("Enter Your Invalid Password");

        // Click on the login button
        loginButton.click();
    }

    @AfterTest
    public void tearDown() {
        // Close the browser
        if (driver != null) {
            driver.quit();
        }
    }
}
