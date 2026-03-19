# Revenue Recognition & Accounting Engine

> **Note on Confidentiality:** This project is a proprietary commercial application developed under a Non-Disclosure Agreement (NDA). To respect intellectual property rights, the source code is not publicly available. This documentation serves as a functional and architectural case study.

---

## 🛡️ Business Context
The **Revenue Recognition** system is a specialized financial engine designed to automate complex, multi-year financial lifecycles. It manages the transition from raw transactional data to validated accounting vouchers, ensuring compliance with internal financial standards that follow IFRS.

* **Revenue Amortization & Deferral:** Automates the release of deferred financial records over predefined contract periods.
* **Asynchronous ETL Orchestration:** Separates user-facing management from heavy data processing to ensure system responsiveness.
* **Automated Voucher Generation:** Replaces manual entry with a logic-based engine, eliminating human error in cross-departmental financial balancing.

---

## 🛠️ Tech Stack & Skills
* **Backend:** .NET 6 (.NET Web API & .NET Worker Service).
* **Messaging:** **Azure Service Bus** (Queues, Peek-Lock, MaxConcurrentCalls=1).
* **Identity:** MS Entra ID (B2B), Custom Auth Gateway (MSAL/OIDC).
* **Infrastructure:** **Docker Engine (Linux Mode)** (API & Worker), **IIS 10** (Reverse Proxy & Static Hosting), Windows Server 2019.
* **Database:** MS SQL Server 2016 (Bare-Metal).

---

## 🧠 Key Decisions & "Why"
* **Co-location with Logical Isolation:**
    * *Why:* Running the .NET Web API and Worker on the same Docker Linux engine reduces infrastructure complexity while providing "hard" resource boundaries that traditional Windows services lack.
* **IIS as Reverse Proxy & Static Host:**
    * *Why:* Leverages existing Windows infrastructure to handle SSL termination and serve the React SPA efficiently, acting as a secure gateway to the containerized Kestrel-based API.
* **Azure Service Bus for Sequential Task Queuing:**
    * *Why:* To decouple the UI from long-running tasks and enforce a "one-by-one" rule. This protects the legacy SQL Server from I/O spikes and deadlocks.
* **Containerized Worker Resource Limits:**
    * *Why:* Financial ETL is memory-intensive and prone to **Large Object Heap (LOH)** fragmentation. Using Docker with strict RAM limits ensures that memory is fully reclaimed upon task completion or failure.
* **Hardware-Level OOM Management:**
    * *Why:* Unlike IIS pools, Docker's resource enforcement is instant. If a division exceeds its quota, the container is recycled immediately, providing a "clean slate" for the next task.
* **Transactional "Peek-Lock" Resolution:**
    * *Why:* To ensure **Zero Data Loss**. The task is only "Completed" after a successful SQL commit. Any crash leads to an automatic, safe retry from the queue.

---

## 🚀 Key Achievements (Impact)

### 1. Eliminated "Noise Neighbor" Performance Issues
By encapsulating the heavy ETL into a Docker container with strict caps, the Worker can no longer starve the user-facing .NET Web API or the IIS host of resources.
> **Outcome:** Achieved 100% availability for critical business APIs during peak financial processing periods.

### 2. Safeguarded Legacy Database Integrity
Implemented a strictly sequential processing model that feeds data into SQL Server at a controlled pace.
> **Outcome:** Eliminated transaction timeouts and deadlocks, ensuring stable execution plans for complex accounting logic.

### 3. Automated Self-Healing Architecture
Leveraged the combination of Service Bus retries and Docker's restart policies to handle unexpected memory spikes.
> **Outcome:** Reduced manual IT intervention by 90%; the system automatically recovers and retries failed divisions without data loss.

---

*Created for portfolio purposes. Contact me for a detailed walkthrough of the architectural decisions behind this project.*