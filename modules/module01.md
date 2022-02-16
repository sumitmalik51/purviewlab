# Module 01 - Create an Azure Purview Account

## Introduction

To create and use the Azure Purview platform, you will need to provision an Azure Purview account.

## Objectives

* Create an Azure Purview account using the Azure portal.
* Provide additional users access to Azure Purview's data plane.

## Table of Contents

| #  | Section | Role |
| --- | --- | --- |
| 1 | [Create an Azure Purview Account](#1-create-an-azure-purview-account) | Azure Administrator |
| 2 | [Grant Access to Azure Purview's Data Plane](#2-grant-access-to-azure-purviews-data-plane) | Collection Administrator |

## 1. Create an Azure Purview Account

1. In the Azure portal, expand the portal's left navigation and select **+ Create a resource**, search for **Azure Purview** and select it.

2. On the **Azure Purview** blade, select **Create**.

    ![Create Purview Resource](../images/module01/Mod1-purview01.png)

3. Provide the below inputs on the **Basics** tab.  

    > Note: Replace the **DID** with the **Deployment Id** from the Environemnt Details Page.

    | Parameter  | Example Value |
    | --- | --- |
    | Subscription | `YOUR_AZURE_SUBSCRIPTION` |
    | Resource group | `purviewlab-rg` |
    | Purview account name | `pvlab-[DID]-pv` |
    | Location | `Choose the same region as the Resource Group` |
    | Managed Resource Group Name | `purviewlab-rg-managed` |

    ![Purview Account Basics](../images/module01/Mod1-purview02.png)

    > **Did you know?**
    >
    > **Capacity Units** determine the size of the platform and is a **provisioned** (always on) set of resources that is needed to keep the Azure Purview platform up and running. 1 Capacity Unit is able to support approximately 25 data map operations per second and includes up to 2GB of metadata storage about data assets.
    >
    > Capacity Units are required regardless of whether you plan to invoke the Azure Purview API endpoints directly (i.e. ISV scenario) or indirectly via Purview Studio (GUI).
    >
    > Note: With the introduction of the [Elastic Data Map](https://docs.microsoft.com/en-us/azure/purview/concept-elastic-data-map), you no longer need to specify how many Capacity Units that you need. Azure Purview will scale capacity elastically based on the request load.
    > 
    > **vCore Hours** on the other hand, is the unit of measure for **serverless** compute that is needed to run a scan. You only pay per vCore Hour of scanning that you consume (rounded up to the nearest minute).
    >
    > For more information, check out the [Azure Purview Pricing](https://azure.microsoft.com/en-us/pricing/details/azure-purview/) page.

4. On the **Networking** tab, select **All networks**.
   
    ![Networking](../images/module01/Mod1-purview03.png)

5. On the **Review + Create** tab, once the message in the ribbon returns "Validation passed", verify your selections and click **Create**.

    ![Create Purview Account](../images/module01/Mod1-purview04.png)

6. Wait several minutes while your deployment is in progress. Once complete, click **Go to resource**.

    ![Go to resource](../images/module01/Mod1-purview05.png)

## 2. Grant Access to Azure Purview's Data Plane

1. Navigate to your Azure Purview account and click **Open** within the **Open Purview Studio** tile.

    ![Access Control](../images/module01/Mod1-purview06.png)

2. On the left-hand side, navigate to **Data map**.

    ![Add Role Assignment](../images/module01/Mod1-purview07.png)

3. Select **Collections (1)** and click on **Role assignments (2)**.

    ![Collections](../images/module01/Mod1-purview08.png)

4. On the right-hand side of **Data curators**, click the **Add** icon.

    ![Add Role Assignment](../images/module01/Mod1-purview09.png)

5. Search for another user (ex; **user_01**) within your Azure Active Directory, select their account, click OK.

    ![Add or Remove Data Curators](../images/module01/user01.png)

    > **Did you know?**
    >
    > Azure Purview has a set of predefined data plane roles that can be used to control who can access what.
    >
    > For more information, check out [Access control in Azure Purview](https://docs.microsoft.com/en-us/azure/purview/catalog-permissions).

    | Role  | Collections | Catalog | Sources/Scans | Description | 
    | --- | --- | --- | --- | --- |
    | Collection Admin | `Read/Write` | | | Manage collections and role assignments. |
    | Data Reader ||  `Read` |  | Access to catalog (read only). |
    | Data Curator || `Read/Write` |  | Access to catalog (read & write). |
    | Data Source Admin |  || `Read/Write` | Manage data sources and data scans. |

## Knowledge Check

[http://aka.ms/purviewlab/q01](http://aka.ms/purviewlab/q01)

1. Which of the following Azure Purview pricing meters is fluid, with consumption varying based on usage?

    A ) Capacity Units  
    B ) vCore Hours  
    C ) Neither

2. Which of the following Azure Purview pricing meters is always on, with consumption based on quantity provisioned?

    A ) Capacity Units  
    B ) vCore Hours  
    C ) Neither

3. Which Azure Purview module provides the base functionality (i.e. source registration, automated scanning and classification, data discovery)?

    A ) C0  
    B ) C1  
    C ) D0

4. Which predefined Azure Purview role provides access to manage data sources?

    A ) Purview Data Reader  
    B ) Purview Data Curator  
    C ) Purview Data Source Administrator

## Summary

This module provided an overview of how to provision an Azure Purview account using the Azure Portal and how to grant the appropriate level of access to Azure Purview's data plane.
