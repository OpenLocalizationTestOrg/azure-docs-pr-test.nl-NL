---
title: aaaMove gegevens van Sybase met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens van Sybase-Database met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ad003ec502028d56db9570fe08af329eb5b71817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a>Gegevens verplaatsen van Sybase met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een on-premises Sybase-database. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.

U kunt gegevens uit een on-premises Sybase gegevens store tooany ondersteund sink gegevensopslag kopiëren. Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel. Data factory ondersteunt momenteel alleen gegevens uit een Sybase-gegevens opslaan tooother gegevensarchieven verplaatsen, maar niet voor het verplaatsen van gegevens uit andere gegevens winkels tooa Sybase-gegevensarchief. 

## <a name="prerequisites"></a>Vereisten
Data Factory-service ondersteunt verbindende tooon lokale Sybase gegevensbronnen waarvoor gebruik Hallo Data Management Gateway. Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway.

Gateway is vereist, zelfs als Hallo Sybase-database wordt gehost in een Azure IaaS VM. U kunt Hallo gateway installeren op Hallo dezelfde IaaS VM als Hallo gegevens opslaan of op een andere virtuele machine zo lang Hallo gateway kunt verbinding maken met toohello-database.

> [!NOTE]
> Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.

## <a name="supported-versions-and-installation"></a>Ondersteunde versies en installatie
Data Management Gateway tooconnect toohello Sybase-Database, moet u tooinstall hello [data provider voor Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 of boven op Hallo hetzelfde systeem als Data Management Gateway Hallo. Sybase versie 16 en hoger wordt ondersteund.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's. 

- Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren. 
- U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. 
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. 

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een on-premises Sybase-gegevensopslag zijn [JSON-voorbeeld: gegevens kopiëren van Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) sectie van dit artikel. 

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooa Sybase-gegevensarchief zijn:

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooSybase gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **OnPremisesSybase** |Ja |
| server |Naam van Hallo Sybase-server. |Ja |
| database |Naam van Hallo Sybase-database. |Ja |
| Schema |Naam van Hallo schema in Hallo-database. |Nee |
| authenticationType |Type verificatie gebruikt tooconnect toohello Sybase-database. Mogelijke waarden zijn: anoniem, basis en Windows. |Ja |
| gebruikersnaam |Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt. |Nee |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven. |Nee |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale Sybase-database gebruiken. |Ja |

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).

Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo **typeProperties** sectie voor de gegevensset van het type **RelationalTable** (inclusief Sybase gegevensset) heeft Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van de tabel Hallo in Hallo Sybase-Database-instantie waarnaar de gekoppelde service verwijst. |Nee (als **query** van **RelationalSource** is opgegeven) |

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.

Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

Wanneer Hallo-bron is van het type **RelationalSource** (waaronder Sybase), Hallo volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: Selecteer * from MijnTabel. |Nee (als **tableName** van **gegevensset** is opgegeven) |


## <a name="json-example-copy-data-from-sybase-tooazure-blob"></a>JSON-voorbeeld: gegevens kopiëren van Sybase tooAzure Blob
Hallo volgende voorbeeld wordt een voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ze geven weer hoe toocopy gegevens van Sybase-database tooAzure Blob Storage. Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.   

Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:

1. Een gekoppelde service van het type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).
2. Een liked service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Hallo [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo voorbeeld kopieert gegevens van de resultaten van een query in een Sybase-database tooa blob elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

Instellen als eerste stap Hallo data management gateway. Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.

**Sybase gekoppelde service:**

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

**Azure Blob-opslag gekoppelde service:**

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

**Sybase invoergegevensset:**

Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Sybase en bevat een kolom met de naam 'tijdstempel' voor de reeksgegevens.

Instelling 'extern': true Hallo Data Factory-service informeert dat deze gegevensset externe toohello gegevensfactory en niet door een activiteit in de gegevensfactory hello wordt geproduceerd. U ziet dat Hallo **type** Hallo gekoppelde service is ingesteld op: **RelationalTable**.

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
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

**Azure Blob-uitvoergegevensset:**

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```JSON
{
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Pijplijn met de kopieeractiviteit:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun per uur is. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource** en **sink** type is ingesteld, te**BlobSink**. Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens uit Hallo DBA geselecteerd. Ordertabel in Hallo-database.

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a>Toewijzing van het type voor Sybase
Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel Hallo kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:

1. Systeemeigen bron typen too.NET type converteren
2. Converteren van .NET-type toonative sink-type

Sybase ondersteunt T-SQL en T-SQL-typen. Zie voor een toewijzingstabel van sql typen too.NET type [Azure SQL-Connector](data-factory-azure-sql-connector.md) artikel.

## <a name="map-source-toosink-columns"></a>Bronkolommen toosink toewijzen
Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Herhaalbare leesbewerking van relationele bronnen
Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten. In Azure Data Factory, kunt u een segment handmatig opnieuw. U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt. Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd. Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
