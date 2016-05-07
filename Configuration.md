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
Scanning is run through the ./src/test/resources/features/app_scan.feature

In order to properly scan an application with [OWASP ZAP](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project) the framework should be configured to login and navigate the application through Selenium steps. These steps are configured in the Java class defined in the 'class' tag in config.xml, e.g.:

    <class>net.continuumsecurity.MyComplexApp</class>

A simple example class should extend the **WebApplication** class and implement the **Navigable** interface:

        public class MyComplexApp extends WebApplication implements INavigable {

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

The Selenium "driver" instance is automatically configured by the parent WebApplication class.  Notice the references to Config.getInstance(), which are used to read values from the config file.  For the method above, we'll need to configure the _baseUrl_ (ending with a slash):

    <baseUrl>http://www.example.com/</baseUrl>

And the default login credentials:

    <defaultUsername>bob</defaultUsername>
    <defaultPassword>password</defaultPassword>

With that done, we can launch the ZAP scanning tests:

    ./gradlew -Dcucumber.options="--tags @app_scan --tags ~@skip" test

## Testing SSL

Install the SSLyze package and point config.xml to it:

     <sslyze>
        <path>/opt/sslyze/sslyze_cli.py</path>
        <option>--regular</option>
     </sslyze>

And run the SSL tests:

    ./gradlew -Dcucumber.options="--tags @ssl" test

## Testing Authentication and Session Management

Specific interfaces need to be implemented to test these features: **ILogin** and **ILogout**
See the RopeyTasksApplication.java file for an example of how to implement these.



