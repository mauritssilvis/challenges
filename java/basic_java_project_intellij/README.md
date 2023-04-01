# Challenges > Java > Setting up a basic Java project using IntelliJ IDEA

> A basic Java project, set up using IntelliJ IDEA

## Introduction

With this part of the [Challenges](https://github.com/mauritssilvis/challenges) > [Java](https://github.com/mauritssilvis/challenges/tree/main/java) project, I provide the code and settings for a basic Java project, set up using IntelliJ IDEA.

Below, I give [background information](#1-background) on the project's [code](#11-java) and [IntelliJ IDEA's configuration](#12-intellij-idea).

## 1. Background

### 1.1 Java

This project makes use of Java.
I describe this programming language in the [Java section](../#21-java) of [Challenges > Java](..).

#### 1.1.1 Code

For demonstrative purposes, the current project contains only a single Java class called `Main`, which consists of a `main` method outputting a well-known message:

```java
package nl.mauritssilvis.challenges.java.intellij.general.projects.basic;

public class Main {
  public static void main(String[] args) {
    System.out.println("Hello world!");
  }
}
```

### 1.2 IntelliJ IDEA

This project is set up using [IntelliJ IDEA](https://www.jetbrains.com/idea/) (see, e.g., the [IntelliJ IDEA section](../#22-intellij-idea) of [Challenges > Java](..)).

The used IntelliJ IDEA configuration is described in what follows.

#### 1.2.1 Configuration

The [.idea](.idea) folder of this project contains several IntelliJ-IDEA-related configuration files.
A few of these files are highlighted below.

##### Code styles

First, to make cross-platform coding easier, Unix-style line endings are selected in the file [Project.xml](.idea/codeStyles/Project.xml).
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

Automatic copyright messages including the current year and an [SPDX license identifier](https://spdx.dev/ids/) for the [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html) are configured in the file [GNU_GPL_v3.xml](.idea/copyright/GNU_GPL_v3.xml):

```xml
<component name="CopyrightManager">
  <copyright>
    <option name="notice" value="Copyright © &amp;#36;today.year Maurits Silvis&#10;SPDX-License-Identifier: GPL-3.0-or-later" />
    <option name="myName" value="GNU GPL v3" />
  </copyright>
</component>
```

##### Inspection profiles

To learn about possible code improvements and optimizations, a code inspection profile in which all Java-17-compatible IntelliJ IDEA inspections are turned on is provided in [All.xml](.idea/inspectionProfiles/All.xml).
A profile in which only the default inspections are selected is stored in [Defaults.xml](.idea/inspectionProfiles/Default.xml).

##### Run configurations

This project comes with one run configuration for executing the `main` method of the `Main` class.

## License

Copyright © 2021–2023 Maurits Silvis

This source code package is subject to the terms and conditions defined in the GNU General Public License v3.0, which can be found in the file [LICENSE.md](../../LICENSE.md), or later.
