Tests can be run directly from Gradle, through an IDE or from Continuous Integration servers like Jenkins.
Cucumber uses meta tags on the features and/or scenarios to provide some control over which get included or excluded in a test run.  BDD-Security uses the @skip tag as a convention to skip features or scenarios.

## Gradle
Gradle is configured in the build.gradle file and the default task is 'test'.  This runs a JUnit test case: net.continuumsecurity.junit.SecurityTest which in turn runs the Cucumber features.  _SecurityTest_ uses annotations to setup the default behaviour for Cucumber reporting.

To run a specific feature just specify its tag in the cucumber.options property:
    
    ./gradle -Dcucumber.options="--tags @authentication"

This will only run features or scenarios that have the @authentication tag.  This is standard Cucumber behaviour.

## Skipping Tests
- If not tags are specified in the cucumber.options property then @skip tags are skipped and all other features are run.  
- If the cucumber.options property specifies additional tags, then it should also include the '--tags ~@skip' option so that features tagged with @skip are skipped.

For example to run the 'authentication' and 'http_headers' features but to skip features with the '@skip' tag, use:

./gradle -Dcucumber.options="--tags @authentication,@http_headers --tags ~@skip"

## From IDE
Simply run the SecurityTest file as a JUnit test, and specify the cucumber.options as a system property in the run configuration.


