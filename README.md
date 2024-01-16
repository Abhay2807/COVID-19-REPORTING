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

#
