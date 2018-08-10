This section explains the basic knowledge required for understanding Judgels codebase.

## Tech stack

Backends (Jophiel, Sandalphon, Uriel, Sealtiel, Jerahmeel):
- Java 8
- [Dropwizard](https://www.dropwizard.io/) for main REST server app
- [MySQL](https://www.mysql.com/) for database
- [JPA](https://en.wikipedia.org/wiki/Java_Persistence_API) implemented with [Hibernate](http://hibernate.org/orm/) for ORM
- [Caffeine](https://github.com/ben-manes/caffeine) for cache
- [Dagger](https://google.github.io/dagger/) for dependency injection
- [Immutables](https://immutables.github.io/) for objects immutability
- [Guava](https://github.com/google/guava) for collections

Frontend (Raphael):
- [TypeScript](https://www.typescriptlang.org/)
- [Yarn](https://yarnpkg.com/)
- [React](https://reactjs.org/) with [CRA-TypeScript](https://github.com/wmonk/create-react-app-typescript)
- [Redux](https://redux.js.org/)
- [Blueprint](https://blueprintjs.com/)