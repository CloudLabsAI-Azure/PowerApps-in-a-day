# Module 1: Power Apps Canvas App

### Estimated Duration: 60 Minutes

## Overview

This lab showcases how Microsoft Business Application Platform technologies enable citizen developers to build a customized device ordering solution. Using Power Apps, participants will design an interface to browse, filter, compare devices, and submit orders with custom forms. Power Automate will streamline approval workflows, sending automated requests to managers and allowing approvals directly via email. Microsoft Dataverse will securely store order data and enable admins to manage and view all orders. The solution ensures a seamless user experience with notifications for approvals/rejections and supports a tailored procurement process for device purchases.

## Lab objectives

In this lab, you will complete the following tasks:

- Exercise 1: Create the app in Power Apps
- Exercise 2: Add Device Gallery and Connect to Data Source
- Exercise 3: Add Compare Screen

### Lab Prerequisites

Follow the pre-requisite steps described in the **Lab Overview and Pre-requisites** (Page 1 of lab guide). Before beginning this lab, confirm that you have provisioned an environment where you will save your apps, flows and database entities.

**IMPORTANT:** Do not proceed before going through the lab pre-requisite steps

## Exercise 1: Create the app in Power Apps

**IMPORTANT:** Do not proceed before going through the lab pre-requisite steps.


### Task 1: Sign-in to Power Apps web studio

1. Navigate to Power Apps Portal using the below URL and click Sign-in. You may also directly navigate to Make Power Apps.

   ```
   http://powerapps.microsoft.com/
   ```
      ![](images/pp6.png)     

2. Login to the account using the below credentials.

    * Azure Username/Email: <inject key="AzureAdUserEmail"></inject> 
    * Azure Password: <inject key="AzureAdUserPassword"></inject>
    
3. Click on the **Environment** drop down and select the **Contoso Test** environment whihch we created in the previous task.

      ![](images/pp7.png)

      > **Note:** If your environment doesn't show up, try logging out and logging in again

### Task 2: Create a new application

1. In the home page, click on the search bar and search for canvas app and select **Canvas app from blank** from the dropdown.

      ![](images/pp8.png)
   
1. Click on **Create**.
 
1. Input **Device Ordering App (1)** in the App Name field, Select **Tablet (2)** for the Format and click on **Create (3)**.

      ![](images/pp9.png)
   
      > **Note:** If prompted, select your region, then click **Get started**.

      > **Note:** It takes few minutes to complete. Refresh the page after few minutes.
 
1. Click on **Skip** if you receive the **Welcome to Power Apps Studio** prompt.

### Task 3: Rename the screen

In this task, you will rename Screen1 to Main Screen.

1. Select the screen by clicking the **Screen1** tile in the **Tree view**.

2. Click on the **Ellipsis (...)** beside the **Screen1** and select the **Rename** option.

      ![](images/pp10.png)

3. Change the name to **Main Screen.**

      **_Tip_** _: It is a good practice to rename screens and controls as you create them, so they are easier to locate as you work with formulas that reference different controls. In this lab, you will be prompted to rename screens and some of the controls. For
the others, you may rename them as you please on your own. It is important that you rename screens as prompted in this lab as future steps may rely on specific screen names._

### Task 4: Add a header containing the app name and logged in user’s name

1. With Main Screen selected, click on the **+ Insert** button.

      ![](images/pp11.png)
   
2. Drag **Text Label** from the Insert pane and drop it on the Main Screen.

   ![](images/Module1/powerAppsCanvasApp11.png)  
   
3. Select the **Tree View** tab.

   ![](images/Module1/powerAppsCanvasApp12.png)  
   
4. Rename Label1 to **Header Label** , see the previous task on renaming controls.

   > **NOTE** : It is IMPORTANT to rename this label correctly, so subsequent instructions in the lab work as expected.

   ![](images/Module1/powerAppsCanvasApp13.png)  
   
5. Select **Text** from the property drop-down list and enter **"Device Ordering App"** in the formula bar. You can also
   type directly in the label.

   ![](images/Module1/powerAppsCanvasApp14.png)  
   
6. Resize the label such that the width is the width of the screen and the height is a reasonable size for a header. You
   can resize the label by either dragging the corners of the label or adjusting the size in the Right Pane.

   ![](images/Module1/powerAppsCanvasApp15.png)  
   
7. Align center the text.

   ![](images/Module1/powerAppsCanvasApp16.png)  
   
8. From the top, select the more options icon ,change the **Color** to White and the **Background Color** to Blue.

      ![](images/pp15.png)
   
9. Change the **Font Size** to 24.

      ![](images/pp16.png)
 
    > **_Tip_** _: You can also use the formula bar above or the Advanced tab on the far right of the screen to enter specific values
or formulas for any property on a control._

10. Select **+ Insert** button and drag another **Text Label** to the Main Screen. You will use this label to display the
    logged in user’s name.

      ![](images/pp17.png)
   
11. Drag the label to the far-right side of the screen as shown and center the label vertically to be in line with the
    header text. As you center your label, purple alignment markers will appear.

    ![](images/Module1/powerAppsCanvasApp20.png)  
   
12. Rename the label to **User Label**.

13. Change the value of the Text field to: "Hello, " & User().FullName

      ![](images/pp18.png)
    > **_Note_** _: All functions in Power Apps are case sensitive. As you start typing “User” you will see a drop-down of available choices.
It is a good idea to pick from the autocomplete options. You will also notice help text at the top showing the required
parameters, in this case, it requires no input parameters._

14. Right-align the text in the label by selecting the **Align** and **Align Right** option in the **Home** tab on the ribbon.

15. Change the text **Color** to **White**.

16. Widen the label, so the text does not wrap for longer usernames.

17. Change the **PaddingRight** property from **5** to **20**. You can do this quickly using the Properties pane on the right
    side.

    ![](images/Module1/powerAppsCanvasApp22.png)  
    > **Note:** The **User()** function in Power Apps allows you to retrieve the Email, Full Name, and Picture for the currently logged
in user. App users will always be logged in with their business or school account (Azure Active Directory (AAD) credentials),
so this information will always be available for any Power Apps app.

#### Task 5: Save the Application

In this task, you will save an initial version of the app. It is a good practice to keep saving app updates at regular intervals.

1. First, you will check if there are any errors. Click on then **App Checker** icon.

      ![](images/pp19.png) 
   
2. The **App Checker** pane will come to view. Errors will be displayed here if there are any.

3. Close the **App Checker** pane.
   
4. Click on **Settings**.

      ![](images/pp20.png)

5. In the application settings page, you can:

     - Change your app name
     - Customize the app icon – choose a background color and icon

      ![](images/pp21.png)

6. Select the **Display** tab to view the available screen orientation and aspect ratio settings. For this app, we will leave
    it at the default setting of Landscape with 16:9 aspect ratio.

      ![](images/pp22.png)
   
7. Close the **Settings**.

8. Click on **Save** from the top right.

      ![](images/pp23.png)

   > **_Tip:_** _In Power Apps when you save a version of your app the first version is published by default and available to everyone
you share the app with. Subsequent saves are only visible to the app maker in the studio. You must explicitly publish it for all
app users to get the update. For more details on saving, publishing and sharing apps, you can find the refernces below:

 Publish App: `https://powerapps.microsoft.com/tutorials/save-publish-app/`

 Share App: `https://powerapps.microsoft.com/tutorials/share-app/`

 Save and Publish App: `https://powerapps.microsoft.com/blog/saveandpublish/`

### Exercise 2: Add Device Gallery and Connect to Data Source

In this exercise, you will add a gallery of all available devices making it easy for users to browse the list and get a quick
overview of the devices available.

#### Task 1: Add device gallery

1. With Main Screen selected, select the **+ Insert** tab.

2. Type **Horizontal** and select **Horizontal Gallery**.

      ![](images/pp24.png)
   
   > This will add a gallery called **Gallery1** onto the screen. Notice the control tree view on the left displays this gallery with
three controls within it – two labels and an image. A data pane will pop up on the right.  
      
3. Expand **Connectors** , then click **Show all connectors**.

      ![](images/pp25.png)

4. Select **Import from Excel.**

      ![](images/pp26.png)

5. In the File Open dialog, browse to the location `C:\LabFiles\PowerApps-in-a-day` inside the LabVM and select **Device-Order-Data.xlsx** to load it.

6. Select both tables, **Devices** and **Manufacturers,** and click the **Connect** button. This will add both these tables as
    static data into the application.
    
      ![](images/pp27.png)

   > **Note** : In this lab, you will work with tables imported from a static data file and embedded as resources in the app. If you
were building a real solution, the same tables would likely be stored in the cloud, such as in a SharePoint list, a SQL table,
or a Microsoft Dataverse table.

8. Select **Gallery1** and notice the **Items** property is set to **Devices**. Notice the gallery is populated with data.

      ![](images/pp50.png)

      > **Note:** The name of the device can differ.

9. Rename the **Gallery1** to **Device Gallery**.

      ![](images/pp51.png)

### Task 2: Arrange the device gallery

1. Resize and reposition the gallery. You can drag and drop the gallery or use the gallery properties pane on the right.

      ![](images/pp52.png)
 
2. Select the **Device Gallery** and click the **Edit (pencil) icon** in the top left to edit the template cell.

      ![](images/pp53.png)
 
3. Using the right drag control, resize the first box to be narrower. Notice that all the items get narrower and more devices are visible on the screen.
       
4. Narrow the image as well by **clicking on the image control and resizing it using the drag handles**. Make sure the width of the image control is positioned within the template. 

5. Notice the gallery control on our screen automatically has scrolling capabilities.

      ![](images/pp54.png)
   
### Task 3: Add gallery to show manufacturers

1. Select the **Main Screen**.

2. Select the **Insert (1)** tab, **search (2)** for Vertical and click on **Vertical Gallery (3)**

      ![](images/pp55.png)

3. Select **Manufacturers** for the data source.

   ![](images/Module1/devicegallery7.png) 
 
4. Rename the gallery to **Manufacturer Gallery**.

   ![](images/Module1/devicegallery8.png) 
 
5. Move this new gallery so that it is left aligned with the left edge of the screen and top aligned with the top of the device gallery. Your two galleries should like the image below.

      ![](images/pp56.png)

6. Select **Manufacturer Gallery (1)** (not just the template cell), in the **Properties** tab on the right, click **Layout (2)**. Scroll down to the **Gallery** section and select **2 Columns (3)**.
   
      ![](images/pp57.png)
 
7. Change the **Wrap Count** from **2** to **1**. This will change it to a single column gallery.

   ![](images/Module1/devicegallery12.png) 

8. Select the **image control** within the gallery (the Edit Pencil icon) and **reduce its height** by dragging the middle
    bottom drag control upwards. If you select the first image, the image size will reduce whereas the template size
    will still be expanded.

9. Reduce **the height of the template cell** until three or four images occupy the gallery without scrolling. We
    essentially want the image to occupy the entire cell.

    ![](images/Module1/devicegallery13.png) 
   
10. Click on **Save** from the top right.
    
### Task 4: Connect Manufacturer Gallery to manufacturers table

Earlier you connected the data source using the Data tab in the right pane. You can also connect to data via the formula
bar.

1. Select the **Manufacturer Gallery**. Make sure the whole gallery is selected and not just the first cell.

2. Select **Items** from the property drop-down next to the formula bar. Notice that the gallery is populated with
    images of buildings. This is because Power Apps picked a default binding which mapped to the HQ column in the
    table.
  
   ![](images/Module1/devicegallery14.png) 
   
3. Select the image control in the first template cell in the gallery and change the value of **Image** in the formula bar
    from **ThisItem.HQ** to **ThisItem.Logo**. All the gallery items will now display logo images. You can also use the left
    tree view to select the controls, sometimes that is easier!

    ![](images/Module1/devicegallery15.png) 
    
    > Note: Autosuggest offers you valid options for authoring formulas. See in the image below, we want to define the
image to display from our data. Once we type “ThisItem.” our Autosuggest tells us that we have three valid options
for this formula. This can help guide you to making valid formulas.
    
4. Select the first (top-most) image and using the **Properties** pane on the right, set the **Image position** property to
    **Fit**.

   ![](images/Module1/devicegallery17.png) 

5. Reduce the height of the template cell such that all nine manufacturers fit without a scrollbar. To do this, use the
    drag handles to first reduce the height of the image and subsequently reduce the height of the template cell.
    Note again that to select the template cell, select the entire gallery and click on the pencil icon in the top left.
   
   
###  Task 5: Highlight the selected item in the gallery

In this task, you will use the **TemplateFill** property of the manufacturer gallery to specify a highlight color for the selected
item

1. With the **Manufacturer Gallery** selected, set the **TemplateFill** property on the gallery to the following formula to
    conditionally set the fill color of the selected cell to light blue:
   
    ```
    If(ThisItem.IsSelected,LightBlue)
    ```

    > Alternately, you could set the TemplateFill property to:

     ```
     If(ThisItem.IsSelected,ColorFade ('Header Label'.Fill,75%))
     ```
      This approach is recommended so the fill color matches the header label with a 75% fade. If you change the fill
color of header label, the fill color of the selected item in the gallery will automatically change.

   ![](images/Module1/devicegallery19.png) 

2. Now try using the preview mode to perform a quick test of this highlighting. You can enable preview mode by
    holding down the Alt key (also known as the Option key) and clicking a few different manufacturers in the gallery,
    notice the selected item in the manufacturer gallery is highlighted in a light blue color. The preview mode ends
    when you stop holding the key.


Alternatively, you could click the Play ( ) button to enter preview mode, and to exit this you would hit the X in
the upper right corner or use the Esc key.


### Task 6: Configure text labels in the device gallery

1. Select the subtitle in the **Device Gallery**. It may already have the default value set to the **DeviceType** property
    (e.g. Tablet).

2. Let us now change the label to display the device price by setting the label’s Text property to: **ThisItem.Price**

  ![](images/Module1/devicegallery22.png) 
   
   Here are some additional formatting suggestions. These are for cosmetic purposes only, feel free to skip past these:

   - Expand the width of the label to the template width.

      Notice that if you do this with the Title1 label, the subtitle label expands as well. This is because it is X property is set
to Title1.X, the X coordinate position of the Title1 label. You can find more details on the relative positioning of controls here: `https://powerapps.microsoft.com/blog/ux-patterns-control-positioning/`

     - _Change the_ **PaddingLeft** _of the Subtitle from_ **0** _to_ **10**_._

     - _Change the font of the Subtitle to_ **Segoe UI**_._

     - To add the $ to the Subtitle, use the Text format expression: Text(ThisItem.Price,"$##,###.00") or for alternate/European locales: Text(ThisItem.Price;"$##.###,00")

     Note: After you enter the above value in the formula bar, it will automatically resolve to include your locale, e.g. [$-en-
US]. If you see an error here, it might be because your locale is not yet supported, in which case as a workaround,
manually change it to [$-en-US]:

   ![](images/Module1/devicegallery23.png) 
   
3. Select the **Title1**.

4. In the property drop-down list, select the **Text** field and change to **ThisItem.Title**.

   ![](images/Module1/devicegallery24.png) 

**Optional UI enhancement:**

- Like above, expand the width of the label to the template width and change the value of the **PaddingLeft**
    property of the Title1 label from **0 to 10**. Or set it to Title1.PaddingLeft.

- Change font to **Segoe UI**.

5. Click on **Save**.

#### Task 9: Add a checkbox to add a device to Compare list

We want to allow users to select multiple devices to compare before making a final selection on the next screen.

1. Select the **Device Gallery** , click the Pencil edit icon in the top left of the gallery to select the template cell.

   ![](images/Module1/devicegallery27.png) 
   
2. Make sure that only the first item in the gallery is selected (not the entire gallery).
 
   ![](images/Module1/devicegallery28.png) 
3. Add a checkbox by clicking **Insert** - > **Input** - > **Checkbox**.

   ![](images/Module1/devicegallery29.png) 

4. Move the inserted checkbox below the price.

   ![](images/Module1/devicegallery30.png) 
   
5. Change the checkbox text to **“Compare”.** You can do this by setting the **Text** property.

   ![](images/Module1/devicegallery31.png) 
   
### Task 10: Create a collection for the selected devices

When a user selects a device to compare, we will add it to a collection called **CompareList**. You can think of this as an in-
memory collection of devices that have been selected for comparison.

1. Select the **Checkbox** control and click on the **Action** tab in the ribbon, click **OnCheck** and set the value in the
    formula bar to: Collect(CompareList,ThisItem)

   ![](images/Module1/devicegallery32.png) 
   
2. Set the **OnUncheck** value to: Remove(CompareList,ThisItem)
    This is required to make sure the unchecked items are removed from the collection.
  
  ![](images/Module1/devicegallery33.png) 
  
3. Set the **Default** property of the checkbox to the formula: ThisItem in CompareList

   ![](images/Module1/devicegallery34.png) 
   
   > The **Default** setting of the checkbox is a Boolean true or false value that determines if the checkbox should be checked or
not by default. Setting it to this formula will ensure that the checkbox is checked by default if the item has already been
added to the collection since the result will be true, i.e. this item *is* in CompareList.

4. Let’s test out adding items to a collection by running the app in Preview (F5) or by clicking the Preview button on
    the top right. Click on the checkboxes of three devices.

   ![](images/Module1/devicegallery35.png) 
   
5. Close the preview.

6. Click the **View** tab and select **Collections**.

   ![](images/Module1/devicegallery36.png) 
   
7. You will see the **CompareList** collection and the three items you selected.

   ![](images/Module1/devicegallery37.png) 
   
   > Note that each item in the collection has all the information for each machine that we get from the **Machines** data source,
not just the fields we display in the Devices Gallery.


8. Click the back arrow on the top left to get back to the main view.

9. Click **Preview** again.

10. Uncheck all the checked items and click on close the preview.

   ![](images/Module1/devicegallery38.png) 

11. Click the **View** tab and select **Collections**.

   ![](images/Module1/devicegallery39.png) 
   
12. All items will be removed from the **CompareList** collection.

13. Click on then back arrow.

    For more information on working with Collections in Power Apps, you can find the refernces below:

    - Create Update Collections: `https://powerapps.microsoft.com/tutorials/create-update-collection/` and

    - Clear Collections: `https://powerapps.microsoft.com/tutorials/function-clear-collect-clearcollect/`

### Task 11: Set the default selection to the first manufacturer and test the app

To avoid getting a blank list of devices when the app starts, set the default selected item in the Manufacturer gallery to be
the first item.

1. Select the entire gallery (by clicking **Manufacturer Gallery** in the tree view on the left) and set the **Default**
    property of the gallery in the formula bar to: First(Manufacturers)

    This will set it to the first item in the table.

   ![](images/Module1/devicegallery40.png) 

2. To preview the app, press the Preview button on the upper right of the top menu. Pressing the F5 key will also
    preview the application. **Note** : You can also test your app right on the canvas by holding down the Alt key to
    activate buttons and other controls, as well as double-clicking to type into controls.

3. Your app should look like the image below.

   ![](images/Module1/devicegallery41.png) 
   
4. To exit preview mode, click the X in the top right corner.

   ![](images/Module1/devicegallery42.png) 
   
5. Save the application.


### Exercise 3: Add Compare Screen

The second screen is where users compare the selected devices and then choose the one they wish to submit for approval.

This screen will include:


- A back button for navigation back to the main screen.

- A list of selected devices for comparison (carried over from the main screen).

- Additional details for each device.

- Highlighting the selected device

In a subsequent lab, you will create the database entities to store the device orders and add an edit form to this screen to
enter additional information and submit the request.

#### Task 1: Add screen


1. From the ribbon click **Home** and **New Screen** and choose **Blank**.

   ![](images/Module1/devicegallery43.png) 
   
2. Rename the screen to **Compare Screen**.

   ![](images/Module1/devicegallery44.png) 
   
3. In the left tree view, select the **Main Screen** , click on the **Insert** tab on the ribbon and select **Button** to add a
    button to the screen.

   ![](images/Module1/devicegallery45.png) 

4. Place the button in the bottom right corner.

   ![](images/Module1/devicegallery46.png) 

5. Set the button’s **Text** property to: "Compare " & CountRows(CompareList) & " item(s)"

   ![](images/Module1/devicegallery47.png) 
   
6. Resize the button, so the text fits without wrapping.

   ![](images/Module1/devicegallery48.png) 

7. Select the button and set its **DisplayMode** property to Disabled if there are no items in CompareList:
    If(CountRows(CompareList) > 0, DisplayMode.Edit, DisplayMode.Disabled)

   ![](images/Module1/devicegallery49.png) 
   
8. Unselect all devices – notice the button is grayed.

   ![](images/Module1/devicegallery50.png) 
   
9. Select the **compare button** and **copy (Ctrl-C)** this button.
   
10. **Paste (Ctrl-V)** the button on the same screen.

11. Position it to the left of the compare button.

   ![](images/Module1/devicegallery51.png) 

12. Change the **Text** property to "Clear Selection"

13. Set the **OnSelect** property for this button to: Clear(CompareList). This will remove all the items in the
    CompareList collection.

   ![](images/Module1/devicegallery52.png) 
   
14. Select the **Compare** button, click on the **Action** tab and select **Navigate.**

   ![](images/Module1/devicegallery53.png) 
   
15. Select **Compare Screen** from the drop-down and **ScreenTransition.None** for transition type.

   ![](images/Module1/devicegallery54.png) 

16. Click **Preview**.

17. Select a couple of devices and click the **Compare** button and verify that it takes you to the second screen.

   ![](images/Module1/devicegallery55.png) 
   
18. You should navigate to the new empty screen. Close the preview.

   ![](images/Module1/devicegallery56.png) 
   
19. Go to the **Main Screen** in the tree view.

20. Select both the **User Label** and **Header Label** , right click and select **Group**.

   ![](images/Module1/devicegallery57.png) 
   
21. Rename the group **Header**.

22. Click on the ... button of the **Header** and select **Copy**.

   ![](images/Module1/devicegallery58.png) 

23. Right click on the **Compare Screen** by and select **Paste**.

   ![](images/Module1/devicegallery59.png) 
   
24. The **Header** in the **Compare Screen** should look like the image below.

   ![](images/Module1/devicegallery60.png) 
   
25. Copy **Device Gallery** from the **Main Screen** and paste it in the **Compare Screen**.

26. Move the gallery to the left edge of the screen. Align the top of the gallery to be just under the header banner. Use the right drag handle to reduce the width of the gallery and create space for a data entry form on the right of
    the screen. You will insert a Form control here and configure it in a subsequent lab.
    
   ![](images/Module1/devicegallery61.png)     
   
27. Rename this gallery to **Compare List Gallery**.

   ![](images/Module1/devicegallery62.png) 

#### Task 2: Configure the gallery

In this task, you will configure the gallery to show devices that were selected from the comparison gallery on the Main
Screen.


1. Select the new **Compare List Gallery**.

2. Select **Items** in the property drop-down list and change the data source in the formula bar to CompareList.

   ![](images/Module1/devicegallery63.png) 
   
3. The gallery will now show the selected items from the Main Screen.

   ![](images/Module1/devicegallery64.png) 
   
#### Task 3: Remove and add controls to the gallery

In the **Compare Screen** we are selecting a given item to get approved, so we do not need a Compare checkbox.

1. Select the **Compare checkbox** on the left most template cell and press the **Delete** key to delete the checkbox.

2. Now let’s add a few labels to display additional attributes about the device. A good way to do this is to copy
    paste. Select the first label in the gallery that is displaying the device name. Copy it (Ctrl-C) and paste it (Ctrl-V).
    Rename these labels as you go for ease of use later.


3. Move the new label so that it is just below the price. Set the **Text** property to: ThisItem.ManufacturerName.

   ![](images/Module1/devicegallery65.png) 
   
4. Use the ribbon to change the font weight from **Semibold** to **Normal** and change the **Size** property from 20 to 18.

   ![](images/Module1/devicegallery66.png) 
   
5. Copy and paste this label and move the new fourth label below the third label. Set its **Text** property to:
    ThisItem.Memory

   ![](images/Module1/devicegallery67.png) 
   
6. Repeat this and add text boxes to display the additional device properties – Processor, Storage, ScreenSize, etc.
    Feel free to customize the labels by changing their Size, Color, Fill and Font Weight properties.


Note : For this lab, to save time you may add one or two of these additional properties and skip adding all the
additional device properties.



#### Task 4: Highlight the selected device

Like the behavior in the manufacturer gallery in the first screen, use the **TemplateFill** property to specify a highlight color
for the selected item.

1. Select the **Compare List Gallery.**

2. With the whole gallery selected, set the **TemplateFill** property to:

   ```
   If(ThisItem.IsSelected,ColorFade('Header Label'.Fill, 75%))
   ```
   
   ![](images/Module1/devicegallery68.png)   
   
   This is conditionally setting a Fill color if the cell is selected. You could have set a specific color or RGB value, but we recommend using the ColorFade function, so it matches the header label with a 75% fade. If you change the fill color of header label, this template fill color will      automatically change.


3. Holding down **Alt** , click a few different items in the gallery, notice the selected item is highlighted in a light blue
    color.

#### Task 5: Add an icon to navigate to the first screen

1. Select the **Compare Screen**.

2. Go to **Insert** , then **Icons** and select the **Left** icon. Position it in the upper left corner of the screen.

   ![](images/Module1/devicegallery69.png)  

3. Select the arrow control, change the **Color** property to **White**. You can change this in the formula bar or through
    the **Properties** pane on the right.

   ![](images/Module1/devicegallery70.png)   
   
4. Move the arrow to the top-left corner.

   ![](images/Module1/devicegallery71.png)   
   
5. Set the **OnSelect** action for the icon to Back(). This will cause navigation back to the previous screen.

   ![](images/Module1/devicegallery72.png)   
   
**Optional UI enhancement:**

 - Add **padding around the icon** using the Properties pane. Set the padding values to 10 each for Top, Bottom, Left, and
Right. This will make the icon look smaller but still have a larger hit target for the click action. This is a good pattern to use
for most icons.


####  Task 6: Test the app

Let’s save the app by selecting **File** - > **Save**. It is a good idea to save your app regularly. **Note** : You can also test your app
right on the canvas by holding down the Alt key to activate buttons and other controls, as well as double-clicking to type
into controls.

1. Go to the **Main Screen** and **Preview** the app by hitting the **Play** button in the top right.

   ![](images/Module1/devicegallery73.png)   
   
2. Uncheck if there are any checked devices.

3. Select **Microsoft** on the left to show a filtered set of devices.

4. Check the compare box on a few devices on the main screen from a few different manufacturers.

5. Click the **Compare** button to navigate to the compare screen.

6. Tap or click on different devices in the gallery and verify that the selection highlight works.

7. Click the **Back** button and confirm you get back to the main screen.

   ![](images/Module1/devicegallery74.png)   
   
8. Click **Clear Selection**.

   ![](images/Module1/devicegallery75.png)   

9. The **CompareList** will clear, and the **Compare** button will become disabled.

   ![](images/Module1/devicegallery76.png)   
   
10. Close the preview.

#### Task 7: Test the app on a mobile device

Congratulations! You’ve created your Power Apps app. Now let’s publish and test it on a mobile device.

1. **File** - > **Save**.

2. **C** lick the **Publish** button.

3. Click **Publish this version** on the confirmation prompt.

   ![](images/Module1/devicegallery77.png)   
   
   This action will publish the latest saved version of the app.

4. Go to your device’s app store application. Search for “ **Power Apps** ” and install the Power Apps application.
    Launch the app.
   
   ![](images/Module1/devicegallery78.png)   


5. When the app starts, it will prompt for your business or school account credentials. **Log in** with the same account
    that you used to create the Power Apps app. You should see the app you just created in the list of apps. **Run the**
    **app**.

### Task 8: [Optional] Share the application with a colleague

You may optionally share the application with another user within the same organizational tenant as the user who created
the app. So, if you had logged in as meganb@contoso.com, you may share the app with any other User, Security Group or
Distribution Group within the @contoso.com tenant.

1. To share the app, go to Make Power Apps. Log in if prompted for credentials.

2. Select **Apps** in the left pane, look for your Device Ordering app in the app list, click the three dots (...) next to the
    app to bring up the context menu. Click the **Share** option.

   ![](images/Module1/devicegallery80.png)   
   
3. In the share screen, enter the name of the user **Lab admin01** or **Lab admin02** to share the app. You may also share
    it with a user group.

   ![](images/Module1/devicegallery81.png)   

4. Select the user or group; this will add it to the **Shared with** list below. You may provide this user/group either **Can**
    **use** or **Can edit** permissions.

   ![](images/Module1/devicegallery82.png)   
   
5. If the **Send an email invitation** is checked, when you hit **Save** , the user or all users in the group will receive an
    email letting them know that the app has been shared with them, along with a link to open the app.

   ![](images/Module1/devicegallery83.png)  
   
**Next steps**

Now that you have learned the basics of creating an app, take a little time to think about what you would like to create
next. What made you most excited about the device ordering app? What would you have done differently? Here’s an
example of some changes you can make to the UI:

   ![](images/Module1/devicegallery84.png)   
   
Features like shading, number of rows, and greying out items not selected can have a big impact on how your app looks and feels. To learn more, check out the links in the reference section and take the next step in building great apps.


