# Lab 2 - Connecting to IoT Sitewise

In this lab, you will ingest the data sent from devices created in IoT Device Simulator into IoT Sitewise, where it can be viewed using Sitewise Monitor.

## Step 1 - Create a model

Log into the AWS console and open the IoT Sitewise service. Click on the left sidebar and select the Models link.

![models on sitewise](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/1labtwo.png)
Here we will build models, which serves as a virtual template representing our sensors and machines. The data streams we produced in Lab 1 will be associated with measurement definitions defined in models. Models are also used to create a hierarchy among the different devices. For example, this can be used to show the relationship between a factory and its production lines.

Click the Create model button on the left column to create a model for the refrigerator. Use this information for the model:

![model attributes](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/2labtwo.png)![attributes2](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/3labtwo.png)

 - Attributes are static fields that never change (information about the device such as serial number)
 - Measurements are timestamped data streams, used to take in data from sensors
 - Transforms can convert measurements to another form (in this example, converting Fahrenheit to Celsius)
 - Metrics are functions that process data over time

Click save at the bottom to finish the refrigerator model. Now we will repeat this process two more times to create models for the packing line and conveyor belt. 

![refrigerator model](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/4labtwo.png)
![model attributes2](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/5labtwo.png)
Similar metrics such as average, min, or max can also be defined for the speed of these devices.

## Step 2 - Create the model hierarchy

Now we will create parent models to represent the hierarchy among these devices. At the highest level we will have groups of factories, called "Production Farms", which will be made up of "Factories". Each Factory will contain "Production Lines" and/or "Refrigerator Clusters". Production Lines will be made up of "Packing Lines" and "Conveyor Belts" we made in Step 1, while Refrigerator Clusters will be made up of "Refrigerators" also created in Step 1.

Lets start by making a Refrigerator Cluster. Create a new model as before and name it Refrigerator Cluster. Fill in the hierarchy definition:

![hierarchy](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/6labtwo.png)
This declares that Refrigerators are children of the parent model Refrigerator Cluster.

Repeat these steps to create parent models for Production Lines, Factories, and Production Farms.

## Step 3 - Create an asset from a model

From these models built in the last step, we will now create assets. Assets are a particular instance of a model, similar to how widgets are a particular instance of a device type.
 
To create an asset, select Assets on the left sidebar. Then click on Create asset. Select Refrigerator Model to create a refrigerator asset and give it a unique name (for example, Fridge1).

![asset creation](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/7labtwo.png)
Create two more refrigerator assets, two packing line assets, two conveyor belt assets. Then create one refrigerator cluster, two production lines, two factories, and one production farm from our parent models.

For each of the parent assets, click edit on the top right to modify its properties and add in their relationships to their children. For example, for the refrigerator cluster, add the three fridges to the Assets associated with this asset category.

![asset association](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/8labtwo.png)
After all the parent and children assets have been associated, this is how the device hierarchy should look with example names for each asset.

![final hierarchy](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/9labtwo.png)
## Step 4 - Create an IoT Core rule to ingest data to Sitewise

Now that all the assets are set up, the data from IoT Device Simulator can be ingested into IoT Sitewise to be associated with these assets. In the AWS console, open the IoT Core service. On the left sidebar click the Act drop-down and select Rules.

Select Create in the top right. Name the rule SitewiseDeviceRule and put `SELECT * FROM '/octank/data/'` in the Rule query statement. This SQL statement will take all the messages sent to `/octank/data/` and send it to the following action we are about to configure.

![rules](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/10labtwo.png)
Next, under Set one or more actions click Add action. In this new list of options select "Send message data to asset properties in AWS IoT SiteWise". Choose the "By property alias" option. Add the following three entries:

![temperature](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/11labtwo.png)![door open](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/12labtwo.png)![speed](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/13labtwo.png)
The property alias is the address of where the data is being sent to in IoT Sitewise. Time in seconds and offset in nanos is used to collect the timestamps of the data. Value is the actual data being sent to the asset property.

Finally under Role, choose Create Role to create an IAM role for this rule action. This role allows AWS IoT to push data to properties in your device fleet asset and its asset hierarchy.

Click Add action to finish the rule.

## Step 5 - Configure assets to receive data

Back in the IoT Sitewise console, navigate back to the assets page. For each asset, choose the edit option in the top right. From the previous lab, add their corresponding unique deviceid from IoT Device Simulator to the asset's Serial Number attribute. For the measurement attribute, fill in the box with the the property alias from the IoT Core rule, replacing `${deviceid}` with that same deviceid. For example, the conveyor belt device below has a deviceid of `DT3y9Rbmk3`.

![serial numbers](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab2/14labtwo.png)
This tells IoT Sitewise which data streams correspond to which attributes in each of the assets. Now IoT Sitewise has access to the data generated by IoT Device Simulator.
