
# Key-Value Store System Design

## 📌 Requirements

### ✅ Functional
- Store, retrieve, update key-value pairs.

### ✅ Non-Functional
- High throughput.
- Low latency (<50ms).
- High availability.

---

## 🗺️ Architecture Diagram

![Key-Value Store Diagram](key-value-store-diagram.png)

---

## 🧩 Components

- **Client:** Browser or mobile app sending HTTP requests.
- **Load Balancer:** AWS ELB or Nginx to distribute traffic.
- **App Servers:** Java / Spring Boot for handling requests.
- **Key-Value Store:** Redis (in-memory) or DynamoDB (persistent), with **sharding**.
- **Secondary Nodes:** Replication (e.g., Redis replicas, DynamoDB global tables) for high availability.

---

## 🛠️ Design Choices

- **Redis**: Chosen for ultra-low-latency in-memory storage.
- **Sharding**: Partition data by hash of the key to scale horizontally.
- **Replication**: Synchronous or asynchronous replication to ensure high availability and fault tolerance.

---

## 💻 Java Implementation

- **Spring Boot REST APIs**
  - `PUT /key/value` → Store/update value.
  - `GET /key` → Retrieve value.

- **Spring Data Redis** (or DynamoDB SDK)
  - Used for seamless integration with Redis or DynamoDB.
  - Leverages existing Java and Spring ecosystem experience.
