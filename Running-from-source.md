The following steps show how to run the Judgels platform locally, from source, with minimal configuration. You can then further configure each microservice by following the respective docs (TBA).

1. Set up Jophiel, Uriel, and Raphael using the instructions from the previous sections.

1. Import seed data for Jophiel and Uriel databases. The data can be found inside `seeds` directory.

1. Run Jophiel server (`../gradlew run` inside `judgels-backends/jophiel`). By default, it will listen to port 9001. To make sure that it is running correctly, hit the version endpoint:

       curl -v http://localhost:9001/api/v2/version

   It should return 200 OK with the version string.

1. Similary, run Uriel server. By default, it will listen to port 9003.

1. Run Raphael dev server (`yarn start` inside `judgels-frontends/raphael`). By default, it will open your default web browser and navigate to `http://localhost:3000`.

1. Make sure that you can see the login page with no errors.

1. Log in to Judgels using superadmin account (username: `superadmin`, password: `superadmin`).

1. Make sure that you can log in successfully.
