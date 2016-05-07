BDD-Security is a standard [gradle](http://gradle.org/) project and can be imported into Java IDE's like IntelliJ, Netbeans or Eclipse.

By default, the project is configured to test the demonstration vulnerable web application described on the getting started page.  The degree of configuration changes required to test your own web application depends on which security specifications ("features") you'd like to run.

Configuration is done in two primary files:

1. config.xml
1. A Java class that contains Selenium steps to login and navigate your app (defined in the _class_ attribute in config.xml)

In addition, you can change the security requirements/specifications themselves by editing their .features files in ./src/test/resources/features/

