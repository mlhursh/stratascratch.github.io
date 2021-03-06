# Basic SQL Exercises (*with Solutions*)

## Instructions
- Log-in to your Strata Scratch account.
- All tables used in this exercise are taken from the datasets schema. Make sure you select this schema on the SQL editor settings.
- Try to answer the following questions by writing the appropriate SQL query on the editor.
- This is the teacher version of the SQL basic exercises. Each question is followed with the correct solution and output.

## Questions
1. How many of passengers embarked on the Titanic? 
   
   `Table: datasets.titanic`
   
   *Solution:*
   
   To know the number of passengers, we need to count the distinct names on the `datasets.titanic` table. The following query will give
   us an answer of 891 passengers.
   ```sql
      SELECT count(distinct name)
      FROM datasets.titanic
   ```  
   *Output:* `891`
   
2. How many passengers were in first class (pclass =1), a woman, and survived (survived = 1)?
   
   `Table: datasets.titanic`
   
   *Solution:*
   
   Here, we want to know the number of women who were in the first class and survived. So we count the number of distinct `passengerid`
   and add other parameters, such as `pclass`, `sex` and `survived`. 
   ```sql
      SELECT
        count(distinct passengerid)
      FROM datasets.titanic
      WHERE
        pclass = 1
        AND sex = 'female'
        AND survived = 1
   ```
   *Output:* `91`
   
3. How many athletes participated in the 2014 combine?
   
   `Table: datasets.nfl_combine`
   
   *Solution:*
   
   To know the number of athletes who participated in the 2014 combine, we count the number of distinct names from the 
   `datasets.nfl_combine` table. Then we add a condition year equal to 2014 to filter out our data.
   ```sql
      SELECT count(distinct name)
      FROM datasets.nfl_combine
      WHERE year = '2014'
   ```
   *Output:* `335`
   
4. What is the average weight of all the athletes?
   
   `Table: datasets.nfl_combine`
   
   *Solution:*
   
   In our solution, we use the `avg` function to compute the average weight of all the athletes listed on the table. The result should display the average weight `245.6` as the answer on the SQL editor.
   ```sql
      SELECT
        avg(weight)
      FROM datasets.nfl_combine
   ```
   *Output:* `245.6`
   
5. How many athletes were drafted into NFL in 2015?
   
   `Table: datasets.nfl_combine`
   
   *Solution:*
   
   We can count the number of athletes drafted into NFL by counting the distinct name from the `datasets.combine` table. We added the conditions to select data only within the year 2015 and the column should not contain a null value.
   ```sql
      SELECT
        count(distinct name)
      FROM datasets.combine
      WHERE year = 2015
      AND (pickround NOTNULL or pickround <> '0')
   ```
   *Output:* `321`
   
6. How many accounts performed a login in 2016?
   
   `Table: datasets.product_logins`
   
   *Solution:*
   
   To solve the problem, we simply count the number of distinct account ids from the table. We filter the data by counting only those within the log in date between `2016-01-01` and `2016-12-31.`
   ```sql
      SELECT 
        count(distinct account_id)
      FROM datasets.product_logins
      WHERE login_date BETWEEN '2016-01-01' and '2016-12-31'
   ```
   *Output:* `156832`
   
7. What were the top 10 songs in 2010?
   Include the rank, group name, and song name from highest ranked song to lowest.
   
   `Table: datasets.billboardtop_100year_end`
   
   *Solution:*
   
   To know the top 10 songs, we first select the rank, the group name and the song name. Since we want to know the top 10 songs in 2010, a condition statement was added which include the year and rank. To combine the same songs who where ranked many times, we include the `GROUP BY` statement and sorted the data in ascending order through the `ORDER BY` and `ASC` statements.
   ```sql
      SELECT
        year_rank as rank, 
        "group" as group_name,
        song_name as song_name
      FROM datasets.billboard_top_100_year_end
      WHERE year = 2010
      AND year_rank BETWEEN 1 and 10
      GROUP BY 1,2,3
      ORDER BY year_rank ASC
   ```
   *Output:*
   
   ![strata scratch](assets/1.png)
   
8. What is Samantha’s and Lisa’s total sales revenue?

   `Table: datasets.sales_performance`
   
   *Solution:*
   
   To get the total sales revenue, we simply solved for the sum of the sales revenue from the table. We only added the data generated by Samantha and Lisa through a condition on the last statement.
   ```sql
      SELECT
        sum(sales_revenue) as total_revenue
      FROM datasets.sales_performance
      WHERE salesperson = 'Samantha' or salesperson = 'Lisa'
   ```
   *Output:* `112650`
   
9. What is the average SAT score by school? Rank by highest average SAT score

   `Table: datasets.sat_scores`
   
   *Solution:*
   
   We solve for the average SAT score by summing up the `sat_math`, `sat_verbal` and `sat_writing` from the dataset. The data is then grouped and sorted in descending order through the `GROUP BY`, `ORDER BY` and `DESC` clauses.
   ```sql
      SELECT
        school, 
        avg(sat_math + sat_verbal + sat_writing) as avg_sat_score
      FROM datasets.sat_scores
      GROUP BY 1
      ORDER BY avg_sat_score DESC
   ```
   *Output:*
   
   ![strata scratch](assets/2.png)
   
10. Count the number of user events by `event_name` from users on a macbook pro.
    Output should be ranked with highest event count first.

    `Table: datasets.playbook_events`
    
    *Solution:*
    
    Here, we want to count the number of user events through the SELECT statement by including the event name and count the number of events. Since we are only concerned with macbook pro users, this condition is added through the `WHERE` statement, followed by the `GROUP BY`, `ORDER BY` and `DESC` clauses to group and sort the data in descending order.
    ```sql
       SELECT
         event_name,
         count(*) as event_count
       FROM datasets.playbook_events
       WHERE device = 'macbook pro'
       GROUP BY 1
       ORDER BY event_count DESC
    ```
    *Output:*
    
    ![strata scratch](assets/3.png)
    


