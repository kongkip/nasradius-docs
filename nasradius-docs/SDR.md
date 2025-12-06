
# System Requirements Document (SRD) for ISP Billing Software

## 1. Introduction

### 1.1 Purpose

This document outlines the system requirements for an Internet Service Provider (ISP) billing software developed using Django for the backend, React for the frontend, and integrated with FreeRADIUS for authentication, authorization, and accounting. It serves as a guideline for developers, stakeholders, and users involved in the development, deployment, and usage of the system.

### 1.2 Scope

The ISP billing software aims to provide a comprehensive solution for managing customer subscriptions, tracking service usage, generating invoices, processing payments, and offering detailed reports and analytics. The system will ensure secure and efficient operation for both the ISP's administrative staff and its customers.

### 1.3 Definitions and Acronyms

-   **API:** Application Programming Interface
-   **AAA:** Authentication, Authorization, and Accounting
-   **SRD:** System Requirements Document
-   **UI:** User Interface
-   **DB:** Database
-   **RADIUS:** Remote Authentication Dial-In User Service

## 2. Overall Description

### 2.1 User Needs

-   ISPs need a scalable and reliable system for billing and customer management.
-   Customers require easy access to their usage, billing information, and the ability to make payments online.

### 2.2 Assumptions and Dependencies

-   The system assumes reliable internet connectivity for accessing the web-based interface.
-   Payment processing depends on third-party services like PayPal or Stripe.

## 3. System Features and Requirements

### 3.1 Functional Requirements

#### 3.1.1 User Management

-   **FR1.1** The system shall allow the creation, modification, and deletion of user accounts.
-   **FR1.2** The system shall support role-based access control for different user types (admin, staff, customer).

#### 3.1.2 Service Plans Management

-   **FR2.1** Admins can create, update, and delete service plans, including details like speed, data caps, and pricing.

#### 3.1.3 Subscription Management

-   **FR3.1** Customers can view, subscribe to, and change service plans through the user interface.

#### 3.1.4 Billing and Invoicing

-   **FR4.1** The system shall automatically generate monthly invoices based on subscription and additional usage.
-   **FR4.2** Customers can view, download, and pay invoices through the UI.

#### 3.1.5 Payment Processing

-   **FR5.1** The system shall integrate with external payment gateways for processing payments.

#### 3.1.6 Usage Tracking and Reporting

-   **FR6.1** FreeRADIUS shall track data usage for billing purposes.
-   **FR6.2** The system shall offer reports on usage statistics, financials, and customer activity.

#### 3.1.7 Network Access Control and Management

-   **FR7.1** The system shall integrate with MikroTik routers to manage network access for hotspot and PPPoE users.
-   **FR7.2** The system shall support dynamic updates to MikroTik routers for user bandwidth limits, data caps, and other access parameters based on their subscription plan.
-   **FR7.3** MikroTik routers shall redirect unauthenticated users to a login page and authenticate them through the FreeRADIUS server.
-   **FR7.4** The system shall track user session data and usage metrics through interactions between MikroTik routers and the FreeRADIUS server, feeding this data into the billing and usage tracking mechanisms.

### 3.2 Non-Functional Requirements

#### 3.2.1 Performance

-   **NFR1** The system shall handle up to 10,000 concurrent users without significant degradation in performance.

#### 3.2.2 Scalability

-   **NFR2** The system shall be scalable to accommodate a growing number of users and data volume.

#### 3.2.3 Security

-   **NFR3** The system shall implement secure authentication, data encryption, and comply with relevant privacy regulations.

#### 3.2.4 Reliability

-   **NFR4** The system shall ensure an uptime of 99.9%, excluding scheduled maintenance.

### 3.3 System Interfaces

-   **SI1** RESTful API for backend/frontend communication.
-   **SI2** Integration interface with FreeRADIUS for AAA.
-   **SI3** Payment gateway APIs for financial transactions.
-   **SI4** The system shall interface with MikroTik routers for authenticating hotspot and PPPoE connections using the RADIUS protocol. This includes receiving access requests, sending authentication and accounting responses, and enforcing network policies as dictated by the Django backend.

### 3.4 User Interfaces

-   **UI1** Responsive web interface for both administrative staff and customers.
-   **UI2** Admin dashboard for managing users, subscriptions, and viewing reports.
-   **UI3** Customer portal for account management, billing, and usage reports.

### 3.5 Hardware and Software Requirements

#### 3.5.1 Backend (Django)

-   **HSR1** Server with Linux, 4+ CPU cores, 8GB+ RAM, and sufficient storage for the database and logs.
-   **HSR2** PostgreSQL or MySQL as the database system.

#### 3.5.2 Frontend (React)

-   **HSR3** Hosting environment capable of serving static assets and handling dynamic content delivery.

#### 3.5.3 FreeRADIUS Server

-   **HSR4** Server with Linux, 2+ CPU cores, 4GB+ RAM, and network connectivity to manage AAA requests.

## 4. Documentation and Support

### 4.1 Installation Guide

-   Detailed instructions for setting up the system components, including the Django backend, React frontend, and FreeRADIUS server.

### 4.2 User Manual

-   Comprehensive guides for end-users on how to use the software, including account management, subscription handling, and payment instructions.

### 4.3 Technical Support

-   Information on how to access technical support, including contact details and available hours.

## 5. Appendices

### 5.1 Glossary

-   Definitions of technical terms and acronyms used in the document.

### 5.2 Reference Documents

-   Links to external documents, API references, and third-party services documentation relevant to the project.

This System Requirements Document provides a comprehensive overview of the ISP billing software project, outlining the functional and non-functional requirements, system architecture, and user interaction with the system. It serves as a foundational document for the development, implementation, and maintenance of the system.

```mermaid
graph TD
    A[User] -->|Connects to Network| MT[MikroTik Router]
    MT -->|Redirects to Captive Portal| CP[Captive Portal Login]
    CP -->|User Logs In| F[FreeRADIUS Server]
    B[Web Interface] -.->|Interacts with| C[React Frontend]
    C -.->|API Calls| D[Django Backend]
    D -.->|Manages| E[Database]
    F -->|Authenticates & Authorizes| D
    D -.->|Processes Payments| G[Payment Gateway]
    F -.->|Tracks Usage & Sessions| MT
    E -.->|Read/Write| D
    G -.->|Transaction Info| D
    MT -.->|Requests AAA| F
    F -.->|Session Info & Control| MT
    D -->|Generates| CP
    F -->|Grants Access| A
    A -.->|Accesses Services| B

    classDef component fill:#f9f,stroke:#333,stroke-width:2px;
    class B,C,D,E,F,G,MT,CP component;
  ```
