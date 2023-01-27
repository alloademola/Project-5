# Project-5
On this project we, are going to, be dealing with Client/Server Architecture Using A MySQL Relational Database Management System

To IMPLEMENT A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS).
The  very first TASK to follow is 

To Implement a Client Server Architecture using MySQL Database Management System (DBMS).
To demonstrate a basic client-server using MySQL Relational Database Management System (RDBMS), follow the below instructions

firstly you need to configure two server here on your EC2 server, namely,  
mysql server and mysql client.
so once done, you will connect your mysql server and run the below command

sudo apt update -y

<img width="1440" alt="Screenshot 2023-01-25 at 23 49 48" src="https://user-images.githubusercontent.com/118350020/214709618-00efe8e0-507f-4746-902d-081d3742e859.png">
 so after this, we are going to run the below commad again, to install our mysql server
 
 sudo apt install mysql-server -y 
 <img width="1440" alt="Screenshot 2023-01-26 at 00 02 00" src="https://user-images.githubusercontent.com/118350020/214711549-aa639231-f425-4126-8bb7-01cb1f52d74c.png">
the next to do now is to enable the service, so we are going to use below commad

sudo systemctl enable mysql
<img width="1440" alt="Screenshot 2023-01-26 at 00 05 39" src="https://user-images.githubusercontent.com/118350020/214712035-ce70370a-bc74-48f7-bc33-a9705159aec8.png">

The next thing to do now is to install MySQL Client software On mysql client Linux Server 
we are going to connect our server for mysql client on the EC2
after connecting , we. need to run this command below
sudo apt update
<img width="1440" alt="Screenshot 2023-01-26 at 00 25 54" src="https://user-images.githubusercontent.com/118350020/214716031-116031b8-e042-44dd-b002-d9c26fdb26ae.png">

so the next step is run the next command below
sudo apt install mysql-client -y
<img width="1440" alt="Screenshot 2023-01-26 at 00 30 42" src="https://user-images.githubusercontent.com/118350020/214716798-52776871-1f54-42e4-b61e-cf6a9fff4ef3.png">

Note: By default, both of our EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses. Use mysql server's local IP address to connect from mysql client. MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups. For extra security, do not allow all IP addresses to reach your ‘mysql server’ – allow access only to the specific local IP address of your ‘mysql client’.

So we need to configure MySQL server to allow connections from remote hosts.
but before we  do this, if you recalled,  we just installed `mysql server and mysql client server respectively,
So we dont have the datebase, we dont have the user,  we dont have the table,  we dont have anything
we just have the services. running on the server.
So we need the database on the mysql server and we also need the user.
This are important things we needed to configured, in other for us to have access to that quality higher to removed access.
So thats where the user of basic commands of mysql comes in
So from our mysql server, we are going to run this command below to run the security script

sudo mysql_secure_installion

<img width="1440" alt="Screenshot 2023-01-27 at 01 41 10" src="https://user-images.githubusercontent.com/118350020/214983094-3fe2c5f6-0020-4a2f-8034-3c20a0c0d5b8.png">
So we are going to run the below command, So that we can create the user
sudo mysql -p 

<img width="1440" alt="Screenshot 2023-01-27 at 02 04 12" src="https://user-images.githubusercontent.com/118350020/214984355-091efed9-198f-4e8a-844c-d623f99e8340.png">

so we are going to enter the below command to create the remote user
CREATE USER 'remote_user'@'%' IDENTIFIED WITH mysql_native_password BY 'Demo';

<img width="1440" alt="Screenshot 2023-01-27 at 02 08 15" src="https://user-images.githubusercontent.com/118350020/214986177-829693bf-cf2c-48c5-ac45-11354d4d9fc6.png">

So the next thing to do is to create the database, with the below command
CREATE DATABASE test_db;

<img width="1440" alt="Screenshot 2023-01-27 at 02 17 19" src="https://user-images.githubusercontent.com/118350020/214987055-c3f0b78b-56e2-4064-941a-a72ce520f31a.png">

so next step is to grant previleges , using the below command
GRANT ALL ON test_db.* TO 'remote_user'@'%' WITH GRANT OPTION;

<img width="1440" alt="Screenshot 2023-01-27 at 02 23 16" src="https://user-images.githubusercontent.com/118350020/214988248-46b4401b-d98c-492f-96c6-fe1fe90315af.png">

So we have granted all privileges so next is the Flush privileges, So we are going to use the below command
FLUSH PRIVILEGES;
<img width="1440" alt="Screenshot 2023-01-27 at 02 28 18" src="https://user-images.githubusercontent.com/118350020/214989407-4ca2843b-8a0c-4a9f-ac99-7fb382a8c9c3.png">

So after this, we can exit using the command below.
exit;

<img width="1440" alt="Screenshot 2023-01-27 at 02 30 14" src="https://user-images.githubusercontent.com/118350020/214989959-8c904cfc-c6f8-464c-9a8c-a8fc6e02fae9.png">

So our User is created also our Database as being created as well


so now , we need to configure MySQL server to allow connections from remote hosts. we are using the below command
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
Replace ‘127.0.0.1’ to ‘0.0.0.0’ like this:
<img width="1440" alt="Screenshot 2023-01-26 at 01 05 15" src="https://user-images.githubusercontent.com/118350020/214721823-2e8f2594-94c4-425b-b7b3-68a7617bac0a.png">

so we need to restart our server, we are going to use the below command to get that done

sudo systemctl restart mysql 

so From mysql client Linux Server,connect remotely to mysql server Database Engine without using SSH. 
You must use the mysql utility to perform this action.

so from our mysql client , we are going to run this command below
sudo mysql -u remote_user -h 172.31.20.224 -p
<img width="1440" alt="Screenshot 2023-01-27 at 02 43 29" src="https://user-images.githubusercontent.com/118350020/214992129-83d14522-9f21-4531-bedc-87c667e64bc2.png">

So the password asked, you need to input the password set earlier on into it.
<img width="1440" alt="Screenshot 2023-01-27 at 02 45 53" src="https://user-images.githubusercontent.com/118350020/214992299-153071d8-45fe-43db-ad82-f58323b3c79b.png">
<img width="1440" alt="Screenshot 2023-01-27 at 02 47 16" src="https://user-images.githubusercontent.com/118350020/214992493-63e1e906-2b6f-4448-ba32-72733a3b391e.png">


as you can see, they are both connected from out client instance
So now let us Check that we have successfully connected to a remote MySQL server and can perform SQL queries: on our client server
we are going to use the command below
Show databases;

If you see an output similar to the below image, then you have successfully completed this project – you have deloyed a fully functional MySQL Client-Server set up.
Well Done! You are getting there gradually. You can further play around with this set up and practice in creating/dropping databases & tables and inserting/selecting records to and from them.

<img width="1440" alt="Screenshot 2023-01-27 at 02 51 38" src="https://user-images.githubusercontent.com/118350020/214993686-2db16efa-d929-4e8d-9e12-e34120a3b34e.png">

Congratulations!
DONE.
