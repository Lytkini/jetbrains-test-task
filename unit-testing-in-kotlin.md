---
layout: default
title: Unit Testing in Kotlin
---

# Unit Testing in Kotlin

Just like in Java, unit testing in Kotlin helps to check whether classes, methods, and other small pieces of your application are working correctly. Kotlin unit tests can achieve that using [a set of test annotations and assertion functions](link-to-the-annotations-and-assertions-section.html) provided in the `kotlin.test` library.

The library includes several modules that target different platforms and testing frameworks:

- `kotlin-test-common` – provides assertion functions for use in common code of multiplatform projects;
- `kotlin-test-annotations-common` – provides test annotations for use in common code of multiplatform projects;
- `kotlin-test` – provides a JVM implementation of the `kotlin-test-common` assertion functions for use in multiplatform projects;
- `kotlin-test-junit` – provides an implementation of the `kotlin-test-annotations-common` assertion functions for JUnit and maps the `kotlin-test-annotations-common` annotations to JUnit test annotations;
- `kotlin-test-junit5` – provides an implementation of the `kotlin-test-annotations-common` assertion functions for JUnit 5 and maps the `kotlin-test-annotations-common` annotations to JUnit 5 test annotations;
- `kotlin-test-testng` – provides an implementation of the `kotlin-test-annotations-common` assertion functions for TestNG and maps the `kotlin-test-annotations-common` annotations to TestNG;
- `kotlin-test-js` – provides a JS implementation of the `kotlin-test-common` and `kotlin-test-annotations-common` assertion functions and annotations with the out-of-the-box support for Jasmine, Mocha, and Jest testing frameworks.

This article describes how to configure various projects for writing Kotlin unit tests and shows how to create and run a simple Kotlin unit test.

## Project configuration

To use the `kotlin.test` library, you need to define one or more library modules as dependencies in a project's build file.

A particular set of modules is defined by testing frameworks and a target platform of the project. 

### JVM

Depending on your project's testing framework, you need to define one or more of the following `kotlin.test` modules:

- `kotlin-test-junit`;
- `kotlin-test-junit5`;
- `kotlin-test-testng`;

If you use gradle, define modules in the `testImplementation` configuration, in the `dependencies` block within `build.gradle` (`build.gradle.kts`):

<div class="multi-language-sample" data-lang="groovy">
<div class="sample" markdown="1" theme="idea" mode='groovy'>

```groovy
dependencies {
    implementation("org.jetbrains.kotlin:kotlin-stdlib-jdk8")
    testImplementation("org.jetbrains.kotlin:kotlin-test-junit")
}
```

</div>
</div>

<div class="multi-language-sample" data-lang="kotlin">
<div class="sample" markdown="1" theme="idea" mode='kotlin' data-highlight-only>

```kotlin
dependencies {
    implementation(kotlin("stdlib-jdk8"))
    testImplementation(kotlin("test-junit"))
}
```

</div>
</div>

If you use Maven, define the following dependencies within `pom.xml`:

```xml
<dependencies>
    ...
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.jetbrains.kotlin</groupId>
            <artifactId>kotlin-test-junit</artifactId>
            <version>${kotlin.version}</version>
            <scope>test</scope>
        </dependency>
</dependencies>
```

### JS

<!-- TODO -->

### MPP

<!-- TODO -->

### Native

<!-- TODO -->

## Creating Kotlin unit test

Kotlin unit tests are separate classes that provide testing functionality for pieces of an application's source code.

Here we will create a Kotlin unit test for the `concatenate()` method of the following class:

```kotlin
class Unit {
    fun concatenate(firstString: String, secondString: String ): String {
        return firstString + secondString
    }
}
```

To create a Kotlin unit test for the `Unit` class within Gradle or Maven project, create the following class in the `src/test/kotlin` directory:

```kotlin
import kotlin.test.Test
import kotlin.test.assertEquals

class UnitTest {
    @Test fun `stringsAreConcatenated`() {
        val unit = Unit()

        val result: String = unit.concatenate("one", "two")

        assertEquals("onetwo", result)
    }
}
```

>You can use spaces in the name of the test function if you put the name into backticks like this: \`strings are concatenated\`. This approach improves the readability of your code.
>
>[Read the "Improving Kotlin Tests" section](link-to-the-improving-kotlin-tests.html) for more information on how to write better Kotlin unit tests.
{:.note}

The `@Test` annotation tells a test runner to run the test function.

The test uses `assertEquals()` function to check if the `unit.concatenate()` method is working correctly.

The section ["Annotations and Assertions"](link-to-the-annotations-and-assertions-section.html) provides detailed information about the annotations and assertion functions available in the `kotlin.test` library.

## Running unit tests

You can run unit tests from an IDE interface or using a command in the command line.

If you use Gradle, run the following command:

```shell
./gradlew test
```

>You can find a detailed Gradle test report in `build/reports/tests/test/index.html`.
{:.note}

If you use Maven, run the following command:

```shell
./mvn test
```