# 📁 File Access Management for Organizational Branches

This guide describes how to configure directory structures, user accounts, and access permissions for various organizational branches so that users can manage files securely within their respective areas.

---

## 🛠️ Prerequisites

- You must have **root/sudo access** to the system.
- All commands assume execution on a **Linux/Unix** shell (e.g., bash).

---

## ✅ Step 1: Create Branch Directories

Each department or branch will have its own directory under `/org`.

```bash
sudo mkdir -p /org/{HR,Finance,Sales,Marketing,IT}
```
## ✅ Step 2: Create User Accounts

Create user accounts for each department:

```bash
# HR
sudo useradd Prajwal
sudo useradd Samarth

# Finance
sudo useradd Ashray
sudo useradd Pavani

# Sales
sudo useradd Mahith
sudo useradd Raghu
sudo useradd Pratham

# Marketing
sudo useradd Atrinandan
sudo useradd Rushil

# IT
sudo useradd Pavan
sudo useradd Abhinandan
```
## ✅ Step 3: Create Personal Folders Inside Branch Directories
Creating the personal account in the each department 

```bash
# HR
sudo mkdir -p /org/HR/{Prajwal,Samarth}

# Finance
sudo mkdir -p /org/Finance/{Ashray,Pavani}

# Sales
sudo mkdir -p /org/Sales/{Mahith,Raghu,Pratham}

# Marketing
sudo mkdir -p /org/Marketing/{Atrinandan,Rushil}

# IT
sudo mkdir -p /org/IT/{Pavan,Abhinandan}
```

## ✅ Step 4: Assign Ownership and Permissions
Use `chown` and `chmod` to control access. Users will have `read/write/delete` access to their folders and their branch folder, but no access to others.

```bash
# HR
sudo chown -R Prajwal:Prajwal /org/HR/Prajwal
sudo chown -R Samarth:Samarth /org/HR/Samarth
sudo chmod 770 /org/HR
sudo chmod 700 /org/HR/*

# Finance
sudo chown -R Ashray:Ashray /org/Finance/Ashray
sudo chown -R Pavani:Pavani /org/Finance/Pavani
sudo chmod 770 /org/Finance
sudo chmod 700 /org/Finance/*

# Sales
sudo chown -R Mahith:Mahith /org/Sales/Mahith
sudo chown -R Raghu:Raghu /org/Sales/Raghu
sudo chown -R Pratham:Pratham /org/Sales/Pratham
sudo chmod 770 /org/Sales
sudo chmod 700 /org/Sales/*

# Marketing
sudo chown -R Atrinandan:Atrinandan /org/Marketing/Atrinandan
sudo chown -R Rushil:Rushil /org/Marketing/Rushil
sudo chmod 770 /org/Marketing
sudo chmod 700 /org/Marketing/*

# IT
sudo chown -R Pavan:Pavan /org/IT/Pavan
sudo chown -R Abhinandan:Abhinandan /org/IT/Abhinandan
sudo chmod 770 /org/IT
sudo chmod 700 /org/IT/*
```

##✅ Step 5: (Optional) Group Access Management
To allow HR users to view all folders (for auditing or administration), you could create an hrgroup, add HR users to it, and grant read/execute permissions on all directories.
```bash
# Create HR group
sudo groupadd hrgroup
sudo usermod -aG hrgroup Prajwal
sudo usermod -aG hrgroup Samarth

# Add HR group permission to all user folders
sudo setfacl -m g:hrgroup:rx /org/*/*
```

##✅ Step 6: Verify Access
You can switch to each user account and verify they can create, read, and delete files only in their designated folders.
```bash
# Switch to Samarth
su - Samarth
echo "Hello HR" > /org/HR/Samarth/hello.txt
cat /org/HR/Samarth/hello.txt
rm /org/HR/Samarth/hello.txt

```

#🧾 Command Summary
```bash
# Create directories
sudo mkdir -p /org/{HR,Finance,Sales,Marketing,IT}

# Create users (sample)
sudo useradd Prajwal
sudo useradd Samarth
# Repeat for others...

# Create personal folders
sudo mkdir -p /org/HR/{Prajwal,Samarth}
# Repeat for others...

# Set ownership
sudo chown -R Samarth:Samarth /org/HR/Samarth
# Repeat for others...

# Set permissions
sudo chmod 770 /org/HR
sudo chmod 700 /org/HR/*
# Repeat for other departments
```
