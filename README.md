# SQL_50_StudyPlan

Q.1 [Recyclable-and-low-fat-products](https://leetcode.com/problems/recyclable-and-low-fat-products/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT product_id FROM Products where low_fats='Y' and recyclable='Y'

Q.2 [Find-customer-referee](https://leetcode.com/problems/find-customer-referee/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT name FROM Customer WHERE referee_id!=2 or referee_id is null;
SELECT name FROM Customer WHERE coalesce(referee_id,'')!=2

Q.3 [Big-countries](https://leetcode.com/problems/big-countries/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT name,population,area FROM World WHERE area>=3000000 or population>=25000000

Q.4 [Article-views-i](https://leetcode.com/problems/article-views-i/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT author_id as id FROM Views
WHERE author_id=viewer_id
GROUP BY author_id
ORDER BY author_id;

Q.5 [Invalid-tweets](https://leetcode.com/problems/invalid-tweets/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT tweet_id FROM Tweets 
WHERE length(content) > 15;
