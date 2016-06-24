---
title: Create WMI Filters for the GPO
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8a64b9c-4e24-44a2-8027-9acfbc2808e5
---
# Create WMI Filters for the GPO
To make sure that each GPO associated with a group can only be applied to computers running the correct version of Windows, use the Group Policy Management MMC snap-in to create and assign WMI filters to the GPO. Although you can create a separate membership group for each GPO, you would then have to manage the memberships of the different groups. Instead, use only a single membership group, and let WMI filters automatically ensure the correct GPO is applied to each computer.

-   [To create a WMI filter that queries for a specified version of Windows](#bkmk_1)

-   [To link a WMI filter to a GPO](#bkmk_2)

**Administrative credentials**

To complete these procedures, you must be a member of the Domain Administrators group, or otherwise be delegated permissions to modify the GPOs.

First, create the WMI filter and configure it to look for a specified version (or versions) of the Windows operating system.

## <a name="bkmk_1"></a>
#### To create a WMI filter that queries for a specified version of Windows

1.  On a computer that has the Group Policy Management feature installed, click **Start**, click **Administrative Tools**, and then click **Group Policy Management**.

2.  In the navigation pane, expand **Forest:** *YourForestName*, expand **Domains**, expand *YourDomainName*, and then click **WMI Filters**.

3.  Click **Action**, and then click **New**.

4.  In the **Name** text box, type the name of the WMI filter.

    > [!NOTE]
    > Be sure to use a name that clearly indicates the purpose of the filter. Check to see if your organization has a naming convention.

5.  In the **Description** text box, type a description for the WMI filter. For example, if the filter excludes domain controllers, you might consider stating that in the description.

6.  Click **Add**.

7.  Leave the **Namespace** value set to **root\CIMv2**.

8.  In the **Query** text box, type:

    ```
    select * from Win32_OperatingSystem where Version like "6.%"
    ```

    This query will return **true** for computers running Windows 8,  Windows 7 , Windows Vista,  Windows Server 2012 ,  Windows Server 2008 , and  Windows Server 2008 R2 . To set a filter for just Windows 8 and  Windows Server 2012 , use `"6.2%"`. To specify multiple versions, combine them with `or`, as shown in the following:

    ```
    ... where Version like "6.1%" or Version like "6.2%"
    ```

    To restrict the query to only clients or only servers, add a clause that includes the `ProductType` parameter. To filter for client operating systems only, such as Windows 8 or  Windows 7 , use only `ProductType="1"`. For server operating systems that are not domain controllers, use `ProductType="3"`. For domain controllers only, use `ProductType="2"`. This is a useful distinction, because you often want to prevent your GPOs from being applied to the domain controllers on your network.

    The following clause returns **true** for all computers that are not domain controllers:

    ```
    ... where ProductType="1" or ProductType="3"
    ```

    The following complete query returns **true** for all computers running Windows 8, and returns **false** for any server operating system or any other client operating system.

    ```
    select * from Win32_OperatingSystem where Version like "6.2%" and ProductType="1"
    ```

    The following query returns **true** for any computer running  Windows Server 2012 , except domain controllers:

    ```
    select * from Win32_OperatingSystem where Version like "6.2%" and ProductType="3"
    ```

9. Click **OK** to save the query to the filter.

10. Click **Save** to save your completed filter.

## <a name="bkmk_2"></a>After you have created a filter with the correct query, link the filter to the GPO. Filters can be reused with many GPOs simultaneously; you do not have to create a new one for each GPO if an existing one meets your needs.

#### To link a WMI filter to a GPO

1.  On a computer that has the Group Policy Management feature installed, click **Start**, click **Administrative Tools**, and then click **Group Policy Management**.

2.  In the navigation pane, find and then click the GPO that you want to modify.

3.  Under **WMI Filtering**, select the correct WMI filter from the list.

4.  Click **Yes** to accept the filter.


