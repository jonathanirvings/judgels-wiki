This guide is intended for Judgels developers and contributors.

## New developer onboarding

- Clone this repository.
- Follow the guide to [run Judgels from source](https://github.com/ia-toki/judgels/wiki/Running-from-source).
- For backend developers:
  - [Read basic concepts](https://github.com/ia-toki/judgels/wiki/Dev's-Guide:-Backend-basic-concepts).
  - [Set up IDE](https://github.com/ia-toki/judgels/wiki/Dev's-Guide:-Setting-up-backend-IDE).
- For frontend developers:
  - [Read basic concepts](https://github.com/ia-toki/judgels/wiki/Dev's-Guide:-Frontend-basic-concepts).
  - [Set up IDE](https://github.com/ia-toki/judgels/wiki/Dev's-Guide:-Setting-up-frontend-IDE).

## Legacy Judgels integration

We are still in the process of migrating the whole platform. Some caveats:

- Some microservices are still in their old repositories:
  - [Sandalphon](https://github.com/judgels/sandalphon)
  - [Jerahmeel](https://github.com/judgels/jerahmeel)
  - [Gabriel](https://github.com/judgels/gabriel)
- Uriel contest management can only be done using the legacy [Uriel](https://github.com/judgels/uriel).
- Upon login, Jophiel will generate cookies as well as access tokens, in order to be compatible with the old microservices.