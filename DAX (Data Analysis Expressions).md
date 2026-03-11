

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


*NOTE - Always keep all the DAX measures under one table. In the front end, under the HOME tab, click on "enter data" . There is no need to enter any data. Just name the table as _Key Measures Tables and click on the load. You will see the table. Now right click on that table and create new measures.
Alternately, you can also create measure table in the power query editor as well.*

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



# DAX - DATE table

| Syntax | Description | 
|---|---|
|CALENDARAUTO([fiscal_year_end_month]) | The date range returned is dates between the begining of the fiscal year associated with MinDate and the end of the fiscal year associated with MaxDate|
|  CALENDAR(<start_date>, <end_date>) |  CALENDAR Function (DAX)	Returns a table with a single column named “Date” that contains a contiguous set of dates. The range of dates is from the specified start date to the specified end date, inclusive of those two dates. |
|CALENDARAUTO() | In this example, the MinDate and MaxDate in the data model are July 1, 2010 and June 30, 2011 ...Return all dates between January 1, 2010 and December 31, 2011 |
|CALENDERAUTO(3) | Return all dates between March 1, 2010 and February 28, 2012) |
|CALENDER(<start_date>, <end_date>) | Example- The following formula returns a table with dates between January 1st 2005 and December 31st 2015. = CALENDER(DATE(2005,1,1), DATE((2015,12,31))...Example 2 - For a data model which includes actual sates datea and future sales forecasts. The following expression returns the date table covering the range of dates in these two tables. = CALENDAR (MINX (Sales, [Date]), MAXX (Forecast, [Date])) |




### How to create a DATE TABLE .. Below is the template to create a new DATE TABLE
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

            
            
if statement 
if the condition is true then we put this one otherwise show this one
For e.g sample column = if (sampleTable[sampleColumn] = " ", BLANK(), SampleTable[SampleColumn])


# DAX - Aggregation function

| Syntax | Description | 
|---|---|
|AVERAGE( ) | example  - Average sales quantity = AVERAGE(sales[quantity]) |
|  MAX ( ) |  example - calculating the maximum value of a column - Maximum of sales quantity = MAX (sales [quantity]) |
|SUM ( ) | calculating the sum of quantity - for example - Sample measure = SUM(sales[quantity]) |
| COUNT ( ) | e.g sample measure count = COUNT(sampleTable[sampleColumn])  ..it will not count rows which are blank...|
| COUNTROWS( ) | e.g sample measure count = COUNTROWS(sampleTable[sampleColumn])  ..it will count all the rows in table including blanks |
| COUNTA( ) | The function COUNT( ) cannot work with values of type Boolean (true or false)..In this case, we have use to use COUNTA( ) ..e.g sample measure count = COUNTA(sampleTable[sampleColumn]) |
| DISTINCTCOUNT ( ) | The function DISTINCTCOUNT( ) will count all the distinct values including the empty values ..e.g sample measure count = DISTINCTCOUNT(sampleTable[sampleColumn]) |
| COUNTBLANK( ) | The function COUNTBLANK( ) counts the blank values e.g sample measure count = BLANKCOUNT(sampleTable[sampleColumn]) |
| AVERAGE ( ) or COUNTAX ( ) | the function AVERAGE( ) counts the average values howeever we can also use COUNTAX( ) |


# DAX - Different version of Aggregation function with "X" in the end

| Syntax | Description | 
|---|---|
|SUMX( ) | example  - in calculated column we can can write the formula as revenue = sales[quantity] * sales[price].. in the measures  we cannot write  like this  revenue measure = SUM(sales[quantity]) * SUM(sales[price])..this is wrong ...the result is not correct... we have to use SUMX( )..what this will do is first it take the multiplication of quantity and price (e.g revenue = sales[quantity] * sales[price] and then take the SUM ..e.g Revenue measure = SUMX(table, expression)  ..revenue measure = SUMX(sales, sales[quantity] * sales[price])..what it does is, first it calculates at the row level and then it is stored in the memory then it takes the SUM |
| AVERAGEX( ) | similary we can use AVERAGEX ( ) function using measures |


Exercise
### SUMX vs. SUM and AVERAGEX vs AVERAGE
The AVERAGEX function works just like the SUMX function.
Sometimes you have to use the RELATED function as well.

Question 1:

What is the average price of our products?
Would you use the AVERAGE or AVERAGEX function?
Hint: The "amount" of sales is NOT considered, so each product is considered equally.
Answer: 3,88.

Solution 1:
Average Product Price = AVERAGE( products[price] )


Question 2 (more difficult):
What is the average profit of our sold products?
(not considering how many of these are sold, so that in average every product is just counted once)
Would you use the Average or AverageX Function?
Hint 1: Amount of sales should not be considered.
Hint 2: Work on the products table
Hint 3: profit = price * profit margin
Answer: 0,78$.

Solution 2:
Average profit = AVERAGEX(products,products[price]*products[profit margine])


Question 3:
What is the total quantity of our sales?
Answer:  35377.

Solution 3:
Sum of quantity = SUM( sales[quantity] )

Question 4 (a bit more difficult):
What is the total profit of our sold products?
Hint 1: SUM or SUMX?
Hint 2: Use the RELATED function.
Answer:  27.612,70$.

Solution 4:
Total of profit = SUMX(sales, sales[price] * sales[quantity] * RELATED( products[profit margine] ))

Question 5 (also a bit more difficult):
What is the average tax amount we pay in our sales?
Hint: Use the RELATED function for the tax rate and the AVERAGEX function in the sales table.
Answer:  1,42$.

Solution 5:
Average Tax amount = AVERAGEX(sales, sales[price] * sales[quantity] * RELATED(products[tax rate]))


# Filter context vs Row context

        Revenue LastYear = CALCULATE('key measures table'[Revenue Measure], SAMEPERIODLASTYEART(DateTable[Date]))
        Revenue filtered by a state = CALCULATE ([Revenue Measure], location[state] = "Utan"
        Revenue filtered by a state = CALCULATE([Revenue Measure], FILTER(location , location[state] = "Utah"))
        SampleFilterTable = FILTER( products, products[price] > 5 )
        
        
        

















































      

