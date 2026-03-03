# Hill Harvest Organics - Project Summary

**Hill Harvest Organics** is a modern, full-stack E-commerce platform dedicated to selling organic produce. Built as a **Modular Monolith** with a Package-by-Feature (Domain) architecture, the project prioritizes robustness, security, and a seamless user experience.

### 💻 Tech Stack & Infrastructure
*   **Backend:** Java 21, Spring Boot 3, Spring Data JPA, Spring Security
*   **Frontend:** React, TypeScript, React Router, Context API
*   **Database:** PostgreSQL (hosted on **Supabase**) utilizing UUIDv7 primary keys
*   **Cloud & Storage:** AWS S3 (for product images & invoice storage), **AWS CloudFront** (configured in same `ap-south-1` region as S3 to minimize origin-fetch latency and reduce data egress costs), AWS SES (for transactional emails)
*   **Messaging:** AWS SQS, Spring Events (Observer Pattern)
*   **Payments:** Razorpay Integration
*   **Observability:** Prometheus & Grafana with a **Sidecar Grafana Agent**, Loki (logging)
*   **Deployment:** Docker, CI/CD pipelines (GitHub Actions) deployed to **AWS Lightsail**. Utilizing a **Sidecar Redis** container for caching and rate-limiting (with plans to migrate to a managed service).

---

### 🛍️ User-Facing Features (What Interviewers Will See)

When interacting with the platform, users and administrators experience a fully functional e-commerce ecosystem:

*   **Authentication & Profiles:** Users can sign up via Phone/OTP or Google OAuth2. They have a dedicated profile dashboard to manage addresses and view order history.
*   **Dynamic Product Catalog:** A responsive storefront displaying organic products with real-time stock availability, filtering, and detailed product pages.
*   **Seamless Cart Experience:** Users can add/remove items with a smart cart that automatically merges "Guest" carts into "Authenticated" carts upon login. Built-in rate-limiting protects against checkout spam.
*   **Secure Checkout & Payments:** End-to-end checkout flow integrated with Razorpay. The system handles payment success/failures via secure Webhooks.
*   **Verified Customer Reviews:** Users can leave ratings and comments on products—but *only* if the system verifies they have successfully purchased the item.
*   **Automated Communication:** Customers receive automated HTML emails via AWS SES for Order Confirmations and Status updates, along with securely generated PDF invoices.
*   **Admin Dashboard:** A secure, role-based admin panel to dynamically manage products, inventory, user roles, and monitor incoming orders.

---

### 🚀 Key Architectural Highlights

*   **Modular Monolith Design:** The backend is consciously structured as a Modular Monolith using Package-by-Domain principles (`auth`, `product`, `order`, `payment`). This ensures high cohesion and loose coupling, making it ready to be split into microservices if scaling demands it in the future.
*   **Pessimistic Inventory Locking:** To prevent race conditions during high-concurrency checkouts, the inventory service implements pessimistic database locking (`findByProductIdWithLock`), guaranteeing that overselling is impossible.
*   **Payment Webhook Resilience:** Built a secure webhook endpoint to receive asynchronous payment updates from Razorpay. To handle potential network failures from the payment gateway, an asynchronous background worker actively polls the API to verify the status of long-pending orders.
*   **Database Optimization (UUIDv7, Indexing & N+1 Fixes):** Proactively eliminated N+1 database querying issues using JPA Join Fetches. Migrated the entire database from randomized UUIDv4 keys to sequential, time-ordered **UUIDv7** keys to drastically reduce PostgreSQL B-tree index fragmentation and optimize `INSERT` speeds. Implemented **B-Tree Indexing and Composite Indexing** across heavy-query columns (like multi-tenant or relational user queries) and applied precise **Pagination strategies** to handle large datasets effectively without loading them entirely into server memory.
*   **Idempotent Event Consumers:** Built SQS consumers (like the Notification Service and Invoice Generator) with strict idempotency checks using Redis and DB state tracking. This ensures that even if AWS SQS delivers a message twice, users won't receive duplicate emails or invoices.
*   **Docker & CI/CD Pipelines:** The application is fully containerized using Docker, with automated CI/CD pipelines configured to ensure code quality and reliable, repeatable deployments.
