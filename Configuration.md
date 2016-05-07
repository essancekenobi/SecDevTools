BDD-Security is a standard [gradle](http://gradle.org/) project and can be imported into Java IDE's like IntelliJ, Netbeans or Eclipse.

By default, the project is configured to test the demonstration vulnerable web application described on the getting started page.  The degree of configuration changes required to test your own web application depends on which security specifications ("features") you'd like to run.

Configuration is done in two primary files:

1. config.xml
1. A Java class that contains Selenium steps to login and navigate your app (defined in the _class_ attribute in config.xml)

In addition, you can change the security requirements/specifications themselves by editing their .features files in ./src/test/resources/features/

## Select a Browser
The default Selenium browser is HtmlUnit which is a pure Java web client that uses the Rhino JS engine. This might be OK for some apps, but most JS heavy sites will need a real browser.  BDD-Security supports Chrome/Chromium and Firefox.  To select Chrome as the browser, edit config.xml and choose the Chrome driver binary that's appropriate for your platform:

    <defaultDriver path="src/test/resources/drivers/chromedriver-mac">Chrome</defaultDriver>

## Scan with OWASP ZAP
In order to properly scan an application with [OWASP ZAP](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project) the framework should be configured to login and navigate the application through Selenium steps. These steps are configured in the Java class defined in the 'class' tag in config.xml, e.g.:

    <class>net.continuumsecurity.MyComplexApplication</class>

A simple example would be:
    public class MyComplexApp extends WebApplication {

    public void navigate() {
        driver.get(Config.getInstance().getBaseUrl() + "user/login");
        UserPassCredentials creds = new UserPassCredentials(Config.getInstance().getDefaultCredentials());
        driver.findElement(By.id("username")).clear();
        driver.findElement(By.id("username")).sendKeys(creds.getUsername());
        driver.findElement(By.id("password")).clear();
        driver.findElement(By.id("password")).sendKeys(creds.getPassword());
        driver.findElement(By.name("_action_login")).click();
        
        //Click on the "tasks" link
        findAndWaitForElement(By.linkText("Tasks")).click();
        
        //Enter a search query
        driver.findElement(By.id("q")).clear();
        driver.findElement(By.id("q")).sendKeys("test");
        driver.findElement(By.id("search")).click();
    }

    }


