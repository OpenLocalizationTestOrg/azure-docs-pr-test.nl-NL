---
title: aaaManage Azure Data Lake Analytics met behulp van Python | Microsoft Docs
description: 'Meer informatie over hoe toouse Python toocreate een Data Lake opslaan account en het verzenden van taken. '
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: d4213a19-4d0f-49c9-871c-9cd6ed7cf731
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 3c0fff155db7c4fd4e84c2562816995eb156be16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="35f7e-103">Azure Data Lake Analytics beheren met Python</span><span class="sxs-lookup"><span data-stu-id="35f7e-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="35f7e-104">Python-versies</span><span class="sxs-lookup"><span data-stu-id="35f7e-104">Python versions</span></span>

* <span data-ttu-id="35f7e-105">Een 64-bits versie van Python gebruiken.</span><span class="sxs-lookup"><span data-stu-id="35f7e-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="35f7e-106">U kunt Hallo Python standaarddistributiepunt gevonden op  **[Python.org downloadt](https://www.python.org/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="35f7e-106">You can use hello standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="35f7e-107">Veel ontwikkelaars deze handige toouse Hallo vinden  **[Anaconda Python-distributie](https://www.continuum.io/downloads)**.</span><span class="sxs-lookup"><span data-stu-id="35f7e-107">Many developers find it convenient toouse hello **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="35f7e-108">Dit artikel is geschreven met behulp van Python-versie 3.6 uit Hallo Python-distributie</span><span class="sxs-lookup"><span data-stu-id="35f7e-108">This article was written using Python version 3.6 from hello standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="35f7e-109">Azure Python-SDK installeren</span><span class="sxs-lookup"><span data-stu-id="35f7e-109">Install Azure Python SDK</span></span>

<span data-ttu-id="35f7e-110">Hallo volgende modules installeren:</span><span class="sxs-lookup"><span data-stu-id="35f7e-110">Install hello following modules:</span></span>

* <span data-ttu-id="35f7e-111">Hallo **azure-mgmt-resource** -module bevat andere Azure-modules voor Active Directory, enz.</span><span class="sxs-lookup"><span data-stu-id="35f7e-111">hello **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="35f7e-112">Hallo **azure-mgmt-datalake-store** -module bevat beheerbewerkingen voor hello Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="35f7e-112">hello **azure-mgmt-datalake-store** module includes hello Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="35f7e-113">Hallo **azure-datalake-store** module hello Azure Data Lake Store bestandssysteembewerkingen bevat.</span><span class="sxs-lookup"><span data-stu-id="35f7e-113">hello **azure-datalake-store** module includes hello Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="35f7e-114">Hallo **azure-datalake-analytics** module omvat hello Azure Data Lake Analytics-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="35f7e-114">hello **azure-datalake-analytics** module includes hello Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="35f7e-115">Eerst voor zorgen er Hallo laatste `pip` door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="35f7e-115">First, ensure you have hello latest `pip` by running hello following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="35f7e-116">Dit document is geschreven met `pip version 9.0.1`.</span><span class="sxs-lookup"><span data-stu-id="35f7e-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="35f7e-117">Gebruik de volgende Hallo `pip` tooinstall Hallo-modules uit Hallo commandline-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="35f7e-117">Use hello following `pip` commands tooinstall hello modules from hello commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="35f7e-118">Een nieuwe pythonscript maken</span><span class="sxs-lookup"><span data-stu-id="35f7e-118">Create a new Python script</span></span>

<span data-ttu-id="35f7e-119">Plak de volgende code in een script Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="35f7e-119">Paste hello following code into hello script:</span></span>

```python
## Use this only for Azure AD service-to-service authentication
#from azure.common.credentials import ServicePrincipalCredentials

## Use this only for Azure AD end-user authentication
#from azure.common.credentials import UserPassCredentials

## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

## Required for Azure Data Lake Analytics catalog management
from azure.mgmt.datalake.analytics.catalog import DataLakeAnalyticsCatalogManagementClient

## Use these as needed for your application
import logging, getpass, pprint, uuid, time
```

<span data-ttu-id="35f7e-120">Voer dit script tooverify die Hallo modules kunnen worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="35f7e-120">Run this script tooverify that hello modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="35f7e-121">Authentication</span><span class="sxs-lookup"><span data-stu-id="35f7e-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="35f7e-122">Interactieve gebruikersverificatie met een pop-upvenster</span><span class="sxs-lookup"><span data-stu-id="35f7e-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="35f7e-123">Deze methode wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="35f7e-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="35f7e-124">Interactieve gebruikersverificatie met een apparaatcode</span><span class="sxs-lookup"><span data-stu-id="35f7e-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="35f7e-125">Niet-interactieve verificatie met SPI en een geheim</span><span class="sxs-lookup"><span data-stu-id="35f7e-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="35f7e-126">Niet-interactieve verificatie met de API en een certificaat</span><span class="sxs-lookup"><span data-stu-id="35f7e-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="35f7e-127">Deze methode wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="35f7e-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="35f7e-128">Algemene scriptvariabelen</span><span class="sxs-lookup"><span data-stu-id="35f7e-128">Common script variables</span></span>

<span data-ttu-id="35f7e-129">Deze variabelen worden gebruikt in de voorbeelden van Hallo.</span><span class="sxs-lookup"><span data-stu-id="35f7e-129">These variables are used in hello samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a><span data-ttu-id="35f7e-130">Hallo-clients maken</span><span class="sxs-lookup"><span data-stu-id="35f7e-130">Create hello clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="35f7e-131">Een Azure-resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="35f7e-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="35f7e-132">Een Data Lake Analytics-account maken</span><span class="sxs-lookup"><span data-stu-id="35f7e-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="35f7e-133">Maak eerst een store-account.</span><span class="sxs-lookup"><span data-stu-id="35f7e-133">First create a store account.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```
<span data-ttu-id="35f7e-134">Maakt een ADLA-account dat dit archief wordt op.</span><span class="sxs-lookup"><span data-stu-id="35f7e-134">Then create an ADLA account that uses that store.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```

## <a name="submit-a-job"></a><span data-ttu-id="35f7e-135">Verzenden van een taak</span><span class="sxs-lookup"><span data-stu-id="35f7e-135">Submit a job</span></span>

```python
script = """
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

## <a name="wait-for-a-job-tooend"></a><span data-ttu-id="35f7e-136">Wachten op een taak tooend</span><span class="sxs-lookup"><span data-stu-id="35f7e-136">Wait for a job tooend</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="35f7e-137">Lijst met pijplijnen en herhalingen</span><span class="sxs-lookup"><span data-stu-id="35f7e-137">List pipelines and recurrences</span></span>
<span data-ttu-id="35f7e-138">Afhankelijk van of uw taken pijplijn of terugkeerpatroon metagegevens gekoppeld hebt, kunt u pijplijnen en terugkeerpatronen aanbieden.</span><span class="sxs-lookup"><span data-stu-id="35f7e-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="35f7e-139">Compute-beleid beheren</span><span class="sxs-lookup"><span data-stu-id="35f7e-139">Manage compute policies</span></span>

<span data-ttu-id="35f7e-140">Hallo DataLakeAnalyticsAccountManagementClient object biedt methoden voor het beheer van Hallo compute-beleid voor een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="35f7e-140">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="35f7e-141">Compute-beleidsregels weergeven</span><span class="sxs-lookup"><span data-stu-id="35f7e-141">List compute policies</span></span>

<span data-ttu-id="35f7e-142">Hallo volgende code haalt een lijst met compute-beleidsregels voor een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="35f7e-142">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="35f7e-143">Maak een nieuw compute-beleid</span><span class="sxs-lookup"><span data-stu-id="35f7e-143">Create a new compute policy</span></span>

<span data-ttu-id="35f7e-144">Hallo volgende code maakt een nieuw beleid voor een Data Lake Analytics-account voor compute, instelling Hallo maximale AUs beschikbaar toohello opgegeven gebruiker too50 en Hallo Minimumprioriteit prioriteit too250.</span><span class="sxs-lookup"><span data-stu-id="35f7e-144">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="35f7e-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="35f7e-145">Next steps</span></span>

- <span data-ttu-id="35f7e-146">toosee Hallo dezelfde zelfstudie met een ander hulpprogramma, klikt u op Hallo-tabselectors op Hallo Hallo pagina bovenaan.</span><span class="sxs-lookup"><span data-stu-id="35f7e-146">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
- <span data-ttu-id="35f7e-147">toolearn U-SQL, Zie [aan de slag met Azure Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="35f7e-147">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="35f7e-148">Zie [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md) voor informatie over beheertaken.</span><span class="sxs-lookup"><span data-stu-id="35f7e-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

