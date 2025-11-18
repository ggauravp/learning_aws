# 1. Create an EC2 Instance
- Launch a new Ubuntu EC2 instance.
- When creating the instance:
  1. Add an SSH key pair (PEM)
  2. Add a security group that allows:
   - Port 22 → Your IP (for SSH)
   - Port 5432 → Your IP (for PostgreSQL access)

# 2. Downloand the SSH key pair in window

# 3. Copy the SSH key into WSL
- Inside WSL ubuntu create a folder
 - -  mkdir ~/ec2_keys
- copy the PEM file into this folder and set correct permissioin 
 - - chmod 600 ~/ec2_keys/your-key.pem

# 4. SSH into the EC2 Instance
  ssh -i ~/ec2_keys/your-key.pem ubuntu@(EC2-public-IP)

# 5. Install PostgreSQL on EC2
 - sudo apt update
 - sudo apt install postgresql -y

# 6. Configure PostgreSQL to Allow Remote Connections
1. Edit postgresql.conf
- sudo nano /etc/postgresql/16/main/postgresql.conf

  change 
  listen_adresses = '*'  

  [CTRL+O = SAVE, ENTER, CTRL+X = EXIT]

2. Edit pg_hba.conf
- sudo nano /etc/postgresql/16/main/pg_hba.conf

  Add following line at the bottom

  host    all     all     0.0.0.0/0     md5

                         (OR own ip/32)
                         
  [CTRL+O = SAVE, ENTER, CTRL+X = EXIT]
                     
3. Restart PostgreSQL
- sudo pg_ctlcluster 16 main restart

# 7. Create a PostgreSQL User and Database (on EC2)
- Enter PostgreSQL:

  sudo -u postgres psql

- Create user:

  CREATE USER myuser WITH PASSWORD 'mypassword';

- Create database:

  CREATE DATABASE mydb OWNER myuser;

- Exit:

  \q

# 8. Install PostgreSQL Client on Your Local WSL
- On WSL Ubuntu

  sudo apt update

  sudo apt install postgresql-client -y

# 9. Connect to EC2 PostgreSQL From WSL
- Make sure to exit from SSH now.

 psql -h <EC2-public-IP> -U myuser -d mydb

- Enter  PostgreSQL password and it will show:

  mydb=>
  
Meaning remote connection succeeded.
