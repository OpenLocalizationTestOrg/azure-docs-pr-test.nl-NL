---
title: aaaMove gegevens uit de SAP HANA met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens uit de SAP HANA met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a>Verplaatsen van gegevens uit SAP HANA, met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit in Azure Data Factory toomove gegevens uit een lokale SAP HANA Hallo. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.

U kunt gegevens uit een on-premises SAP HANA store tooany ondersteund sink gegevens gegevensopslag kopiëren. Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel. Data factory ondersteunt momenteel alleen verplaatsen van gegevens uit een SAP HANA tooother gegevens worden opgeslagen, maar niet voor SAP HANA tooan verplaatsen van gegevens van andere gegevens worden opgeslagen.

## <a name="supported-versions-and-installation"></a>Ondersteunde versies en installatie
Deze connector ondersteunt een willekeurige versie van de SAP HANA-database. Het ondersteunt kopiëren van gegevens van HANA informatiemodellen (zoals weergaven, analyse en berekening) en rij/kolom tabellen met behulp van SQL-query's.

tooenable hello connectiviteit toohello SAP HANA-exemplaar installeren Hallo volgende onderdelen:
- **Data Management Gateway**: Data Factory-service ondersteunt verbindingen van tooon-premises gegevens winkels (inclusief SAP HANA) met een onderdeel genaamd Data Management Gateway. toolearn over Data Management Gateway en stapsgewijze instructies voor het instellen van Hallo-gateway, Zie [verplaatsen tussen on-premises gegevens gegevensarchief gegevensarchief toocloud](data-factory-move-data-between-onprem-and-cloud.md) artikel. Gateway is vereist, zelfs als Hallo SAP HANA wordt gehost in een Azure IaaS virtuele machine (VM). U kunt Hallo gateway installeren op Hallo dezelfde virtuele machine als Hallo gegevens opslaan of op een andere virtuele machine zo lang Hallo gateway kunt verbinding maken met toohello-database.
- **SAP HANA ODBC-stuurprogramma** op Hallo gateway-apparaat. U kunt Hallo SAP HANA ODBC-stuurprogramma downloaden van Hallo [SAP Software Download Center](https://support.sap.com/swdc). Zoeken met trefwoorden Hallo **SAP HANA-CLIENT voor Windows**. 

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's. 

- Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren. 
- U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. 
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. 

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een lokale SAP HANA zijn [JSON-voorbeeld: gegevens kopiëren van SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) sectie van dit artikel. 

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooan SAP HANA-gegevensarchief zijn:

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel bevat de beschrijving voor JSON-elementen specifieke tooSAP HANA gekoppelde service.

Eigenschap | Beschrijving | Toegestane waarden | Vereist
-------- | ----------- | -------------- | --------
server | Naam van het Hallo-server op welke Hallo SAP HANA exemplaar zich bevindt. Als de server een aangepaste poort gebruikt is, geeft u `server:port`. | Tekenreeks | Ja
authenticationType | Het type verificatie. | De tekenreeks. 'Basic' of 'Windows' | Ja 
gebruikersnaam | Naam van het Hallo-gebruiker met toegang toohello SAP-server | Tekenreeks | Ja
wachtwoord | Wachtwoord voor gebruiker Hallo. | Tekenreeks | Ja
gatewayName | Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale SAP HANA-exemplaar gebruiken. | Tekenreeks | Ja
encryptedCredential | Hallo versleutelde referentie-tekenreeks. | Tekenreeks | Nee

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).

Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Er zijn geen type-specifieke eigenschappen ondersteund voor SAP HANA-gegevensset Hallo van het type **RelationalTable**. 


## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen zoals naam, beschrijving, invoer en uitvoer tabellen, zijn de beleidsregels zijn beschikbaar voor alle typen activiteiten.

Dat eigenschappen beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit Hallo variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

Wanneer u de gegevensbron in de kopieerbewerking is van het type **RelationalSource** (waaronder SAP HANA), Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query | Hiermee geeft u Hallo SQL query tooread gegevens van Hallo SAP HANA-exemplaar. | SQL-query. | Ja |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a>JSON-voorbeeld: gegevens uit een SAP HANA tooAzure Blob kopiëren
Hallo volgende voorbeeld vindt u voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). In dit voorbeeld laat zien hoe toocopy gegevens uit een lokale SAP HANA tooan Azure Blob Storage. Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.  

> [!IMPORTANT]
> Dit voorbeeld bevat JSON-fragmenten. Dit omvat geen stapsgewijze instructies voor het maken van de gegevensfactory Hallo. Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies.

Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:

1. Een gekoppelde service van het type [SapHana](#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo voorbeeld gegevens worden gekopieerd van een SAP HANA-exemplaar tooan Azure blob per uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

Instellen als eerste stap Hallo data management gateway. Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.

### <a name="sap-hana-linked-service"></a>SAP HANA gekoppelde service
Deze gekoppelde service wordt uw exemplaar voor SAP HANA toohello gegevensfactory. Hallo type wordt ingesteld te**SapHana**. Hallo typeProperties sectie bevat verbindingsinformatie voor Hallo SAP HANA-exemplaar.

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service
Deze gekoppelde service uw Azure Storage-account toohello data factory. Hallo type wordt ingesteld te**AzureStorage**. Hallo typeProperties sectie bevat de verbindingsgegevens voor hello Azure Storage-account.

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

### <a name="sap-hana-input-dataset"></a>SAP HANA-invoergegevensset

Deze gegevensset definieert Hallo SAP HANA-gegevensset. U stelt Hallo Hallo Data Factory-gegevensset te**RelationalTable**. Op dit moment kunt opgeeft u geen type-specifieke eigenschappen voor een SAP HANA-gegevensset. Hallo-query in Hallo Kopieeractiviteit definitie geeft aan welke gegevens tooread van Hallo SAP HANA-exemplaar. 

Instellen van de eigenschap external tootrue informeert het Hallo Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.

Frequentie en het interval eigenschappen definieert Hallo planning. In dit geval Hallo gegevens gelezen uit Hallo SAP HANA exemplaar per uur. 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a>Azure Blob-uitvoergegevensset
Deze gegevensset definieert Hallo uitvoer Azure Blob-gegevensset. de eigenschap type Hallo is tooAzureBlob ingesteld. Hallo bevat typeProperties waar Hallo gegevens gekopieerd vanaf Hallo SAP HANA-exemplaar worden opgeslagen. Hallo-gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a>Pijplijn met de kopieeractiviteit

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource** (voor SAP HANA-bron) en **sink** type is ingesteld, te**BlobSink**. Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a>Toewijzing van het type voor SAP HANA
Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello benadering in twee stappen te volgen:

1. Systeemeigen bron typen too.NET type converteren
2. Converteren van .NET-type toonative sink-type

Bij het verplaatsen van gegevens uit een SAP HANA, worden uit SAP HANA typen too.NET typen Hallo volgende toewijzingen gebruikt.

SAP HANA-Type | .NET op basis van Type
------------- | ---------------
TINYINT | Byte
SMALLINT | Int16
INT | Int32
BIGINT | Int64
ECHTE | Één
DOUBLE | Één
DECIMALE | Decimale
BOOLEAANSE WAARDE | Byte
VARCHAR | Tekenreeks
NVARCHAR | Tekenreeks
CLOB | Byte]
ALPHANUM | Tekenreeks
BLOB | Byte]
DATUM | Datum/tijd
TIJD | TimeSpan
TIJDSTEMPEL | Datum/tijd
SECONDDATE | Datum/tijd

## <a name="known-limitations"></a>Bekende beperkingen
Er zijn enkele bekende beperkingen bij het kopiëren van gegevens uit een SAP HANA:

- NVARCHAR tekenreeksen zijn afgekapt toomaximum lengte van 4000 Unicode-tekens
- SMALLDECIMAL wordt niet ondersteund.
- VARBINARY wordt niet ondersteund.
- Geldige datums tussen 12-1899/30 zijn en 12-9999/31

## <a name="map-source-toosink-columns"></a>Bronkolommen toosink toewijzen
Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Herhaalbare leesbewerking van relationele bronnen
Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten. In Azure Data Factory, kunt u een segment handmatig opnieuw. U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt. Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd. Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
