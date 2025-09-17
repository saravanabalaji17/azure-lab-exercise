

* **VNet**
* **Public + Private subnets**
* **Route tables (public + private)**
* **Internet route in the public RT**
* **Jumpbox (AlmaLinux) with public IP**
* **Private VM (AlmaLinux) with no public IP**
* **Access private VM via jumpbox**

---

# 🔹 Lab Exercise: Azure Networking with Jumpbox & Private VM

---

## Step 1: Create Resource Group

1. Go to **Resource groups → Create**
2. Name:

   ```
   <studentname>-rg
   ```

   Example: `raj-rg`
3. Select region: `East US`
4. **Review + Create → Create**

---

## Step 2: Create Virtual Network

1. Go to **Virtual networks → Create**
2. Name:

   ```
   <studentname>-vnet
   ```

   Example: `raj-vnet`
3. Address space: `10.0.0.0/16`
4. Add subnets:

   * Public subnet → `10.0.1.0/24`
     Name: `<studentname>-public-subnet`
   * Private subnet → `10.0.2.0/24`
     Name: `<studentname>-private-subnet`
5. **Review + Create → Create**

---

## Step 3: Create Route Tables

### Public Route Table

1. Go to **Route tables → Create**

   * Name: `<studentname>-rt-public`
   * Resource group: `<studentname>-rg`
2. After creation → Open Route Table → Routes → **Add**

   * Name: `internet-route`
   * Address prefix: `0.0.0.0/0`
   * Next hop: `Internet`
3. Associate subnet: `<studentname>-public-subnet`

---

### Private Route Table

1. Create another route table:

   * Name: `<studentname>-rt-private`
   * Resource group: `<studentname>-rg`
2. No new routes needed (default local routes apply)
3. Associate subnet: `<studentname>-private-subnet`

---

## Step 4: Create Jumpbox VM (Public Access)

1. Go to **Virtual machines → Create**

   * Name: `<studentname>-jumpbox`
   * Image: **AlmaLinux 9**
   * Size: Standard\_B1s
   * Authentication: SSH key or password
   * Networking:

     * VNet: `<studentname>-vnet`
     * Subnet: `<studentname>-public-subnet`
     * Public IP: **Enabled**
     * NIC NSG: Allow **SSH (22)** inbound
2. **Review + Create → Create**

---

## Step 5: Create Private VM

1. Go to **Virtual machines → Create**

   * Name: `<studentname>-private-vm`
   * Image: AlmaLinux 9
   * Size: Standard\_B1s
   * Authentication: SSH key or password
   * Networking:

     * VNet: `<studentname>-vnet`
     * Subnet: `<studentname>-private-subnet`
     * Public IP: **None**
     * NIC NSG: Allow SSH (22) **only from VNet**
2. **Review + Create → Create**

---

## Step 6: Test Access

1. From your local PC → SSH into jumpbox:

   ```bash
   ssh azureuser@<jumpbox-public-ip>
   ```
2. Inside jumpbox → SSH into private VM using private IP:

   ```bash
   ssh azureuser@10.0.2.4
   ```

   (replace with actual private IP)

---

# ✅ End Result

* `<studentname>-jumpbox` → Public access (via public subnet + route)
* `<studentname>-private-vm` → No internet access, only reachable from jumpbox
* Route tables correctly applied:

  * Public RT → internet route `0.0.0.0/0`
  * Private RT → local only

---
