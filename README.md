# Android Archetype

An empty Android application and library with initial configuration for boring stuff.

The intention of this project is to have a base from where projects should start. Normally there are plenty of configurations we need to make on top of the new project template so that we can use the project safely. This project provides some of them already configured either as a reference or as a base for a clone. 

It is important to notice that there several opinions here that may not be universal truth. Though they all can be further configured to your liking.

What we provide here is:

## `app` and `library`

Most applications we write nowadays have two or more modules: one with the main application used by smartphones and tablets and another with code that might be re-used by other modules be it connection handling, custom validaton logic and etc.

This project is empty but it must contain a package. Remember to update the package definition in:

- Directories
- build.gradle

## Gradle

This project is configured to use a more recent version of the Gradle build system. Currently it is at `3.2.1`. 

See more detailed explanation about the structure of build files and plugins in the [GRADLE.md](#/docs/GRADLE.md)

## Signing configuration

Plenty of libraries check that your app is your app by comparing its package signature. Google and Facebook are common examples. It is good practice to have a default shared debug keystore to avoid having several keys registered which are tied to one developer's machine. This project provides a default debugg keystore in folder `/distribution`.

Also, it expects that for release packages to be signed you need to provide the parameters as environment variables.

## `.gitignore`

The default .gitignore file generated by Android Studio is quite limited. This project provides more configurations to be excluded like MacOS specific files, JetBrains IDE files and etc.

We believe that IDE configuration should not be a part of the repository and therefore we don't include *.iml files.

## Linters

This project already enables extra linters like Checkstyle, PMD and FindBugs. Their configuration files are segregated in `/tools/linters`.

### Checkstyle

We enforce the [Google convention for Java](https://google.github.io/styleguide/javaguide.html) as the standard code style. This is the standard used by the Java community which we believe is way more adopted than the style advocated [here](https://source.android.com/source/code-style.html). The later should be used only throughout the AOSP source base. 

The checkstyle configuration is taken from http://checkstyle.sourceforge.net/google_style.html .

### Findbugs and PMD

The configuration is ready to take any exclusions or filter inclusions you might want to add. They all live in the folder `/tools/linters`.


## Formatting according to the style in Android Studio

In order to make it easy to abide to the formatting rules defined by Checkstyle, this project provides two script files that can be used to import the configuration into Android Studio. In order to use them all is needed is to run the scripts:

``` sh
# In Linux and MacOS
./tools/install-google-style.sh

# in Windows
tools\install-google-style.bat
```

## JaCoCo (Java Code Coverage) unified report generation

This project has a custom Gradle configuration to generate a report that unifies the coverage statistics of local and instrumented tests. This is custom task is defined in file `/tools/jacoco.gradle` and follows the discussion presented in [this blog post](https://medium.com/@rafael_toledo/setting-up-an-unified-coverage-report-in-android-with-jacoco-robolectric-and-espresso-ffe239aaf3fa).

## Test Butler

We believe that testing is a fundamental part of any development effort. In mobile there is a great discussion whether we can use only local testing or if we should use an instrumented setup. We strongly believe that both approaches have their role in development of Android applications. More about our point of view in [this blog post](https://medium.com/concrete-solutions/android-local-or-instrumented-tests-9da545af7777).

To have better tests in emulators we strongly advice using [Test Butler](https://github.com/linkedin/test-butler). This project has this dependency already configured with a custom `AndroidJUnitTestRunner` as per Test Butler's documentation. 

Another important thing is that to use it, you need to install Test Butler apk in the emulators in question. This project has a custom Gradle task that installs the APK automatically in all connected emulators. It resides in `/tools/test-butler.gradle`.

## Retrolambda

Modern development of Android applications use Java 8 features through Retrolambda. This project has it already configured. In a future this will change to Jack compiler toolkit.

## Build types

This project has standard three build types configured: debug, QA and release. 

## Test dependencies

We have opted to configure only the basic test frameworks like Espresso for instrumented tests and Robolectric + Hamcrest for local tests. The only exception to this rule is a wrapper of Square's MockWebServer that provides a fixture based testing approach to ease mocking HTTP interactions. That is [RequestMatcher](https://github.com/concretesolutions/requestmatcher). 

## Documentation

This project has a set of documentation for the project's team to implement:

  - [GIT](/docs/GIT.md)
  - [Source code styleguide](/docs/STYLEGUIDE.md)
  - [Gradle organization](/docs/GRADLE.md)
  - [Testing best practices](/docs/TESTING.md)
  - [Dependencies](/docs/DEPENDENCIES.md)
  - [Application Architecture](/docs/ARCHITECTURE.md)


