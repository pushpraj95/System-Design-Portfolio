
# Chat System Design

## Requirements
- Functional: Real-time messaging between users.
- Non-Functional: Low latency, scalable, reliable message delivery.

## Architecture Diagram
(Text-based representation)

```
+-----------+
|   Client  |  ← Web/Mobile App (e.g., React, Android)
+-----+-----+
      |
      | WebSocket/HTTP(S) Request
      v
+--------------+
| Load Balancer|  ← Nginx / AWS ELB / HAProxy
+------+-------+
       |
       | Distributes traffic
       v
+--------------------+
|   App Servers      |  ← Authentication, Message API, Routing Logic
|  (Stateless)       |
+--------+-----------+
         |
         | Persistent WebSocket Connection
         v
+--------------------+
| WebSocket Servers  |  ← Handles real-time bi-directional messaging
| (e.g., Netty, Socket.IO, STOMP) |
+--------+-----------+
         |
         | Message Queue (Optional for decoupling)
         |
         v
+-------------------+
|     Database      |  ← Stores messages, user info, metadata
| (SQL/NoSQL/Redis) |
+-------------------+
```

## Components

- **Client**: Sends/receives messages via WebSocket or HTTP.
- **Load Balancer**: Distributes incoming traffic.
- **App Servers**: Stateless services handling auth, REST APIs, WebSocket upgrades.
- **WebSocket Servers**: Manages real-time bi-directional communication.
- **Database**: Persists chat messages, metadata, user info.

## Message Flow

```
Client → Load Balancer → App Server → WebSocket Server → Database (store message)
                                      ↑                      ↓
                              Other clients notified via WebSocket
```
