
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



Fix performance issues
Completed
100 XP
10 minutes
Occasionally, organizations will need to address performance issues when running reports. Power BI provides the Performance Analyzer tool to help fix problems and streamline the process.

Consider the scenario where you're building reports for the Sales team in your organization. You’ve imported your data, which is in several tables within the Sales team’s SQL database, by creating a data connection to the database through DirectQuery. When you create preliminary visuals and filters, you notice that some tables are queried faster than others, and some filters are taking longer to process compared to others.

Optimize performance in Power Query
The performance in Power Query depends on the performance at the data source level. The variety of data sources that Power Query offers is wide, and the performance tuning techniques for each source are equally wide. For instance, if you extract data from a Microsoft SQL Server, you should follow the performance tuning guidelines for the product. Good SQL Server performance tuning techniques include index creation, hardware upgrades, execution plan tuning, and data compression. These topics are beyond the scope here, and are covered only as an example to build familiarity with your data source and reap the benefits when using Power BI and Power Query.

Power Query takes advantage of good performance at the data source through a technique called Query Folding.

Query folding
The query folding within Power Query Editor helps you increase the performance of your Power BI reports. Query folding is the process by which the transformations and edits that you make in Power Query Editor are simultaneously tracked as native queries, or simple Select SQL statements, while you're actively making transformations. The reason for implementing this process is to ensure that these transformations can take place in the original data source server and don't overwhelm Power BI computing resources.

You can use Power Query to load data into Power BI. Then use Power Query Editor to transform your data, such as renaming or deleting columns, appending, parsing, filtering, or grouping your data.

Consider a scenario where you’ve renamed a few columns in the Sales data and merged a city and state column together in the “city state” format. Meanwhile, the query folding feature tracks those changes in native queries. Then, when you load your data, the transformations take place independently in the original source, this ensures that performance is optimized in Power BI.

The benefits to query folding include:

More efficiency in data refreshes and incremental refreshes. When you import data tables by using query folding, Power BI is better able to allocate resources and refresh the data faster because Power BI doesn't have to run through each transformation locally.

Automatic compatibility with DirectQuery and Dual storage modes. All DirectQuery and Dual storage mode data sources must have the back-end server processing abilities to create a direct connection, which means that query folding is an automatic capability that you can use. If all transformations can be reduced to a single Select statement, then query folding can occur.

The following scenario shows query folding in action. In this scenario, you apply a set of queries to multiple tables. After you add a new data source by using Power Query, and you're directed to the Power Query Editor, you go to the Query Settings pane and right-click the last applied step, as shown in the following figure.

Screenshot of the last applied step right-clicked to show the context menu.

If the View Native Query option isn't available (not displayed in bold type), then query folding isn't possible for this step, and you'll have to work backward in the Applied Steps area until you reach the step in which View Native Query is available (displays in bold type). This process will reveal the native query that is used to transform the semantic model.

Native queries aren't possible for the following transformations:

Adding an index column
Merging and appending columns of different tables with two different sources
Changing the data type of a column
A good guideline to remember is that if you can translate a transformation into a Select SQL statement, which includes operators and clauses such as GROUP BY, SORT BY, WHERE, UNION ALL, and JOIN, you can use query folding.

While query folding is one option to optimize performance when retrieving, importing, and preparing data, another option is query diagnostics.

Query diagnostics
Another tool that you can use to study query performance is query diagnostics. You can determine what bottlenecks may exist while loading and transforming your data, refreshing your data in Power Query, running SQL statements in Query Editor, and so on.

To access query diagnostics in Power Query Editor, go to Tools in the Home ribbon. When you're ready to begin transforming your data or making other edits in Power Query Editor, select Start Diagnostics in the Session Diagnostics section. When you're finished, make sure that you select Stop Diagnostics.

Screenshot of the Tools tab with session diagnostics options in the Power query Editor.

Selecting Diagnose Step shows you the length of time that it takes to run that step, as shown in the following image. This selection can tell you if a step takes longer to complete than others, which then serves as a starting point for further investigation.

Screenshot of applying query diagnostics.

This tool is useful when you want to analyze performance on the Power Query side for tasks such as loading semantic models, running data refreshes, or running other transformative tasks.

Other techniques to optimize performance
Other ways to optimize query performance in Power BI include:

Process as much data as possible in the original data source. Power Query and Power Query Editor allow you to process the data; however, the processing power that is required to complete this task might lower performance in other areas of your reports. Generally, a good practice is to process, as much as possible, in the native data source.

Use native SQL queries. When using DirectQuery for SQL databases, such as the case for our scenario, make sure that you aren't pulling data from stored procedures or common table expressions (CTEs).

Separate date and time, if bound together. If any of your tables have columns that combine date and time, make sure that you separate them into distinct columns before importing them into Power BI. This approach will increase compression abilities.

For more information, refer to Query Folding Guidance and Query Folding.



Resolve data import errors
Completed
100 XP
7 minutes
While importing data into Power BI, you may encounter errors resulting from factors such as:

Power BI imports from numerous data sources.
Each data source might have dozens (and sometimes hundreds) of different error messages.
Other components can cause errors, such as hard drives, networks, software services, and operating systems.
Data often can't comply with any specific schema.
The following sections cover some of the more common error messages that you might encounter in Power BI.

Query timeout expired
Relational source systems often have many people who are concurrently using the same data in the same database. Some relational systems and their administrators seek to limit a user from monopolizing all hardware resources by setting a query timeout. These timeouts can be configured for any timespan, from as little as five seconds to as much as 30 minutes or more.

For instance, if you’re pulling data from your organization’s SQL Server, you might see the error shown in the following figure.

Screenshot of the data import errors for query timeout.

Power BI Query Error: Timeout expired
This error indicates that you’ve pulled too much data according to your organization’s policies. Administrators incorporate this policy to avoid slowing down a different application or suite of applications that might also be using that database.

You can resolve this error by pulling fewer columns or rows from a single table. While you're writing SQL statements, it might be a common practice to include groupings and aggregations. You can also join multiple tables in a single SQL statement. Additionally, you can perform complicated subqueries and nested queries in a single statement. These complexities add to the query processing requirements of the relational system and can greatly elongate the time of implementation.

If you need the rows, columns, and complexity, consider taking small chunks of data and then bringing them back together by using Power Query. For instance, you can combine half the columns in one query and the other half in a different query. Power Query can merge those two queries back together after you're finished.

We couldn't find any data formatted as a table
Occasionally, you may encounter the “We couldn’t find any data formatted as a table” error while importing data from Microsoft Excel. Fortunately, this error is self-explanatory. Power BI expects to find data formatted as a table from Excel. The error even tells you the resolution. Perform the following steps to resolve the issue:

Open your Excel workbook, and highlight the data that you want to import.

Press the Ctrl-T keyboard shortcut. The first row will likely be your column headers.

Verify that the column headers reflect how you want to name your columns. Then, try to import data from Excel again. This time, it should work.

Screenshot of the Power B I Excel error: We couldn't find any data formatted as a table.

Couldn't find file
While importing data from a file, you may get the "Couldn't find file" error.

Screenshot of the Could not find file error screen.

Usually, this error is caused by the file moving locations or the permissions to the file changing. If the cause is the former, you need to find the file and change the source settings.

Open Power Query by selecting the Transform Data button in Power BI.

Highlight the query that is creating the error.

On the left, under Query Settings, select the gear icon next to Source.

Screenshot of the query settings pane with Source selected under Applied Steps.

Change the file location to the new location.

Screenshot of the file location settings pane.

Data type errors
Sometimes, when you import data into Power BI, the columns appear blank. This situation happens because of an error in interpreting the data type in Power BI. The resolution to this error is unique to the data source. For instance, if you're importing data from SQL Server and see blank columns, you could try to convert to the correct data type in the query.

Instead of using this query:

SELECT CustomerPostalCode FROM Sales.Customers

Use this query:

SELECT CAST(CustomerPostalCode as varchar(10)) FROM Sales.Customers

By specifying the correct type at the data source, you eliminate many of these common data source errors.

You may encounter different types of errors in Power BI that are caused by the diverse data source systems where your data resides.

If you experience an error not covered, you can search Microsoft documentation for the error message, and the resolution you need.




