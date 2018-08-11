This section explains the basic knowledge required for understanding Judgels codebase on the frontend side.

- [Tech stack](#tech-stack)
- [Authentication](#authentication)
- [Application layers](#application-layers)

## Tech stack

- [TypeScript](https://www.typescriptlang.org/)
- [Prettier](https://prettier.io/)
- [Yarn](https://yarnpkg.com/)
- [React](https://reactjs.org/) with [create-react-app-typescript](https://github.com/wmonk/create-react-app-typescript)
- [Redux](https://redux.js.org/)
- [Palantir Blueprint](https://blueprintjs.com/)

## Authentication

- Access token of the currently logged-in user is stored in local storage using [redux-persist](https://github.com/rt2zz/redux-persist).
- When hitting backend endpoints, the token is passed as an `Authorization` header in the HTTP request.

## Application layers

- **API modules**: TypeScript representation of backend endpoints. Example: `user.ts`
- **Actions**: Redux thunks that handle backend API calls. Example: `userActions.ts`