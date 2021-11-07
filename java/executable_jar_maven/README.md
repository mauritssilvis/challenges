# Challenges > Java > Creating an executable JAR using Maven

> A Maven project that creates an executable JAR

## Introduction

With this part of the [Challenges](https://github.com/mauritssilvis/challenges) project, I provide the code and settings for a Maven project that can create an executable JAR.

Below, I give a brief [overview](#1-background) of the project's [code](#11-code), the used [Maven configuration](#12-maven) and the available [IntelliJ IDEA run configurations](#13-intellij-idea).
I also detail some [issues](#2-issues-and-solutions) that can occur when creating an executable JAR using Maven, and I provide possible solutions to these issues.

A description of Maven and IntelliJ IDEA, their configuration, and several problems that may occur when setting up a Maven project can be found in [Setting up a basic Maven project using IntelliJ IDEA](../basic_maven_project_intellij_idea).

## 1. Background

### 1.1 Code

For demonstrative purposes, the current project contains only a single Java class called `Main`, which consists of a `main` method outputting a well-known message:

```java
public class Main {
  public static void main(String[] args) {
    System.out.println("Hello world!");
  }
}
```

### 1.2 Maven

This project is managed and built using [Maven](../basic_maven_project_intellij_idea#12-maven).

#### 1.2.1 Configuration

To ensure that the JAR created by Maven is executable, the [project object model](../basic_maven_project_intellij_idea#121-project-object-model) of the current project, [pom.xml](pom.xml), contains the following configuration for the [Maven JAR plugin](https://maven.apache.org/plugins/maven-jar-plugin/):

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
                nl.mauritssilvis.challenges.maven.jar.executable.standalone.Main
              </mainClass>
            </manifest>
          </archive>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

Here, the latest version of the [Maven JAR plugin](https://maven.apache.org/plugins/maven-jar-plugin/) (currently 3.2.0) was selected.

#### 1.2.2 Build

The JAR can be built using the command

```shell
$ mvn clean install
```

### 1.3 IntelliJ IDEA run configurations

The project comes with two run configuration, one for creating and one for executing the resulting JAR.

## 2. Issues and solutions

While setting up and building a Maven project, several problems may occur, which are partly documented under [Setting up a basic Maven project using IntelliJ IDEA](../basic_maven_project_intellij_idea).
An additional problem may occur when trying to execute a JAR created using Maven.
I describe this problem, here, including a possible solution.

### 2.1 Maven JAR plugin issues

At least one issue may be reported by the [Maven JAR plugin](https://maven.apache.org/plugins/maven-jar-plugin/).

#### 2.1.1 no main manifest attribute, in standalone-1.0-SNAPSHOT.jar

When trying to execute a JAR, the following error may occur:

```text
no main manifest attribute, in standalone-1.0-SNAPSHOT.jar
```

To solve this problem, configure the Maven JAR plugin in the Maven project object model, `pom.xml`, in such a way that it specifies the class with which execution has to start.
For the current project, this looks as follows:

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
                nl.mauritssilvis.challenges.maven.jar.executable.standalone.Main
              </mainClass>
            </manifest>
          </archive>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

Here, the latest version of the [Maven JAR plugin](https://maven.apache.org/plugins/maven-jar-plugin/) (currently 3.2.0) was selected.

## License

Copyright © 2021 Maurits H. Silvis

This source code package is subject to the terms and conditions defined in the GNU General Public License v3.0, which can be found in the file [LICENSE.md](../../LICENSE.md), or later.
