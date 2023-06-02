# Java challenges

> A collection of programming challenges solved using Java

## Introduction

With this part of the [Challenges](https://github.com/mauritssilvis/challenges) project, I provide solutions to common programming challenges in Java.

Below, I first give an [overview](#1-overview) of the challenges that I have solved so far.
I then provide some [background information](#2-background) on [Java](#21-java) and the tools I used, namely, [Bash](#22-bash), [IntelliJ IDEA](#23-intellij-idea) and [Maven](#24-maven).

## 1. Overview

Currently, Java solutions are available for the following challenges, categorized according to the tools I used.

### 1.1 Command-line projects

I solved the challenges in this section using the [command line](#22-bash).

#### 1.1.1 General

The challenges listed below were solved without a build tool.

##### Projects

* [Setting up a Java project using the command line](basic-java-project-cli)

### 1.2 IntelliJ IDEA projects

I solved the following challenges using [IntelliJ IDEA](#23-intellij-idea).
For some challenges, I did not use a build tool ([general](#121-general)).
For others, I used [Maven](#122-maven).

#### 1.2.1 General

##### Projects

* [Setting up a basic Java project using IntelliJ IDEA](basic-java-project-intellij)

#### 1.2.2 Maven

##### Projects

* [Setting up a basic Maven project using IntelliJ IDEA](basic-maven-project-intellij)

##### JARs

* [Creating an executable JAR using Maven](executable-jar-maven-intellij)

## 2. Background

In this section, I provide some background information on [Java](#21-java) and the tools I used to solve the above-mentioned programming challenges, namely, [Bash](#22-bash), [IntelliJ IDEA](#23-intellij-idea) and [Maven](#24-maven).

### 2.1 Java

[Java](https://www.oracle.com/java/) is an object-oriented programming language with a syntax similar to C and C++.
As is the case for C and C++ code, Java code has to be compiled before it can be executed.
C and C++ are, however, compiled into platform-specific machine code.
Instead, Java compiles to platform-independent class files containing so-called bytecode.
This bytecode can be executed on a platform of choice by a platform-specific Java virtual machine (JVM).

Most of the above-mentioned projects are configured to use the latest long-term support (LTS) version of Java (Java 20 at the time of writing).
These projects require the installation of the Java Development Kit (JDK) 20 or later (see, e.g., https://adoptium.net/temurin/releases/).


### 2.2 Bash

TODO

### 2.3 IntelliJ IDEA

[IntelliJ IDEA](https://www.jetbrains.com/idea/) is an integrated development environment (IDE) developed by [JetBrains](https://www.jetbrains.com/).
This IDE supports Java and several other JVM languages and can be extended with plugins to retrieve support for other programming languages.
IntelliJ IDEA has [detailed online documentation](https://www.jetbrains.com/help/idea/discover-intellij-idea.html), and its [community edition](https://www.jetbrains.com/idea/download/) can be downloaded and used for free.

IntelliJ IDEA makes it easy to configure code styles, automatic copyright notices, code inspection profiles, run configurations and more.
The basic IntelliJ IDEA configuration used in the above-mentioned projects is described in the [IntelliJ IDEA section](basic-java-project-intellij#12-intellij-idea) of [Setting up a basic Java project using IntelliJ IDEA](basic-java-project-intellij).

### 2.4 Maven

[Maven](https://maven.apache.org/) is a build tool that can be used to manage and build projects written in Java and other programming languages.
The [project object model](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html), a file named `pom.xml`, is central to using Maven.
In this file, the project properties can be set, build plugins can be configured, project dependencies can be defined, etc.

The basic Maven configuration used in the above-mentioned projects is discussed in the [Maven section](basic-maven-project-intellij#13-maven) of [Setting up a basic Maven project using IntelliJ IDEA](basic-maven-project-intellij).
A step-by-step guide for setting up a Maven project using IntelliJ IDEA can be found in the [Maven section](https://www.jetbrains.com/help/idea/maven-support.html#create_new_maven_project) of IntelliJ IDEA's [online documentation](https://www.jetbrains.com/help/idea/discover-intellij-idea.html).

## License

Copyright © 2021–2023 Maurits Silvis

This source code package is subject to the terms and conditions defined in the GNU General Public License v3.0, which can be found in the file [LICENSE.md](../LICENSE.md), or later.
