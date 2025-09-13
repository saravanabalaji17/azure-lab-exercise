## 🎯 Lab Exercise: Create 3 Linux VMs in Availability Zones

### **Resource Group**

* **Name:** `<studentname>-rg`

---

### **Part 1 – Create Resource Group**

1. Log in to [Azure Portal](https://portal.azure.com).
2. Go to **Resource groups → Create**.

   * Resource group name: `<studentname>-rg`
   * Region: Choose a region that **supports Availability Zones** (e.g., *East US 2*, *West Europe*, *Central India*).
   * Click **Review + Create → Create**.

---

### **Part 2 – Create 3 Linux VMs across Zones**

We’ll create VMs one by one, placing each in a different Availability Zone.

#### **VM1**

* **Resource group:** `<studentname>-rg`
* **VM name:** `<studentname>-linux-vm1`
* **Region:** Same as RG
* **Availability options:** Availability zone
* **Zone:** 1
* **Image:** AlmaLinux OS 9 – x64 Gen2
* **Size:** Standard\_B1s
* **Authentication:** SSH public key (generate or use existing)
* **Inbound ports:** Allow SSH (22)
* Click **Review + Create → Create**

#### **VM2**

* **VM name:** `<studentname>-linux-vm2`
* **Zone:** 2
* Other settings same as above.

#### **VM3**

* **VM name:** `<studentname>-linux-vm3`
* **Zone:** 3
* Other settings same as above.

---

### **Part 3 – Verification**

1. After deployment, check all 3 VMs:

   * Go to **Virtual machines** → Select a VM → **Overview** → confirm **Availability Zone**.
2. Connect to each VM:

   ```bash
   ssh -i <studentname>-key.pem azureuser@<vm-public-ip>
   hostname && uptime
   ```
3. Confirm each VM is in a **different zone** (1, 2, 3).

---

### **Outcome**

* You now have **3 Linux VMs**, each in a different **Availability Zone**, ensuring resilience against a **datacenter failure** within the region.
* If one datacenter goes down, the other two VMs will still be running.
