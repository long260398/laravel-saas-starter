# Laravel SaaS Starter Kit

> Production-ready Laravel 11 boilerplate — Auth, Roles, Stripe & Docker included.
> Skip 2-3 days of setup. Start building your product on day one.

**[Get the full source code on Gumroad →](https://longnguyen77.gumroad.com)**

---

## What's included

| Feature | Details |
|---|---|
| Authentication | Register, login, logout via Laravel Sanctum |
| Roles & Permissions | Admin / Manager / User + middleware |
| REST API v1 | Versioned routes, standard JSON responses |
| Admin Dashboard API | User stats, role management |
| Stripe Integration | Payment intents + webhook handling |
| Docker | Multi-stage Dockerfile + docker-compose |
| CI/CD | GitHub Actions with MySQL |
| Tests | 5 feature tests, all passing |

---

## Tech Stack

- **Laravel 11** + PHP 8.3
- **Laravel Sanctum** — API token auth
- **MySQL** + Redis
- **Stripe API**
- **Docker** + GitHub Actions

---

## Folder Structure

```
app/
├── Http/
│   ├── Controllers/
│   │   ├── Api/V1/AuthController.php
│   │   ├── Api/V1/UserController.php
│   │   └── Admin/DashboardController.php
│   ├── Middleware/RoleMiddleware.php
│   ├── Requests/Auth/
│   └── Resources/UserResource.php
├── Models/
│   ├── User.php
│   └── Role.php
├── Services/
│   ├── AuthService.php
│   └── StripeService.php
└── Traits/ApiResponse.php

database/
├── migrations/
└── seeders/RoleSeeder.php

routes/api.php
tests/Feature/AuthTest.php
Dockerfile
docker-compose.yml
.github/workflows/ci.yml
```

---

## API Endpoints

| Method | Endpoint | Auth | Role |
|--------|----------|------|------|
| POST | `/api/v1/register` | No | — |
| POST | `/api/v1/login` | No | — |
| POST | `/api/v1/logout` | Yes | any |
| GET | `/api/v1/me` | Yes | any |
| PUT | `/api/v1/users/{id}` | Yes | any |
| GET | `/api/v1/admin/stats` | Yes | admin |
| GET | `/api/v1/admin/users` | Yes | admin |
| POST | `/api/v1/admin/users/{id}/role/{role}` | Yes | admin |
| GET | `/api/v1/manage/users` | Yes | admin, manager |

---

## Sample API Responses

**POST /api/v1/register**
```json
{
  "success": true,
  "message": "Registration successful",
  "data": {
    "user": {
      "id": 1,
      "name": "John Doe",
      "email": "john@example.com",
      "roles": ["user"],
      "verified": false,
      "created_at": "2026-06-10 08:00:00"
    },
    "token": "1|abc123xyz..."
  },
  "errors": null
}
```

**GET /api/v1/admin/stats**
```json
{
  "success": true,
  "message": "Success",
  "data": {
    "total_users": 142,
    "verified_users": 130,
    "new_today": 5,
    "new_this_month": 38
  },
  "errors": null
}
```

**POST /api/v1/login — wrong password**
```json
{
  "success": false,
  "message": "The given data was invalid.",
  "data": null,
  "errors": {
    "email": ["The provided credentials are incorrect."]
  }
}
```

---

## Quick Start (after purchase)

```bash
# 1. Install dependencies
composer install

# 2. Configure environment
cp .env.example .env
php artisan key:generate

# 3. Migrate and seed default roles + admin account
php artisan migrate --seed --seeder=RoleSeeder

# 4. Start server
php artisan serve
```

Default admin account after seeding:
- Email: `admin@example.com`
- Password: `password`

---

## Run with Docker

```bash
docker compose up -d
docker compose exec app php artisan migrate --seed --seeder=RoleSeeder
```

---

## Tests

```
php artisan test

✅ test_user_can_register
✅ test_user_can_login
✅ test_login_fails_with_wrong_credentials
✅ test_authenticated_user_can_fetch_profile
✅ test_user_can_logout

Tests: 5 passed — Assertions: 14
```

---

## Get the full source code

**[Download on Gumroad — $29](https://longnguyen77.gumroad.com)**

Includes: full source code, README, .env.example, Docker setup, CI config, and free updates.

---

*Built with Laravel 11 · PHP 8.3 · 2026 Edition*
