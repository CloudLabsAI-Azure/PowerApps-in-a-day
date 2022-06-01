# Power Platform

# App in a Day

Module 4 : Power Automate

### Hands-on Lab Step-by-Step

```
April 2022
```

## Contents

- Power Automate
   - Lab Prerequisites
   - Exercise 1: Create Approval Request Flow
   - Exercise 2: Conditional Logic
   - Exercise 3: Test the cloud flow
   - Exercise 4: Update the Flow
   - Exercise 4: (Optional) Add a Teams Notification
- References
- Copyright


**1 |** P a g e ©20 22 Microsoft Corporation

## Power Automate

### Lab Prerequisites

This is the fourth lab in a five-part series covering Power Apps, Microsoft Dataverse, and Power Automate. The assumption
is that you have successfully completed the first three modules, or at least the initial part of setting up an environment as
described in the overview – “ **00 - AppInADay Lab Overview.pdf** ”.

If you have not completed the previous modules, you can use the partially completed version of the lab package in the
“\Completed\Module 3 ” folder. Follow the instructions in the document “Importing Module 3 Completed” before
proceeding with this module, which will provision the app and the Microsoft Dataverse Table into your environment.

### Integrating a Power Apps App with Power Automate

In this lab, you will create a flow that uses the Modern Approvals service to automate the approval workflow – it will send
an email to the selected approver and take an action based on their response.

You should already have an app with these two screens:


©20 20 Microsoft Corporation 2 | P a g e

### Exercise 1: Create Approval Request Flow

The flow will trigger when a new item is added to the **Device Order** Table in the Microsoft Dataverse.

- It will use the Approvals Service to send an approval request.
- The approver will receive an email with options to Approve or Rejects and add comments.
- Once the approver responds, the record in the Device Order table will be updated with the appropriate approval
    status and comments.
- An email will be sent to the requester informing them whether the device was approved or rejected.

```
There are two ways to create a flow – from blank or from a template. In this lab, we will create the approval flow
starting with a blank flow.
```
Task 1 : Login on Power Apps website and create a flow

1. Navigate to [Make Power Apps](https://make.powerapps.com/) and make sure you are in the correct environment.
2. Select **Flows**.
3. Click **New** and select **Automated – cloud flow**.


**3 |** P a g e ©20 22 Microsoft Corporation

Task 2 : Configure the trigger

The first thing you will need to configure is the trigger, i.e. when should this flow run. A flow can be triggered:

```
a. manually from a Power Apps app,
b. manually from a flow button,
c. on a fixed schedule, or
d. when an event occurs, such as a new item being added to a table, a new email arriving in a user’s inbox, a
new tweet being posted that meets certain conditions, etc.
```
In this scenario, we will configure the flow to trigger when a **new item is added** to the **Device Order Table** table in the
**Microsoft Dataverse**

1. **Enter a name** for your flow, such as – “New device approval request”
2. In the **Choose your flow’s trigger** box, search for when a row is added and select **When a row is added**
    **modified, or deleted**.


©20 20 Microsoft Corporation 4 | P a g e

3. Click **Create**.
4. Select **Added** for Change type
5. Click the **Table Name** drop-down and select **Device Orders**. You can type “device orders” to search for it.
6. Click the **Scope** drop-down and select **Organization**. Scope allows you to limit when your flow will run, for
    example you could choose User and it would only run for orders you create. In this case you are choosing
    organization because you want this flow to run for records created by anyone in your entire organization.

Task 3 : Add action to send an approval request

1. Click **+ New step**.


**5 |** P a g e ©20 22 Microsoft Corporation

2. Search for **Approvals** and select **Start and wait for an approval**.

_This will use the modern approval service. For more information see the blog post at Flow Modern Approvals._

3. In the **Approval type** dropdown select **Approve/Reject - First to Respond**.
4. For the Title, we will add some text and one variable. This variable will contain the Device Name of the device
    order request. Enter **_New device request for_** in the **Title** text box.


©20 20 Microsoft Corporation 6 | P a g e

5. Select **Device Name** for the **Dynamic content.**

**_Note_** _: if the Dynamic content box is not visible, click the Add dynamic content button -_

6. Select the **Assigned to** field, select click **Approver**. Click on the **Add dynamic content** button to show/hide the
    dynamic content pane.

You might get a warning message about this field being optional. Ignore it and ignore similar warnings in future.

**_Note_** _: Recall from the earlier lab that this will be the approver’s email address_.


**7 |** P a g e ©20 22 Microsoft Corporation

7. Click **Show Advanced Options**.
8. Select the **Requestor** field and select **Requested By**
9. In the **Details** field, type **_A new device has been requested_** and hit <Enter>.


©20 20 Microsoft Corporation 8 | P a g e

10. Select **Device Name** from the Dynamic content pane.
11. Type **_, $_** and select **Price.** You may need to click the **"See More"** option under the dynamic content search bar in
    order to see the Price option.
12. Hit Enter and type **_Department Contribution: $_**
13. Select **Department Contribution**.


**9 |** P a g e ©20 22 Microsoft Corporation

14. Hit Enter, type **_Comments:_** and select **Comments**.
15. Your **Flow** will now look like the image below.
**16. Save** your flow


©20 20 Microsoft Corporation 10 | P a g e

**_Note_** _: When creating your own approval flows, you may additionally include a clickable link that will be displayed in the
approval email. In this scenario, for example, you could include a link to view device details in an online catalogue. You
would include the_ **_Item link_** _and_ **_Item link description_**_._

**_Note_** _: You could also set the_ **_Item link_** _to deep link into a Power Apps app to view more details about the request. In this
scenario, you might pass an OrderID or a DeviceID as a URL parameter. Power Apps accepts URL parameters, see [Flow URL
Parameters](https://powerapps.microsoft.com/tutorials/function-param/) for more details._

### Exercise 2: Conditional Logic

In flow, you can add conditions to take different actions depending on a certain result, in this case, whether the request
was approved or rejected.

Task 1: Add conditional logic to flow

1. Click **+ New step**.
2. Search for **Condition** and select it.


**11 |** P a g e ©20 22 Microsoft Corporation

3. Click in the left edit box that says, “Choose a value” and select **Outcome** from the dynamic content pane. You may
    need to press the “+” icon below the edit box to hide the dynamic content pane.
4. Select **is equal to** for condition and type **Approve** for **Value**.

Task 2: Add conditional logic to flow

We will now configure what actions to perform if the response is approved or not – YES branch vs. NO branch.

We will add two actions:

```
a. Update the record in the Device Order table
b. Send an email to the employee who requested the device
```
1. In the left **If yes** box, click **Add an action**


©20 20 Microsoft Corporation 12 | P a g e

2. Search for **Update a Row** and select **Update a Row Microsoft Dataverse**
3. Select **Device Orders** for **Table Name**.
4. Click on the **Row ID** and select Device Order from the Dynamic content pane.

This is the unique lookup ID for the record (or row) that was created.

5. Click **Show advanced options**.
6. Select **Approve** from the **Approval Status** drop-down.


**13 |** P a g e ©20 22 Microsoft Corporation

7. Select the **Approved Date** field and select the **Expression** tab.
8. Type **utcNow()** and click **OK**.
9. Save the flow.

Task 3: Add another action

You will now add the send email action to the If Yes branch.

1. From within the yes branch, Click **Add an Action**.
1. Search for **send email** and select **Send an email (V2) – Office 365 Outlook**.
2. Click **Sign in** if prompted.


©20 20 Microsoft Corporation 14 | P a g e

3. Click **Accept**.
4. Click on the **To** field and click **Switch to Advanced Mode**.
5. Select **Requested By** for **To.** Select from under the **When a record is added** action.
6. Type **_Your device order has been approved!_** for **Subject**.


**15 |** P a g e ©20 22 Microsoft Corporation

7. Click on the **Code View** button.
8. Set the **Body** value as shown below:

```
Select Device Name and Estimated Ship Date from the When a record is added action.
```
**_Note_** _: If you do not have an Office 365 mailbox setup, you can use one of the other connectors to send the email, such as
Outlook.com, Gmail or SendGrid._

9. Click **Save**.


©20 20 Microsoft Corporation 16 | P a g e

### Exercise 3: Test the cloud flow

To test the flow, you will:

```
a. Run the Device Ordering app and submit an approval request
b. Verify the request was sent to the approver
c. Approve the request
d. Verify that the Microsoft Dataverse record was updated, and an email was sent back to the requestor
```
Task 1: Test the cloud flow

**Note** : When a new device record is added to the Device Order Table in Microsoft Dataverse, it may take up to ten minutes
for the flow to trigger. To ensure the flow runs immediately, select the **Test** option in the top right and select the
**“Manually”** option. Then go ahead and submit a device request. The flow should run immediately.

Note: You may see a warning in the Flow checker that the Power Automate Approvals has not been installed for your
environment. Run the flow to initiate provisioning the Power Automate Approvals.

1. Select **Manually** and click **Test.**
2. To submit a device request, go to [Make Power Apps](http://make.powerapps.com/)
3. Select **Apps** and start the **Device Ordering App.**


**17 |** P a g e ©20 22 Microsoft Corporation

4. Select a few devices and click Compare.
5. Select one of the devices, provide email for Approver.


©20 20 Microsoft Corporation 18 | P a g e

6. Provide a comment and click Submit device request.
7. Click **OK**.
8. The flow will run and send email to the manager email you provided. The request for approval email will look like
    the image below; it will include **Device information** , **Price** , **Department Contribution (the calculated field),** and
    the **Requester Comment**.

```
REMINDER : If the flow does not run immediately, please wait, it may take up to ten minutes for the flow to be
triggered. To ensure the flow runs immediately, see note above - select the Test option in the top right and select
the “I’ll perform the trigger action” option. Then go ahead and submit a device request. The flow should run
immediately. The email, however, may take a few minutes to appear regardless of when the flow starts.
```
9. Click **Approve**.
10. Add a comment and click **Submit**.


**19 |** P a g e ©20 22 Microsoft Corporation

11. The flow will continue to run; it will update the row and send an email to the requestor. The email sent to the
    requester will look like the image below.
12. Check the flow, you will notice that the flow is now marked as **Succeeded** in the run history.


©20 20 Microsoft Corporation 20 | P a g e


**21 |** P a g e ©20 22 Microsoft Corporation

### Exercise 4: Update the Flow

In this exercise, you will add two actions to the “if no” branch.

Task 1: Add actions

1. If you don’t already have the flow open, open it in edit mode.
2. In the If no branch, click **Add an action**.
10. Search for **Update a Row** and select **Update a Row (Dataverse)**


©20 20 Microsoft Corporation 22 | P a g e

3. Select **Device Orders** for **Table Name** , select **Device Order** for **Item ID** , and click **Show advanced options**
4. Select **Reject** for **Approval Status**.
5. Click **Add an action**.
6. Search for **_send email_** and select **Send an email (v2) - Office 365 Outlook**.


**23 |** P a g e ©20 22 Microsoft Corporation

7. Provide the information shown on the image below. This will send an email to the requestor informing them that
    their device request was not approved. Select **Requested By** and **Device Name** from under the **When a record is**
    **added** header.
8. **Save** the flow.

Task 2: Test the updated Flow

1. Click **Test** in the top right of the flow editor and start the Flow.
2. Run the Device Ordering app -> Select a device and submit an approval request.
3. You should receive an email with options to Approve or Reject the request. Select **Reject** this time and enter some
    comments, such as “Not eligible for new device.” Click **Submit**.
4. Confirm that the requestor receives an email informing them that their device approval request was rejected.


©20 20 Microsoft Corporation 24 | P a g e

5. Navigate to [Make Power Apps](https://make.powerapps.com/) select **Apps** and start the **Device Procurement** application.
6. Device Orders will now have the Approval Status.

Task 3: Visit the approval center

1. Use the Device Ordering app to **submit a few more approval requests**.
2. Navigate to [Power Automate](https://flow.microsoft.com/) and make sure you are in the correct environment. Login with your lab credentials if
    prompted.
3. Expand **Action items** and select **Approvals**.


**25 |** P a g e ©20 22 Microsoft Corporation

4. Notice that all pending approval requests are visible.
5. Go ahead and approve or reject a request from this screen. The details are displayed in the right pane where you
    can **enter comments** and **Confirm**.
6. The request will no longer be visible as it has been processed.


©20 20 Microsoft Corporation 26 | P a g e

**_Note_** _: All approval requests sent to the current logged on user will be visible in the Approvals Center. This includes approvals
sent from any app or flow._

7. You can also use the Approvals Center to view all requests that you have sent and are **Awaiting response** from
    the approver. Select the **Sent requests** tab at the top to view all requests that you have sent.
8. Open the **Power Automate mobile app** on your mobile device.
9. Login and switch to the environment where the flow is deployed.
10. Select **Approvals** in the top right and view all pending approvals.
11. You can quickly approve or reject these pending requests from this screen.
12. If you have push notifications turned on and are signed into the flow mobile app – when you receive a new
    Approval request it will trigger a push notification on your phone. You can give this a shot.


**27 |** P a g e ©20 22 Microsoft Corporation

Congratulations! You have successfully completed this lab. You have created your Power Apps app and flow and
connected them to a Microsoft Dataverse Table. Now you are ready to build your own apps and workflows.

### Exercise 4: (Optional) Add a Teams Notification

In this optional exercise, you will modify the existing flow to include a Teams notification for your approval flow.

Task 1 : Modify the Flow

1. Click to expand the **Send an email** step inside the **If yes** branch.
2. Click **Add an action**.


©20 20 Microsoft Corporation 28 | P a g e

3. Search for Flow bot and select **Post a message in a chat or channel**
4. Select **Flow bot** for Post as and **Chat with Flow Bot** for Post in.


**29 |** P a g e ©20 22 Microsoft Corporation

5. Insert **Requested By** in the Recipient field.
6. In the **Message** input, type **_Your device has been approved_** and then select **Device Name** from under the
    Dynamics Content **When a Record is added** header.
7. Type **Estimated Ship Date:** and then select **Estimated Ship Date** from under the Dynamics Content **When a**
    **record is created** header.


©20 20 Microsoft Corporation 30 | P a g e

8. Click on the **... Menu** button of the **Post a message** step and select **Copy to my clipboard**.
9. Go to the **If no** branch and click **Add an action**.
10. Select **My clipboard**.


**31 |** P a g e ©20 22 Microsoft Corporation

11. Select the step you copied.
12. Click to expand the step you just pasted.
13. Delete the current Message content and change the Message to **Your device request for**
14. Place your cursor at the end of the text and select **Device Name** from the dynamic content pane. Add **was not**
    **approved** to the end of the content. The step should now look like the image below.
15. Click **Save** to save your changes.

Task 2 : Test your modified flow

Now that the flow has been modified, you are ready to test it.

1. Click **Test** in the top right of the flow editor and select **Manually**
2. In another tab, navigate to [Microsoft Teams](https://teams.microsoft.com/).
3. Open a third tab and run the Device Ordering app -> Select a device and submit an approval request.
4. You should receive an email with options to Approve or Reject the request. Select **Approve**.
5. Shortly after hitting submit, you should see a message and a notification in the Chat tab on your app bar –
    this is from the Flow Bot. Click to open the chat. Wait a moment if it does not appear immediately.
6. You should see the approval of the request.


©20 20 Microsoft Corporation 32 | P a g e

## References

App in a Day introduces some of the key functionalities available in Power Apps, Power Automate, Power BI and the
Microsoft Dataverse. For an up to date list of learning references, see [Power Apps Resources](http://aka.ms/powerapps-resources) and [Power Automate
Resources](https://flow.microsoft.com/blog/power-automate-learning-resources/).


**33 |** P a g e ©20 22 Microsoft Corporation

## Copyright

**© 2022 Microsoft Corporation. All rights reserved.**

By using this demo/lab, you agree to the following terms:

The technology/functionality described in this demo/lab is provided by Microsoft Corporation for purposes of obtaining
your feedback and to provide you with a learning experience. You may only use the demo/lab to evaluate such technology
features and functionality and provide feedback to Microsoft. You may not use it for any other purpose. You may not
modify, copy, distribute, transmit, display, perform, reproduce, publish, license, create derivative works from, transfer, or
sell this demo/lab or any portion thereof.

COPYING OR REPRODUCTION OF THE DEMO/LAB (OR ANY PORTION OF IT) TO ANY OTHER SERVER OR
LOCATION FOR FURTHER REPRODUCTION OR REDISTRIBUTION IS EXPRESSLY PROHIBITED.

THIS DEMO/LAB PROVIDES CERTAIN SOFTWARE TECHNOLOGY/PRODUCT FEATURES AND FUNCTIONALITY,
INCLUDING POTENTIAL NEW FEATURES AND CONCEPTS, IN A SIMULATED ENVIRONMENT WITHOUT
COMPLEX SET-UP OR INSTALLATION FOR THE PURPOSE DESCRIBED ABOVE. THE TECHNOLOGY/CONCEPTS
REPRESENTED IN THIS DEMO/LAB MAY NOT REPRESENT FULL FEATURE FUNCTIONALITY AND MAY NOT
WORK THE WAY A FINAL VERSION MAY WORK. WE ALSO MAY NOT RELEASE A FINAL VERSION OF SUCH
FEATURES OR CONCEPTS. YOUR EXPERIENCE WITH USING SUCH FEATURES AND FUNCTIONALITY IN A
PHYSICAL ENVIRONMENT MAY ALSO BE DIFFERENT.

FEEDBACK. If you give feedback about the technology features, functionality and/or concepts described in this demo/lab
to Microsoft, you give to Microsoft, without charge, the right to use, share and commercialize your feedback in any way
and for any purpose. You also give to third parties, without charge, any patent rights needed for their products,
technologies and services to use or interface with any specific parts of a Microsoft software or service that includes the
feedback. You will not give feedback that is subject to a license that requires Microsoft to license its software or
documentation to third parties because we include your feedback in them. These rights survive this agreement.

MICROSOFT CORPORATION HEREBY DISCLAIMS ALL WARRANTIES AND CONDITIONS WITH REGARD TO THE
DEMO/LAB, INCLUDING ALL WARRANTIES AND CONDITIONS OF MERCHANTABILITY, WHETHER EXPRESS,
IMPLIED OR STATUTORY, FITNESS FOR A PARTICULAR PURPOSE, TITLE AND NON-INFRINGEMENT.
MICROSOFT DOES NOT MAKE ANY ASSURANCES OR REPRESENTATIONS WITH REGARD TO THE ACCURACY
OF THE RESULTS, OUTPUT THAT DERIVES FROM USE OF DEMO/ LAB, OR SUITABILITY OF THE INFORMATION
CONTAINED IN THE DEMO/LAB FOR ANY PURPOSE.

DISCLAIMER

This demo/lab contains only a portion of new features and enhancements in Microsoft Power Apps. Some of the features
might change in future releases of the product. In this demo/lab, you will learn about some, but not all, new features.

