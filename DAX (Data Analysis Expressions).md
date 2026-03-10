

###  DAX (Data Analysis Expressions)
DAX is used to create powerful calculations in Power BI, helping us to analyse and visualize the data.

#### DAX Calculation Types - You can use DAX to add 3 types of calculations to the semantic models;
There are 3 types of DAX calculation namely
    - Calculated Tables - are used to create date tables or role-playing dimensions or to enable what-if analysis
    - Calculated Columns - can be added to tables in the model
    - Measures - achieves summarization over model data

    

##### Calculated columns
this computes values row-by-row during data refresh and stores them in the model.
The formula is evaluated for each table row and it returns a single value. When added to an Import storage mode table, the formula is evaluated when the semantic model is refreshed, and it increases the storage size of your model. When added to a DirectQuery storage mode table, the formula is evaluated by the underlying source database when the table is queried.
- It creates a physical data column
- Increases the storage size
- Can prolong data refresh time

#### Measures
Computed on-the-fly at query time (runtime) based on user interaction (slicers/filters). It does not take up storage space and is best for numerical aggregations
The formula achieves summarization over model data. Similar to a calculated column, the formula must return a single value. However, unlike calculated columns, which are evaluated at data refresh time, measures are evaluated at query time. Their results are never stored in the model.
#### How to create a Measure Table

    Go to power query editor -> select the Transform tab -> click on the "enter data" -> A new window will appear 
    -> No need to enter any data. It is just going to hold the measures -> Just Name the Table as '_01_Core_Measures' -> click OK
![creating measure](https://github.com/user-attachments/assets/12db0371-dad5-40a4-930a-339fe82ed9b9)


#### DAX Measures 

    DISTINCTCOUNT()
    - it is used to count the number of distinct values in a column
    total transaction = distinctcount(sales[sales_Id])

    COUNT()
    total products = count(product_dim[product_id])

    SUM()
    total sales = sum(sales[total sales])

    AVERAGE()
    average order size = average(sales[total sales])
    or
    DIVIDE()
    average order size = divide([total sales], [total transactions])
    
    RANKX()
    product sales rank = rankx(

    
In order to format the values to show in dollars and coma separated, select that particular measure and under measure tools, select currency, click on the $ symbol , coma icon and select the decimal place that you require as shown below
![formating values](https://github.com/user-attachments/assets/5d42c83e-246d-445a-8855-8bb89fab95f1)



# DAX 

| Syntax | Description | 
|---|---|
|CALENDARAUTO([fiscal_year_end_month]) | CALENDARAUTO Function (DAX)	Returns a table with a single column named “Date” that contains a contiguous set of dates. The range of dates is calculated automatically based on data in the model.|
|  CALENDAR(<start_date>, <end_date>) |  CALENDAR Function (DAX)	Returns a table with a single column named “Date” that contains a contiguous set of dates. The range of dates is from the specified start date to the specified end date, inclusive of those two dates. |


        
      

