

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
|CALENDARAUTO([fiscal_year_end_month]) | The date range returned is dates between the begining of the fiscal year associated with MinDate and the end of the fiscal year associated with MaxDate|
|  CALENDAR(<start_date>, <end_date>) |  CALENDAR Function (DAX)	Returns a table with a single column named “Date” that contains a contiguous set of dates. The range of dates is from the specified start date to the specified end date, inclusive of those two dates. |
|CALENDARAUTO() | In this example, the MinDate and MaxDate in the data model are July 1, 2010 and June 30, 2011 ...Return all dates between January 1, 2010 and December 31, 2011 |
|CALENDERAUTO(3) | Return all dates between March 1, 2010 and February 28, 2012) |
|CALENDER(<start_date>, <end_date>) | Example- The following formula returns a table with dates between January 1st 2005 and December 31st 2015. = CALENDER(DATE(2005,1,1), DATE((2015,12,31))...Example 2 - For a data model which includes actual sates datea and future sales forecasts. The following expression returns the date table covering the range of dates in these two tables. = CALENDAR (MINX (Sales, [Date]), MAXX (Forecast, [Date])) |



            DateTable = 
          ADDCOLUMNS ( 
          CALENDAR(MINX('sales','sales'[date]),MAXX('sales','sales'[date])),
          "DateAsInteger", FORMAT ( [date], "YYYYMMDD" ),
           "Year", YEAR ( [date] ), "MonthNo", FORMAT ( [date], "MM" ), 
          "YearMonthNo", FORMAT ( [date], "YYYY/MM" ), 
          "YearMonth", FORMAT ( [date], "YYYY/mmm" ), 
          "MonthShort", FORMAT ( [date], "mmm" ),
          "MonthLong", FORMAT ( [date], "mmmm" ), 
          "WeekNo", WEEKDAY ( [date] ), 
          "WeekDay", FORMAT ( [date], "dddd" ), 
          "WeekDayShort", FORMAT ( [date], "ddd" ), 
          "Quarter", "Q" & FORMAT ( [date], "Q" ), 
          "YearQuarter", FORMAT ( [date], "YYYY" ) & "/Q" & FORMAT ( [date], "Q" ))

            
            
        
      

