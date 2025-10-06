# Zero Trust Network Access (ZTNA) Model using OpenZiti

## I. Project Objective
This project aims to build a complete **Zero Trust Network Access (ZTNA)** model using **OpenZiti**.  
The objective is to establish **secure, identity-based, and policy-driven access** to distributed resources across **multi-cloud** and **on-premise** platforms, replacing the traditional VPN model.

---

## II. System Architecture

**The architecture includes:**

- 1 AWS instance running the **Policy Engine (PE)** and **Policy Enforcement Point (PEP)**
- 1 Azure virtual machine hosting a **PostgreSQL database resource**
- 1 Kali machine hosting a **local Apache web resource**
- 1 Windows machine, 1 Ubuntu machine, and 1 Android device used to **remotely access the resources**

![Architecture](https://github.com/user-attachments/assets/9c9eb458-fbbc-42e3-9f5a-d3364ad34dc3)

---

## III. Identity and Policy Configuration

<img width="3840" height="2409" alt="Configuration" src="https://github.com/user-attachments/assets/cf1b5598-3500-4405-be16-ed025a85c9ee" />

### 1. Identities

**Client Identities:**
- **client-user-A:** Represents a user with web-only access rights, assigned the `#web-clients` attribute.  
- **client-user-B2:** Represents a user with database access rights, assigned the `#db-clients` attribute.  

**Hosting Identities (Terminators):**
- **kali-local-host:** The server hosting the web service, assigned the `#web-hosts` attribute.  
- **azure-db-host:** The server hosting the database, assigned the `#db-hosts` attribute.  

---

### 2. Services
- **apache-service:** Represents the Apache web service.  
- **postgres-service:** Represents the PostgreSQL database service.  

---

### 3. Policies

**Dial Policy:** Grants an Identity permission to initiate a connection to a Service.  
**Bind Policy:** Grants an Identity permission to host/receive a connection for a Service.  

**Defined policies:**

**1. For the Web Service**
- **web-dial-policy:** Allows identities with the `#web-clients` attribute (i.e., `client-user-A`) to Dial the `@apache-service`.  
- **web-bind-policy:** Allows identities with the `#web-hosts` attribute (i.e., `kali-local-host`) to Bind the `@apache-service`.  

**2. For the Database Service**
- **db-dial-policy:** Allows identities with the `#db-clients` attribute (i.e., `client-user-B2`) to Dial the `@postgres-service`.  
- **db-bind-policy:** Allows identities with the `#db-hosts` attribute (i.e., `azure-db-host`) to Bind the `@postgres-service`.  

---

### Reference
**Documentation:** [https://netfoundry.io/docs/openziti/learn/introduction/](https://netfoundry.io/docs/openziti/learn/introduction/)
