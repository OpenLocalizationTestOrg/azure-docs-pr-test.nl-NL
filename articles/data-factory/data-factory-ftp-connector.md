---
title: aaaMove gegevens van een FTP-server met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens van een FTP-server met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a>Gegevens verplaatsen van een FTP-server met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse hello kopieeractiviteit in Azure Data Factory toomove gegevens van een FTP-server. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.

U kunt gegevens kopiëren van een FTP-server tooany ondersteund sink-gegevensarchief. Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel. Data Factory ondersteunt momenteel alleen zwevend gegevens van een FTP-server tooother gegevens worden opgeslagen, maar niet verplaatsen van gegevens van andere gegevens worden opgeslagen tooan FTP-server. Deze ondersteuning biedt voor zowel on-premises en in de cloud van de FTP-servers.

> [!NOTE]
> Hallo kopieeractiviteit verwijdert Hallo-bronbestand niet nadat het is gekopieerde toohello bestemming. Als u toodelete Hallo-bronbestand na een geslaagde kopie moet, maakt u een aangepaste activiteit toodelete Hallo-bestand en Hallo activiteit in de pijplijn hello gebruiken. 

## <a name="enable-connectivity"></a>Connectiviteit inschakelen
Als u overstapt gegevens uit een **lokale** FTP-server tooa cloud-gegevensarchief (bijvoorbeeld tooAzure Blob-opslag), installeren en gebruiken van Data Management Gateway. Hallo Data Management Gateway is een clientagent die op uw on-premises machine is geïnstalleerd en kunt u cloud services tooconnect tooan lokale resource. Zie voor meer informatie [Data Management Gateway](data-factory-data-management-gateway.md). Zie voor stapsgewijze instructies voor het Hallo-gateway instellen en gebruiken deze [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md). U Hallo gateway tooconnect tooan FTP-server, zelfs als het Hallo-server zich op een Azure-infrastructuur als een dienst (IaaS) virtuele machine (VM).

Het is mogelijk tooinstall Hallo gateway op Hallo dezelfde lokale machine of IaaS VM zoals Hallo FTP-server. We raden echter aan dat u Hallo-gateway op een afzonderlijke computer of op IaaS VM tooavoid bronconflicten en voor betere prestaties installeert. Wanneer u Hallo-gateway op een afzonderlijke computer installeert, is het Hallo-machine moeten kunnen tooaccess Hallo FTP-server.

## <a name="get-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens van een FTP-bron verplaatst met behulp van verschillende hulpprogramma's of API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Data Factory-Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht.

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.

Of u Hallo-hulpprogramma's of API's gebruiken, voert u hello te volgen stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan:

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u hulpprogramma's of API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling. Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van een FTP-gegevensarchief zijn Hallo [JSON-voorbeeld: gegevens kopiëren van FTP-server tooAzure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) sectie van dit artikel.

> [!NOTE]
> Zie voor meer informatie over ondersteunde bestands- en compressie indelingen toouse [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooFTP zijn.

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel beschrijft de JSON-elementen specifieke tooan gekoppeld FTP-service.

| Eigenschap | Beschrijving | Vereist | Standaard |
| --- | --- | --- | --- |
| type |Deze tooFtpServer ingesteld. |Ja |&nbsp; |
| host |Hallo-naam of IP-adres van Hallo FTP-server opgeven. |Ja |&nbsp; |
| authenticationType |Hallo verificatietype opgeven. |Ja |Basic, anonieme |
| gebruikersnaam |Hallo-gebruiker met toegang toohello FTP-server opgeven. |Nee |&nbsp; |
| wachtwoord |Hallo-wachtwoord voor gebruiker hello (gebruikersnaam) opgeven. |Nee |&nbsp; |
| encryptedCredential |Hallo versleutelde referentie tooaccess Hallo FTP-server opgeven. |Nee |&nbsp; |
| gatewayName |Hallo naam opgeven van Hallo gateway in Data Management Gateway tooconnect tooan lokale FTP-server. |Nee |&nbsp; |
| poort |Geef op welke Hallo FTP-server luistert Hallo-poort. |Nee |21 |
| enableSsl |Geef op of toouse FTP via een SSL/TLS-kanaal. |Nee |De waarde True |
| enableServerCertificateValidation |Geef op of tooenable server SSL certificaatcontrole wanneer u FTP via SSL/TLS-kanaal. |Nee |De waarde True |

### <a name="use-anonymous-authentication"></a>Gebruik anonieme verificatie

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a>Gebruik van gebruikersnaam en wachtwoord voor basisverificatie in tekst zonder opmaak

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a>Gebruik poort, enableSsl, enableServerCertificateValidation

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a>EncryptedCredential gebruiken voor verificatie en gateway

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets [gegevenssets maken](data-factory-create-datasets.md). Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen van de gegevensset.

Hallo **typeProperties** sectie verschilt voor elk type dataset. Het levert informatie die specifieke toohello gegevensset type. Hallo **typeProperties** sectie voor een gegevensset van het type **FileShare** heeft Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| folderPath |Subpad toohello map. Gebruik van escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks. Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.<br/><br/>U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen en eindigen datums en tijden. |Ja |
| fileName |Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo. Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.<br/><br/>Wanneer **fileName** is niet opgegeven voor een uitvoergegevensset Hallo-naam van Hallo gegenereerd bestand is in de volgende indeling Hallo: <br/><br/>Gegevens. <Guid>.txt (voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Nee |
| fileFilter |Geef een filter toobe gebruikt tooselect een subset van de bestanden in Hallo **folderPath**, in plaats van alle bestanden.<br/><br/>Toegestane waarden zijn: `*` (meerdere tekens) en `?` (willekeurig teken).<br/><br/>Voorbeeld 1:`"fileFilter": "*.log"`<br/>Voorbeeld 2:`"fileFilter": 2014-1-?.txt"`<br/><br/> **fileFilter** is van toepassing op een bestandsshare-invoergegevensset. Deze eigenschap wordt niet ondersteund met Hadoop Distributed File System (HDFS). |Nee |
| partitionedBy |Gebruikt een dynamische toospecify **folderPath** en **fileName** voor tijd reeksgegevens. Bijvoorbeeld, kunt u een **folderPath** met parameters die voor elk uur van gegevens. |Nee |
| Indeling | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set Hallo **type** eigenschap onder indeling tooone van deze waarden. Zie voor meer informatie, Hallo [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren-indeling ](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. <br><br> Als u wilt toocopy bestanden zoals ze tussen winkels op basis van bestanden (binaire kopiëren zijn), moet u Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan. |Nee |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**, en ondersteunde niveaus zijn **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |
| useBinaryTransfer |Geef op of overdrachtsmodus toouse Hallo binary. Hallo-waarden zijn true zijn voor binaire modus (dit is de standaardwaarde Hallo) en false voor ASCII. Deze eigenschap kan alleen worden gebruikt wanneer hello type bijbehorende gekoppelde service type: FtpServer. |Nee |

> [!NOTE]
> **Bestandsnaam** en **fileFilter** niet gelijktijdig worden gebruikt.

### <a name="use-hello-partionedby-property"></a>Hallo partionedBy eigenschap gebruiken
Zoals vermeld in de vorige sectie hello, kunt u een dynamische **folderPath** en **fileName** voor tijd reeksgegevens Hello **partitionedBy** eigenschap.

toolearn over tijd reeks gegevenssets, planning en segmenten, Zie [gegevenssets maken](data-factory-create-datasets.md), [planning en uitvoering](data-factory-scheduling-and-execution.md), en [pijplijnen maken](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Voorbeeld 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
In dit voorbeeld {segment} is vervangen door de waarde van de Data Factory systeemvariabele SliceStart hello, in Hallo opmaken opgegeven (YYYYMMDDHH). Hallo SliceStart verwijst toostart tijd van Hallo segment. Hallo mappad verschilt voor elk segment. (Bijvoorbeeld wikidatagateway/wikisampledataout/2014100103 of wikidatagateway/wikisampledataout/2014100104.)

#### <a name="sample-2"></a>Voorbeeld 2

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
In dit voorbeeld Hallo jaar, maand, dag en tijd van de SliceStart worden uitgepakt in verschillende variabelen die worden gebruikt door Hallo **folderPath** en **fileName** eigenschappen.

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten [pijplijnen maken](data-factory-create-pipelines.md). Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.

Eigenschappen die beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit op Hallo Hallo daarentegen, variëren met elk activiteitstype. Voor de kopieeractiviteit hello afhankelijk Hallo type-eigenschappen Hallo soorten gegevensbronnen en Put.

In de kopieerbewerking wanneer Hallo bron van het type **FileSystemSource**, Hallo eigenschap na is beschikbaar in **typeProperties** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| Recursieve |Hiermee wordt aangegeven of gegevens Hallo recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo. |True, False (standaard) |Nee |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a>JSON-voorbeeld: gegevens kopiëren van de FTP-server tooAzure Blob
In dit voorbeeld laat zien hoe toocopy gegevens van een FTP-server tooAzure Blob-opslag. Echter gegevens kunnen worden gekopieerd direct tooany Hallo sinks vermelde in Hallo [ondersteunde gegevensarchieven en indelingen](data-factory-data-movement-activities.md#supported-data-stores-and-formats), met behulp van de kopieeractiviteit Hallo in Data Factory.  

Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):

* Een gekoppelde service van het type [FtpServer](#linked-service-properties)
* Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Invoer [gegevensset](data-factory-create-datasets.md) van het type [bestandsshare](#dataset-properties)
* Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [FileSystemSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

Hallo-voorbeeld worden gegevens gekopieerd van een FTP-server tooan Azure blob elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

### <a name="ftp-linked-service"></a>Gekoppelde FTP-service

Basisverificatie, wordt dit voorbeeld met het Hallo-gebruikersnaam en wachtwoord in tekst zonder opmaak. U kunt ook een van de volgende manieren hello gebruiken:

* Anonieme verificatie
* Basisverificatie met versleutelde referenties
* FTP via SSL/TLS (FTPS)

Zie Hallo [FTP gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service

```JSON
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
### <a name="ftp-input-dataset"></a>FTP-invoergegevensset

Deze gegevensset verwijst toohello FTP-map `mysharedfolder` en de bestandsnaam `test.csv`. Hallo pijplijn kopieert Hallo toohello bestemming.

Instelling **externe** te**true** informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a>Azure Blob-uitvoergegevensset

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). Hallo mappad voor Hallo blob wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. mappad Hallo Hallo jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a>Een kopieeractiviteit in een pijplijn met systeem bron- en blob bestandssink

Hallo pijplijn bevat een kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**FileSystemSource**, en Hallo **sink** type is ingesteld, te**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="next-steps"></a>Volgende stappen
Zie Hallo artikelen te volgen:

* toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (kopieeractiviteit) in Gegevensfactory en verschillende manieren toooptimize, Zie Hallo [activiteit prestaties en prestatieafstemming handleiding kopiëren](data-factory-copy-activity-performance.md).

* Zie voor stapsgewijze instructies voor het maken van een pijplijn met een kopieeractiviteit hello [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
