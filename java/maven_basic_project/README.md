# Challenges > Java > Creating a basic Maven project

> A basic Maven project, set up using IntelliJ IDEA

## About

With this part of the [Challenges](https://github.com/mauritssilvis/challenges) project, I provide the code and settings for a basic Maven project, set up using IntelliJ IDEA.

## Issues and solutions

While setting up and executing a Maven project, several problems may occur.
I list several of such problems, here, including possible solutions.

### Maven resources plugin: `Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!`

The Maven resources plugin may through a warning of the form

```
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
```

This warning indicates that no encoding has been set for project files, i.e., sources and resources.
To set the file encoding, include the following section in the Maven project file, `pom.xml`:

```
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

### Maven compiler plugin: `File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!` 

Similarly, the Maven compiler plugin may return

```
[WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
```

This warning indicates that no encoding has been set for project files, i.e., sources and resources.
To set the file encoding, include the following section in the Maven project file, `pom.xml`:

```
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

## License

Copyright © 2021 Maurits H. Silvis

This source code package is subject to the terms and conditions defined in the GNU General Public License v3.0, which can be found in the file [LICENSE.md](../../LICENSE.md), or later.
