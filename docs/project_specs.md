# Project Specification: TicketSafe

## 1. Overview
*   **Project Name**: TicketSafe
*   **Status**: Initial Specification
*   **One-Sentence Description**: A deliberately vulnerable multi-user support ticket API built with FastAPI to demonstrate common application security flaws and secure remediations.
*   **Primary Objective**: To demonstrate mastery of both backend engineering and Application Security (AppSec) by modeling, exploiting, and fixing insecure business logic.

## 2. Core Theme: Broken Access Control
This project focuses on the transition from authentication (who you are) to authorization (what you are allowed to do), specifically targeting **Broken Object Level Authorization (BOLA/IDOR)** and **Broken Function Level Authorization**.

## 3. Architecture & Entities
### User Roles
*   **User**: Standard customer; can manage their own tickets.
*   **Agent**: Support staff; can manage assigned tickets and internal notes.
*   **Admin**: System manager; full visibility and user management.

### Data Model
*   **User**: Identity and role management.
*   **Ticket**: The core unit of work (Subject, Description, Status).
*   **Comment**: Threaded communication (Public vs. Internal).
*   **Attachment**: Files associated with tickets.
*   **AuditLog**: Record of sensitive system actions.

## 4. Technical Stack
*   **Framework**: FastAPI (with Uvicorn ASGI)
*   **Database**: SQLite (Development-friendly)
*   **ORM**: SQLAlchemy
*   **Data Validation**: Pydantic
*   **Testing/Exploitation**: Postman, cURL, Pytest
*   **Deployment**: Docker (Planned)

## 5. Security Lab: Vulnerabilities vs. Controls

| Vulnerability (The "Flaw") | Secure Remediation (The "Fix") |
| :--- | :--- |
| **BOLA / IDOR**: Accessing any ticket via ID | Strict ownership checks on every request |
| **Broken Function Auth**: Users accessing Admin routes | Centralized Role-Based Access Control (RBAC) |
| **Excessive Data Exposure**: Leaking PII in API responses | Defined Pydantic Response Models (Filtering) |
| **Insecure Attachments**: Publicly accessible file paths | Signed URLs or session-based access control |
| **Missing Rate Limiting**: Brute-force on login | Middleware-based rate limiting |
| **Weak Logging**: No trail of sensitive changes | Robust Audit Logging for all state changes |

## 6. Development Strategy
*   **Branch `vulnerable-demo`**: Contains the intentionally flawed logic for demonstration and walkthroughs.
*   **Branch `main`**: The "hardened" version featuring all secure remediations.

## 7. Functional Requirements
- [ ] **Auth**: Implementation of JWT-based login/registration.
- [ ] **Ticket Lifecycle**: CRUD operations for tickets with role-based visibility.
- [ ] **Internal Notes**: Ensure 'Agent' comments are invisible to 'Users'.
- [ ] **Admin Panel**: Route for role escalation and audit log review.
- [ ] **Audit Trail**: Automated logging for every `POST/PATCH/DELETE` action.

## 8. Future Goals (Stretch)
*   Containerization via Docker.
*   Automated security unit tests (checking for 403s on unauthorized IDs).
*   Visualizing the attack surface with a Threat Model diagram.
