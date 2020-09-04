# Industrial Dashboard for the Food Industry
This workshop will guide you through building a dashboard that updates in real time. This solution has several applications in industrial settings, including monitoring production equipment for operational efficiency or maintenance. In this example, a dashboard will be built for a company in the food industry. 

Data will come from virtual devices created using IoT Device Simulator. This data will be ingested into IoT Sitewise, where it will be viewed in Sitewise Monitor. An alarm that activates on sensor readings will also be built using IoT Core and Simple Notification Service.

![Screenshot of dashboard](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/1intro.png)

## Architecture

![Architecture diagram](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/2intro.png)

## Lab 1 - Setting up IoT Device Simulator

This lab will set up the IoT Device Simulator solution, walking through how to set up virtual devices to send mock data.

## Lab 2 - Connecting to IoT Sitewise

The data generated in the previous lab will be ingested into the IoT Sitewise service, through the use of MQTT messages and IoT Core rules.

## Lab 3 - Creating a dashboard

In this lab, a dashboard will be built to showcase the updating data in real time. It will support user management and displaying different views. All these features are built within IoT Sitewise.

## Lab 4 - Creating an alarm

Lastly, an alarm will be added to this solution through IoT Core and SNS. MQTT messages will be sent back to IoT Core where a rule will send appropriate data points to SNS to notify users when sensors detect specified values.


