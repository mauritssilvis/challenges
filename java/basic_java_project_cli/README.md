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

Here, the `src` folder contains the source file, Main.java, stored in a directory structure that matches the package `nl.mauritssilvis.challenges.java.cli.general.projects.basic` of the class `Main`.
The `out` folder, which is created upon compilation (see the Compile section), has the same structure as the `src` folder, but contains the compiled bytecode instead of source code.

#### 1.1.3 Compile

#### 1.1.4 Run

## 2. Issues and solutions

## License

Copyright © 2021 Maurits H. Silvis

This source code package is subject to the terms and conditions defined in the GNU General Public License v3.0, which can be found in the file [LICENSE.md](../../LICENSE.md), or later.
