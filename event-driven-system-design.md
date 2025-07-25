
# Event-Driven System Design

## Requirements
- Functional: Process events (pub/sub).
- Non-Functional: High throughput, fault tolerance.

## Architecture Diagram
![Event-Driven Diagram](event-driven-diagram.png)

## Components
- Client
- Load Balancer
- App Servers
- Event Bus (Kafka)
- Replication Nodes

## Design Choices
- **Kafka**: Pub/sub for events.
- **Partitioning**: By event type.
- **Replication**: For fault tolerance.

## Java Implementation
- Spring Kafka for event handling.
- Leverages my microservices experience.
