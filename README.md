# EDUQUEST

[![Java](https://img.shields.io/badge/Java-21-007396?logo=java&logoColor=white)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.3-6DB33F?logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![MySQL](https://img.shields.io/badge/MySQL-8.x-4479A1?logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Stripe](https://img.shields.io/badge/Stripe-Payments-635BFF?logo=stripe&logoColor=white)](https://stripe.com/)

A scalable education platform backend built with Java 21 and Spring Boot 3.4.3. EduQuest supports course management, quizzes, Stripe payments, and role-based access control.

## ✨ Features
- JWT-based authentication with ADMIN, TEACHER, and STUDENT roles
- Course management with file, image, and video uploads
- Quiz creation with questions and automatic result calculation
- Question banks organized by subject
- Course ratings and rating distribution
- Stripe payment integration (Payment Intents + Webhooks)
- Swagger / OpenAPI documentation

## 🧰 Tech Stack
- Java 21
- Spring Boot 3.4.3
- Spring Security + JWT (jjwt)
- Spring Data JPA + Hibernate
- MySQL
- Flyway (database migrations)
- Stripe SDK (payments)
- Swagger / OpenAPI

## 🚀 Getting Started
### Prerequisites
- Java 21
- Maven (or use the Maven wrapper)
- MySQL

### Installation
```powershell
./mvnw clean package
```

### Environment Variables and Config
Configuration is stored in `src/main/resources/application.properties`. Review and update the following values:
- `spring.datasource.url`
- `spring.datasource.username`
- `spring.datasource.password`
- `server.port`
- `app.jwt-secret`
- `app.jwt-expiration-ms`
- `stripe.secret-key`
- `stripe.publishable-key`
- `stripe.webhook-secret`
- `file.upload-dir`

Do not commit real secrets to source control. Use environment-specific overrides for production.

### Run
```powershell
./mvnw spring-boot:run
```

## 🧭 API Overview
| Module | Endpoint | Method | Purpose |
|---|---|---|---|
| Auth | `/auth/register/student` | POST | Register student |
| Auth | `/auth/register/teacher` | POST | Register teacher |
| Auth | `/auth/login` | POST | Login and receive JWT |
| Courses | `/courses` | GET | List courses |
| Courses | `/courses/{id}` | GET | Get course by id |
| Courses | `/courses` | POST | Create course with uploads |
| Courses | `/courses/{id}` | PUT | Update course |
| Courses | `/courses/{id}` | DELETE | Delete course |
| Courses | `/courses/search?subject=...` | GET | Search courses by subject |
| Ratings | `/courses/ratings/{courseId}/rate` | POST | Rate course |
| Ratings | `/courses/ratings/{courseId}/distribution` | GET | Rating distribution |
| Quizzes | `/quizzes/create` | POST | Create quiz |
| Quizzes | `/quizzes/active` | GET | Get active quiz |
| Quizzes | `/quizzes/questions` | POST | Add question to active quiz |
| Quizzes | `/quizzes/questions` | GET | List questions in active quiz |
| Quizzes | `/quizzes/questions/{questionId}` | PUT | Update question |
| Quizzes | `/quizzes/questions/{questionId}` | DELETE | Delete question |
| Quizzes | `/quizzes/submit` | POST | Submit answers and calculate result |
| Question Banks | `/question-banks/subject/{subject}` | GET | Get question banks by subject |
| Payments | `/payments/create-intent` | POST | Create payment intent |
| Payments | `/payments/webhook` | POST | Stripe webhook handler |

## 🔐 Authentication
EduQuest uses JWT-based authentication. Users authenticate via `/auth/login` and receive a token to include in the `Authorization: Bearer <token>` header. Roles are enforced by Spring Security:
- `ADMIN`
- `TEACHER`
- `STUDENT`

## 💳 Stripe Integration
Payments are handled using Stripe Payment Intents. The backend creates intents via `/payments/create-intent`, and Stripe webhooks are processed at `/payments/webhook`.

## 🗃️ Database Migrations (Flyway)
Flyway runs automatically on startup to apply SQL migrations from `src/main/resources/db/migration`.

## 📚 Swagger / OpenAPI
If enabled, access the UI at:
- `/swagger-ui/index.html`

## 📄 License
Specify your license here. If you do not have one yet, add a `LICENSE` file and update this section.
