# 🏡 Airbnb Clone – Backend API

This is a backend-focused **Airbnb clone** built with Django and Django REST Framework (DRF). The project replicates key Airbnb features and provides a scalable, secure, and maintainable API backend for a booking platform.

---

## 📌 Overview

The project aims to implement core Airbnb functionalities including:

- User authentication and profile management  
- Property listing creation, editing, and deletion  
- Search and filtering of listings  
- Booking system with date validation  
- Reviews and ratings  
- RESTful API endpoints for frontend/mobile integration

The goal is to create a modular and extensible backend ready for production, with clear security protocols and developer-friendly API documentation.

---

## 🚀 Technology Stack

| Technology | Purpose |
|------------|---------|
| **Python 3.11+** | Primary language for backend logic |
| **Django** | Web framework for handling backend views, models, and admin interface |
| **Django REST Framework (DRF)** | Used to expose the application’s functionalities via RESTful APIs |
| **PostgreSQL** | Primary relational database (fallback: SQLite for local development) |
| **JWT Authentication** | Secure, stateless user authentication for APIs |
| **Docker** *(optional)* | Containerized development for consistency across environments |
| **Swagger / DRF-YASG** | API documentation and testing interface |

---

## 👥 Team Roles

| Role | Responsibility |
|------|----------------|
| **🧠 Project Manager** | Oversees planning, communication, and ensures alignment with project goals |
| **🛠️ Backend Developer** | Implements API endpoints, business logic, and backend features using Django/DRF |
| **🗃️ Database Administrator** | Designs models, manages migrations, and optimizes database performance |
| **🧪 QA Engineer / Tester** | Writes automated/manual tests and ensures regression and bug testing |
| **🔒 DevOps Engineer** | Handles Docker, CI/CD setup, deployment, and environment management |
| **📄 Technical Writer** | Documents features, API endpoints, usage guidelines, and changelogs |

---

## 🗃️ Database Design

### 🔐 Users
Represents registered users — both guests and hosts.

**Fields:**
- `id`: Primary key
- `email`: Unique login identifier
- `password`: Hashed password
- `is_host`: Boolean to flag hosts
- `date_joined`: Timestamp

**Relationships:**
- One user can create multiple properties
- One user can make multiple bookings
- One user can write multiple reviews

---

### 🏠 Properties
Represents listings available for booking.

**Fields:**
- `id`: Primary key
- `owner`: ForeignKey to `User`
- `title`: Short descriptor
- `description`: Detailed content
- `price_per_night`: Decimal

**Relationships:**
- Belongs to one host
- Can have many bookings and reviews

---

### 📅 Bookings
Represents reservations made by users.

**Fields:**
- `id`: Primary key
- `guest`: ForeignKey to `User`
- `property`: ForeignKey to `Property`
- `check_in`: Date
- `check_out`: Date

**Relationships:**
- One booking per guest per property

---

### ⭐ Reviews
User-submitted property reviews.

**Fields:**
- `id`: Primary key
- `author`: ForeignKey to `User`
- `property`: ForeignKey to `Property`
- `rating`: Integer (1-5)
- `comment`: Text

**Relationships:**
- One user ➝ many reviews
- One property ➝ many reviews

---

### 💳 Payments
Tracks transaction data.

**Fields:**
- `id`: Primary key
- `booking`: OneToOneField
- `amount`: Decimal
- `status`: Enum/CharField
- `payment_method`: Card, PayPal, etc.

**Relationships:**
- One booking ➝ one payment

---

### 🔗 Entity Relationship Summary

- One `User` ➝ Many `Properties`
- One `User` ➝ Many `Bookings`
- One `User` ➝ Many `Reviews`
- One `Property` ➝ Many `Bookings`
- One `Property` ➝ Many `Reviews`
- One `Booking` ➝ One `Payment`

---

## ✨ Feature Breakdown

### 👤 User Management
User registration, login, profile management, and authentication via JWT. Handles both guests and hosts with role-based permissions.

### 🏠 Property Management
Hosts can create, update, and delete property listings with detailed info such as title, description, price, and location.

### 📆 Booking System
Allows guests to reserve properties. Handles date availability, total cost calculation, and prevents double-booking.

### ⭐ Review & Rating System
Users can rate and leave feedback on properties after their stay. Boosts platform trust and guides future guests.

### 💳 Payment Integration
Handles payment records and transaction logic. Designed to be extended to integrate real payment gateways.

### 📄 API Documentation
Swagger (DRF-YASG) provides interactive API documentation for testing and developer onboarding.

---

## 🔐 API Security

| Security Layer | Purpose |
|----------------|---------|
| **Authentication (JWT)** | Secures endpoints with stateless login and logout using tokens |
| **Authorization (RBAC)** | Restricts actions based on user roles (host, guest) |
| **Rate Limiting** | Prevents brute-force attacks and API abuse using throttling |
| **Validation & Sanitization** | Prevents malicious input and ensures data consistency |
| **Secure Payments** | Protects transactions with endpoint security and HTTPS |
| **Logging & Error Handling** | Logs suspicious activity, prevents leakage of sensitive system errors |

Security ensures protection of user data, financial integrity, and platform trust.

---

## 🚀 CI/CD Pipeline

CI/CD (Continuous Integration and Deployment) automates building, testing, and deploying code for faster, safer releases.

### 📦 Purpose

- Run tests on every push or pull request
- Ensure clean and reproducible builds
- Automate deployment to staging/production

### 🛠️ Tools

| Tool | Purpose |
|------|---------|
| **GitHub Actions** | Run CI workflows like tests, linting, and deployments |
| **Docker** | Containerization for environment consistency |
| **Docker Compose** | Multi-container orchestration (e.g., DB + App) |
| **Heroku / Render / Railway** | Optional PaaS platforms with CI/CD integrations |

Future additions: code coverage, static analysis, and staging previews.

---
