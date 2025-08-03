# Prompql Aurelia Bank Challenge

## Overview

This repository contains the solution to the Aurelia Bank Challenge, utilizing PromptQL and Hasura technologies. The system is containerized using Docker Compose and is structured to support scalable, observable, and modular development.

## Folder Structure

- `app/`
  - Contains connectors for different databases and related compose files.
    - `connector/ash_promptql_mongo_2/compose.yaml`: Service definition for the MongoDB connector.
    - `connector/ash_promptql_postgres/compose.yaml`: Service definition for the Postgres connector.
  - Also contain metadata of the individual data models.
    - `metadata/accounts.hml`: Represents Aurelia Bank accounts core information related to the accounts.
    - `metadata/aml_cases.hml`: Represents detailed records of Anti-Money Laundering (AML) investigations.
    - `metadata/customers.hml`: Represents customers who have registered with Aurelia Bank.
    - `metadata/financial_transfer.hml`: Represents financial transactions between entities, providing detailed information about the transfer.
    - `metadata/sanctions.hml`: Represents sanctions data, capturing detailed information about entities, their types, and the lists they are associated with.
    - `metadata/sars.hml`: Represents Suspicious Activity Reports (SARs) filed by the Aurelia Bank.
- `engine/`
  - Source and Dockerfile for the core engine service.
- `globals/`
  - (Purpose unspecified; typically used for shared configuration or global scripts.)
- Root files:
  - `compose.yaml`: Main Docker Compose file that includes connectors and defines all core services.
  - `hasura.yaml`: Hasura configuration (details minimal).
  - `otel-collector-config.yaml`: Configuration for the OpenTelemetry Collector for observability.
  - `supergraph.yaml`: Supergraph configuration for service orchestration.
  - `README.md`: Project documentation (this file).

## Major Components

- **Engine**: The main service container built from the `engine/` directory. It handles authentication, CORS, SQL interface, and metadata management.
- **Connectors**: 
  - **MongoDB Connector**: Defined in `app/connector/ash_promptql_mongo_2/compose.yaml`. Connects to a MongoDB database and is configured via environment variables.
  - **Postgres Connector**: Defined in `app/connector/ash_promptql_postgres/compose.yaml`. Connects to a Postgres database and is configured via environment variables.
- **PromptQL Playground**: Local playground for running PromptQL queries, configured in the main `compose.yaml`.
- **OpenTelemetry Collector**: For distributed tracing and observability, as defined in `otel-collector-config.yaml`.

## Getting Started

### Prerequisites

- Docker and Docker Compose installed.
- Required environment variables set for secrets and service configuration (see compose files for details).

### Running the Project

1. Clone this repository:
   ```sh
   git clone https://github.com/ashritkulkarni/prompql-aurelia-bank-challenge.git
   cd prompql-aurelia-bank-challenge
   ```
2. Set up environment variables as needed (see the `compose.yaml` and connector compose files for required variables).
3. Start the services:
   ```sh
   docker compose up --build
   ```
4. The following services will be available:
    - Engine: [http://localhost:3280](http://localhost:3280)
    - PromptQL Playground: [http://localhost:3282](http://localhost:3282)
    - Connectors: Ports `6064` (MongoDB), `6936` (Postgres)

### Service Configuration

- All service- and connector-specific environment variables must be set before starting. Refer to `compose.yaml` and the connector `compose.yaml` files for the required variables.

## Observability

- Uses OpenTelemetry Collector for tracing and metrics. Configuration is provided in `otel-collector-config.yaml` and mapped in the main compose file.

## Contributing

Feel free to open issues or submit pull requests for improvements or bug fixes.

## License

Currently unspecified. Please add a license file if you intend to open source this project.

## References

- [PromptQL Documentation](https://promptql.com/)
- [Hasura Documentation](https://hasura.io/docs/)
