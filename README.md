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
GROUP BY machine_id ;
ANOTHER APPROACH:-SELECT a.machine_id,ROUND(AVG(b.timestamp-a.timestamp),3) AS processing_time 
FROM Activity a JOIN Activity b
ON a.machine_id =b.machine_id AND a.process_id=b.process_id AND a.activity_type='start' AND b.activity_type='end'
GROUP BY a.machine_id

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

Q.27 [Followers Count](https://leetcode.com/problems/find-followers-count/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT user_id,count(follower_id) AS followers_count
FROM Followers 
GROUP BY user_id
ORDER BY user_id

Q.28 [Biggest-single-number](https://leetcode.com/problems/biggest-single-number/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT MAX(num) as num FROM MyNumbers WHERE num IN (SELECT num FROM MyNumbers GROUP BY num
HAVING COUNT(*)=1)

Q.29 [Customers-who-bought-all-products](https://leetcode.com/problems/customers-who-bought-all-products/description/?envType=study-plan-v2&envId=top-sql-50)

Solution:-select customer_id from customer
group by customer_id
having count(distinct product_key)=(select count(distinct product_key) from product)

## Advanced Select and Joins

Q.30 [Number-of-employees-which-report-to-each-employee](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT E.employee_id,E.name,COUNT(M.reports_to) AS reports_count,
ROUND(AVG(M.AGE),0) AS average_age
FROM Employees E JOIN Employees M
ON E.employee_id=M.reports_to
GROUP BY E.employee_id,E.name
ORDER BY E.employee_id

Q.31 [Primary-department-for-each-employee](https://leetcode.com/problems/primary-department-for-each-employee/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT employee_id,department_id FROM Employee WHERE primary_flag='Y'
UNION ALL
SELECT employee_id,department_id FROM Employee GROUP BY employee_id HAVING COUNT(department_id)=1
APPROACH2:-SELECT employee_id,department_id FROM Employee WHERE primary_flag='Y'
OR (employee_id,department_id) IN (SELECT employee_id,department_id FROM Employee
GROUP BY employee_id HAVING COUNT(department_id)=1)

Q.32 [Triangle-judgement](https://leetcode.com/problems/triangle-judgement/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT x,y,z,CASE WHEN (x+y>z and x+z>y and y+z>x) THEN 'Yes' ELSE 'No'
END AS triangle 
FROM Triangle 

Q.33 [Consecutive-numbers](https://leetcode.com/problems/consecutive-numbers/description/?envType=study-plan-v2&envId=top-sql-50)

Solution:-select distinct l1.num AS ConsecutiveNums from logs l1,logs l2,logs l3
where l1.id = l2.id+1 and l2.Id=l3.Id+1
and l1.Num=l2.Num and l2.Num=l3.Num

Q.34 [Product-price-at-a-given-date](https://leetcode.com/problems/product-price-at-a-given-date/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT distinct a.product_id,coalesce(b.new_price,10) AS price FROM Products a
LEFT JOIN
(
SELECT product_id,rank() over(partition by product_id ORDER BY change_date desc)
AS rank,new_price FROM Products WHERE change_date <='2019-08-16'
) AS B
ON a.product_id=b.product_id AND b.rank=1
ORDER BY price desc;

Q.35 [Last-person-to-fit-in-the-bus](https://leetcode.com/problems/last-person-to-fit-in-the-bus/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT person_name FROM
(SELECT person_name,turn,
sum(weight) OVER(ORDER BY turn) AS rnk FROM Queue) a
WHERE rnk<=1000
ORDER BY turn desc limit 1

Q.36 [Count-salary-categorie](https://leetcode.com/problems/count-salary-categories/description/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT "High Salary" AS category,COUNT(*) AS accounts_count FROM Accounts WHERE income > 50000
UNION ALL
SELECT "Low Salary" AS category,COUNT(*) AS accounts_count FROM Accounts WHERE income < 20000
UNION ALL
SELECT "Average Salary" AS category,COUNT(*) AS accounts_count FROM Accounts WHERE income BETWEEN 20000 AND 50000;

## Subqueries

Q.37 [Employees-whose-manager-left-the-company](https://leetcode.com/problems/employees-whose-manager-left-the-company/description/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT employee_id FROM Employees WHERE salary < 30000 AND manager_id NOT IN
(SELECT employee_id FROM Employees) 
ORDER BY employee_id

Q.38 [Exchange-seats](https://leetcode.com/problems/exchange-seats/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT id,CASE WHEN id%2=0 THEN (lag(student) OVER (order by id))
ELSE IFNULL(lead(student) OVER(ORDER BY id),student)
END AS student
FROM Seat

Q.39 [Movie-rating](https://leetcode.com/problems/movie-rating/?envType=study-plan-v2&envId=top-sql-50)

Solution:-(SELECT name AS "results" FROM Users U JOIN MovieRating MR ON U.user_id=MR.user_id GROUP BY name ORDER BY COUNT(rating) desc,name limit 1) UNION ALL (SELECT title AS "results" FROM Movies M JOIN MovieRating MR ON M.movie_id=MR.movie_id WHERE created_at between '2020-02-01' and '2020-02-29' GROUP BY title ORDER BY AVG(rating) desc,title limit 1)

Q.40 [Restaurant-growth](https://leetcode.com/problems/restaurant-growth/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT visited_on, amount, ROUND(amount/7, 2) AS average_amount
FROM (
    SELECT DISTINCT visited_on, 
    SUM(amount) OVER(ORDER BY visited_on RANGE BETWEEN INTERVAL 6 DAY   PRECEDING AND CURRENT ROW) amount, 
    MIN(visited_on) OVER() 1st_date 
    FROM Customer
) t
WHERE visited_on>= 1st_date+6;

Q.41 [Friend-requests-ii-who-has-the-most-friends](https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends/?envType=study-plan-v2&envId=top-sql-50)

Solution:-WITH A AS (select requester_id as id from RequestAccepted
union all
select accepter_id as id from RequestAccepted)
SELECT id,count(id) as num FROM A
GROUP BY id
ORDER BY num desc limit 1

Q.42 [Investments-in-2016](https://leetcode.com/problems/investments-in-2016/?envType=study-plan-v2&envId=top-sql-50)

Solution:-WITH A AS (
    SELECT pid,tiv_2015,tiv_2016, COUNT(CONCAT(lat,lon)) over (partition by CONCAT(lat,lon)) AS CNT1,COUNT(tiv_2015) over (partition by (tiv_2015)) AS CNT2 FROM Insurance 
)
SELECT ROUND(SUM(tiv_2016),2) AS tiv_2016 FROM A WHERE CNT1=1 AND CNT2!=1

Q.43 [Department-top-three-salaries](https://leetcode.com/problems/department-top-three-salaries/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT D.Name as Department, E.Name as Employee, E.Salary 
FROM Department D, Employee E, Employee E2  
WHERE D.ID = E.DepartmentId and E.DepartmentId = E2.DepartmentId and 
E.Salary <= E2.Salary
group by D.ID,E.Name having count(distinct E2.Salary) <= 3
order by D.Name, E.Salary desc

## Advanced String Functions / Regex / Clause

Q.44 [Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT user_id,CONCAT(UPPER(SUBSTRING(name,1,1)),LOWER(SUBSTRING(name,2))) AS name
FROM Users ORDER BY user_id

Q.45 [Patients-with-a-condition](https://leetcode.com/problems/patients-with-a-condition/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT patient_id,patient_name,conditions FROM Patients 
WHERE conditions LIKE '% DIAB1%' OR conditions LIKE 'DIAB1%'

Q.46 [Delete-duplicate-emails](https://leetcode.com/problems/delete-duplicate-emails/?envType=study-plan-v2&envId=top-sql-50)

Solution:-delete p2
from person p1,person p2
where p1.email=p2.email and p2.id>p1.id;

Q.47 [Second-highest-salary](https://leetcode.com/problems/second-highest-salary/?envType=study-plan-v2&envId=top-sql-50)

Solution:-Select max(salary) as SecondHighestSalary from Employee
where salary< (Select max(salary) from Employee)

Q.48 [Group-sold-products-by-the-date](https://leetcode.com/problems/group-sold-products-by-the-date/?envType=study-plan-v2&envId=top-sql-50)

Solution:-Select sell_date,count(distinct product) as num_sold,group_concat(distinct product)
as products
from Activities
group by sell_date

Q.49 [List-the-products-ordered-in-a-period](https://leetcode.com/problems/list-the-products-ordered-in-a-period/?envType=study-plan-v2&envId=top-sql-50)

Solution:-Select p.product_name,sum(o.unit) as unit from
Products p join Orders o
on p.product_id=o.product_id
where MONTH(order_date)=2 and YEAR(order_date)=2020
group by p.product_name
Having unit>=100

Q.50 [Find-users-with-valid-e-mails](https://leetcode.com/problems/find-users-with-valid-e-mails/?envType=study-plan-v2&envId=top-sql-50)

Solution:-SELECT * FROM Users 
WHERE mail regexp '^[a-zA-Z][a-zA-Z0-9-._]*@leetcode[.]com'
