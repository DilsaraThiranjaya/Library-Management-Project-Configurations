# Library Management System: Centralized Configurations

This repository serves as the centralized configuration store for the Library Management System microservices ecosystem. It is designed to be consumed by the **Spring Cloud Config Server**.

## Purpose

To maintain a "Single Source of Truth" for all environment-specific and shared configurations across the platform and domain services. By decoupling configuration from the application binary, we can manage environment changes without rebuilding or redeploying code.

## Repository Structure

The repository follows an "Application-First" folder structure, which aligns with the `search-paths: '{application}'` configuration in the Config Server.

-   `api-gateway/`: Configurations for the Spring Cloud Gateway.
-   `service-registry/`: Eureka Server configurations.
-   `book-service/`: Domain configurations for Book management (MySQL, JPA).
-   `member-service/`: Domain configurations for Member management (MongoDB).
-   `file-service/`: Integration configurations for Google Cloud Storage.

## How it works

1.  **Config Server** clones this repository on startup.
2.  **Microservices** query the Config Server at boot time using their `spring.application.name`.
3.  **Config Server** looks up the folder matching that name and serves the `application.yml` file found within.

## Managing Changes

To update a service's configuration:
1.  Modify the appropriate YAML file in this repository.
2.  Commit and push the changes to the `main` branch.
3.  Refresh the target microservice using the `/actuator/refresh` endpoint (if using `@RefreshScope`) or restart the service to pick up the latest changes.