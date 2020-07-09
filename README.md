# pymongoDB
pymongoDB

http://kb.objectrocket.com/mongo-db/using-flask-on-a-raspberry-pi-with-mongodb-part-1-1136#configure+the+raspbian+mongodb+server

$ sudo apt update && sudo apt install python3-pip

$ pip3 install pymongo

$ pip3 install flask

$ sudo apt-get install nginx

$ sudo /etc/init.d/nginx start
(http:\\localhost)

$ sudo apt-get install mongodb

$ sudo apt-get install mongodb-server

Install MongoDB 4.2 on Raspbian Bionic Beaver
First, you’ll need to get the PGP key for the MongoDB v4.2 repository:


$ wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
Next, use the echo command to append the repository link and list the file to your Raspbian’s /etc/apt/sources.list.d directory:


$ echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list
Finally, you’ll need to update and install MongoDB from the newly-added Debian repository:

$ sudo apt-get update && sudo apt-get install mongodb-org
If you don’t want to build MongoDB from source or install an older version, another option would be to install Docker and run a newer version of MongoDB in a containerized environment on the Raspberry Pi.

---------------------------------------------------

Start MongoDB
At this point, you should be able to start the MongoDB service; however, there’s still some configuration that needs to be done. Use the following systemctl command to start the MongoDB service:

$ sudo systemctl start mongodb
You can use the enable option to enable the service so that it starts whenever you boot the Raspberry Pi:

$ sudo systemctl enable mongodb
Finally, use the service command to initialize and set up your MongoDB service by authenticating a user:

$ service mongodb start
After you complete the configuration, execute the mongod command to make sure that the service is running. If you get an error saying: “ERROR: dbpath (/data/db/) does not exist“, you’ll need to set up the MongoDB database path first.

The command shown below can be used to create the /date/db directory and subdirectory. Then, you can grant ownership of the directory to the pi user with the chown command:

$ sudo mkdir -p /data/db && sudo chown pi /data/db

-------------------

Start MongoDB
At this point, you should be able to start the MongoDB service; however, there’s still some configuration that needs to be done. Use the following systemctl command to start the MongoDB service:

$ sudo systemctl start mongodb
You can use the enable option to enable the service so that it starts whenever you boot the Raspberry Pi:

$ sudo systemctl enable mongodb
Finally, use the service command to initialize and set up your MongoDB service by authenticating a user:

$ service mongodb start
After you complete the configuration, execute the mongod command to make sure that the service is running. If you get an error saying: “ERROR: dbpath (/data/db/) does not exist“, you’ll need to set up the MongoDB database path first.

The command shown below can be used to create the /date/db directory and subdirectory. Then, you can grant ownership of the directory to the pi user with the chown command:

$ sudo mkdir -p /data/db && sudo chown pi /data/db

$ sudo nano /etc/mongodb.conf
from
bind_ip = 127.0.0.1 
to
bind_ip = 0.0.0.0.

$ sudo service mongodb restart
$ curl localhost:27017
It looks like you are trying to access MongoDB over HTTP on the native driver port.


------------------------------


// $ pip3 install pymongo==3.4.0

$ nano pymongoex.py

    import pymongo

    myclient = pymongo.MongoClient("mongodb://localhost:27017/")
    mydb = myclient["mydatabase"]
    mycol = mydb["customers"]

    mylist = [
      { "name": "Amy", "address": "Apple st 652"},
      { "name": "Hannah", "address": "Mountain 21"},
      { "name": "Michael", "address": "Valley 345"},
      { "name": "Sandy", "address": "Ocean blvd 2"},
      { "name": "Betty", "address": "Green Grass 1"},
      { "name": "Richard", "address": "Sky st 331"},
      { "name": "Susan", "address": "One way 98"},
      { "name": "Vicky", "address": "Yellow Garden 2"},
      { "name": "Ben", "address": "Park Lane 38"},
      { "name": "William", "address": "Central st 954"},
      { "name": "Chuck", "address": "Main Road 989"},
      { "name": "Viola", "address": "Sideway 1633"}
    ]

    x = mycol.insert_many(mylist)

    #print list of the _id values of the inserted documents:
    print(x.inserted_ids)


$ python3 pymongoex.py



