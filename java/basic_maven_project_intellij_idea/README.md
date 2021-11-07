# Challenges > Java > Setting up a basic Maven project using IntelliJ IDEA

> A basic Maven project, set up using IntelliJ IDEA

## Introduction

With this part of the [Challenges](https://github.com/mauritssilvis/challenges) project, I provide the code and settings for a basic Java project, managed using Maven and set up using IntelliJ IDEA.

Below, I give an [overview](#1-background) of the project's [code](#11-code), the two tools used, namely, [Maven](#12-maven) and [IntelliJ IDEA](#13-intellij-idea), and their configuration.
I also detail several [issues](#2-issues-and-solutions) that can occur when setting up a Maven project, and I provide possible solutions to these issues. 

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

This Java project is managed and built using [Apache Maven](https://maven.apache.org/).

#### 1.2.1 Project object model

The [project object model](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html), `pom.xml`, is central to the use of Maven.
In this file, the project properties can be set, build plugins can be configured, project dependencies can be defined, etc.

#### 1.2.2 Configuration

In the project object model of the current project, [pom.xml](pom.xml), the so-called project coordinates are set to

```xml
<project>
  <groupId>nl.mauritssilvis.challenges.maven.project</groupId>
  <artifactId>basic</artifactId>
  <version>1.0-SNAPSHOT</version>
</project>
```

The encoding of the source files is set to UTF-8 using

```xml
<project>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
</project>
```

Finally, the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) is configured as

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.1</version>
        <configuration>
          <source>17</source>
          <target>17</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

Here, the latest version of the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) (currently 3.8.1) was selected. 
Moreover, to be up-to-date with recent developments, Java 17 was selected, which requires the [Java Development Kit 17](https://jdk.java.net/17/).

#### 1.2.3 Build

The project can be built using the command

```shell
$ mvn clean install
```

Execution of this command will compile the above-mentioned Java class file, package it as a JAR and make this JAR available in your local Maven repository.

### 1.3 IntelliJ IDEA

[IntelliJ IDEA](https://www.jetbrains.com/idea/) is an integrated development environment developed by JetBrains, of which the community edition can be downloaded and used for free.
IntelliJ IDEA comes with a [detailed online documentation](https://www.jetbrains.com/help/idea/discover-intellij-idea.html), which contains a step-by-step guide for [setting up a Maven project](https://www.jetbrains.com/help/idea/maven-support.html#create_new_maven_project).

The [.idea](.idea) folder of this project contains several IntelliJ-IDEA-related files.
A few of these files are highlighted below.

#### 1.3.1 Code styles

First, to make cross-platform coding easier, Unix line endings are selected in the file [codeStyleConfig.xml](.idea/codeStyles/codeStyleConfig.xml).
In addition, rulers are shown at 80 characters.

```xml
<component name="ProjectCodeStyleConfiguration">
  <code_scheme name="Project" version="173">
    <option name="LINE_SEPARATOR" value="&amp;#10;" />
    <option name="SOFT_MARGINS" value="80" />
  </code_scheme>
</component>
```

#### 1.3.2 Copyright

Automatic copyright messages including a license identifier are configured in the file [GNU_GPL_v3.xml](.idea/copyright/GNU_GPL_v3.xml):

```xml
<component name="CopyrightManager">
  <copyright>
    <option name="notice" value="Copyright © &amp;#36;today.year Maurits H. Silvis&#10;SPDX-License-Identifier: GPL-3.0-or-later" />
    <option name="myName" value="GNU GPL v3" />
  </copyright>
</component>
```

#### 1.3.3 Inspection profiles

To learn about possible code improvements and optimizations, an inspection profile in which all Java-17-compatible IntelliJ IDEA code inspections are turned on is provided in [All.xml](.idea/inspectionProfiles/All.xml).
A profile in which only the default inspections are selected is stored in [Defaults.xml](.idea/inspectionProfiles/Default.xml).

#### 1.3.4 Run configurations

The project comes with two run configuration, one for creating and one for executing the resulting JAR.
Note that the latter run configuration will [fail](#24-maven-jar-plugin-issues).

## 2. Issues and solutions

While setting up and building a Maven project, several problems may occur.
I list several of such problems, here, including possible solutions.
Specifically, I discuss problems related to the [project object model](#21-project-object-model-issues), the [Maven resources plugin](#22-maven-resources-plugin-issues), the [Maven compiler plugin](#23-maven-compiler-plugin-issues) and the [Maven JAR plugin](#24-maven-jar-plugin-issues).

### 2.1 Project object model issues

Several issues may arise in relation to the [project object model](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html).

#### 2.1.1 The goal you specified requires a project to execute but there is no POM in this directory

When executing Maven goals, the following error may occur:

```text
[ERROR] The goal you specified requires a project to execute but there is no POM in this directory. Please verify you invoked Maven from the correct directory.
```

To solve this problem, ensure the top-level directory of the project contains a Maven project object model file called `pom.xml` and ensure Maven is run in this directory. 

#### 2.1.2 Non-readable POM: input contained no data

When executing Maven goals, the following error may occur:

```text
[ERROR] Some problems were encountered while processing the POMs:
[FATAL] Non-readable POM: input contained no data
```

To solve this problem, ensure the Maven project object model, `pom.xml`, contains at least the `project` root element.
This root element can be included without,

```xml
<project></project>
```

or with the optional XML preamble and namespace information,

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
[ERROR] 'modelVersion' is missing. @ line 1, column 9
```

To solve this problem, set the model version in the Maven project object model, `pom.xml`:

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
</project>
```

#### 2.1.4 'groupId' is missing / 'artifactId' is missing / 'version' is missing

When executing Maven goals, one or more of the following errors may occur:

```text
[ERROR] Some problems were encountered while processing the POMs:
[FATAL] 'groupId' is missing. @ line 1, column 9
[FATAL] 'artifactId' is missing. @ line 1, column 9
[FATAL] 'version' is missing. @ line 1, column 9
```

To solve these problems, include the project coordinates, i.e., the group ID, the ID and the version of the artifact, in the Maven project object model, `pom.xml`.
For the current project, these coordinates are given by

```xml
<project>
  <groupId>nl.mauritssilvis.challenges.maven.project</groupId>
  <artifactId>basic</artifactId>
  <version>1.0-SNAPSHOT</version>
</project>
```

#### 2.1.5 'build.plugins.plugin.(groupId:artifactId)' artifactId of a plugin must be defined

When executing Maven goals, the following error may occur:

```text
[ERROR] Some problems were encountered while processing the POMs:
[FATAL] 'build.plugins.plugin.(groupId:artifactId)' artifactId of a plugin must be defined.  @ line 21, column 21
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

When using Maven plugins, a warning similar to

```text
[WARNING] Some problems were encountered while building the effective model for nl.mauritssilvis.challenges.maven.project:basic:jar:1.0-SNAPSHOT
[WARNING] 'build.plugins.plugin.version' for org.apache.maven.plugins:maven-compiler-plugin is missing. @ line 23, column 21
[WARNING]
[WARNING] It is highly recommended to fix these problems because they threaten the stability of your build.
[WARNING]
[WARNING] For this reason, future Maven versions might no longer support building such malformed projects.
```

may be shown.

To prevent this warning as well as potential future problems with your project, select the latest version of the Maven plugin in the Maven project object model, `pom.xml`.
For example, for the Maven compiler plugin, extend the `build` section of `pom.xml` with

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.1</version>
      </plugin>
    </plugins>
  </build>
</project>
```

Here, the latest version of the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) (currently 3.8.1) was selected.

### 2.2 Maven resources plugin issues

At least one issue may be reported by the [Maven resources plugin](http://maven.apache.org/plugins/maven-resources-plugin/).

#### 2.2.1 Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!

The Maven resources plugin may throw a warning of the form

```text
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
```

This warning indicates that no encoding has been set for the project files, i.e., for the source and resource files of the project.
To set the file encoding to UTF-8, include the following line in the `properties` section of the Maven project object model, `pom.xml`:

```xml
<project>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
</project>
```

### 2.3 Maven compiler plugin issues

Several issues may be reported by the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/).

#### 2.3.1 File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent! 

Similar to the Maven resources plugin, the Maven compiler plugin may return

```text
[WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
```

This warning indicates that no encoding has been set for the project files, i.e., for the source and resource files of the project.
To set the file encoding to UTF-8, include the following line in the `properties` section in the Maven project object model, `pom.xml`:

```xml
<project>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
</project>
```

#### 2.3.2 Source option is no longer supported. Use 7 or later.

The Maven compiler plugin may halt with one of the following errors:

```text
[ERROR] Source option 1.3 is no longer supported. Use 7 or later.
```

```text
[ERROR] Source option 5 is no longer supported. Use 7 or later.
```

```text
[ERROR] Source option 6 is no longer supported. Use 7 or later.
```

To solve this problem, explicitly set the Java source version in the Maven project object model, `pom.xml`.
For Java 17, this can be done by extending the `properties` section of `pom.xml` with the line

```xml
<project>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
  </properties>
</project>
```

In addition, select the latest version of the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) (currently 3.8.1) in the `build` section of `pom.xml`:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.1</version>
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
        <version>3.8.1</version>
        <configuration>
          <source>17</source>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

#### 2.3.3 Target option is no longer supported. Use 7 or later.

The Maven compiler plugin may halt with one of the following errors:

```text
[ERROR] Target option 1.1 is no longer supported. Use 7 or later.
```

```text
[ERROR] Target option 5 is no longer supported. Use 7 or later.
```

```text
[ERROR] Target option 6 is no longer supported. Use 7 or later.
```

To solve this problem, explicitly set the Java target version in the Maven project object model, `pom.xml`.
For Java 17, this can be done by extending the `properties` section of `pom.xml` with the line

```xml
<project>
  <properties>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>
</project>
```

In addition, select the latest version of the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) (currently 3.8.1) in the `build` section of `pom.xml`:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.1</version>
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
        <version>3.8.1</version>
        <configuration>
          <target>17</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

#### 2.3.4 Failure executing javac, but could not parse the error / Source release 17 requires target release 17

The Maven compiler plugin may encounter either of the following errors while compiling:

```text
[ERROR] Failure executing javac, but could not parse the error
```

or

```text
source release 17 requires target release 17
```

To solve this problem, ensure that both the Java source and target versions are set in the Maven project object model, `pom.xml`.
Additionally, ensure that the target version is not smaller than the source version.
Java 17 can be selected by extending the `properties` section of `pom.xml` with the lines

```xml
<project>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>
</project>
```

In addition, select the latest version of the [Maven compiler plugin](https://maven.apache.org/plugins/maven-compiler-plugin/) (currently 3.8.1) in the `build` section of `pom.xml`:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.1</version>
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
        <version>3.8.1</version>
        <configuration>
          <source>17</source>
          <target>17</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

### 2.4 Maven JAR plugin issues

At least one issue may be reported by the [Maven JAR plugin](https://maven.apache.org/plugins/maven-jar-plugin/).

#### 2.4.1 no main manifest attribute, in basic-1.0-SNAPSHOT.jar

When trying to execute a JAR, the following error may occur:

```text
no main manifest attribute, in basic-1.0-SNAPSHOT.jar
```

To solve this problem, configure the Maven JAR plugin according to [Creating an executable JAR using Maven](../executable_jar_maven).

## License

Copyright © 2021 Maurits H. Silvis

This source code package is subject to the terms and conditions defined in the GNU General Public License v3.0, which can be found in the file [LICENSE.md](../../LICENSE.md), or later.
