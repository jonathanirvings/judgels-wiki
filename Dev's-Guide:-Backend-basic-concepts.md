This section explains the basic knowledge required for understanding Judgels codebase on the backend side.

- [Tech stack](#tech-stack)
- [Database design](#database-design)
- [Authentication and authorization](#authentication-and-authorization)
- [REST application layers](#rest-application-layers)
- [Example request-response flow](#example-request-response-flow)
- [Further readings](#further-readings)

## Tech stack

- Java 8
- [Gradle](https://gradle.org/) as build tool
- [Palantir Baseline](https://github.com/palantir/gradle-baseline) for code style checker
- [Palantir SLS Packaging](https://github.com/palantir/sls-packaging) for packaging app
- [Palantir http-remoting](https://github.com/palantir/http-remoting) for communication between microservices
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

- Jophiel stores the session of a logged-in user as a token in the form of random string.
- An HTTP request to a backend endpoint may be accompanied by an `Authorization` header, in the form of `Bearer <token>`, meaning that the request was initiated by the user represented by the bearer token.
- Backends ask Jophiel to convert the bearers token in the authorization header into a user JID.
- Each backend has its own authorization scheme whether or not to allow certain users to hit certain endpoints.

## REST application layers

- **Service**: declares the REST API endpoints. Example: `ContestService`.
- **Resource**: implements the REST API endpoints. Example: `ContestResource`.
- **Store**: manages CRUD operations of business objects. Example: `ContestStore`.
- **Dao**: declares the CRUD operations in database. Example: `ContestDao`.
- **HibernateDao**: implements the CRUD operations by executing SQL queries. Example: `ContestHibernateDao`.
- **Model**: represents a row in a database. Example: `ContestModel`.

## Example request-response flow

Say we hit Uriel with this HTTP request:

    curl -XGET -H "Authorization: Bearer token123" http://localhost:9004/api/v2/contests/JIDCONTabcdefghijklmnopqrst

The following is a simplified sequence of events that will happen.

1. The endpoint lives as a JAX-RS annotated method `getContest()` in `ContestService` interface.
1. The implementation class, `ContestResource`, is registered as a Jersey resource via Dropwizard.
1. The resource is then invoked, with the authorization header passed as an argument.
1. Using `ActorChecker`, the authorization containing bearer token is converted into user JID representing the currently logged-in user (actor).
1. The resource method asks `ContestRoleChecker`, whether the actor is allowed to view the contest.
1. The resource method asks the store `ContestStore` to get the `Contest` by its JID.
1. The store asks the DAO `ContestDao` to get the database row in the contest table by its JID.
1. The DAO implementation, `ContestHibernateDao`, executes the appropriate SQL query to get the row.
1. The store gets the row, and converts the row (`ContestModel`) into business object (`Contest`).
1. The store returns the `Contest` to the resource method.
1. The resource method returns the `Contest`.
1. The return value is then converted into an HTTP response, with a JSON body representing the contest object.

## Further readings

It is important to also read the documentation of these libraries in order to help understand Judgels backend codebase:

- [Dropwizard](https://www.dropwizard.io/)
  - Jersey, JAX-RS
  - configs, bundles
- [Dagger](https://google.github.io/dagger/users-guide):
  - components, modules, providers, singletons
  - how dependency injections work
- [Immutables](https://immutables.github.io/)
  - immutability, builders, precondition checks
- [Palantir http-remoting](https://github.com/palantir/http-remoting)
  - how microservices talk to each other
  - how microservices handle errors from each other