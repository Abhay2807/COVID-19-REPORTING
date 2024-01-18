# COVID-19-REPORTING

# STEP 01 
# Using MS azure DATA FACTORY for data ingestion

I have built two data ingestion pipelines for working with COVID-19 data.

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/583c0dc1-5207-4607-a0c8-3017aaab55ea)


The first pipeline ingests data after extracting zipped file from Azure Blob Storage (ABS) to Azure Data Lake Storage (ADLS). I uploaded population by age data (zipped File) from the Eurostat website into ABS. The event trigger runs the pipeline as soon as the file comes in ABS and auto-deletes the file from ABS after ingestion. 

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/0da0f259-90da-4ab2-99a6-8d81021cd537)

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/f9034c5f-17e3-4a5d-ae79-b512db483813)

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/07e7534f-314a-450d-b95d-c265bd6090c2)

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/1c6e687a-678b-4897-8035-7fff1a16d661)


The second pipeline ingests data from the ECDC website(https://www.ecdc.europa.eu/en/covid-19/data), which is first stored in this GitHub repo. I have used an HTTP connection to the ADLS container, using a schedule trigger, to ingest this data. The pipeline picks all required connection details from a JSON lookup file and uses each activity to run a copy activity for each file. This method is efficient and allows you to ingest any number of files into the ADLS container in a single pipeline run.

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/0f7ed84f-711b-43b0-beca-f5107db2f956)
![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/2e9247bd-5ceb-4372-9184-7dbe78fe416f)

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/08a4331d-2d56-4278-b950-3c6741b7c380)

# STEP 02 
# Using data Flow for transformation 

I have completed the second step of transforming the biggest ECDC file called Cases_Deaths.csv, which is present in the raw container in ADLS. 
![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/9b7ec3ee-e279-48c1-9304-ca06975c7f72)


![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/5e6793f4-b1d4-4737-8e56-0252b6937412)

My Target was to get some desired columns in output after,doing transformation using data flow:

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/485433bc-4bd2-410c-aa6a-a22a56730d0b)

Data Flow :

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/c349032f-4cfd-4c4c-8b14-9d6b4988a996)


The transformation process was carried out through a series of steps, beginning with the source transformation to define the input file for processing. 

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/3f62a447-cc8f-427e-a9d0-d6140a6d2773)

Next, the filter transformation was employed to eliminate undesired columns. The select transformation was then utilized to remove all unwanted fields. 

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/7d3d94a5-c6fb-4fc3-aaeb-f8dcb4f87f5c)

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/7625d11e-3704-4520-aff0-d7edf7c91443)

The pivot transformation was used subsequently to generate new columns for confirmed cases and deaths, using the Pivot key: "Indicator" and the Pivoted Column: "Count", respectively. Following this, the Lookup transformation was employed to obtain all the other desired columns from the lookup file and perform an inner join with the output of the pivot modifier. 

Lookup:
![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/f606754c-0aa4-4359-a37a-7bf7c031214f)


![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/14824cc1-6813-4c50-b9ba-4e9910e2d902)

The select transformation was used once more to acquire all the desired fields. Finally, the sink transformation was leveraged to write the transformed file to the ADLS container, employing a partition to write the output in multi-file format.

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/5a04d2f6-2f97-458c-9463-da8fb2d4cd69)

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/69447d8e-c642-4cba-8cc8-31765d7087f1)

Desired results:


![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/561126ab-83d0-46b2-9e40-511814cf6377)


![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/e9df75a8-b2c0-48e7-bd29-6f0901b410ce)



Pipelines execution:

![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/dd19c2cf-8862-47d0-bbdb-08a9696e51c5)
![image](https://github.com/Abhay2807/COVID-19-REPORTING/assets/76277587/0271b9d1-366a-4b36-9426-24413e12b1fc)





