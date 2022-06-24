# Dynamics 365 Connected Field Service, Azure Sample Template

By deploying this template, you confirm that you’ve read and agree to the Terms of Service and the [Microsoft Privacy Statement](https://privacy.microsoft.com/en-us/privacystatement)

<img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true" alt="Deploy To Azure" style="max-width: 100%;">

Connected Field Service enables organizations to transform the way they provide service from a costly break-fix model to a proactive and predictive service model through the combination of IoT diagnostics, scheduling, asset maintenance, and inventory on the same platform.
Connected Field Service enables organizations to transform the way they provide service from a costly break-fix model to a proactive and predictive service model through the combination of IoT diagnostics, scheduling, asset maintenance, and inventory on the same platform.
There are three ways you can use to connect IoT-enabled devices into the Field Service solution:

- Connected Field Service for [Azure IoT Central](https://azure.microsoft.com/en-us/services/iot-central/)
- Connected Field Service for [Azure IoT Hub](https://azure.microsoft.com/en-us/services/iot-hub/)
- Connected Field Service for non-Azure IoT providers using the extensible IoT provider framework

This repo will help you set up and configure Connected Field Service with Azure IoT Hub. For more information on using other providers, please see our documentation page here: [Connected Field Service - Overview | Microsoft Docs](https://docs.microsoft.com/en-us/dynamics365/field-service/connected-field-service)

Connected Field Service for Azure IoT Hub is an add-on solution that brings Azure IoT platform-as-a-service (PaaS) offering into Dynamics365 for Field Service. With this offering, you can run a deployment app to put all the Azure IoT services and Dynamics puzzles together. All Azure IoT services run in your own Azure cloud subscription.  
This deployment package will help you:
A) Deploy and configure an IoT Hub instance. Connected Field Services uses the IoT Hub to manage the state of registered devices and assets. In addition, the IoT Hub sends commands and notifications to connected devices—and tracks message delivery with acknowledgement receipts.
B) Deploy a device simulation (optional). This is a test web app to emulate the device that is sending commands or receiving commands from the IoT Hub.
C) Deploy Time Series Insight (optional). Time Series Insights can be included in your deployment for detailed device insights and analytics.
D) Deploy PowerBI (optional). Microsoft Power BI for device analytics can be included in your deployment. Choosing this will deploy two additional resources, Azure Streaming Analytics and SQL Server database.
