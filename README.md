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

## Deployment steps
By deploying this template, you confirm that you’ve read and agree to the [Terms of Service]() and the [Microsoft Privacy Statement](https://privacy.microsoft.com/en-us/privacystatement)

[<img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true" alt="Deploy To Azure" style="max-width: 100%;">]("https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmicrosoft%2FDynamics-365-Connected-Field-Service-Deployment%2FARMDeployment%2FazureDeploy.json%3Ftoken%3DGHSAT0AAAAAABVLOZFX4JO3AKEQACZBO7QMYV6UGOQ/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2Fmicrosoft%2FDynamics-365-Connected-Field-Service-Deployment%2Fmain%2FcustomUi.json%3Ftoken%3DGHSAT0AAAAAABVLOZFXAYU3TCH2P77UF6FAYV6VPYQ"target="_blank")

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

### Start the Azure Stream Analytics jobs
1. Sign into the Azure portal and navigate to the Resource Group where your resources were deployed.
2. Click to open each Stream Analytics job that was deployed and, from the Overview tab, press Start.
