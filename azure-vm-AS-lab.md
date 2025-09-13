## 🎯 Lab Exercise: Create 3 Linux VMs in an Availability Set

### **Resource Group**

* **Name:** `<studentname>-rg`

---

### **Part 1 – Create Resource Group**

1. Sign in to [Azure Portal](https://portal.azure.com).
2. Go to **Resource groups → Create**.

   * Name: `<studentname>-rg`
   * Region: (e.g., *East US*, *Central India*)
   * **Review + Create → Create**

---

### **Part 2 – Create Availability Set**

1. In the search bar, type **Availability sets** → **Create**

   * Resource group: `<studentname>-rg`
   * Name: `<studentname>-availset`
   * Region: same as RG
   * Fault domains: **2** (simulates racks/power units)
   * Update domains: **5** (for rolling updates)
   * Click **Review + Create → Create**

---

### **Part 3 – Create 3 Linux VMs inside the Availability Set**

#### **VM1**

* Go to **Virtual machines → Create**
* Resource group: `<studentname>-rg`
* VM name: `<studentname>-linux-vm1`
* Region: same as RG
* **Availability options:** Availability set → Select `<studentname>-availset`
* Image: AlmaLinux OS 9 – x64 Gen2
* Size: Standard\_B1s
* Authentication: SSH public key
* Inbound ports: Allow SSH (22)
* Review + Create → Create

#### **VM2**

* VM name: `<studentname>-linux-vm2`
* Availability set: `<studentname>-availset`
* Other settings same as VM1

#### **VM3**

* VM name: `<studentname>-linux-vm3`
* Availability set: `<studentname>-availset`
* Other settings same as VM1

---

### **Part 4 – Verification**

1. Open **Availability Set → Instances**

   * Confirm VMs are distributed across **Fault Domains (FDs)** and **Update Domains (UDs)**.
2. Connect to each VM using SSH and check:

   ```bash
   hostname && uptime
   ```

---

### **Outcome**

* You now have **3 Linux VMs** inside an **Availability Set**.
* Azure ensures:

  * At least **one VM stays up** during planned maintenance (update domains).
  * VMs are distributed across different **fault domains** (different racks/power sources).


