# System Architecture

## Architectural Style
MeasureStream follows a microservices architecture combined with
event-driven communication.

Each service is independently deployable and communicates primarily
through asynchronous events.

## High-Level Architecture
![architecture](../diagrams/architecture.png)

## Core Components

### Sensor Manager
Responsible for:
- Sensor registration and lifecycle management
- Emitting events related to sensors and nodes

### Measure Manager
Responsible for:
- Consuming measurement-related events
- Persisting time-series data in MongoDB

### Setting Manager
Responsible for:
- Managing configuration and calibration parameters
- Propagating updates through events

### Message Broker
Apache Kafka is used as the backbone for inter-service communication.

### Databases
- PostgreSQL: metadata, configuration, sensors
- MongoDB: time-series measurements

## Communication Model

The system uses an event-driven communication model.

- Producers emit domain events to Kafka topics
- Consumers subscribe to topics of interest
- Services are loosely coupled

This approach improves scalability and fault isolation.

## Synchronous Communication
REST APIs are used for:
- External client interactions
- Administrative operations

## Security Overview
Authentication and authorization are handled through Keycloak.

- OAuth2 / OpenID Connect
- Centralized identity management
- Role-based access control

## Scalability and Fault Tolerance
- Services can be scaled independently
- Kafka provides message durability
- Stateless services enable horizontal scaling

