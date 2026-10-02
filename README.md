# The Pine House, a modern cloud native ecommerce store - Project Summary
https://thepinehouse.in/

> Multi-cloud monorepo — Spring Boot on AWS Lightsail + FastAPI/LangGraph on self-managed GCP cloud run — with event-driven SQS messaging, CI via GithubActions, and Terraform-managed infrastructure.


The platform handles product catalog, inventory, orders, payments, logistics, notifications, and AI-powered customer support.

## Architecture

### Backend Service
![Service Architecture](./assets/serviceArch.png)

---

### AI Service
![Service Architecture](./assets/aiServiceArchitecture.png)

---

### Tech Stack

### Backend

![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge\&logo=springboot\&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge\&logo=openjdk\&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge\&logo=postgresql\&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge\&logo=supabase\&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge\&logo=redis\&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-FF9900?style=for-the-badge\&logo=amazonaws\&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge\&logo=docker\&logoColor=white)

### AI Service

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge\&logo=python\&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge\&logo=fastapi\&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge\&logo=langchain\&logoColor=white)

### Cloud & Infrastructure

![GCP](https://img.shields.io/badge/GCP-4285F4?style=for-the-badge\&logo=googlecloud\&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge\&logo=terraform\&logoColor=white)

## Key Features

* Product catalog and inventory management
* Customer authentication with Google OAuth
* Cart and order management
* Razorpay payments and webhook processing
* Shiprocket logistics integration
* SMS and email notifications
* Slack-based admin operations
* AI-powered customer support
* RAG-based product and knowledge-base search
* Redis-based caching, sessions, rate limiting and idempotency
* Asynchronous processing using AWS SQS

## Repository Structure

```text
Hill-Harvest-Organics/
├── backend/          # Spring Boot backend
├── ai_service/       # FastAPI + LangGraph AI service
└── infrastructure/   # Terraform infrastructure
```

## Deployment

The backend runs on **AWS**, while the AI service runs independently on **GCP Cloud Run**.

Infrastructure is provisioned using Terraform and deployments are automated through GitHub Actions.

## Integrations

* Google OAuth
* Razorpay
* Shiprocket
* 2Factor.in
* Slack
* Grafana Cloud
* Google Gemini
* OpenAI
* Groq
* Jina AI


* Google OAuth
* Razorpay
* Shiprocket
* 2Factor.in
* Slack
* Grafana Cloud
* Google Gemini
* OpenAI
* Groq
* Jina AI


## 🎥 Demo (Store Assistant)

<p align="center">
  <h3> 1. Catalog suggestions</h3>
  <img src="assets/suggestionDemo.gif" width="300"/> </br>
  <h3> 2. Support agent for queries related to orders</h3>
  <img src="assets/supportDemo.gif" width="300"/> </br>
  <h3> 3. Retrieval from knowledge base</h3>
  <img src="assets/faq_policyAgent.gif" width="300"/>
</p>
