# Lab 4 - Creating an alarm

In this lab, we will create an alert to showcase the ability to pass on data from IoT Sitewise to other AWS services. It will alert users when a refrigerator door is open.

## Step 1 - Create an SNS Topic

Open the AWS console and navigate to Simple Notification Service. On the left sidebar select "Topics" and choose "Create topic" on the right. Create a topic for our refrigerator door notification.

![create sns topic](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab4/1labfour.png)
This topic will send notifications to all subscribed users when an alert is received. To subscribe to the topic, click on SitewiseFridgeDoorAlarm on the Topics page. Under the subscriptions tab, select "Create subscription" and select a protocol from the drop-down. SNS supports many different notifications, including SMS and email. Fill in the required information and select "Create subscription" at the bottom.

![subscription to topic](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab4/2labfour.png)
Now the SNS topic is configured to send notifications to your desired account.

## Step 2 - Enable notifications in Sitewise asset properties

Next we will configure IoT Sitewise to send data into a new topic accessible to IoT Core. Open the AWS console and select IoT Sitewise. Navigate back to the Assets page. To send door data back to IoT Core, edit each refrigerator asset and enable notification for the door open property.

![sitewise notifications](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab4/3labfour.png)
IoT Sitewise will now send the door open data to the topic listed under the property. We will use this topic in the next step when we create a rule in IoT Core.

## Step 3 - Create an IoT Core rule to send data to SNS

Next we will walk through creating a rule to check the data sent from Sitewise and send an alert to SNS. Open the AWS console and open the IoT Core service. Navigate back to the Rules page under Act from the left sidebar. Click the Create button on the top right to make a new rule. Name the rule "SitewiseOpenDoor" and use this SQL code as the query rule:
```
SELECT get(payload.values, 0).value.booleanValue AS doorOpen 
FROM '$aws/sitewise/asset-models/f24dc317-87c8-4064-a6ea-d74b1b0787ce/assets/+/properties/6eed2ac1-01d5-4a49-887b-0ac3793b7684'
WHERE (get(payload.values, 0).value.booleanValue = true) 
```
In the FROM clause, you will need to replace the string with the topic from Step 2. You can replace the string after assets with a "+" like in the example above to make the rule work for all fridges with a dooropen property.

This SQL query checks the dooropen value and sends the data to the action when a true is detected, meaning a notification will be sent when the refrigerator door is open.

For the action category, select add action and choose "Send a message as an SNS push notification". For the SNS target, choose the topic we made in Step 1. Choose RAW for the message format and choose Create Role for the access role. 

![rule action for SNS](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab4/4labfour.png)
Finish the action and create the rule. The action routes the data to SNS and triggers a notification that is sent to topic subscribers. The notification system for refrigerator doors is now complete. 
