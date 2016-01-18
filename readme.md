#Parent Project to be extended by your project

##Prerequisite
*	JDK 1.8 or later
*	Chrome driver referable by /usr/webdriver/chromedriver
*	gpg tool (required for perform release)

##Provide
*	selenium integration test
	*	default web server bind address: http://localhost:80
	*	Usage:
		Put junit test case file, file ending with Test.java, in src/test/ *your* / *package* /
		
		Test Case Example:
		
			package net.gplatform.sudoor.server.test.unit;
			
			import java.util.regex.Pattern;
			import java.util.concurrent.TimeUnit;
			
			import net.gplatform.sudoor.server.Application;
			
			import org.junit.*;
			import org.junit.runner.RunWith;
			
			import static org.junit.Assert.*;
			import static org.hamcrest.CoreMatchers.*;
			
			import org.openqa.selenium.*;
			import org.openqa.selenium.chrome.ChromeDriver;
			import org.openqa.selenium.firefox.FirefoxDriver;
			import org.openqa.selenium.support.ui.Select;
			import org.springframework.boot.test.SpringApplicationConfiguration;
			import org.springframework.boot.test.WebIntegrationTest;
			import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
			
			@RunWith(SpringJUnit4ClassRunner.class)
			@SpringApplicationConfiguration(classes = Application.class)
			@WebIntegrationTest
			public class LoginITTest {
			  private WebDriver driver;
			  private String baseUrl;
			  private boolean acceptNextAlert = true;
			  private StringBuffer verificationErrors = new StringBuffer();
			
			  @Before
			  public void setUp() throws Exception {
				driver = new ChromeDriver();
				String hostname = System.getProperty("runtime.websvr.hostname");
				String port = System.getProperty("runtime.websvr.port");
				baseUrl = "http://"+hostname+":"+ port;
				driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
			  }
			
			  @Test
			  public void testLogin() throws Exception {
				driver.get(baseUrl + "/sudoor/login");
				driver.findElement(By.name("username")).clear();
				driver.findElement(By.name("username")).sendKeys("admin");
				driver.findElement(By.name("password")).clear();
				driver.findElement(By.name("password")).sendKeys("admin");
				TestUtils.takeScreenshot(driver, "LoginITTest/loginPage.png");
				driver.findElement(By.name("submit")).click();
				TestUtils.takeScreenshot(driver, "LoginITTest/successPage.png");
			  }
			
			  @After
			  public void tearDown() throws Exception {
				driver.quit();
				String verificationErrorString = verificationErrors.toString();
				if (!"".equals(verificationErrorString)) {
				  fail(verificationErrorString);
				}
			  }
			
			  private boolean isElementPresent(By by) {
				try {
				  driver.findElement(by);
				  return true;
				} catch (NoSuchElementException e) {
				  return false;
				}
			  }
			
			  private boolean isAlertPresent() {
				try {
				  driver.switchTo().alert();
				  return true;
				} catch (NoAlertPresentException e) {
				  return false;
				}
			  }
			
			  private String closeAlertAndGetItsText() {
				try {
				  Alert alert = driver.switchTo().alert();
				  String alertText = alert.getText();
				  if (acceptNextAlert) {
					alert.accept();
				  } else {
					alert.dismiss();
				  }
				  return alertText;
				} finally {
				  acceptNextAlert = true;
				}
			  }
			}


*	jmeter performance test
	Usage:
	Put your jmeter test case file, file ending with .jmx, in src/test/jmeter
	Run: `mvn install -P test.performance`

*	release via maven-release-plugin
	Usage:
	prepare release(change version, apply label...):
	`mvn release:prepare -Dusername=xxx -Dpassword=xxx`
	perform release(push artifact to oss):
	`mvn release:perform`

*	repositories definition
	https://oss.sonatype.org/content/repositories/snapshots
	https://oss.sonatype.org/content/repositories/staging
	
*	distribution repositories definition
	https://oss.sonatype.org/service/local/staging/deploy/maven2
	https://oss.sonatype.org/content/repositories/snapshots