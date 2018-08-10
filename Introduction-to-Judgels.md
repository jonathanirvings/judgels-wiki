Judgels is a competitive programming platform. Using Judgels, we can:

- create programming problems with various types, set up test data, and test solutions.
- hold programming contests with various configurations.
- manage users with different authorizations (e.g. contest supervisors, contest contestants).

## Microservices

Judgels consists of several microservices, each having a codename after a Greek archangel name.

- **Raphael** (Frontend Gate): serves the web frontend.
- **Jophiel** (User Gate): manages user accounts, authentication, and authorization.
- **Sandalphon** (Repository Gate): manages problems.
- **Uriel** (Competition Gate): manages contests.
- **Jerahmeel** (Training Gate): manages training and problem archives.
- **Sealtiel** (Message Gate): manages grading requests and responses between microservices.
- **Gabriel** (Grader): grades submissions.
