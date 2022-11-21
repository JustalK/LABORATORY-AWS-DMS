# LABORATORY-AWS-DMS

As I am working on my different aws certification. I am also testing how to use the different tool provided by **AWS**. This laboratory was created for testing how to migrate a database from a server to a documentDB using **DMS**, database migration service. I have documented with screen at each step how to do this. This is quite a long process but the result is perfect without any faulty copy.

## Plan of the presentation

I explain with all the details how I build the project and my way of working.

- [Create a DocumentDB Cluster](#create-a-documentDB-cluster)
- [Modification on EC2](#modification-on-ec2)
- [Create a replicate instance](#create-a-replicate-instance)
- [Create endpoints](#create-endpoints)
- [Create Database Migration](#create-database-migration)
- [Test](#test)
- [System](#System)

#### Create a DocumentDB Cluster

Login on AWS and search for DocumentDB. Click on the button `Create Cluster`

![./documentation/1.png](./documentation/1.png)

![./documentation/2.png](./documentation/2.png)

![./documentation/3.png](./documentation/3.png)

#### Modification on EC2

When going on the cluster of your DocumentDB, you should see the following information:

![./documentation/4.png](./documentation/4.png)

Connect to your ec2 using SSH and use the first command of the previous screen to download the certficate.

![./documentation/5.png](./documentation/5.png)

If you are using UFW, open the port 27017 using the command:

```bash
sudo ufw enable 27017
```

![./documentation/10.png](./documentation/10.png)

In the security group, open the port 27017

![./documentation/11.png](./documentation/11.png)

Change the network of the mongodb in the mongod file.

```bash
sudo nano /etc/mongod.conf
```

![./documentation/12.png](./documentation/12.png)

Modify the network interface line with the ec2 url inside `bindIp`.

![./documentation/13.png](./documentation/13.png)

And finally, restart the mongo service.

![./documentation/14.png](./documentation/14.png)

#### Create a replicate instance

Search for DMS and click on the button `Create replicate instance`

![./documentation/6.png](./documentation/6.png)

![./documentation/7.png](./documentation/7.png)

![./documentation/8.png](./documentation/8.png)

#### Create endpoints

Create the source endpoint which represent the mongodb inside the ec2.

![./documentation/16.png](./documentation/16.png)

And test the endpoints.

![./documentation/17.png](./documentation/17.png)

Create the target endpoint which represent the cluster documentDB.

![./documentation/19.png](./documentation/19.png)

![./documentation/20.png](./documentation/20.png)

![./documentation/21.png](./documentation/21.png)

#### Create Database Migration

Go in the AWS DMS and click on the button `Create task`.

![./documentation/22.png](./documentation/22.png)

![./documentation/24.png](./documentation/24.png)

![./documentation/25.png](./documentation/25.png)

![./documentation/26.png](./documentation/26.png)

![./documentation/27.png](./documentation/27.png)

The migration should now start. It might take a while.

![./documentation/28.png](./documentation/28.png)

Once done, the status of the migration will change.

![./documentation/29.png](./documentation/29.png)

#### Test

Connect to the documentDB Cluster and check if the database contains all the data.

![./documentation/31.png](./documentation/31.png)

Alternatively, you can check the result of the migration in DMS in the tab `table statistics`.

![./documentation/32.png](./documentation/32.png)

## System

Ubuntu Version: Ubuntu 20.04.1 LTS
Node Version: v16.17.3

```bash
# Get the version of node
$ node -v

# Get the latest version of ubuntu
$ lsb_release -a
```