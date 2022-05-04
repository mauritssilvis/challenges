# Problems

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
