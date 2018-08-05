
The following steps show how to run the Judgels platform locally, from source, with minimal configuration. You can then further configure each microservice by following the respective docs (TBA).

1. Set up Jophiel and Raphael using the instructions from the previous section.

1. Run Jophiel server (`./gradlew run`). By default, it will listen to port 9001. To make sure that it is running correctly, hit the version endpoint:

       curl -v http://localhost:9001/api/v2/version

   It should return 200 OK with the version string. (Or 204 No Content if you run the server on IDEA.)

1. By default, Jophiel will create a superadmin account with username: `superadmin` and password: `superadmin`.

1. Run Raphael dev server (`yarn start`). By default, it will open your default web browser and navigate to `http://localhost:3000`.

1. Make sure that you can see the login page with no errors.

1. Log in to Judgels using the previously-mentioned superadmin account.

1. Make sure that you can log in successfully.

## Configurations

TBA.
