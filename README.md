# TicketSafe

## Warning

This project is intentionally vulnerable in parts for educational and demonstration purposes. It is designed to show how insecure application logic can be introduced, exploited, and remediated. Do not deploy it to production or expose it to the public internet.

## Project Overview

TicketSafe is a deliberately vulnerable multi-user support ticket API built with FastAPI to demonstrate common application security flaws and secure remediations.

The project is centered on a realistic support ticket workflow with different user roles, protected resources, and privileged actions. Instead of focusing on scanner output, TicketSafe focuses on how vulnerabilities happen inside the application itself, especially around authorization, data exposure, and abuse prevention.

## Why I Built This

I built TicketSafe to strengthen my application security skills and show that I can think like both a backend engineer and an AppSec engineer.

My earlier security work focused on scan automation and vulnerability workflow support. This project goes deeper into application-layer security by showing:

- how insecure business logic gets introduced
- how authenticated users can still abuse weak authorization
- how insecure API responses can expose too much data
- how those issues should be remediated in code and design

## Core Security Themes

TicketSafe is designed to demonstrate and document issues such as:

- Broken Object-Level Authorization (IDOR / BOLA)
- Broken Function-Level Authorization
- Excessive Data Exposure
- Missing Rate Limiting
- Insecure Attachment Access
- Weak or Missing Audit Logging

## Secure Remediations Demonstrated

The secure version of the project focuses on practical remediations, including:

- object ownership checks
- centralized role-based authorization
- safe response models
- rate limiting on sensitive routes
- controlled access to attachments
- improved audit logging for sensitive actions

## What This Project Is Meant to Show

This project is meant to show that I can:

- build a realistic API with a modern Python framework
- model insecure application logic intentionally
- reproduce exploit paths clearly
- explain root causes and business impact
- implement secure remediations cleanly
- document security findings like an AppSec engineer

## Tech Stack

- **Framework:** FastAPI
- **ASGI Server:** Uvicorn
- **ORM:** SQLAlchemy
- **Database:** SQLite
- **Validation / Serialization:** Pydantic
- **Testing / Demo:** Postman, curl, Python scripts
- **Documentation:** Markdown

## Planned Roles

TicketSafe uses a multi-role model to make authorization flaws more realistic.

- **User**  
  Can register, log in, create tickets, view their own tickets, and comment on their own tickets.

- **Agent**  
  Can view assigned tickets, update status, and add internal comments.

- **Admin**  
  Can view all tickets, assign tickets, manage user roles, export summaries, and review logs.

## Planned Core Entities

- User
- Ticket
- Comment
- Attachment
- AuditLog

## Example Vulnerability Scenarios

Examples of the kinds of issues TicketSafe is built to demonstrate:

- a normal user changes a ticket ID and accesses another user's ticket
- a non-admin user calls an admin-only endpoint because the route only checks authentication
- an API response includes internal or unnecessary fields that should not be exposed
- a login route has no rate limiting, allowing brute-force attempts
- a user accesses an attachment by guessing a direct file path or identifier

## Demo Flow

A typical demo flow for TicketSafe looks like this:

1. Create multiple users with different roles
2. Log in and create support tickets
3. Reproduce vulnerable behavior against insecure endpoints
4. Document the issue, root cause, and business impact
5. Apply secure remediations
6. Re-test the same workflows and confirm the fix

## Project Structure

```text
TicketSafe-AppSec-Lab/
├── README.md
├── .gitignore
├── requirements.txt
├── main.py
├── app/
│   ├── core/
│   │   ├── config.py
│   │   └── security.py
│   ├── db/
│   │   ├── base.py
│   │   └── session.py
│   ├── models/
│   │   ├── user.py
│   │   ├── ticket.py
│   │   ├── comment.py
│   │   ├── attachment.py
│   │   └── audit_log.py
│   ├── schemas/
│   │   ├── user.py
│   │   ├── ticket.py
│   │   ├── auth.py
│   │   └── comment.py
│   ├── api/
│   │   ├── deps.py
│   │   └── routes/
│   │       ├── auth.py
│   │       ├── tickets.py
│   │       ├── admin.py
│   │       ├── profile.py
│   │       └── attachments.py
│   ├── services/
│   └── utils/
├── scripts/
│   ├── seed_data.py
│   ├── exploit_idor.py
│   ├── exploit_admin_route.py
│   ├── brute_force_demo.py
│   └── verify_secure_routes.py
├── docs/
│   ├── project_spec.md
│   ├── architecture.md
│   ├── threat_model.md
│   ├── findings.md
│   ├── remediation.md
│   └── demo_walkthrough.md
├── tests/
├── screenshots/
├── demo/
└── notes/
```

## Getting Started

### Prerequisites

Make sure you have the following installed:

- Python 3.10+
- pip
- Git

### Installation

Clone the repository:

```bash
git clone https://github.com/chrispy-02/ticketsafe-appsec-lab.git
cd ticketsafe-appsec-lab
```

Create and activate a virtual environment:

**macOS / Linux**
```bash
python3 -m venv venv
source venv/bin/activate
```

**Windows**
```bash
python -m venv venv
venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

### Running the App

Start the FastAPI app with Uvicorn:

```bash
uvicorn main:app --reload
```

Once running, the app should be available at:

- **API root:** `http://127.0.0.1:8000`
- **Interactive docs:** `http://127.0.0.1:8000/docs`
- **ReDoc:** `http://127.0.0.1:8000/redoc`

## Current Status

TicketSafe is being built as an AppSec portfolio project. Some features, routes, exploit scripts, and documentation may still be in progress as the project evolves.

## Documentation

Additional project documentation lives in the `docs/` directory:

- **`docs/project_spec.md`**  
  Full project scope, goals, vulnerabilities, and remediation plan

- **`docs/architecture.md`**  
  High-level system design and security-relevant decisions

- **`docs/threat_model.md`**  
  Assets, actors, abuse cases, and controls

- **`docs/findings.md`**  
  Structured write-ups for vulnerabilities, reproduction steps, root cause, impact, and fixes

- **`docs/remediation.md`**  
  Notes on how vulnerable implementations were hardened

- **`docs/demo_walkthrough.md`**  
  Planned demo sequence for presenting the project

## Branch Strategy

The project is planned around a vulnerable-to-remediated progression:

- **`vulnerable-demo`**  
  Demonstrates intentionally insecure behavior for educational purposes

- **`main`**  
  Contains the remediated version with security controls applied

## Why This Project Is Different From a Scanner Project

TicketSafe is not a vulnerability scanner or scan orchestration platform.

Its purpose is to demonstrate how vulnerabilities happen inside the application itself. That includes insecure authorization logic, overexposed API responses, weak privileged action handling, and missing abuse controls. The focus is on exploitability, root cause, and remediation.

## Future Improvements

Planned improvements include:

- stronger automated tests for authorization logic
- Docker support
- more complete audit logging
- better file and attachment handling
- CI checks
- expanded findings documentation
- additional abuse-case test scripts

## Educational Use Only

This repository includes intentionally vulnerable patterns for learning, demonstration, and portfolio purposes. It should only be used in safe local environments that you control.

## License

This project is licensed under the MIT License.
