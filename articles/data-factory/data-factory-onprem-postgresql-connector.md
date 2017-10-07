---
title: aaaMove gegevens van PostgreSQL met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens uit een PostgreSQL-Database met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a>Verplaatsen van gegevens uit een PostgreSQL met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een on-premises PostgreSQL-database. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.

U kunt gegevens uit een on-premises PostgreSQL gegevens store tooany ondersteund sink gegevensopslag kopiëren. Zie voor een lijst van gegevensarchieven als PUT wordt ondersteund door Hallo kopieeractiviteit [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Data factory momenteel ondersteunt het verplaatsen van gegevens uit een PostgreSQL-database tooother gegevensarchieven, maar niet voor tooan PostgreSQL-database verplaatsen van gegevens van andere gegevens worden opgeslagen. 

## <a name="prerequisites"></a>Vereisten

Data Factory-service ondersteunt verbindende tooon lokale PostgreSQL gegevensbronnen waarvoor gebruik Hallo Data Management Gateway. Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway.

Gateway is vereist, zelfs als Hallo PostgreSQL-database wordt gehost in een Azure IaaS VM. U kunt de gateway installeren op Hallo dezelfde IaaS VM als Hallo gegevens opslaan of op een andere virtuele machine zo lang Hallo gateway kunt verbinding maken met toohello-database.

> [!NOTE]
> Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.

## <a name="supported-versions-and-installation"></a>Ondersteunde versies en installatie
Voor Data Management Gateway tooconnect toohello PostgreSQL-Database, installeert u Hallo [Ngpsql-gegevensprovider voor PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 of boven op Hallo hetzelfde systeem als Data Management Gateway Hallo. PostgreSQL versie 7.4 en hoger wordt ondersteund.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises PostgreSQL-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's. 

- Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren. 
- U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: 
    - Azure Portal
    - Visual Studio
    - Azure PowerShell
    - Azure Resource Manager-sjabloon
    - .NET API
    - REST API

     Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. 
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. 

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een on-premises PostgreSQL-gegevensopslag zijn [JSON-voorbeeld: gegevens kopiëren van PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) sectie van dit artikel. 

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooa PostgreSQL-gegevensarchief zijn:

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooPostgreSQL gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **OnPremisesPostgreSql** |Ja |
| server |Naam van Hallo PostgreSQL-server. |Ja |
| database |Naam van Hallo PostgreSQL-database. |Ja |
| Schema |Naam van Hallo schema in Hallo-database. Hallo-schemanaam is hoofdlettergevoelig. |Nee |
| authenticationType |Type verificatie gebruikt tooconnect toohello PostgreSQL-database. Mogelijke waarden zijn: anoniem, basis en Windows. |Ja |
| gebruikersnaam |Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt. |Nee |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven. |Nee |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale PostgreSQL-database gebruiken. |Ja |

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen van de gegevensset.

Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo typeProperties sectie voor de gegevensset van het type **RelationalTable** (inclusief PostgreSQL gegevensset) heeft Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van de tabel Hallo in Hallo PostgreSQL-Database-instantie waarnaar de gekoppelde service verwijst. Hallo tableName is hoofdlettergevoelig. |Nee (als **query** van **RelationalSource** is opgegeven) |

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.

Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

Wanneer de bron is van het type **RelationalSource** (waaronder PostgreSQL), Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: "query": "Selecteer * uit \"MySchema\".\" MyTable\"'. |Nee (als **tableName** van **gegevensset** is opgegeven) |

> [!NOTE]
> Schema- en tabelnamen zijn hoofdlettergevoelig. Omsluiten in `""` (dubbele aanhalingstekens) in Hallo-query.  

**Voorbeeld:**

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a>JSON-voorbeeld: gegevens kopiëren van PostgreSQL tooAzure Blob
In dit voorbeeld voorbeeld JSON definities bevat dat u een pijplijn toocreate gebruiken met behulp van kunt [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ze geven weer hoe toocopy gegevens uit een PostgreSQL-database tooAzure Blob Storage. Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.   

> [!IMPORTANT]
> Dit voorbeeld bevat JSON-fragmenten. Dit omvat geen stapsgewijze instructies voor het maken van de gegevensfactory Hallo. Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies.

Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:

1. Een gekoppelde service van het type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Hallo [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo voorbeeld kopieert gegevens van de resultaten van een query in een PostgreSQL-database tooa blob elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

Instellen als eerste stap Hallo data management gateway. Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.

**PostgreSQL gekoppelde service:**

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
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

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
**PostgreSQL invoergegevensset:**

Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in PostgreSQL en bevat een kolom met de naam 'tijdstempel' voor de reeksgegevens.

Instelling `"external": true` informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
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

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun per uur is. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource** en **sink** type is ingesteld, te**BlobSink**. Hallo SQL-query is opgegeven voor Hallo **query** eigenschap selecteert Hallo gegevens uit Hallo public.usstates tabel in Hallo PostgreSQL-database.

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a>Toewijzing van het type voor PostgreSQL
Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:

1. Systeemeigen bron typen too.NET type converteren
2. Converteren van .NET-type toonative sink-type

Bij het verplaatsen van gegevens tooPostgreSQL worden hello volgende toewijzingen gebruikt vanuit PostgreSQL type too.NET type.

| Type PostgreSQL-Database | PostgresSQL aliassen | .NET framework-type |
| --- | --- | --- |
| abstime | |Datum/tijd | &nbsp;
| bigint |int8 |Int64 |
| bigserial |serial8 |Int64 |
| bits [(n)] | |Byte [], String | &nbsp;
| bit uiteenlopende [(n)] |varbit |Byte [], String |
| Booleaanse waarde |BOOL |Booleaanse waarde |
| Vak | |Byte [], String |&nbsp;
| bytea | |Byte [], String |&nbsp;
| teken [(n)] |char [(n)] |Tekenreeks |
| teken wisselende [(n)] |varchar [(n)] |Tekenreeks |
| CID | |Tekenreeks |&nbsp;
| CIDR | |Tekenreeks |&nbsp;
| cirkel | |Byte [], String |&nbsp;
| Datum | |Datum/tijd |&nbsp;
| DateRange | |Tekenreeks |&nbsp;
| dubbele precisie |FLOAT8 |dubbele |
| INet | |Byte [], String |&nbsp;
| intarry | |Tekenreeks |&nbsp;
| int4range | |Tekenreeks |&nbsp;
| int8range | |Tekenreeks |&nbsp;
| geheel getal |int, int4 |Int32 |
| interval [velden] [(p)] | |Periode |&nbsp;
| JSON | |Tekenreeks |&nbsp;
| jsonb | |Byte] |&nbsp;
| regel | |Byte [], String |&nbsp;
| lseg | |Byte [], String |&nbsp;
| macaddr | |Byte [], String |&nbsp;
| Money | |Decimale |&nbsp;
| numerieke [(p, s)] |Decimal [(p, s)] |Decimale |
| numrange | |Tekenreeks |&nbsp;
| OID | |Int32 |&nbsp;
| Pad | |Byte [], String |&nbsp;
| pg_lsn | |Int64 |&nbsp;
| beheerpunt | |Byte [], String |&nbsp;
| veelhoek | |Byte [], String |&nbsp;
| echte |FLOAT4 |Één |
| smallint |int2 |Int16 |
| smallserial |serial2 |Int16 |
| Seriële |serial4 |Int32 |
| Tekst | |Tekenreeks |&nbsp;

## <a name="map-source-toosink-columns"></a>Bronkolommen toosink toewijzen
Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Herhaalbare leesbewerking van relationele bronnen
Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten. In Azure Data Factory, kunt u een segment handmatig opnieuw. U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt. Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd. Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
