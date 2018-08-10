This section explains the basic knowledge required for understanding Judgels codebase on the backend side.

- [Tech stack](#tech-stack)
- [Database design](#database-design)
- [Authentication and authorization](#authentication-and-authorization)
- [REST application layers](#rest-application-layers)

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
- Each object in Judgels has a database-generated auto-increment ID. We don't use this ID for referencing objects.
- Instead, each object in Judgels has a unique identifier called **JID** (Judgels ID) in the form of **JIDXXXXYYYYYYYYYYYYYYYYYYYY**, where X is object type code and Y is a shortened UUID. For example: **JIDUSER7uMucIkm1exJTu7sJvxR**.
- JIDs as unique identifiers enables easy backup or migration between different Judgels app instances.
- In addition to JID, each object may have user-friendly ID. For example: usernames, problem slugs, contest slugs.
- Complex properties are stored either on disk database as JSON strings. For example: grading result details.
- Additionally, each object may have the following columns:
  - **createdBy**, **createdAt**, **createdIp**: user, time, and IP when this object is created.
  - **updatedBy**, **updatedAt**, **updatedIp**: user, time, and IP when this object is updated.

## Authentication and authorization

An HTTP request to a Judgels backend endpoint may be accompanied by an `Authorization` header, in the form of `Bearer <token>`. It means that the request was initiated by the user represented by the bearer token. The backend will ask Jophiel to convert the bearer token into a user JID. Then, the backend will decide whether the user JID is allowed to access the endpoint. 

## REST application layers

- **Service**: declares the REST API endpoints. Example: `ContestService`.
- **Resource**: implements the REST API endpoints. Example: `ContestResource`.=
- **Store**: manages CRUD operations of business objects. Example: `ContestStore`.
- **Dao**: declares the CRUD operations in database. Example: `ContestDao`.
- **HibernateDao**: implements the CRUD operations in database. Example: `ContestHibernateDao`.
- **Model**: represents a row in a database. Example: `ContestModel`.