## Truthish

A testing API inspired by [Google truth](https://github.com/google/truth) but
rewritten in Kotlin from the ground up so it can be used in Kotlin
multiplatform projects.

# Using Truthish in Your Project

*Truthish* is 100% Kotlin, so unlike some multiplatform libraries, you only need
to reference it in your `commonTest` dependencies:

```
build.gradle

kotlin {
  jvm()
  js()
  ...
  sourceSets {
    ...
    commonTest {
        dependencies {
            implementation kotlin("test-common")
            implementation kotlin("test-annotations-common")
            implementation "io.github.bitspittle:truthish:$version"
        }
    }
    ...
  }
}
```

# Editing Truthish

*Truthish* is designed to rely on Gradle and, therefore, work in any code
editing environment. However, using IntelliJ is recommended, for its top-notch
Kotlin support.

To open *Truthish* the first time, simply import the `truthish` root folder,
using Gradle as the external model. Using all default settings should work
just fine.

# Testing Truthish

## JVM

*Truthish* is a multiplatform library, meaning there really are multiple
versions of it, and you may want to test against all of them. However, it's
easiest to test against the JVM target, so let's start with that.

Simply run

`./gradlew jvmTest`

If using IntelliJ, you can double-click this task through the Gradle toolbar.

`truthish > Tasks > verification > jvmTest`

Once you've done that, IntelliJ will save it as a reusable run configuration,
at which point you can rerun the task using a debugger.

## JS

The (current) approach to running tests requires a small amount bit of manual
effort.

First run

`/.gradlew jsTest`

or, via IntelliJ

`truthish > Tasks > verification > jsTest`

Then, navigate to `js-stage` and open `index.html`. The tests automatically
run, but you can open up the dev console to see their output after the fact,
to make sure everything ran smoothly. (Truthish is intentionally chatty so
you should be able to see a lot of console output)

`js-stage` is a testing stage which symlinks to all the JS generated by
*truthish*, so whenever you rebuild, its target dependencies should be updated
automatically.

# Code coverage

As of the time of writing this README, IntelliJ code coverage does not work for
mutliplatform environments. As a result, jacoco support has been added to the
Gradle scripts, which reports code coverage using the JVM.

To see a coverage report, run

`./gradlew jvmCoverage`

Once finished, a report will be generated at:

`build/reports/jacoco/jvmCoverage/html/index.html`

Gradle should open the report automatically, but if it doesn't, that's where you
can find it.

Note that inline methods are not accounted for correctly, and do not get credit
for being used even when they are.

