# PostgreSQL-Installation on RHEL using online & using source code

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
 
- 1️⃣ Select the PostgreSQL Version: Choose the version you want (e.g., PostgreSQL 16).
- 2️⃣ Select Your Platform: Choose RHEL 8 or 9 depending on your system.
- 3️⃣ Select the Architecture: Ensure you select x86_64 (64-bit).
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
---
## PostgreSQL Installation Guide for RHEL Using Source Code
 
### Installing PostgreSQL from source allows for custom configurations and optimization for your specific environment. Follow these steps to compile and install PostgreSQL from source on RHEL.
```
 why source code:- 
✅ Custom Configurations: Modify compile options for performance tuning.
✅ Latest Features: Access the newest PostgreSQL versions before they hit repositories.
✅ Full Control: Choose your own installation paths and settings.
```
 
---
 
- Step 1: Install Required Dependencies
```
 
Before compiling PostgreSQL, install the necessary development tools and libraries:
 
sudo yum groupinstall -y "Development Tools"
sudo yum install -y gcc readline-devel zlib-devel
```
 
 
---
 
- Step 2: Download the PostgreSQL Source Code
```
Visit the PostgreSQL official website and choose the latest stable version. Then, download it using wget:
 
wget https://ftp.postgresql.org/pub/source/v16.4/postgresql-16.4.tar.gz
```
 
---
 
- Step 3: Extract the Source Code
```
Extract the downloaded archive and navigate into the source directory:
 
tar -xvzf postgresql-16.4.tar.gz
cd postgresql-16.4
```
 
---
 
- Step 4: Configure the Build Options
``` 
Run the configure script to prepare for compilation. The --prefix option specifies where PostgreSQL will be installed:
 
./configure --prefix=/usr/local/pgsql
 
```
---
 
- Step 5: Compile and Install PostgreSQL
```
Start the compilation process:
 
make
 
Once completed, install PostgreSQL:
 
sudo make install
```
 
---
 
- Step 6: Create PostgreSQL User and Directories
``` 
For security, create a dedicated PostgreSQL user and set up the data directory:
 
sudo useradd -m postgres
sudo mkdir -p /usr/local/pgsql/data
sudo chown -R postgres:postgres /usr/local/pgsql
```
 
---
 
- Step 7: Initialize the PostgreSQL Database
```
Switch to the postgres user and initialize the database cluster:
 
sudo -i -u postgres /usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
```
 
---
 
- Step 8: Start the PostgreSQL Server
```
Start the PostgreSQL server manually using pg_ctl:
 
sudo -i -u postgres /usr/local/pgsql/bin/pg_ctl -D /usr/local/pgsql/data start
```
 
---
 
- Step 9: Enable PostgreSQL to Start on Boot (Optional)
``` 
To make PostgreSQL start automatically on system boot, create a systemd service:
 
sudo cp contrib/start-scripts/linux /etc/init.d/postgresql
sudo chmod +x /etc/init.d/postgresql
sudo systemctl enable postgresql
``` 
 
---
 
- Step 10: Connect to PostgreSQL
``` 
Switch to the postgres user and open the PostgreSQL shell:
 
sudo -i -u postgres /usr/local/pgsql/bin/psql
 
Verify the installation:
 
SELECT version();
``` 
 
---
 

