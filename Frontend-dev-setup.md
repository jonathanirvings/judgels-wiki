This guide applies to developers of Judgels' only frontend microservice, Raphael.

- [Prerequisites](#prerequisites)
- [Preparing local working directory](#preparing-local-working-directory)
- [Running the frontend locally](#running-the-frontend-locally)
- [Configuring IDE](#configuring-ide)

## Prerequisites

- Yarn 1.3+
- IntelliJ IDEA (optional, or another IDE)

## Preparing local working directory

1. Go inside Raphael directory (`judgels/judgels-frontends/raphael`).
1. Copy the example config:

       cp public/var/conf/raphael.js.example public/var/conf/raphael.js

1. Run:

       yarn install
       yarn test

   This will download all required NPM dependencies and run the unit tests. Make sure the tests pass before moving on to the next sections.

## Running the frontend locally in dev mode

The frontend can be run from terminal:

    yarn start

## Configuring linters on IDE

You should to set up your IDE so that it runs Prettier (`node_modules/prettier/bin/prettier.js --write <current-file>`) on save.

In particular, if you use IntelliJ IDEA:

1. Open IDEA's Preferences.
1. Go to Tools -> File Watchers.
1. Add the following two entries: Prettier TS and Prettier TSX as depicted below.

[[images/prettier-ts.png]]
[[images/prettier-tsx.png]]