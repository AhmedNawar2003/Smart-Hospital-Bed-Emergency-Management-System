# 🏥 Smart Hospital Bed & Emergency Management System

<div align="center">

[![Typing SVG](https://readme-typing-svg.demolab.com?font=JetBrains+Mono\&weight=700\&size=22\&pause=1000\&color=FF4D6D\&center=true\&vCenter=true\&width=900\&lines=🏥+Smart+Hospital+Bed+%26+Emergency+Management+System;Production-Grade+Microservices+%7C+Java+21;Emergency+Response+%7C+Real-Time+%7C+Cloud-Native;Spring+Boot+%7C+Kafka+%7C+JWT+%7C+Docker)](https://git.io/typing-svg)

### `Java 21` · `Spring Boot` · `Spring Cloud` · `Kafka` · `JWT` · `Docker` · `Cloud-Native`

**A production-grade, event-driven microservices platform** designed to solve a critical healthcare problem in Egypt — helping hospitals manage bed availability, ICU capacity, emergency cases, and ambulance dispatching in real-time.

Built with **Java 21**, **Spring Boot**, **Spring Cloud**, and modern **Cloud-Native** architecture principles.

<br/>

![Java](https://img.shields.io/badge/Java-21-ED8B00?style=for-the-badge\&logo=openjdk\&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-6DB33F?style=for-the-badge\&logo=springboot\&logoColor=white)
![Spring Cloud](https://img.shields.io/badge/Spring%20Cloud-2024.x-6DB33F?style=for-the-badge\&logo=spring\&logoColor=white)
![Kafka](https://img.shields.io/badge/Apache%20Kafka-231F20?style=for-the-badge\&logo=apachekafka\&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?style=for-the-badge\&logo=postgresql\&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-Cache-DC382D?style=for-the-badge\&logo=redis\&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge\&logo=docker\&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge\&logo=jsonwebtokens\&logoColor=white)
![Resilience4j](https://img.shields.io/badge/Resilience4j-Circuit%20Breaker-critical?style=for-the-badge)
![Zipkin](https://img.shields.io/badge/Zipkin-Tracing-FE7139?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Production%20Ready-00C851?style=for-the-badge)

</div>

---

## 📁 Project Structure

```text
smart-hospital-system/
├── pom.xml
├── docker-compose.yml
├── .env
│
├── eureka-server/
│   ├── pom.xml
│   └── src/main/
│       ├── java/com/hospital/eureka/
│       │   ├── EurekaServerApplication.java
│       │   └── SecurityConfig.java
│       └── resources/application.yml
│
├── config-server/
│   ├── pom.xml
│   └── src/main/
│       ├── java/com/hospital/config/
│       │   └── ConfigServerApplication.java
│       └── resources/
│           ├── application.yml
│           └── configs/
│               ├── auth-service.yml
│               ├── hospital-service.yml
│               ├── bed-service.yml
│               ├── emergency-service.yml
│               ├── ambulance-service.yml
│               ├── notification-service.yml
│               └── analytics-service.yml
│
├── api-gateway/
│   ├── pom.xml
│   └── src/main/
│       ├── java/com/hospital/gateway/
│       │   ├── ApiGatewayApplication.java
│       │   ├── filter/AuthenticationFilter.java
│       │   └── config/FallbackController.java
│       └── resources/application.yml
│
├── auth-service/
├── hospital-service/
├── bed-service/
├── emergency-service/
├── ambulance-service/
├── notification-service/
└── analytics-service/
```

---

## 📋 Table of Contents

* [Overview](#-overview)
* [Problem Statement](#-problem-statement)
* [System Architecture](#️-system-architecture)
* [Services Breakdown](#-services-breakdown)
* [Security Model](#-security-model)
* [Emergency Workflow](#-emergency-workflow)
* [Bed Management Lifecycle](#-bed-management-lifecycle)
* [Tech Stack](#️-tech-stack)
* [Design Highlights](#-design-highlights)
* [Database Design](#️-database-design)
* [API Endpoints](#-api-endpoints)
* [Observability](#-observability)
* [Getting Started](#-getting-started)
* [Future Enhancements](#-future-enhancements)

---

## 🔍 Overview

**Smart Hospital System** is a fully distributed, event-driven healthcare management platform that enables:

* 🏥 **Real-time hospital bed tracking**
* 🚑 **Emergency response coordination**
* 🧠 **Smart hospital recommendations**
* 📡 **Live ambulance dispatch tracking**
* 🔔 **Emergency alerts & notifications**
* 📊 **Hospital analytics & reporting**

The system is built using a scalable **Microservices Architecture** with strong focus on:

* scalability
* reliability
* distributed systems
* fault tolerance
* cloud-native engineering
* enterprise backend architecture

---

## 🇪🇬 Problem Statement

Hospitals in Egypt face major operational challenges:

| Problem                                    | Impact                                                |
| ------------------------------------------ | ----------------------------------------------------- |
| ❌ No centralized bed availability tracking | Patients waste time searching for available hospitals |
| ❌ ICU shortages                            | Critical emergency delays                             |
| ❌ Poor ambulance coordination              | Slower emergency response times                       |
| ❌ Manual hospital communication            | Inefficient patient transfers                         |
| ❌ No real-time analytics                   | Poor resource allocation                              |

This system digitizes emergency healthcare coordination by enabling hospitals, ambulance teams, and emergency operators to collaborate in real-time.

---

## 🏛️ System Architecture

<p align="center">
  <img src="/smart_hospital_system.png" width="100%" alt="Smart Hospital System Architecture"/>
</p>

```text
                    ┌─────────────────────────────┐
                    │      Client Applications     │
                    │     Web / Mobile / Admin     │
                    └──────────────┬──────────────┘
                                   │ HTTPS
                    ┌──────────────▼──────────────┐
                    │         API Gateway          │
                    │         Port: 8080           │
                    │ JWT Validation · Routing     │
                    │ Rate Limiting · Security     │
                    └──────┬───────────────┬───────┘
                           │               │
          ┌────────────────┼───────────────┼────────────────┐
          │                │               │                │
┌─────────▼──────┐ ┌───────▼──────┐ ┌─────▼──────┐ ┌──────▼──────┐
│  Auth Service  │ │ Hospital Svc │ │ Bed Service│ │ Emergency   │
│  Port: 8081    │ │ Port: 8082   │ │ Port: 8083 │ │ Service     │
│ JWT · OAuth2   │ │ Hospitals    │ │ ICU Beds   │ │ Port: 8084  │
└────────────────┘ └──────────────┘ └─────┬──────┘ └──────┬──────┘
                                          │               │
                                  ┌───────▼───────────────▼──────┐
                                  │        Apache Kafka           │
                                  │     Event-Driven Messaging    │
                                  └──────────────┬────────────────┘
                                                 │
                    ┌────────────────────────────┼──────────────────────────┐
                    │                            │                           │
          ┌─────────▼──────────┐      ┌──────────▼──────────┐     ┌─────────▼──────┐
          │ Notification Svc   │      │   Analytics Svc     │     │ Ambulance Svc  │
          │ Port: 8086         │      │ Port: 8087          │     │ Port: 8085     │
          │ Email · SMS Alerts │      │ Reports · Statistics│     │ Dispatch Track │
          └────────────────────┘      └─────────────────────┘     └────────────────┘

       ┌───────────────┐     ┌──────────────────┐     ┌────────────────┐
       │ Config Server │     │   Eureka Server  │     │    Zipkin      │
       │ Port: 8888    │     │ Port: 8761       │     │ Port: 9411     │
       └───────────────┘     └──────────────────┘     └────────────────┘
```

---

## 🧩 Services Breakdown

### 🔧 Infrastructure Services

| Service       | Port   | Description                                                 |
| ------------- | ------ | ----------------------------------------------------------- |
| API Gateway   | `8080` | Central entry point, JWT validation, routing, rate limiting |
| Eureka Server | `8761` | Dynamic service discovery                                   |
| Config Server | `8888` | Centralized configuration management                        |
| Zipkin        | `9411` | Distributed tracing & monitoring                            |
| Kafka         | `9092` | Event-driven communication                                  |
| Redis         | `6379` | Caching & session management                                |

---

### 🏥 Business Services

| Service              | Port   | Responsibilities                         |
| -------------------- | ------ | ---------------------------------------- |
| Auth Service         | `8081` | Authentication, JWT, OAuth2, RBAC        |
| Hospital Service     | `8082` | Hospitals, branches, departments         |
| Bed Service          | `8083` | ICU beds, availability tracking          |
| Emergency Service    | `8084` | Emergency case handling & prioritization |
| Ambulance Service    | `8085` | Ambulance dispatch & tracking            |
| Notification Service | `8086` | Email, SMS, system alerts                |
| Analytics Service    | `8087` | Reports, statistics, hospital analytics  |

---

## 🔐 Security Model

### Authentication Strategy

* JWT-based authentication
* OAuth2 login support
* Role-Based Access Control (RBAC)
* Stateless authentication
* Gateway-level token validation

### Roles

| Role                 | Permissions                     |
| -------------------- | ------------------------------- |
| `SUPER_ADMIN`        | Full system access              |
| `HOSPITAL_ADMIN`     | Manage hospital resources       |
| `DOCTOR`             | Access patient & emergency data |
| `NURSE`              | Bed & ward management           |
| `AMBULANCE_DRIVER`   | Dispatch & tracking             |
| `EMERGENCY_OPERATOR` | Emergency case coordination     |

### JWT Example

```json
{
  "sub": "admin@hospital.com",
  "role": "ROLE_HOSPITAL_ADMIN",
  "iat": 1714500000,
  "exp": 1714586400
}
```

---

## 🚑 Emergency Workflow

```text
                    EMERGENCY CREATED
                             │
                             ▼
                 ┌──────────────────────┐
                 │ Emergency Service    │
                 │ Priority Detection   │
                 └──────────┬───────────┘
                            │ publishes
                            ▼
                 ┌──────────────────────┐
                 │ emergency.created    │
                 │     Kafka Topic      │
                 └──────────┬───────────┘
                            │ consumed by
        ┌───────────────────┴────────────────────┐
        │                                        │
┌───────▼────────┐                    ┌──────────▼────────┐
│ Ambulance Svc  │                    │ Notification Svc  │
│ Assign nearest │                    │ Send emergency    │
│ ambulance      │                    │ alerts            │
└────────────────┘                    └───────────────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │ Bed Service          │
                 │ Reserve ICU Bed      │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │ Analytics Service    │
                 │ Store response stats │
                 └──────────────────────┘
```

---

## 🛏️ Bed Management Lifecycle

### Bed Status Flow

```text
AVAILABLE → RESERVED → OCCUPIED → AVAILABLE
                  ↓
             MAINTENANCE
```

### Emergency Priority Levels

| Level      | Description                             |
| ---------- | --------------------------------------- |
| `CRITICAL` | Immediate ICU or emergency intervention |
| `HIGH`     | High-risk emergency                     |
| `MEDIUM`   | Stable but urgent                       |
| `LOW`      | Minor emergency                         |

---

## 🛠️ Tech Stack

### ⚙️ Backend Core

![Java](https://img.shields.io/badge/Java-21-ED8B00?style=for-the-badge\&logo=openjdk\&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-6DB33F?style=for-the-badge\&logo=springboot\&logoColor=white)
![Spring Cloud](https://img.shields.io/badge/Spring%20Cloud-2024.x-6DB33F?style=for-the-badge\&logo=spring\&logoColor=white)
![Maven](https://img.shields.io/badge/Maven-3.9+-C71A36?style=for-the-badge\&logo=apachemaven\&logoColor=white)

### 🔐 Security

![Spring Security](https://img.shields.io/badge/Spring%20Security-6DB33F?style=for-the-badge\&logo=springsecurity\&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-JJWT-000000?style=for-the-badge\&logo=jsonwebtokens\&logoColor=white)
![OAuth2](https://img.shields.io/badge/OAuth2-Google%20Login-4285F4?style=for-the-badge\&logo=google\&logoColor=white)

### 📨 Messaging & Communication

![Kafka](https://img.shields.io/badge/Apache%20Kafka-7.x-231F20?style=for-the-badge\&logo=apachekafka\&logoColor=white)
![OpenFeign](https://img.shields.io/badge/OpenFeign-REST%20Client-6DB33F?style=for-the-badge\&logo=spring\&logoColor=white)
![Resilience4j](https://img.shields.io/badge/Resilience4j-Circuit%20Breaker-FF6347?style=for-the-badge)

### 🗄️ Data Layer

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?style=for-the-badge\&logo=postgresql\&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-7-DC382D?style=for-the-badge\&logo=redis\&logoColor=white)
![Hibernate](https://img.shields.io/badge/JPA%20%2F%20Hibernate-59666C?style=for-the-badge\&logo=hibernate\&logoColor=white)

### 📊 Observability

![Zipkin](https://img.shields.io/badge/Zipkin-Tracing-FE7139?style=for-the-badge)
![Swagger](https://img.shields.io/badge/Swagger-OpenAPI%203-85EA2D?style=for-the-badge\&logo=swagger\&logoColor=black)
![Micrometer](https://img.shields.io/badge/Micrometer-Metrics-1DB954?style=for-the-badge)

### 🐳 DevOps

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge\&logo=docker\&logoColor=white)
![Docker Compose](https://img.shields.io/badge/Docker%20Compose-Multi--Service-2496ED?style=for-the-badge\&logo=docker\&logoColor=white)

---

## 🎯 Design Highlights

| Area                | Implementation       | Benefit                          |
| ------------------- | -------------------- | -------------------------------- |
| Architecture        | Microservices        | Independent deployment & scaling |
| Data Management     | Database-per-Service | Isolation & bounded contexts     |
| Async Communication | Kafka Event Bus      | Decoupled processing             |
| Service Discovery   | Netflix Eureka       | Dynamic service registration     |
| Centralized Config  | Spring Cloud Config  | Easy environment management      |
| Security            | JWT + OAuth2 + RBAC  | Enterprise-grade authentication  |
| Resilience          | Resilience4j         | Circuit breaker & fallback       |
| Caching             | Redis                | Fast bed availability lookups    |
| Observability       | Zipkin + Micrometer  | Distributed tracing              |
| Containerization    | Docker Compose       | Easy deployment                  |

---

## 🧠 Design Patterns Used

| Pattern           | Usage                               |
| ----------------- | ----------------------------------- |
| Strategy Pattern  | Emergency prioritization algorithms |
| Factory Pattern   | Notification creation               |
| Observer Pattern  | Bed status updates & alerts         |
| Builder Pattern   | Complex report generation           |
| Singleton Pattern | Configuration management            |
| Adapter Pattern   | Third-party ambulance/SMS APIs      |

---

## 📐 SOLID Principles Applied

* Single Responsibility Principle (SRP)
* Open/Closed Principle (OCP)
* Liskov Substitution Principle (LSP)
* Interface Segregation Principle (ISP)
* Dependency Inversion Principle (DIP)

---

## 🗃️ Database Design

Each microservice owns its own database.

| Service              | Database          |
| -------------------- | ----------------- |
| Auth Service         | `auth_db`         |
| Hospital Service     | `hospital_db`     |
| Bed Service          | `bed_db`          |
| Emergency Service    | `emergency_db`    |
| Ambulance Service    | `ambulance_db`    |
| Notification Service | `notification_db` |
| Analytics Service    | `analytics_db`    |

### Core Entities

| Service      | Main Entities                      |
| ------------ | ---------------------------------- |
| Auth         | User, Role, RefreshToken           |
| Hospital     | Hospital, Branch, Department       |
| Bed          | Bed, Ward, BedAssignment           |
| Emergency    | EmergencyCase, EmergencyAssignment |
| Ambulance    | Ambulance, Driver, DispatchRequest |
| Notification | Notification, Alert                |
| Analytics    | Report, Statistics                 |

---

## 📄 API Endpoints

### Auth Service — `/api/v1/auth`

| Method | Endpoint         | Description            |
| ------ | ---------------- | ---------------------- |
| POST   | `/register`      | Register user          |
| POST   | `/login`         | Login & JWT generation |
| POST   | `/refresh-token` | Refresh JWT token      |
| GET    | `/oauth2/google` | Google OAuth2 login    |

---

### Hospital Service — `/api/v1/hospitals`

| Method | Endpoint | Description        |
| ------ | -------- | ------------------ |
| GET    | `/`      | Get all hospitals  |
| POST   | `/`      | Create hospital    |
| GET    | `/{id}`  | Get hospital by ID |
| PUT    | `/{id}`  | Update hospital    |
| DELETE | `/{id}`  | Delete hospital    |

---

### Bed Service — `/api/v1/beds`

| Method | Endpoint           | Description          |
| ------ | ------------------ | -------------------- |
| GET    | `/available`       | Get available beds   |
| POST   | `/reserve/{bedId}` | Reserve bed          |
| PATCH  | `/release/{bedId}` | Release bed          |
| GET    | `/icu`             | ICU bed availability |

---

### Emergency Service — `/api/v1/emergencies`

| Method | Endpoint       | Description           |
| ------ | -------------- | --------------------- |
| POST   | `/`            | Create emergency case |
| GET    | `/active`      | Active emergencies    |
| PATCH  | `/{id}/assign` | Assign hospital       |
| PATCH  | `/{id}/close`  | Close emergency       |

---

### Ambulance Service — `/api/v1/ambulances`

| Method | Endpoint       | Description          |
| ------ | -------------- | -------------------- |
| GET    | `/available`   | Available ambulances |
| POST   | `/dispatch`    | Dispatch ambulance   |
| PATCH  | `/{id}/status` | Update status        |

---

## 📊 Observability

| Tool             | Purpose                 | URL                                                                                |
| ---------------- | ----------------------- | ---------------------------------------------------------------------------------- |
| Eureka Dashboard | Service registry        | [http://localhost:8761](http://localhost:8761)                                     |
| Zipkin           | Distributed tracing     | [http://localhost:9411](http://localhost:9411)                                     |
| Swagger UI       | API documentation       | [http://localhost:{port}/swagger-ui.html](http://localhost:{port}/swagger-ui.html) |
| Actuator         | Health checks & metrics | [http://localhost:{port}/actuator](http://localhost:{port}/actuator)               |

---

## 🚀 Getting Started

### ✅ Prerequisites

| Tool   | Version |
| ------ | ------- |
| JDK    | 21+     |
| Maven  | 3.9+    |
| Docker | Latest  |
| Git    | Latest  |

---

### 📥 Clone Repository

```bash
git clone https://github.com/AhmedNawar2003/smart-hospital-system.git
cd smart-hospital-system
```

---

### 🔨 Build All Services

```bash
mvn clean install
```

---

### 🐳 Run with Docker Compose

```bash
docker-compose up -d
```

---

### 🔢 Startup Order

| Step | Service           |
| ---- | ----------------- |
| 1    | Eureka Server     |
| 2    | Config Server     |
| 3    | Kafka + Zookeeper |
| 4    | PostgreSQL        |
| 5    | Redis             |
| 6    | Auth Service      |
| 7    | Business Services |
| 8    | API Gateway       |

---

## 🗺️ Ports Summary

| Service              | Port   |
| -------------------- | ------ |
| API Gateway          | `8080` |
| Auth Service         | `8081` |
| Hospital Service     | `8082` |
| Bed Service          | `8083` |
| Emergency Service    | `8084` |
| Ambulance Service    | `8085` |
| Notification Service | `8086` |
| Analytics Service    | `8087` |
| Eureka Server        | `8761` |
| Config Server        | `8888` |
| Kafka                | `9092` |
| Zipkin               | `9411` |
| Redis                | `6379` |
| PostgreSQL           | `5432` |

---

## 📈 Future Enhancements

* [ ] Next.js Admin Dashboard
* [ ] Mobile App (React Native)
* [ ] AI-based emergency prediction
* [ ] Kubernetes deployment
* [ ] CI/CD pipelines using GitHub Actions
* [ ] SMS integration using Twilio/Vonage
* [ ] Real-time GPS ambulance tracking
* [ ] Multi-governorate deployment support
* [ ] Push notifications via Firebase
* [ ] ML-based hospital recommendation engine

---

## 👨‍💻 Author

<div align="center">

**Ahmed Nawar** — Backend Engineer · Java & Spring Boot Specialist

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Ahmed%20Nawar-0077B5?style=for-the-badge\&logo=linkedin\&logoColor=white)](https://www.linkedin.com/in/ahmed-nawar-246513243)
[![GitHub](https://img.shields.io/badge/GitHub-AhmedNawar2003-181717?style=for-the-badge\&logo=github\&logoColor=white)](https://github.com/AhmedNawar2003)
[![Email](https://img.shields.io/badge/Email-nawarahmed652%40gmail.com-D14836?style=for-the-badge\&logo=gmail\&logoColor=white)](mailto:nawarahmed652@gmail.com)

<br/>

⭐ If you find this project useful, please give it a star.

</div>
