# Dump and Restore PostgreSQL on EC2

![image](https://github.com/user-attachments/assets/d405bd15-41a2-4df9-9282-8cc0b44b6a49)

Things to consider:

1. Network Connectivity (VPC, Subnet, SG, and etc) 
2. The PostgreSQL client version on EC2 A and EC2 B must be the same



## 1. Install PostgreSQL Client on EC2 A
To access the PostgreSQL database from EC2 Apps, you need to install the PostgreSQL Client.

Run the following command:
```sh
sudo apt update && sudo apt install -y postgresql-client-17
```

## 2. Access PostgreSQL Database on EC2 B (Connectivity Check)
Once the installation is complete, use the following command to access the database:
```sh
PGPASSWORD="<passwoord>" psql -h <private-ip> -U <username> -d <database_name>
```
If you encounter any errors, please share the error message for further assistance. 🚀

---

# Dump & Restore PostgreSQL Database
## **Note:**
Ensure that the PostgreSQL Client version used for dumping and restoring is the same to avoid compatibility issues.

## 1. Dump PostgreSQL Database on EC2 A
Run the following command to create a database dump:
```sh
sudo PGPASSWORD="<password>" pg_dumpall -h 10.0.147.10 -U <username> -f sl_dump.sql
```

## 2. Restore PostgreSQL Database on EC2 A
Steps to restore the database on EC2 Apps:

### a. Install PostgreSQL on EC2 Apps (If not already installed)
https://github.com/rickichann/db-tutor-installing-postgresql-on-ubuntu 

### b. Move the dump file to the PostgreSQL directory
```sh
sudo mv sl_dump.sql /var/lib/postgresql/
sudo chown postgres:postgres /var/lib/postgresql/sl_dump.sql
sudo chmod 644 /var/lib/postgresql/sl_dump.sql
```

### c. Run the restore process on EC2 A
```sh
sudo PGPASSWORD="<password>" psql -U <username> -f /var/lib/postgresql/sl_dump.sql
```

After the restore process is complete, make sure to verify that the data has been successfully recovered. 🚀

