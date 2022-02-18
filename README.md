# Device communications Guide
Here you will find some tutorials to conect your devices by LoraWan - The Things Network and store your data in InfluxDB data bases using Node-RED and visualize it by Grafana. Follow the next steps. 


## 1. Install Influxdb
The InfluxDB 2.1 time series platform is purpose-built to collect, store, process and visualize metrics and events. The influx CLI lets you manage InfluxDB from your command line.
You need to install both the influx database and the client (CLI) to create and manage them.

You can download both of them form here: https://docs.influxdata.com/influxdb/v2.1/install/  

Once you download influxdb v2.1 (latest version so far, but check if there is a new one) move and extract files to C: "Programs Files" and make de same with CLI. The initial setup process for InfluxDB walks through creating a default organization, user, bucket, and Operator API token. Open ```cmd``` and go find the Influx folder on your Program Files. It is recomended to rename the main folder as "InfluxData" and store influxdb folder and CLI folder into it. Rename the influxdb installation folder as "influxdb" and CLI installation folder as "influxcli".  

Run the following command to run influxdb:
```
cd "\Program Files\InfluxData\influxdb\influxdb.exe"
```

Go on your browser and paste ```localhost:8086``` on the adress bar. Here you can set up your initial user (Username, Password, Organization Name, Bucket Name). Click Continue and influxdb will be initialized with a primary user, organization, and bucket. You are ready to write or collect data.

## 2. Install Node-RED
It is necessary to install ```Node.js```  to install Node-RED. You can follow the steps from this link: https://nodered.org/docs/getting-started/windows

## 3. Get MQTT API Keys from TheThingNetwork Applications
Go on TheThingsNetwork and open your device application. You will find ```MQTT``` on "Integrations" where the MQTT credentials are stored. The Application Server exposes an MQTT server to work with streaming events. In order to use the MQTT server you need to create a new API key, which will function as connection password. You can also use an existing API key, as long as it has the necessary rights granted. 

<center><img width="422" alt="MQTT_ApiKeys" src="https://user-images.githubusercontent.com/88738496/154685019-9d16ec05-b75d-4353-904f-59bc1b930464.PNG">

## 4. Run Node-RED and install necessary modules
Open another terminal and write the following command: ```node-red```. Node-RED will start running now. If you are using a browser on the same computer that is running Node-RED, you can access it with the url: http://localhost:1880. The interface should be something like this:

<img width="800" alt="Node-RED" src="https://user-images.githubusercontent.com/88738496/154686497-d070ddd1-36c6-48f2-8f12-29dd30b406fe.PNG">

For connecting influxdb with Node-RED it will be necessary to install ```node-red-contrib-influxdb``` command. Press the uppper-right button on Node-RED browser and go on "Manage Palettes". Here you can install it:
  
  <img width="280" alt="Node-red-installationpluggins" src="https://user-images.githubusercontent.com/88738496/154687080-c6f4573b-57c3-42ff-99be-9ffc9791d820.PNG">

  https://nodered.org/docs/tutorials/

## 5. Connect The thins network with Node-RED by MQTT:
  
On Node-RED  -  network, pull a ```mqtt in``` node into your flow. It will connect to a MQTT broker and publishes messages. Double click on it:
Click on "Use TLS" and press pencil button. 
  
<img width="324" alt="mqtt-nodered" src="https://user-images.githubusercontent.com/88738496/154688538-83eb1d97-3678-4bd7-89bb-52438d73d980.PNG">
  
Now it's time to configure your API user and Key:
  1. Copy your Public TLS address from TheThingsNetwork on server (be carefull, you will need to separate the port into a new box)
  2. Go to "Security"
  3. Copy yur username and password from TheThinsNetwork
  4. Click Update
  
On the Upper-Right side of the page, click on "Deploy". Your mqtt node should be connected now.
  
## 6. Create an Influxdb field on Node-RED
On Node-RED  -  storage, pull an ```influxdb out``` node into your flow. Connect it to your ```mqqt in```.
Define here your influxdb credentials created before:
  1. Server: URL(http://localhost:8086) and your Token
  2. Organisation name and Bucket
  
  
