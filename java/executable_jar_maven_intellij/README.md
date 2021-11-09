# Challenges > Java > Creating an executable JAR using Maven

> A Maven project that creates an executable JAR

## Introduction

With this part of the [Challenges](https://github.com/mauritssilvis/challenges) project, I provide the code and settings for a Maven project that can create an executable JAR.

Below, I give a brief [overview](#1-background) of the project's [code](#11-code), the used [Maven configuration](#12-maven) and the available [IntelliJ IDEA run configurations](#13-intellij-idea).
I also detail some [issues](#2-issues-and-solutions) that can occur when creating an executable JAR using Maven, and I provide possible solutions to these issues.

A description of Maven and IntelliJ IDEA, their configuration, and problems that may occur when setting up a basic Maven project can be found in [Setting up a basic Maven project using IntelliJ IDEA](../basic_maven_project_intellij).

## 1. Background

### 1.1 Code

For demonstrative purposes, the current project contains only a single Java class called `Main`, which consists of a `main` method outputting a well-known message:

```java
package nl.mauritssilvis.challenges.java.intellij.maven.jars.executable.standalone;

public class Main {
  public static void main(String[] args) {
    System.out.println("Hello world!");
  }
}
```

### 1.2 Maven

This Java project is managed and built using [Maven](https://maven.apache.org/).
A brief overview of the basic Maven project details is given in the [Maven](../basic_maven_project_intellij#12-maven) section of [Setting up a basic Maven project using IntelliJ IDEA](../basic_maven_project_intellij).

#### 1.2.1 Configuration

To ensure that the JAR created by Maven is executable, the project object model of the current project, [pom.xml](pom.xml), contains the following configuration for the [Maven JAR plugin](https://maven.apache.org/plugins/maven-jar-plugin/):

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <version>3.2.0</version>
        <configuration>
          <archive>
            <manifest>
              <mainClass>
                nl.mauritssilvis.challenges.java.intellij.maven.jars.executable.standalone.Main
              </mainClass>
            </manifest>
          </archive>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

Here, the latest version of the [Maven JAR plugin](https://maven.apache.org/plugins/maven-jar-plugin/) (currently 3.2.0) is selected and the main class is defined as

```text
nl.mauritssilvis.challenges.java.intellij.maven.jars.executable.standalone.Main
```

#### 1.2.2 Build

The executable JAR can be built using the command

```shell
$ mvn clean install
```

### 1.3 IntelliJ IDEA

This project is set up using [IntelliJ IDEA](https://www.jetbrains.com/idea/).
A brief overview of the IntelliJ IDEA project basics is given in the [IntelliJ IDEA](../basic_maven_project_intellij#13-intellij-idea) section of [Setting up a basic Maven project using IntelliJ IDEA](../basic_maven_project_intellij).

#### 1.3.1 Run configurations

The project comes with two run configuration, one for creating and one for executing the resulting JAR.

## 2. Issues and solutions

While setting up and building a Maven project, several problems may occur.
I partly documented these problems in the [Issues and solutions](../basic_maven_project_intellij#2-issues-and-solutions) section of [Setting up a basic Maven project using IntelliJ IDEA](../basic_maven_project_intellij).

Additional problems may occur when trying to execute a JAR created using Maven.
I describe the problems related to the [Maven JAR plugin](#21-maven-jar-plugin-issues), including possible solutions.

### 2.1 Maven JAR plugin issues

Several issues may arise in relation to the [Maven JAR plugin](https://maven.apache.org/plugins/maven-jar-plugin/).

#### 2.1.1 no main manifest attribute, in standalone-1.0-SNAPSHOT.jar

When trying to execute a JAR, an error similar to the following may occur:

```text
no main manifest attribute, in standalone-1.0-SNAPSHOT.jar
```

To solve this problem, use the `build` section of the project object model, `pom.xml`, to configure the Maven JAR plugin.
Specifically, set the main class property to the fully qualified name of the class with which execution has to start.

For the current project, the `build` section of `pom.xml` contains the following directives:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <version>3.2.0</version>
        <configuration>
          <archive>
            <manifest>
              <mainClass>
                nl.mauritssilvis.challenges.java.intellij.maven.jars.executable.standalone.Main
              </mainClass>
            </manifest>
          </archive>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

Here, the latest version of the [Maven JAR plugin](https://maven.apache.org/plugins/maven-jar-plugin/) (currently 3.2.0) is selected and the main class is specified as

```text
nl.mauritssilvis.challenges.java.intellij.maven.jars.executable.standalone.Main
```

#### 2.1.2 Could not find or load main class

When trying to execute a JAR, an error similar to the following may occur:

```text
Error: Could not find or load main class nl.mauritssilvis.challenges.java.intellij.maven.jars.executable.standalone.NonExisting
Caused by: java.lang.ClassNotFoundException: nl.mauritssilvis.challenges.java.intellij.maven.jars.executable.standalone.NonExisting
```

Such an error is caused by a faulty specification of the main class of your project.

To solve this problem, ensure that the Maven JAR plugin is properly configured in the `build` section of the project object model, `pom.xml`.
In particular, set the main class property to the proper fully qualified path of the class with which execution has to start.

For the current project, the configuration of the Maven JAR plugin looks as follows:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <version>3.2.0</version>
        <configuration>
          <archive>
            <manifest>
              <mainClass>
                nl.mauritssilvis.challenges.java.intellij.maven.jars.executable.standalone.Main
              </mainClass>
            </manifest>
          </archive>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

Here, the latest version of the [Maven JAR plugin](https://maven.apache.org/plugins/maven-jar-plugin/) (currently 3.2.0) is selected and the main class is specified as

```text
nl.mauritssilvis.challenges.java.intellij.maven.jars.executable.standalone.Main
```

#### 2.1.3 Main method not found in class

When trying to execute a JAR, an error similar to the following may occur:

```text
Error: Main method not found in class nl.mauritssilvis.challenges.java.intellij.maven.jars.executable.standalone.Main, please define the main method as:
   public static void main(String[] args)
or a JavaFX application class must extend javafx.application.Application
```

This error arises when the main class of your project doesn't contain a proper main method.

To solve this problem, ensure that the main class of your project contains a method with the signature

```java
public static void main(String[] args) {
  // ...
}
```

For the current project, the configuration of the Maven JAR plugin that is part of the `build` section of the project object model, `pom.xml`, looks as follows:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <version>3.2.0</version>
        <configuration>
          <archive>
            <manifest>
              <mainClass>
                nl.mauritssilvis.challenges.java.intellij.maven.jars.executable.standalone.Main
              </mainClass>
            </manifest>
          </archive>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

Here, the latest version of the [Maven JAR plugin](https://maven.apache.org/plugins/maven-jar-plugin/) (currently 3.2.0) is selected and the main class is defined as

```text
nl.mauritssilvis.challenges.java.intellij.maven.jars.executable.standalone.Main
```

This main class contains has a main method with a recognized signature:

```java
package nl.mauritssilvis.challenges.java.intellij.maven.jars.executable.standalone;

public class Main {
  public static void main(String[] args) {
    System.out.println("Hello world!");
  }
}
```

## License

Copyright © 2021 Maurits H. Silvis

This source code package is subject to the terms and conditions defined in the GNU General Public License v3.0, which can be found in the file [LICENSE.md](../../LICENSE.md), or later.
