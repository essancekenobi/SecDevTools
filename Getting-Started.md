# Prerequisites

JDK 8

## Run the Demo
### Download a vulnerable web application
BDD-Security tests web applications and servers from the outside. To get started with a quick demonstration, we provide a vulnerable web application in the form of a self-executing .jar file from [here.](https://github.com/continuumsecurity/RopeyTasks/blob/master/ropeytasks.jar)

Launch this application in a terminal:
     java -jar ropeytasks.jar

### Checkout BDD-Security

     git clone https://github.com/continuumsecurity/RopeyTasks.git

Execute the 'authentication' specification:

    ./gradlew -Dcucumber.options="--tags @authentication --tags ~@skip" test

The framework    
    
    
