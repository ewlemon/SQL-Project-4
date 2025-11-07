###############
# Creating and Importing table
###############

USE home_schema;

CREATE TABLE chronic_disease (
    YearStart INT,
    YearEnd INT,
    LocationAbbr VARCHAR(10),
    LocationDesc VARCHAR(255),
    DataSource VARCHAR(100),
    Topic VARCHAR(255),
    Question TEXT,
    Response VARCHAR(255),
    DataValueUnit VARCHAR(50),
    DataValueType VARCHAR(100),
    DataValue FLOAT,
    DataValueAlt FLOAT,
    DataValueFootnoteSymbol VARCHAR(10),
    DataValueFootnote TEXT,
    LowConfidenceLimit FLOAT,
    HighConfidenceLimit FLOAT,
    StratificationCategory1 VARCHAR(100),
    Stratification1 VARCHAR(100),
    StratificationCategory2 VARCHAR(100),
    Stratification2 VARCHAR(100),
    StratificationCategory3 VARCHAR(100),
    Stratification3 VARCHAR(100),
    Geolocation VARCHAR(255),
    LocationID INT,
    TopicID VARCHAR(50),
    QuestionID VARCHAR(50),
    ResponseID VARCHAR(50),
    DataValueTypeID VARCHAR(50),
    StratificationCategoryID1 VARCHAR(50),
    StratificationID1 VARCHAR(50),
    StratificationCategoryID2 VARCHAR(50),
    StratificationID2 VARCHAR(50),
    StratificationCategoryID3 VARCHAR(50),
    StratificationID3 VARCHAR(50)
);

SET GLOBAL local_infile = 1;

SHOW VARIABLES LIKE 'local_infile';

LOAD DATA LOCAL INFILE 'C:\\Users\\ewlem\\Downloads\\U.S._Chronic_Disease_Indicators.csv'
INTO TABLE chronic_disease
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;

###############
# Viewing the table
###############

SELECT *
FROM `home_schema`.`chronic_disease`;

SELECT count(*) AS totalrows
FROM `home_schema`.`chronic_disease`;

###############
# The amount of rows should be 309,215 to match with the excel file
# Many columns are completely null or data is suppressed
###############

SELECT Response, DataValueFootnote, DataValueFootnoteSymbol, StratificationCategory2, Stratification2, StratificationCategory3, Stratification3, ResponseID, StratificationCategoryID2, StratificationID2, StratificationCategoryID3, StratificationID3
FROM `home_schema`.`chronic_disease`;

###############
# Other columns are not useful and/or partially filled
###############

SELECT *
FROM `home_schema`.`chronic_disease`
WHERE LowConfidenceLimit = 0 OR HighConfidenceLimit = 0;

SELECT count(*) AS totalrowsconfidence
FROM `home_schema`.`chronic_disease`
WHERE LowConfidenceLimit = 0 OR HighConfidenceLimit = 0;

###############
# Dropping columns that aren't useful or are not filled
###############

ALTER TABLE `home_schema`.`chronic_disease`
DROP COLUMN Response,
DROP COLUMN DataValueFootnoteSymbol,
DROP COLUMN DataValueFootnote,
DROP COLUMN LowConfidenceLimit,
DROP COLUMN HighConfidenceLimit,
DROP COLUMN StratificationCategory2,
DROP COLUMN Stratification2,
DROP COLUMN StratificationCategory3,
DROP COLUMN Stratification3,
DROP COLUMN ResponseID,
DROP COLUMN StratificationCategoryID2,
DROP COLUMN StratificationID2,
DROP COLUMN StratificationCategoryID3,
DROP COLUMN StratificationID3,
DROP COLUMN StratificationID1;

###############
# Name Changes
###############

ALTER TABLE `home_schema`.`chronic_disease`
CHANGE COLUMN LocationAbbr StateCode VARCHAR(10),
CHANGE COLUMN LocationDesc StateName VARCHAR(255),
CHANGE COLUMN DataValueType ValueType VARCHAR(100),
CHANGE COLUMN StratificationCategory1 StratificationCategory VARCHAR(255),
CHANGE COLUMN Stratification1 Stratification VARCHAR(255),
CHANGE COLUMN StratificationCategoryID1 StratificationCategoryID VARCHAR(100);

###############
# New table after dropped columns
###############

SELECT *
FROM `home_schema`.`chronic_disease`;

###############
# Exploring DataValueUnit
###############

SELECT DISTINCT DataValueUnit
FROM `home_schema`.`chronic_disease`;

SELECT *
FROM `home_schema`.`chronic_disease`
WHERE DataValueUnit = "per 100,000";

UPDATE `home_schema`.`chronic_disease`
SET DataValueUnit = "cases per 100,000"
WHERE DataValueUnit = "per 100,000";

SELECT *
FROM `home_schema`.`chronic_disease`
ORDER BY DataValueUnit;

###############
# Exploring DataValue & DataValueAlt
###############

SELECT *
FROM `home_schema`.`chronic_disease`
WHERE DataValue != DataValueAlt;

ALTER TABLE `home_schema`.`chronic_disease`
DROP COLUMN  DataValueAlt;

###############
# Exploring StratificationCategory & StratificationCategoryID
###############

SELECT *
FROM `home_schema`.`chronic_disease`
WHERE StratificationCategory != StratificationCategoryID;

ALTER TABLE `home_schema`.`chronic_disease`
DROP COLUMN  StratificationCategory;

###############
# Deleting rows with no values
###############

DELETE FROM `home_schema`.`chronic_disease`
WHERE DataValue = 0;

###############
# New Table
###############

SELECT *
FROM `home_schema`.`chronic_disease`;

SELECT COUNT(*) AS totalrows
FROM `home_schema`.`chronic_disease`;

###############
# Looking at distinct values
###############

SELECT DISTINCT YearStart
FROM `home_schema`.`chronic_disease`;

SELECT DISTINCT YearEnd
FROM `home_schema`.`chronic_disease`;

SELECT DISTINCT StateCode
FROM `home_schema`.`chronic_disease`;

SELECT DISTINCT StateName
FROM `home_schema`.`chronic_disease`;

SELECT DISTINCT DataSource
FROM `home_schema`.`chronic_disease`;

SELECT DISTINCT Topic
FROM `home_schema`.`chronic_disease`;

SELECT DISTINCT StratificationCategory
FROM `home_schema`.`chronic_disease`;

SELECT DISTINCT Stratification
FROM `home_schema`.`chronic_disease`;

SELECT DISTINCT StratificationCategoryID
FROM `home_schema`.`chronic_disease`;

###############
# More exploration
###############

SELECT *
FROM `home_schema`.`chronic_disease`
WHERE Topic = "Health Status" AND Question = "Life expectancy at birth";

SELECT *
FROM `home_schema`.`chronic_disease`
ORDER BY YearStart;

SELECT *
FROM `home_schema`.`chronic_disease`
WHERE DataValueUnit = "Number"
ORDER BY ValueType;

###############
# Removing Duplicates
###############

CREATE TABLE chronic_disease_clean AS
SELECT DISTINCT * FROM `home_schema`.`chronic_disease`;

SELECT *
FROM chronic_disease_clean;

SELECT count(*) AS totalrows
FROM chronic_disease_clean;

DROP TABLE `home_schema`.`chronic_disease`;

RENAME TABLE chronic_disease_clean TO chronic_disease;

###############
# Final table
###############

SELECT *
FROM chronic_disease;
