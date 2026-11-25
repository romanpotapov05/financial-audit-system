# Financial Audit & Internal Control Management System

![Java](https://img.shields.io/badge/Java-21-orange?style=flat-square&logo=openjdk)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen?style=flat-square&logo=springboot)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-17-blue?style=flat-square&logo=postgresql)
![Liquibase](https://img.shields.io/badge/Liquibase-Migrations-2962FF?style=flat-square)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat-square&logo=docker)
![Testcontainers](https://img.shields.io/badge/Testing-Testcontainers-purple?style=flat-square)

An enterprise-grade web application designed to digitize, standardize, and enforce internal financial audit workflows, control testing, and compliance tracking in corporate environments.

> **Academic Context:**  
> This project is developed as an Engineering Thesis (*Praca inżynierska*) at **Częstochowa University of Technology** (*Politechnika Częstochowska, Wydział Informatyki i Sztucznej Inteligencji*).  
> - **Polish Title:** *Projekt i implementacja systemu informatycznego wspomagającego proces przeprowadzania audytu wewnętrznego w zakresie procedur finansowych w przedsiębiorstwie.*  
> - **English Title:** *Design and implementation of an IT system supporting the internal audit process of financial procedures in an enterprise.*

---

## 🎯 Business Domain & Compliance Alignment

Financial audits in large enterprises require strict traceability, accountability, and adherence to internal control frameworks (such as **COSO**). This system replaces error-prone manual spreadsheets with an automated workflow featuring:

* **End-to-End Audit Lifecycle:** Planning engagements, executing control tests on financial procedures, logging findings (non-conformities), and tracking Corrective and Preventive Actions (CAPA).
* **Immutable Audit Trail:** Full entity-level revision history powered by **Hibernate Envers**, guaranteeing non-repudiation of every state transition and financial record modification.
* **Segregation of Duties (SoD):** Enforced business rules preventing conflicts of interest (e.g., an auditor cannot approve their own findings or audit a department they manage).
* **Automated Financial Rule Validation:** Server-side validation engine checking threshold anomalies, approval signatures, and procedural compliance.

---

## 🏗️ System Architecture

The backend follows a modular, domain-centric architecture designed for high maintainability and clear separation of business rules from infrastructure concerns.

```mermaid
flowchart LR
    Client[Angular / React SPA] -->|HTTPS / REST + JWT| Gateway[Spring Security Filter Chain]
    Gateway --> Controller[REST Controllers & DTO Validation]
    Controller --> Service[Domain Services & State Machine]
    Service --> Validation[Financial Rules Engine]
    Service --> Repo[Spring Data JPA]
    Repo --> Envers[Hibernate Envers Interceptor]
    Repo --> DB[(PostgreSQL)]
    Envers --> DB