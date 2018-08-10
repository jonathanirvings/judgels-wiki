This section explains the basic knowledge required for understanding Judgels codebase on the backend side.

- [Tech stack](#tech-stack)
- [Database design](#database-design)
- [Application layers](#application-layers)

## Tech stack

- Java 8
- [Dropwizard](https://www.dropwizard.io/) for main REST server app
- [MySQL](https://www.mysql.com/) for database
- [JPA](https://en.wikipedia.org/wiki/Java_Persistence_API) implemented with [Hibernate](http://hibernate.org/orm/) for ORM
- [Caffeine](https://github.com/ben-manes/caffeine) for cache
- [Dagger](https://google.github.io/dagger/) for dependency injection
- [Immutables](https://immutables.github.io/) for objects immutability
- [Guava](https://github.com/google/guava) for collections

## Database design

Judgels adapts the database design explained here: [Phabricator Database Schema](https://secure.phabricator.com/book/phabcontrib/article/database/). In particular:

- Here, by "objects" we mean objects as in REST resources. For example: users, problems, contests.
- Each object in Judgels has a **JID** (Judgels ID) in the form of **JIDXXXXYYYYYYYYYYYYYYYYYYYY**, where X is object type code and Y is a shortened UUID. For example: **JIDUSER7uMucIkm1exJTu7sJvxR**.
- No foreign keys, since we want that objects can be migrated between different Judgels app instances.
- Properties that have complex structure are stored either on disk database as JSON strings. For example: grading result details.
- Additionally, each object may have the following columns:
  - **createdBy**, **createdAt**, **createdIp**: user, time, and IP when this object is created.
  - **updatedBy**, **updatedAt**, **updatedIp**: user, time, and IP when this object is updated.

## Application layers

1. **Service**: declares the REST API endpoints. Example: `ContestService`.
1. **Resource**: implements the REST API endpoints. Example: `ContestResource`.
1. **Role checker**: authorizes REST API calls. Example: `ContestRoleChecker`.
1. **Store**: manages CRUD operations of business objects. Example: `ContestStore`.
1. **Dao**: declares the CRUD operations in database. Example: `ContestDao`.
1. **HibernateDao**: implements the CRUD operations in database. Example: `ContestHibernateDao`.
1. **Model**: represents a row in a database. Example: `ContestModel`.