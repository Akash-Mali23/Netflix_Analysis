SELECT TOP (10) [Users]
      ,[Country]
      ,[Subscription_type]
      ,[Age]
      ,[Generation]
      ,[watchtime_hours]
      ,[Type_of_viewer]
      ,[Genre]
      ,[Last_Login]
      ,[Login_status]
  FROM [MySQL_project].[dbo].[netflix_analysis]

 USE MySQL_project;
SELECT * FROM dbo.netflix_analysis;

--==================================================================================
  --questions begins
 --=================================================================================
  --which top 10 countries has most number of netflix users?
SELECT TOP 10 Country, COUNT(*) AS User_Count  
FROM netflix_analysis  
GROUP BY Country  
ORDER BY User_Count DESC;
--==================================================================================
--least netflix using countries
SELECT TOP 5 Country, COUNT(*) AS least_users  
FROM netflix_analysis  
GROUP BY Country  
ORDER BY least_users ASC;
--=====================================================================================
-- subscription type by country
select * from netflix_analysis where Subscription_type ='Premium'
--========================================================================================
--which countries have high numbers of primium users?
select top (5) Country , count(*) as most_premium_users from netflix_analysis group by Country order by most_premium_users desc;
--=========================================================================================
--1 User Distribution & Growth

-- What is the total number of users in each country?
select country , count(*) as Total_number_of_users from netflix_analysis group by Country order by Total_number_of_users Desc;

-- What is the average age of users per country?
select country, AVG(Age) as Average_Age_per_country from netflix_analysis group by Country
 
--============================================================================================
 --Which subscription type has the highest watch time?
SELECT Subscription_type, SUM(watchtime_hours) AS Total_Watchtime
FROM netflix_analysis
WHERE watchtime_hours <= 899
GROUP BY Subscription_type
ORDER BY Total_Watchtime DESC;

 --What is the average watch time for each subscription type?
 SELECT Subscription_type, AVG(watchtime_hours) AS Total_Watchtime
FROM netflix_analysis
WHERE watchtime_hours <= 899
GROUP BY Subscription_type
ORDER BY Total_Watchtime DESC;
--====================================================================================================
--Which subscription type has the most lost users?
SELECT Subscription_type, COUNT(*) AS Lost_Users
FROM netflix_analysis
WHERE Login_status = 'Lost User' -- Change this if needed
GROUP BY Subscription_type
ORDER BY Lost_Users DESC;

--Which Country has the most lost users?
SELECT Country, COUNT(*) AS Lost_Users
FROM netflix_analysis
WHERE Login_status ='Lost User'  
GROUP BY Country
ORDER BY Lost_Users DESC;

--Which Country has the most Dormant users?
SELECT Country, COUNT(*) AS Dormant_User
FROM netflix_analysis
WHERE Login_status ='Dormant User'
GROUP BY Country
ORDER BY Dormant_User DESC;

--Which Country has the most Recently  inactive users?
SELECT Country, COUNT(*) AS Recently_Inactive
FROM netflix_analysis
WHERE Login_status ='Recently Inactive'
GROUP BY Country
ORDER BY Recently_Inactive DESC;


--Which country has the most Hardcore Viewers?
SELECT TOP 1 Country, COUNT(*) AS Hardcore_Viewers_Count  
FROM netflix_analysis  
WHERE Type_of_viewer = 'Hardcore Viewer'  
GROUP BY Country  
ORDER BY Hardcore_Viewers_Count DESC;
--================================================================================
--Which genre is the most popular among users?
SELECT TOP 1 Genre, COUNT(*) AS Genre_Count  
FROM netflix_analysis  
GROUP BY Genre  
ORDER BY Genre_Count DESC;

--What is the average watch time per user type?
SELECT Type_of_viewer, AVG(watchtime_hours) AS Avg_Watchtime  
FROM netflix_analysis  
GROUP BY Type_of_viewer  
ORDER BY Avg_Watchtime DESC;

--Which country has the most Gen Z users?
SELECT TOP 1 Country, COUNT(*) AS GenZ_Users_Count  
FROM netflix_analysis  
WHERE Generation = 'Gen Z'  
GROUP BY Country  
ORDER BY GenZ_Users_Count DESC;

--Which generation is the most active in the last 3 months?
SELECT TOP 1 Generation, COUNT(*) AS Active_Users  
FROM netflix_analysis  
WHERE Last_Login >= DATEADD(MONTH, -3, GETDATE())  
GROUP BY Generation  
ORDER BY Active_Users DESC;

--What is the most popular genre among different generations?
SELECT Generation, Genre, COUNT(*) AS Genre_Count  
FROM netflix_analysis  
GROUP BY Generation, Genre  
ORDER BY Generation, Genre_Count DESC;
--========================================================================
--How many users are Lost vs Dormant?
SELECT Login_status, COUNT(*) AS User_Count  
FROM netflix_analysis  
WHERE Login_status IN ('Lost User', 'Dormant User')  
GROUP BY Login_status;

--Which generation has the most lost users?
SELECT TOP 1 Generation, COUNT(*) AS Lost_Users_Count  
FROM netflix_analysis  
WHERE Login_status = 'Lost User'  
GROUP BY Generation  
ORDER BY Lost_Users_Count DESC;

--Which country has the highest percentage of lost users?
SELECT Country,  
       COUNT(CASE WHEN Login_status = 'Lost User' THEN 1 END) * 100 / COUNT(*) AS Lost_User_Percentage  
FROM netflix_analysis  
GROUP BY Country  
ORDER BY Lost_User_Percentage DESC;











