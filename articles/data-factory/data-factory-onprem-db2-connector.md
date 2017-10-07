---
title: gegevens van de aaaMove van DB2 met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over hoe toomove gegevens uit een lokale DB2-database met behulp van Azure Data Factory-Kopieeractiviteit
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a>Gegevens verplaatsen van DB2 met behulp van Azure Data Factory-Kopieeractiviteit
Dit artikel wordt beschreven hoe u de Kopieeractiviteit in Azure Data Factory toocopy gegevens van een gegevensarchief voor lokale DB2-database tooa kunt gebruiken. U kunt kopiëren tooany gegevensopslag die wordt vermeld als een ondersteunde sink in Hallo [activiteiten voor gegevensverplaatsing Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats) artikel. In dit onderwerp is gebaseerd op Hallo Data Factory-artikel, dat geeft een overzicht van de verplaatsing van gegevens met behulp van de Kopieeractiviteit en lijsten Hallo ondersteund data store combinaties. 

Data Factory ondersteunt momenteel alleen zwevend gegevens uit een DB2-database tooa [ondersteunde sink gegevensarchief](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Verplaatsen van gegevens van andere gegevens worden opgeslagen tooa DB2-database wordt niet ondersteund.

## <a name="prerequisites"></a>Vereisten
Data Factory ondersteunt verbindende tooan lokale DB2-database met behulp van Hallo [data management gateway](data-factory-data-management-gateway.md). Stapsgewijze instructies tooset Hallo gateway upgegevens toomove met uw gegevens pipeline, kunt u Hallo [verplaatsen van gegevens uit de lokale toocloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.

Een gateway is vereist, zelfs als hello DB2 op Azure IaaS VM gehost wordt. U kunt Hallo gateway installeren op Hallo dezelfde IaaS VM als Hallo-gegevensarchief. Als Hallo gateway verbinding toohello database maken kunt, kunt u Hallo gateway installeren op een andere virtuele machine.

Hallo data management gateway biedt een ingebouwd DB2-stuurprogramma, zodat u niet moet toomanually installeert een stuurprogramma toocopy gegevens uit een DB2.

> [!NOTE]
> Zie voor tips over het oplossen van de verbinding en gateway problemen Hallo [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) artikel.


## <a name="supported-versions"></a>Ondersteunde versies
Hallo Data Factory DB2-connector ondersteunt Hallo IBM DB2-platformen en versies met gedistribueerd relationele Database architectuur (DRDA) SQL toegang Manager versie 9, 10 en 11 te volgen:

* IBM DB2 voor z-/ OS-versie 11.1
* IBM DB2 voor z-/ OS-versie 10.1
* IBM DB2 voor i (AS400) versie 7.2
* IBM DB2 voor i (AS400) versie 7.1
* IBM DB2 voor Linux, UNIX- en Windows (LUW) versie 11
* IBM DB2 voor LUW versie 10.5
* IBM DB2 voor LUW versie 10.1

> [!TIP]
> Als u Hallo 'hello pakket bijbehorende tooan SQL-instructie aanvraag voor het uitvoeren is niet gevonden foutbericht. SQLSTATE 805-51002 SQLCODE =, = "hello reden hiervoor is een benodigde pakket is niet gemaakt voor normale gebruiker Hallo op Hallo OS. tooresolve dit probleem, volgt u deze instructies voor het type DB2:
> - DB2 voor i (AS400): laat een hoofdgebruiker Hallo verzameling voor normale gebruiker Hallo voordat u Kopieeractiviteit maken. toocreate hello verzameling Hallo-opdracht gebruiken:`create collection <username>`
> - DB2 voor z-/ OS of LUW: gebruik een account met hoge bevoegdheden--hoofdgebruiker of beheerder met pakket-instanties en BIND, BINDADD, moeten de MACHTIGINGEN EXECUTE tooPUBLIC--toorun Hallo eenmaal kopiëren. Hallo benodigde pakket wordt automatisch gemaakt tijdens het Hallo kopiëren. Daarna kunt u back-toohello normale gebruiker schakelen voor uw volgende kopie wordt uitgevoerd.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopie activiteit toomove gegevens uit een on-premises DB2-gegevensopslag met behulp van verschillende hulpprogramma's en API's: 

- Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello Azure Data Factory-Wizard voor kopiëren. Zie voor een snel overzicht over het maken van een pijplijn met behulp van de Wizard kopiëren Hallo Hallo [zelfstudie: een pijplijn maken met behulp van de Wizard kopiëren Hallo](data-factory-copy-data-wizard-tutorial.md). 
- U kunt ook extra toocreate een pijplijn, met inbegrip van hello Azure-portal, Visual Studio, Azure PowerShell, een Azure Resource Manager-sjabloon, Hallo .NET API en Hallo REST-API. Zie voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit, Hallo [Kopieeractiviteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:

1. Gekoppelde services toolink en uitvoergegevens winkels tooyour een gegevensfactory maken.
2. Maakt u gegevenssets toorepresent invoer en uitvoergegevens voor Hallo kopieerbewerking. 
3. Een pijplijn maken met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. 

Wanneer u Hallo Wizard kopiëren JSON-definities voor Hallo Data Factory gekoppelde services, worden gegevenssets en pijplijn entiteiten automatisch voor u gemaakt. Wanneer u hulpprogramma's of API's (met uitzondering van Hallo .NET API) gebruikt, kunt u Data Factory-entiteiten Hallo definiëren met behulp van Hallo JSON-indeling. Hallo [JSON-voorbeeld: gegevens kopiëren van DB2 tooAzure blobopslag](#json-example-copy-data-from-db2-to-azure-blob) toont Hallo JSON definities voor Hallo Data Factory-entiteiten die gebruikt toocopy gegevens uit een on-premises DB2-gegevensopslag zijn.

Hallo volgende secties bevatten informatie over Hallo JSON-eigenschappen die zijn gebruikt toodefine Hallo Data Factory-entiteiten die specifieke tooa DB2-gegevensarchief zijn.

## <a name="db2-linked-service-properties"></a>DB2 gekoppelde service-eigenschappen
Hallo volgende tabel geeft een lijst Hallo JSON-eigenschappen die specifiek tooa DB2 gekoppelde service zijn.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| **type** |Deze eigenschap te moet worden ingesteld**OnPremisesDB2**. |Ja |
| **Server** |Hallo-naam van Hallo DB2-server. |Ja |
| **database** |Hallo-naam van Hallo DB2-database. |Ja |
| **schema** |Hallo-naam van het Hallo-schema in Hallo DB2-database. Deze eigenschap is hoofdlettergevoelig. |Nee |
| **authenticationType** |Hallo type verificatie dat is gebruikt tooconnect toohello DB2-database. Hallo mogelijke waarden zijn: anoniem, basis en Windows. |Ja |
| **gebruikersnaam** |Hallo-naam voor de gebruikersaccount Hallo als u basisverificatie of Windows-verificatie gebruikt. |Nee |
| **wachtwoord** |Hallo-wachtwoord voor gebruikersaccount Hallo. |Nee |
| **gatewayName** |Hallo-naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale DB2-database gebruiken. |Ja |

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een lijst met eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets en Hallo secties, Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties, zoals **structuur**, **beschikbaarheid**, en Hallo **beleid** voor een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure Blob storage, Azure Table opslag, enzovoort).

Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo **typeProperties** sectie voor een gegevensset van het type **RelationalTable**, waarop Hallo DB2 gegevensset bevat, heeft de volgende eigenschap Hallo:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| **tableName** |Hallo-naam van de tabel Hallo in Hallo DB2-database-instantie die Hallo gekoppelde service verwijst. Deze eigenschap is hoofdlettergevoelig. |Nee (als hello **query** eigenschap van de kopieeractiviteit van een van het type **RelationalSource** is opgegeven) |

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een lijst met eigenschappen die beschikbaar zijn voor het definiëren van de activiteiten kopiëren en Hallo secties, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen van de activiteit, zoals kopiëren **naam**, **beschrijving**, **invoer** tabel **levert** tabel en **beleid**, zijn beschikbaar voor alle typen activiteiten. eigenschappen die beschikbaar in Hallo zijn Hallo **typeProperties** sectie van de activiteit Hallo voor elk activiteitstype. Voor de Kopieeractiviteit, wordt Hallo eigenschappen variëren afhankelijk van Hallo soorten gegevensbronnen en Put.

Voor de Kopieeractiviteit wanneer Hallo bron van het type **RelationalSource** (waaronder DB2), Hallo volgende eigenschappen beschikbaar zijn in Hallo **typeProperties** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| **query** |Hallo aangepaste query tooread Hallo gegevens gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: `"query": "select * from "MySchema"."MyTable""` |Nee (als hello **tableName** eigenschap van een dataset is opgegeven) |

> [!NOTE]
> Schema- en tabelnamen zijn hoofdlettergevoelig. In de query-instructie hello, moet u de namen van eigenschappen met behulp van "" (dubbele aanhalingstekens). Bijvoorbeeld:
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a>JSON-voorbeeld: gegevens kopiëren van DB2 tooAzure Blob-opslag
In dit voorbeeld bevat definities van de JSON voorbeeld kunt u een pijplijn toocreate door Hallo gebruiken [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Hallo-voorbeeld ziet u hoe toocopy gegevens uit een DB2-database tooBlob opslag. Echter gegevens te kunnen worden gekopieerd[alle ondersteunde gegevens opslaan sink-type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Azure Data Factory-Kopieeractiviteit.

Hallo voorbeeld heeft Hallo Data Factory-entiteiten te volgen:

- Een DB2 gekoppelde service van het type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)
- Een Azure Blob-opslag gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
- Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)
- Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
- Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van Hallo [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) eigenschappen

Hallo voorbeeld gegevens worden gekopieerd van de resultaten van een query in een DB2-database tooan Azure blob per uur. Hallo JSON-eigenschappen die worden gebruikt in de steekproef Hallo worden Hallo die in secties Hallo entiteit definities beschreven.

Als eerste stap, installeren en configureren van een data gateway. Instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.

**DB2 gekoppelde service**

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
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

**Azure Blob-opslag gekoppelde service**

```json
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

**Invoergegevensset DB2**

Hallo-voorbeeld wordt ervan uitgegaan dat u een tabel in DB2 MijnTabel "" met een kolom met het label 'tijdstempel' hello tijd reeks gegevens hebt gemaakt.

Hallo **externe** eigenschap is ingesteld te 'true'. Deze instelling informeert Hallo Data Factory-service dat deze gegevensset externe toohello gegevensfactory en niet door een activiteit in de gegevensfactory hello wordt geproduceerd. U ziet dat Hallo **type** eigenschap is ingesteld, te**RelationalTable**.


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
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

**Azure Blob-uitvoergegevensset**

Gegevens worden geschreven tooa nieuwe blob elk uur door Hallo instelling **frequentie** eigenschap te "Uur" en Hallo **interval** eigenschap too1. Hallo **folderPath** eigenschap voor Hallo blob dynamisch wordt geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. mappad Hallo Hallo jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Pijplijn voor de kopieeractiviteit Hallo**

Hallo pijplijn bevat een kopieeractiviteit die is geconfigureerd toouse opgegeven invoer- en uitvoergegevenssets en geplande toorun elk uur is. Hallo in JSON-definitie voor de pijplijn Hallo Hallo, **bron** type is ingesteld, te**RelationalSource** en Hallo **sink** type is ingesteld, te**BlobSink**. Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens uit de tabel 'Orders' hello selecteert.

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a>Toewijzing van het type voor DB2
Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel Kopieeractiviteit automatische typeconversies van brontype type toosink uitvoert met behulp van Hallo benadering in twee stappen te volgen:

1. Converteren van een systeemeigen bron type tooa .NET-type
2. Converteren van een .NET type tooa systeemeigen sink-type

Hallo worden volgende toewijzingen gebruikt wanneer de Kopieeractiviteit converteert Hallo gegevens uit een DB2 type tooa .NET-type:

| Type DB2-database | .NET framework-type |
| --- | --- |
| SmallInt |Int16 |
| Geheel getal |Int32 |
| BigInt |Int64 |
| Real |Één |
| dubbele |dubbele |
| Float |dubbele |
| Decimale |Decimale |
| DecimalFloat |Decimale |
| numerieke |Decimale |
| Date |Datum/tijd |
| Time |TimeSpan |
| tijdstempel |Datum/tijd |
| XML |Byte] |
| CHAR |Tekenreeks |
| VarChar |Tekenreeks |
| LongVarChar |Tekenreeks |
| DB2DynArray |Tekenreeks |
| Binaire |Byte] |
| VarBinary |Byte] |
| LongVarBinary |Byte] |
| Afbeelding |Tekenreeks |
| VarGraphic |Tekenreeks |
| LongVarGraphic |Tekenreeks |
| CLOB |Tekenreeks |
| Blob |Byte] |
| DbClob |Tekenreeks |
| SmallInt |Int16 |
| Geheel getal |Int32 |
| BigInt |Int64 |
| Real |Één |
| dubbele |dubbele |
| Float |dubbele |
| Decimale |Decimale |
| DecimalFloat |Decimale |
| numerieke |Decimale |
| Date |Datum/tijd |
| Time |TimeSpan |
| tijdstempel |Datum/tijd |
| XML |Byte] |
| CHAR |Tekenreeks |

## <a name="map-source-toosink-columns"></a>Bronkolommen toosink toewijzen
hoe toomap kolommen in Hallo bron gegevensset toocolumns in Hallo sink gegevensset, Zie toolearn [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-reads-from-relational-sources"></a>Herhaalbare leesbewerkingen van relationele bronnen
Wanneer u gegevens uit een relationele gegevensopslag kopiëren, moet u herhaalbaarheid rekening tooavoid ongewenste resultaten. In Azure Data Factory, kunt u een segment handmatig opnieuw. U kunt ook Hallo opnieuw configureren **beleid** eigenschap voor een gegevensset toorerun een segment wanneer er een fout optreedt. Zorg ervoor dat Hallo dezelfde gegevens gelezen ongeacht hoe vaak Hallo segment is opnieuw uitvoeren en ongeacht hoe u Hallo segment opnieuw uitvoeren. Zie voor meer informatie [Repeatable leest uit relationele bronnen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Prestaties en afstemmen
Meer informatie over de belangrijkste factoren die invloed hebben op prestaties van de Kopieeractiviteit en manieren toooptimize prestaties in Hallo Hallo [handleiding afstemmen en uitvoering van de activiteit](data-factory-copy-activity-performance.md).
