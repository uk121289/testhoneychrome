# testhoneychrome
package honeytest;
import java.io.File;
import java.util.List;
import java.util.Set;
import java.util.concurrent.TimeUnit;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.By;
import org.openqa.selenium.By.ByName;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.openqa.selenium.support.ui.Select;
import org.openqa.selenium.WebDriver.Options;

public class creatingdriver {
	public static void main(String[] args) throws Exception   {
  // Set the path to your ChromeDriver executable
        System.setProperty("webdrive.chrome.driver", "C:\\Users\\hey_p\\OneDrive\\maven_project\\workspace\\extentiontesting\\target\\ChromeSetup.exe");
// Create ChromeOptions instance
        ChromeOptions options = new ChromeOptions();
      //  options.addArguments("--incognito");
 // Add the extension to ChromeOptions
        System.out.println("Opening extension");
        options.addExtensions(new File("C:\\Users\\hey_p\\OneDrive\\maven_project\\workspace\\extentiontesting\\target\\honeychrome.crx"));
        WebDriver driver=new ChromeDriver(options);
        driver.manage().window().maximize();
        driver.get("https://www.myer.com.au/");
        Thread.sleep(10000); // wait
 //handle extension unwanted tab
        String originalHandle = driver.getWindowHandle();
        Set<String> allHandles = driver.getWindowHandles();
       	        for (String handle : allHandles) {
            if (!handle.equals(originalHandle)) {
                driver.switchTo().window(handle);         
                driver.close(); 
                       }
                    }
  	     System.out.println("Extension added to chrome");
        driver.switchTo().window(originalHandle); 
//Click on Sign in
   driver.findElement(By.xpath("//*[@id=\"radix-:r0:\"]/p")).click();//
   driver.findElement(By.xpath("//*[@id=\"radix-:r1:\"]/div/div/div/p[1]/a")).click();
// pass credentials
  driver.findElement(By.name("username")).sendKeys("test@testmail.com");
  driver.findElement(By.name("password")).sendKeys("ABC1232@7lo");
  driver.findElement(By.xpath("//*[@id=\"mw-ulp-login-widget-container\"]/main/section/div/div/div/form/div[2]/button")).click();
  System.out.println("logged in to page");
//navigate to HOME
  driver.findElement(By.xpath("/html[1]/body[1]/div[1]/main[1]/header[1]/div[2]/nav[1]/ul[1]/li[5]/button[1]/span[1]")).click();
  System.out.println("navigated to HOME tab");
// navigate to coffee machine tab
  driver.findElement(By.xpath("/html[1]/body[1]/div[1]/main[1]/header[1]/div[2]/nav[1]/div[2]/div[1]/div[2]/ul[2]/li[2]/a[1]")).click();
   System.out.println("coffe machine selected");
  driver.findElement(By.xpath("//*[@id=\"165916360\"]/div/div[1]/a/div[2]/p[2]")).click();
  System.out.println("machine added to cart");
  
    System.out.println("honey chrome extentioin displayed on page");

 }
}
