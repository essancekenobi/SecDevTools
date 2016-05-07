The default Gradle test task produces 3 reports:

1. [HTML Cucumber reports](http://www.continuumsecurity.net/cucumber/feature-overview.html) in build/reports/cucumber/pretty/feature-overview.html
2. JSON Cucumber results: build/reports/cucumber/all_tests.json
3. JUnit results: build/reports/junit/all_tests.xml

These locations can be changed by editing net.continuumsecurity.junit.SecurityTest or by setting cucumber.options as a system property (see Cucumber-JVM docs for more details).



