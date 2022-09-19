# Module 08 - Monitor

## :loudspeaker: Introduction

Microsoft Purview administrators can use Azure Monitor to track the operational state of a Microsoft Purview account instance. This information, for example, can be the number of scans completed or cancelled. Metrics are collected to provide data points for you to track potential problems, troubleshoot, and improve the reliability of the Microsoft Purview platform.

## :thinking: Prerequisites

* An [Azure account](https://azure.microsoft.com/free/) with an active subscription.
* A Microsoft Purview account (see [module 01](../modules/module01.md)).
* Your subscription must have the **Microsoft.Insights** resource provider registered.

## :dart: Objectives

* View Azure Purview metrics.
* Send Azure Purview diagnostic logs to Azure Storage.

## :bookmark_tabs: Table of Contents

1. [Provide a User Access to Azure Purview Metrics](#1-provide-a-user-access-to-azure-purview-metrics)
2. [Visualize Azure Purview Metrics](#2-visualize-azure-purview-metrics)
3. [Send Diagnostic Logs to Azure Storage](#3-send-diagnostic-logs-to-azure-storage)

## 1. Provide a User Access to Azure Purview Metrics

Metrics can be accessed from the Azure Portal for an Azure Purview account instance. Access to the metrics can be granted via a role assignment.
* The person who created the Purview account automatically gets permissions to view metrics.
* Other individuals can be provided access by adding them to the **Monitoring Reader** role.

1. Sign in to the [Azure portal](https://portal.azure.com), navigate to your **Azure Purview** account (e.g. `pvlab-{DID}-pv`), select **Access Control** and click **Add role assignment**.

    ![Azure Purview Access Control](../images/module08/M8-T1-S1.png)

2. Filter the list of roles by searching for `Monitoring Reader`, select the **Monitoring Reader** role and then click **Next**.

    ![Add Role Assignment](../images/module08/M8-T1-S2.png)

3. Click **Select members**, search for the user named **ODL_User <inject key="DeploymentID" enableCopy="false" />** in your Azure Active Directory and select that user from the list, and then click **Select**.

    > :bulb: **Did you know?**
    >
    > **Monitoring Reader** role can view all monitoring data but cannot modify any resource or edit any settings related to monitoring resources. This role is appropriate for users in an organization such as Azure Purview administrators.

    ![Assign Role](../images/module08/M8-T1-S3.png)

4. Click **Review + assign** to progress to the final screen, then click **Review + assign** once more to add the role assignment.

    ![Verify Access](../images/module08/M8-T1-S4.png)

## 2. Visualize Azure Purview Metrics

1. Navigate to your **Azure Purview** account instance and click **Metrics**.

    ![Azure Purview Metrics](../images/module08/M8-T2-Update1.png)

2. Click to open the **Metric** drop-down menu and select one of the metrics (e.g. `Scan time taken`).

    **Available Metrics**
    | Metric ID  | Metric Name | Metric Description |
    | --- | --- | --- |
    | DataMapCapacityUnits | `Data Map Capacity Units` | Indicates the number of capacity units consumed. |
    | DataMapStorageSize | `Data Map Storage Size` | Indicates the data map storage size. |
    | ScanCancelled | `Scan Cancelled` | Indicates the number of scans cancelled. |
    | ScanCompleted | `Scan Completed` | Indicates the number of scans completed successfully. |
    | ScanFailed | `Scan Failed` | Indicates the number of scans failed. |
    | ScanTimeTaken | `Scan Time Taken` | Indicates the total scan time in seconds. |

    ![Select Metric](../images/module08/M8-T2-Update2.png)

3. Click on the chart type to change the graph to a **Bar chart**.

    ![Metrics Chart Type](../images/module08/08.07-metrics-chart.png)

4. Click on the **time range** to change the duration to **Last 30 Days** and click **Apply**.

    ![Metrics Time Range](../images/module08/08.08-metrics-range.png)

5. Below is an example. Note: The account instance would need some historical scan activity in order to visualize the metric. 

    ![Metrics Graph](../images/module08/08.09-metrics-graph.png)

## 3. Send Diagnostic Logs to Azure Storage

1. Navigate to your **Azure Purview** account instance, click **Diagnostic settings** and select **Add diagnostic setting**.

    > :bulb: **Did you know?**
    >
    > **Diagnostic settings** can be used to send platform logs and metrics to one or more destinations (Log Analytics Workspace, Storage Account, an Event Hub).

    ![Add Diagnostic Setting](../images/module08/M8-T3-Update1.png)

2. Provide the diagnostic setting a name as `Audit` (1), select **ScanStatus** (2), select **Archive to a storage account** (3), select the existing storage account `pvlab{randomId}adls` and click **Save**.

    > :bulb: **Did you know?***
    >
    > **ScanStatus** tracks the scan life cycle. A scan operation follows progress through a sequence of states, from Queued, Running and finally a terminal state of Succeeded | Failed | Canceled. An event is logged for each state transition.

    ![Save Diagnostic Setting](../images/module08/M8-T3-S2.png)

3. To test the capture of raw events, trigger a full scan by navigating to **Azure Purview Studio**, **Data map**(1) > **Sources**(2) and click **View details**(3) on the existing **Azure Data Lake Storage Gen2** tile.

    ![Source Details](../images/module08/M8-T3-S3.png)

4. Navigate to the **Scans**(1) tab and click the name of a previously run scan (2).

    ![Source Scans](../images/module08/M8-T3-S4.png)

5. Open the **Run scan now**(1) drop-down menu and select **Full Scan**(2).

    ![Full Scan](../images/module08/M8-T3-S5.png)

6. Monitor the scan status by periodically clicking the **Refresh** button.

    ![Scan Progress](../images/module08/08.19-scan-progress-1.1.png)

7. Once the scan is complete, navigate to the storage account named **pvlab{randomId}adls** within the Azure Portal, select **Storage Browser** from the left hand side menu.

    ![Storage Explorer](../images/module08/08.20-storage-explorer-1.1.png)

8. Now, expand **Blob containers** and select **insights-logs-scanstatuslogevent**, navigate down the folder hierarchy until you reach a JSON document `PT1H.json`.

    ![Storage Explorer](../images/module08/08.20-storage-explorer-1.png)

8. Download and open a local copy of the JSON document to see the details (e.g. dataSourceName, dataSourceType, assetsDiscovered, scanTotalRunTimeInSeconds, etc).

    ![Event JSON](../images/module08/08.21-event-json.png)

## :mortar_board: Knowledge Check

[http://aka.ms/purviewlab/q08](http://aka.ms/purviewlab/q08)

1. Which built-in role is needed to provide users access to **view monitoring data**?

    A ) Purview Data Reader  
    B ) Metrics Reader  
    C ) Monitoring Reader

2. Which of the following is **not** available as an Azure Purview metric?

    A ) ScanCompleted  
    B ) ScanDuration  
    C ) ScanTimeTaken

3. The **ScanStatusLogEvent** schema contains an attribute that indicates the total run time. What is the name of this attribute?

    A ) scanTotalRunTime  
    B ) scanTotalRunTimeInSeconds  
    C ) scanTotalDuration

## :tada: Summary
This module provided an overview of how to visualize Azure Purview metrics within the Azure Portal and how to capture raw telemetry to an Azure Storage account.
