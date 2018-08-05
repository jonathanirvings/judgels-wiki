This guide applies to Raphael.

- [Prerequisites](#prerequisites)
- [Preparing local working directory](#preparing-local-working-directory)
- [Running the frontend locally](#running-the-frontend-locally)
- [Configuring IDE](#configuring-ide)

## Prerequisites

- Yarn 1.3+
- Docker

## Preparing local working directory

1. Clone the Raphael repository.
1. Go inside the repository directory (`raphael`).
1. Copy the example config:

       cp public/var/conf/raphael.js.example public/var/conf/raphael.js

1. Run:

       yarn && yarn test

   This will download all required NPM dependencies and run the unit tests. Make sure the tests pass before moving on to the next sections.

## Running the frontend locally

The frontend can be run from terminal:

    yarn start

## Configuring IDE

You should to set up your IDE so that it runs Prettier (`node_modules/prettier/bin/prettier.js --write <current-file>`) on save.