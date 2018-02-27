
# Lab 200 - Creating ICS Connections

## Introduction

This is the second of several labs that are part of the **ICS HCM Development Workshop**.

In this lab, you will learn how to create a basic ICS connection, using a basic orchestration.

## Objectives

- Create your first FTP and SOAP connections to later be used in the Integration that will be created in Lab 300.

## Required Artifacts

- The following lab and an Oracle Public Cloud account that will be supplied by your instructor.

## **2.1** Login to your Oracle Cloud account

### **2.1.1** Login to ICS Home Page

>***NOTE:*** the **User Name** and **Password** values will be given to you by your instructor. See _Lab 100 **1.1.1**: Login to your Oracle Cloud Account_ for more information on how to sign into the ICS home page

![](images/200/image001.png)  

## **2.2** Creating Simple Orchestration Integration

### **2.2.1** Create Talent Profile SOAP Input Connection

This connection is used to call the importAndLoadData operation of the HCM Data Loader SOAP API. Its WSDL URL points to an HCM Cloud instance in Oracle’s demo environment.


**2.2.1.1** Click on the **Connections** section

![](images/200/image002.png)

**2.2.1.2** Click on **Create** in the upper right of the screen

![](images/200/image003.png)

**2.2.1.3** Select the **SOAP** Connection, by either doing a search, or by scrolling down to the **SOAP** connection, by clicking on the **Select** button of the **SOAP** connection.

![](images/200/image139.png)

**2.2.1.4** Fill in the information for the new connection

- **Name** in the form of _ICSHCM_SOAP_TalentProfile_Input_UserXX_ where XX is the number in your allocated user.
- **Role** _Trigger_ since we going to use the connection as an trigger the start of an integration

![](images/200/image148.png)

**2.2.1.5** click **Create**

![](images/200/image141.png)


**2.2.1.6** Click on the connection you just created. It opens up the window for you to configure different properties for the adapter.

![](images/200/image1000.png)

We need to access the file "TalentProfile.wsdl" for our next step. The file is located in the Artifacts folder given as part of the workshop by the instructor. Please make sure you have the file before moving on to next step.

**2.2.1.7** Click on **Configure Connectivity** under **Connection Properties** section.

Check the box under the **Upload File** column.

Open up the folder Artifacts that was provided to you and locate the file "TalentProfile.wsdl".

Select this file and click **OK**.

Then click on the **Upload Button**

Then click **Ok** to close.

![](images/200/image149.png)


**2.2.1.8** Scroll down the same page and then click on the **Configure Security** under the **Security** section. This will bring up the prompt to configure your SOAP Security.


**2.2.1.9** You will now be asked to create the Security credentials for your SOAP connection.

Leave the **Security Policy** as **Username Password Token**, or else change it if something else is selected.

This is what is required to login to Integration Cloud Service

Now click on **Ok** to close the prompt.

![](images/200/image150.png)


**2.2.1.10** Click on **Test**

![](images/200/image007.png)

**2.2.1.11** Click **Save**

![](images/200/image008.png)

**2.2.1.12** Click on the **Close** link in the upper right

Your connection appears in the list of configured connections and is even marked as **New** !

![](images/200/image151.png)

----

### **2.2.2** Create the FA-UCM SOAP Connection

This connection is used to call the importAndLoadData operation of the HCM Data Loader SOAP API. Its WSDL URL points to an HCM Cloud instance in Oracle’s demo environment.


**2.2.2.1** Click on the **Connection** section

![](images/200/image002.png)

**2.2.2.2** Click on **Create** in the upper right of the screen

![](images/200/image003.png)

**2.2.2.3** Select the **SOAP** Connection, by either doing a search, or by scrolling down to the **SOAP** connection, by clicking on the **Select** button of the **SOAP** connection.

![](images/200/image139.png)

**2.2.2.4** Fill in the information for the new connection

- **Name** in the form of _ICSHCM-POC-FA-UCM-Conn_UserXX_ where XX is the number in your allocated user.
- **Role** _Invoke_ since we going to use the connection as an invoke to start the integration

![](images/200/image145.png)

**2.2.2.5** click **Create**

![](images/200/image141.png)

**2.2.2.6** Click on **Configure Connectivity**.

![](images/200/image141.png)

In the **WSDL URL** field enter "https://ucf6-fap0868-fs.oracledemos.com/idcws/GenericSoapPort?WSDL"

Then click **Ok** to close.

![](images/200/image146.png)

>***Note*** The default security configuration is set to **Basic Authentication**, which by the way, is the only option available for REST trigger connections. When invoking the trigger, we will use our ICS username/password.

**2.2.2.7** Scroll down the same page and then click on the **Configure Security**. This will bring up the prompt to configure your SOAP Security.


**2.2.2.8** You will now be asked to create the Security credentials for your SOAP connection.

Leave the **Security Policy** as **Basic Authentication**, or else change it if something else is selected.

We need configure **User Name** and **Password**. The **User Name** and **Password** can be obtained from the supplement guide provided by the instructor.

If a User Name and Password are not provided, use the default settings:
**User Name:** faadmin
**Password:** fusionfa1

Now click on **Ok** to close the prompt.

![](images/200/image154.png)


**2.2.2.9** Click on **Test**

![](images/200/image007.png)

**2.2.2.10** Click **Save**

![](images/200/image008.png)

**2.2.2.11** Click on the **Close** link in the upper right

Your connection appears in the list of configured connections and is even marked as **New** !

![](images/200/image147.png)

----

### **2.2.3** Create the FA-HCM SOAP Connection

This connection is used to call the GenericSoapPort service of UCM to upload the data file to UCM. Basic authentication must be configured. The WSDL URL points to the UCM instance associated with the HCM instance.


**2.2.3.1** Click on the **Connection** section

![](images/200/image002.png)

**2.2.3.2** Click on **Create** in the upper right of the screen

![](images/200/image003.png)

**2.2.3.3** Select the **SOAP** Connection, by either doing a search, or by scrolling down to the **SOAP** connection, by clicking on the **Select** button of the **SOAP** connection.

![](images/200/image139.png)

**2.2.3.4** Fill in the information for the new connection

- **Name** in the form of _ICSHCM-POC-FA-HCM-Conn_UserXX_ where XX is the number in your allocated user.
- **Role** _Invoke_ since we going to use the connection as an invoke to start the integration

![](images/200/image140.png)

**2.2.3.5** click **Create**

![](images/200/image141.png)

**2.2.3.6** Click on **Configure Connectivity**.
In the **WSDL URL** field enter "https://ucf6-fap0868-hcm.oracledemos.com/hcmCommonDataLoader/HCMDataLoader?WSDL"

Then click **Ok** to close.

![](images/200/image153.png)

>***Note*** The default security configuration is set to **Basic Authentication**, which by the way, is the only option available for REST trigger connections. When invoking the trigger, we will use our ICS username/password.

**2.2.3.7** Scroll down the same page and then click on the **Configure Security**. This will bring up the prompt to configure your SOAP Security.

**2.2.3.8** We need configure **User Name** and **Password**. The **User Name** and **Password** can be obtained from the supplement guide provided by the instructor.


**2.2.3.9** You will now be asked to create the Security credentials for your FTP connection.

Leave the **Security Policy** as **Basic Authentication**, or else change it if something else is selected.

For the **User Name** use the **User name** from supplement.

In the **Password** field use the **Password** from supplement.

Now click on **Ok** to close the prompt.

![](images/200/image143.png)


**2.2.3.10** Click on **Test**

![](images/200/image007.png)

**2.2.3.11** Click **Save**

![](images/200/image008.png)

**2.2.3.12** Click on the **Close** link in the upper right

Your first connection appears in the list of configured connections and is even marked as **New** !

![](images/200/image144.png)

----

### **2.2.4** Creating an FTP Connection

**2.2.4.1** Go to the cloud dashboard page and click on **Integration** service. Ex: https://myservices.us2.oraclecloud.com/mycloud/faces/dashboard.jspx

Every domain will have FTP server associated with it. We will use this FTP server to host our files.


![](images/200/image086.png)

**2.2.4.2** Check the Additional Information. The FTP server details are given.

Copy Domain SFTP User Name, Host, port, and save it somewhere.

**Domain SFTP User Name:**
**SFTP Host:**
**Port:**


This will be the FTP user which is used in FTP connection creation.

![](images/200/image087.png)

**2.2.4.3** You can also access this info by clicking  on **Users** on the top right  ->SFTP Users  Username

![](images/200/image088.png)

**2.2.4.4** Now click on the SFTP Users in the panel to see the users with Secure FTP user accounts.

![](images/200/image089.png)

**2.2.4.5** Navigate back to the ICS console

![](images/200/image090.png)

![](images/200/image091.png)

Now click on the **Connections**

![](images/200/image092.png)

**2.2.4.6** On the top bar click on **Create** to bring up the menu to create a new Connection.

![](images/200/image130.png)

The following prompt should pop up. Either scroll down and select or search for "FTP"

![](images/200/image131.png)

**2.2.4.7** The following screen should display when you click to create a new FTP Connection.

![](images/200/image133.png)


**2.2.4.8** In the **Name** field enter "ICSHCM-POC-FTP_UserXX" and replace the "XX" with your assigned user name.

Set the Role to **Trigger and Invoke**


**2.2.4.9** Click on **Configure Connectivity**. Use the
Domain **SFTP Host** as **FTP server host address** from step **1.2** which was retrieved from dashboard, without the port included.

Enter the **Port** as found in step **1.2**. It is most likely **22**.

Set the **SFTP Connection** to **True**.

Port : 22
SFTP connection: True

Then click **Ok** to close.

![](images/200/image134.png)

**2.2.4.10** Scroll down the same page and then click on the **Configure Security**. This will bring up the prompt to configure your FTP Security.

![](images/200/image135.png)

**2.2.4.11** You will now be asked to create the Security credentials for your FTP connection.

Leave the **Security Policy** as **FTP Server Access Policy**, or else change it if something else is selected.

For the **User Name** use the **Domain SFTP User Name** that you previously saved from step **4.2**.

In the **Password** field user the password that you originally used to log into Oracle Cloud provided by the instructor. It will be the password for either the cloud.admin or UserXX users.

Now click on **Ok** to close the prompt.

![](images/200/image136.png)

**2.2.4.12** Then click **Test** in order to test the connect. A green bar should come across the top of the screen that reads, "Connection ICSHCM-POC-FTP_UserXX was tested successfully."

![](images/200/image137.png)

Click on the **Save** in order to save your Connection. A green bar should come across the top of the screen that reads, "Connection ICSHCM-POC-FTP_UserXX was saved successfully."

![](images/200/image138.png)

----



- This Lab is now completed.
