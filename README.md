# spring-boot-keycloak-integration

[![Java CI with Maven](https://github.com/hendisantika/spring-boot-keycloak-integration/actions/workflows/maven.yml/badge.svg)](https://github.com/hendisantika/spring-boot-keycloak-integration/actions/workflows/maven.yml)
![Java](https://img.shields.io/badge/Java-25-orange?logo=openjdk)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-4.1-brightgreen?logo=springboot)
![Keycloak](https://img.shields.io/badge/Keycloak-25-blue?logo=keycloak)

# Keycloak Integration with Spring Boot 4

This project demonstrates how to secure a Spring Boot application (OAuth2 Resource Server) using Keycloak, a powerful
open-source Identity and Access Management tool.

## Features

- Single Sign-On (SSO) with OpenID Connect
- Stateless JWT authentication (OAuth2 Resource Server)
- Role-Based Access Control (RBAC) using Keycloak client roles (`resource_access`)
- Method-level authorization with `@PreAuthorize`

## Tech Stack

| Component       | Version                         |
|-----------------|---------------------------------|
| Java            | 25 (Temurin recommended)        |
| Spring Boot     | 4.1.x                           |
| Spring Security | 7.x (lambda DSL)                |
| Keycloak        | 25.x (via Docker Compose)       |
| Build tool      | Maven Wrapper (`./mvnw`)        |

## Prerequisites

- JDK 25+
- Docker & Docker Compose
- Maven 3.9+ (optional, the Maven Wrapper `./mvnw` is included)

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing
purposes.

### Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/hendisantika/spring-boot-keycloak-integration.git
    ```
2. Navigate into the project directory:
    ```bash
    cd spring-boot-keycloak-integration
    ```
3. Build the project and run the tests:
    ```bash
    ./mvnw clean verify
    ```
4. Run the Spring Boot application (port `8081`):
    ```bash
    ./mvnw spring-boot:run
    ```
   Thanks to `spring-boot-docker-compose`, the Keycloak container defined in `compose.yml` is started automatically.

### Keycloak Setup

1. Start Keycloak manually (optional when using `spring-boot:run`):
    ```bash
    docker compose up -d
    ```
2. Open the [Keycloak Admin UI Console](http://localhost:9090 "Keycloak Admin UI Console") and log in with
   `admin` / `admin`.
3. Create a new Realm named `PowerRanger`, or update `application.yml` with your own realm name.
4. Create a client named `springboot-keycloak` (matches `jwt.auth.converter.resource-id`).
5. Create the client roles `client_user` and `client_admin`.
6. Create users and assign the client roles to them.

> **Note:** make sure `spring.security.oauth2.resourceserver.jwt.issuer-uri` in
> `src/main/resources/application.yml` points to the host/port where Keycloak is exposed
> (e.g. `http://localhost:9090/realms/PowerRanger` when using the provided `compose.yml`).

## Usage

1. Get an access token from Keycloak:
    ```bash
    curl -s -X POST "http://localhost:9090/realms/PowerRanger/protocol/openid-connect/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -d "grant_type=password" \
      -d "client_id=springboot-keycloak" \
      -d "username=<username>" \
      -d "password=<password>"
    ```
2. Call the secured endpoints with the token:
    ```bash
    curl -H "Authorization: Bearer <access_token>" http://localhost:8081/api/v1/demo
    ```

| Method | Endpoint                   | Required role  |
|--------|----------------------------|----------------|
| GET    | `/api/v1/demo`             | `client_user`  |
| GET    | `/api/v1/demo/hello-2`     | `client_admin` |

## CI/CD & Dependency Management

- **GitHub Actions** (`.github/workflows/maven.yml`) builds and tests the project with JDK 25 on every push and pull
  request to `main`, and submits the Maven dependency graph to GitHub.
- **Dependabot** (`.github/dependabot.yml`) keeps dependencies up to date:
    - Maven dependencies daily (Spring Boot and minor/patch updates are grouped)
    - GitHub Actions weekly
    - Docker Compose images (Keycloak) weekly

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

This project is licensed under the MIT License.
