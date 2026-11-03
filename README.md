# Pressroom News Platform

Beginner-friendly monorepo: Next.js public site, NestJS API gateway, separate news and auth services, PostgreSQL + Prisma.

## Deliberately simple infrastructure
No Redis, RabbitMQ, or Docker. Services communicate with normal HTTP requests. Install PostgreSQL directly on your computer and create a database named `pressroom`.

## Requirements
- Node.js 22 LTS
- pnpm 10 (`corepack enable`)
- PostgreSQL 16+

## Setup
1. Install PostgreSQL and create database `pressroom`.
2. Copy `.env.example` to `.env`; update the database password and JWT secrets.
3. Run `pnpm install`.
4. Run `pnpm --filter @pressroom/database db:generate`.
5. Run `pnpm --filter @pressroom/database db:migrate`.
6. Run `pnpm dev`.

Website: http://localhost:3000
Gateway health: http://localhost:4000/api/health
News service health: http://localhost:4101/health
Auth service health: http://localhost:4102/health

## Current status
The public website reads published articles from PostgreSQL through the gateway/news service. The admin page is a visual starter only. Real admin login, permissions, article create/edit/publish endpoints, image uploads, and scheduling are follow-up milestones. Do not deploy publicly before authentication and authorization are implemented.

## Structure
- `apps/web`: Next.js public site and admin UI starter
- `services/api-gateway`: frontend-facing REST gateway
- `services/news-service`: article API and database access
- `services/auth-service`: authentication service foundation
- `packages/database`: Prisma schema and client
- `packages/shared`: shared types
