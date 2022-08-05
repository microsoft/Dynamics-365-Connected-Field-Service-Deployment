# Dynamics 365 Connected Field Service - Azure IoT Deployment Template

## Overview

Connected Field Service enables organizations to transform the way they provide service from a costly break-fix model to a proactive and predictive service model through the combination of IoT diagnostics, scheduling, asset maintenance, and inventory on the same platform.
Connected Field Service enables organizations to transform the way they provide service from a costly break-fix model to a proactive and predictive service model through the combination of IoT diagnostics, scheduling, asset maintenance, and inventory on the same platform.
There are three ways you can use to connect IoT-enabled devices into the Field Service solution:

- Connected Field Service for [Azure IoT Central](https://azure.microsoft.com/en-us/services/iot-central/)
- Connected Field Service for [Azure IoT Hub](https://azure.microsoft.com/en-us/services/iot-hub/)
- Connected Field Service for non-Azure IoT providers using the extensible IoT provider framework

This repo will help you set up and configure Connected Field Service with Azure IoT Hub. For more information on using other providers, please see our documentation page here: [Connected Field Service - Overview | Microsoft Docs](https://docs.microsoft.com/en-us/dynamics365/field-service/connected-field-service)

Connected Field Service for Azure IoT Hub is an add-on solution that brings Azure IoT platform-as-a-service (PaaS) offering into Dynamics 365 for Field Service. With this offering, you can use this template and below instructions to put all the Azure IoT services and Dynamics puzzles together. All Azure IoT services run in your own Azure cloud subscription.

This deployment package will help you:

- Deploy and configure an IoT Hub instance. Connected Field Services uses the IoT Hub to manage the state of registered devices and assets. In addition, the IoT Hub sends commands and notifications to connected devices—and tracks message delivery with acknowledgement receipts.
- Deploy a device simulation (optional). This is a test web app to emulate the device that is sending commands or receiving commands from the IoT Hub.
- Deploy Time Series Insight (optional). Time Series Insights can be included in your deployment for detailed device insights and analytics.
- Deploy PowerBI (optional). Microsoft Power BI for device analytics can be included in your deployment. Choosing this will deploy two additional resources, Azure Streaming Analytics and SQL Server database.

## Prerequisites

1. Your Dynamics 365 organization should have the latest version of the Connected Field Service solution.
2. You'll need an Azure subscription where you can deploy resources.
3. You must have the Owner level permissions on your Azure environment
4. You must have Dynamics 365 System Adminisistrator role on your CRM organization
5. You need to have Dynamics 365 Connected Field Service installed on your CRM organization
6. Before you beging with the deployment, please ensure that the IoT Hub quota for your Azure subscription is within limits. For more information see [IoT Hub Limits](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#iot-hub-limits)

## Deployment steps

By deploying this template, you confirm that you’ve read and agree to the [Terms of Service](https://github.com/microsoft/Dynamics-365-Connected-Field-Service-Deployment/blob/main/Terms_of_Service.md) and the [Microsoft Privacy Statement](https://privacy.microsoft.com/en-us/privacystatement)

[![Deploy To Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/users-vsaurab10-prerequisites/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmicrosoft%2FDynamics-365-Connected-Field-Service-Deployment%2Fmain%2FazureDeploy.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2Fmicrosoft%2FDynamics-365-Connected-Field-Service-Deployment%2Fmain%2FcustomUi.json)

**Note**: During deployment you'll be asked to provide your organization's unique name. You can find your organization's unique name by navigating to Advanced Settings on your Dynamics organization. Then navigate to Customizations > Developer Resources.

## Post deployment Steps

After deploying Azure resource from ARM template, follow the below steps to complete the deployment.

### Authorize API Connection between Dynamics 365 and Azure IoT

Please refer to the instructions [here](https://docs.microsoft.com/en-us/dynamics365/field-service/cfs-authorize-api-connection). This is required to begin using Connected Field Service with IoT Hub.

### Create new IoT Provider Instance

1. Login to your Dynamics 365 organization and open Connected Field Service application
2. From site map, go to Settings -> Providers and click New to create a new IoT Provider Instance
3. On the New IoT Provide Instance form, fill the below fields
   - For Name, enter the name of the Resource Group in Azure where you deployed IoT resources.
   - For IoT Provider, choose "IoT Hub Provider".
   - For Provider Instance Id, enter the name of the IoT Hub resource that was deployed to your Resource Group in Azure.
   - For URL, enter the URL of the overview for the Resource Group in the Azure portal (e.g. `https://portal.azure.com/[tenant_info]/subscriptions/[subscription_id]/resourceGroups/[resource_group_name]/overview`)
4. Click Save or Save & Close to create new IoT Provide Instance record

### Update the IoT Settings record

1. From the sitemap, click IoT Settings and then click on IoT Provider Settings tab
2. Set Default IoT Provide Instance to the IoT Provider Instance created previously
3. Click Save or Save & Close to save your changes

### Update the service endpoint

1. Using the Plug-in Registration Tool (available [here](https://docs.microsoft.com/dynamics365/customerengagement/on-premises/developer/download-tools-nuget?view=op-9-1)), login to the org where you're setting up Connected Field Service.
2. Once connected to the org, find the Service Endpoint called "IoT Message" and click on it.
3. Click on Update.
4. For namespace address, find the host name for the Service Bus Namespace deployed to your resource group. Enter this into the Plug-in Registration Tool prefixed by "sb://". It should look something like this - sb://myServiceBusNamespace.servicebus.windows.net
5. In the Service Bus Namespace resource, there will be a queue with a name ending in "-crm". Copy the full name and enter this as the Topic Name in the Plug-in Registration Tool.
6. In the Service Bus Namespace resource, navigate to Shared access policies > RootManageSharedAccessKey. Copy the primary key and paste it into the Plug-in Registration Tool for SAS Key.
7. Click Save.

Example:

![image](https://user-images.githubusercontent.com/25106863/182724363-f7488f6e-8509-4ba5-b766-ac473396b8c0.png)

### Upload devicerules.json

The Stream Analytics job deployed to your resource group will have a reference to a devicerules.json file. This file defines a rule that is useful for creating IoT Alerts when using the thermostat Simulator app. To make use of this, you will need to upload the devicerules.json file to the Azure storage. This file is found in this GitHub repo.

1. In the storage account deployed to your resource group, create a container called devicerules
2. In the storage account, use Storage Browser to open the newly created devicerules container
3. Add a directory inside the container named 2016-05-30
4. Inside the 2016-05-30 directory, create another directory called 22-40
5. Inside the 22-40 directory, upload the devicerules.json file found in this GitHub repo

### Start the Azure Stream Analytics jobs

1. Sign into the Azure portal and navigate to the Resource Group where your resources were deployed.
2. Click to open each Stream Analytics job that was deployed and, from the Overview tab, press Start.

### Update TSI connection

If you're working with Azure Time Series Insights, you'll need to update some information in your Dynamics 365 org.

1. Open up the Connected Field Service app module in your Dynamics 365 org.
2. Open the browser developer tools and open the console.
3. Enter and the below script into the console and run it, replacing the Value parameter with your Application (client) Id
4. Execute the script twice more, replacing the Key first with TSI_PLUGIN_CLIENT_APPLICATION_ID then with TSI_PLUGIN_CLIENT_SECRET, and replacing the Value with the respective values.

```javascript
var req = {};

req.getMetadata = function () {
  return {
    boundParameter: null,
    parameterTypes: {
      Key: {
        typeName: "Edm.String",
        structuralProperty: 1,
      },
      Value: {
        typeName: "Edm.String",
        structuralProperty: 1,
      },
    },
    operationType: 0,
    operationName: "msdyn_IoTSetConfiguration",
  };
};

req["Key"] = "TSI_PLUGIN_AZURE_TENANT_ID";
req["Value"] = "REPLACE";

Xrm.WebApi.online.execute(req).then(
  function (data) {
    console.log("Success Response Status: " + data.status);
  },
  function (error) {
    console.log("Error: " + error.message);
  }
);
```
