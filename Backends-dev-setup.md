- [Prerequisites](#prerequisites)
- [Preparing local working directory](#preparing-local-working-directory)
- [Preparing local database](#preparing-local-database)
- [Running the server locally](#running-the-server-locally)
- [Creating a new IDEA project](#creating-a-new-idea-project)
- [Things to note when working with IDEA](#things-to-note-when-working-with-idea)

## Prerequisites

- Java 8 JDK
- MySQL 5.7+
- Docker
- [IntelliJ IDEA](https://www.jetbrains.com/idea/) (the "official" IDE for Judgels development)

## Preparing local working directory

1. Clone the Jophiel repository.
1. Go inside the repository directory (`jophiel`).
1. Copy the example config:

       cp jophiel-dist/var/conf/jophiel.yml.example jophiel-dist/var/conf/jophiel.yml

1. Run:

       ./gradlew test

   This will download all required JAR dependencies and run the unit tests. Make sure the tests pass before moving on to the next sections.

## Preparing local database

1. Create a new database called `judgels_jophiel`.
1. Open the config file `jophiel-dist/var/conf/jophiel.yml`.
1. Under `database:`, modify `url`, `user`, and `password` as necessary.
1. Check database connection and migration status:

       ./gradlew dbStatus

1. Run database migration:

       ./gradlew dbMigrate

## Running the server locally

The server can be run from terminal:

    ./gradlew run

## Creating a new IDEA project

1. Generate a new IDEA project:

       ./gradlew idea

1. Open IDEA.
1. Click **Open**, and then select `jophiel/jophiel.ipr`. The project should now be ready.
1. Important! Whenever an **Unlinked Gradle Project** popup appears and asks you to import the Gradle project, just ignore it and close the popup.
1. Some of our libraries (Immutables, Dagger 2, Hibernate Static Metamodel) will generate classes during compilation (e.g. `judgels.jophiel.api.user.ImmutableUser`). This need to be also enabled in IDEA:
   1. Open IDEA's **Preferences**.
   1. Go to Build, Execution, Deployment -> Compiler -> Annotation Processors
   1. Set the following options:
      - Tick **Enable annotation processing**.
      - Tick **Obtain processors from project classpath**.
      - **Store generated sources relative to**: select **Module content root**
   1. Save.
1. Try building the project by clicking **Build** -> **Rebuild Project**.
1. Try running the local server from IDEA, by clicking **Run** -> **Run...** -> **jophiel-dist-run**. It is usually faster than running from terminal.

## Things to note when working with IDEA

1. If you add a new dependency (in one of the `build.gradle`s), run `./gradlew idea` again to download the JARs and to tell IDEA to pick up the new dependency.
1. If you write a new class with Immutables/Dagger/Hibernate annotations, hit **Build** -> **Rebuild Project** again to generate the corresponding classes.
1. **IMPORTANT**: If you have compilation errors, the annotation preprocessing won't be run, so you may get too many compilation errors related to generated classes being not found. There is no workaround yet.