# **Implement a Client Server Architecture using MySQL Database Management System (DBMS).**

The client server architecture is an architecture of a computer network where two or more computers(remote & host) are connected to one another over a network and can communicate with one another by sending and receiveing requests. 

In a client/server architecture, the server acts as the producer and the client acts as a consumer. The server houses and provides high-end, computing-intensive services to the client on demand. These services can include application access, storage, file sharing, printer access and/or direct access to the server’s raw computing power.

This Project focuses on building out a server client architecture using MySQL.

# **Create Virtual Servers on AWS Using the EC2 Service**

- Create two servers on your AWS console and configure one to act as a client and the other as a server

```
Server A - MySQL CLient
Server B- MySQL Server
```
- On Server A install the MySQL client package using the `apt` command

```
serverA@ipaddress:~$ sudo apt install mysql-client
```

- On Server B install the MySQL server package using the `apt` command

```
serverA@ipaddress:~$ sudo apt install mysql-server
```

# **Configure Inbound Connections & Traffic Source**

- Set the Inbound rules on your MySQL Server to allow cnnections from port 3306 as this is default port MySQL server listens from. Also, set the source to allow connections only from the private ipaddress of the MySQL client.

![4](https://user-images.githubusercontent.com/47898882/126144528-1161bd0d-4fbd-4936-b5d6-97db29b2cd23.JPG)


- Go into the `/etc/mysql/mysql.conf.d/mysqld.cnf` file and configure the bind address from 127.0.0.1 to 0.0.0.0. This allows for the server to be accessed remotely

![3](https://user-images.githubusercontent.com/47898882/126144609-b8759a3e-6685-4226-abfb-87a05adfec34.JPG)

# **Create Database & User on MySQL Server**
- Use the `mysql_secure_installation` command to make MySQL more secure and remove all the defaults. There'll be a prompt for creation of password, create the password and follow the other prompts till the end. You can ignore these prompts by pressing the *ENTER* key

```
serverA@ipaddress:~$ sudo mysql_secure_installation
```
- Go into the SQL console on your terminal using `sudo mysql`.

- Create a Database on MySQL Server

```
mysql> CREATE DATABASE `remote_database`;
```
- Create a User and grant him full privileges to the database, then exit the sql shell.

```
mysql> CREATE USER 'remote_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';

mysql> mysql> GRANT ALL ON remote_database.* TO 'remote_user'@'%';

mysql> exit
```

- Go to the MySQL client terminal and connect remotely to the MySQL server using the command below:

```
serverB@ipaddress:~$ sudo mysql -u remote_user -h "server-privateip-address" -p
```

- You should be connected remotely as shown below.

![1](https://user-images.githubusercontent.com/47898882/126146986-5804e78d-b29b-4781-8fd2-641ed36492b1.JPG)

- To test that it works, use `SHOW DATABASES;` to check if the database(remote_database) you created and assigned full privileges to that user exists. 

![5](https://user-images.githubusercontent.com/47898882/126147970-9cd82816-e4a8-4ed5-8d5c-811b44256b36.JPG)


## *This is how to implement a Client-Server Arcitecture using MySQL.*


