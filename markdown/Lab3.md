# Lab 3 - Creating a dashboard

In this lab, you will build a dashboard in IoT Sitewise to view the data from IoT Device Simulator in real time.

## Step 1 - Create a new portal

Log into the AWS console and open the IoT Sitewise service. Click on the left sidebar and select Portals.

![select portals](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab3/1labthree.png)
Choose "Create portals" in the top right. Follow the steps in the configuration wizard. Fill in a name and email for your portal. For Permissions, select the "create and use a new service role" option. For administrators, add your own AWS account as an administrator. More administrators and users can be added now or at a later time, if desired.

Now that your portal has been created, it can be access by clicking on its URL. This is the link that will be used by users and administrators to access assets and Sitewise Monitor dashboard.

![links to portal](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab3/2labthree.png)
## Step 2 - Create your projects

Once in the portal, click the Projects link in the left sidebar. Select the Create project option. Our first project is going to be called "Tracy Refrigeration Center" and will have access to the three refrigerators cluster we built.

Once created, a project can be associated with one particular asset. Select add an asset. Select your refrigerator cluster asset and click on "Add asset to project" at the top. Select existing project and choose the Tracy Refrigeration Center. Now Tracy Refrigeration Center has access to the refrigeration cluster and the three fridges that belong to it.

![project main page](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab3/3labthree.png)
More projects can be created to give differing levels of access. For example, create one more project called "Administrator" and associate it with the production farm asset we built in Lab 2. This project will have access the whole production farm, allowing you to view all devices in both factories. 

Additionally on the project page, administrators and users can be given access. Administrators have edit access in the project, while users can only view. This can be used to give individuals access to different views (e.g. refrigerator engineers only having access to the Tracy Refrigeration Center).

![user management](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab3/4labthree.png)
## Step 3 - Build a dashboard

On the project page, we can now create a dashboard. Select "Create dashboard".

![build dashboard](https://github.com/casanabria2/iotsitewise-workshop/raw/master/WorkshopPics/lab3/5labthree.png)
Here you can:

 1. Edit the title of the dashboard
 2. Select different assets the project has access to
 3. Drag and drop measurements and metrics belonging to a selected asset

Use these tools to customize your dashboard. When finished, click "Save dashboard" at the top right. Multiple dashboards can be created in each project, showing different groups of devices or different views of the data. Only users with access to a particular project will be able to access particular dashboards.

