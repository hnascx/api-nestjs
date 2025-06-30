# NestJS Forum API

A forum API built with **NestJS**, following Clean Architecture, DDD, and SOLID principles. It enables account creation, authentication, questions, answers, comments, attachments, and notifications.

## Table of Contents

- [Architecture](#architecture)
- [Technologies & Libraries](#technologies--libraries)
- [Database & ORM](#database--orm)
- [Infrastructure (Docker)](#infrastructure-docker)
- [Environment Configuration](#environment-configuration)
- [Main Features](#main-features)
- [Main Endpoints](#main-endpoints)
- [Available Scripts](#available-scripts)
- [Testing](#testing)
- [License](#license)

---

## Architecture

- **NestJS**: Main framework, modular, with dependency injection.
- **Clean Architecture**: Clear separation between domain, application, infrastructure, and interfaces.
- **DDD**: Well-defined entities, aggregates, repositories, and use cases.
- **SOLID**: Principles applied throughout the codebase.

## Technologies & Libraries

- **NestJS** (`@nestjs/*`)
- **Prisma ORM** (`@prisma/client`, `prisma`)
- **PostgreSQL** (relational database)
- **Redis** (cache)
- **JWT** (`@nestjs/jwt`, `passport-jwt`)
- **BcryptJS** (password hashing)
- **Zod** (schema validation)
- **Cloudflare** (attachments storage)
- **Vitest** (unit and e2e testing)
- **ESLint/Prettier** (code style)

## Database & ORM

- **Prisma** as ORM.
- **PostgreSQL** as the main database.
- Models: User, Question, Answer, Comment, Attachment, Notification.
- Role support (STUDENT, INSTRUCTOR).

## Infrastructure (Docker)

- `docker-compose.yml` provides:
  - **PostgreSQL** (port 5432)
  - **Redis** (port 6379)
- Persistent volumes for data.

## Environment Configuration

Required environment variables (see `src/infra/env/env.ts`):

- `DATABASE_URL`
- `JWT_PRIVATE_KEY`
- `JWT_PUBLIC_KEY`
- `CLOUDFLARE_ACCOUNT_ID`
- `AWS_BUCKET_NAME`
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `REDIS_HOST` (default: 127.0.0.1)
- `REDIS_PORT` (default: 6379)
- `REDIS_DB` (default: 0)
- `PORT` (default: 3333)

## Main Features

- **JWT Authentication** (login, register)
- **CRUD for Questions and Answers**
- **Comments on questions and answers**
- **Best answer selection**
- **Attachment upload (S3/Cloudflare)**
- **Notifications**
- **Pagination in listings**
- **Data validation with Zod**

## Main Endpoints

- `POST /accounts` — Create account
- `POST /sessions` — Authenticate (login)
- `POST /questions` — Create question
- `GET /questions` — List recent questions (paginated)
- `GET /questions/:slug` — Get question by slug
- `PUT /questions/:id` — Edit question
- `DELETE /questions/:id` — Delete question
- `POST /questions/:questionId/answers` — Answer question
- `PUT /answers/:id` — Edit answer
- `DELETE /answers/:id` — Delete answer
- `PATCH /answers/:answerId/choose-as-best` — Choose best answer
- `POST /questions/:questionId/comments` — Comment on question
- `POST /answers/:answerId/comments` — Comment on answer
- `DELETE /questions/comments/:id` — Delete question comment
- `DELETE /answers/comments/:id` — Delete answer comment
- `POST /attachments` — Upload attachment
- `PATCH /notifications/:notificationId/read` — Mark notification as read

## Available Scripts

- `start`, `start:dev`, `start:prod` — Start the API
- `test`, `test:watch`, `test:e2e` — Unit and e2e tests
- `lint`, `format` — Lint and formatting

## Testing

- **Vitest** for unit and e2e tests.
- Coverage for use cases, controllers, and integrations.