# NewWorkflow
create a new file 
package com.libraries;

import org.openqa.selenium.WebDriver;
import org.testng.ITestResult;
import org.testng.annotations.AfterClass;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.BeforeMethod;

import com.libraries.GlobalSelenium.Browser;

public class Base {
	public WebDriver driver;
	public GlobalSelenium myLibraryGS = new GlobalSelenium();

	@BeforeClass
	public void beforeAllTest() {
		System.out.println("running before all tests.");

	}

	// this method will run only one time right after all tests/methods
	@AfterClass
	public void afterAllTest() {
		System.out.println("running after all tests.");
	}

	@BeforeMethod
	public void setUp() {

		//driver = myLibraryGS.startABrowser(Browser.FIREFOX);
		driver = myLibraryGS.startABrowser(Browser.CHROME);
	}

	@AfterMethod
	public void tearDown(ITestResult result) {
		if(ITestResult.FAILURE == result.getStatus()) {
			myLibraryGS.takeScreenshot(result.getName());
		}
		myLibraryGS.tearDown();
	}

}
