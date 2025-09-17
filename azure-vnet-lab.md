

* **VNet**
* **Public + Private subnets**
* **Route tables (public + private)**
* **Internet route in the public RT**
* **Jumpbox (AlmaLinux) with public IP**
* **Private VM (AlmaLinux) with no public IP**
* **Access private VM via jumpbox**



# 🔹 Lab Exercise: Public & Private VNet with Jumpbox

## 1. Create Resource Group

1. Go to **Azure Portal** → **Resource Groups** → **Create**.
2. Name: `RG-Network-Lab`
3. Region: Choose your region (e.g., East US).
4. Click **Review + Create → Create**.

---

## 2. Create Virtual Network

1. Go to **Virtual Networks** → **Create**.
2. Name: `vnet-lab`
3. Resource Group: `RG-Network-Lab`
4. Address space: `10.0.0.0/16`
5. Click **Next: IP Addresses**

### Add Subnets

* **Public Subnet**

  * Name: `public-subnet`
  * Address range: `10.0.1.0/24`
* **Private Subnet**

  * Name: `private-subnet`
  * Address range: `10.0.2.0/24`

Click **Review + Create → Create**.

---

## 3. Create Route Tables

### Public Route Table

1. Go to **Route tables** → **Create**.
2. Name: `public-rt`
3. Resource Group: `RG-Network-Lab`
4. Region: same as VNet.

After creation:

* Go to **Routes** → **Add**.

  * Route name: `internet-route`
  * Address prefix: `0.0.0.0/0`
  * Next hop: `Internet`
  * Save.

Associate subnet:

* Go to **Subnet** → **Associate** → choose `public-subnet`.

---

### Private Route Table

1. Create another route table: `private-rt`
2. Associate with `private-subnet`.
   👉 (No route to Internet here, keeps VM private).

---

## 4. Create Jumpbox VM (Public Access)

1. Go to **Virtual Machines** → **Create VM**.
2. Resource Group: `RG-Network-Lab`
3. Name: `jumpbox-vm`
4. Image: **AlmaLinux 9 (latest)**
5. Size: Standard\_B1s (small, for lab).
6. Authentication: SSH key or password.
7. Networking:

   * VNet: `vnet-lab`
   * Subnet: `public-subnet`
   * Public IP: **Enabled** (auto-create).
   * NIC NSG: Allow SSH (22).
8. Create.

---

## 5. Create Private VM (Private Access)

1. Go to **Virtual Machines** → **Create VM**.
2. Name: `private-vm`
3. Image: AlmaLinux 9
4. Size: Standard\_B1s
5. Networking:

   * VNet: `vnet-lab`
   * Subnet: `private-subnet`
   * Public IP: **None**
   * NSG: Allow SSH from VNet (optional).
6. Create.

---

## 6. Test Connectivity

1. SSH into **Jumpbox**:

   ```bash
   ssh azureuser@<Public-IP-of-Jumpbox>
   ```
2. From Jumpbox, SSH into **Private VM** (use its private IP):

   ```bash
   ssh azureuser@10.0.2.4
   ```

   (replace `10.0.2.4` with actual private VM IP from portal).

---

# ✅ End Result

* **Public Subnet + Route Table → Internet access**
* **Private Subnet + Route Table → No direct Internet**
* **Jumpbox VM (Public) → can SSH to Private VM**
* **Private VM → only accessible through Jumpbox**

---
