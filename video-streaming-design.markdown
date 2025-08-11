# Video Streaming System Design

## Requirements
- Functional: Stream video content in real-time.
- Non-Functional: Low latency (<200ms), scalable.

## Architecture Diagram
![Video Streaming Diagram](video-streaming-diagram.png)

## Components
- Client, Load Balancer, App Servers, CDN, Media Server, Cache, Database.

## Design Choices
- Caching: Redis for metadata and video segments.
- CDN: Global content delivery.
- Sharding: Scales by region.

## Java Implementation
- Spring Boot APIs.
- Spring Data Redis for caching.
- Custom streaming integration.