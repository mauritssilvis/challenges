# Challenges > Java

> A collection of programming challenges, solved using Java

## Introduction

With this part of the [Challenges](https://github.com/mauritssilvis/challenges) project, I provide solutions to common programming challenges in Java.

Under [Status](#1-status), I give an overview of the challenges that I solved using Java so far.
I also provide some [background information](#2-background) on [Java](#21-java) and the tools I used, namely, [IntelliJ IDEA](#22-intellij-idea) and [Maven](#23-maven).

## 1. Status

Currently, Java solutions are available to challenges in the following categories.
Note that I solved all these challenges using [IntelliJ IDEA](#22-intellij-idea).

### Maven

#### Projects

* [Setting up a basic Maven project using IntelliJ IDEA](basic_maven_project_intellij)

#### JARs

* [Creating an executable JAR using Maven](executable_jar_maven_intellij)

## 2. Background

In this section, I provide some background information on [Java](#21-java) and the tools I used to solve the above-mentioned programming challenges, namely, [IntelliJ IDEA](#22-intellij-idea) and [Maven](#23-maven).

### 2.1 Java

[Java](https://www.oracle.com/java/) is an object-oriented programming language with a syntax similar to that of C and C++.
As is the case for C and C++ code, Java code has to be compiled before it can be executed.
C and C++ are, however, compiled into platform-specific machine code.
Instead, Java compiles to platform-independent class files containing so-called bytecode.
This bytecode can then be executed on a platform of choice by a platform-specific Java virtual machine (JVM).

To be up-to-date with recent developments, most of the above-mentioned projects are configured to make use of Java 17.
To compile and build these projects, the [Java Development Kit 17](https://jdk.java.net/17/) is required.

### 2.2 IntelliJ IDEA

[IntelliJ IDEA](https://www.jetbrains.com/idea/) is an integrated development environment (IDE) developed by [JetBrains](https://www.jetbrains.com/).
This IDE supports Java and several other Java virtual machine languages, and can be extended with plugins to retrieve support for other programming languages.
IntelliJ IDEA comes with a [detailed online documentation](https://www.jetbrains.com/help/idea/discover-intellij-idea.html) and its [community edition](https://www.jetbrains.com/idea/download/) can be downloaded and used for free.

IntelliJ IDEA makes it easy to configure code styles, automatic copyright notices, code inspection profiles, run configurations and more.
The basic IntelliJ IDEA configuration used in the above-mentioned projects is described in the [IntelliJ IDEA section](basic_maven_project_intellij#12-intellij-idea) of [Setting up a basic Maven project using IntelliJ IDEA](basic_maven_project_intellij).

### 2.3 Maven

[Maven](https://maven.apache.org/) is a build tool that can be used to manage and build projects written in Java and other programming languages.
The [project object model](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html), a file named `pom.xml`, is central to the use of Maven.
In this file, the project properties can be set, build plugins can be configured, project dependencies can be defined, etc.

The basic Maven configuration used in the above-mentioned projects is discussed in the [Maven section](basic_maven_project_intellij#13-maven) of [Setting up a basic Maven project using IntelliJ IDEA](basic_maven_project_intellij).
A step-by-step guide for setting up a Maven project using IntelliJ IDEA can be found in the [Maven section](https://www.jetbrains.com/help/idea/maven-support.html#create_new_maven_project) of IntelliJ IDEA's [online documentation](https://www.jetbrains.com/help/idea/discover-intellij-idea.html).

## License

Copyright © 2021 Maurits H. Silvis

This source code package is subject to the terms and conditions defined in the GNU General Public License v3.0, which can be found in the file [LICENSE.md](../LICENSE.md), or later.
