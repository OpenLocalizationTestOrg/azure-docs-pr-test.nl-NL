---
title: aaaMove gegevens vanaf Amazon eenvoudige Storage-Service met behulp van de Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens vanaf Amazon eenvoudige Storage-Service (S3) met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a>Gegevens verplaatsen van Amazon eenvoudige Storage-Service met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse hello kopieeractiviteit in Azure Data Factory toomove gegevens vanaf Amazon eenvoudige Storage-Service (S3). Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.

U kunt gegevens kopiëren van Amazon S3 tooany ondersteund sink-gegevensarchief. Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel. Data Factory ondersteunt momenteel alleen zwevend gegevens vanaf Amazon S3 tooother gegevensarchieven, maar tooAmazon S3 niet verplaatsen van gegevens van andere gegevens worden opgeslagen.

## <a name="required-permissions"></a>Vereiste machtigingen
toocopy gegevens vanaf Amazon S3, zorg ervoor dat u de volgende machtigingen Hallo hebt gekregen:

* `s3:GetObject`en `s3:GetObjectVersion` voor Amazon S3 Object bewerkingen.
* `s3:ListBucket`voor Amazon S3-Bucket bewerkingen. Als u Data Factory-Wizard kopiëren, Hallo `s3:ListAllMyBuckets` is ook vereist.

Zie voor meer informatie over de volledige lijst van Amazon S3 machtigingen Hallo [machtigingen geven in een beleid](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens worden verplaatst van een bron Amazon S3 met behulp van verschillende hulpprogramma's of API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie voor een snel overzicht [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md).

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit, Hallo [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Of u hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u hulpprogramma's of API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling. Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van een gegevensarchief Amazon S3 zijn Hallo [JSON-voorbeeld: gegevens kopiëren van Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) sectie van dit artikel.

> [!NOTE]
> Zie voor meer informatie over ondersteunde indelingen voor de bestands- en compressie voor een kopieeractiviteit [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

Hallo volgende secties bevatten informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooAmazon S3 zijn.

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Een gekoppelde service een gegevensfactory store tooa gegevens gekoppeld. Maken van een gekoppelde service van het type **AwsAccessKey** toolink uw gegevensfactory tooyour Amazon S3 gegevensarchief. Hallo volgende tabel biedt een beschrijving op voor JSON-elementen specifieke tooAmazon S3 (AwsAccessKey) gekoppeld-service.

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| accessKeyID |ID van de geheime toegangssleutel Hallo. |Tekenreeks |Ja |
| secretAccessKey |Hallo geheime toegangssleutel zelf. |Versleutelde geheime tekenreeks |Ja |

Hier volgt een voorbeeld:

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
een gegevensset toorepresent toospecify invoergegevens in Azure Blob storage, stel de eigenschap Hallo type van de gegevensset Hallo te**AmazonS3**. Set Hallo **linkedServiceName** eigenschap van de naam van dataset toohello Hallo Hallo Amazon S3 gekoppelde service. Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets [gegevenssets maken](data-factory-create-datasets.md). 

Secties zoals structuur, beschikbaarheid en beleid zijn identiek voor alle typen van de gegevensset (zoals SQL-database, blob van Azure en Azure-tabel). Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo **typeProperties** sectie voor een gegevensset van het type **AmazonS3** (inclusief Hallo Amazon S3 gegevensset) heeft Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| bucketName |Hallo S3-Bucketnaam. |Tekenreeks |Ja |
| sleutel |Hallo S3 objectsleutel. |Tekenreeks |Nee |
| voorvoegsel |Voorvoegsel voor Hallo S3 objectsleutel. Objecten waarvan sleutels met dit voorvoegsel beginnen worden geselecteerd. Geldt alleen als sleutel is leeg. |Tekenreeks |Nee |
| Versie |Hallo-versie van Hallo S3-object als S3 versiebeheer is ingeschakeld. |Tekenreeks |Nee |
| Indeling | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set Hallo **type** eigenschap onder indeling tooone van deze waarden. Zie voor meer informatie, Hallo [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [JSON-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren-indeling ](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. <br><br> Als u bestanden als toocopy wilt-tussen bestandsgebaseerde winkels (binaire kopiëren) overslaan Hallo indeling sectie in beide definities invoer en uitvoer gegevensset. |Nee | |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Hallo ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**. Hallo ondersteund niveaus zijn: **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee | |


> [!NOTE]
> **bucketName + toets** Hallo-locatie van Hallo S3 object, waarbij bucket Hallo hoofdcontainer voor S3-objecten en sleutel Hallo volledig pad toohello S3-object.

### <a name="sample-dataset-with-prefix"></a>Voorbeeldgegevensset met voorvoegsel

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a>Voorbeeldgegevensset (met versie)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a>Dynamische paden voor S3
Hallo voorgaande voorbeeld gebruikt vaste waarden voor Hallo **sleutel** en **bucketName** eigenschappen in Hallo Amazon S3-gegevensset.

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

U kunt deze eigenschappen tijdens runtime dynamisch berekenen met behulp van systeemvariabelen zoals SliceStart Gegevensfactory hebben.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

U kunt doen hello dezelfde voor Hallo **voorvoegsel** eigenschap van een gegevensset Amazon S3. Zie voor een lijst van ondersteunde functies en variabelen [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md).

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten [pijplijnen maken](data-factory-create-pipelines.md). Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten. Eigenschappen die beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit Hallo variëren met elk activiteitstype. Voor de kopieeractiviteit hello afhankelijk eigenschappen van Hallo soorten gegevensbronnen en Put. Wanneer een bron in de kopieerbewerking Hallo is van het type **FileSystemSource** (waaronder Amazon S3), Hallo eigenschap na is beschikbaar in **typeProperties** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| Recursieve |Hiermee geeft u op of toorecursively lijst S3 onder Hallo directory-objecten. |waar/onwaar |Nee |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a>JSON-voorbeeld: gegevens kopiëren van Amazon S3 tooAzure Blob-opslag
In dit voorbeeld laat zien hoe toocopy gegevens vanaf Amazon S3 tooan Azure Blob-opslag. Echter gegevens kunnen worden gekopieerd rechtstreeks te[van Hallo put die worden ondersteund](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de kopieeractiviteit Hallo in Data Factory.

Hallo-voorbeeld bevat JSON-definities voor Hallo Data Factory-entiteiten te volgen. U kunt deze definities toocreate een pijplijn toocopy gegevens vanaf Amazon S3 tooBlob opslag, met behulp van Hallo [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).   

* Een gekoppelde service van het type [AwsAccessKey](#linked-service-properties).
* Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Invoer [gegevensset](data-factory-create-datasets.md) van het type [AmazonS3](#dataset-properties).
* Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [FileSystemSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo voorbeeld kopieert gegevens van Amazon S3 tooan Azure blob elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

### <a name="amazon-s3-linked-service"></a>Amazon S3 gekoppelde service

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service

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

### <a name="amazon-s3-input-dataset"></a>Invoergegevensset Amazon S3

Instelling **'extern': true** informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory. Deze eigenschap tootrue niet instellen op een invoergegevensset dat niet door een activiteit in de pijplijn hello wordt geproduceerd.

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a>Azure Blob-uitvoergegevensset

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. mappad Hallo Hallo jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a>De kopieeractiviteit in een pijplijn met een bron Amazon S3 en een blob-sink

Hallo pijplijn bevat een kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**FileSystemSource**, en **sink** type is ingesteld, te**BlobSink**.

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> Zie toomap kolommen uit een toocolumns bron gegevensset uit een gegevensset sink [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).


## <a name="next-steps"></a>Volgende stappen
Zie Hallo artikelen te volgen:

* toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (kopieeractiviteit) in Gegevensfactory en verschillende manieren toooptimize, Zie Hallo [activiteit prestaties en prestatieafstemming handleiding kopiëren](data-factory-copy-activity-performance.md).

* Zie voor stapsgewijze instructies voor het maken van een pijplijn met een kopieeractiviteit hello [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
