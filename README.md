
# First Part: Test Design

Note: The following HLS is for Android platform, it concerns only the main features of **monefy** app as there are many features are exclusive for pro users.


| Module | Positive Scenario | Negative Scenario | Priority |
| :------: | :-----------------: | :-----------------: | :------: |
|Onboarding screen|Check app behaviour when user open the app for the first time/Clear data from the app| |high|
||
|Onboarding screen|Check app behaviour when user click 'INCOME' button once| | high|
|Onboarding screen|Check app behaviour when user hold on any button of expense icons|| medium |
|Onboarding screen|Check the spendings distribution on the chart meets the actual expenses the user entered in the app | | medium |
|Onboarding screen|Check app behaviour when user try to click 'Expenses' button multiple times | | low |
|Onboarding screen|Check the spendings chart icons and it's UI elements are visible and not deformed while the testing device on dark mode| || medium |
|Onboarding scree|Check the mentioned screen match the design|| low |
|New income screen|Check app behaviour when user add more than one income at the same category ||medium|
|New income screen|Check app behaviour when user add the income as calculated formula instead of direct integer||medium|
|New income screen|| Check app behaviour when user try to add empty/0 as income |low|
|New expense screen||Check app behaviour when user try to add new expense while the mobile network is off|low|
|Balance screen|Check app behaviour when user delete existing income from a category that has more than one listed income||medium|
|Balance screen|Check app behaviour when user edit 'Note' section in existing salary||medium|
|New transfer|Check app behaviour when user try to transfer amount of money that exceed the amount which is in the transfer account ||medium|
|New transfer||Check app behaviour when user try to perform a transformation process and got interrupted with a call on the same device  while he's in the middle of the process |low|
|Accounts|Check app behaviour when user try to add a new account with an arabic name||medium|
|Settings|Check app behaviour when user check on 'budget mode' option with a setted budget to 1000||High|
|Settings|Check app behaviour when user app language to 'Francais'||High|


# Second Part: Bug Reporting

1. [Reported bugs can be found in here](https://docs.google.com/spreadsheets/d/14LDf9zIIzDn2MJi2Ybu3JkGJM5PO4ymIUHrb8YNBz0U/edit#gid=0)

## UX issues and Suggested improvements:

### Issues:
1. About the app page is deformed (written in different font size).

###  Improvements:
1- Budget should be monthly based (it's no use to have the same budget applied every month) or at least it can be optional to choose.<br/>
2. App needs better iconography for category section.<br/>
3. App needs to support Arabic to be applied as a main language for the app.<br/>
4. There should be helping instructions for the main features in the app, for current version the most instructions appear only on the main page.<br/>

# Third Part: Test Automation

## List of suggested test cases for search function of NAS Trends website.

1. [List can be found here](https://docs.google.com/spreadsheets/d/14LDf9zIIzDn2MJi2Ybu3JkGJM5PO4ymIUHrb8YNBz0U/edit#gid=607730443)

## Automated script for Test case ID #7

```java
code
package WorkingWithElements;
import org.openqa.selenium.By;
import org.openqa.selenium.By.ByClassName;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import static org.testng.Assert.assertNotNull;

import java.util.concurrent.TimeUnit;

public class WorkingWithWebElements {
	
	FirefoxDriver TheDriver;

	@BeforeTest
	public void OpenURL ()
	{	
		System.setProperty("webdriver.gecko.driver", System.getProperty("user.dir")+"\\Resources\\geckodriver.exe");
		TheDriver = new FirefoxDriver();
		TheDriver.navigate().to("https://www.nastrends.com/");
		TheDriver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);

	}
	
	@Test
	public void NasSearch ()
	{
		WebElement SearchIcon = TheDriver.findElement(By.className("fa fa-search fa-2x"));
		SearchIcon.click();	
		TheDriver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);

		WebElement SearchBar = TheDriver.findElement(By.className("search-input"));
		SearchBar.sendKeys("I Feel Great");
		SearchIcon.click();	
		
		WebElement Check = TheDriver.findElementByLinkText("I Feel Great");
		
		assertNotNull(Check);
		
	}

		@AfterTest
		public void CloseDriver ()
		{
			TheDriver.quit();
		}
}
```
