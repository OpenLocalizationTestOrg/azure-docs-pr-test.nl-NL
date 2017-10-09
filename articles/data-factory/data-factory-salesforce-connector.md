---
title: gegevens van de aaaMove van Salesforce met behulp van de Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens van Salesforce met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a>Gegevens verplaatsen van Salesforce met behulp van Azure Data Factory
In dit artikel bevat een overzicht van hoe u Kopieeractiviteit kunt gebruiken in een Azure data factory toocopy worden gegevens uit de gegevensopslag van Salesforce tooany die wordt vermeld onder Hallo Sink kolom in Hallo [ondersteunde gegevensbronnen en put](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel. In dit artikel is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin Kopieeractiviteit en combinaties van ondersteunde gegevens store een algemeen overzicht van de verplaatsing van gegevens biedt.

Azure Data Factory ondersteunt momenteel alleen te verplaatsen van gegevens van Salesforce[ondersteunde gegevensarchieven sink](data-factory-data-movement-activities.md#supported-data-stores-and-formats), maar ondersteunt geen bewegende gegevens van andere gegevens winkels tooSalesforce.

## <a name="supported-versions"></a>Ondersteunde versies
Deze connector ondersteunt de volgende edities van Salesforce Hallo: ontwikkelaarsversie, Professional Edition, Enterprise Edition of onbeperkte Edition. En het kopiëren van Salesforce productie, sandbox en aangepast domein ondersteunt.

## <a name="prerequisites"></a>Vereisten
* API-machtiging moet zijn ingeschakeld. Zie [hoe inschakelen API-toegang in Salesforce door machtigingenset?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)
* toocopy gegevens van Salesforce tooon-premises gegevensopslagexemplaren, hebt u ten minste Data Management Gateway 2.0 is geïnstalleerd in uw on-premises omgeving.

## <a name="salesforce-request-limits"></a>SalesForce aanvraaglimieten
SalesForce heeft limieten voor totaal aantal API-aanvragen en de gelijktijdige API-aanvragen. Houd er rekening mee Hallo volgende punten:

- Als het aantal gelijktijdige aanvragen Hallo Hallo limiet overschrijdt, beperking plaatsvindt en worden er willekeurige fouten.
- Als het totale aantal aanvragen Hallo Hallo limiet overschrijdt, wordt Hallo Salesforce-account van 24 uur geblokkeerd.

Hallo "REQUEST_LIMIT_EXCEEDED" fout kan ook worden weergegeven in beide scenario's. Zie sectie Hallo 'API aanvraaglimieten' in hello [Salesforce Developer limieten](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) artikel voor meer informatie.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens worden verplaatst van Salesforce met verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren: 

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. 
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. 

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van Salesforce zijn [JSON-voorbeeld: gegevens kopiëren van Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) sectie van dit artikel. 

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooSalesforce zijn: 

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel bevat beschrijvingen van JSON-elementen die specifiek toohello Salesforce gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **Salesforce**. |Ja |
| environmentUrl | Hallo-URL van de Salesforce-exemplaar opgeven. <br><br> -Standaard is 'https://login.salesforce.com'. <br> -toocopy gegevens van de sandbox, 'https://test.salesforce.com' opgeven. <br> -toocopy gegevens van aangepast domein opgeven, bijvoorbeeld 'https://[domain].my.salesforce.com'. |Nee |
| gebruikersnaam |Geef een gebruikersnaam voor Hallo-gebruikersaccount. |Ja |
| wachtwoord |Geef een wachtwoord voor gebruikersaccount Hallo. |Ja |
| securityToken |Geef een beveiligingstoken voor Hallo-gebruikersaccount. Zie [security token ophalen](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) voor instructies over het tooreset of ophalen van een beveiligingstoken. toolearn over beveiligingstokens in het algemeen Zie [beveiligings- en Hallo API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Ja |

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets en secties Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen gegevensset (Azure blob Azure SQL Azure-tabel en enzovoort).

Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo typeProperties sectie voor een gegevensset van het type Hallo **RelationalTable** heeft Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |Naam van de tabel Hallo in Salesforce. |Nee (als een **query** van **RelationalSource** is opgegeven) |

> [!IMPORTANT]
> Hallo '__c' onderdeel Hallo API-naam is vereist voor elk object dat aangepast.

![Naam van de Data Factory - verbinding Salesforce - API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst van de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten en secties Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen, zoals naam, beschrijving, invoer en uitvoer tabellen en verschillende beleidsregels zijn beschikbaar voor alle typen activiteiten.

Hallo-eigenschappen die beschikbaar zijn in de sectie typeProperties van Hallo-activiteit op Hallo daarentegen Hallo, variëren met elk activiteitstype. Voor de Kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

In de kopieeractiviteit, wanneer bron Hallo Hallo type **RelationalSource** (waaronder Salesforce), Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |Een SQL-92-query of [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query. Bijvoorbeeld `select * from MyTable__c`. |Nee (als hello **tableName** Hallo **gegevensset** is opgegeven) |

> [!IMPORTANT]
> Hallo '__c' onderdeel Hallo API-naam is vereist voor elk object dat aangepast.

![Naam van de Data Factory - verbinding Salesforce - API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a>Tips voor query
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>Bij het ophalen van gegevens met behulp van waar component voor datum/tijd-kolom
Geef bij de Hallo SOQL of SQL-query, betalen aandacht toohello verschil van datum/tijd-indeling. Bijvoorbeeld:

* **Voorbeeld van SOQL**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`
* **SQL-voorbeeld**:
    * **Met behulp van kopie wizard toospecify Hallo query:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`
    * **Met een JSON toospecify Hallo query bewerken (char goed escape):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`

### <a name="retrieving-data-from-salesforce-report"></a>Ophalen van gegevens uit het Salesforce-rapport
U kunt gegevens ophalen uit het Salesforce-rapporten door te geven van de query als `{call "<report name>"}`, bijvoorbeeld. `"query": "{call \"TestReport\"}"`.

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>Bij het ophalen van records verwijderd uit Salesforce Prullenbak
tooquery hello voorlopig verwijderde records uit Salesforce-Prullenbak, kunt u **' IsDeleted = 1 "** in uw query. Bijvoorbeeld:

* tooquery alleen Hallo verwijderde records opgeven "Selecteer * uit MyTable__c **waar IsDeleted = 1**'
* alle records Hallo bestaande en Hallo verwijderd, inclusief Hallo tooquery opgeven "Selecteer * uit MyTable__c **waar IsDeleted = 0 of IsDeleted = 1**'

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a>JSON-voorbeeld: gegevens kopiëren van Salesforce tooAzure Blob
Hallo volgende voorbeeld wordt een voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van Hallo [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ze geven weer hoe toocopy gegevens van Salesforce tooAzure Blob Storage. Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.   

Hier volgen Hallo Data Factory-artefacten moet u toocreate tooimplement Hallo scenario. Hallo gedeelten Hallo lijst vindt u meer informatie over deze stappen.

* Een gekoppelde service van het type Hallo [Salesforce](#linked-service-properties)
* Een gekoppelde service van het type Hallo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Invoer [gegevensset](data-factory-create-datasets.md) van het type Hallo [RelationalTable](#dataset-properties)
* Uitvoer [gegevensset](data-factory-create-datasets.md) van het type Hallo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

**SalesForce gekoppelde service**

In dit voorbeeld wordt Hallo **Salesforce** gekoppelde service. Zie Hallo [Salesforce gekoppelde service](#linked-service-properties) gedeelte voor het Hallo-eigenschappen die worden ondersteund door deze gekoppelde service.  Zie [security token ophalen](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) voor instructies over hoe tooreset/get Hallo-beveiligingstoken.

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
**Een gekoppelde Azure Storage-service**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
    }
}
```
**SalesForce invoergegevensset**

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Instelling **externe** te**true** informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

> [!IMPORTANT]
> Hallo '__c' onderdeel Hallo API-naam is vereist voor elk object dat aangepast.

![Naam van de Data Factory - verbinding Salesforce - API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

**De Azure Blob-uitvoergegevensset**

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Pijplijn met de Kopieeractiviteit**

Hallo pipeline bevat Kopieeractiviteit die wordt geconfigureerd toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource**, en Hallo **sink** type is ingesteld, te**BlobSink**.

Zie [RelationalSource type-eigenschappen](#copy-activity-properties) voor Hallo lijst met eigenschappen die worden ondersteund door Hallo RelationalSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }
        ]
    }
}
```
> [!IMPORTANT]
> Hallo '__c' onderdeel Hallo API-naam is vereist voor elk object dat aangepast.

![Naam van de Data Factory - verbinding Salesforce - API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a>Toewijzing van het type voor Salesforce
| SalesForce-type | . Type op basis van NET |
| --- | --- |
| Automatische getal |Tekenreeks |
| Selectievakje |Booleaanse waarde |
| Valuta |dubbele |
| Date |Datum/tijd |
| Datum/tijd |Datum/tijd |
| E-mail |Tekenreeks |
| Id |Tekenreeks |
| Opzoekrelatie |Tekenreeks |
| Meervoudige selectie selectielijst |Tekenreeks |
| Aantal |dubbele |
| Procent |dubbele |
| Telefoon |Tekenreeks |
| Selectielijst |Tekenreeks |
| Tekst |Tekenreeks |
| Tekstgebied |Tekenreeks |
| Tekstgebied (lang) |Tekenreeks |
| Tekstgebied (uitgebreid) |Tekenreeks |
| Tekst (versleuteld) |Tekenreeks |
| URL |Tekenreeks |

> [!NOTE]
> toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a>Prestaties en afstemmen
Zie Hallo [Kopieeractiviteit prestaties en prestatieafstemming handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
