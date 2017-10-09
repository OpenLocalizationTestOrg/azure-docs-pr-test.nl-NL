---
title: aaaTransform gegevens met behulp van U-SQL-script - Azure | Microsoft Docs
description: Meer informatie over hoe de service voor het berekenen van tooprocess of transformatie gegevens door op Azure Data Lake Analytics U-SQL-scripts.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a>Transformeer gegevens door het U-SQL-scripts uitvoeren op Azure Data Lake Analytics 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive-activiteit](data-factory-hive-activity.md) 
> * [Pig-activiteit](data-factory-pig-activity.md)
> * [MapReduce-activiteit](data-factory-map-reduce.md)
> * [Hadoop-Streamingactiviteit](data-factory-hadoop-streaming-activity.md)
> * [Spark-activiteit](data-factory-spark.md)
> * [Machine Learning-batchuitvoeringsactiviteit](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning-activiteit resources bijwerken](data-factory-azure-ml-update-resource-activity.md)
> * [Opgeslagen procedureactiviteit](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL-activiteit](data-factory-usql-activity.md)
> * [Aangepaste activiteit .NET](data-factory-use-custom-activities.md)

Een pijplijn in een Azure data factory verwerkt gegevens in gekoppelde storage-services met behulp van gekoppelde compute services. Het bevat een reeks activiteiten, waarbij elke activiteit uitvoert voor een specifieke verwerking. Dit artikel wordt beschreven Hallo **Data Lake Analytics U-SQL-activiteit** die wordt uitgevoerd een **U-SQL** script op een **Azure Data Lake Analytics** berekenen van de gekoppelde service. 

> [!NOTE]
> Een Azure Data Lake Analytics-account maken voordat u een pijplijn maakt met een Data Lake Analytics U-SQL-activiteit. Zie toolearn over Azure Data Lake Analytics [aan de slag met Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).
> 
> Bekijk Hallo [bouwen van uw eerste pijplijn-zelfstudie](data-factory-build-your-first-pipeline.md) voor gedetailleerde stappen toocreate een gegevensfactory, gekoppelde services, gegevenssets en een pijplijn. JSON-codefragmenten gebruiken met Data Factory-Editor of Visual Studio of Azure PowerShell toocreate Data Factory-entiteiten.

## <a name="supported-authentication-types"></a>Ondersteunde verificatietypen
U-SQL-activiteit ondersteunt hieronder verificatietypen tegen Data Lake Analytics:
* Verificatie van service-principal
* Verificatie van gebruikersreferenties (OAuth) 

Het is raadzaam dat u service-principal verificatie, met name voor een geplande U-SQL-uitvoering. Verlopen van het token kan gebeuren met verificatie van gebruikersreferenties. Zie voor configuratiedetails Hallo [gekoppelde service-eigenschappen](#azure-data-lake-analytics-linked-service) sectie.

## <a name="azure-data-lake-analytics-linked-service"></a>Azure Data Lake Analytics gekoppelde Service
U maakt een **Azure Data Lake Analytics** gekoppelde service toolink een Azure Data Lake Analytics compute-service tooan Azure data factory. Hallo Data Lake Analytics U-SQL-activiteit in de pijplijn Hallo verwijst toothis gekoppelde service. 

Hallo bevat volgende tabel beschrijvingen van Hallo generieke eigenschappen die worden gebruikt in Hallo JSON-definitie. U kunt verder tussen service-principal en verificatie van gebruikersreferenties.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| **type** |Hallo type eigenschap moet worden ingesteld op: **AzureDataLakeAnalytics**. |Ja |
| **Accountnaam** |Azure Data Lake Analytics-accountnaam. |Ja |
| **dataLakeAnalyticsUri** |Azure Data Lake Analytics-URI. |Nee |
| **abonnements-id** |Azure-abonnement-id |Nee (als dit niet is opgegeven, abonnement van Hallo data factory wordt gebruikt). |
| **resourceGroupName** |Naam van een Azure-resourcegroep |Nee (als dit niet is opgegeven, brongroep van Hallo data factory wordt gebruikt). |

### <a name="service-principal-authentication-recommended"></a>Verificatie van de service principal (aanbevolen)
toouse service principal verificatie, de registratie een Toepassingsentiteit in Azure Active Directory (Azure AD) en verleen het Hallo toegang krijgen tot de tooData Lake Store. Zie voor gedetailleerde stappen [authentication Service-naar-serviceconnector](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Noteer Hallo waarden, waarin u volgende toodefine Hallo gekoppelde service:
* Toepassings-id
* Sleutel van toepassing 
* Tenant-id

Verificatie van de service-principal door te geven van de volgende eigenschappen hello gebruiken:

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| **servicePrincipalId** | Geef Hallo van client-id op. | Ja |
| **servicePrincipalKey** | De sleutel van de toepassing hello opgeven. | Ja |
| **tenant** | Geef informatie op Hallo tenant (domain name of tenant-ID) in uw toepassing zich bevindt. U kunt deze ophalen door zwevende Hallo muis in Hallo rechterbovenhoek Hallo Azure-portal. | Ja |

**Voorbeeld: Service-principal-verificatie**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Verificatie van gebruikersreferenties
Ook kunt u verificatie van gebruikersreferenties voor Data Lake Analytics door te geven Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| **autorisatie** | Klik op Hallo **autoriseren** knop op Hallo Data Factory-Editor en voer uw referenties die Hallo automatisch gegenereerde autorisatie-URL toothis eigenschap toewijst. | Ja |
| **sessie-id** | OAuth-sessie-ID van Hallo OAuth-autorisatie-sessie. Elke sessie-ID is uniek en kan slechts één keer worden gebruikt. Deze instelling wordt automatisch gegenereerd wanneer u Hallo Data Factory-Editor. | Ja |

**Voorbeeld: Verificatie van gebruikersreferenties**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Verlopen van het token
Hallo autorisatiecode die u hebt gegenereerd met Hallo **autoriseren** knop verloopt na enige tijd opnieuw. Zie de volgende tabel voor Hallo verlopen tijden voor verschillende soorten gebruikersaccounts Hallo. Mogelijk ziet u Hallo volgende foutbericht weergegeven wanneer Hallo verificatie **-token verloopt**: referentie-bewerkingsfout: invalid_grant - AADSTS70002: fout bij het valideren van referenties. AADSTS70008: Hallo opgegeven toegangsmachtiging is verlopen of ingetrokken. Traceer-ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 correlatie-ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 tijdstempel: 2015-12-15 21:09:31Z

| Gebruikerstype | Verloopt na |
|:--- |:--- |
| Gebruikersaccounts die niet worden beheerd door Azure Active Directory (@hotmail.com, @live.com, enz.) |12 uur |
| Gebruikersaccounts die worden beheerd door Azure Active Directory (AAD) |het is 14 dagen na de laatste segment Hallo worden uitgevoerd. <br/><br/>negentig dagen weergegeven, als een segment op basis van de gekoppelde service op basis van OAuth ten minste eenmaal in de 14 dagen wordt uitgevoerd. |

tooavoid/los deze fout, opnieuw autoriseren hello met **autoriseren** wanneer hello **-token verloopt** en implementeer gekoppelde Hallo-service opnieuw. U kunt ook de waarden voor genereren **sessionId** en **autorisatie** eigenschappen programmatisch met code als volgt:

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

Zie [AzureDataLakeStoreLinkedService klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), en [AuthorizationSessionGetResponse klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) onderwerpen voor meer informatie informatie over Hallo Data Factory-klassen in Hallo code gebruikt. Voeg een verwijzing naar: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll voor Hallo WindowsFormsWebAuthenticationDialog klasse. 

## <a name="data-lake-analytics-u-sql-activity"></a>Data Lake Analytics U-SQL-activiteit
Hallo volgende JSON-codefragment definieert een pijplijn met een Data Lake Analytics U-SQL-activiteit. Hallo activiteitsdefinitie bevat een verwijzing toohello Azure Data Lake Analytics gekoppelde service die u eerder hebt gemaakt.   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

Hallo volgende tabel beschrijft namen en beschrijvingen van eigenschappen die specifiek toothis activiteit zijn. 

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| type |de eigenschap type Hello te moet worden ingesteld**DataLakeAnalyticsU SQL**. |Ja |
| scriptPath |Pad toofolder met Hallo U-SQL-script. Naam van bestand Hallo is hoofdlettergevoelig. |Nee (als u een script gebruiken) |
| scriptLinkedService |Gekoppelde service die is gekoppeld aan Hallo-opslag met Hallo script toohello data factory |Nee (als u een script gebruiken) |
| Script |Geef in plaats van het opgeven van scriptPath en scriptLinkedService inline-script. Bijvoorbeeld: `"script": "CREATE DATABASE test"`. |Nee (als u scriptPath en scriptLinkedService gebruiken) |
| degreeOfParallelism |maximum aantal knooppunten Hallo toorun Hallo taak tegelijkertijd worden gebruikt. |Nee |
| Prioriteit |Hiermee wordt bepaald welke taken uit in de wachtrij moeten geselecteerde toorun eerst. Hallo Hallo minder, Hallo hogere Hallo prioriteit. |Nee |
| parameters |Parameters voor Hallo U-SQL-script |Nee |
| runtimeVersion | Runtime-versie van Hallo U-SQL-engine toouse | Nee | 
| compilationMode | <p>Compilatiemodus van U-SQL. Moet een van de volgende waarden:</p> <ul><li>**Semantische:** alleen uitvoeren semantische controles en de benodigde bevestigingen.</li><li>**Volledige:** uitvoeren Hallo volledige compilatie, met inbegrip van syntaxiscontrole, optimalisatie, genereren van code, enzovoort.</li><li>**SingleBox:** Hallo volledige compilatie, met TargetType instelling tooSingleBox uitvoeren.</li></ul><p>Als u een waarde voor deze eigenschap niet opgeeft, bepaalt Hallo server Hallo optimale compilatiemodus. </p>| Nee | 

Zie [SearchLogProcessing.txt Script definitie](#sample-u-sql-script) voor Hallo script definitie. 

## <a name="sample-input-and-output-datasets"></a>Voorbeeld van invoer- en uitvoergegevenssets
### <a name="input-dataset"></a>Invoergegevensset
In dit voorbeeld is de invoergegevens Hallo bevindt zich in een Azure Data Lake Store (SearchLog.tsv-bestand in Hallo datalake/invoer map). 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a>Uitvoergegevensset
In dit voorbeeld wordt Hallo uitvoergegevens die wordt geproduceerd door Hallo U-SQL-script opgeslagen in een Azure Data Lake Store (datalake/uitvoermap). 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a>Sample Data Lake Store gekoppelde Service
Hier is Hallo definitie van Hallo voorbeeld die Azure Data Lake Store service die wordt gebruikt door Hallo i gekoppelde/o-gegevenssets. 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

Zie [tooand gegevens verplaatsen van Azure Data Lake Store](data-factory-azure-datalake-connector.md) artikel voor een beschrijving van de JSON-eigenschappen. 

## <a name="sample-u-sql-script"></a>U-SQL-voorbeeldscript

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

waarden voor Hallo  **@in**  en  **@out**  parameters in Hallo U-SQL-script worden doorgegeven dynamisch door ADF Hallo 'parameters' sectie. Zie Hallo 'parameters' in hello pijplijn definitie.

U kunt ook andere eigenschappen zoals degreeOfParallelism en prioriteit opgeven in de definitie van de pijplijn voor Hallo-taken die worden uitgevoerd op Hallo Azure Data Lake Analytics-service.

## <a name="dynamic-parameters"></a>Dynamische parameters
In Hallo voorbeeld pijplijn definitie zijn in en uit parameters toegewezen met vastgelegde waarden. 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

Dynamische parameters mogelijke toouse is in plaats daarvan. Bijvoorbeeld: 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

In dit geval invoerbestanden zijn nog steeds opgehaald uit Hallo /datalake/input map en uitvoerbestanden worden gegenereerd in Hallo /datalake/output map. Hallo-bestandsnamen zijn dynamisch, op basis van de begintijd van Hallo segment.  

