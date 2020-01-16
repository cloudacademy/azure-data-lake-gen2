# Using Azure Data Lake Storage Gen2
This file contains text you can copy and paste for the examples in Cloud Academy's _Using Azure Data Lake Storage Gen2_ course.  

### Introduction
[Azure Free Trial](https://azure.microsoft.com/free) 

### Ingesting Data
```
wget https://raw.githubusercontent.com/cloudacademy/azure-data-lake-gen2/master/radio.json
```
```
azcopy login
```
```
azcopy copy 'radio.json' 'https://cadatalakegen2.dfs.core.windows.net/datalake/radio.json'
```

### Accessing ADLS from Azure Databricks
```
abfss://datalake@cadatalakegen2.dfs.core.windows.net
```
```
configs = {
"fs.azure.account.auth.type": "CustomAccessToken",
"fs.azure.account.custom.token.provider.class": spark.conf.get("spark.databricks.passthrough.adls.gen2.tokenProviderClassName")
}

dbutils.fs.mount(
source = "abfss://datalake@cadatalakegen2.dfs.core.windows.net/",
mount_point = "/mnt/datalake",
extra_configs = configs)
```

### Analyzing Data with Azure Databricks
```
%sql
DROP TABLE IF EXISTS radio;
CREATE TABLE radio
USING json
OPTIONS (
path "/mnt/datalake/radio.json"
)
```
```
%sql
SELECT * from radio
```

### Summary
[Azure Data Lake Storage Gen2 documentation](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)  
[Azure Databricks documentation](https://docs.microsoft.com/azure/azure-databricks/)  
support@cloudacademy.com
