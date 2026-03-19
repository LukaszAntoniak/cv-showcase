# Authentication Gateway (Identity Proxy)

> **Note on Confidentiality:** This project is a proprietary commercial application developed under a Non-Disclosure Agreement (NDA). To respect intellectual property rights, the source code is not publicly available. This documentation serves as a functional and architectural case study.

---

## 🛡️ Business Context
The **Authentication Gateway** is a centralized **Identity-as-a-Service (IDaaS)** platform designed to unify and secure the authentication lifecycle across the enterprise ecosystem. It abstracts the complexities of Microsoft Entra ID (Azure AD) and MSAL, providing a single, hardened entry point for all internal applications.

* **Transition from Local Credentials to SSO:** Addresses the inherent security and usability limitations of traditional login/password approaches in enterprise React applications. By implementing MSAL, the system leverages **Single Sign-On (SSO)**, aligning with corporate identity standards and eliminating the need for insecure local credential management.

* **Centralized Identity Orchestration:** Replaces fragmented authentication implementations in individual apps with a "Single Source of Truth," ensuring a consistent and secure login experience across the entire organization.

* **Security "Air-Gap" (Token Obfuscation):** Implements a high-security protocol that removes sensitive Microsoft JWT tokens from the client-side environment (browser), effectively neutralizing the risk of token theft via Cross-Site Scripting (XSS).

* **Dynamic RBAC Distribution:** Functions as an authorization engine that maps complex Active Directory groups into simplified, actionable Role-Based Access Control (RBAC) models, consumed by frontends for dynamic feature management.

* **Audit & Session Governance:** Centralizes the tracking of user sessions and authentication events, providing security teams with a unified audit trail of access across all connected platforms (Manual Payment, Revenue Recognition, etc.).

---

## 🛠️ Tech Stack & Skills
* **Backend:** .NET Core 6 API (Containerized).
* **Frontend:** React (SPA), MSAL.js, HashRouter, State Management for Identity Handshaking.
* **Identity & Security:** OAuth2 / OpenID Connect (OIDC), MS Entra ID (B2B), AES-256 Encryption, MD5 Opaque Token Mapping.
* **Infrastructure:** IIS (Reverse Proxy), URL Rewrite Module, Docker, Windows Server 2019.
* **Database:** MS SQL Server 2016 (Bare-Metal).

---

## 🧠 Key Decisions & "Why"
* **Implementation of MSAL:** * *Why:* Traditional login/password credentials scale poorly and pose higher security risks. Transitioning to MSAL enabled **Single Sign-On (SSO)**, allowing for instant, centralized de-provisioning of access when a user leaves the organization.
* **Implementation of Opaque Token Exchange:** * *Why:* By exchanging the functional Microsoft JWT for a non-sensitive hash (pointer), the system ensures that even if a browser session is compromised, the attacker has no direct access to Microsoft Graph or other sensitive APIs.
* **IIS URL Rewrite for Service Masking:** * *Why:* Configured the Reverse Proxy to handle all routing. This integrates the Gateway into a unified "Frontline" IP space, matching the architecture of the *Manual Payment Hub* and *Revenue Recognition* modules.
* **Server-Side AES-256 Encryption:** * *Why:* Every token is encrypted before being stored in the database to ensure that in the event of a database breach, the tokens remain unreadable and useless.
* **Centralized RBAC Strategy:** * *Why:* Moving the role-mapping logic to the Gateway simplifies management. User permissions can be updated in a single database and reflected across all enterprise apps instantly without frontend code changes.

---

## 🚀 Key Achievements (Impact)

### 1. Hardened Security Posture (Zero-Token Exposure)
By removing sensitive JWTs from `LocalStorage` and browser memory, the application ecosystem became resilient against standard token-theft vectors.
> **Outcome:** Achieved a "Zero-Token Exposure" architecture for all connected internal applications.

### 2. Standardized Developer Experience
Created a "plug-and-play" authentication module for other internal development teams.
> **Outcome:** Reduced the time required to implement secure authentication in new projects from days to a few hours of configuration.

### 3. Compliance & Governance
By migrating to MSAL/SSO, the system achieved full compliance with corporate security policies regarding identity management.
> **Outcome:** Enhanced the organization's ability to respond to security incidents by enabling "Global Logout" and centralized session monitoring.

---

*Created for portfolio purposes. Contact me for a detailed walkthrough of the architectural decisions behind this project.*