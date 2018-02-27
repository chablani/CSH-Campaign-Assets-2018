Updated: 11-14-17

<img class="float-right" src="https://oracle.github.io/learning-library/workshops/common-content/images/touch-the-cloud/ttc-logo.png" width="200">
# Lab 100 - Explore Integration Cloud Service

---

## Objectives

- Explore Integration Cloud Service (ICS) to become familiar with it's service console and functionality.

## Required Artifacts

- The following lab and an Oracle Public Cloud account that will be supplied by your instructor.

## Introduction

This is the first of several labs that are part of the **ICS Development** workshop.

In this lab, we will explore the main parts of Integration Cloud Service (ICS).  You will acquire a good overview of the Oracle Integration Cloud Service (ICS), the next generation integration platform. You will explore various consoles and tools available to interact with your integration. The exercise will get your familiar with all the tooling available to work with this cloud service. Oracle ICS can function as a central hub for taking in external data feeds, correctly formatting it for HCM Cloud, and automating the final upload of external data into HCM Cloud via HCM Data Loader, With all feeds flowing through ICS, there is greater visibility into the end-to-end data flow between HCM Cloud and external systems. This greatly reduces the integration cost.

We’ll look at the following:
1.	Oracle Cloud Services Dashboard
2.	ICS Designer User Interface
3.	ICS Monitoring User Interface

Here is a description of what is happening with ICS integration that we'll be working in the lab:

Oracle HCM manages persons (workers) of an organization. Each person in HCM has an associated profile. A person’s profile can contain all kinds of information relevant to the person and the organization they belong to. Different categories of information in a profile are organized as Content Sections. Each content section is associated with a Content Type. One example of a content section (or content type) is “Competencies”, which describes a person’s various competency levels.
In our use case, a custom content type called “Additional Qualifications” has been created in HCM. This content type has three content items defined: Artist, Athlete and Photographer. The use case in this example calls for adding additional qualifications to a person’s profile.

Steps for Integration:

1.	Accept an XML document as input
2.	Convert input XML data into HDL format data
3.	Zip HDL format data (HCM Data Loader requires zipped file)
4.	Base64 encode zipped HDL format data (base64 encoding is required to transmit binary data in SOAP/XML web service)
5.	Call UCM Generic SOAP Service to upload the zip file content (base64 encoded zipped data from the prior step)
6.	Call HCM Data Loader SOAP Service to schedule an Import and Load HCM File Data process
7.	Return the HCM processed ID to ICS caller

Let’s start by logging into the Oracle Cloud account and explore the Services Dashboard

## 1.1: Explore the Oracle Cloud Dashboard

### **1.1.1**: Login to your Oracle Cloud account

---

**1.1.1.1** From your browser (Firefox or Chrome recommended) go to the following URL:
<https://cloud.oracle.com>

**1.1.1.2** Click _Sign In_ in the upper right hand corner of the browser
**IMPORTANT** - Under My Services, change Data Center to `US Commercial 2 (us2)` and click on Sign In to My Services

![](images/100/image001.png)

**1.1.1.3** If your identity domain is not already set, enter it and click **Go**

**NOTE:** the **Identity Domain** values will be given to you from your instructor.

![](images/100/image002.png)  

**1.1.1.4** Once your Identity Domain is set, enter your `User Name` and `Password` and click **Sign In**

***NOTE:*** the **User Name and Password** values will be given to you by your instructor.

![](images/100/image003.png)  

**1.1.1.5** You will be presented with a Dashboard displaying the various cloud services available to this account.

**NOTE:** The Cloud Services dashboard is intended to be used by the *Cloud Administrator* user role.  The Cloud Administrator is responsible for adding users, service instances, and monitoring usage of the Oracle cloud service account.  Developers and Operations roles will go directly to the service console link, not through the service dashboard.

![](images/100/image004.png)

**1.1.1.6**  To get to the Integration Cloud Service (ICS) service console where you will work on developing the integration, click on the `hamburger` icon in the _Integration_ section, then click on the `View Details` link.

![](images/100/image004a.png)

**1.1.1.7**  Select the `Open Service Console` link to go to the ICS Service Console.  

![](images/100/image004b.png)  

**1.1.1.8**  You will now be presented with the ICS Service Console from which you will be performing the rest of this workshop lab.

![](images/100/image004c.png)  

## 1.2: Explore the ICS Designer User Interface

---

### **1.2.1:**	Explore ICS Connections

---

**1.2.1.1:** Select the `Connections` graphic in the designer portal

![](images/100/image005.png)  

**1.2.1.2:** Make note of the connections that have been created. Notice that, among others, there are four connections, one called *ICSHCM_SOAP_TalentProfile_Input_UserXX*, one called *ICSHCM-POC-FA-HCM-Conn_ UserXX*, one called *ICSHCM-POC-FA-UCM-Conn_UserXX* and the other called *ICSHCM-POC-FTP_UserXX*.

![](images/100/image010.png)  

**1.2.1.3:** Click on the `Create` button in the upper-right so we can see all the different ICS Connectors that are available.

![](images/100/image010b.png)

**1.2.1.4:** Scroll through the list of connection types that are available in ICS:

![](images/100/image010c.png)

**1.2.1.5:** Note that the icons with the plug are those that support the ICS Connectivity Agent for those service types which are not in the cloud, but on-premise, behind the company firewall.

**1.2.1.6:** When you are done browsing, select the “Cancel” button to dismiss the “Select an Adapter” dialog.

### **1.2.2:**	Explore ICS Integrations

---

**1.2.2.1** Select the `Hamburger` menu icon on top of the ICS Service Console to go to the `Designer` menu.

**1.2.2.2** Select the `Integrations` menu selection

![](images/100/image034.png)

**1.2.2.3** Select the `Hamburger` menu icon again to dismiss the left-hand navigation and get some screen real-estate back.

**1.2.2.4** Make note of the integrations that have been created. We will be working with the integration called *ICSHCM Add Talent Profile UserXX*.

![](images/100/image012.png)  

**1.2.2.5** Open the integration `ICSHCM Add Talent Profile UserXX` by clicking on the integration name.  We want to see what it looks like.  Since the integration is already active, we’ll be looking at it in `Viewing` mode.  There will be a warning that _Edit is not possible..._ in yellow displayed along the top.  You can dismiss the warning bar by selecting the little "X" on the very right of the warning.

![](images/100/image012a.png)

**1.2.2.6** You can see that this orchestration has many steps in it.  The view of the orchestration is *Zoom to Fit* in the browser real estate.  In order to get a closer view of the individual steps, you can either scroll with your mouse wheel to zoom in and out, or you can use the *-/+* slider in the top right of the designer.

**1.2.2.7** Try zooming in and out by using both methods.  

**1.2.2.8** If you get zoomed-in too close and want to pan, you’ll be able to move around the orchestration using the Pan window by clicking on the dark area and moving around.

![](images/100/image012b.png)

**1.2.2.9** Select the `Start` icon and the drawing gets reset to a zoomed in view with the orchestration trigger at the very top.  This is a nice feature if you don't know where you are in a large orchestration.

   ![](images/100/image012c.png)

**1.2.2.10** Try selecting the `Maximize` viewing control on the very right of the view control bar.  This will hide some of the detail on top of the screen to give the designer the most area to work in.  Hitting the `Maximize` button again will toggle that view.

![](images/100/image012d.png)

**1.2.2.11** Let’s look at some of the components of the integration.  Select the `Maximize` view button again to restore the window.

**1.2.2.12** The component at the very top of the orchestration is the `Trigger`.  The trigger is representative of the connector that’s sending data into the integration.  It is highlighted with a little lightning bolt signifying an incoming event.

**1.2.2.13** If you hover over the Trigger node, you can see the details.  Our trigger is a SOAP connector type.  It is called *addTalentprofileData* and it is using the connection named *addTalentprofileData* that we looked at before in the Connection section of the ICS Designer.

![](images/100/image012e.png)

**1.2.2.14** If you click on the Trigger, a pop-up will appear with a view icon in the shape of an eye.  Select the little eye so we can walk through the wizard that was used to setup the SOAP trigger.

![](images/100/image012f.png)

**1.2.2.15** After the wizard initializes, you’ll be shown the basic information about the trigger – it’s name and description.

![](images/100/image012g.png)

**1.2.2.16** Select the `Next` button to see the `Operations` that were configured for this SOAP Trigger.  Details like the Port Type, Operation, and request and response objects are shown.  In our case, no special SOAP headers were needed so that was set to `No`.

![](images/100/image012h.png)

**1.2.2.17** Select the `Next` button to see hte `Headers` configuration.  We didn't select to add any special headers, so the default of _No_ is shown.

![](images/100/image012t.png)

**1.2.2.18** Select `“Next` again to see the `Summary` of the Trigger’s configuration.  The SOAP WSDL was uploaded to ICS when the connection was first configured, not in the wizard to configure the Trigger.

![](images/100/image012i.png)

**1.2.2.19** Select the `Close` button to dismiss the Trigger view wizard.

**1.2.2.20** Let’s view the next node down in the integration.  This is an *Assign* node.  The job of this Assign activity is to initialize variables that will be used in the calls to be made to the File system.

![](images/100/image012j.png)

**1.2.2.21** The variables defined in this Assign activity are view only.  Later on in this lab, we’ll de-activate the integration and all the values will be changeable. You can see the variable fileName defined. Using variable rather than hard-coding these in the mapping for the adapter is preferable because they can be re-used across multiple adapter invocations if necessary.There are two file names involved in HCM Data Loader. First, the zip file name can be any name with a zip extension. Second file name is the actual data file contained in the zip file. HCM Data Loader defines a file name for each data object. In our case, the data file name must be TalentProfile.dat. In our implementation, the zip file name has a pattern of “TPyyyymmddhhmmss”. The zip extension is appended in a later step.


![](images/100/image012k.png)

**1.2.2.22** Select the `Close` button in the upper-right to go back to the view of the orchestration.

**1.2.2.23** Back in the view of the orchestration we want to explore some of the nodes toward the bottom.  You can pan directly in the design window by clicking & holding the mouse button down in the background of the design palette, then you can pan up and down.

![](images/100/image012l.png)

**1.2.2.24** Pan down to the map called `writeInputAsHDLFormat`.  Click on this map activity and select the view icon.  We are going to see the mapping between an input XML data to a full XML data set that contains additional meta data labels required by HDL.

![](images/100/image012m.png)

**1.2.2.25** This is the most complex mapping in this integration because we’re leveraging has thousands of attributes that can be passed.

**1.2.2.26** What you’ll see in the mapper is the possible input variables on the left and that can be mapped to on the right.  The values that have been mapped are shown to the right side of the inbound variables in the mapper.

**1.2.2.27** In order to simplify this view, we want to `Filter` the Target variables.  Select the `Filter` button above the Target section and then select the radio button labeled `Mapped`, then select the `Apply` button.

![](images/100/image012n.png)

**1.2.2.28** Now we only see variables in the Target that have been mapped from a Source variable.  If you want to get a visual depiction of where a Target variable has been mapped from, select the little green checkbox to the very left of the Target variable.  This will make a line visible from the Source variable to the Target.

![](images/100/image012o.png)


**1.2.2.29** Once you are done exploring this complex ICS map, select the `Close` button in the upper-right to return back to the ICS orchestration.

**1.2.2.30** We’ve spent a lot of time exploring the `ICSHCM Add Talent Profile UserXX` integration.  Let’s move on and explore the Agent setup.  Select the `Close` button in the upper-right to navigate back to the ICS Designer.

![](images/100/image012s.png)


## 1.3: Explore the ICS Monitoring User Interface

### **1.3.1:**	Open ICS Monitoring Console

---

**1.3.3.1** Select the `Hamburger` menu icon on top of the ICS Service Console and click the back arrow to see the `Monitoring` menu if it isn't visible.

**1.3.3.2** Next, select the `Monitoring` menu selection to go the ICS monitoring capabilities.

![](images/100/image110a.png)

**1.3.3.3** Next, select the `Dashboards` selection to go to the main ICS monitoring dashboard page.

![](images/100/image110b.png)

### **1.3.2:**	Explore ICS Monitoring Console - Dashboard

---

**1.3.2.1** You will be presented with the ICS Monitoring Dashboard.  Observe the various data that is available from this dashboard such as *% of successful messages*, *# of Currently Used Connections*, etc.

![](images/100/image016.png)  

**1.3.2.2** On the right side of the `Dashboard` there are links where you can view the `Activity Stream`, Download the logs, and Download an Incident if a service request needs to be raised.

**1.3.2.3** Click on the Activity Stream link

![](images/100/image017.png)

**1.3.2.4** You will be directed to the `Integration` screen where you can view a summary of all messages that have passed through ICS in a tabular form.

![](images/100/image018.png)

**1.3.2.5** In the `Activity Stream` you can see the steps in the *ICSHCM_ADD_TALENT_PROFILE* integration that were executed and whether or not they were successful.

### **1.3.3:**	Explore ICS Monitoring Console - Logfiles

---

**1.3.3.1** In order to see the details of the payload that passed through the ICS integration, you need to download the Activity Stream Log from the `Download Logs` link on the right of the Activity Stream.

**1.3.3.2** Select the `Download Activity Stream` link and then save the zipfile to a location on your workstation such as *C:\temp* (Windows path)

![](images/100/image019.png)
![](images/100/image020.png)

**1.3.3.3** A downloading informational message will be shown with a blue background at the top of the page.  You can dismiss it by selecting the "X" at the right of the message bar.

![](images/100/image020a.png)

**1.3.3.4** Extract the zipfile and you’ll see that there are 2 directories of logfiles – this is because the ICS instance is running on a cluster of 2 servers for high availability.

![](images/100/image021.png)

**1.3.3.5** Navigate into one of the server directories and examine the `ics-flow.log` file in your favorite text editor.

**1.3.3.6** Here is a view of the end of the *ics-flow.log* file in the *Notepad++* text editor showing the response given by addTalentProfileData of the payload after a successful execution of the SOAP API call:

![](images/100/image022.png)

**1.3.3.7** This logfile is helpful for investigation during development or runtime analysis.  The capture of the runtime payloads can be turned on or off during activation of the ICS integration where you are prompted whether or not you want to save the payloads.

### **1.3.4:**	Explore ICS Monitoring Console - Integrations

---

**1.3.4.1** Back in the ICS Monitoring console, select `Integrations` from the left-hand navigation.

**1.3.4.2** Note that all the statistics of the _ICSHCM Add Talent Profile UserXX_ are shown.

![](images/100/image023.png)


### **1.3.5:**	Explore ICS Monitoring Console - Tracking

---

**1.3.5.1** Select the `Tracking` link in the navigation bar on the left

![](images/100/image030.png)

**1.3.5.2** The ICS `Tracking` monitor page shows all integration flows that have been executed.

**1.3.5.3** Select the chevron just to the right of the *Tracking* label at the top of the page to change the granularity of the Tracking report to `Last 6 Hours`

![](images/100/image031.png)

**1.3.5.4** Next, drill into a `COMPLETED` integration flow by selecting the integration name.

![](images/100/image032.png)

**1.3.5.5** We can now see that all steps in the this ICS integration flow were successful because the arrow is green highlighting all the orchestration flow steps.

![](images/100/image033.png)

**1.3.5.6** Select the `Close` button to go back to the ICS monitoring page.

![](images/100/image034.png)

**1.3.5.7** We are now done exploring the ICS monitoring features.

You now have used Oracle Integration Cloud Service to explore an integration to HCM Cloud by taking in external data feeds, correctly formatting it for HCM Cloud.

This ICS Overview Lab is now completed.
