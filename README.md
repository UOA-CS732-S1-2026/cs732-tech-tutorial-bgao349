# Bi Aviation

A full-stack **Aircraft Maintenance & Dispatch Management System** built with a React + Vite frontend and a Spring Boot backend. The platform provides a unified dashboard for managing aircraft, maintenance plans, maintenance tasks, ground staff, and daily dispatching workflows.

---

## Features

- **Aircraft Management** — Maintain the aircraft fleet, view aircraft details, and track maintenance history.
- **Maintenance Plan & Task Management** — Create, assign and track maintenance plans and their sub-tasks.
- **Dispatching Management** — Organize dispatching records and manage the staff involved in each job.
- **Staff Management** — Maintain the list of ground/maintenance staff available for assignment.
- **Paginated Lists & Filtering** — Server-side pagination powered by PageHelper for responsive browsing of large datasets.

---

## Tech Stack

### Frontend (`bi-aviation/`)
- **React 19** + **Vite 7**
- **Ant Design 6** for UI components
- **Redux Toolkit** + **React-Redux** for state management
- **React Router v7** for routing
- **Axios** for HTTP requests
- **ESLint** for code quality

### Backend (`backend/bi-avaition-backend/`)
- **Spring Boot 4.0.2** (Spring Web MVC)
- **Java 17**
- **MyBatis** (`mybatis-spring-boot-starter`) for data access
- **MySQL** as the relational database
- **PageHelper** for pagination
- **Lombok** for boilerplate reduction
- **Maven** as the build tool

---

## Project Structure

```
Bi Aviation/
├── bi-aviation/                     # React + Vite frontend
│   ├── src/
│   │   ├── apis/                    # Axios-based API modules
│   │   ├── components/              # Reusable UI components (Button, Select, Table)
│   │   ├── hooks/                   # Custom React hooks
│   │   ├── layouts/                 # Layout components
│   │   ├── pages/                   # Route-level pages
│   │   │   ├── aircraft/            # AircraftList, AircraftMaintenance
│   │   │   └── dispatching_management/  # dispatchinglist, stafflist
│   │   ├── router/                  # React Router configuration
│   │   ├── store/                   # Redux Toolkit store
│   │   └── utils/                   # Helpers (e.g., Axios instance)
│   ├── vite.config.js
│   └── package.json
│
└── backend/bi-avaition-backend/     # Spring Boot backend
    ├── src/main/java/org/example/biavaitionbackend/
    │   ├── controller/              # REST controllers
    │   ├── service/ + service/impl/ # Service layer
    │   ├── mapper/                  # MyBatis mappers
    │   ├── pojo/                    # Entity / Result / PageResult
    │   └── dto/                     # Data Transfer Objects
    ├── src/main/resources/
    │   ├── application.yml          # Datasource & MyBatis config
    │   └── org/...                  # Mapper XML files
    └── pom.xml
```

---

## Prerequisites

Before starting, make sure you have the following installed:

- **Node.js** 18+ (recommended 20+) and **npm**
- **JDK 17**
- **Maven 3.8+** (or use the bundled `mvnw` wrapper)
- **MySQL 8+** running locally

---

## Getting Started

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd "Bi Aviation"
```

### 2. Set up the database

Create the MySQL database used by the backend:

```sql
CREATE DATABASE aircraft DEFAULT CHARACTER SET utf8mb4;
```

Then import your schema and seed data (tables for `aircraft`, `maintenance_plan`, `maintenance_task`, `staff`, etc.) into the `aircraft` database.

If your MySQL credentials differ from the defaults, update `backend/bi-avaition-backend/src/main/resources/application.yml`:

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/aircraft?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=Pacific/Auckland
    driver-class-name: com.mysql.cj.jdbc.Driver
    username: root
    password: 123456
```

### 3. Start the backend

```bash
cd backend/bi-avaition-backend

# On macOS / Linux
./mvnw spring-boot:run

# On Windows
mvnw.cmd spring-boot:run
```

The backend will start on **http://localhost:8080**.

Alternatively, you can build a runnable JAR:

```bash
./mvnw clean package
java -jar target/bi-avaition-backend-0.0.1-SNAPSHOT.jar
```

### 4. Start the frontend

In a new terminal:

```bash
cd bi-aviation
npm install
npm run dev
```

The dev server will start (by default on **http://localhost:5173**). Vite is configured to proxy `/api/*` requests to the backend at `http://localhost:8080`, so no CORS configuration is required during development.

### 5. Open the app

Open your browser and navigate to the URL printed by Vite (e.g. `http://localhost:5173`).

---

## Available Scripts

### Frontend (`bi-aviation/`)

| Script            | Description                                |
|-------------------|--------------------------------------------|
| `npm run dev`     | Start the Vite development server with HMR |
| `npm run build`   | Build the production bundle                |
| `npm run preview` | Preview the production build locally       |
| `npm run lint`    | Run ESLint on the project                  |

### Backend (`backend/bi-avaition-backend/`)

| Command                      | Description                                  |
|------------------------------|----------------------------------------------|
| `./mvnw spring-boot:run`     | Run the Spring Boot application              |
| `./mvnw clean package`       | Build a runnable JAR in `target/`            |
| `./mvnw test`                | Run the unit tests                           |

---

## Production Build

1. Build the frontend:
   ```bash
   cd bi-aviation
   npm run build
   ```
   The static assets will be output to `bi-aviation/dist/`.

2. Build the backend JAR:
   ```bash
   cd backend/bi-avaition-backend
   ./mvnw clean package -DskipTests
   ```

3. Deploy the JAR to your server and serve the frontend `dist/` bundle from any static host (Nginx, S3, etc.). Remember to either configure your reverse proxy to forward `/api` to the backend, or update the frontend API base URL accordingly.

---


