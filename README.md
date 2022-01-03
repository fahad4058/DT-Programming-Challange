
#### Authors

Fahad Maqsood (fahad4058@gmail.com)

Dated: 30-12-2021, Koblenz, 56068, Germany.



## Daimler Trucks - Truck Analytics : Data Analytics Programming Challange

## Overview
### About
This challange is comprised of Data Engineering and Data Science tasks which involves Data Preparation using ETL pipeline. Furthermore, 
the prepared data has to be analyzed and evaluated by performing multiple operations to achieve the desired results.


### Technologies used
- Jupyter Notebook for coding purposes.
- Apache Spark using PySpark(Spark with Python and Pandas API) for Data Dnalytics.
- Data visulatization libraries - seaborn, matlplotlib, worcloud were briefly used to highlight the potential of data visulatization tools and techniques in context to Data Analytics.  

### Data used
The Data used is provided by the Daimler Trucks Analytics which consists of tabular data in Excel format. 
The Excel file vehicle_data.xlsx consists of three sheets namely sales_codes, vehicle hash and engines which contains following information:
- sales_codes: vehicle hash, production dates, shipping countries, and a sales code array which shows the composition of a vehicle in terms of sales codes.
- vehicle_hash: vehicle hash, unique vehicle ID "fin", recording dates and source.
- engines: code group ID and names, engine sales codes and names/codes of Engines.   

## Tasks 
### Data Engineering
Implementation of an ETL(Extract, Transform and Load) pipeline consisting of following sub-tasks:
- Loading Data
- Data Cleaning and Preparation
- Merging together the data based on a key
- Selecting the data for further Implementation
### Data Science

Following sub-tasks have to be performed on the prepared data:

- What are the top three countries in which between 01/01/2014 and 31/12/2020 most vehicles were sold?
- In which of these years, we have sold a total of most vehicles?
- Which FIN is the first vehicle sold in terms of time?
- How many vehicles were sold between 01/01/2017 and 01/01/2021 with OM934, OM936, OM470 and OM471 engines?
- Which vehicles (FIN) were sold to New Zealand between 01/01/2017 and 01/01/2021 and with an OM936 engine?

The Jupyter notebook "programming_challange.ipynb" can be found in the repository.

## Solution
Implementation of an ETL (Extract, Transform and Load) pipeline.

### Step Involved
The whole process was implemented on Jupyter notebook using the python and pandas API on Apache Spark for execution of the Data Engineering and Data Science task on single-node machine.

Following are the steps followed to achieve the desired results:

1- Data Extraction from the vehicle_data.xlsx file. The data-set comprises of three excel sheets which were converted to .csv file format for ease of use. It results into three "Dataframes" for further execution. 

2- Dataframes are futher analyzed thoroughly for missing and corrupt values.

3- Observation through inital analysis leads to the data cleaning and transformations where necessary.

4- Prepared and dataframes are then merged together resulting into a new dataframe.  

5- The desired columns are then selected from the merged datframe.

6- Merged data is then saved/loaded into the orignal data source which in this case is the vehicle_data.xlsx file.  

7- Once the final dataframe is ready further operations can be performed to extract useful information and trends within the data.




## Demonstration
### Task 1: Data Engineering
#### 1) Data Extraction
The data extracted is as follows:

Sales code dataframe 
![Capture](https://user-images.githubusercontent.com/65433300/147683012-70ad2b2f-1cc9-4d87-bb7f-27cb5aa62360.GIF)
count: 500 entries

Vehicle hash dataframe
![Capture](https://user-images.githubusercontent.com/65433300/147683348-892bb38a-5d9f-49d3-b5df-c95f3d685e38.JPG)
count: 500 entries

Engines dataframe
![image](https://user-images.githubusercontent.com/65433300/147683529-b65f38d4-fa13-44cc-9c7d-3ce8e512d0ac.png)

The datatypes of the the columns in each of the above dataframes can be seen in the figure respectively:

![image](https://user-images.githubusercontent.com/65433300/147683773-f64b9157-f699-40c5-ae45-9f64ba792fd0.png)

#### Observations
Observation shows:

* Presence of un-necessary columns which should be removed.

![image](https://user-images.githubusercontent.com/65433300/147685107-230fb914-9547-492e-a2be-c55889830664.png)

The highlighted columns have to be removed.

* Vehicle ID "fin" is a unique ID comprised of capital alphabets and numerals and follows a specific format. Those entries have to be removed which don't correspond to the ID format.

![image](https://user-images.githubusercontent.com/65433300/147688423-dfb1a1cc-6140-4dc4-adf0-c53da35ae3a7.png)

6 odd entries in the fin column.

* Data types of some columns has to be rectified e.g. "production_date" should be DATE type. 

![image](https://user-images.githubusercontent.com/65433300/147688858-6a5e3d21-e3a8-441a-903a-80316092557a.png)

* Production Dates of some vehicles have null and corrupt values.

![image](https://user-images.githubusercontent.com/65433300/147694220-493e7749-2798-46dc-b116-5aa93971373f.png)

these entries are to be removed.

* Format of country name should be a capital letter followed by small alphabets.

![image](https://user-images.githubusercontent.com/65433300/147694406-c5e184c8-5ed6-4f17-ac75-a9a11b19fabf.png)

Only case conversion is required here.

* "Sales_code_array" is just a string whereas it should be an array with string element type. 

![image](https://user-images.githubusercontent.com/65433300/147694514-b6ac2d73-213c-4dd5-b829-8aa30c7b1d11.png)

* It's safe to assume that a vehicle/truck is driven by ONE engine only. If the composition of truck(Sales_code_array) is comprised of two or more engines then that particular entry has to removed.

![image](https://user-images.githubusercontent.com/65433300/147694987-7bd361bf-8126-462f-aacb-b90541bccfdc.png)

There are multiple entries where sales_code_array contains sales codes of more than one engines. Therefore, it has to be catered.

* Rows with NULL/undefined values has to be removed.

![image](https://user-images.githubusercontent.com/65433300/147695878-2f98edc0-3c38-4a05-93ce-32829ce0178e.png)

Rows with "any" null/nan values has to be removed.

#### 2) Data Cleaning and Preparation
The dataframes were processed and transformed to mitigate the corrupt and faulty entries. Following shows the prepared data for future processing:

* Sales codes dataframe:
![image](https://user-images.githubusercontent.com/65433300/147770659-494747a2-fd82-48d2-b6c7-1aaf2b56fbe3.png)

![image](https://user-images.githubusercontent.com/65433300/147770781-51c0a75a-0e15-4dc2-a136-14f32cb9f486.png)

* vehicle hash dataframe:
![image](https://user-images.githubusercontent.com/65433300/147770842-7cd8c083-e767-4a0e-b87f-6f228d283395.png)

![image](https://user-images.githubusercontent.com/65433300/147770877-5cfb2fe3-721d-4372-942f-e180c2d4dd27.png)

#### 3) Merged Data
Based on the encrypted "h_vehicle_hash" the resulting dataframes are merged and results into:

![image](https://user-images.githubusercontent.com/65433300/147771493-68ee81f7-6c11-408d-b5e1-36978e5baf34.png)

![image](https://user-images.githubusercontent.com/65433300/147771701-6180b87f-7ac5-48fc-9301-526106f683e7.png)

Above results shows the prepared data has 398 entries left after cleaning and transformations.

#### 4) Final dataframe
The final dataframe consists of "fin","production_date","country" and "sales_code_array" columns.

![image](https://user-images.githubusercontent.com/65433300/147771860-abfcae8f-6704-43e2-9083-845670a474a5.png)

This data is further Saved as an excel sheet in the orignal vehicle_data.xlsx file named as "merged vehicle data"

![image](https://user-images.githubusercontent.com/65433300/147772079-9fc2485e-cdce-40df-9cf6-d6ae70ffc0bf.png)

### Task 2: Data Science
Subtasks and results are as follows: 

#### 1- What are the top three countries in which between 01/01/2014 and 31/12/2020 most vehicles were sold? 
![image](https://user-images.githubusercontent.com/65433300/147772470-bf26a2bf-bf23-4b83-8ee6-066a92a013dd.png)

![image](https://user-images.githubusercontent.com/65433300/147773335-e87a19da-ebb3-4467-b88b-457192381f3a.png)

#### 2- In which of these years most vehicles were sold?
![image](https://user-images.githubusercontent.com/65433300/147773414-fc2dd634-5266-44b3-ad74-b83c5ec41075.png)

![image](https://user-images.githubusercontent.com/65433300/147773468-c3814d74-85ee-4380-9b91-8eebce4c6bb3.png)

graphical representation

#### 3- Which FIN is the first vehicle sold in terms of time?
![image](https://user-images.githubusercontent.com/65433300/147773602-b6a7d68e-98d0-48b3-94ea-2bfd6a32581d.png)

#### 4- How many vehicles were sold between 01/01/2017 and 01/01/2021 with OM934, OM936, OM470 and OM471 engines ?
![image](https://user-images.githubusercontent.com/65433300/147773841-d631765c-a7e3-4213-a3a3-9a56e68a1781.png)

![image](https://user-images.githubusercontent.com/65433300/147773877-5e00652d-f795-48b4-92fe-ed040a4e7112.png)

A total of 88 vehicles

#### 5- Which vehicles (FIN) were sold to New Zealand between 01/01/2017 and 01/01/2021 and with an OM936 engine?

![image](https://user-images.githubusercontent.com/65433300/147774061-92450306-51f0-430e-b48f-9e3e6a338b70.png)

#### References

* Please refer to the Jupyter Notebook titled "programming_challange.ipynb" for the complete codes and description.

* [Apache Spark](https://spark.apache.org/docs/latest/)
