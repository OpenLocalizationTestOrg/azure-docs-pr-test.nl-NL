---
title: Azure Data Lake Analytics beheren met Azure .NET SDK | Microsoft Docs
description: 'Informatie over het beheren van Data Lake Analytics-taken en gegevensbronnen en gebruikers. '
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
ms.openlocfilehash: 0f8a95f96ce4c816dfb9132923faa9a9bf20c205
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a><span data-ttu-id="4d7be-103">Azure Data Lake Analytics beheren met Azure .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4d7be-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="4d7be-104">Informatie over het beheren van Azure Data Lake Analytics-accounts, gegevensbronnen, gebruikers en taken met behulp van de Azure .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="4d7be-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure .NET SDK.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4d7be-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4d7be-105">Prerequisites</span></span>

* <span data-ttu-id="4d7be-106">**Visual Studio 2015, Visual Studio 2013 update 4 of Visual Studio 2012 met Visual C++ geïnstalleerd**.</span><span class="sxs-lookup"><span data-stu-id="4d7be-106">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="4d7be-107">**Microsoft Azure SDK voor .NET versie 2.5 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="4d7be-107">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="4d7be-108">U kunt dit installeren met het [Webplatforminstallatieprogramma](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d7be-108">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="4d7be-109">**Vereiste NuGet-pakketten**</span><span class="sxs-lookup"><span data-stu-id="4d7be-109">**Required NuGet Packages**</span></span>

### <a name="install-nuget-packages"></a><span data-ttu-id="4d7be-110">NuGet-pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="4d7be-110">Install NuGet packages</span></span>

|<span data-ttu-id="4d7be-111">Pakket</span><span class="sxs-lookup"><span data-stu-id="4d7be-111">Package</span></span>|<span data-ttu-id="4d7be-112">Versie</span><span class="sxs-lookup"><span data-stu-id="4d7be-112">Version</span></span>|
|-------|-------|
|[<span data-ttu-id="4d7be-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span><span class="sxs-lookup"><span data-stu-id="4d7be-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span></span>](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| <span data-ttu-id="4d7be-114">2.3.1</span><span class="sxs-lookup"><span data-stu-id="4d7be-114">2.3.1</span></span>|
|[<span data-ttu-id="4d7be-115">Microsoft.Azure.Management.DataLake.Analytics</span><span class="sxs-lookup"><span data-stu-id="4d7be-115">Microsoft.Azure.Management.DataLake.Analytics</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|<span data-ttu-id="4d7be-116">3.0.0</span><span class="sxs-lookup"><span data-stu-id="4d7be-116">3.0.0</span></span>|
|[<span data-ttu-id="4d7be-117">Microsoft.Azure.Management.DataLake.Store</span><span class="sxs-lookup"><span data-stu-id="4d7be-117">Microsoft.Azure.Management.DataLake.Store</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|<span data-ttu-id="4d7be-118">2.2.0</span><span class="sxs-lookup"><span data-stu-id="4d7be-118">2.2.0</span></span>|
|[<span data-ttu-id="4d7be-119">Microsoft.Azure.Management.ResourceManager</span><span class="sxs-lookup"><span data-stu-id="4d7be-119">Microsoft.Azure.Management.ResourceManager</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="4d7be-120">1.6.0-Preview</span><span class="sxs-lookup"><span data-stu-id="4d7be-120">1.6.0-preview</span></span>|
|[<span data-ttu-id="4d7be-121">Microsoft.Azure.Graph.RBAC</span><span class="sxs-lookup"><span data-stu-id="4d7be-121">Microsoft.Azure.Graph.RBAC</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="4d7be-122">3.4.0-Preview</span><span class="sxs-lookup"><span data-stu-id="4d7be-122">3.4.0-preview</span></span>|

<span data-ttu-id="4d7be-123">U kunt deze pakketten via de opdrachtregel NuGet installeren met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="4d7be-123">You can install these packages via the NuGet command line with the following commands:</span></span>

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a><span data-ttu-id="4d7be-124">Algemene variabelen</span><span class="sxs-lookup"><span data-stu-id="4d7be-124">Common variables</span></span>

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a><span data-ttu-id="4d7be-125">Authentication</span><span class="sxs-lookup"><span data-stu-id="4d7be-125">Authentication</span></span>

<span data-ttu-id="4d7be-126">U hebt meerdere mogelijkheden voor melden bij Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4d7be-126">You have multiple options for logging on to Azure Data Lake Analytics.</span></span> <span data-ttu-id="4d7be-127">Het volgende fragment toont een voorbeeld van verificatie met interactieve gebruikersverificatie met een pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="4d7be-127">The following snippet shows an example of authentication with interactive user authentication with a pop-up.</span></span>

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

<span data-ttu-id="4d7be-128">De broncode voor **GetCreds_User_Popup** en de code voor andere opties voor verificatie worden behandeld in [Data Lake Analytics .NET-verificatieopties](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span><span class="sxs-lookup"><span data-stu-id="4d7be-128">The source code for **GetCreds_User_Popup** and the code for other options for authentication are covered in [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span></span>


## <a name="create-the-client-management-objects"></a><span data-ttu-id="4d7be-129">De client beheerobjecten maken</span><span class="sxs-lookup"><span data-stu-id="4d7be-129">Create the client management objects</span></span>

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

## <a name="manage-accounts"></a><span data-ttu-id="4d7be-130">Accounts beheren</span><span class="sxs-lookup"><span data-stu-id="4d7be-130">Manage accounts</span></span>

### <a name="create-an-azure-resource-group"></a><span data-ttu-id="4d7be-131">Een Azure-resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="4d7be-131">Create an Azure Resource Group</span></span>

<span data-ttu-id="4d7be-132">Als u dit nog niet hebt gemaakt, moet u een Azure-resourcegroep te maken van de onderdelen van uw Data Lake Analytics hebben.</span><span class="sxs-lookup"><span data-stu-id="4d7be-132">If you haven't already created one, you must have an Azure Resource Group to create your Data Lake Analytics components.</span></span> <span data-ttu-id="4d7be-133">U moet uw referenties voor verificatie, abonnements-ID en een locatie.</span><span class="sxs-lookup"><span data-stu-id="4d7be-133">You  need your authentication credentials, subscription ID, and a location.</span></span> <span data-ttu-id="4d7be-134">De volgende code toont hoe u een resourcegroep maken:</span><span class="sxs-lookup"><span data-stu-id="4d7be-134">The following code shows how to create a resource group:</span></span>

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
<span data-ttu-id="4d7be-135">Zie voor meer informatie [Azure-resourcegroepen en Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span><span class="sxs-lookup"><span data-stu-id="4d7be-135">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span></span>

### <a name="create-a-data-lake-store-account"></a><span data-ttu-id="4d7be-136">Een Data Lake Store-account maken</span><span class="sxs-lookup"><span data-stu-id="4d7be-136">Create a Data Lake Store account</span></span>

<span data-ttu-id="4d7be-137">ADLA account vereist ooit een ADLS-account.</span><span class="sxs-lookup"><span data-stu-id="4d7be-137">Ever ADLA account requires an ADLS account.</span></span> <span data-ttu-id="4d7be-138">Als u niet wilt gebruiken al hebt, kunt u één met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="4d7be-138">If you don't already have one to use, you can create one with the following code:</span></span>

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="4d7be-139">Een Data Lake Analytics-account maken</span><span class="sxs-lookup"><span data-stu-id="4d7be-139">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="4d7be-140">De volgende code maakt een ADLS-account</span><span class="sxs-lookup"><span data-stu-id="4d7be-140">The following code creates an ADLS account</span></span>

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a><span data-ttu-id="4d7be-141">Lijst met Data Lake Store-accounts</span><span class="sxs-lookup"><span data-stu-id="4d7be-141">List Data Lake Store accounts</span></span>

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a><span data-ttu-id="4d7be-142">Lijst met Data Lake Analytics-accounts</span><span class="sxs-lookup"><span data-stu-id="4d7be-142">List Data Lake Analytics accounts</span></span>

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a><span data-ttu-id="4d7be-143">Controleren of een account bestaat</span><span class="sxs-lookup"><span data-stu-id="4d7be-143">Checking if an account exists</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="4d7be-144">Informatie ophalen over een account</span><span class="sxs-lookup"><span data-stu-id="4d7be-144">Get information about an account</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a><span data-ttu-id="4d7be-145">Een account verwijderen</span><span class="sxs-lookup"><span data-stu-id="4d7be-145">Delete an account</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-the-default-data-lake-store-account"></a><span data-ttu-id="4d7be-146">De standaard Data Lake Store-account ophalen</span><span class="sxs-lookup"><span data-stu-id="4d7be-146">Get the default Data Lake Store account</span></span>

<span data-ttu-id="4d7be-147">Elk Data Lake Analytics-account vereist een Data Lake Store-standaardaccount.</span><span class="sxs-lookup"><span data-stu-id="4d7be-147">Every Data Lake Analytics account requires a default Data Lake Store account.</span></span> <span data-ttu-id="4d7be-148">Deze code gebruiken om te bepalen van de Store-standaardaccount voor Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="4d7be-148">Use this code to determine the default Store account for an Analytics account.</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a><span data-ttu-id="4d7be-149">Gegevensbronnen beheren</span><span class="sxs-lookup"><span data-stu-id="4d7be-149">Manage data sources</span></span>

<span data-ttu-id="4d7be-150">Data Lake Analytics ondersteunt momenteel de volgende gegevensbronnen:</span><span class="sxs-lookup"><span data-stu-id="4d7be-150">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="4d7be-151">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4d7be-151">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="4d7be-152">Azure Storage-Account</span><span class="sxs-lookup"><span data-stu-id="4d7be-152">Azure Storage Account</span></span>](../storage/common/storage-introduction.md)

### <a name="link-to-an-azure-storage-account"></a><span data-ttu-id="4d7be-153">Koppelen aan een Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="4d7be-153">Link to an Azure Storage account</span></span>

<span data-ttu-id="4d7be-154">U kunt koppelingen naar Azure Storage-accounts maken.</span><span class="sxs-lookup"><span data-stu-id="4d7be-154">You can create links to Azure Storage accounts.</span></span>

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a><span data-ttu-id="4d7be-155">Lijst van gegevensbronnen voor Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4d7be-155">List Azure Storage data sources</span></span>

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

### <a name="list-data-lake-store-data-sources"></a><span data-ttu-id="4d7be-156">Lijst met Data Lake Store-gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="4d7be-156">List Data Lake Store data sources</span></span>

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

### <a name="upload-and-download-folders-and-files"></a><span data-ttu-id="4d7be-157">Uploaden en downloaden van bestanden en mappen</span><span class="sxs-lookup"><span data-stu-id="4d7be-157">Upload and download folders and files</span></span>
<span data-ttu-id="4d7be-158">U kunt het Data Lake Store client management bestandssysteemobject uploaden en downloaden van afzonderlijke bestanden of mappen van Azure op uw lokale computer met behulp van de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="4d7be-158">You can use the Data Lake Store file system client management object to upload and download individual files or folders from Azure to your local computer, using the following methods:</span></span>

- <span data-ttu-id="4d7be-159">UploadFolder</span><span class="sxs-lookup"><span data-stu-id="4d7be-159">UploadFolder</span></span>
- <span data-ttu-id="4d7be-160">UploadFile</span><span class="sxs-lookup"><span data-stu-id="4d7be-160">UploadFile</span></span>
- <span data-ttu-id="4d7be-161">DownloadFolder</span><span class="sxs-lookup"><span data-stu-id="4d7be-161">DownloadFolder</span></span>
- <span data-ttu-id="4d7be-162">DownloadFile</span><span class="sxs-lookup"><span data-stu-id="4d7be-162">DownloadFile</span></span>

<span data-ttu-id="4d7be-163">De eerste parameter voor deze methoden is de naam van de Data Lake Store-Account, gevolgd door de parameters voor het bronpad en het doelpad.</span><span class="sxs-lookup"><span data-stu-id="4d7be-163">The first parameter for these methods is the name of the Data Lake Store Account, followed by parameters for the source path and the destination path.</span></span>

<span data-ttu-id="4d7be-164">Het volgende voorbeeld ziet het downloaden van een map in de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4d7be-164">The following example shows how to download a folder in the Data Lake Store.</span></span>

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="4d7be-165">Een bestand in een Data Lake Store-account maken</span><span class="sxs-lookup"><span data-stu-id="4d7be-165">Create a file in a Data Lake Store account</span></span>

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

### <a name="verify-azure-storage-account-paths"></a><span data-ttu-id="4d7be-166">Controleer of de paden van Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="4d7be-166">Verify Azure Storage account paths</span></span>
<span data-ttu-id="4d7be-167">De volgende code controleert als een Azure Storage-account (storageAccntName) bestaat al in een Data Lake Analytics-account (analyticsAccountName), en als een container (containerName) bestaat in de Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="4d7be-167">The following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in the Azure Storage account.</span></span>

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a><span data-ttu-id="4d7be-168">Catalogus en taken beheren</span><span class="sxs-lookup"><span data-stu-id="4d7be-168">Manage catalog and jobs</span></span>
<span data-ttu-id="4d7be-169">Het object DataLakeAnalyticsCatalogManagementClient biedt methoden voor het beheren van de SQL-database die is opgegeven voor elke Azure Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="4d7be-169">The DataLakeAnalyticsCatalogManagementClient object provides methods for managing the SQL database provided for each Azure Data Lake Analytics account.</span></span> <span data-ttu-id="4d7be-170">De DataLakeAnalyticsJobManagementClient biedt methoden voor het verzenden en beheren van taken worden uitgevoerd op de database met de U-SQL-scripts.</span><span class="sxs-lookup"><span data-stu-id="4d7be-170">The DataLakeAnalyticsJobManagementClient provides methods to submit and manage jobs run on the database with U-SQL scripts.</span></span>

### <a name="list-databases-and-schemas"></a><span data-ttu-id="4d7be-171">Lijst met databases en schema 's</span><span class="sxs-lookup"><span data-stu-id="4d7be-171">List databases and schemas</span></span>
<span data-ttu-id="4d7be-172">Tussen de verschillende dingen die u kunt weergeven, zijn de meest voorkomende databases en hun schema.</span><span class="sxs-lookup"><span data-stu-id="4d7be-172">Among the several things you can list, the most common are databases and their schema.</span></span> <span data-ttu-id="4d7be-173">De volgende code verkrijgt van een verzameling van databases en vervolgens het schema voor elke database worden opgesomd.</span><span class="sxs-lookup"><span data-stu-id="4d7be-173">The following code obtains a collection of databases, and then enumerates the schema for each database.</span></span>

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

### <a name="list-table-columns"></a><span data-ttu-id="4d7be-174">Lijst met kolommen</span><span class="sxs-lookup"><span data-stu-id="4d7be-174">List table columns</span></span>
<span data-ttu-id="4d7be-175">De volgende code toont hoe u toegang tot de database met een client voor Data Lake Analytics-catalogus voor een lijst met de kolommen in een opgegeven tabel.</span><span class="sxs-lookup"><span data-stu-id="4d7be-175">The following code shows how to access the database with a Data Lake Analytics Catalog management client to list the columns in a specified table.</span></span>

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

### <a name="list-failed-jobs"></a><span data-ttu-id="4d7be-176">Mislukte taken weergeven</span><span class="sxs-lookup"><span data-stu-id="4d7be-176">List failed jobs</span></span>
<span data-ttu-id="4d7be-177">De volgende code geeft informatie over taken die niet zijn geslaagd.</span><span class="sxs-lookup"><span data-stu-id="4d7be-177">The following code lists information about jobs that failed.</span></span>

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a><span data-ttu-id="4d7be-178">Lijst pijplijnen</span><span class="sxs-lookup"><span data-stu-id="4d7be-178">List pipelines</span></span>
<span data-ttu-id="4d7be-179">De volgende code geeft informatie over elke pijplijn van taken die worden verzonden aan het account.</span><span class="sxs-lookup"><span data-stu-id="4d7be-179">The following code lists information about each pipeline of jobs submitted to the account.</span></span>

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a><span data-ttu-id="4d7be-180">Lijst met herhalingen</span><span class="sxs-lookup"><span data-stu-id="4d7be-180">List recurrences</span></span>
<span data-ttu-id="4d7be-181">De volgende code geeft informatie over elke herhaling van taken die worden verzonden aan het account.</span><span class="sxs-lookup"><span data-stu-id="4d7be-181">The following code lists information about each recurrence of jobs submitted to the account.</span></span>

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a><span data-ttu-id="4d7be-182">Algemene scenario's voor grafiek</span><span class="sxs-lookup"><span data-stu-id="4d7be-182">Common graph scenarios</span></span>

### <a name="look-up-user-in-the-aad-directory"></a><span data-ttu-id="4d7be-183">Gebruiker in de AAD-directory opzoeken</span><span class="sxs-lookup"><span data-stu-id="4d7be-183">Look up user in the AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-the-objectid-of-a-user-in-the-aad-directory"></a><span data-ttu-id="4d7be-184">Ophalen van de object-id van een gebruiker in het AAD-directory</span><span class="sxs-lookup"><span data-stu-id="4d7be-184">Get the ObjectId of a user in the AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a><span data-ttu-id="4d7be-185">Compute-beleid beheren</span><span class="sxs-lookup"><span data-stu-id="4d7be-185">Manage compute policies</span></span>
<span data-ttu-id="4d7be-186">Het object DataLakeAnalyticsAccountManagementClient biedt methoden voor het beheren van de compute-beleidsregels voor een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="4d7be-186">The DataLakeAnalyticsAccountManagementClient object provides methods for managing the compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="4d7be-187">Compute-beleidsregels weergeven</span><span class="sxs-lookup"><span data-stu-id="4d7be-187">List compute policies</span></span>
<span data-ttu-id="4d7be-188">De volgende code haalt een overzicht van compute-beleidsregels voor een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="4d7be-188">The following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="4d7be-189">Maak een nieuw compute-beleid</span><span class="sxs-lookup"><span data-stu-id="4d7be-189">Create a new compute policy</span></span>
<span data-ttu-id="4d7be-190">De volgende code maakt een nieuw compute-beleid voor een Data Lake Analytics-account, de maximale AUs beschikbaar stellen voor de opgegeven gebruiker tot 50 en de prioriteit van de minimale job 250.</span><span class="sxs-lookup"><span data-stu-id="4d7be-190">The following code creates a new compute policy for a Data Lake Analytics account, setting the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a><span data-ttu-id="4d7be-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d7be-191">Next steps</span></span>
* [<span data-ttu-id="4d7be-192">Overzicht van Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4d7be-192">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="4d7be-193">Azure Data Lake Analytics beheren met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4d7be-193">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="4d7be-194">Azure Data Lake Analytics-taken bewaken en problemen oplossen met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4d7be-194">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
