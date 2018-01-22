# Introduction

## Tutorial Overview
* Learn how to setup and run a local MongoDB instance using either `brew` or running mongodb directly from the downloaded application.  You can obtain the latest version of mongodb from the official website [here](https://mongodb.com). You may also clone this repo as well. 
* Learn how to setup `RoboMongo`


## Setting up and running MongoDB Localhost

First ensure that you have a copy of mongodb either installed via `brew`, cloning this repo, or downloading the latest copy from [mongodb](https://mongodb.com) official website.

The official setup documentation is located here: [Setup Mongodb](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)

### Setup with Brew

update brew sot hat you get the latest version of mongodb
```
brew update
```

install mongodb
```
brew install mongodb
```

> **Note**: when running mongodb from the terminal either from `brew` or manually running each program, it will by default, look for a database directly at `/data/db`.  The newest version of MacOS does not allow non-sudo users to write to the directory `/` or the root directory of your mac.  To get around this you need to pass in a database directory flag so that mongodb will search at the specified location and not error out. 

### Starting MongoDB
#### Step 1
Ensure that you have made a directory either in your `home` folder such as `/users/timdillman/db`.  

To create a database directory in your `home folder` on your mac, simply run 

```
cd ~ <hit return key>
mkdir {whatever name you want recommend lowercase with no spaces} <hit return key>
```
you should then see a document directory inside your `home folder` on your Mac where you can store all your mongodb databases. 

#### Step 2
Now that you have a place to store your database, simply run the command to start mongodb

#### starting mongo if installed by `brew`
```
mongod --dbpath ~/db
```

#### starting mongo if downloaded from `mongo website`
```
cd {download directory}/bin
./mongod --dbpath ~/db
```

if you have done everything correctly you should see an output similar too this 
> both `brew` and `downloaded` versions of mongo will output the same console verbosity.

> it is important that you do not kill the terminal directly by closing it.  You will want to shutdown mongo by hitting the `control-c` so that mongo can properly shutdown.  Failure to do so may corrupt your databases and you will have to delete them in order to fix the issue. 
```
2018-01-18T14:27:15.923-0500 I CONTROL  [initandlisten] MongoDB starting : pid=19964 port=27017 dbpath=/Users/timdillman/Documents/db 64-bit host=Tims-MBP.knology.net
2018-01-18T14:27:15.923-0500 I CONTROL  [initandlisten] db version v3.6.1
2018-01-18T14:27:15.923-0500 I CONTROL  [initandlisten] git version: 025d4f4fe61efd1fb6f0005be20cb45a004093d1
2018-01-18T14:27:15.923-0500 I CONTROL  [initandlisten] OpenSSL version: OpenSSL 1.0.2n  7 Dec 2017
...
output abbreviated
...
2018-01-18T14:27:16.575-0500 I FTDC     [initandlisten] Initializing full-time diagnostic data capture with directory '/Users/timdillman/Documents/db/diagnostic.data'
2018-01-18T14:27:16.576-0500 I NETWORK  [initandlisten] waiting for connections on port 27017
```
----

# Setting Up RoboMongo (Robo T3)
As of this documentation, the latest version of RoboMongo or Robo T3 can be found [here](https://robomongo.org)

There are two versions of RoboMongo
1. Free version [here](https://robomongo.org/download)
2. Paid version [here](https://studio3t.com/)

In order to complete this tutorial, we will be using the free version.  You can do pretty much anything you need with the free version.  

> This program is actually not required at all in order to query a mongo database however it provides a nice GUI on top of your running mongo databases and allows you to visually navigate `collections` and `documents`. It is expected that you understand how mongodb works when using this program.  Use caution, you **cannot undo** most operations performed using this tool. 

### Adding A Connection / Database
#### Step 1
Open robomongo.  You should be presented with this screen.
![Robomongo ConnectionOverview](https://github.com/liltimtim/mongodb_howto/blob/master/tutorial_resources/connection_overview.png?raw=true)

If you are not presented with this screen, click on the `connections` icon

![Connections Icon](https://github.com/liltimtim/mongodb_howto/blob/master/tutorial_resources/new_connection_icon.png?raw=true)

> this will open up the connection overview screen

Next click the `Create` button at the top left corner of the window. 

You should see this screen
![New Connect Setup](https://github.com/liltimtim/mongodb_howto/blob/master/tutorial_resources/connection_tab_settings.png?raw=true)

> The primary tabs we will be discussing are `connection` and `Authentication`

#### Step 2 - Entering Connection Information

Under the `Connection` tab there are 4 primary things of note. 
1. Type: You can select `Direct Connect` or `Replica Set`. 
> this tutorial only covers `Direct Connect`
2. Name: An arbitrary name you give the connection.  This is no way affects connecting to a database its just for your own convenience. 
3. address: this is the address at which to connect.  
> When entering an address **do not** include the URI portion of a mongodb address: `mongodb://`.  That **is not** an `address` that is a URI `scheme`.  Also, do no include the port number.  You must enter the port in the proper field. 
> To learn more about what a URI is, visit [Wiki](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier)
4. the port field.

##### Local Host Setup
For connecting to localhost, you can just leave all the default values that robomongo places into the fields and hit "Save".  This will save the connection in the list.  To connect to your saved localhost database:

* Ensure you are running mongodb

You should see this screen when you connect to your localhost box

![Localhost connection overview](https://github.com/liltimtim/mongodb_howto/blob/master/tutorial_resources/running_localhost_overview.png?raw=true)

#### Step 2.1 Heroku and MLab Connection Setup
For most projects, we will be using `heroku` and the `mlab` resource addon. 

Go to Heroku's [website](https://heroku.com)

In your own overview list of servers, ensure that you are on the correct team if you do not see a list / the server you are looking for. 

![Server List](https://github.com/liltimtim/mongodb_howto/blob/master/tutorial_resources/heroku_server_list.png?raw=true)

Select the server you wish to view from this list. 

> for this tutorial I'm going to select `caars-qa` server for no particular reason. 

You should see a screen similar too this
> Note that the tutorial was done in 2018, the interface may have changed since then. 

![Heroku Server Overview](https://github.com/liltimtim/mongodb_howto/blob/master/tutorial_resources/caars_heroku_overview.png?raw=true)

Select the `Settings` tab

Under the `Settings` tab you should see a screen similar to this

![Heroku Settings Screeen](https://github.com/liltimtim/mongodb_howto/blob/master/tutorial_resources/heroku_settings_tab.png?raw=true)

Tap the "Reveal Configs" button

![Reveal Configs](https://github.com/liltimtim/mongodb_howto/blob/master/tutorial_resources/herokur_rev_btn.png?raw=true)

You should now see all your configs

![All Configs](https://github.com/liltimtim/mongodb_howto/blob/master/tutorial_resources/heroku_config_not_hidden.png?raw=true)

> The config you are looking for is the `MONGODB_URI` setting.  

Copy the `MONGODB_URI` configuration setting. You should have something similar to this URI:

`mongodb://heroku_1df7hmsb:s9n0ub1qc6fb2833b7t7solevr@ds243657-a0.mlab.com:43657,ds243657-a1.mlab.com:43657/heroku_1df7hmsb?replicaSet=rs-ds243657`

The formatting of a mongodb URI is 

`[scheme]://[username]:[password]@[database_url]:[port]/[database_name],[replica_set_information]`

We can use this information to extract out the sections we will need which are `username`, `passpword`, `database_url`, `port`, and `database_name`

In our case the values are:

[username] : heroku_1df7hmsb

[password] : s9n0ub1qc6fb2833b7t7solevr

[database_url] : ds243657-a0.mlab.com

[database_name] : heroku_1df7hmsb

[port] : 43657

> Note that this is a `special case` because this database has a `replica set`.  This is like a mirror for your database.  anything you do with the primary database, it is also done on the replica set.  This is how mongodb ensures reliability for the database. The URI is still the same format however just with extra parameters.  Normally, a `sandbox` URI would not include a replica set and would look like this 

```
mongodb://heroku_1df7hmsb:s9n0ub1qc6fb2833b7t7solevr@ds243657-a0.mlab.com:43657/heroku_1df7hmsb
```

Now go back to robomongo and enter this information we have extracted from Heroku in order to connect too the database and view its data.  

Your Connection setting should look like this...

![Connection Setting](https://github.com/liltimtim/mongodb_howto/blob/master/tutorial_resources/caars_connection_setting.png?raw=true)

Your Authentication tab should appear like this...

![Connection Tab](https://github.com/liltimtim/mongodb_howto/blob/master/tutorial_resources/caars_auth_settings.png?raw=true)

> **Note** that usually `MLab` instances use the `username` as the `database` name.  This is **coincidental** and is not the **rule** its the **exception**.  You cannot rely on this always being true. 

> Ensure that "Perform Authentication" checkbox is selected otherwise youw ill not be able to enter information

> Ensure that the `Auth Mechanism` is set to `SCRAM-SHA-1` for authentication mech. 
------

# MongoDB Toolsets

## Introduction

Tutorial teaches about the following tools offerred by MongoDB.  You can use either the **brew** version of mongo or downloading it from the official MongoDB website.  Both software accepts the same input parameters for this tutorial. 

* mongodump
* mongorestore

> This tutorial was designed and uses V 3.6 of MongoDB to include its toolsets.  If any command fails or differs from this tutorial its probably because you have a newer version.  Always look at the documentation on the official website which, will always have the latest information. 

**Goals**
1. Demonstrate how to backup and restore a database. 
2. Demonstrate how to use these tools to transition a sandbox MLab instance into production instance by first dumping the sandbox database and restoring it into an MLab production instance. 

Directions covered:

1. MLab ->mongodump-> Localhost (snapshot)
2. Localhost (snapshot) ->mongorestore-> MLab

### mongodump

Used to completely output all the collections in a database.  This tools exports .bson and .json files that represent a mongo database.  Typically, it exports into a folder of your choosing. You may also use queries to dump specific portions of data from the database however this is a more advanced topic which wont be covered. 

> More information can be found at MongoDB [here v3.6](https://docs.mongodb.com/manual/reference/program/mongodump/)

### mongorestore

Used to restore a single database from the mongodump snapshot.  This tool allows to globally restore a database or select an individual collection to restore. You can also run queries to restore only a particular dataset but this is advanced usage and will not be covered in this tutorial. 

> More information can be found at MongoDB [here v3.6](https://docs.mongodb.com/manual/reference/program/mongorestore/)

## Using mongodump

### Step 1 - Ensure mongorestore is on your machine

in the terminal, type the following

```
mongorestore --version
```


You should see similar output to the following below
> If you do not see this output, it means that you do not have mongodb installed using brew.  This is fine, you can run the tool directly from the **bin** folder if you downloaded mongodb from its official repo.  
```
Timothys-iMac:mongodb_howto timothydillman$ mongorestore --version
mongorestore version: r3.6.2
git version: 2b10d8492e1185039be4d5f2242a5b11ea102303
Go version: go1.9.2
   os: darwin
   arch: amd64
   compiler: gc
OpenSSL version: OpenSSL 1.0.2n  7 Dec 2017
```

Let's get started by dumping a database from an MLab sandbox instance.  

We will be using d2113736.mlab.com instance for this tutorial (which may or may not exist anymore)


In your terminal type this command...
```
mongodump -h ds113736.mlab.com:13736 -u heroku_d4dg1ksj -p sjd25k9nnv5p8p2jm0m12ft2jv -d heroku_d4dg1ksj -o ~/Projects/db_dumps
```

**-h [host_name]**: This command tells mongodump 'where' the database is and what port to use in order to connect. 

**-u [username]**: This tells mongodump the username to use to connect to the database (very similar to setting up a RoboMongo connection).

**-p [password]**: This tells mongodump what the password is for the user you defined. 

**-d [database_name]**: This tells mongodump which database you want to dump

**-o [dump_directory]**: This tells mongodump 'where' on your machine to dump this database. 
> -o is a destructive command which --**will not**-- prompt you before overriding anything at the location you specify.  Tread with caution!

Inspecting the output contents will give you something similar to the following

```
Timothys-iMac:heroku_d4dg1ksj timothydillman$ ls -all
total 19488
drwxr-xr-x  34 timothydillman  staff     1088 Jan 22 06:25 .
drwxr-xr-x   3 timothydillman  staff       96 Jan 22 06:25 ..
-rw-r--r--   1 timothydillman  staff     2296 Jan 22 06:25 ChargeRequest.bson
...
Content Abbreviated
...
-rw-r--r--   1 timothydillman  staff        0 Jan 22 06:25 _Role.bson
-rw-r--r--   1 timothydillman  staff      209 Jan 22 06:25 _Role.metadata.json
-rw-r--r--   1 timothydillman  staff     3819 Jan 22 06:25 _SCHEMA.bson
-rw-r--r--   1 timothydillman  staff       95 Jan 22 06:25 _SCHEMA.metadata.json
-rw-r--r--   1 timothydillman  staff    16131 Jan 22 06:25 _Session.bson
-rw-r--r--   1 timothydillman  staff       96 Jan 22 06:25 _Session.metadata.json
```
