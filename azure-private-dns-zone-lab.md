

# 🧪 Azure Private DNS Zone – Lab Exercise

### 🎯 Goal

* Create a Private DNS Zone in Azure
* Link it to a Virtual Network
* Add DNS records
* Test resolution between two VMs

### 🔹 Step 1: Create Resource Group

* **Name:** `<studentname>_rg`
* Example: `Arun_rg`

---

### 🔹 Step 2: Create Virtual Network & Subnet

* **VNet Name:** `<studentname>_vnet`
* Address space: `10.10.0.0/16`
* **Subnet Name:** `<studentname>_subnet1`
* Subnet range: `10.10.1.0/24`

---

### 🔹 Step 3: Deploy Two VMs

* **VM1 Name:** `<studentname>_vm1`
* **VM2 Name:** `<studentname>_vm2`
* Place both inside: `<studentname>_vnet` → `<studentname>_subnet1`

✅ Verify connectivity by pinging private IPs between VMs.

---

### 🔹 Step 4: Create Private DNS Zone

* **Private DNS Zone Name:** `<studentname>_privatedns.local`
* Example: `Arun_privatedns.local`

---

### 🔹 Step 5: Link DNS Zone to VNet

* Inside the DNS Zone → **Virtual Network Links → + Add**
* **Link Name:** `<studentname>_vnetlink`
* Select `<studentname>_vnet`
* Enable **Auto-registration** ✅

---

### 🔹 Step 6: Add DNS Records

1. **A Record**

   * Name: `<studentname>_app1`
   * IP: Private IP of `<studentname>_vm1`

2. **CNAME Record**

   * Name: `<studentname>_web`
   * Alias: `<studentname>_app1.<studentname>_privatedns.local`

---

### 🔹 Step 7: Test DNS Resolution

From **`<studentname>_vm2`** run:

```bash
nslookup <studentname>_app1.<studentname>_privatedns.local
nslookup <studentname>_web.<studentname>_privatedns.local
ping <studentname>_app1.<studentname>_privatedns.local
```

✅ Should resolve to `<studentname>_vm1` private IP.

---

### 🔹 Step 8: Verify Auto-Registration

* On `<studentname>_vm1`, check hostname:

  ```bash
  hostname
  ```

* Then from `<studentname>_vm2`:

  ```bash
  nslookup <hostname>.<studentname>_privatedns.local
  ```

---

## 📝 Expected Outcome

* All DNS queries resolve within the VNet using the Private DNS Zone.
* Naming convention makes resources **organized and student-specific**.

---
