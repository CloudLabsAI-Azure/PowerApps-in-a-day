# Power Platform

# App in a Day

Module 4 : Power Automate

### Hands-on Lab Step-by-Step

## Contents

- Power Automate
   - Lab Prerequisites
   - Exercise 1: Create Approval Request Flow
   - Exercise 2: Conditional Logic
   - Exercise 3: Test the cloud flow
   - Exercise 4: Update the Flow
   - Exercise 4: (Optional) Add a Teams Notification
- References

## Power Automate

### Lab Prerequisites

This is the fourth lab in a five-part series covering Power Apps, Microsoft Dataverse, and Power Automate. The assumption
is that you have successfully completed the first three modules, or at least the initial part of setting up an environment as
described in the overview **(Page 1 of lab guide)**.

If you have not completed the previous modules, you can use the partially completed version of the lab package in the
**C:\PowerApps-in-a-day\Completed\Module 3** folder. Follow the instructions in the document **Importing Module 3 Completed** before
proceeding with this module, which will provision the app and the Microsoft Dataverse Table into your environment.

### Integrating a Power Apps App with Power Automate

In this lab, you will create a flow that uses the Modern Approvals service to automate the approval workflow – it will send
an email to the selected approver and take an action based on their response.

You should already have an app with these two screens:

![](./images/Module4/Device_ordering_app.png)

## Exercise 1: Create Approval Request Flow

The flow will trigger when a new item is added to the **Device Order** Table in the Microsoft Dataverse.

- It will use the Approvals Service to send an approval request.
- The approver will receive an email with options to Approve or Rejects and add comments.
- Once the approver responds, the record in the Device Order table will be updated with the appropriate approval
    status and comments.
- An email will be sent to the requester informing them whether the device was approved or rejected.

   > There are two ways to create a flow – from blank or from a template. In this lab, we will create the approval flow
starting with a blank flow.

### Task 1 : Login on Power Apps website and create a flow

1. Navigate to Make Power Apps Portal and make sure you are in the correct environment.

   ![](./images/Module4/PowerApps-flow1.png)
   
1. Select **Flows**.

   ![](./images/Module4/PowerApps-flow2.png)
   
1. Click **New** and select **Automated – cloud flow**.

   ![](./images/Module4/PowerApps-flow3.png)


### Task 2 : Configure the trigger

The first thing you will need to configure is the trigger, i.e. when should this flow run. A flow can be triggered:

   1. manually from a Power Apps app,
   1. manually from a flow button,
   1. on a fixed schedule, or
   1. when an event occurs, such as a new item being added to a table, a new email arriving in a user’s inbox, a
new tweet being posted that meets certain conditions, etc.


In this scenario, we will configure the flow to trigger when a **new item is added** to the **Device Order Table** table in the
**Microsoft Dataverse**

1. Enter the below name for your flow.
 
   ```
   New device approval request
   ```
   
   ![](./images/Module4/PowerApps-flow4.png)

1. In the **Choose your flow’s trigger** box, search for when a row is added and select **When a row is added**
    **modified, or deleted**.
    
   ![](./images/Module4/PowerApps-flow5.png)

1. Click **Create**.
1. Select **Added** for Change type.

   ![](./images/Module4/PowerApps-flow6.png)
   
1. Click the **Table Name** drop-down and select **Device Orders**. You can type “device orders” to search for it.
   
1. Click the **Scope** drop-down and select **Organization**. Scope allows you to limit when your flow will run, for
    example you could choose User and it would only run for orders you create. In this case you are choosing
    organization because you want this flow to run for records created by anyone in your entire organization.
  
   ![](./images/Module4/PowerApps-flow7.png)
   
### Task 3 : Add action to send an approval request


1. Click **+ New step**.

   ![](./images/Module4/PowerApps-flow8.png)
   
1. Search for **Approvals** and select **Start and wait for an approval**.

   ![](./images/Module4/PowerApps-flow9.png)

   > This will use the modern approval service. For more information see the blog post at Flow Modern Approvals by navigating to this URL `https://flow.microsoft.com/blog/introducing-modern-approvals/`

1. In the **Approval type** dropdown select **Approve/Reject - First to Respond**.

   ![](./images/Module4/PowerApps-flow10.png)
   
1. For the Title, we will add some text and one variable. This variable will contain the Device Name of the device
    order request. Enter **_New device request for_** in the **Title** text box.

   ![](./images/Module4/PowerApps-flow11.png)

1. Select **Device Name** for the **Dynamic content.**

   ![](./images/Module4/PowerApps-flow12.png)
   
   > **_Note_** _: if the Dynamic content box is not visible, click the Add dynamic content button - ![](./images/Maodule4/PowerApps-flow13.png)

1. Select the **Assigned to** field, select click **Approver**. Click on the **Add dynamic content** button to show/hide the
    dynamic content pane.

   ![](./images/Module4/PowerApps-flow14.png)
   
     - You might get a warning message about this field being optional. Ignore it and ignore similar warnings in future.

     > **_Note_** _: Recall from the earlier lab that this will be the approver’s email address_.

1. Click **Show Advanced Options**.

   ![](./images/Module4/PowerApps-flow15.png)
   
1. Select the **Requestor** field and select **Requested By**.

   ![](./images/Module4/PowerApps-flow16.png)
   
1. In the **Details** field, type **_A new device has been requested_** and hit <Enter>.

   ![](./images/Module4/PowerApps-flow17.png)
   
1. Select **Device Name** from the Dynamic content pane.
   
   ![](./images/Module4/PowerApps-flow18.png)
   
1. Type **_, $_** and select **Price.** You may need to click the **"See More"** option under the dynamic content search bar in
    order to see the Price option.
   
   ![](./images/Module4/PowerApps-flow19.png)
   
1. Hit Enter and type **_Department Contribution: $_** .
   
1. Select **Department Contribution**.

   ![](./images/Module4/PowerApps-flow20.png)

1. Hit Enter, type **_Comments:_** and select **Comments**.
 
   ![](./images/Module4/PowerApps-flow21.png)
   
1. Your **Flow** will now look like the image below.
   
   ![](./images/Module4/PowerApps-flow22.png)
   
1. **Save** your flow.


> **_Note_** _: When creating your own approval flows, you may additionally include a clickable link that will be displayed in the
approval email. In this scenario, for example, you could include a link to view device details in an online catalogue. You
would include the_ **_Item link_** _and_ **_Item link description_**_._

> **_Note_** _: You could also set the_ **_Item link_** _to deep link into a Power Apps app to view more details about the request. In this
scenario, you might pass an OrderID or a DeviceID as a URL parameter. Power Apps accepts URL parameters, you can find more details about Flow 
Parameters Here: `https://powerapps.microsoft.com/tutorials/function-param/`

   
## Exercise 2: Conditional Logic

In flow, you can add conditions to take different actions depending on a certain result, in this case, whether the request
was approved or rejected.

### Task 1: Add conditional logic to flow

1. Click **+ New step**.
   
    ![](./images/Module4/PowerApps-flow23.png)  
   
1. Search for **Condition** and select it.
   
    ![](./images/Module4/PowerApps-flow24.png)  

1. Click in the left edit box that says, “Choose a value” and select **Outcome** from the dynamic content pane. You may
    need to press the “+” icon below the edit box to hide the dynamic content pane.
   
       ![](./images/Module4/PowerApps-flow25.png)  

4. Select **is equal to** for condition and type **Approve** for **Value**.

    ![](./images/Module4/PowerApps-flow26.png)  

   
### Task 2: Add conditional logic to flow

We will now configure what actions to perform if the response is approved or not – YES branch vs. NO branch.

We will add two actions:

   1. Update the record in the Device Order table
   1. Send an email to the employee who requested the device

   
1. In the left **If yes** box, click **Add an action**.

   ![](./images/Module4/PowerApps-flow27.png)  

1. Search for **Update a Row** and select **Update a Row Microsoft Dataverse**.
   
    ![](./images/Module4/PowerApps-flow28.png)  
   
1. Select **Device Orders** for **Table Name**.
   
1. Click on the **Row ID** and select Device Order from the Dynamic content pane.

    ![](./images/Module4/PowerApps-flow29.png)  

   > This is the unique lookup ID for the record (or row) that was created.

1. Click **Show advanced options**.
   
1. Select **Approve** from the **Approval Status** drop-down.

   ![](./images/Module4/PowerApps-flow30.png)  

1. Select the **Approved Date** field and select the **Expression** tab.
   
   ![](./images/Module4/PowerApps-flow31.png)  
   
1. Type **utcNow()** and click **OK**.
   
    ![](./images/Module4/PowerApps-flow32.png)  

1. **Save** the flow.

### Task 3: Add another action

You will now add the send email action to the If Yes branch.

1. From within the yes branch, Click **Add an Action**.
   
   ![](./images/Module4/PowerApps-flow33.png)  

1. Search for **send email** and select **Send an email (V2) – Office 365 Outlook**.
   
    ![](./images/Module4/PowerApps-flow34.png)  
   
1. Click **Sign in** if prompted.

    ![](./images/Module4/PowerApps-flow35.png)  

1. Click **Accept**.
   
    ![](./images/Module4/PowerApps-flow36.png)  
  
4. Click on the **To** field and click **Switch to Advanced Mode**.
   
    ![](./images/Module4/PowerApps-flow37.png)  
   
1. Select **Requested By** for **To.** Select from under the **When a record is added** action.
   
    ![](./images/Module4/PowerApps-flow38.png)  
   
1. Type **_Your device order has been approved!_** for **Subject**.

1. Click on the **Code View** button.
   
   ![](./images/Module4/PowerApps-flow39.png)  
   
8. Set the **Body** value as shown below:

    ```
    Select Device Name and Estimated Ship Date from the When a record is added action.
    ```
   
   ![](./images/Module4/PowerApps-flow40.png)  
   
   > **_Note_** _: If you do not have an Office 365 mailbox setup, you can use one of the other connectors to send the email, such as
Outlook.com, Gmail or SendGrid._

9. Click **Save**.


### Exercise 3: Test the cloud flow

To test the flow, you will:

  1. Run the Device Ordering app and submit an approval request
  1. Verify the request was sent to the approver
  1. Approve the request
  1. Verify that the Microsoft Dataverse record was updated, and an email was sent back to the requestor

### Task 1: Test the cloud flow

**Note** : When a new device record is added to the Device Order Table in Microsoft Dataverse, it may take up to ten minutes
for the flow to trigger. To ensure the flow runs immediately, select the **Test** option in the top right and select the
**“Manually”** option. Then go ahead and submit a device request. The flow should run immediately.

Note: You may see a warning in the Flow checker that the Power Automate Approvals has not been installed for your
environment. Run the flow to initiate provisioning the Power Automate Approvals.

   ![](./images/Module4/PowerApps-testflow1.png)  

1. Select **Manually** and click **Test.**
   
   ![](./images/Module4/PowerApps-testflow2.png)  
   
1. To submit a device request, navigate to Power Apps Portal by using this URL `http://make.powerapps.com/`.
   
1. Select **Apps** and start the **Device Ordering App** by clicking on **Play** button.

   ![](./images/Module4/PowerApps-testflow3.png)  
   
1. Select a few devices and click Compare.
   
   ![](./images/Module4/PowerApps-testflow4.png)  
   
1. Select one of the devices, provide email for Approver.

   ![](./images/Module4/PowerApps-testflow5.png)  

1. Provide a comment and click Submit device request.
   
   ![](./images/Module4/PowerApps-testflow6.png)  
   
1. Click **OK**.
1. The flow will run and send email to the manager email you provided. The request for approval email will look like
    the image below; it will include **Device information** , **Price** , **Department Contribution (the calculated field),** and
    the **Requester Comment**.

   > REMINDER : If the flow does not run immediately, please wait, it may take up to ten minutes for the flow to be
triggered. To ensure the flow runs immediately, see note above - select the Test option in the top right and select
the “I’ll perform the trigger action” option. Then go ahead and submit a device request. The flow should run
immediately. The email, however, may take a few minutes to appear regardless of when the flow starts.

      ![](./images/Module4/PowerApps-testflow7.png)  

1. Click **Approve**.
   
1. Add a comment and click **Submit**.

   ![](./images/Module4/PowerApps-testflow8.png)  

1. The flow will continue to run; it will update the row and send an email to the requestor. The email sent to the
    requester will look like the image below.
   
   ![](./images/Module4/PowerApps-testflow9.png)  
   
1. Check the flow, you will notice that the flow is now marked as **Succeeded** in the run history.

   ![](./images/Module4/PowerApps-testflow10.png)  

   
## Exercise 4: Update the Flow

In this exercise, you will add two actions to the “if no” branch.

### Task 1: Add actions

1. If you don’t already have the flow open, open it in edit mode by clicking on **Edit button**.
   
    ![](./images/Module4/PowerApps-flow41.png)  
   
1. In the If no branch, click **Add an action**.
   
    ![](./images/Module4/PowerApps-flow42.png)  
   
1. Search for **Update a Row** and select **Update a Row (Dataverse)**

    ![](./images/Module4/PowerApps-flow43.png)  
   
1. Select **Device Orders** for **Table Name** , select **Device Order** for **Item ID** , and click **Show advanced options**.
   
    ![](./images/Module4/PowerApps-flow44.png)  
   
1. Select **Reject** for **Approval Status**.
 
    ![](./images/Module4/PowerApps-flow45.png)  
   
1. Click **Add an action**.
   
1. Search for **_send email_** and select **Send an email (v2) - Office 365 Outlook**.

    ![](./images/Module4/PowerApps-flow46.png)  

7. Provide the information shown on the image below. This will send an email to the requestor informing them that
    their device request was not approved. Select **Requested By** and **Device Name** from under the **When a record is**
    **added** header.
   
    ![](./images/Module4/PowerApps-flow47.png)  
   
8. **Save** the flow.

### Task 2: Test the updated Flow

1. Click **Test** in the top right of the flow editor and start the Flow.
   
1. Run the Device Ordering app -> Select a device and submit an approval request.
   
1. You should receive an email with options to Approve or Reject the request. Select **Reject** this time and enter some
    comments, such as “Not eligible for new device.” Click **Submit**.
   
    ![](./images/Module4/PowerApps-flow48.png)  
   
1. Confirm that the requestor receives an email informing them that their device approval request was rejected.

    ![](./images/Module4/PowerApps-flow49.png)  

1. Navigate to [Make Power Apps](https://make.powerapps.com/) select **Apps** and start the **Device Procurement** application.

    ![](./images/Module4/PowerApps-flow50.png)  
   
1. Device Orders will now have the Approval Status.

    ![](./images/Module4/PowerApps-flow51.png)  
   
### Task 3: Visit the approval center

1. Use the Device Ordering app to **submit a few more approval requests**.
   
1. Navigate to Power Automate using the below URL and make sure you are in the correct environment. Login with your lab credentials if
    prompted.
   
   ```
   https://flow.microsoft.com/
   ```
   
1. Expand **Action items** and select **Approvals**.

   ![](./images/Module4/PowerApps-approvalcenter1.png)  
   
1. Notice that all pending approval requests are visible.
   
   ![](./images/Module4/PowerApps-approvalcenter2.png)  
   
1. Go ahead and approve or reject a request from this screen. The details are displayed in the right pane where you
    can **enter comments** and **Confirm**.
   
   ![](./images/Module4/PowerApps-approvalcenter3.png)  
   
1. The request will no longer be visible as it has been processed.

   > **_Note_** _: All approval requests sent to the current logged on user will be visible in the Approvals Center. This includes approvals
sent from any app or flow._

1. You can also use the Approvals Center to view all requests that you have sent and are **Awaiting response** from
    the approver. Select the **Sent requests** tab at the top to view all requests that you have sent.
   
1. Open the **Power Automate mobile app** on your mobile device.
   
1. Login and switch to the environment where the flow is deployed.
   
   ![](./images/Module4/PowerApps-approvalcenter4.png)  
   
1. Select **Approvals** in the top right and view all pending approvals.
   
   ![](./images/Module4/PowerApps-approvalcenter5.png)   
   
1. You can quickly approve or reject these pending requests from this screen.
   
   ![](./images/Module4/PowerApps-approvalcenter6.png)   
   
1. If you have push notifications turned on and are signed into the flow mobile app – when you receive a new
    Approval request it will trigger a push notification on your phone. You can give this a shot.

   Congratulations! You have successfully completed this lab. You have created your Power Apps app and flow and
connected them to a Microsoft Dataverse Table. Now you are ready to build your own apps and workflows.

## Exercise 4: (Optional) Add a Teams Notification

In this optional exercise, you will modify the existing flow to include a Teams notification for your approval flow.

### Task 1 : Modify the Flow

1. Click to expand the **Send an email** step inside the **If yes** branch.
   
   ![](./images/Module4/PowerApps-updateflow1.png)  
   
1. Click **Add an action**.

   ![](./images/Module4/PowerApps-updateflow2.png)     
   
1. Search for Flow bot and select **Post a message in a chat or channel**.
   
   ![](./images/Module4/PowerApps-updateflow3.png)  
   
1. Select **Flow bot** for Post as and **Chat with Flow Bot** for Post in.

   ![](./images/Module4/PowerApps-updateflow4.png)  

1. Insert **Requested By** in the Recipient field.
   
   ![](./images/Module4/PowerApps-updateflow5.png)   
   
1. In the **Message** input, type **_Your device has been approved_** and then select **Device Name** from under the
    Dynamics Content **When a Record is added** header.
   
   ![](./images/Module4/PowerApps-updateflow6.png)  
   
1. Type **Estimated Ship Date:** and then select **Estimated Ship Date** from under the Dynamics Content **When a**
    **record is created** header.
   ![](images/Module4/PowerApps-updateflow6.1.png)  

1. Click on the **... Menu** button of the **Post a message** step and select **Copy to my clipboard**.
   
   ![](./images/Module4/PowerApps-updateflow7.png)
   
1. Go to the **If no** branch and click **Add an action**.
   
   ![](./images/Module4/PowerApps-updateflow8.png)    
   
1. Select **My clipboard**.

   ![](./images/Module4/PowerApps-updateflow9.png)  

1. Select the step you copied.
   
   ![](./images/Module4/PowerApps-updateflow10.png)    
   
1. Click to expand the step you just pasted.
1. Delete the current Message content and change the Message to **Your device request for**
1. Place your cursor at the end of the text and select **Device Name** from the dynamic content pane. Add **was not**
    **approved** to the end of the content. The step should now look like the image below.
   
   ![](./images/Module4/PowerApps-updateflow11.png)     
   
1. Click **Save** to save your changes.

Task 2 : Test your modified flow

Now that the flow has been modified, you are ready to test it.

1. Click **Test** in the top right of the flow editor and select **Manually**
2. In another tab, navigate to [Microsoft Teams using below URL.
   
   ```
   https://teams.microsoft.com/
   ```
3. Open a third tab and run the Device Ordering app -> Select a device and submit an approval request.
4. You should receive an email with options to Approve or Reject the request. Select **Approve**.
5. Shortly after hitting submit, you should see a message and a notification in the Chat tab on your app bar –
    this is from the Flow Bot. Click to open the chat. Wait a moment if it does not appear immediately.
6. You should see the approval of the request.

   ![](./images/Module4/PowerApps-updateflow12.png)  



