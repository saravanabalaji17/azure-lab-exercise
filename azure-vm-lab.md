## 🎯 Lab Exercise: Create Linux & Windows VMs in Azure

### **Resource Group**

* **Name:** `<studentname>-rg`

---

### **Part 1 – Create Linux Virtual Machine**

1. Sign in to the **Azure Portal** → [https://portal.azure.com](https://portal.azure.com).
2. In the left menu, click **Resource groups** → **Create**

   * Resource group name: `<studentname>-rg`
   * Region: Choose the nearest region
   * Click **Review + Create → Create**
3. In the search bar, type **Virtual machines** → **Create → Azure Virtual Machine**

   * **Resource group:** `<studentname>-rg`
   * **VM name:** `<studentname>-linux-vm`
   * **Region:** Same as RG
   * **Image:** *AlmaLinux OS 9 – x64 Gen2* (or Ubuntu if AlmaLinux not available)
   * **Size:** Standard\_B1s (free tier eligible)
   * **Authentication type:** SSH public key

     * Generate new key pair → Key name: `<studentname>-key`
   * **Inbound ports:** Allow SSH (22)
   * Click **Review + Create → Create**
   * Download the **private key (.pem)** if prompted.

✅ Linux VM is created. You can connect using:

```bash
ssh -i <studentname>-key.pem azureuser@<public-ip>
```

---

### **Part 2 – Create Windows Virtual Machine**

1. In Azure Portal, go to **Virtual machines** → **Create → Azure Virtual Machine**

   * **Resource group:** `<studentname>-rg`
   * **VM name:** `<studentname>-windows-vm`
   * **Region:** Same as Linux VM
   * **Image:** *Windows Server 2022 Datacenter – x64 Gen2*
   * **Size:** Standard\_B2s (or free tier eligible if available)
   * **Authentication type:** Password

     * Username: `azureuser`
     * Password: `<choose-strong-password>`
   * **Inbound ports:** Allow RDP (3389)
   * Click **Review + Create → Create**

✅ Windows VM is created. You can connect using **Remote Desktop (RDP)**:

* Open **Remote Desktop Connection** (`mstsc` on Windows)
* Enter VM’s **Public IP**
* Login with username `azureuser` and your password.

---

### **Verification**

* **Linux VM** → run:

  ```bash
  whoami && hostname
  ```
* **Windows VM** → open **PowerShell** and run:

  ```powershell
  whoami ; hostname
  ```
