# Challenges > Java > Setting up a basic Java project using the command line

> A basic Java project, set up using the command line

## Introduction

With this part of the [Challenges > Java](..) project, I provide the code and settings for a basic Java project, set up using the command line.

Below, I give detailed [background information](#1-background) on the project's [code](#11-java).
In addition, I list several [issues](#2-issues-and-solutions) that can occur when setting up a Java project.
I also describe solutions to these issues.

## 1. Background

### 1.1 Java

This project makes use of Java.
I describe this programming language in the [Java section](../#21-java) of [Challenges > Java](..).

#### 1.1.1 Code

For demonstrative purposes, the current project contains only a single Java file, [Main.java](src/nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main.java), which comprises a Java class with the corresponding name `Main`. 
This class contains a `main` method outputting a well-known message:

```java
package nl.mauritssilvis.challenges.java.cli.general.projects.basic;

public class Main {
  public static void main(String[] args) {
    System.out.println("Hello world!");
  }
}
```

#### 1.1.2 Directory structure

The directory structure of this project is as follows:

```text
basic_java_project_cli
├─ out
│  └─ nl
│      └─ mauritssilvis
│          └─ challenges
│              └─ java
│                  └─ cli
│                      └─ general
│                          └─ projects
│                              └─ basic
│                                 └─ Main.class
│
├─ src
│  └─ nl
│      └─ mauritssilvis
│          └─ challenges
│              └─ java
│                  └─ cli
│                      └─ general
│                          └─ projects
│                              └─ basic
│                                 └─ Main.java
│
├─ .gitignore
└─ README.md
```

Here, the `src` folder contains the source file, `Main.java`, stored in a directory structure that matches the package of the class `Main`, i.e., `nl.mauritssilvis.challenges.java.cli.general.projects.basic`.
The `out` folder, which is created upon [compilation](#113-compilation), has the same structure as the `src` folder, but is there to contain the compiled bytecode instead of source code.

#### 1.1.3 Compilation

The most basic way to compile the Java source code in `Main.java` consists in navigating to the directory of this file and calling the Java compiler:

```shell
cd src/nl/mauritssilvis/challenges/java/cli/general/projects/basic
javac Main.java
```

These commands will compile the Java code of `Main.java` into bytecode, which is then stored in the class file `Main.class` in the directory where the source code is located.

As we will see, the class file, `Main.class`, cannot be executed from the folder in which it is stored.
Moreover, Java source and class files are generally stored in different locations.
Therefore, it is more convenient to compile the source file from the project root folder with a directive that specifies the output directory:

```shell
javac -d out src/nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main.java
```

#### 1.1.4 Execution

After [compilation](#113-compilation), the Java class file, `Main.class`, that is buried in the `out` folder can be executed in several ways.

A convenient way to execute this class is given by:

```shell
cd out
java nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main
```

As is explained below, the `.class` extension of the class file should not be included.

Equivalently, one could execute the following commands:

```shell
cd out
java nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main
```

Rather than navigating to a folder containing class files manually, it is more common to execute a Java class under specification of the class path.
For the current project, this looks as follows:

```shell
java -cp out nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main
```

All above commands will result in the following output:

```text
Hello world!
```

Note that Java executes classes by their class name, not by their file name.
Therefore, the above commands should not include the `.class` extension of the Java class file name `Main.class`.

Moreover, for classes that are part of a package, the supplied class name should be the fully qualified name, which includes both the package and the class name.
For the current project, this fully qualified class name is:

```text
nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main
```

As the above shows, fully qualified class names can be specified using both slashes and dots.

The folder from which a class that is part of a package is executed has to contain a directory structure corresponding to the package name.
Therefore, the Java class file `Main.class` cannot be executed from any other folder than the `out` folder.
In particular, this class file cannot be executed from its containing parent folder.

#### 1.1.5 Direct execution

TODO

## 2. Issues and solutions

TODO

## License

Copyright © 2021, 2022 Maurits H. Silvis

This source code package is subject to the terms and conditions defined in the GNU General Public License v3.0, which can be found in the file [LICENSE.md](../../LICENSE.md), or later.
