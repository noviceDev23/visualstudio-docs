---
title: "Using lookup tables in data binding - Windows Forms controls| Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "data binding, user controls"
  - "LookupBindingPropertiesAttribute class, examples"
  - "user controls [Visual Basic], creating"
ms.assetid: c48b4d75-ccfc-4950-8b14-ff8adbfe4208
caps.latest.revision: 14
author: "gewarren"
ms.author: "gewarren"
manager: ghogen
ms.technology: "vs-data-tools"
ms.workload: 
  - "data-storage"
---
# Create a Windows Forms user control that supports lookup data binding
When displaying data on Windows Forms, you can choose existing controls from the **Toolbox**, or you can author custom controls if your application requires functionality not available in the standard controls. This walkthrough shows how to create a control that implements the <xref:System.ComponentModel.LookupBindingPropertiesAttribute>. Controls that implement the <xref:System.ComponentModel.LookupBindingPropertiesAttribute> can contain three properties that can be bound to data. Such controls are similar to a <xref:System.Windows.Forms.ComboBox>.  
  
 For more information on control authoring, see [Developing Windows Forms Controls at Design Time](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time).  
  
 When authoring controls for use in data-binding scenarios you need to implement one of the following data-binding attributes:  
  
|Data-binding attribute usage|  
|-----------------------------------|  
|Implement the <xref:System.ComponentModel.DefaultBindingPropertyAttribute> on simple controls, like a <xref:System.Windows.Forms.TextBox>, that display a single column (or property) of data. For more information, see [Create a Windows Forms user control that supports simple data binding](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md).|  
|Implement the <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> on controls, like a <xref:System.Windows.Forms.DataGridView>, that display lists (or tables) of data. For more information, see [Create a Windows Forms user control that supports complex data binding](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md).|  
|Implement the <xref:System.ComponentModel.LookupBindingPropertiesAttribute> on controls, like a <xref:System.Windows.Forms.ComboBox>, that display lists (or tables) of data, but also need to present a single column or property. (This process is described in this walkthrough page.)|  
  
 This walkthrough creates a lookup control that binds to data from two tables. This example uses the `Customers` and `Orders` tables from the Northwind sample database. The lookup control will be bound to the `CustomerID` field from the `Orders` table. It will use this value to look up the `CompanyName` from the `Customers` table.  
  
 During this walkthrough, you will learn how to:  
  
-   Create a new **Windows Forms Application**.  
  
-   Add a new **User Control** to your project.  
  
-   Visually design the user control.  
  
-   Implement the `LookupBindingProperty` attribute.  
  
-   Create a dataset with the **Data Source Configuration** wizard.  
  
-   Set the **CustomerID** column on the **Orders** table, in the **Data Sources** window, to use the new control.  
  
-   Create a form to display data in the new control.  
  
## Prerequisites  
This walkthrough uses SQL Server Express LocalDB and the Northwind sample database.  
  
1.  If you don't have SQL Server Express LocalDB, install it either from the [SQL Server Editions download page](https://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx), or through the **Visual Studio Installer**. In the Visual Studio Installer, SQL Server Express LocalDB can be installed as part of the **Data storage and processing** workload, or as an individual component.  
  
2.  Install the Northwind sample database by following these steps:  

    1. In Visual Studio, open the **SQL Server Object Explorer** window. (SQL Server Object Explorer is installed as part of the **Data storage and processing** workload in the Visual Studio Installer.) Expand the **SQL Server** node. Right-click on your LocalDB instance and select **New Query...**.  

       A query editor window opens.  

    2. Copy the [Northwind Transact-SQL script](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) to your clipboard. This T-SQL script creates the Northwind database from scratch and populates it with data.  

    3. Paste the T-SQL script into the query editor, and then choose the **Execute** button.  

       After a short time, the query finishes executing and the Northwind database is created.  
  
## Create a Windows Forms Application  
 The first step is to create a **Windows Forms Application**.  
  
#### To create the new Windows project  
  
1. In Visual Studio, on the **File** menu, select **New**, **Project...**.  
  
2. Expand either **Visual C#** or **Visual Basic** in the left-hand pane, then select **Windows Classic Desktop**.  

3. In the middle pane, select the **Windows Forms App** project type.  

4. Name the project **LookupControlWalkthrough**, and then choose **OK**. 
  
     The **LookupControlWalkthrough** project is created, and added to **Solution Explorer**.  
  
## Add a user control to the project  
 This walkthrough creates a lookup control from a **User Control**, so add a **User Control** item to the **LookupControlWalkthrough** project.  
  
#### To add a user control to the project  
  
1.  From the **Project** menu, select **Add User Control**.  
  
2.  Type `LookupBox` in the **Name** area, and then click **Add**.  
  
     The **LookupBox** control is added to **Solution Explorer**, and opens in the designer.  
  
## Design the LookupBox control  
  
#### To design the LookupBox control  
  
-   Drag a <xref:System.Windows.Forms.ComboBox> from the **Toolbox** onto the user control's design surface.  
  
## Add the required data-binding attribute  
 For lookup controls that support data binding, you can implement the <xref:System.ComponentModel.LookupBindingPropertiesAttribute>.  
  
#### To implement the LookupBindingProperties attribute  
  
1.  Switch the **LookupBox** control to code view. (On the **View** menu, choose **Code**.)  
  
2.  Replace the code in the `LookupBox` with the following:  
  
     [!code-vb[VbRaddataDisplaying#5](../data-tools/codesnippet/VisualBasic/create-a-windows-forms-user-control-that-supports-lookup-data-binding_1.vb)]
     [!code-csharp[VbRaddataDisplaying#5](../data-tools/codesnippet/CSharp/create-a-windows-forms-user-control-that-supports-lookup-data-binding_1.cs)]  
  
3.  From the **Build** menu, choose **Build Solution**.  
  
## Create a data source from your database  
This step creates a data source using the **Data Source Configuration**wizard, based on the `Customers` and `Orders` tables in the Northwind sample database.  
  
#### To create the data source  
  
1.  On the **Data** menu, click **Show Data Sources**.  
  
2.  In the **Data Sources** window, select **Add New Data Source** to start the **Data Source Configuration** wizard.  
  
3.  Select **Database** on the **Choose a Data Source Type** page, and then click **Next**.  
  
4.  On the **Choose your Data Connection** page do one of the following:  
  
    -   If a data connection to the Northwind sample database is available in the drop-down list, select it.  
  
    -   Select **New Connection** to launch the **Add/Modify Connection** dialog box.  
  
5.  If your database requires a password, select the option to include sensitive data, and then click **Next**.  
  
6.  On the **Save connection string to the Application Configuration file** page, click **Next**.  
  
7.  On the **Choose your Database Objects** page, expand the **Tables** node.  
  
8.  Select the `Customers` and `Orders` tables, and then click **Finish**.  
  
     The **NorthwindDataSet** is added to your project, and the `Customers` and `Orders` tables appear in the **Data Sources** window.  
  
## Set the CustomerID column of the Orders table to use the LookupBox control  
 Within the **Data Sources** window, you can set the control to be created prior to dragging items onto your form.  
  
#### To set the CustomerID column to bind to the LookupBox control  
  
1.  Open **Form1** in the designer.  
  
2.  Expand the **Customers** node in the **Data Sources** window.  
  
3.  Expand the **Orders** node (the one in the **Customers** node below the **Fax** column).  
  
4.  Click the drop-down arrow on the **Orders** node, and choose **Details** from the control list.  
  
5.  Click the drop-down arrow on the **CustomerID** column (in the **Orders** node), and choose **Customize**.  
  
6.  Select the **LookupBox** from the list of **Associated Controls** in the **Data UI Customization Options** dialog box.  
  
7.  Click **OK**.  
  
8.  Click the drop-down arrow on the **CustomerID** column, and choose **LookupBox**.  
  
## Add controls to the form  
 You can create the data-bound controls by dragging items from the **Data Sources** window onto **Form1**.  
  
#### To create data-bound controls on the Windows Form  
  
-   Drag the **Orders** node from the **Data Sources** window onto the Windows Form, and verify that the **LookupBox** control is used to display the data in the `CustomerID` column.  
  
## Bind the control to look up CompanyName from the Customers table  
  
#### To setup the lookup bindings  
  
-   Select the main **Customers** node in the **Data Sources** window, and drag it onto the combo box in the **CustomerIDLookupBox** on **Form1**.  
  
     This sets up the data binding to display the `CompanyName` from the `Customers` table, while maintaining the `CustomerID` value from the `Orders` table.  
  
## Running the application  
  
#### To run the application  
  
-   Press F5 to run the application.  
  
-   Navigate through some records, and verify that the `CompanyName` appears in the `LookupBox` control.  
  
## See Also  
 [Bind Windows Forms controls to data in Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
