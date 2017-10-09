---
title: aaaManage Azure Data Lake Analytics met Azure .NET SDK | Microsoft Docs
description: 'Meer informatie over hoe Data Lake Analytics toomanage taken, gegevensbronnen, gebruikers. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 811d172d-9873-4ce9-a6d5-c1a26b374c79
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 98630ba411823644a8bce1f1b0c1331f689cbb0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a>Azure Data Lake Analytics beheren met Azure .NET SDK
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Meer informatie over hoe Hallo toomanage Azure Data Lake Analytics-accounts, gegevensbronnen, gebruikers en taken met behulp van Azure .NET SDK. 

## <a name="prerequisites"></a>Vereisten

* **Visual Studio 2015, Visual Studio 2013 update 4 of Visual Studio 2012 met Visual C++ geïnstalleerd**.
* **Microsoft Azure SDK voor .NET versie 2.5 of hoger**.  Installeren met behulp van Hallo [webplatforminstallatieprogramma](http://www.microsoft.com/web/downloads/platform.aspx).
* **Vereiste NuGet-pakketten**

### <a name="install-nuget-packages"></a>NuGet-pakketten installeren

|Pakket|Versie|
|-------|-------|
|[Microsoft.Rest.ClientRuntime.Azure.Authentication](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| 2.3.1|
|[Microsoft.Azure.Management.DataLake.Analytics](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|3.0.0|
|[Microsoft.Azure.Management.DataLake.Store](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|2.2.0|
|[Microsoft.Azure.Management.ResourceManager](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|1.6.0-Preview|
|[Microsoft.Azure.Graph.RBAC](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|3.4.0-Preview|

U kunt deze pakketten via de opdrachtregel voor Hallo NuGet installeren Hello volgende opdrachten:

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a>Algemene variabelen

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a>Authentication

U hebt meerdere mogelijkheden voor logboekregistratie op tooAzure Data Lake Analytics. Hallo toont volgende fragment een voorbeeld van verificatie met interactieve gebruikersverificatie met een pop-upvenster.

``` csharp
using System;
using System.IO;
using System.Threading;
using System.Security.Cryptography.X509Certificates;

using Microsoft.Rest;
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.DataLake.Analytics;
using Microsoft.Azure.Management.DataLake.Analytics.Models;
using Microsoft.Azure.Management.DataLake.Store;
using Microsoft.Azure.Management.DataLake.Store.Models;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Microsoft.Azure.Graph.RBAC;

public static Program
{
   public static string TENANT = "microsoft.onmicrosoft.com";
   public static string CLIENTID = "1950a258-227b-4e31-a9cf-717495945fc2";
   public static System.Uri ARM_TOKEN_AUDIENCE = new System.Uri( @"https://management.core.windows.net/");
   public static System.Uri ADL_TOKEN_AUDIENCE = new System.Uri( @"https://datalake.azure.net/" );
   public static System.Uri GRAPH_TOKEN_AUDIENCE = new System.Uri( @"https://graph.windows.net/" );

   static void Main(string[] args)
   {
      string MY_DOCUMENTS= System.Environment.GetFolderPath( System.Environment.SpecialFolder.MyDocuments);
      string TOKEN_CACHE_PATH = System.IO.Path.Combine(MY_DOCUMENTS, "my.tokencache");

      var tokenCache = GetTokenCache(TOKEN_CACHE_PATH);
      var armCreds = GetCreds_User_Popup(TENANT, ARM_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var adlCreds = GetCreds_User_Popup(TENANT, ADL_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var graphCreds = GetCreds_User_Popup(TENANT, GRAPH_TOKEN_AUDIENCE, CLIENTID, tokenCache);
   }
}
```

Hallo broncode voor **GetCreds_User_Popup** en code Hallo voor andere opties voor verificatie worden behandeld in [Data Lake Analytics .NET-verificatieopties](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)


## <a name="create-hello-client-management-objects"></a>Hallo-client beheerobjecten maken

``` csharp
var resourceManagementClient = new ResourceManagementClient(armCreds) { SubscriptionId = subid };

var adlaAccountClient = new DataLakeAnalyticsAccountManagementClient(armCreds);
adlaAccountClient.SubscriptionId = subid;

var adlsAccountClient = new DataLakeStoreAccountManagementClient(armCreds);
adlsAccountClient.SubscriptionId = subid;

var adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClient(adlCreds);
var adlaJobClient = new DataLakeAnalyticsJobManagementClient(adlCreds);

var adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(adlCreds);

var  graphClient = new GraphRbacManagementClient(graphCreds);
graphClient.TenantID = domain;

```

## <a name="manage-accounts"></a>Accounts beheren

### <a name="create-an-azure-resource-group"></a>Een Azure-resourcegroep maken

Als u dit nog niet hebt gemaakt, moet u een Azure-resourcegroep toocreate hebben de onderdelen van uw Data Lake Analytics. U moet uw referenties voor verificatie, abonnements-ID en een locatie. Hallo van de volgende code wordt getoond hoe toocreate een resourcegroep:

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
Zie voor meer informatie [Azure-resourcegroepen en Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).

### <a name="create-a-data-lake-store-account"></a>Een Data Lake Store-account maken

ADLA account vereist ooit een ADLS-account. Als u één toouse nog geen hebt, kunt u één met de volgende code Hallo maken:

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a>Een Data Lake Analytics-account maken

Hallo volgende code maakt een ADLS-account

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a>Lijst met Data Lake Store-accounts

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a>Lijst met Data Lake Analytics-accounts

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a>Controleren of een account bestaat

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a>Informatie ophalen over een account

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a>Een account verwijderen

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-hello-default-data-lake-store-account"></a>Hallo standaard Data Lake Store-account ophalen

Elk Data Lake Analytics-account vereist een Data Lake Store-standaardaccount. Gebruik deze code toodetermine Hallo Store-standaardaccount voor een Analytics-account.

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a>Gegevensbronnen beheren

Data Lake Analytics ondersteunt momenteel Hallo gegevensbronnen te volgen:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure Storage-Account](../storage/common/storage-introduction.md)

### <a name="link-tooan-azure-storage-account"></a>Koppeling tooan Azure Storage-account

U kunt koppelingen tooAzure Storage-accounts maken.

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a>Lijst van gegevensbronnen voor Azure Storage

``` csharp
var stg_accounts = adlaAccountClient.StorageAccounts.ListByAccount(rg, adla);

if (stg_accounts != null)
{
  foreach (var stg_account in stg_accounts)
  {
      Console.WriteLine($"Storage account: {0}", stg_account.Name);
  }
}
```

### <a name="list-data-lake-store-data-sources"></a>Lijst met Data Lake Store-gegevensbronnen

``` csharp
var adls_accounts = adlsClient.Account.List();

if (adls_accounts != null)
{
  foreach (var adls_accnt in adls_accounts)
  {
      Console.WriteLine($"ADLS account: {0}", adls_accnt.Name);
  }
}
```

### <a name="upload-and-download-folders-and-files"></a>Uploaden en downloaden van bestanden en mappen
U kunt gebruiken Hallo Data Lake Store-bestand system client management object tooupload en downloaden afzonderlijke bestanden of mappen naar de lokale computer Azure tooyour Hallo volgende methoden gebruiken:

- UploadFolder
- UploadFile
- DownloadFolder
- DownloadFile

de eerste parameter Hello om deze methoden is Hallo-naam van Hallo Data Lake Store-Account, gevolgd door de parameters voor het bronpad Hallo en Hallo doelpad.

Hallo volgende voorbeeld ziet u hoe toodownload een map in Data Lake Store Hallo.

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a>Een bestand in een Data Lake Store-account maken

``` csharp
using (var memstream = new MemoryStream())
{
   using (var sw = new StreamWriter(memstream, UTF8Encoding.UTF8))
   {
      sw.WriteLine("Hello World");
      sw.Flush();

      adlsFileSystemClient.FileSystem.Create(adls, "/Samples/Output/randombytes.csv", memstream);
   }
}
```

### <a name="verify-azure-storage-account-paths"></a>Controleer of de paden van Azure Storage-account
Hallo controleert volgende code als een Azure Storage-account (storageAccntName) bestaat al in een Data Lake Analytics-account (analyticsAccountName), en als een container (containerName) bestaat in hello Azure Storage-account.

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a>Catalogus en taken beheren
Hallo DataLakeAnalyticsCatalogManagementClient object biedt methoden voor het beheren van Hallo SQL-database voor elk Azure Data Lake Analytics-account opgegeven. Hallo DataLakeAnalyticsJobManagementClient biedt methoden toosubmit en beheren van taken uitvoeren op Hallo-database met U-SQL-scripts.

### <a name="list-databases-and-schemas"></a>Lijst met databases en schema 's
U aanbieden kunt, verschillende dingen Hallo meest voorkomende zijn onder Hallo databases en hun schema. Hallo volgende code verkrijgt van een verzameling van databases en vervolgens worden opgesomd Hallo-schema voor elke database.

``` csharp
var databases = adlaCatalogClient.Catalog.ListDatabases(adla);
foreach (var db in databases)
{
  Console.WriteLine($"Database: {db.Name}");
  Console.WriteLine(" - Schemas:");
  var schemas = adlaCatalogClient.Catalog.ListSchemas(adla, db.Name);
  foreach (var schm in schemas)
  {
      Console.WriteLine($"\t{schm.Name}");
  }
}
```

### <a name="list-table-columns"></a>Lijst met kolommen
Hallo volgende code toont hoe tooaccess Hallo database met een Data Lake Analytics-catalogus management-client toolist Hallo kolommen in een opgegeven tabel.

``` csharp
var tbl = adlaCatalogClient.Catalog.GetTable(adla, "master", "dbo", "MyTableName");
IEnumerable<USqlTableColumn> columns = tbl.ColumnList;

foreach (USqlTableColumn utc in columns)
{
  string scriptPath = "/Samples/Scripts/SearchResults_Wikipedia_Script.txt";
  Stream scriptStrm = adlsFileSystemClient.FileSystem.Open(_adlsAccountName, scriptPath);
  string scriptTxt = string.Empty;
  using (StreamReader sr = new StreamReader(scriptStrm))
  {
      scriptTxt = sr.ReadToEnd();
  }

  var jobName = "SR_Wikipedia";
  var jobId = Guid.NewGuid();
  var properties = new USqlJobProperties(scriptTxt);
  var parameters = new JobInformation(jobName, JobType.USql, properties, priority: 1, degreeOfParallelism: 1, jobId: jobId);
  var jobInfo = adlaJobClient.Job.Create(adla, jobId, parameters);
  Console.WriteLine($"Job {jobName} submitted.");

}
```

### <a name="list-failed-jobs"></a>Mislukte taken weergeven
Hallo geeft volgende code informatie over taken die niet zijn geslaagd.

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a>Lijst pijplijnen
Hallo geeft volgende code informatie over elke pijplijn van taken ingediende toohello account.

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a>Lijst met herhalingen
Hallo geeft volgende code informatie over elke herhaling van taken ingediende toohello account.

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a>Algemene scenario's voor grafiek

### <a name="look-up-user-in-hello-aad-directory"></a>Hallo AAD-directory-gebruiker opzoeken

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-hello-objectid-of-a-user-in-hello-aad-directory"></a>Hallo ObjectId van een gebruiker in Hallo AAD-directory ophalen

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a>Compute-beleid beheren
Hallo DataLakeAnalyticsAccountManagementClient object biedt methoden voor het beheer van Hallo compute-beleid voor een Data Lake Analytics-account.

### <a name="list-compute-policies"></a>Compute-beleidsregels weergeven
Hallo volgende code haalt een lijst met compute-beleidsregels voor een Data Lake Analytics-account.

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a>Maak een nieuw compute-beleid
Hallo volgende code maakt een nieuw beleid voor een Data Lake Analytics-account voor compute, instelling Hallo maximale AUs beschikbaar toohello opgegeven gebruiker too50 en Hallo Minimumprioriteit prioriteit too250.

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a>Volgende stappen
* [Overzicht van Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md)
* [Azure Data Lake Analytics-taken bewaken en problemen oplossen met Azure Portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
