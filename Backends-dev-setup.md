This guide applies to developers of Judgels' backend microservices (Jophiel, Sandalphon, Uriel, Sealtiel, Gabriel).

- [Prerequisites](#prerequisites)
- [Preparing local working directory](#preparing-local-working-directory)
- [Preparing Jophiel](#preparing-jophiel)
- [Preparing Uriel](#preparing-uriel)
- [Creating a new IDEA project](#creating-a-new-idea-project)
- [Things to note when working with IDEA](#things-to-note-when-working-with-idea)

## Prerequisites

- Java 8 JDK
- MySQL 5.7+
- Docker
- IntelliJ IDEA

## Preparing local working directory

1. Go inside the backends directory (`judgels-backends`).
1. Run:

       ./gradlew test

   This will download all required JAR dependencies and run the unit tests. Make sure the tests pass before moving on to the next sections.

## Preparing Jophiel

1. Create a new local database called `judgels_jophiel`.
1. Go inside Jophiel directory (`judgels-backends/jophiel`).
1. Copy the example config:

       cp jophiel-dist/var/conf/jophiel.yml.example jophiel-dist/var/conf/jophiel.yml

1. Open the config file `jophiel-dist/var/conf/jophiel.yml`.
1. Under `database:`, modify `url`, `user`, and `password` as necessary.
1. Check database connection and migration status:

       ../gradlew dbStatus

1. Run database migration:

       ../gradlew dbMigrate

1. Verify that there are tables generated in the database.
1. Import the seed data: `judgels/seeds/judgels_jophiel.sql`.
1. Try running it locally:

       ../gradlew run

## Preparing Uriel

1. Create a new local database called `judgels_uriel`.
1. Go inside Uriel directory (`judgels-backends/uriel`).
1. Copy the example config:

       cp uriel-dist/var/conf/uriel.yml.example uriel-dist/var/conf/uriel.yml

1. Open the config file `uriel-dist/var/conf/uriel.yml`.
1. Under `database:`, modify `url`, `user`, and `password` as necessary.
1. Check database connection and migration status:

       ../gradlew dbStatus

1. Run database migration:

       ../gradlew dbMigrate

1. Verify that there are tables generated in the database.
1. Import the seed data: `judgels/seeds/judgels_uriel.sql`.
1. Try running it locally:

       ../gradlew run

## Creating a new IDEA project

1. Go inside the backends directory (`judgels-backends`).
1. Generate a new IDEA project:

       ./gradlew idea

1. Open IDEA.
1. Click **Open**, and then select `judgels-backends/judgels-backends.ipr`. The project should now be ready.
1. Important! Whenever an **Unlinked Gradle Project** popup appears and asks you to import the Gradle project, just ignore it and close the popup.
1. Some of our libraries (Immutables, Dagger 2, Hibernate Static Metamodel) will generate classes during compilation (e.g. `judgels.jophiel.api.user.ImmutableUser`). This need to be also enabled in IDEA:
   1. Open IDEA's Preferences.
   1. Go to Build, Execution, Deployment -> Compiler -> Annotation Processors.
   1. Set the following options:

      [[images/annotation-preprocessors.png]]

   1. Save.
1. Try building the project by clicking **Build** -> **Rebuild Project**.
1. Try running the local servers from IDEA, by clicking e.g. **Run** -> **Run...** -> **jophiel-dist-run**. It is usually faster than running from terminal.

## Things to note when working with IDEA

1. If you add a new dependency (in one of the `build.gradle`s), run `./gradlew idea` again to download the JARs and to tell IDEA to pick up the new dependency.
1. If you write a new class with Immutables/Dagger/Hibernate annotations, hit **Build** -> **Rebuild Project** again to generate the corresponding classes.
1. **IMPORTANT**: If you have compilation errors, the annotation preprocessing won't be run, so you may get too many compilation errors related to generated classes being not found. There is no workaround yet.