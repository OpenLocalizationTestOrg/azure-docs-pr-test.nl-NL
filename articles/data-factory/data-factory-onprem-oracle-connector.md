---
title: aaaCopy gegevens van/naar Oracle gebruik Data Factory | Microsoft Docs
description: Meer informatie over hoe toocopy gegevens van Oracle-database die on-premises met Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a>Gegevens kopiëren van lokale Oracle met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een lokale Oracle-database. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
U kunt gegevens kopiëren **uit een Oracle-database** toohello gegevensarchieven te volgen:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooan Oracle-database**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a>Vereisten
Data Factory ondersteunt verbindende tooon-premises Oracle-gegevensbronnen waarvoor gebruik wordt Hallo Data Management Gateway. Zie [Data Management Gateway](data-factory-data-management-gateway.md) toolearn artikel over Data Management Gateway en [verplaatsen van gegevens uit de lokale toocloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies over het instellen van Hallo gateway een pijplijn gegevens toomove gegevens.

Gateway is vereist, zelfs als hello Oracle wordt gehost door een virtuele machine van Azure IaaS. U kunt Hallo gateway installeren op Hallo dezelfde IaaS VM als Hallo gegevens opslaan of op een andere virtuele machine zo lang Hallo gateway kunt verbinding maken met toohello-database.

> [!NOTE]
> Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.

## <a name="supported-versions-and-installation"></a>Ondersteunde versies en installatie
Twee versies van stuurprogramma's bieden ondersteuning voor deze connector Oracle:

- **Microsoft-stuurprogramma voor Oracle (aanbevolen)**: vanaf Data Management Gateway versie 2.7, een Microsoft-stuurprogramma voor Oracle wordt automatisch geïnstalleerd samen met de gateway hello, dus u hoeft niet tooadditionally ingang Hallo stuurprogramma tooestablish connectiviteit tooOracle, en u kunt ook de prestaties beter kopie dit stuurprogramma gebruikt. Hieronder versies van Oracle worden databases ondersteund:
    - Oracle 12c R1 (12.1)
    - Oracle 11g R1, R2 (11.1, 11.2)
    - Oracle 10g R1, R2 (10.1, 10.2)
    - Oracle 9i R1, R2 (9.0.1, 9.2)
    - Oracle 8i R3 (8.1.7)

> [!IMPORTANT]
> Microsoft-stuurprogramma voor Oracle ondersteunt momenteel alleen kopiëren van gegevens uit Oracle, maar niet schrijven tooOracle. En dit stuurprogramma biedt geen ondersteuning voor opmerking Hallo test verbinding mogelijkheid in het tabblad Data Management Gateway diagnostische gegevens. U kunt ook Hallo kopie wizard toovalidate Hallo connectiviteit gebruiken.
>

- **Oracle-gegevensprovider voor .NET:** u kunt ook toouse Oracle-gegevensprovider toocopy gegevens uit / tooOracle. Dit onderdeel is opgenomen in [Oracle Data Access-onderdelen voor Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/). Hallo juiste versie (32/64 bits) installeren op Hallo-machine waarop Hallo gateway is geïnstalleerd. [Oracle-gegevensprovider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) toegang tot tooOracle Database 10 g versie 2 of hoger.

    Als u 'XCopy installatie' kiest, stappen in Hallo Leesmij.htm. U wordt aangeraden u Hallo installatieprogramma met een gebruikersinterface (niet-XCopy een).

    Na de installatie van de provider hello, **opnieuw** Hallo Data Management Gateway hostservice op uw machine met behulp van de Services-applet (of) Data Management Gateway Configuration Manager.  

Als u de wizard tooauthor Hallo kopiëren kopieerpijplijn gebruikt, worden Hallo stuurprogrammatype automatisch bepaald. Microsoft-stuurprogramma wordt standaard gebruikt tenzij uw versie van de gegevensgateway lager dan 2.7 is of kies van Oracle als sink.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een lokale Oracle-database verplaatst met behulp van verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:

1. Maak een **gegevensfactory**. Een gegevensfactory kan één of meer pijplijnen bevatten. 
2. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory. Bijvoorbeeld, als u gegevens uit een Oralce database tooan Azure blob-opslag kopiëren wilt, u twee gekoppelde services toolink uw Oracle-database en de Azure storage-account tooyour data factory. Zie voor de gekoppelde service-eigenschappen die specifiek tooOracle, [gekoppelde service-eigenschappen](#linked-service-properties) sectie.
3. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. In vermeld in de laatste stap Hallo Hallo voorbeeld maakt u een gegevensset toospecify Hallo tabel in de Oracle-database waarin de invoergegevens Hallo. Maken van een andere dataset toospecify Hallo blob-container en Hallo map Hallo gegevens gekopieerd van Hallo Oracle-database. Zie voor eigenschappen van gegevensset die specifieke tooOracle, [eigenschappen van gegevensset](#dataset-properties) sectie.
4. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. In Hallo voorbeeld eerder vermeld, gebruikt u OracleSource als een bron- en BlobSink als een sink voor de kopieeractiviteit Hallo. Op dezelfde manier als u uit Azure Blob Storage tooOracle Database kopiëren wilt, gebruikt u BlobSource en OracleSink in Hallo kopieeractiviteit. Zie voor activiteitseigenschappen kopiëren die specifieke tooOracle database, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie. Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag. 

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een lokale Oracle-database zijn, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-oracle-database) sectie van dit artikel.

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten zijn:

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooOracle gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **OnPremisesOracle** |Ja |
| driverType | Geef op welke stuurprogramma toouse toocopy gegevens uit / tooOracle Database. Toegestane waarden zijn **Microsoft** of **ODP** (standaard). Zie [ondersteunde versie en installatieopties](#supported-versions-and-installation) gedeelte stuurprogrammagegevens. | Nee |
| connectionString | Geef informatie tooconnect toohello Oracle-Database-exemplaar voor de eigenschap connectionString Hallo nodig. | Ja |
| gatewayName | Naam van Hallo gateway die die gebruikte tooconnect toohello lokale Oracle-server |Ja |

**Voorbeeld: met behulp van het stuurprogramma Microsoft:**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Voorbeeld: met behulp van ODP stuurprogramma**

Raadpleeg te[deze site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) voor Hallo indelingen toegestaan.

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Oracle, Azure blob-, Azure-tabel, enz.).

Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo typeProperties sectie voor Hallo gegevensset van het type OracleTable heeft Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van de tabel Hallo in Hallo Oracle-Database die Hallo gekoppelde service verwijst. |Nee (als **oracleReaderQuery** van **OracleSource** is opgegeven) |

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.

> [!NOTE]
> Hallo Kopieeractiviteit slechts één invoer en slechts één uitvoer produceert.

Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

### <a name="oraclesource"></a>OracleSource
In de kopieerbewerking wanneer Hallo bron van het type **OracleSource** Hallo volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| oracleReaderQuery |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: Selecteer * from MijnTabel <br/><br/>Als niet wordt opgegeven, Hallo SQL-instructie die is uitgevoerd: Selecteer * from MijnTabel |Nee (als **tableName** van **gegevensset** is opgegeven) |

### <a name="oraclesink"></a>OracleSink
**OracleSink** ondersteunt Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| writeBatchTimeout |Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt. |TimeSpan<br/><br/> Voorbeeld: 00:30:00 (30 minuten). |Nee |
| writeBatchSize |Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt. |Geheel getal (aantal rijen) |Nee (standaard: 100) |
| sqlWriterCleanupScript |Geef een query voor de Kopieeractiviteit tooexecute zodat de gegevens van een bepaald segment wordt opgeschoond. |Een query-instructie. |Nee |
| sliceIdentifierColumnName |Geef kolomnaam voor Kopieeractiviteit toofill met segment-ID automatisch gegenereerd en die is gebruikt tooclean van gegevens van een bepaald segment wanneer opnieuw uitgevoerd. |De naam van de kolom van een kolom met gegevenstype binary(32). |Nee |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a>JSON-voorbeelden voor het kopiëren van gegevens tooand van Oracle-database
Hallo volgende voorbeeld wordt een voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ze geven weer hoe toocopy gegevens van / naar/van Azure Blob Storage tooan Oracle-database. Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a>Voorbeeld: Gegevens kopiëren van Oracle tooAzure Blob

Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:

1. Een gekoppelde service van het type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) als bron en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) als sink.

Hallo voorbeeld kopieert gegevens uit een tabel in een lokale Oracle-database tooa blob per uur. Zie voor meer informatie over diverse eigenschappen die worden gebruikt in de steekproef Hallo documentatie in de secties na Hallo voorbeelden.

**Oracle gekoppelde service:**

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Azure Blob-opslag gekoppelde service:**

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Oracle-invoergegevensset:**

Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Oracle en bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.

Instelling 'extern': 'true' informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
        },
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
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": "\t",
                "rowDelimiter": "\n"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Pijplijn met de kopieeractiviteit:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun per uur is. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**OracleSource** en **sink** type is ingesteld, te**BlobSink**.  Hallo SQL-query is opgegeven met **oracleReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a>Voorbeeld: Gegevens kopiëren van Azure Blob-tooOracle
Dit voorbeeld toont hoe toocopy gegevens uit een Azure Blob Storage tooan lokale Oracle-database. Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** vanaf elke Hallo bronnen vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.  

Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:

1. Een gekoppelde service van het type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) als bron [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) als sink.

Hallo-voorbeeld worden gegevens gekopieerd van een blob tooa-tabel in een lokale Oracle-database om het uur. Zie voor meer informatie over diverse eigenschappen die worden gebruikt in de steekproef Hallo documentatie in de secties na Hallo voorbeelden.

**Oracle gekoppelde service:**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Azure Blob-opslag gekoppelde service:**
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Azure Blob-invoergegevensset**

Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1). Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand en dag deel uit van de begintijd Hallo en bestandsnaam gebruikt Hallo uur deel uit van de begintijd Hallo. "extern": "true" instelling informeert Hallo Data Factory-service dat deze tabel externe toohello gegevensfactory en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
                }
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
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

**Oracle-uitvoergegevensset:**

Hallo-voorbeeld wordt ervan uitgegaan dat u een tabel "MijnTabel" in Oracle hebt gemaakt. Hallo-tabel maken in Oracle met hetzelfde aantal kolommen Hallo zoals Hallo Blob CSV-bestand toocontain verwacht. Nieuwe rijen worden toohello tabel toegevoegd om het uur.

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

**Pijplijn met de kopieeractiviteit:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en Hallo **sink** type is ingesteld, te**OracleSink**.  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a>Tips voor probleemoplossing
### <a name="problem-1-net-framework-data-provider"></a>Probleem 1: .NET Framework-gegevensprovider

U ziet de volgende Hallo **foutbericht**:

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

**Mogelijke oorzaken:**

1. Hallo .NET Framework Data Provider voor Oracle is niet geïnstalleerd.
2. Hallo .NET Framework Data Provider voor Oracle geïnstalleerde too.NET Framework 2.0 en is niet gevonden in mappen Hallo .NET Framework 4.0.

**Resolutie/tijdelijke oplossing:**

1. Als u dit nog niet hebt geïnstalleerd Hallo .NET-Provider voor Oracle, [installeren](http://www.oracle.com/technetwork/topics/dotnet/downloads/) en probeer het opnieuw Hallo scenario.
2. Als u Hallo foutbericht krijgt zelfs na het installeren van de provider hello, Hallo volgende stappen:
   1. Machine config van .NET 2.0 openen vanuit de map Hallo: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.
   2. Zoeken naar **Oracle-gegevensprovider voor .NET**, en u moet kunnen toofind een vermelding zoals weergegeven in het voorbeeld onder na Hallo **systeem.gegevens** -> **DbProviderFactories**: '<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle-gegevensprovider voor .NET" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" />”
3. Deze vermelding toohello machine.config-bestand in Hallo na v4.0 map kopiëren: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config en wijziging Hallo versie too4.xxx.x.x.
4. '< Pad ODP.NET geïnstalleerde > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll' in hello globale assembly-cache (GAC) installeren door te voeren `gacutil /i [provider path]`. ## tips voor probleemoplossing

### <a name="problem-2-datetime-formatting"></a>Probleem 2: opmaak voor datum/tijd

U ziet de volgende Hallo **foutbericht**:

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

**Resolutie/tijdelijke oplossing:**

Mogelijk moet u tooadjust Hallo queryreeks in de kopieerbewerking op basis van hoe datums zijn geconfigureerd in de Oracle-database, zoals weergegeven in de volgende hello (met Hallo to_date functie) voorbeeld:

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a>Toewijzing van het type voor Oracle
Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:

1. Systeemeigen bron typen too.NET type converteren
2. Converteren van .NET-type toonative sink-type

Bij het verplaatsen van gegevens uit Oracle, worden volgende toewijzingen Hallo gebruikt van het type Oracle-too.NET gegevenstype en vice versa.

| Oracle-gegevenstype | .NET framework-gegevenstype |
| --- | --- |
| BBESTAND |Byte] |
| BLOB |Byte] |
| CHAR |Tekenreeks |
| CLOB |Tekenreeks |
| DATUM |Datum/tijd |
| FLOAT |Decimaal, tekenreeks (als precision > 28) |
| GEHEEL GETAL |Decimaal, tekenreeks (als precision > 28) |
| INTERVAL jaar tooMONTH |Int32 |
| INTERVAL dag tooSECOND |TimeSpan |
| LANG |Tekenreeks |
| LANGE ONBEWERKTE |Byte] |
| NCHAR |Tekenreeks |
| NCLOB |Tekenreeks |
| AANTAL |Decimaal, tekenreeks (als precision > 28) |
| NVARCHAR2 |Tekenreeks |
| ONBEWERKTE |Byte] |
| ROWID |Tekenreeks |
| TIJDSTEMPEL |Datum/tijd |
| TIJDSTEMPEL MET DE LOKALE TIJDZONE |Datum/tijd |
| TIJDSTEMPEL MET TIJDZONE |Datum/tijd |
| NIET-ONDERTEKEND GEHEEL GETAL |Aantal |
| VARCHAR2 |Tekenreeks |
| XML |Tekenreeks |

> [!NOTE]
> Gegevenstype **INTERVAL jaar tooMONTH** en **INTERVAL dag tooSECOND** worden niet ondersteund bij gebruik van Microsoft-stuurprogramma.

## <a name="map-source-toosink-columns"></a>Bronkolommen toosink toewijzen
Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Herhaalbare leesbewerking van relationele bronnen
Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten. In Azure Data Factory, kunt u een segment handmatig opnieuw. U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt. Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd. Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
