# URL Shortener System Design

## Requirements
- **Functional**: Shorten long URLs, redirect short URLs to original, track clicks (optional).
- **Non-Functional**: Scalable (millions of requests/day), low latency (<200ms), high availability, reliable storage.

## Architecture Diagram
![URL Shortener Diagram](url-shortener-diagram.png)

## Components
- **Client**: Browser/app sending requests to shorten or access URLs.
- **Load Balancer**: Distributes traffic to app servers (e.g., AWS ELB, round-robin).
- **Application Servers**: Java/Spring Boot servers handling:
  - Shortening: Generate short code (base62), store in DB/cache.
  - Redirect: Lookup short code in cache/DB, return long URL.
- **Cache**: Redis for frequent URL mappings (lowers DB load).
- **Database**: MySQL (consistent, CP system) or DynamoDB (scalable, AP system).

## Data Flow
1. **Shorten**: Client → Load Balancer → Spring Boot → Save to Redis/MySQL → Return short URL.
2. **Redirect**: Client → Load Balancer → Spring Boot → Check Redis → Check MySQL → Redirect.

## Design Choices
- **Load Balancer**: Ensures scalability/availability, similar to Nginx in past Java projects.
- **Redis Cache**: Reduces DB queries for redirects, like Spring Cache in my apps.
- **MySQL/DynamoDB**: MySQL for consistency (orders-like data); DynamoDB for scalability.
- **Base62 Encoding**: Generates short codes (e.g., abc123) in Java for uniqueness.

## Java Implementation Notes
- **Spring Boot**: REST APIs (POST /shorten, GET /{shortCode}) using Spring MVC.
- **Redis**: Spring Data Redis for caching, similar to session management.
- **Database**: Spring Data JPA for MySQL or AWS SDK for DynamoDB, leveraging my backend experience.