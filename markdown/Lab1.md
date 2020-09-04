# Lab 1 - Setting up IoT Device Simulator

In this lab, you will setup IoT Device Simulator to send sample data to IoT Sitewise. Device Simulator will be accessible through a web portal once created, where virtual devices can then be built.

## Step 1 - Deploying the Device Simulator solution

To test IoT services and device integration, AWS provides a CloudFormation template for IoT Device Simulator. See the following page to set up the reference implementation for use with this lab: https://aws.amazon.com/solutions/implementations/iot-device-simulator/

## Step 2 - Creating your first device type

After setting it up, log into the Device Simulator console and click on "Create a Device Type" under your current number of devices.

![Create a Device Type](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab1/1labone.png)

For our first device type, we will make a refrigerator type. This will serve as the base type that all of our individual refrigerator devices will be based on. Fill in the fields with this information:

 - Device Type Name: Refrigerator
 - Visibility: PRIVATE (Default)
 - Data Topic: /octank/data/
 - Data Transmission Duration: 3600000
 - Data Transmission Interval: 2000 (Default)

These options will configure your refrigerator devices to send MQTT messages to the `/octank/data/` topic. Data will be transmitted for 1 hour, with updated values every 2 seconds.

Next, we need to configure what data is sent by the device. Under Message Payload, add an attribute. 

For the first attribute, name it "deviceid" and keep the DEVICE ID type in the drop-down. This field will hold a unique string that will identify individual refrigerators. 

Create another attribute with the name "temperature" and type FLOAT. Set the integer minimum value to 38 and the integer maximum value to 41. This attribute will specify the refrigerator's current temperature and is set to be around 38 to 41 degrees Fahrenheit. The simulated temperature will be between these values. Leave all other fields on their default values.

For the final attribute, name it "dooropen" and give it type BOOLEAN. Set the Default Value to "false". This attribute will report whether the refrigerator door has been left open. The Default Value specifies that the door should report that it is closed, rather than fluctuating between true and false randomly. Leave the other fields on their default values.

Your finished configuration should look like this:

![Finished configuration](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab1/2labone.png)
Click save at the bottom to complete your device type.

The refrigerator type is now complete. Now repeat this process to create two more types of devices, a conveyor belt and packing line.

Name each "Conveyorbelt" and "Packingline", respectively. Set all other fields in the Device Type Definition section to the same values as Refrigerator. All these devices will be sending data to the same topic for the same lengths of time.

For the message payload, both types will need the same "deviceid" attribute to uniquely identify an instance, as well as a "speed" attribute in float format to represent the device sensor. Set the minimum and maximum value to 12 and 15 respectively.

## Step 3 - Creating device instances

Now that the device types are finished, we can create multiple instances of these types to create a fleet of virtual devices. Click on Widgets on the left sidebar and choose "+ Add Widget".

![create widget](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab1/3labone.png)
A prompt will pop up asking for the type of device as well as how many instances. Create three refrigerators, two packing lines, and two conveyor belts.

![make widget prompt](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab1/4labone.png)
The widgets will automatically start upon creation. Press the stop button on the left of the widget to stop each of them for now. When you're ready to simulate data, start each widget to begin the mock data generation.

Note that each widget has a unique string underneath its name. We'll need these unique strings in the next lab.

*![unique deviceid](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab1/5labone.png)*
