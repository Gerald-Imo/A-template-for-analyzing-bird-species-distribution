<h1>SQL queries for anlysing species distribution</h1>

<h2>Description</h2>
These SQL queries function as template designed to be used in conjunction with .csv tables similar to "NCRN Bird Monitoring Data 2007 - 2017" dataset (available on www.data.gov). The Queries enable researchers to identify species diversity hotspots, track seasonal variations in species abundance, and evaluate the impact of habitat changes on species distributions
<br />

<h2>Potential users</h2>

- <b>Sustainable finance firms</b> 
- <b>Ecology researchers</b> 
- <b>Conservation agencies</b>

<h2>How to use effcectively</h2>

- <b>Download the "NCRN Bird Monitoring Data 2007 - 2017" dataset and use as data recording template</b>
- <b>Use the SQL queries wchich I provided below for your insight</b> 

<h2>SQL queries (Please note: best viewed under code section)</h2>

--To count the total number bird species:
SELECT COUNT(DISTINCT Scientific_Name) AS Species_Count
FROM ANTI
--To identify the location types:
SELECT DISTINCT Location_type from ANTI

--To count the number of observers:
SELECT COUNT(DISTINCT Observer) AS Observer_Count
FROM ANTI

--To identify the observer with the greatest number of birds sighted:
--Displaying the total number of birds observed by the respective observer:

SELECT Observer, COUNT(Scientific_name) AS Observer_Countings 
FROM ANTI
GROUP BY Observer
ORDER BY Observer_Countings DESC

--Total number of Male birds counted:
SELECT Sex, COUNT(Sex) AS MalesCounted 
FROM ANTI 
WHERE Sex = 'Male'
GROUP BY Sex 

--Counting Male Birds by Species:
SELECT Sex, Scientific_Name, COUNT(Scientific_Name) AS MalesCounted 
FROM ANTI 
WHERE Sex = 'Male'
GROUP BY Sex, Scientific_Name
ORDER BY MalesCounted DESC
--or--
SELECT Sex, Scientific_Name, COUNT(*) AS MalesCounted 
FROM ANTI 
WHERE Sex = 'Male'
GROUP BY Sex, Scientific_Name
ORDER BY MalesCounted DESC

--Total number of Female Birds counted:
SELECT Sex, COUNT(Sex) AS TotalFemalesCounted
FROM ANTI 
WHERE Sex = 'Female'
GROUP BY Sex

--Counting Female Birds by Species:
SELECT Sex, Scientific_Name, COUNT(Scientific_Name) AS FemalesCounted 
FROM ANTI 
WHERE Sex = 'Female'
GROUP BY Sex, Scientific_Name
ORDER BY FemalesCounted DESC

--Total number of birds of undetermined gender counted:
SELECT Sex, COUNT(Sex) AS UndeterminedGender
FROM ANTI 
WHERE Sex = 'Undetermined'
GROUP BY Sex

--Counting the undetermined genders by Species:
SELECT Sex, Scientific_Name, COUNT(Scientific_Name) AS UndeterminedGender 
FROM ANTI 
WHERE Sex = 'Undetermined'
GROUP BY Sex, Scientific_Name
ORDER BY UndeterminedGender DESC

--To identify where NULL value exists in respect of sex:
SELECT Observer, Scientific_Name, COUNT(Scientific_name) AS 'Undetermined(Null)' 
FROM ANTI
WHERE Sex IS NULL
GROUP BY Observer, Scientific_Name
ORDER BY 'Undetermined(Null)' DESC

--To identify the observer with the greatest number of birds observations at height 50 to 100 meters:
SELECT Observer, COUNT(Scientific_name) AS Observer_Countings 
FROM ANTI
WHERE Distance = '50 - 100 Meters'
GROUP BY Observer
ORDER BY Observer_Countings DESC

--To identify the bird species sighted within high altitude ranges:
SELECT Common_Name, Scientific_Name, COUNT(Scientific_Name) AS High_flyers 
FROM ANTI
WHERE Distance = '50 - 100 Meters'
GROUP BY Common_Name, Scientific_Name
ORDER BY High_flyers DESC
--or--
SELECT Scientific_Name, COUNT(*) AS High_flyers 
FROM ANTI
WHERE Distance = '50 - 100 Meters'
GROUP BY Scientific_Name
ORDER BY High_flyers DESC

--To identify the bird species sighted within low altitude ranges:
SELECT Scientific_Name, COUNT(*) AS Low_flyers 
FROM ANTI
WHERE Distance = '<= 50 Meters'
GROUP BY Scientific_Name
ORDER BY Low_flyers DESC
--or--
SELECT Scientific_Name, COUNT(Scientific_Name) AS Low_flyers 
FROM ANTI
WHERE Distance = '<= 50 Meters'
GROUP BY Scientific_Name
ORDER BY Low_flyers DESC

--To identify the bird species sighted within low altitude ranges in the forest area:
SELECT Common_Name, Scientific_Name, COUNT(*) AS Low_flyers_Forest 
FROM ANTI
WHERE Distance = '<= 50 Meters' and Location_Type = 'forest'
GROUP BY Common_Name, Scientific_Name
ORDER BY Low_flyers_Forest DESC

--To identify the bird species sighted within high altitude ranges in the grassland area:
SELECT Common_Name, Scientific_Name, COUNT(*) AS High_flyers_Grassland 
FROM ANTI
WHERE Distance = '50 - 100 Meters' and Location_Type = 'Grassland'
GROUP BY Common_Name, Scientific_Name
ORDER BY High_flyers_Grassland DESC

--to identify the most frequently sighted male in the forest region:
SELECT MAX(DISTINCT Scientific_name) AS Scientific_Name, 
COUNT(DISTINCT Scientific_name) AS MostSighted_Male_Forest 
FROM ANTI
WHERE Sex = 'Male' AND Location_Type = 'Forest'
ORDER BY MostSighted_Male_Forest DESC

--to identify the most frequently sighted female in the Forest region:
SELECT MAX(DISTINCT Scientific_name) AS Scientific_Name, 
COUNT(DISTINCT Scientific_name) AS MostSighted_Female_Forest 
FROM ANTI
WHERE Sex = 'Female' AND Location_Type = 'Forest'
ORDER BY MostSighted_Female_Forest DESC

--to identify the most frequently sighted male in the Grassland region:
SELECT MAX(DISTINCT Scientific_name) AS Scientific_Name, 
COUNT(DISTINCT Scientific_name) AS MostSighted_Male_Grassland 
FROM ANTI
WHERE Sex = 'Male' AND Location_Type = 'Grassland'
ORDER BY MostSighted_Male_Grassland DESC

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
