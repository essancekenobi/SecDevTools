Since Cucumber produces JUnit output, BDD-Security can be run and the results used by Jenkins without any additional plugins.

## Minimal Configuration
Use a Gradle build task and set Cucumber options in the 'Tasks' section, e.g.:

    -Dcucumber.options="--tags @authentication,@http_headers --tags ~@skip"

Add a _Post-Build Action_ to publish JUnit test results and set the _Test report XMLs_ to: build/reports/junit/*.xml 

## Better reporting
There are at least two HTML reporting plugins that can be used with Cucumber to produce good looking and easily navigable reports:

1. [Cucumber-JVM reports](https://github.com/jenkinsci/cucumber-reports-plugin)
2. [Bootstrap multi-test results report](https://wiki.jenkins-ci.org/display/JENKINS/Bootstraped+Multi+Test+Results+Report)

### Cucumber-JVM Reports
Add a _Post-Build Action_ and set the JSON reports path to: build/reports

### Bootstrap multi-test results report
Add a _Post-Build Action_ and set the JSON reports path to: build/reports

