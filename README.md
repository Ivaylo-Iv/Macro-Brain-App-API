# Macro Brain API

A small Express backend for the Macro Brain app — a demo user service that
exposes simple authentication, profile and image-entry endpoints. This repo is
intended as a lightweight backend for the frontend app and for learning / demo
purposes.

**Status:** Prototype / demo (not production-ready — see Security notes).

## Features

- Simple in-memory user store (mocked data)
- Endpoints for sign-in, registration, profile lookup and image entry count
- Uses `express`, `cors`, and `bcrypt-nodejs` for password hashing demo

## Tech stack

- Node.js + Express
- Dependencies listed in `package.json` (see `dependencies`)

## Install

1. Clone the repo and change to the project directory.
2. Install dependencies:

```bash
npm install
```

## Run

Start the server in development mode (uses `nodemon` as defined in
`package.json`):

```bash
npm start
```

The server is configured for local development. By default the example logs a
message referencing port `3000` — you may need to set a proper numeric port in
`server.js` or set `process.env.PORT` before running in environments that require
a specific port.

## API Endpoints

All examples assume the server is running on `http://localhost:3000` (adjust
the host/port as needed).

- GET `/` — returns the list of users (mock data)

  Example:

  ```bash
  curl http://localhost:3000/
  ```

- GET `/profile/:id` — get user profile by id

  Example:

  ```bash
  curl http://localhost:3000/profile/123
  ```

- POST `/signin` — sign in user (demo: compares against first user)

  Request JSON body:

  ```json
  { "email": "john@example.com", "password": "cookies" }
  ```

- POST `/register` — register a new user (adds to in-memory store)

  Request JSON body:

  ```json
  { "name": "Alice", "email": "alice@example.com", "password": "pw" }
  ```

- PUT `/image/:id` — increment `entries` count for user with given id

  Example:

  ```bash
  curl -X PUT http://localhost:3000/image/123
  ```

## Data model (in-memory)

Users are stored in an in-memory `database` object inside `server.js`. Each user
has the fields: `id`, `name`, `email`, `password`, `entries`, and `joined`.

## Security & Notes

- This project uses a mocked in-memory data store and stores example plaintext
  passwords in the demo users. Do not use this as-is in production.
- While `bcrypt-nodejs` is included and demonstrated, the current registration
  flow does not persist hashed passwords to the in-memory store — consider
  updating the flow to properly hash and store passwords before deploying.
- The `server.js` currently binds to the literal string `$PORT` — adjust to a
  numeric port or use `process.env.PORT` for real deployments.

## Contributing

This project is small and intended for demos. If you want to contribute:

- Open an issue for feature requests or bugs.
- Send a pull request with a focused change and tests if applicable.

## License

See the `LICENSE` file in this repository.
