# SQL_50_StudyPlan

## SELECT
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

## BASIC JOINS
Q.6 [Replace-employee-id-with-the-unique-identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT U.unique_id,E.name FROM Employees E LEFT JOIN EmployeeUNI U
ON U.id=E.id

Q.7 [Product-sales-analysis](https://leetcode.com/problems/product-sales-analysis-i/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT product_name,year,price FROM Sales S JOIN Product P
ON S.product_id=P.product_id

Q.8 [Customer-who-visited-but-did-not-make-any-transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT v.customer_id,count(v.visit_id) AS count_no_trans
FROM Visits v WHERE v.visit_id not in (SELECT t.visit_id FROM Transactions t) 
GROUP BY v.customer_id

Q.9 [Rising-temperature](https://leetcode.com/problems/rising-temperature/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT w1.id 
FROM Weather as w1, Weather as w2
WHERE datediff(w1.recordDate,w2.recordDate)=1 and w1.Temperature>w2.Temperature

Q.10 [Average-time-of-process-per-machine](https://leetcode.com/problems/average-time-of-process-per-machine/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT machine_id,
ROUND((SUM(CASE WHEN ACTIVITY_TYPE="end" THEN timestamp END)-
SUM(CASE WHEN ACTIVITY_TYPE="start" THEN timestamp END))/COUNT(CASE WHEN ACTIVITY_TYPE="start" THEN 1 END),3) as processing_time
FROM Activity
GROUP BY machine_id  

Q.11 [Employee-bonus](https://leetcode.com/problems/employee-bonus/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT E.name,B.bonus FROM Employee E LEFT JOIN Bonus B
ON E.empId=B.empId WHERE B.bonus < 1000 OR B.bonus is null;
Another Approach:-SELECT e.name, b.bonus from
    Employee e left join bonus b 
        USING(empId)
    where 
        ifnull(b.bonus, 0) <1000;

Q.12 [Students & Examination](https://leetcode.com/problems/students-and-examinations/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT s.student_id,s.student_name,sb.subject_name,count(e.subject_name) AS attended_exams FROM Students s CROSS JOIN Subjects sb LEFT JOIN Examinations e
ON s.student_id=e.student_id AND sb.subject_name=e.subject_name
GROUP BY s.student_id,s.student_name,sb.subject_name
ORDER BY S.student_id,sb.subject_name

### [Note]--Cross join tb krte ager dusre table me foreign key nhi mil raha ar self joi tb krte jb sirf ek table hain ar usme same data me comparison krna ho AND count ar group by tb lete jb distinct data ho wo count me lete ar jisme chahiye usko groupby me lete.

Q.13 [Managers-with-at-least-5-direct-reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT name FROM Employee WHERE id IN
(SELECT managerId FROM EMPLOYEE GROUP BY managerId HAVING count(*)>=5)

Q.14 [Confirmation-rate](https://leetcode.com/problems/confirmation-rate/?envType=study-plan-v2&id=top-sql-50)

Solution:-SELECT S.user_id,ROUND(AVG(case when action='confirmed' THEN 1 ELSE 0 END),2) AS confirmation_rate 
FROM Signups S
LEFT JOIN Confirmations C ON S.user_id=C.user_id
GROUP BY S.user_id;

## Basic Aggregate Function
Q.15 [Not-boring-movies](https://leetcode.com/problems/not-boring-movies/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT id,movie,description,rating FROM Cinema 
WHERE id%2!=0 And description!='boring'    
ORDER BY rating DESC;

Q.16 [Average Selling Price](https://leetcode.com/problems/average-selling-price/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT P.product_id,Round(SUM(U.units*P.price)/SUM(U.units),2) AS average_price FROM Prices P JOIN UnitsSold U
ON P.product_id=U.product_id
WHERE u.purchase_date between p.start_date AND p.end_date
GROUP BY P.product_id

Q.17 [Project Employees](https://leetcode.com/problems/project-employees-i/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT P.project_id,ROUND(AVG(E.experience_years),2) AS average_years FROM Project P LEFT JOIN Employee E ON P.employee_id=E.employee_id
GROUP BY P.project_id

Q.18 [Percentage-of-users-attended-a-contest](https://leetcode.com/problems/percentage-of-users-attended-a-contest/?envType=study-plan-v2&envId=top-sql-50)

Solution:-Select r.contest_id, round((count(distinct(r.user_id))*100/count(distinct(u.user_id))),2) as percentage
from users u, register r
group by r.contest_id
order by percentage desc,r.contest_id

Q.19 [Queries-quality-and-percentage](https://leetcode.com/problems/queries-quality-and-percentage/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT query_name,ROUND(AVG(rating/position),2) AS quality,ROUND(100*SUM(CASE WHEN rating < 3 THEN 1 ELSE 0 END)/COUNT(*),2) 
AS poor_query_percentage FROM Queries 
GROUP BY query_name

Q.20 [Monthly-transactions](https://leetcode.com/problems/monthly-transactions-i/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT DATE_FORMAT(trans_date, '%Y-%m') AS month,country,
COUNT(*) AS trans_count,SUM(IF(state='approved', 1,0)) AS approved_count,SUM(amount) AS trans_total_amount ,SUM(IF(state='approved', amount,0)) AS approved_total_amount 
FROM Transactions 
GROUP BY month,country
Note:-DATE_FORMAT(trans_date, '%Y-%m') -- for date format queries

Q.21 [Immediate-food-delivery](https://leetcode.com/problems/immediate-food-delivery-ii/?envType=study-plan-v2&envId=top-sql-50)

Solution:-select round(sum(if(order_date = customer_pref_delivery_date, 1, 0)) / count(*) * 100, 2) as immediate_percentage from Delivery
where (customer_id, order_date) in
(
    Select customer_id, min(order_date) from Delivery group by customer_id
)

Q.22 [Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv/?envType=study-plan-v2&envId=top-sql-50)

Solution:-select round(count(distinct a1.player_id)/(select count(distinct player_id) 
from activity),2) as fraction
from activity a1 join (select player_id, min(event_date) as event_date 
from activity group by 1) a2
on a1.player_id = a2.player_id and datediff(a1.event_date,a2.event_date) = 1;

## Sorting & Grouping
Q.23 [Number-of-unique-subjects-taught-by-each-teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT teacher_id,COUNT(distinct subject_id) AS cnt FROM Teacher
GROUP BY teacher_id

Q.24 [User-activity-for-the-past-30-days](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/description/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT activity_date AS day,COUNT(distinct user_id) AS active_users
FROM Activity WHERE DATEDIFF('2019-07-27',activity_date)<30
AND activity_date<'2019-07-27'
GROUP BY activity_date

Q.25 [Product Sales Analysis](https://leetcode.com/problems/product-sales-analysis-iii/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT product_id,year as first_year,quantity,price FROM Sales WHERE (product_id,year) in
(Select product_id,min(year)
from sales 
group by product_id)
Brute Force:-
SELECT S.product_id,min(S.year) as first_year,S.quantity,S.price
FROM Sales S LEFT JOIN Product P
ON S.product_id=P.product_id
GROUP BY product_id

Q.26 [Classes-more-than-5-students](https://leetcode.com/problems/classes-more-than-5-students/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT class FROM Courses
GROUP BY class
HAVING COUNT(class)>=5
