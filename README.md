# SQL-Crimes-Against-Females-in-India

SELECT *
  FROM CrimesAgainstWomenIndia

  ALTER TABLE CrimesAgainstWomenIndia
  ADD Crime_Type VARCHAR(50)

  UPDATE CrimesAgainstWomenIndia
  SET Crime_Type = Group_Name

  ALTER TABLE CrimesAgainstWomenIndia
  DROP COLUMN Group_Name

SELECT Crime_Type, Area_Name
FROM CrimesAgainstWomenIndia
WHERE Crime_Type <> 'Total Crime'
--GROUP BY Crime_Type
SELECT DISTINCT Crime_Type
FROM CrimesAgainstWomenIndia

SELECT Max(Total_Cases_for_Trial) TotalCasesForTrial, Crime_Type, Area_Name, Year
FROM CrimesAgainstWomenIndia
GROUP BY Crime_Type, Area_Name, Year
ORDER BY Crime_Type DESC, Area_Name DESC, Year DESC

--Number of Crime cases in different location in India
--CRIME CASES IN INDIA BY LOCATION
SELECT Area_Name, SUM(CAST(Total_Cases_for_Trial AS INT)) TotalCrimeCases
FROM CrimesAgainstWomenIndia
WHERE Crime_Type <> 'Total Crime'
GROUP BY Area_Name
ORDER BY TotalCrimeCases DESC

--TOTAL CRIME CASES AGAINST FEMALES IN THE WHOLE OF INDIA
SELECT SUM(CAST(Total_Cases_for_Trial AS INT)) TotalCrimeCasesIndia
FROM CrimesAgainstWomenIndia

--TOTAL CRIMES IN INDIA BY YEAR
SELECT YEAR--, Area_Name
, SUM(CAST(Total_Cases_for_Trial AS INT)) TotalCrimeCases
FROM CrimesAgainstWomenIndia
GROUP BY YEAR--, Area_Name
ORDER BY TotalCrimeCases DESC, YEAR 

--MOST COMMON TYPE OF CRIME AGAINST FEMALES IN INDIA
SELECT Crime_Type, SUM(Total_Cases_for_Trial) TotalCrimeCases
FROM CrimesAgainstWomenIndia
WHERE Crime_Type <> 'Total Crime'
GROUP BY Crime_Type
ORDER BY TotalCrimeCases DESC

--CONVICTED VS TOTAL CRIME CASES AGAINST FEMALES IN INDIA BY AREA IN PERCENTAGE
SELECT Area_Name
, (SUM(Cases_Convicted)/SUM(Total_Cases_for_Trial))*100 AreaPercentageCrime
FROM CrimesAgainstWomenIndia
WHERE Crime_Type <> 'Total Crime'
GROUP BY Area_Name
ORDER BY AreaPercentageCrime DESC
