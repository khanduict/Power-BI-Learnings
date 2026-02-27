
There are three primary components to Power BI:

    - Power BI Desktop (desktop application) - you create visualisation report
    - Power BI service (online platform) - Then publish to Power BI service and then create a dashboard
    - Power BI Mobile (cross-platform mobile app)

The flow of Power BI is:

    - Connect to data with Power BI Desktop.
    - Transform data with Power Query Editor (comes with Power BI Desktop).
    - Model data with Power BI Desktop.
    - Create visualizations and reports with Power BI Desktop.
     - Publish report to Power BI service.
    - Distribute and manage reports in the Power BI service.

Power BI service
Workspaces are the foundation of the Power BI service. When publishing any report, you must choose a workspace. By default, every user has access to My workspace, which is ideal only for testing. When you want to share content with others, always create and use a shared workspace.

Distribute content
In a workspace, you can create an app, which provides consumers a simplified interface to access reports and dashboards. In the app configuration, you set up the app, select the content to include (limited to the current workspace), and choose your audience.

Once you create an app, you must update the app after each change to items in the workspace. The requirement to update the app allows you to control what version of the content is visible to your audience.

    - Flat file - A flat file is a type of file that has only one data table and every row of data is in the same structure.        -  The file doesn't contain hierarchies. E.g CSV and .txt files  
    - Another type of file would be the output files from different applications, like Microsoft Excel workbooks (.xlsx).

Files location
        Local - You can import data from a local file into Power BI. The file isn't moved into Power BI, and a link doesn't remain to it. Instead, a new semantic model is created in Power BI, and data from the Excel file is loaded into it. 
        Accordingly, changes to the original Excel file aren't reflected in your Power BI semantic model. You can use local data import for data that doesn't change.
        
        OneDrive for Business - You can pull data from OneDrive for Business into Power BI. This method is effective in keeping an Excel file and your semantic model, reports, and dashboards in Power BI synchronized. Power BI connects regularly to your file on OneDrive. If any changes are found, your semantic model, reports, and dashboards are automatically updated in Power BI.
        
        OneDrive - Personal - You can use data from files on a personal OneDrive account, and get many of the same benefits that you would with OneDrive for Business. However, you'll need to sign in with your personal OneDrive account, and select the Keep me signed in option. Check with your system administrator to determine whether this type of connection is allowed in your organization.
        
        SharePoint - Team Sites - Saving your Power BI Desktop files to SharePoint Team Sites is similar to saving to OneDrive for Business. The main difference is how you connect to the file from Power BI. You can specify a URL or connect to the root folder.

Select a storage mode
The most popular way to use data in Power BI is to import it into a Power BI semantic model. Importing the data means that the data is stored in the Power BI file and gets published along with the Power BI reports. This process helps make it easier for you to interact directly with your data. However, this approach might not work for all organizations.

To continue with the scenario, you're building Power BI reports for the Sales department at Tailwind Traders, where importing the data isn't an ideal method. The first task you need to accomplish is to create your semantic models in Power BI so you can build visuals and other report elements. The Sales department has many different semantic models of varying sizes. For security reasons, you aren't allowed to import local copies of the data into your reports, so directly importing data is no longer an option. Therefore, you need to create a direct connection to the Sales department’s data source. The following section describes how you can ensure that these business requirements are satisfied when you're importing data into Power BI.

However, sometimes there may be security requirements around your data that make it impossible to directly import a copy. Or your semantic models may simply be too large and would take too long to load into Power BI, and you want to avoid creating a performance bottleneck. Power BI solves these problems by using the DirectQuery storage mode, which allows you to query the data in the data source directly and not import a copy into Power BI. DirectQuery is useful because it ensures you're always viewing the most recent version of the data.

        The three different types of storage modes you can choose from:
        
        Import
        DirectQuery
        Dual (Composite)
        You can access storage modes by switching to the Model view, selecting a data table, and in the resulting Properties pane, selecting which mode that you want to use from the Storage mode drop-down list, as shown in the following visual.
        
        Let’s take a closer look at the different types of Storage Modes.
        
        Import mode
        The Import mode allows you to create a local Power BI copy of your semantic models from your data source. You can use all Power BI service features with this storage mode, including Q&A and Quick Insights. Data refreshes can be scheduled or on-demand. Import mode is the default for creating new Power BI reports.
        
        DirectQuery mode
        The DirectQuery option is useful when you don't want to save local copies of your data because your data won't be cached. Instead, you can query the specific tables that you'll need by using native Power BI queries, and the required data will be retrieved from the underlying data source. Essentially, you're creating a direct connection to the data source. Using this model ensures that you're always viewing the most up-to-date data, and that all security requirements are satisfied. Additionally, this mode is suited for when you have large semantic models to pull data from. Instead of slowing down performance by having to load large amounts of data into Power BI, you can use DirectQuery to create a connection to the source, solving data latency issues as well.
        
        Dual (Composite mode)
        In Dual mode, you can identify some data to be directly imported and other data that must be queried. Any table that is brought in to your report is a product of both Import and DirectQuery modes. Using the Dual mode allows Power BI to choose the most efficient form of data retrieval.



