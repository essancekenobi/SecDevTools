# Prerequisites

1. JDK 8
1. (Optional) to test SSL, install [SSLyze](https://github.com/nabla-c0d3/sslyze)
1. (Optional) to run tests with Nessus you'll need a Nessus server with the API enabled

## Run the Demo
### Download a vulnerable web application
BDD-Security tests web applications and servers from the outside. To get started with a quick demonstration, we provide a vulnerable web application in the form of a self-executing .jar file from [here.](https://github.com/continuumsecurity/RopeyTasks/blob/master/ropeytasks.jar)

Launch this application in a terminal:

     java -jar ropeytasks.jar

### Checkout BDD-Security

     git clone https://github.com/continuumsecurity/RopeyTasks.git

Execute only the 'authentication' feature:

    ./gradlew -Dcucumber.options="--tags @authentication --tags ~@skip"

View the test results in ./build/reports/cucumber/pretty/feature-overview.html    
To execute all the features including ZAP scanning:

    ./gradlew


