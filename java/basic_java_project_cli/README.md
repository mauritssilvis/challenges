# Challenges > Java > Setting up a basic Java project using the command line

> A basic Java project, set up using the command line

## Introduction

With this part of the [Challenges > Java](..) project, I provide the code and settings for a basic Java project, set up using the command line.

## 1. Background

### 1.1 Java

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
The `out` folder, which is created upon compilation (see the [Compilation section](#113-compilation)), has the same structure as the `src` folder, but is there to contain the compiled bytecode instead of source code.

#### 1.1.3 Compilation

The most basic way to compile the Java source code in `Main.java` consists in navigating to the directory of this file and calling the Java compiler:

```shell
cd src/nl/mauritssilvis/challenges/java/cli/general/projects/basic
javac Main.java
```

These commands will compile the Java code of `Main.java` into bytecode, which is then stored in the class file `Main.class` in the directory where the source code is located.

The class file, `Main.class`, cannot be executed from the folder in which it is stored.
Moreover, Java source and class files are generally stored in different locations.
Therefore, it is more convenient to compile the source file from the project root folder with a directive that specifies the output directory:

```shell
javac -d out src/nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main.java
```

#### 1.1.4 Execution

#### 1.1.5 Direct execution

## 2. Issues and solutions

## License

Copyright © 2021 Maurits H. Silvis

This source code package is subject to the terms and conditions defined in the GNU General Public License v3.0, which can be found in the file [LICENSE.md](../../LICENSE.md), or later.
