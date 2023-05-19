# SQL_50_StudyPlan

Q.1 [Recyclable-and-low-fat-products](https://leetcode.com/problems/recyclable-and-low-fat-products/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT product_id FROM Products where low_fats='Y' and recyclable='Y'

Q.2 [Find-customer-referee](https://leetcode.com/problems/find-customer-referee/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT name FROM Customer WHERE referee_id!=2 or referee_id is null
