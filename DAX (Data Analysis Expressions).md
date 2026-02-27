

###  DAX (Data Analysis Expressions)
DAX is used to create powerful calculations in Power BI, helping us to analyse and visualize the data.

#### DAX Calculation Types - You can use DAX to add 3 types of calculations to the semantic models;
There are 3 types of DAX calculation namely
    - Calculated Tables - are used to create date tables or role-playing dimensions or to enable what-if analysis
    - Calculated Columns - can be added to tables in the model
    - Measures - achieves summarization over model data

##### Calculated columns
- It creates a physical data column
- Increases the storage size
- Can prolong data refresh time

How to create a Measure Table

    Go to power query editor -> select the Transform tab -> click on the "enter data" -> A new window will appear 
    -> No need to enter any data. It is just going to hold the measures -> Just Name the Table as '_01_Core_Measures' -> click OK
![creating measure](https://github.com/user-attachments/assets/12db0371-dad5-40a4-930a-339fe82ed9b9)


DAX Measures 

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
    
    

    
In order to format the values to show in dollars and coma separated, select that particular measure and under measure tools, select currency, click on the $ symbol , coma icon and select the decimal place that you require as shown below
![formating values](https://github.com/user-attachments/assets/5d42c83e-246d-445a-8855-8bb89fab95f1)
