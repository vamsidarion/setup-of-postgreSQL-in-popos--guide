# setup-of-postgreSQL-in-popos--guide
Step-by-step setup guide for PostgreSQL on Pop!_OS
# PostgreSQL & pgAdmin Setup Guide

#### 🚀 PostgreSQL Installation Steps

#### Go to PostgreSQL official site and choose Linux → Ubuntu.
#### Run the following commands:

   #### Install PostgreSQL Common Utilities
   ### These are essential tools for managing multiple PostgreSQL versions.  
     sudo apt install -y postgresql-common

  #### Enable the PostgreSQL APT Repository Setup Script
  ###### This script prepares your system to install PostgreSQL from the official source.
    sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh
  #### Install Required Dependencies
  ###### Install curl and ca-certificates to fetch and validate the GPG key.
    sudo apt install curl ca-certificates
  #### Create Directory for PostgreSQL APT GPG Key
  ###### Ensure the directory exists before downloading the key.
    sudo install -d /usr/share/postgresql-common/pgdg
  #### Download PostgreSQL GPG Key
  ###### This key ensures package authenticity from the PostgreSQL repository.
    sudo curl -o /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc --fail https://www.postgresql.org/media/keys/ACCC4CF8.asc
  #### Add PostgreSQL APT Repository to Sources List
  ###### Make sure to replace $VERSION_CODENAME with your actual Ubuntu release name (e.g., jammy, focal, bionic).
    sudo sh -c "echo 'deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt $VERSION_CODENAME-pgdg main' > /etc/apt/sources.list.d/pgdg.list"
  #### Update Package List
  ######  This refreshes your system’s package index to recognize the new PostgreSQL packages.
    sudo apt update
  #### Install PostgreSQL
  ###### Finally, install PostgreSQL from the newly added repository.
    sudo apt -y install postgresql
  #### The PostgreSQL server starts automatically.
  ######  You can now begin interacting with PostgreSQL using the built-in psql command-line client.
  #### Switch to PostgreSQL User
  ######  Use the following command to switch to the default PostgreSQL superuser (postgres):
    sudo -i -u postgres
  #### Launch the psql Client
  ###### Now, open the PostgreSQL shell:
    psql
  #### You’ll see a prompt like:
  ######  postgres=#
  #### This means you're inside the PostgreSQL shell and can now run SQL queries.
  #### Exit psql
    To quit the PostgreSQL shell, type:
    \q
 #### Creating and Connecting to a Database in PostgreSQL
    After accessing the psql shell, you can create a new database and switch to it using the following commands:
 #### Create a new database
    createdb my_pgdb
 #### Connect to the newly created database
    psql -d my_pgdb
 #### Check Current Database Connection
    you can view connection details using:
    \conninfo
 #### Use pgAdmin for Graphical Interface (Optional)
    To interact with PostgreSQL using a graphical interface, you can install pgAdmin, which allows:

    Easy browsing of databases and tables

    Visual query execution

    User and role management
`
  #### Go to the pgAdmin Download Page
     Visit the official pgAdmin download page:
     👉 https://www.pgadmin.org/download/pgadmin-4-apt/
     Scroll down and click on “APT” under “Platform: Linux”.
  #### Install curl (if not already installed)
     sudo apt install curl 
  #### Add the pgAdmin Repository Key
  ######   This ensures the downloaded packages are verified.
     curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg
  #### Add the pgAdmin APT Repository
     sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
 #### Install pgAdmin
    You can choose any of the following based on how you want to use pgAdmin:
#####  ✅ Desktop + Web Mode:
    sudo apt install pgadmin4
##### ✅ Desktop Mode Only:
    sudo apt install pgadmin4-desktop
##### ✅ Web Mode Only:
    sudo apt install pgadmin4-web
# Setup Web Mode (Only if you installed pgadmin4-web)
    Configure the web server:
    sudo /usr/pgadmin4/bin/setup-web.sh
## You'll be prompted to enter:
    Email
    Password
    Confirm by pressing y
## Then, access pgAdmin in your browser:
    http://127.0.0.1/pgadmin4
## Add a PostgreSQL Server in pgAdmin
    Open pgAdmin (desktop).
    Right-click on Servers → Create → Server
    Under the General tab:
    Set a name like Localhost
    
    Under the Connection tab:
      Host: 127.0.0.1

    Username: postgres
      Password: (your PostgreSQL password)

    Click Save ✅  
## If you're unable to connect in pgAdmin due to a wrong password, you can easily reset it using the terminal.
 ##### Reset Password for PostgreSQL User (postgres)
      Open your terminal
 ##### Switch to the PostgreSQL user:
      sudo -i -u postgres
 ##### Enter the PostgreSQL shell:
      psql
 ##### Set a new password:
      \password postgres
 ##### It will prompt:
      Enter new password:
      Enter it again:
 ##### Exit the psql shell:
      \q
 ##### Exit back to your normal user:
      exit
## ✅ Now retry logging in to pgAdmin
      Username: postgres
      Password: (the one you just set)
      This should solve any login failures due to incorrect passwords.
 





