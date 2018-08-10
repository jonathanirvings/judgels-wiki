This section explains how to run the Judgels platform locally from source, with default configuration. This is a good starting point for new developers to ensure that they can run Judgels on their machine.

- [Prerequisites](#prerequisites)
- [Setting up backends project](#setting-up-backends-project)
- [Setting up frontend project](#setting-up-frontend-project)
- [Setting up Jophiel](#setting-up-jophiel)
- [Setting up Uriel](#setting-up-uriel)
- [Running the microservices](#running-the-microservices)

## Prerequisites

- Java 8 JDK
- MySQL 5.7+
- Yarn 1.3+
- Docker
- IntelliJ IDEA

## Setting up backends project

1. Go to the backends directory (`judgels-backends`).
1. Run: `./gradlew check`

   This will download all required JAR dependencies, and run all unit and integration tests. Note that it may take quite a while for the first time.

1. Make sure the tests pass before moving on to the next sections.

## Setting up frontend project

1. Go to Raphael directory (`judgels-frontends/raphael`).
1. Run: `yarn && yarn test`

   This will download all required NPM dependencies and run the tests. Note that it may take quite a while for the first time.

1. Make sure the tests pass before moving on to the next sections.

## Setting up Jophiel

1. Create a new local database called `judgels_jophiel`.
1. Go to Jophiel directory (`judgels-backends/jophiel`).
1. Copy the example config:

       cp jophiel-dist/var/conf/jophiel.yml.example jophiel-dist/var/conf/jophiel.yml

1. Open the config file `jophiel-dist/var/conf/jophiel.yml`.
1. Under `database:`, modify `url`, `user`, and `password` as necessary.
1. Run database migration:

       ../gradlew dbMigrate

1. Verify that there are tables generated in the database.
1. Import the seed data to the database: `seeds/judgels_jophiel.sql`.
1. Verify that there data generated in the database.

## Setting up Uriel

The steps are similar to Jophiel's above. Just replace replace all occurrences of `jophiel` to `uriel`.

## Running the microservices

1. Run Jophiel server:

   - Go to `judgels-backends/jophiel`.
   - Run: `../gradlew run`.
   - By default, it will listen to port 9001.
   - To make sure that it is running correctly, hit the version endpoint: `http://localhost:9001/api/v2/version`. It should return the current version string.

1. Similary, run Uriel server. By default, it will listen to port 9004.
1. Run Raphael server:

   - Go to `judgels-frontends/raphael`.
   - Run: `yarn start`.
   - By default, it will open your default web browser and navigate to `http://localhost:3000`.

1. Make sure that you can see the Judgels homepage with no errors.
1. Log in to Judgels using superadmin account (username: `superadmin`, password: `superadmin`).
1. Make sure that you can log in successfully.

Congratulations, you have successfully run Judgels from source!