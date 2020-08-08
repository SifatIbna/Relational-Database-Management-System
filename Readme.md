# Postgre SQL 

PostgreSQL, also known as Postgres, is a free and open-source relational database management system emphasizing extensibility and SQL compliance. Here we will discuss how to install and use postgre sql in details.


# Installation
Postgresql is an open source RDBMS ( Relational Management System) , available for Windows, Mac, Linux distribution.


## Windows Installation

For windows installation you have to follow thress steps :
- Download PostgreSQL installer for Windows
- Install PostgreSQL
- Verify the installation


### Download Postgresql installer for windows
From Postgresql official page 32 bit and 64 bit installer is available. From there download the installer and the rest is pretty much easy follow.
- One or Two things you have to remember though.
If you follow the installation instruction , then after some step the installer will ask you to give passwords. Remember it's for default **superuser** named **postgres**.
![Image of Yaktocat](https://sp.postgresqltutorial.com/wp-content/uploads/2020/07/Install-PostgreSQL-12-Windows-Step-5.png)

- Next the installer ask you to set a port. The default port of PostgreSQL is 5432. You need to make sure that no other applications are using this port.
- ![Image](https://sp.postgresqltutorial.com/wp-content/uploads/2020/07/Install-PostgreSQL-12-Windows-Step-6.png) 

To check if the installation is complete or not. Search for **psql** in windows search bar. If see a **SQL SHELL** , then the installation is complete.
![Image](https://sp.postgresqltutorial.com/wp-content/uploads/2020/07/Install-PostgreSQL-psql.png)

Second, enter all the necessary information such as the server, database, port, username, and password. To accept the default, you can press **Enter**. Note that you should provide the password that you entered during installing the PostgreSQL.
```console
Server [localhost]: (leave it blank or enter localhost, then press Enter)
Database [postgres]: (leave it blank or enter postgres, then Press Enter)
Port [5432]: (leave it blank or enter 5432, then Press Enter)
Username [postgres]: (leave it blank or enter postgres, then Press Enter)
Password for user postgres: (Give your password)
psql (12.3) 
WARNING: Console code page (437) differs from Windows code page (1252) 
		 8-bit characters might not work correctly. See psql reference page 
		 "Notes for Windows users" for details. Type "help" for help. 
postgres=#
```

**Third**, issue the command `SELECT version();` you will see the following output:
![Image](https://sp.postgresqltutorial.com/wp-content/uploads/2020/07/Install-PostgreSQL-psql-verification.png)

## Linux installation

Linux installation is different than windows installation.Here's how can you install postgresql in Linux Distriution. I am using UBUNTU 18.04 . But the command lines are pretty much same for other distribution.
- Create the file repository configuration: 
```console
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
```
- Import the repository signing key:
```console
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```
-  Update the package lists:
```console
sudo apt-get update
```
- Install the latest version of PostgreSQL.If you want a specific version, use **postgresql-12** or similar instead of **postgresql** :
```console
sudo apt-get install postgresql
```
It will take few minutes to download and install the PostgreSQL.
###  Connect to the PostgreSQL database server via psql
In PostgreSQL, a user account is referred to as a  [role](https://www.postgresqltutorial.com/postgresql-roles/). By default, PostgreSQL uses  **ident** authentication.

It means that PostgreSQL will associate its roles with the system accounts of Linux. If a role exists in PostgreSQL, the same Linux user account with the same name is able to log in as that role.

When you installed PostgreSQL, the installation process created a user account called  `postgres`  associated with the default  `postgres`  role.

To connect to PostgreSQL using the  `postgres`  role, you switch over to the  `postgres`  account on your server by typing:
```console
$ sudo -i -u postgres
```
It’ll prompt for the password of the current user. You need to provide the password and hit the  `Enter`  keyboard.

Then, you can access the PostgreSQL using the  `psql`  by typing the following command:
```console
$ psql
```
You’ll access the **postgres** prompt like this:
```console
postgres=#
```
From here, you can interact with the PostgreSQL like issuing a query.

To quit the PostgreSQL prompt, you run the following command:

```console
postgres=# \q
```
This above command will bring you back to the **postgres** Linux command prompt.
```console
postgres@ubuntu-dev:~$
```
To return to your regular system user, you execute the `exit` command like this:

```console
postgres@ubuntu-dev:~$ exit
```
### Load the sample database
To load the sample database into the PostgreSQL database server, you follow these steps:

**First**, switch over the postgres account using the following command:
```console
$ sudo -i -u postgres
```
It’ll prompt you for the password of the current user.Remeber it's your ubuntu user account password as you are using terminal as a superuser , **sudo** . You need to type the password of the current user and press the `Enter` keyboard.

**Second**, download the sample database using the `curl` tool:
```console
$ curl -O https://sp.postgresqltutorial.com/wp-content/uploads/2019/05/dvdrental.zip
```
**Third**, unzip the dvdrental.zip file to get the dvdrental.tar file:
```console
$ unzip dvdrental.zip
```
The output will show like this :
```console
Archive:  dvdrental.zip
inflating: dvdrental.tar
```
**Fourth**, access the PostgreSQL using the `psql` tool:
```console
$ psql
```
Fifth, create the `dvdrental` database using the `CREATE DATABASE` statement:
```console
postgres=# create database dvdrental;
```
**DON'T FORGET THE SEMICOLON**
The output will show something like this :
```console
CREATE DATABASE
```
**Seventh**, use the [`pg_restore`  tool to restore](https://www.postgresqltutorial.com/postgresql-restore-database/) the `dvdrental` database:
```console
$ pg_restore --dbname=dvdrental --verbose dvdrental.tar
```
**Eighth**, access PostgreSQL database server again using `psql`:
```console
$ psql
```
**Ninth**, switch to the `dvdental` database:
```console
postgres=# \c dvdrental
```
Now, you’re connected to the `dvdrental` database:
```console
dvdrental=#
```
**Finally**, enter the following command to get the number of films in the `film` table:
```console
dvdrental=# select count(*) from film;
```
**Don't Forget the semicolon**
Here is the output:
```console
count 
------- 
1000
(1 row)
```
So this is how you can create and connect to database

## pgadmin 4

There's a tool available for managing postgresql, called **pgadmin** , by which anyone can create and load database  and run any query command easily. It may be run either as a web or desktop application. Now i will show how to install pgadmin 4 on your desktop.

The good news is in windows distribution pgadmin 4 comes with the installer, i mean when you installed postgre sql for windows , the installer took care of everything for you.

But in Linux Distribution you have to install it externally , or what i'm trying to say is , you have to install it using terminal.
Here's is few steps to install pgadmin 4:
### Setup the repository
- Install the public key for the repository (if not done previously):
```console
curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add
```
- Create the repository configuration file:
```console
sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
```
### Install pgAdmin
- Install for both desktop and web modes:
```console
sudo apt install pgadmin4
```
- Install for desktop mode only:
```console
sudo apt install pgadmin4-desktop
```
- Install for web mode only:
```console
sudo apt install pgadmin4-web
```
- Configure the webserver, if you installed
-  pgadmin4-web:
```console
sudo /usr/pgadmin4/bin/setup-web.sh
```
Now if you search in your desktop writing `pgadmin4`, you should find it. After clicking a window should open in your web browser.
![Image](https://linuxhint.com/wp-content/uploads/2018/01/pg-7.2.png)