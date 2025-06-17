Overview
This is a backend-focused Airbnb clone built with Django and Django REST Framework (DRF). The project aims to replicate core Airbnb functionalities such as:

User authentication and profile management

Listing creation, editing, and deletion

Search and filtering of listings

Booking system with date validation

Reviews and ratings

RESTful API endpoints for frontend integration

The goal is to architect a scalable, secure, and maintainable API backend that can power a full-featured booking platform, serving as a solid foundation for frontend expansion or mobile integration.

🚀 Technology Stack
Python 3.11+

Django – Web framework for backend logic and admin tools

Django REST Framework (DRF) – For building RESTful APIs

PostgreSQL – Primary database (optional, fallback to SQLite during dev)

JWT Authentication – For secure token-based login/logout

Docker (optional) – For containerized development

Swagger / DRF-YASG – For interactive API documentation

Team Roles
🧠 Project Manager
Responsible for overall planning, timeline management, and communication. Ensures the project stays on track, aligns with the goals, and meets deadlines.

🛠️ Backend Developer
Designs and implements the server-side logic using Django and Django REST Framework. Handles API endpoints, authentication, business logic, and integration with the database.

🗃️ Database Administrator (DBA)
Designs and manages the data models, relationships, indexing strategies, and database optimization. Ensures data integrity, backups, and performance tuning.

🧪 QA Engineer / Tester
Writes and runs automated/manual tests to ensure API endpoints work correctly and consistently. Also responsible for regression testing and identifying bugs pre-deployment.

🔒 DevOps / Deployment Engineer
Handles environment setup, CI/CD pipelines, Dockerization, and deployment strategies. Ensures smooth version control, staging, and production releases.

📄 Technical Writer
Maintains project documentation including README, API docs (Swagger or DRF-YASG), changelogs, and developer guides to ease onboarding and usage.



🗃️ Database Design
The following are the core entities in the system and their relationships:

🔐 Users
Represents registered users — both guests and hosts.

Important Fields:

id: Primary key (UUID or AutoField)

email: Unique identifier for login

password: Hashed password

is_host: Boolean flag to distinguish hosts from guests

date_joined: Account creation timestamp

Relationships:

A user can create multiple properties (if they’re a host)

A user can book multiple properties (as a guest)

A user can leave multiple reviews

🏠 Properties
Represents a property or listing available for rent.

Important Fields:

id: Primary key

owner: ForeignKey to User

title: Short description of the property

description: Detailed info about the listing

price_per_night: Numeric field for nightly rate

Relationships:

A property is owned by one host (user)

A property can have many bookings and many reviews

📅 Bookings
Represents a reservation of a property by a guest.

Important Fields:

id: Primary key

guest: ForeignKey to User

property: ForeignKey to Property

check_in: Date field

check_out: Date field

Relationships:

A booking is made by one user (guest)

A booking is associated with one property

⭐ Reviews
Represents user-generated feedback for a property.

Important Fields:

id: Primary key

author: ForeignKey to User

property: ForeignKey to Property

rating: Integer (1–5)

comment: Text field

Relationships:

A review is written by one user

A review belongs to one property

💳 Payments
Represents transactions made for bookings.

Important Fields:

id: Primary key

booking: OneToOneField to Booking

amount: Decimal

status: Enum or CharField (pending, completed, failed)

payment_method: e.g., card, PayPal

Relationships:

Each booking has exactly one payment

Payments are tied to users indirectly through bookings

🔗 Entity Relationships Summary
One User ➡️ Many Properties

One User ➡️ Many Bookings

One User ➡️ Many Reviews

One Property ➡️ Many Bookings

One Property ➡️ Many Reviews

One Booking ➡️ One Payment
