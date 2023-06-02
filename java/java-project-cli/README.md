# Setting up a Java project using the command line

> A Java project set up using the command line

## Introduction

With this part of the [Challenges](https://github.com/mauritssilvis/challenges) > [Java](https://github.com/mauritssilvis/challenges/tree/main/java) project, I provide the code and settings for a Java project, set up using the command line.

Below, I give detailed [background information](#1-background) on the project's [code](#11-java).
In addition, I list several [issues](#2-issues-and-solutions) that can occur when setting up a Java project.
I also describe solutions to these issues.

## 1. Background

### 1.1 Java

This project makes use of Java.
I describe this programming language in the [Java section](https://github.com/mauritssilvis/challenges/tree/main/java#21-java) of the [Challenges](https://github.com/mauritssilvis/challenges) > [Java](https://github.com/mauritssilvis/challenges/tree/main/java) project.

#### 1.1.1 Code

For demonstrative purposes, the current project contains only a single Java file, [Main.java](src/nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main.java), which comprises a Java class with the corresponding name `Main`.
This class contains a `main` method outputting a well-known message:

```java
package nl.mauritssilvis.challenges.java.cli.manual.projects.basic;

public class Main {
  public static void main(String[] args) {
    System.out.println("Hello world!");
  }
}
```

#### 1.1.2 Directory structure

The directory structure of this project is as follows:

```text
java-project-cli
├─ out
│  └─ nl
│      └─ mauritssilvis
│          └─ challenges
│              └─ java
│                  └─ cli
│                      └─ manual
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
│                      └─ manual
│                          └─ projects
│                              └─ basic
│                                 └─ Main.java
│
├─ .gitignore
└─ README.md
```

Here, the `src` folder contains the source file, `Main.java`, stored in a directory structure that matches the package of the class `Main`, i.e., `nl.mauritssilvis.challenges.java.cli.manual.projects.basic`.
The `out` folder, which is created upon [compilation](#113-compilation), has the same structure as the `src` folder, but is there to contain the compiled bytecode instead of source code.

#### 1.1.3 Compilation

The most basic way to compile the Java source code in `Main.java` consists in navigating to the directory of this file and calling the Java compiler:

```shell
cd src/nl/mauritssilvis/challenges/java/cli/manual/projects/basic
javac Main.java
```

These commands will compile the Java code of `Main.java` into bytecode, which is then stored in the class file `Main.class` in the directory where the source code is located.

As we will see, the class file, `Main.class`, cannot be executed from the folder in which it is stored.
Moreover, Java source and class files are generally stored in different locations.
Therefore, it is more convenient to compile the source file from the project root folder with a `-d` option that specifies the output directory:

```shell
javac -d out src/nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main.java
```

#### 1.1.4 Execution

After [compilation](#113-compilation), the Java class file, `Main.class`, that is buried in the `out` folder can be executed in several ways.

A convenient way to execute this class is given by:

```shell
cd out
java nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main
```

As is explained below, the `.class` extension of the class file should not be included.

Equivalently, one could execute the following commands:

```shell
cd out
java nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
```

Rather than manually navigating to a folder containing class files, it is more common to execute a Java class relative to a so-called class path.
For the current project, the following command involving the `-cp` option executes the previously compiled class from the class path `out`:

```shell
java -cp out nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
```

All above commands will result in the following output:

```text
Hello world!
```

Note that Java executes classes by their class name, not by their file name.
Therefore, the above commands should not include the `.class` extension of the Java class file name `Main.class`.

Moreover, for classes that are part of a package, the supplied class name should be the so-called fully qualified name, which includes both the package and the class name.
For the current project, this fully qualified class name is:

```text
nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
```

As the above shows, fully qualified class names can be provided to the Java interpreter using both slashes and dots.

Class files of Java classes that are part of a package have to be stored in a directory structure corresponding to the package name.
Otherwise, these classes cannot be executed.
More specifically, the folder from which a class is executed should contain a directory structure corresponding to the package name of that class.
Therefore, the Java class file `Main.class` cannot be executed from any other folder than the `out` folder.
In particular, this class file cannot be executed from its containing parent folder.

#### 1.1.5 Direct execution

Since Java 11, programs consisting of only a single source file can be executed directly, without the need for an explicit compilation step.
For the current project, the following command directly executes the source file `Main.java` from its containing folder:

```shell
cd src/nl/mauritssilvis/challenges/java/cli/manual/projects/basic
java Main.java
```

Alternatively, direct execution from the main project folder is possible:

```bash
java src/nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main.java
```

As expected, the output of the above commands is:

```text
Hello world!
```

## 2. Issues and solutions

While setting up a Java project, several issues may occur.
I list several such issues, here, including possible solutions.
In particular, I discuss problems related to [compilation](#21-compilation-issues) and [execution](#22-execution-issues) of Java programs.

### 2.1 Compilation issues

#### 2.1.1 file not found

Since the Java interpreter accepts class names with slashes and dots, one may be tempted to use dots in paths to Java source files in calls to the Java compiler:

```shell
cd src
javac nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main.java
```

Such commands will, however, result in an error of the form:

```text
error: file not found: nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main.java
Usage: javac <options> <source files>
use --help for a list of possible options
```

To solve this problem, use slashes when a file path to a source file is expected:

```shell
javac -d out src/nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main.java
```

Alternatively, ensure that you called the right tool.
You may have wanted to call the Java interpreter instead of the Java compiler.
In that case, ensure you drop any file extensions, you use the fully qualified class name and you execute the class from the proper location:

```shell
java -cp out nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
```

#### 2.1.2 Class names are only accepted if annotation processing is explicitly requested

When working with Java, you may encounter errors of the following form:

```text
error: Class names, 'Main', are only accepted if annotation processing is explicitly requested
1 error
```

```text
error: Class names, 'nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main', are only accepted if annotation processing is explicitly requested
1 error
```

Such errors respectively result from using the Java compiler in commands of the form:

```shell
cd src/nl/mauritssilvis/challenges/java/cli/manual/projects/basic
javac Main
```

```shell
cd src
javac nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
```

Here, the Java compiler is supplied with class names.

To solve the above problem, do not supply the Java compiler with a class name when a path to a source file is expected.
In addition, ensure the `.java` file extension is present in paths to source files:

```shell
javac -d out src/nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main.java
```

Alternatively, ensure that you called the right tool.
You may have wanted to call the Java interpreter instead of the Java compiler
In that case, ensure you use the fully qualified class name and you execute the class from the proper location:

```shell
java -cp out nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
```

#### 2.1.3 invalid flag

When working with Java, you may encounter an error of the following form:

```text
error: invalid flag: Main.class
Usage: javac <options> <source files>
use --help for a list of possible options
```

Such an error may result from calling the Java compiler on a Java class file:

```shell
cd src/nl/mauritssilvis/challenges/java/cli/manual/projects/basic
javac Main.class
```

To solve the above problem, do not provide the Java compiler with the path of a class file when a path to a source file is expected.
In addition, ensure the `.java` file extension (instead of `.class`) is used in paths to source files:

```shell
javac -d out src/nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main.java
```

Alternatively, ensure that you called the right tool.
You may have wanted to call the Java interpreter instead of the Java compiler.
In that case, ensure you drop any file extensions, you use the fully qualified class name and you execute the class from the proper location:

```shell
java -cp out nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
```

### 2.2 Execution issues

#### 2.2.1 Could not find or load main class / java.lang.ClassNotFoundException

When trying to execute Java programs, you may encounter errors of the following form:

```text
Error: Could not find or load main class Main.class
Caused by: java.lang.ClassNotFoundException: Main.class
```

Such errors result from calling the Java interpreter on class files:

```shell
cd out/nl/mauritssilvis/challenges/java/cli/manual/projects/basic
java Main.class
```

To solve the above problem, do not include the `.class` extension when referring to Java classes.
In addition, ensure execution takes place from the proper path.
For the current project, these two conditions are fulfilled for the following command:

```shell
cd out
java nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main
```

As noted before, a more common way of writing this command is given by:

```shell
java -cp out nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
```

#### 2.2.2 Could not find or load main class / java.lang.NoClassDefFoundError

When trying to execute Java programs, you may encounter errors of the following form:

```text
Error: Could not find or load main class Main
Caused by: java.lang.NoClassDefFoundError: nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main (wrong name: Main)
```

```text
Error: Could not find or load main class out.nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
Caused by: java.lang.NoClassDefFoundError: nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main (wrong name: out/nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main)
```

Such errors result from calling the Java interpreter using commands of the form:

```shell
cd out/nl/mauritssilvis/challenges/java/cli/manual/projects/basic
java Main
```

```shell
java out/nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main
```

To solve the above problem, ensure that classes that belong to a package are executed from a folder that contains a directory structure corresponding to the package name.
For the current project, the following command could be used:

```shell
cd out
java nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main
```

As noted before, a more common way of writing this command is given by:

```shell
java -cp out nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
```

## License

Copyright © 2021–2023 Maurits Silvis

This source code package is subject to the terms and conditions defined in the GNU General Public License v3.0, which can be found in the file [LICENSE.md](../../LICENSE.md), or later.
