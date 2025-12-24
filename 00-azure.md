---

## 1️⃣ What is Cloud Computing?

**Cloud computing** is the delivery of **IT resources over the internet** instead of running them in your own data center.

👉 You can use:

* Servers
* Storage
* Databases
* Networking
* Software

**without buying or managing physical hardware**.

📌 **In short:**

> *Cloud = Rent IT resources on demand via the internet*

---

## 2️⃣ Why Cloud Computing? (Why companies use cloud)

1. **No upfront hardware cost** – Pay only for what you use
2. **Scalability** – Increase or decrease resources in minutes
3. **High availability** – Built-in redundancy & disaster recovery
4. **Global reach** – Deploy applications anywhere in the world
5. **Faster deployment** – Create servers in minutes
6. **Less maintenance** – Cloud provider manages hardware
7. **Security & compliance** – Enterprise-grade security
8. **Cost optimization** – Stop resources when not needed

---

## 3️⃣ What is Microsoft Azure?

**Microsoft Azure** is **Microsoft’s cloud computing platform**.

It provides:

* **Compute** (VMs, Kubernetes, App Services)
* **Networking** (VNet, Load Balancer, Application Gateway)
* **Storage** (Blob, Disk, File)
* **Databases** (SQL, Cosmos DB)
* **Security & Identity** (Entra ID, Defender)

📌 **Simple definition:**

> *Azure is Microsoft’s cloud where you create and manage cloud resources.*

---

## 4️⃣ Azure Global Infrastructure

Azure runs on a **global network of Microsoft data centers**.

### 🌍 Global Infrastructure Hierarchy (Physical)

```
Geography
 └── Region
      └── Availability Zone (AZ)
           └── Datacenter
                └── Rack
                     └── Physical Server
                          └── Hypervisor (Hyper-V)
                               └── Virtual Machine
```

### Explanation (one line each)

| Level                 | Meaning                                              |
| --------------------- | ---------------------------------------------------- |
| **Geography**         | Large global area (Asia, Europe, US) for compliance  |
| **Region**            | A set of nearby datacenters (East US, Central India) |
| **Availability Zone** | Physically separate datacenters in a region          |
| **Datacenter**        | Azure facility with power, cooling, security         |
| **Rack**              | Holds multiple physical servers                      |
| **Physical Server**   | Hardware (Dell / HP / Azure custom servers)          |
| **Hypervisor**        | Hyper-V that runs virtual machines                   |
| **VM**                | Your virtual server                                  |

---

## 5️⃣ Azure Hierarchy (Logical / Resource Hierarchy)

This defines **how Azure resources are organized**.

```
Management Group
 └── Subscription
      └── Resource Group
           └── Resources
```

### Explanation

| Level                | Purpose                                 |
| -------------------- | --------------------------------------- |
| **Management Group** | Manage multiple subscriptions together  |
| **Subscription**     | Billing + access boundary               |
| **Resource Group**   | Logical container for related resources |
| **Resources**        | VM, VNet, Storage, App Gateway, etc.    |

---

## 6️⃣ Azure Management Hierarchy (Governance)

Used for **policy, security, and access control**.

```
Entra ID (Tenant)
 └── Management Group
      └── Subscription
           └── Resource Group
                └── Resources
```

### Key Concepts

| Component      | Meaning                                 |
| -------------- | --------------------------------------- |
| **Entra ID**   | Identity service (users, groups, roles) |
| **Tenant**     | Instance of Entra ID                    |
| **RBAC**       | Who can do what                         |
| **Policies**   | Rules (allowed regions, VM sizes)       |
| **Blueprints** | Standard environments                   |

📌 **Important interview line:**

> *Subscriptions trust a single Entra ID tenant for authentication.*

---

## 7️⃣ How everything connects (Simple Flow)

```
User
 └── Authenticates via Entra ID (Tenant)
      └── Gets access to Subscription
           └── Manages Resource Groups
                └── Creates Resources in Azure Regions
```

---

## 8️⃣ One-line Summary (Perfect for interviews)

> **Cloud computing** provides on-demand IT resources over the internet.
> **Azure** is Microsoft’s cloud platform with a global infrastructure of regions and datacenters, organized using a management hierarchy for governance, security, and cost control.

---
