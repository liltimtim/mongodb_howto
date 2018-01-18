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
