---
uid: EpmIntegrationTrainingAbout
---

# EPM Integration Training

To get started with EPM integration, you can install the EPM Integration Training package. This package contains all the necessary components to understand, navigate, and get hands-on with an EPM solution.

## Installation

If your DataMiner System is connected to dataminer.services, you can deploy the package directly from the [DataMiner Catalog](https://catalog.dataminer.services/details/b661f936-d6e7-447c-baee-f0a5503e75b4). Otherwise, please reach out to your Skyline contact so they may provide the package executable.

You can install the package on a single DMA. If more DMAs are present in the cluster, the package will utilize at most three DMAs to create a front-end element, two back-end elements, and three collectors, distributing them across the DMAs as follows:

- Agent 1:

  - **EPM Availability Front End**

- Agent 2:

  - **EPM Availability Back-End 1**
  - **EPM Availability Collector 1**
  - **EPM Availability Collector 2**

- Agent 3:

  - **EPM Availability Back-End 2**
  - **EPM Availability Collector 3**

## Components

The EPM Integration Training package installs the following components:

- Connectors:

  - Skyline EPM Integration Training Manager
  - Skyline EPM Integration Training Collector

- Dashboards:

  - Device Overview
  - Device Grid Overview

- Low-code app:

  - EPM Integration Training

- Visio drawings:

  - Skyline EPM Integration Training.vsdx

## Table structure

The front-end element has minimal information in its local tables. It retrieves all the DMS information via view tables.

|            | Frontend Local Table | Frontend View Table | Backend Local Table |
|------------|----------------------|---------------------|---------------------|
| Network    | PK,FK,KPIs           | PK,FK,KPIs          | Empty               |
| Region     | PK,FK                | PK,FK,KPIs          | PK,FK,KPIs          |
| Sub-Region | Empty                | PK,FK,KPIs          | PK,FK,KPIs          |
| Hub        | Empty                | PK,FK,KPIs          | PK,FK,KPIs          |
| Station    | Empty                | PK,FK,KPIs          | PK,FK,KPIs          |
| Endpoint   | Empty                | PK,FK               | PK,FK               |
