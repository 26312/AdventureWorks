# AdventureWorks
Dataset for Azure end2end DE project 

Dataset source:
https://www.kaggle.com/datasets/ukveteran/adventure-works/data


## Connecting Azure Databricks to Azure Data Lake

Step:1 Create Service Level Aplication using "Microsoft Entra ID", which will allow DataBricks to access Azure Data Lake

## Azure service principal
Connect to Azure Data Lake Storage Gen2 and Blob Storage:
https://learn.microsoft.com/en-us/azure/databricks/connect/storage/azure-storage

#### You can use the following format to set the cluster Spark configuration in your Notebook.
#### Use spark.conf.set in notebooks, as shown in the following example:


service_credential = dbutils.secrets.get(scope=`"<secret-scope>"`,key=`"<service-credential-key>"`)

spark.conf.set("fs.azure.account.auth.type.`<storage-account>`.dfs.core.windows.net", "OAuth")

spark.conf.set("fs.azure.account.oauth.provider.type.`<storage-account>`.dfs.core.windows.net", "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider")

spark.conf.set("fs.azure.account.oauth2.client.id.`<storage-account>`.dfs.core.windows.net", `"<application-id>"`)

spark.conf.set("fs.azure.account.oauth2.client.secret.`<storage-account>`.dfs.core.windows.net", `service_credential`)

spark.conf.set("fs.azure.account.oauth2.client.endpoint.`<storage-account>`.dfs.core.windows.net", "https://login.microsoftonline.com/<directory-id>/oauth2/token")
