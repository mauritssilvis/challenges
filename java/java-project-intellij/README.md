# Setting up a Java project using IntelliJ IDEA

> A Java project set up using IntelliJ IDEA

## Introduction

With this part of the [Java challenges](..) project, I provide the code and settings for a Java project set up using IntelliJ IDEA.

Below, I give [background information](#1-background) on the project's [code](#11-java) and [IntelliJ IDEA's configuration](#12-intellij-idea).

## 1. Background

### 1.1 Java

This project makes use of Java.
I describe this programming language in the [Java section](../#21-java) of the [Java challenges](..) project.

#### 1.1.1 Code

For demonstrative purposes, the current project contains only a single Java class called `Main`, which consists of a `main` method outputting a well-known message:

```java
package nl.mauritssilvis.challenges.java.intellij.manual.projects.basic;

public class Main {
  public static void main(String[] args) {
    System.out.println("Hello world!");
  }
}
```

### 1.2 IntelliJ IDEA

This project is set up using IntelliJ IDEA (see, e.g., the [IntelliJ IDEA section](../#23-intellij-idea) of the [Java challenges](..) project).

The IntelliJ IDEA configuration is described in what follows.

#### 1.2.1 Configuration

The [.idea](.idea) folder of this project contains several IntelliJ-IDEA-related configuration files.
A few of these files are highlighted below.

##### Code styles

First, Unix-style line endings are selected in the file [Project.xml](.idea/codeStyles/Project.xml), which facilitates cross-platform coding.
In addition, rulers are shown at 80 characters:

```xml
<component name="ProjectCodeStyleConfiguration">
  <code_scheme name="Project" version="173">
    <option name="LINE_SEPARATOR" value="&amp;#10;" />
    <option name="SOFT_MARGINS" value="80" />
  </code_scheme>
</component>
```

##### Copyright

Automatic copyright messages, including the current year and an [SPDX license identifier](https://spdx.dev/ids/) for the [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html), are configured in the file [GNU_GPL_v3.xml](.idea/copyright/GNU_GPL_v3.xml):

```xml
<component name="CopyrightManager">
  <copyright>
    <option name="notice" value="Copyright © &amp;#36;today.year Maurits Silvis&#10;SPDX-License-Identifier: GPL-3.0-or-later" />
    <option name="myName" value="GNU GPL v3" />
  </copyright>
</component>
```

##### Inspection profiles

A code inspection profile in which all Java-20-compatible IntelliJ IDEA inspections are turned on is provided in [All.xml](.idea/inspectionProfiles/All.xml).
This profile facilitates learning about possible code improvements and optimizations.
A profile in which only the default inspections are selected is stored in [Default.xml](.idea/inspectionProfiles/Default.xml).

##### Run configurations

This project comes with a run configuration for executing the `main` method of the `Main` class.

<!-- TODO: Discuss the execution of the code. -->

<!-- TODO: Discuss the project JDK choice. -->

<!-- TODO: Discuss problems with a non-existing JDK. -->

## License

Copyright © 2021–2023 Maurits Silvis

This source code package is subject to the terms and conditions defined in the [GNU General Public License v3.0](../../LICENSE.md) or later.
