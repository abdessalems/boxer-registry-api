<div align="center">

# 🥊 Boxer Registry — REST API

**Backend service for managing boxer profiles, users and authentication.**

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5.3-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Express](https://img.shields.io/badge/Express-4.18-000000?style=flat-square&logo=express&logoColor=white)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=flat-square&logo=mariadb&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-22C55E?style=flat-square)

</div>

---

A REST API built with **Express** and **TypeScript** on a **MariaDB** connection pool. It exposes boxer profiles — record, physique, gym, trainer — along with user accounts and a login flow. Companion frontend: [**Boxer_register**](https://github.com/abdessalems/Boxer_register) (Vue 3).

---

## API

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/` | Service health / index |
| `GET` | `/api/boxers` | List all boxers |
| `GET` | `/api/boxers/:id` | Fetch a single boxer |
| `POST` | `/api/boxers` | Create a boxer |
| `PUT` | `/api/boxers/:id` | Update a boxer |
| `DELETE` | `/api/boxers/:id` | Delete a boxer |
| `GET` | `/api/boxers/favorites` | List favourite boxers |
| `GET` | `/api/users` | List users |
| `POST` | `/api/users` | Register a user |
| `POST` | `/api/auth/login` | Authenticate |
| `POST` | `/api/auth/logout` | End the session |

### Boxer model

`first_name` · `last_name` · `email` · `height` · `weight` · `fight_number` · `win` · `losses` · `kos` · `gym_number` · `title` · `image_link` · `trainer_name`

---

## Architecture

```
src/
├── server/
│   ├── server.ts        Express app, MariaDB pool, route handlers
│   └── requests.http    Ready-to-run HTTP requests for every endpoint
├── model/
│   ├── boxer.ts         Boxer domain model
│   └── User.ts          User domain model
├── app.ts
└── main.ts
public/                  Bundled frontend build served as static files
```

Data access goes through a pooled `mariadb` connection (limit 5). The service also serves the compiled frontend from `public/`, so the API and the SPA can run from a single process.

---

## Getting started

**Requirements:** Node.js 18+, MariaDB (or MySQL).

```bash
git clone https://github.com/abdessalems/Boxer_BackEnd.git
cd Boxer_BackEnd
npm install
```

Configure the database via environment variables — the code falls back to local development defaults if they are unset:

```bash
DB_HOST=localhost
DB_USER=boxer
DB_PASSWORD=your_password
DB_DATABASE=boxer_db
```

Run it in watch mode (`nodemon` + `ts-node`):

```bash
npm start
```

`src/server/requests.http` contains a request for every endpoint — open it in VS Code with the REST Client extension to exercise the API without a frontend.

---

## Status

Coursework project (Full-Stack JS). Functional, but with known gaps: no automated test suite is wired up (`npm test` is a stub), and passwords are stored without hashing — fine for a local exercise, not for deployment.

---

## License

[MIT](LICENSE) © 2023 Abdessalem Saadaoui
