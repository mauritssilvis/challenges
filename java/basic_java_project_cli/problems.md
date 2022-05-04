# Background

## Java execution

### Directly executing the Java source file using Java from any folder

```
cd src/nl/mauritssilvis/challenges/java/cli/general/projects/basic
java Main.java
```

```
java src/nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main.java
```

Hello world!

# Problems

## Java compilation problems

### file not found

Using dots instead of slashes in the Java source file path:

```
javac src.nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main.java
```

```
error: file not found: src.nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main.java
Usage: javac <options> <source files>
use --help for a list of possible options
```

Use normal paths, not using dots to separate folder names:

```
javac src/nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main.java
```

### Class names are only accepted if annotation processing is explicitly requested

Using a class-name-like path:

```
cd out/nl/mauritssilvis/challenges/java/cli/general/projects/basic
javac Main
```

```
error: Class names, 'Main', are only accepted if annotation processing is explicitly requested
1 error
```

```
javac src.nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main
```

```
error: Class names, 'src.nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main', are only accepted if annotation processing is explicitly requested
1 error
```

Do not use class-name-like paths.

### error: invalid flag

Using a class-name-like path with a .class ending:
/
Running the Java compiler on a class file:
/
Any invalid flag:

(
    ```
    javac out.nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main.class
    ```

    ```
    error: invalid flag: out.nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main.class
    Usage: javac <options> <source files>
    use --help for a list of possible options
    ```
)

```
cd out/nl/mauritssilvis/challenges/java/cli/general/projects/basic
javac Main.class
```

```
error: invalid flag: Main.class
Usage: javac <options> <source files>
use --help for a list of possible options
```

Do not run the Java compiler on class files.

## Java execution problems

### Problem: Error: Invalid or corrupt jarfile

### Problem: Executing the class file including its extension

Error: Could not find or load main class / Caused by: java.lang.ClassNotFoundException

```
cd out/nl/mauritssilvis/challenges/java/cli/general/projects/basic
java Main.class
```

(
    ```
    Error: Could not find or load main class Main.class
    Caused by: java.lang.ClassNotFoundException: Main.class
    ```

    ```
    cd out
    java nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main.class
    ```

    ```
    Error: Could not find or load main class nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main.class
    Caused by: java.lang.ClassNotFoundException: nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main.class
    ```

    ```
    java out/nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main.class
    ```

    ```
    Error: Could not find or load main class out.nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main.class
    Caused by: java.lang.ClassNotFoundException: out.nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main.class
    ```
)

Solutions: Do not include the .class extension and execute from the proper folder (either with slashes or with dots):

```
cd out
java nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main
```

```
cd out
java nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main
```

### Problem: Executing a class from the wrong folder

Error: Could not find or load main class / Caused by: java.lang.NoClassDefFoundError

```
cd out/nl/mauritssilvis/challenges/java/cli/general/projects/basic
java Main
```

```
Error: Could not find or load main class Main
Caused by: java.lang.NoClassDefFoundError: nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main (wrong name: Main)

```

```
java out/nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main
```

```
Error: Could not find or load main class out.nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main
Caused by: java.lang.NoClassDefFoundError: nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main (wrong name: out/nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main)
```

Solutions: Execute from the proper folder:

```
cd out
java nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main
```

```
cd out
java nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main
```

```
java -cp out nl/mauritssilvis/challenges/java/cli/general/projects/basic/Main
```

```
java -cp out nl.mauritssilvis.challenges.java.cli.general.projects.basic.Main
```
