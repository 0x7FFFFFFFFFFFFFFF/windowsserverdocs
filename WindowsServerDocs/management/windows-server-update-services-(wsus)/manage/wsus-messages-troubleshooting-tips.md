---
title: WSUS Messages and Troubleshooting Tips
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-management-and-automation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f6317f7-bfe0-42d9-87ce-d8f038c728ca
---
# WSUS Messages and Troubleshooting Tips
This topic provides information about some common WSUS messages.

## WSUS Messages
This section contains information about the following WSUS messages:

-   **computer has not reported status:**

-   **Message ID 6703 \- WSUS Synchronization Failed**

-   **Error 0x80070643: Fatal error during installation**

-   **Some services are not running. Check the following services**

### computer has not reported status:
**Troubleshooting computer connection issues**

This message is generated in the WSUS console when a WSUS client computer does not send information to the WSUS server to indicate it's current update state. This issue is typically caused by the WSUS client computer, not the WSUS server.

The most common reasons are:

-   The computer is turned off

-   The computer has lost connectivity to the network:

    -   The network cable is unplugged

    -   The computer has a faulty network adapter

    -   The network port to which the computer connects has been disabled

    -   The wireless adapter is unable to associate with and connect to  the corporate wireless access point

-   The computer is in hibernation mode

-   The computer has been physically removed from the network

### Message ID 6703 \- WSUS Synchronization Failed
**Message: The request failed with HTTP status 503: Service Unavailable**.

**Source: Microsoft.UpdateServices.Administration.AdminProxy.createUpdateServer.**

When you attempt to open Update Services on the WSUS server you receive the following error:

**Error: Connection Error**

**An error occurred trying to connect to the WSUS server. This error can happen for a number of reasons. Please contact your network administrator if the problem persists. Click the reset Server Node to connect to the server again.**

In addition to the above, attempts to access the URL for the WSUS Administration website \(i.e., http:\/\/CM12CAS:8530\) fails with the error:

**HTTP Error 503. The service is unavailable**

In this situation, the most likely cause is that the WsusPool Application Pool in IIS is in a stopped state.

Also, the Private Memory Limit \(KB\) for the Application Pool is probably set to the default value of 1843200 KB.

if you encounter this problem, increase the Private Memory Limit to 4GB \(4000000 KB\) and restart the Application Pool. To increase the Private Memory Limit, select the WsusPool Application Pool and click Advanced Settings under edit Application Pool. Then set the Private Memory Limit to 4GB \(4000000 KB\).

After the Application Pool has been restarted, monitor the SMS\_WSUS\_SYNC\_manageR component status, wcm.log and wsyncmgr.log for failures. Please note that it may be necessary to increase the Private Memory Limit to 8GB \(8000000 KB\) or higher depending on the environment.

for additional details, see: [WSUS sync in ConfigMgr 2012 fails with HTTP 503 errors](http://blogs.technet.com/b/sus/archive/2015/03/23/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors.aspx)

### Error 0x80070643: Fatal error during installation
**Cause:** WSUS Setup uses Microsoft SQL Server to perform the installation. This problem occurs because the user who is running WSUS Setup does not have System Administrator permissions in SQL Server.

**Resolution:** To resolve this problem, grant System Administrator permissions to a user account or to a group account in SQL Server, and then run WSUS Setup again.

### Some services are not running. Check the following services:
**Selfupdate** See [Automatic Updates Must Be Updated](https://technet.microsoft.com/en-us/library/cc708554(v=ws.10).aspx) for information about troubleshooting the Selfupdate service.

**WSSUService.exe** This service facilitates synchronization. if you have problems with synchronization, access WSUSService.exe by clicking **start**, pointing to **Administrative Tools**, clicking **Services**, and then finding **Windows Server Update Service** in the list of services. Do the following:

-   verify that this service is running. Click **start** if it is stopped or **Restart** to refresh the service.

-   Use Event Viewer to check the **Application**, **Securit**y, and **System** event logs to see if there are any events that might indicate a problem.

-   You can also check the SoftwareDistribution.log to see if there are events that might indicate a problem.

**Web servicesSQL Service** Web services are hosted in IIS. if they are not running, ensure that IIS is running \(or started\). You can also try resetting the Web service by typing **iisreset** at a command prompt.

**SQL Service** Every service except for the selfupdate service requires that the SQL service is running. if any of the log files indicate SQL connection problems, check the SQL service first. To access the SQL service, click **start**, point to **Administrative Tools**, click **Services**, and then look for one of the following:

-   **MSSQLSERver** \(if you are using WMSDE or MSDE, or if you are using SQL Server and are using the default instance name for the instance name\)

-   **MSSQL$WSUS** \(if you are using a SQL Server database and have named your database instance "WSUS"\)

    Right\-click the service, and then click **start** if the service is not running, or **Restart** to refresh the service if it is running.

### See also
WSUS resources on the [Windows Server Update Services](https://technet.microsoft.com/en-us/windowsserver/bb332157.aspx) Windows Server Update Services  TechCenter page


