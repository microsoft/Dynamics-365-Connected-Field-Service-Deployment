# Dynamics 365 Connected Field Service - Azure IoT Deployment Template

## Overview

Connected Field Service enables organizations to transform the way they provide service from a costly break-fix model to a proactive and predictive service model through the combination of IoT diagnostics, scheduling, asset maintenance, and inventory on the same platform.
There are three ways you can use to connect IoT-enabled devices into the Field Service solution:

- Connected Field Service for [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/)
- Connected Field Service for non-Azure IoT providers using the extensible IoT provider framework

This repo will help you set up and configure Connected Field Service with Azure IoT Hub. For more information on using other providers, please see our documentation page here: [Connected Field Service - Overview | Microsoft Docs](https://docs.microsoft.com/dynamics365/field-service/connected-field-service)

Connected Field Service for Azure IoT Hub is an add-on solution that brings Azure IoT platform-as-a-service (PaaS) offering into Dynamics 365 for Field Service. With this offering, you can use this template and below instructions to put all the Azure IoT services and Dynamics puzzles together. All Azure IoT services run in your own Azure cloud subscription.

This deployment package will help you:

- Deploy and configure an IoT Hub instance. Connected Field Services uses the IoT Hub to manage the state of registered devices and assets. In addition, the IoT Hub sends commands and notifications to connected devices—and tracks message delivery with acknowledgement receipts.
- Deploy a device simulation (optional). This is a test web app to emulate the device that is sending commands or receiving commands from the IoT Hub.
- Deploy Time Series Insight (optional). Time Series Insights can be included in your deployment for detailed device insights and analytics.
- Deploy PowerBI (optional). Microsoft Power BI for device analytics can be included in your deployment. Choosing this will deploy two additional resources, Azure Streaming Analytics and SQL Server database.

## Deploy the ARM template

By deploying this template, you confirm that you’ve read and agree to the [Terms of Service](https://github.com/microsoft/Dynamics-365-Connected-Field-Service-Deployment/blob/main/Terms_of_Service.md) and the [Microsoft Privacy Statement](https://privacy.microsoft.com/en-us/privacystatement)

[![Deploy To Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjordanbean-msft%2FDynamics-365-Connected-Field-Service-Deployment%2Fmain%2FazureDeploy.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2Fjordanbean-msft%2FDynamics-365-Connected-Field-Service-Deployment%2Fmain%2FcustomUi.json)

**Note**: During deployment you'll be asked to provide your organization's unique name. You can find your organization's unique name by navigating to Advanced Settings on your Dynamics organization. Then navigate to Customizations > Developer Resources.

## Set up IoT Hub for Connected Field Service

After deploying Azure resource from the ARM template, follow the steps in our documentation to configure IoT settings: [Installation and setup - Connected Field Service for Azure IoT Hub](https://docs.microsoft.com/dynamics365/field-service/installation-setup-iothub)
