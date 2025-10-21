
# Lab 7: Building and Packaging Java Applications with Maven

## Prerequisites

Java JDK installed 

Maven installed

## Steps

- Install Maven


- Clone the Source Code
```bash
git clone https://github.com/Ibrahim-Adel15/build2.git
cd build2
```

- Run Unit Tests
```bash
mvn test
```

- Build the Application
```bash
mvn package
```

- This will generate the JAR file:

target/hello-ivolve-1.0-SNAPSHOT.jar


- Run the Application
```bash
java -jar target/hello-ivolve-1.0-SNAPSHOT.jar
```

- Verify Application

Open the browser or terminal output to ensure the application is running correctly.