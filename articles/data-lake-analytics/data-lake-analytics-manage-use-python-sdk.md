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
# <a name="manage-azure-data-lake-analytics-using-python"></a>Azure Data Lake Analytics beheren met Python

## <a name="python-versions"></a>Python-versies

* Een 64-bits versie van Python gebruiken.
* U kunt Hallo Python standaarddistributiepunt gevonden op  **[Python.org downloadt](https://www.python.org/downloads/)**. 
* Veel ontwikkelaars deze handige toouse Hallo vinden  **[Anaconda Python-distributie](https://www.continuum.io/downloads)**.  
* Dit artikel is geschreven met behulp van Python-versie 3.6 uit Hallo Python-distributie

## <a name="install-azure-python-sdk"></a>Azure Python-SDK installeren

Hallo volgende modules installeren:

* Hallo **azure-mgmt-resource** -module bevat andere Azure-modules voor Active Directory, enz.
* Hallo **azure-mgmt-datalake-store** -module bevat beheerbewerkingen voor hello Azure Data Lake Store-account.
* Hallo **azure-datalake-store** module hello Azure Data Lake Store bestandssysteembewerkingen bevat. 
* Hallo **azure-datalake-analytics** module omvat hello Azure Data Lake Analytics-bewerkingen. 

Eerst voor zorgen er Hallo laatste `pip` door het uitvoeren van de volgende opdracht Hallo:

```
python -m pip install --upgrade pip
```

Dit document is geschreven met `pip version 9.0.1`.

Gebruik de volgende Hallo `pip` tooinstall Hallo-modules uit Hallo commandline-opdrachten:

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a>Een nieuwe pythonscript maken

Plak de volgende code in een script Hallo Hallo:

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

Voer dit script tooverify die Hallo modules kunnen worden geïmporteerd.

## <a name="authentication"></a>Authentication

### <a name="interactive-user-authentication-with-a-pop-up"></a>Interactieve gebruikersverificatie met een pop-upvenster

Deze methode wordt niet ondersteund.

### <a name="interactive-user-authentication-with-a-device-code"></a>Interactieve gebruikersverificatie met een apparaatcode

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a>Niet-interactieve verificatie met SPI en een geheim

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a>Niet-interactieve verificatie met de API en een certificaat

Deze methode wordt niet ondersteund.

## <a name="common-script-variables"></a>Algemene scriptvariabelen

Deze variabelen worden gebruikt in de voorbeelden van Hallo.

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a>Hallo-clients maken

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a>Een Azure-resourcegroep maken

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a>Een Data Lake Analytics-account maken

Maak eerst een store-account.

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
Maakt een ADLA-account dat dit archief wordt op.

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

## <a name="submit-a-job"></a>Verzenden van een taak

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

## <a name="wait-for-a-job-tooend"></a>Wachten op een taak tooend

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a>Lijst met pijplijnen en herhalingen
Afhankelijk van of uw taken pijplijn of terugkeerpatroon metagegevens gekoppeld hebt, kunt u pijplijnen en terugkeerpatronen aanbieden.

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a>Compute-beleid beheren

Hallo DataLakeAnalyticsAccountManagementClient object biedt methoden voor het beheer van Hallo compute-beleid voor een Data Lake Analytics-account.

### <a name="list-compute-policies"></a>Compute-beleidsregels weergeven

Hallo volgende code haalt een lijst met compute-beleidsregels voor een Data Lake Analytics-account.

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a>Maak een nieuw compute-beleid

Hallo volgende code maakt een nieuw beleid voor een Data Lake Analytics-account voor compute, instelling Hallo maximale AUs beschikbaar toohello opgegeven gebruiker too50 en Hallo Minimumprioriteit prioriteit too250.

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a>Volgende stappen

- toosee Hallo dezelfde zelfstudie met een ander hulpprogramma, klikt u op Hallo-tabselectors op Hallo Hallo pagina bovenaan.
- toolearn U-SQL, Zie [aan de slag met Azure Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md).
- Zie [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md) voor informatie over beheertaken.

