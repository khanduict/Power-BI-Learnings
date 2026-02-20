# Power-BI-Learnings
Power BI Learnings

Uploading the data into Power BI
 - Create a new power bi report
 - Click on the Transform data icon and it will open power query editor
 - Under home tab, click on the New Source button, Drop down and click on the "More" tab
 - Select Folder and navigate to the folder path
 - Click on the Transform data button
 - Turn off "enable load". It will not be visible on the front end of the front end. It will be only visible to backend and power query.
 - Rename it as "Source data". It is the connection to the folder and will display all the files within that folder.
 - Right click on the "Source data", click on the "reference". Click on the the particular file (binary) that you want to open. It will unpack and allow to view its contents. Rename the file accordingly under the "queries" tab
 - Repeat the referencing step to unpack new files.
- To keep the files organised, select all the files which are not going to load in the frontend of the power bi, right click and move to a New Group. Rename the group it as "Source Tables"
- Now reference the files again from the "source table" to create Fact Tables and donot turn off the "enable load". Move it to a new group such as "Production Tables". This will be visible  on the frontend of the power bi.


Modeling
- Create a new "dim table" by referencing from the "source table"
- Rename the file (e.g department_dim)
- Select the "department" and "sub-department" and remove all other columns and also remove the duplicates by selecting both the columns
- Go to Add Column tab, click on the index column and add an index column which is starting "From 1". Rename it as "department_key". It will allow to keep in a smaller dim table for both the combination of the deparment and sub-department columns. So that we donot have to keep it in the Fact Table.
- However, we are going to need to create relationship between the Fact Table and Dim Table.
- Go back to the Fact Table, select the Home Tab and click on the "Merge Queries"
- You will see all of the Fact Table field.
- Click on the dropdown menu and select the deparment_dim
- Then we need to specify that we need to create join between the department and sub-deparment between the fact and dim table.
- Hold down on the CTRL keyboard tab and select department field on the fact table first, then select the deparment table on the dim table. Then select the sub-department field on the fact table first and then the sub-department field on the dim table.
- It is very important to notice that when we click on the department first on the fact table and dim table table later and sub-department on the fact table and later dim table, we will see numbers  1 and 2 as the join criteria.
- Then you can specify the Join Kind such as Left Outer, Righter Outer, Full Outer, Inner, Left Anti, Right Anti. For now, i have selected the Left Outer join and Click on OK button.
- Then you will see a join created (department_dim) on the fact table. Click on the two arrows icon and expand the table.
- Select only the column which we are going to bring in from the dim table. In this case, i am selecting the "department_key" and unselect "use original column name as prefix" box. Then click OK
- You will see the keys for the unique department labels which you created in the dim table. Now you got the unique keys for the department, we no longer need to have "department and sub-department" fields in the fact table. We just need the department_key to join the Fact table to the Deparment dim table once we load everything. So select department and sub-department columns and remove it from the fact table.
- Repeat the same process for creating a relationship between the Fact and the Dim Tables.
- Close and Apply the power query
- Go to the model view in the front end of power bi
- Create a new tab e.g rename it as employee data layout
- Arrange the Fact Table and Dim table accordingly

Cardinality
- Go to the model view
- For instance, power bi has automatically created a relationship as 1 to Many because department_dim should only have one value for each department_key and multiple corresponding value in the fact table.
- If you click on the arrow icon, you will see cross filter direction as single
- If the cardinality is one to one (1:1) , every corresponding value in the Fact table should match in the Dim table and vice versa. You will see the cross filter direction as both meaning it moves in both direction.

Transform birth Date to Age
- For instance if we want to transform birth date 1982 to age 44.
- Go to Transform tab -> Format -> Add Prefix -> Value -> 1/1/ and then click OK button
- Go to Transform tab -> Date Type -> Date
- Go to Transform tab -> Date -> Age
- Go to Transform tab -> Duration -> Total Years
- Go to Transform tab -> Date Type -> Whole Numbers

Transform Income from whole number to dollar
- Go to Transform tab -> Data Type -> select Fixed Decimal Number

Replacing values
- Right click on that particular field
- Select replace values
- Enter " Value to Find" and " Replace with"


 
  
