# Setting up a Java project using Maven and IntelliJ IDEA

> A Java project set up using Maven and IntelliJ IDEA

## Introduction

With this part of the [Java challenges](..) project, I provide the code and settings for a Java project set up using Maven and IntelliJ IDEA.

Below, I give detailed [background information](#1-background) on the project’s [code](#11-java), [IntelliJ IDEA’s configuration](#12-intellij-idea) and the used [Maven configuration](#13-maven).
I also describe several [issues](#2-issues-and-solutions) that can occur when setting up a Maven project, for which I provide possible solutions.

This project builds on [Setting up a Java project using IntelliJ IDEA](../java-project-intellij).

## 1. Background

### 1.1 Java

#### 1.1.1 Code

For demonstrative purposes, the current project contains only a single Java class called `Main`, which consists of a `main` method outputting a well-known message:

```java
package nl.mauritssilvis.challenges.java.intellij.maven.projects.basic;

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello world!");
    }
}
```

### 1.2 IntelliJ IDEA

The basic configuration of this project is described in the [IntelliJ IDEA section](../java-project-intellij/#12-intellij-idea) of [Setting up a Java project using IntelliJ IDEA](../java-project-intellij).
Additional details regarding the IntelliJ IDEA run configurations of the current project are given in what follows.

#### 1.2.1 Configuration

##### Run configurations

This project comes with three run configurations.
This first run configuration is called `Main` and directly executes the `main` method of the `Main` class.
The other two run configurations, respectively, create a JAR and execute it.
Note that execution of the JAR [fails](#24-maven-jar-plugin-issues).

### 1.3 Maven

This Java project is managed and built using Maven (see, e.g., the [Maven section](../#24-maven) of the [Java challenges](..) project).

The Maven configuration of the current project is detailed in what follows.

#### 1.3.1 Configuration

##### Project coordinates

In the project object model of the current project, [pom.xml](pom.xml), the so-called project coordinates are set as follows:

```xml
<project>
  <groupId>nl.mauritssilvis.challenges.java.intellij.maven.projects</groupId>
  <artifactId>java-project-maven-intellij</artifactId>
  <version>1.0-SNAPSHOT</version>
</project>
```

##### Encoding

The encoding of the source files is set to UTF-8:

```xml
<project>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
</project>
```

##### Maven compiler plugin

Finally, the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) is configured as follows:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
        <configuration>
          <source>21</source>
          <target>21</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

Here, version 3.11.0 of the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) is selected, which is the latest version at the time of writing.
Additionally, Java 21 is selected, which is the latest long-term support (LTS) version of Java at the time of writing.

#### 1.3.2 Build

The project can be built using the following command:

```shell
mvn clean package
```

Execution of this command cleans the build folder, compiles the above-mentioned Java class file and packages it as a JAR file.

Alternatively, execute the following command:

```shell
mvn clean install
```

In addition to the previous command, this command makes the JAR available in your local Maven repository.
Note that the JAR is [not executable](#24-maven-jar-plugin-issues).

## 2. Issues and solutions

While setting up and building a Maven project, several issues may occur.
I list several such issues below, including possible solutions.
Specifically, I discuss problems related to the [project object model](#21-project-object-model-issues), the [Maven resources plugin](#22-maven-resources-plugin-issues), the [Maven compiler plugin](#23-maven-compiler-plugin-issues) and the [Maven JAR plugin](#24-maven-jar-plugin-issues).

<!-- TODO: Describe what happens when the required Java version is not installed. -->

### 2.1 Project object model issues

Several issues may arise concerning the [project object model](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html).

#### 2.1.1 The goal you specified requires a project to execute but there is no POM in this directory

When executing Maven goals, the following error may occur:

```text
[ERROR] The goal you specified requires a project to execute but there is no POM in this directory ... Please verify you invoked Maven from the correct directory.
```

To solve this problem, ensure the project’s top-level directory contains a project object model file called `pom.xml` and that Maven is run in this directory.

#### 2.1.2 Non-readable POM: input contained no data

When executing Maven goals, the following error may occur:

```text
[ERROR] Some problems were encountered while processing the POMs:
[FATAL] Non-readable POM ...: input contained no data
```

To solve this problem, ensure the project object model, `pom.xml`, contains at least the `project` root element.
This root element can be included without any attributes:

```xml
<project></project>
```

Alternatively, specify the optional XML preamble and namespace information:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
</project>
```

#### 2.1.3 'modelVersion' is missing

When executing Maven goals, the following error may occur:

```text
[ERROR] Some problems were encountered while processing the POMs:
[ERROR] 'modelVersion' is missing. @ line 1, column 10
```

To solve this problem, set the model version in the project object model, `pom.xml`:

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
</project>
```

#### 2.1.4 'groupId' is missing / 'artifactId' is missing / 'version' is missing

When executing Maven goals, one or more of the following errors may occur:

```text
[ERROR] Some problems were encountered while processing the POMs:
[FATAL] 'groupId' is missing. @ line 1, column 10
[FATAL] 'artifactId' is missing. @ line 1, column 10
[FATAL] 'version' is missing. @ line 1, column 10
```

To solve these problems, include the project coordinates, i.e., the group ID, the ID and the version of the artifact, in the project object model, `pom.xml`.

For the current project, these coordinates are defined by the following elements:

```xml
<project>
  <groupId>nl.mauritssilvis.challenges.java.intellij.maven.projects</groupId>
  <artifactId>java-project-maven-intellij</artifactId>
  <version>1.0-SNAPSHOT</version>
</project>
```

#### 2.1.5 'build.plugins.plugin.(groupId:artifactId)' artifactId of a plugin must be defined

When executing Maven goals, the following error may occur:

```text
[ERROR] Some problems were encountered while processing the POMs:
[FATAL] 'build.plugins.plugin.(groupId:artifactId)' artifactId of a plugin must be defined.  @ line 10, column 21
```

To solve this problem, ensure all desired Maven plugins are identified using their artifact ID.

For example, the Maven compiler plugin can be selected with the following `build` section of `pom.xml`:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
</project>
```

#### 2.1.6 'build.plugins.plugin.version' for org.apache.maven.plugins:maven-compiler-plugin is missing

When using Maven plugins, a warning may be shown that is similar to the following:

```text
[WARNING] Some problems were encountered while building the effective model for nl.mauritssilvis.challenges.java.intellij.maven.projects:java-project-maven-intellij:jar:1.0-SNAPSHOT
[WARNING] 'build.plugins.plugin.version' for org.apache.maven.plugins:maven-compiler-plugin is missing. @ line 9, column 21
[WARNING]
[WARNING] It is highly recommended to fix these problems because they threaten the stability of your build.
[WARNING]
[WARNING] For this reason, future Maven versions might no longer support building such malformed projects.
```

To prevent this warning and potential future problems with your project, select the latest Maven plugin version in the project object model, `pom.xml`.

For example, for the Maven compiler plugin, extend the `build` section of `pom.xml` with the following elements:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
      </plugin>
    </plugins>
  </build>
</project>
```

Here, version 3.11.0 of the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) is selected, which is the latest version at the time of writing.

### 2.2 Maven resources plugin issues

The [Maven resources plugin](http://maven.apache.org/plugins/maven-resources-plugin/) may report at least one issue.

#### 2.2.1 Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!

The Maven resources plugin may throw a warning of the following form:

```text
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
```

This warning indicates that no encoding has been set for the project files, i.e., for the source and resource files of the project.

To set the file encoding to UTF-8, include the following line in the `properties` section of the project object model, `pom.xml`:

```xml
<project>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
</project>
```

### 2.3 Maven compiler plugin issues

The [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) may report several issues.

#### 2.3.1 File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!

Similar to the Maven resources plugin, the Maven compiler plugin may return the following warning:

```text
[WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
```

This warning indicates that no encoding has been set for the project files, i.e., for the source and resource files of the project.

To set the file encoding to UTF-8, include the following line in the `properties` section in the project object model, `pom.xml`:

```xml
<project>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
</project>
```

#### 2.3.2 Source value 7 is obsolete and will be removed in a future release / Target value 7 is obsolete and will be removed in a future release

The Maven compiler plugin may return the following warnings:

```text
[WARNING] source value 7 is obsolete and will be removed in a future release
[WARNING] target value 7 is obsolete and will be removed in a future release
```

To solve these warnings, ensure the Java source and target versions are explicitly set in the project object model, `pom.xml`, and are higher than 7.
Additionally, ensure that the target version is not smaller than the source version.

Java 21 can be selected by extending the `properties` section of `pom.xml` with the following lines:

```xml
<project>
  <properties>
    <maven.compiler.source>21</maven.compiler.source>
    <maven.compiler.target>21</maven.compiler.target>
  </properties>
</project>
```

In addition, select the latest version of the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) (3.11.0 at the time of writing) in the `build` section of `pom.xml`:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
      </plugin>
    </plugins>
  </build>
</project>
```

Alternatively, configure the Java target, source and Maven compiler plugin versions in the `build` section:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
        <configuration>
          <source>21</source>
          <target>21</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

#### 2.3.3 Source option is no longer supported. Use 8 or later.

The Maven compiler plugin may halt with one of the following errors:

```text
[ERROR] Source option 1.3 is no longer supported. Use 8 or later.
```

```text
[ERROR] Source option 5 is no longer supported. Use 8 or later.
```

```text
[ERROR] Source option 6 is no longer supported. Use 8 or later.
```

To solve these problems, explicitly set the Java source version in the project object model, `pom.xml`.

The source version can be set to Java 21 by extending the `properties` section of `pom.xml` with the following line:

```xml
<project>
  <properties>
    <maven.compiler.source>21</maven.compiler.source>
  </properties>
</project>
```

In addition, select the latest version of the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) (3.11.0 at the time of writing) in the `build` section of `pom.xml`:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
      </plugin>
    </plugins>
  </build>
</project>
```

Alternatively, configure both the Java source and Maven compiler plugin versions in the `build` section:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
        <configuration>
          <source>21</source>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

#### 2.3.4 Target option is no longer supported. Use 8 or later.

The Maven compiler plugin may halt with one of the following errors:

```text
[ERROR] Target option 1.1 is no longer supported. Use 8 or later.
```

```text
[ERROR] Target option 5 is no longer supported. Use 8 or later.
```

```text
[ERROR] Target option 6 is no longer supported. Use 8 or later.
```

To solve these problems, explicitly set the Java target version in the project object model, `pom.xml`.

The target version can be set to Java 21 by extending the `properties` section of `pom.xml` with the following line:

```xml
<project>
  <properties>
    <maven.compiler.target>21</maven.compiler.target>
  </properties>
</project>
```

In addition, select the latest version of the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) (3.11.0 at the time of writing) in the `build` section of `pom.xml`:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
      </plugin>
    </plugins>
  </build>
</project>
```

Alternatively, configure both the Java target and Maven compiler plugin versions in the `build` section:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
        <configuration>
          <target>21</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

#### 2.3.5 Source release 21 requires target release 21

The Maven compiler plugin may encounter the following error while compiling:

```text
[ERROR] source release 21 requires target release 21
```

To solve these problems, ensure the Java source and target versions are set in the project object model, `pom.xml`.
Additionally, ensure that the target version is not smaller than the source version.

Java 21 can be selected by extending the `properties` section of `pom.xml` with the following lines:

```xml
<project>
  <properties>
    <maven.compiler.source>21</maven.compiler.source>
    <maven.compiler.target>21</maven.compiler.target>
  </properties>
</project>
```

In addition, select the latest version of the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) (3.11.0 at the time of writing) in the `build` section of `pom.xml`:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
      </plugin>
    </plugins>
  </build>
</project>
```

Alternatively, configure the Java target, source and Maven compiler plugin versions in the `build` section:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
        <configuration>
          <source>21</source>
          <target>21</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

### 2.4 Maven JAR plugin issues

At least one issue may arise with the [Maven JAR plugin](https://maven.apache.org/plugins/maven-jar-plugin/).

#### 2.4.1 no main manifest attribute, in java-project-maven-intellij-1.0-SNAPSHOT.jar

When trying to execute a JAR, an error similar to the following may occur:

```text
no main manifest attribute, in java-project-maven-intellij-1.0-SNAPSHOT.jar
```

To solve this problem, configure the Maven JAR plugin according to the discussion of potential [Maven JAR plugin issues](../executable-jar-maven-intellij/#21-maven-jar-plugin-issues) that is part of [Creating an executable JAR using Maven and IntelliJ IDEA](../executable-jar-maven-intellij).

## License

Copyright © 2021–2023 Maurits Silvis

This source code package is subject to the terms and conditions defined in the [GNU General Public License v3.0](../../LICENSE.md) or later.
