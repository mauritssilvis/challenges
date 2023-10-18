# Setting up a Java project using the command line

> A Java project set up using the command line

## Introduction

With this part of the [Java challenges](..) project, I provide the code and settings for a Java project set up using the command line.

Below, I give detailed [background information](#1-background) on the project's [code](#11-java).
In addition, I list several [issues](#2-issues-and-solutions) that can occur when setting up a Java project.
I also describe solutions to these issues.

The listed commands assume the working directory corresponds to this project's main folder and can, for example, be executed using Bash.
I describe this command-line interface in the [Bash section](../#22-bash) of the [Java challenges](..) project.

## 1. Background

### 1.1 Java

This project makes use of Java.
I describe this programming language in the [Java section](../#21-java) of the [Java challenges](..) project.

#### 1.1.1 Installation

To work with Java code, you have to install the Java Development Kit (JDK).

You can install the [Adoptium](https://adoptium.net/) distribution of the JDK as follows:

- Go to https://adoptium.net/temurin/releases/.
- Select the latest long-term support (LTS) version of Java (Java 21 at the time of writing).
- Download the archive or installer matching your system.
- Extract or install the files in a convenient location.

If you want to work with Java from the command line, as is done in this project, you have to add the Java executables to your path:

- Add the full path of the created `jdk-X+Y/bin` folder to your `PATH` environment variable. Here, `X` and `Y` are placeholders for version numbers.

You can then verify your Java installation using the following steps:

- Run the command `java --version`.
- Verify that the output matches the desired JDK version.

#### 1.1.2 Code

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

#### 1.1.3 Directory structure

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
The `out` folder, which is created upon [compilation](#114-compilation), has the same structure as the `src` folder but is there to contain compiled bytecode instead of source code.

#### 1.1.4 Compilation

The most basic way to compile the Java source code in `Main.java` consists in navigating to the directory of this file and calling the Java compiler, `javac`:

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

#### 1.1.5 Execution

After [compilation](#114-compilation), the Java class file, `Main.class`, which is buried in the `out` folder, can be executed in several ways.

A convenient way to execute this class is given by the following commands involving the Java interpreter, `java`:

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

Rather than manually navigating to a folder containing (a hierarchy of directories with) class files, it is more common to execute a Java class relative to a so-called class path.
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

#### 1.1.6 Direct execution

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
I list several such issues here, including possible solutions.
In particular, I discuss problems related to the [installation](#21-installation-issues) of Java and the [compilation](#22-compilation-issues) and [execution](#23-execution-issues) of Java programs.

### 2.1 Installation issues

#### 2.1.1 The `java` command was not found / The `javac` command was not found

While trying to invoke the Java interpreter, `java`, or the Java compiler, `javac`, you may encounter errors of the following form:

```text
java: command not found
```

```text
'java' is not recognized as an internal or external command, operable program
or batch file.
```

```text
java : The term 'java' is not recognized as the name of a cmdlet, function,
script file, or operable program.
```

These errors indicate Java was not installed or the Java installation was not found.

To solve these problems, install the JDK, for example, according to the [installation instructions](#111-installation) given above.
In the process, ensure the `PATH` environment variable contains a reference to the proper JDK folder.

#### 2.1.2 The Java version does not match

When checking the Java version using the command `java --version`, you may encounter unexpected output.
For example, the output may show a lower version of Java than expected:

```text
openjdk 20.0.2 2023-07-18
OpenJDK Runtime Environment Temurin-20.0.2+9 (build 20.0.2+9)
OpenJDK 64-Bit Server VM Temurin-20.0.2+9 (build 20.0.2+9, mixed mode, sharing)
```

To solve this problem, install the desired JDK, for example, according to the [installation instructions](#111-installation) given above.
In the process, ensure the `PATH` environment variable contains a reference to the proper JDK folder.

### 2.2 Compilation issues

#### 2.2.1 file not found

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

Alternatively, ensure that you call the right tool.
You may have wanted to call the Java interpreter instead of the Java compiler.
In that case, ensure you drop any file extensions, use the fully qualified class name and execute the class from the proper location:

```shell
java -cp out nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
```

#### 2.2.2 Class names are only accepted if annotation processing is explicitly requested

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

Alternatively, ensure that you call the right tool.
You may have wanted to call the Java interpreter instead of the Java compiler
In that case, ensure you use the fully qualified class name and execute the class from the proper location:

```shell
java -cp out nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
```

#### 2.2.3 invalid flag

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

Alternatively, ensure that you call the right tool.
You may have wanted to call the Java interpreter instead of the Java compiler.
In that case, ensure you drop any file extensions, use the fully qualified class name and execute the class from the proper location:

```shell
java -cp out nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
```

### 2.3 Execution issues

#### 2.3.1 Could not find or load main class / java.lang.ClassNotFoundException

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

#### 2.3.2 Could not find or load main class / java.lang.NoClassDefFoundError

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

#### 2.3.3 Java is not up-to-date / java.lang.UnsupportedClassVersionError

When trying to execute Java programs, you may encounter an error of the following form:

```text
Error: LinkageError occurred while loading main class nl.mauritssilvis.challenges.java.cli.manual.projects.basic.Main
        java.lang.UnsupportedClassVersionError: nl/mauritssilvis/challenges/java/cli/manual/projects/basic/Main
        has been compiled by a more recent version of the Java Runtime (class
        file version ...), this version of the Java Runtime only recognizes
        class file versions up to ...
```

To solve this problem, install the latest JDK, for example, according to the [installation instructions](#111-installation) given above.
In the process, ensure the `PATH` environment variable contains a reference to the proper JDK folder.

## License

Copyright © 2021–2023 Maurits Silvis

This source code package is subject to the terms and conditions defined in the [GNU General Public License v3.0](../../LICENSE.md) or later.
