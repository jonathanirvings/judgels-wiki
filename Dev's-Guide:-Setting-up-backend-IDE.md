This sections explains how to set up IDE for local backend development.

- [Prerequisites](#prerequisites)
- [Setting up IDEA project](#setting-up-idea-project)
- [Running server from IDEA](#running-server-from-idea)
- [Miscellaneous](#miscellaneous)

## Prerequisites

We highly recommend using IntelliJ IDEA. This section will only cover setup on IDEA.

## Setting up IDEA project

1. Go to the backends directory (`judgels-backends`).
1. Generate a new IDEA project: `./gradlew idea`.
1. Open IDEA.
1. Click **Open**, and then select `judgels-backends/judgels-backends.ipr`. The project should now be ready.
1. **IMPORTANT**: Whenever an **Unlinked Gradle Project** popup appears and asks you to import the Gradle project, just ignore it and close the popup.
1. Some of our libraries (Immutables, Dagger 2, Hibernate Static Metamodel) will generate classes during compilation (e.g. `judgels.jophiel.api.user.ImmutableUser`). This need to be also enabled in IDEA:
   1. Open **Preferences**.
   1. Go to **Build, Execution, Deployment** -> **Compiler** -> **Annotation Processors**.
   1. Set the following options:

      [[images/annotation-preprocessors.png]]

1. Try building the project by clicking **Build** -> **Rebuild Project**.
1. After this, the generated classes should be created. However, they are not marked as source classes yet. To fix this, run `./gradlew idea` again, and then rebuild again.
1. If the build succeeded, you're all set!

## Running server from IDEA

You can run or debug the server directly from IDEA, by clicking e.g. **Run** -> **Run...** -> **jophiel-dist-run**. It is usually faster than running from terminal.

## Miscellaneous

1. If you add a new dependency (in one of the `build.gradle`s), run `./gradlew idea` again to download the JARs and to tell IDEA to pick up the new dependency.
1. If you write a new class with Immutables/Dagger/Hibernate annotations, hit **Build** -> **Rebuild Project** again to generate the corresponding classes.
1. **IMPORTANT**: If you have compilation errors, the annotation preprocessing won't be run, so you may get too many compilation errors related to generated classes being not found. There is no workaround yet.