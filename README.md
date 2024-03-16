# spring-boot-keycloak-integration

# Keycloak Integration with Spring Boot 3

This project demonstrates how to secure a Spring Boot application using Keycloak, a powerful open-source Identity and
Access Management tool.

## Features

- Single Sign-On (SSO) with OpenID Connect
- Role-Based Access Control (RBAC)
- Fine-Grained Authorization

## Prerequisites

- Java 21+
- Maven
- Keycloak Server 24+

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
3. Use Maven to build the project:
    ```bash
    mvn clean install
    ```
4. You can then run the Spring Boot application using:
    ```bash
    mvn clean spring-boot:run
    ```

### Keycloak Setup

1. Run the docker-compose file:
    ```bash
    docker-compose up -d
    ```
2. Navigate to [Keycloak Admin UI Console](http://localhost:9090 "Keycloak Admin UI Console")
3. Create a new Real and name ut ```PowerRanger``` or update the ```application.yml``` file and specify your Realm name
4. Create Roles
5. Create Users
6. Assign roles to users

## Usage

TBD

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

This project is licensed under the MIT License - see the LICENSE.md file for details
