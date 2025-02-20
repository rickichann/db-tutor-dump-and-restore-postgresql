# db-tutor-dump-and-restore-postgresql

# Access EC2 Apps to EC2 Database

## 1. Install PostgreSQL Client on EC2 A
To access the PostgreSQL database from EC2 A, you need to install the PostgreSQL Client.

Run the following command:
```sh
sudo apt update && sudo apt install -y postgresql-client
```

## 2. Access PostgreSQL Database
Once the installation is complete, use the following command to access the database:
```sh
PGPASSWORD="richan" psql -h 10.0.147.10 -U richan -d sl_trans_db
```
If you encounter any errors, please share the error message for further assistance. 🚀

---

# Dump & Restore PostgreSQL Database
## **Note:**
Ensure that the PostgreSQL Client version used for dumping and restoring is the same to avoid compatibility issues.

## 1. Dump PostgreSQL Database
Run the following command to create a database dump:
```sh
sudo PGPASSWORD="postgres" pg_dumpall -h 10.0.147.10 -U postgres -f sl_dump.sql
```

## 2. Restore PostgreSQL Database
Steps to restore the database on EC2 Apps:

### a. Install PostgreSQL on EC2 Apps (If not already installed)
```sh
sudo apt update && sudo apt install -y postgresql
```

### b. Move the dump file to the PostgreSQL directory
```sh
sudo mv sl_dump.sql /var/lib/postgresql/
sudo chown postgres:postgres /var/lib/postgresql/sl_dump.sql
sudo chmod 644 /var/lib/postgresql/sl_dump.sql
```

### c. Run the restore process
```sh
sudo PGPASSWORD="postgres" psql -U postgres -f /var/lib/postgresql/sl_dump.sql
```

After the restore process is complete, make sure to verify that the data has been successfully recovered. 🚀

