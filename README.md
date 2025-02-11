# PostgreSQL-Installation on RHEL

### PostgreSQL can be installed easily on RHEL using the official PostgreSQL Yum Repository. Follow the steps below to set up a PostgreSQL server on your RHEL system.
 
 
---
 
### Step 1: Visit the Official PostgreSQL Website
 
1. Open PostgreSQL Download Page.
 
 
2. Select your Linux Operating System Family (e.g., Linux).
 
 
3. Choose your Linux Distribution (Red Hat).
 
 
4. Follow the provided repository setup instructions.

---
 
### Step 2: Configure the Yum Repository
 
PostgreSQL is not included in the default RHEL repositories. You must install the PostgreSQL Yum repository before proceeding.
 
1️⃣ Select the PostgreSQL Version: Choose the version you want (e.g., PostgreSQL 16).
2️⃣ Select Your Platform: Choose RHEL 8 or 9 depending on your system.
3️⃣ Select the Architecture: Ensure you select x86_64 (64-bit).
```
Now, install the repository using the following command:
 
sudo yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-9-x86_64/pgdg-redhat-repo-latest.noarch.rpm
---
 
Step 3: Disable Built-in PostgreSQL Modules
 
RHEL comes with a built-in PostgreSQL module, which must be disabled to use the official repository.
 
sudo dnf -qy module disable postgresql

---
Step 4: Install PostgreSQL Server and Client
 
Once the repository is set up, install PostgreSQL using:
 
sudo yum install -y postgresql16 postgresql16-server
---
Step 5: Initialize the PostgreSQL Database Cluster
 
After installation, initialize the PostgreSQL database cluster:
 
sudo /usr/pgsql-16/bin/postgresql-16-setup initdb
 
---
Step 6: Enable and Start PostgreSQL
 
To ensure PostgreSQL starts automatically on boot, run:
sudo systemctl enable postgresql-16
sudo systemctl start postgresql-16
 
Verify that PostgreSQL is running:
sudo systemctl status postgresql-16
 
---
 
Step 7: Access the PostgreSQL Database
 
Switch to the PostgreSQL user and connect to the database:
 
sudo -i -u postgres psql
 
Check the installed PostgreSQL version:
 
SELECT version();

```
 

