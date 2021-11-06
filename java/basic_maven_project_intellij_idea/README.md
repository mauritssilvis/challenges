# Challenges > Java > Creating a basic Maven project using IntelliJ IDEA

> A basic Maven project, set up using IntelliJ IDEA

## About

With this part of the [Challenges](https://github.com/mauritssilvis/challenges) project, I provide the code and settings for a basic Maven project, set up using IntelliJ IDEA.

## 1. Background

### 1.1 Maven

#### 1.1.1 Project object model

### 1.2 IntelliJ IDEA

#### 1.2.1 Copyright

#### 1.2.2 Inspection profiles

#### 1.2.3 Run configurations

## 2. Issues and solutions

While setting up and executing a Maven project, several problems may occur.
I list several of such problems, here, including possible solutions.

### 2.1 Project object model issues

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

To solve this problem, ensure the Maven project object model file, `pom.xml`, contains at least the `project` root element.
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
[ERROR] 'modelVersion' is missing. @ line 2, column 10
```

To solve this problem, set the model version in the Maven project file, `pom.xml`:

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
</project>
```

#### 2.1.4 'groupId' is missing / 'artifactId' is missing / 'version' is missing

When executing Maven goals, one or more of the following errors may occur:

```text
[ERROR] Some problems were encountered while processing the POMs:
[FATAL] 'groupId' is missing. @ line 2, column 10
[FATAL] 'artifactId' is missing. @ line 2, column 10
[FATAL] 'version' is missing. @ line 2, column 10
```

To solve these problems, include the project coordinates, i.e., the artifact group ID, ID and version in the Maven project file:

```xml
<project>
    <groupId>nl.mauritssilvis.challenges.maven.project</groupId>
    <artifactId>basic</artifactId>
    <version>1.0-SNAPSHOT</version>
</project>
```

### 2.2 Maven resources plugin issues

#### 2.2.1 Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!

The Maven resources plugin may throw a warning of the form

```text
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
```

This warning indicates that no encoding has been set for project files, i.e., sources and resources.
To set the file encoding to UTF-8, include the following line in the `properties` section of the Maven project file, `pom.xml`:

```xml
<project>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
</project>
```

### 2.3 Maven compiler plugin issues

#### 2.3.1 File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent! 

Similarly, the Maven compiler plugin may return

```text
[WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
```

This warning indicates that no encoding has been set for project files, i.e., sources and resources.
To set the file encoding to UTF-8, include the following line in the `properties` section in the Maven project file, `pom.xml`:

```xml
<project>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
</project>
```

#### 2.3.2 Source option 5 is no longer supported. Use 7 or later. / Source option 6 is no longer supported. Use 7 or later.

The Maven compiler plugin may halt with either of the errors

```text
[ERROR] Source option 5 is no longer supported. Use 7 or later.
```

or

```text
[ERROR] Source option 6 is no longer supported. Use 7 or later.
```

To solve this problem, explicitly set the Java source version in the Maven project file, `pom.xml`.
For Java 16, either enhance the `properties` section of `pom.xml` with the line

```xml
<project>
    <properties>
        <maven.compiler.source>16</maven.compiler.source>
    </properties>
</project>
```

or configure the Maven compiler in the `build` section:

```xml
<project>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>16</source>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

#### 2.3.3 Target option 5 is no longer supported. Use 7 or later. / Target option 6 is no longer supported. Use 7 or later.

The Maven compiler plugin may halt with either of the errors

```text
[ERROR] Target option 5 is no longer supported. Use 7 or later.
```

or

```text
[ERROR] Target option 6 is no longer supported. Use 7 or later.
```

To solve this problem, explicitly set the Java target version in the Maven project file, `pom.xml`.
For Java 16, either enhance the `properties` section of `pom.xml` with the line

```xml
<project>
    <properties>
        <maven.compiler.target>16</maven.compiler.target>
    </properties>
</project>
```

or configure the Maven compiler in the `build` section:

```xml
<project>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <target>16</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

#### 2.3.4 Source release 16 requires target release 16

The Maven compiler may encounter the following fatal error while compiling:

```text
source release 16 requires target release 16
```

To solve this problem, ensure that both the Java source and target versions are set in the Maven project file, `pom.xml`.
Java 16 can be selected by enhancing the `properties` section of `pom.xml` with the lines

```xml
<project>
    <properties>
        <maven.compiler.source>16</maven.compiler.source>
        <maven.compiler.target>16</maven.compiler.target>
    </properties>
</project>
```

or by configuring the Maven compiler in the `build` section:

```xml
<project>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>16</source>
                    <target>16</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

### 2.4 Maven JAR plugin issues

#### 2.4.1 no main manifest attribute, in basic-1.0-SNAPSHOT.jar

When trying to execute a JAR, the following error may occur:

```text
no main manifest attribute, in basic-1.0-SNAPSHOT.jar
```

To solve this problem, configure the Maven JAR plugin in the Maven project file, `pom.xml`, to specify the class with which execution has to start:

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
                                nl.mauritssilvis.challenges.maven.project.basic.Main
                            </mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## License

Copyright © 2021 Maurits H. Silvis

This source code package is subject to the terms and conditions defined in the GNU General Public License v3.0, which can be found in the file [LICENSE.md](../../LICENSE.md), or later.
