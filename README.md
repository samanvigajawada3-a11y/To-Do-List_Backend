# To-Do List Backend

Spring Boot REST API for the To-Do List application. Tasks are stored in MongoDB.

## Requirements

- Java 21 or later
- MongoDB 6 or later (local or hosted)

## Configure and run

Set `MONGODB_URI` to a MongoDB connection string. For example, for a local MongoDB server:

```powershell
$env:MONGODB_URI = 'mongodb://localhost:27017/todolist'
```

On Windows, the included helper starts an installed MongoDB Community Server with a project-local data directory:

```powershell
.\start-mongodb.ps1
```

Keep MongoDB running, then start the API from this directory:

```powershell
.\mvnw.cmd spring-boot:run
```

The API listens on <http://localhost:8080> by default. The allowed browser origins default to `http://localhost:5173` and `http://127.0.0.1:5173`; set `CORS_ALLOWED_ORIGINS` to a comma-separated list when deploying the frontend elsewhere. The server port can be set with `PORT`.

Keep MongoDB credentials in environment variables or your hosting provider's secret settings; do not commit them.

## API

All routes use the `/api` base path:

| Method | Route | Purpose |
| --- | --- | --- |
| `GET` | `/api/tasks` | List tasks |
| `POST` | `/api/tasks` | Create a task |
| `PUT` | `/api/tasks/{id}` | Update a task |
| `DELETE` | `/api/tasks/{id}` | Delete a task |

Task JSON fields are `title`, `description`, `status` (`PENDING` or `COMPLETED`), and `dueDate` (`YYYY-MM-DD` or `null`). Titles are required and limited to 120 characters; descriptions are limited to 2,000 characters.

## Build

```powershell
.\mvnw.cmd -B package
```

The runnable JAR is written under `target/`. The Dockerfile in this repository is configured for a monorepo build context; for a standalone Docker build, adjust its `COPY` paths to the repository root before building.
