---
title: aaaMove-gegevens van de SFTP-server met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens uit een on-premises of een cloud SFTP-server met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a>Gegevens verplaatsen van een SFTP-server met behulp van Azure Data Factory
In dit artikel bevat een overzicht van hoe toouse hello Kopieeractiviteit in Azure Data Factory toomove gegevens uit een on-premises/cloudtoepassing SFTP server tooa gegevensarchief sink ondersteund. In dit artikel is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel met daarin een algemeen overzicht van de verplaatsing van gegevens kopiëren-activiteit en Hallo lijst met gegevensarchieven ondersteund als bronnen/Put.

Data factory ondersteunt momenteel alleen verplaatsen van gegevens uit een SFTP server tooother-gegevens worden opgeslagen, maar niet voor het verplaatsen van gegevens van andere gegevens worden opgeslagen tooan SFTP-server. Deze ondersteuning biedt voor zowel on-premises en in de cloud SFTP-servers.

> [!NOTE]
> Kopieeractiviteit worden Hallo-bronbestand niet verwijderd nadat het is gekopieerde toohello bestemming. Als u toodelete Hallo-bronbestand na een geslaagde kopie moet, maakt u een aangepaste activiteit toodelete Hallo-bestand en Hallo activiteit in de pijplijn hello gebruiken. 

## <a name="supported-scenarios-and-authentication-types"></a>Ondersteunde scenario's en verificatietypen
U kunt deze gegevens SFTP connector toocopy uit **zowel cloud SFTP-servers en on-premises SFTP-servers**. **Basic** en **SshPublicKey** authenticatietypen worden ondersteund bij het verbinden van toohello SFTP-server.

Als u gegevens uit een on-premises SFTP-server, moet u een Data Management Gateway installeren in Hallo lokale omgeving/Azure VM. Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor meer informatie over het Hallo-gateway. Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies voor het Hallo-gateway instellen en gebruiken.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een bron SFTP verplaatst met behulp van verschillende hulpprogramma's voor API's.

- Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

- U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. Zie voor JSON-toocopy gegevens van SFTP server tooAzure Blob Storage voorbeelden, [JSON-voorbeeld: gegevens kopiëren van SFTP server tooAzure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) sectie van dit artikel.

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooFTP gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- | --- |
| type | de eigenschap type Hello te moet worden ingesteld`Sftp`. |Ja |
| host | Naam of IP-adres van Hallo SFTP-server. |Ja |
| poort |De poort op welke Hallo SFTP-server luistert. de standaardwaarde Hallo is: 21 |Nee |
| authenticationType |Geef het verificatietype. Toegestane waarden: **Basic**, **SshPublicKey**. <br><br> Raadpleeg te[Using basisverificatie](#using-basic-authentication) en [met behulp van SSH openbare-sleutelauthenticatie](#using-ssh-public-key-authentication) respectievelijk secties over meer eigenschappen en voorbeelden van JSON. |Ja |
| skipHostKeyValidation | Geef op of tooskip sleutel validatie hosten. | Nee. standaardwaarde Hallo: false |
| hostKeyFingerprint | Hallo-vingerafdruk van Hallo hostsleutel opgeven. | Ja als hello `skipHostKeyValidation` toofalse is ingesteld.  |
| gatewayName |Naam van Hallo Data Management Gateway tooconnect tooan een on-premises SFTP-server. | Ja als u kopiëren van gegevens uit een on-premises SFTP-server. |
| encryptedCredential | Versleutelde referentie tooaccess Hallo SFTP-server. Automatisch gegenereerd als u basisverificatie (gebruikersnaam en wachtwoord) of SshPublicKey verificatie (gebruikersnaam + pad naar de persoonlijke sleutel of inhoud) in kopiëren wizard of Hallo ClickOnce pop-up dialoogvenster opgeven. | Nee. Alleen van toepassing wanneer het kopiëren van gegevens uit een on-premises SFTP-server. |

### <a name="using-basic-authentication"></a>Met behulp van basisverificatie

Basisverificatie toouse ingesteld `authenticationType` als `Basic`, en geef de volgende eigenschappen afgezien van SFTP connector algemene die zijn geïntroduceerd in de laatste sectie Hallo HALLO hallo:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- | --- |
| gebruikersnaam | Gebruiker met toegang toohello SFTP-server. |Ja |
| wachtwoord | Wachtwoord voor gebruiker hello (gebruikersnaam). | Ja |

#### <a name="example-basic-authentication"></a>Voorbeeld: Basisverificatie
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Voorbeeld: Basisverificatie met versleutelde referentie

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a>Met behulp van SSH-verificatie voor openbare sleutel

Stel toouse SSH openbare-sleutelauthenticatie, `authenticationType` als `SshPublicKey`, en geef de volgende eigenschappen afgezien van SFTP connector algemene die zijn geïntroduceerd in de laatste sectie Hallo HALLO hallo:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- | --- |
| gebruikersnaam |Gebruiker met toegang toohello SFTP-server |Ja |
| privateKeyPath | Geef het absolute pad toohello persoonlijke sleutelbestand dat gateway kunt openen. | Geef beide Hallo `privateKeyPath` of `privateKeyContent`. <br><br> Alleen van toepassing wanneer het kopiëren van gegevens uit een on-premises SFTP-server. |
| privateKeyContent | Een geserialiseerde tekenreeks Hallo-inhoud met persoonlijke sleutel. Hallo Wizard kopiëren kunt Hallo persoonlijke sleutelbestand lezen inhoud en extraheren Hallo persoonlijke sleutel automatisch. Als u van andere hulpprogramma/SDK gebruikmaakt, gebruikt u de Hallo privateKeyPath eigenschap. | Geef beide Hallo `privateKeyPath` of `privateKeyContent`. |
| Wachtwoordzin | Hallo pass woordgroep en het wachtwoord toodecrypt Hallo persoonlijke sleutel opgeven als Hallo-sleutelbestand is beveiligd met een wachtwoordzin. | Ja als Hallo-bestand met persoonlijke sleutel wordt beveiligd door een wachtwoordzin. |

> [!NOTE]
> SFTP-connector ondersteunen alleen OpenSSH-sleutel. Zorg ervoor dat uw sleutelbestand Hallo juiste indeling. U kunt Putty hulpprogramma tooconvert uit ppk tooOpenSSH indeling gebruiken.

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a>Voorbeeld: SshPublicKey verificatie met behulp van persoonlijke sleutels filePath

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Voorbeeld: SshPublicKey verificatie met behulp van persoonlijke sleutels inhoud

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen van de gegevensset.

Hallo **typeProperties** sectie verschilt voor elk type dataset. Het levert informatie die specifieke toohello gegevensset type. Hallo typeProperties sectie voor een gegevensset van het type **FileShare** dataset bevat Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| folderPath |Submap pad toohello. Gebruik van escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks. Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.<br/><br/>U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden. |Ja |
| fileName |Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo. Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.<br/><br/>Wanneer fileName niet voor een uitvoergegevensset opgegeven is, zou Hallo van Hallo gegenereerd bestand in worden Hallo volgt deze indeling: <br/><br/>Gegevens. <Guid>.txt (voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nee |
| fileFilter |Geef dat een filter toobe tooselect gebruikt een subset van de bestanden in Hallo folderPath in plaats van alle bestanden.<br/><br/>Toegestane waarden zijn: `*` (meerdere tekens) en `?` (willekeurig teken).<br/><br/>Voorbeelden 1:`"fileFilter": "*.log"`<br/>Voorbeeld 2:`"fileFilter": 2014-1-?.txt"`<br/><br/> fileFilter geldt voor een invoergegevensset bestandsshare. Deze eigenschap wordt niet ondersteund met HDFS. |Nee |
| partitionedBy |partitionedBy mag gebruikte toospecify een dynamische folderPath bestandsnaam op van de reeksgegevens. Bijvoorbeeld, folderPath geparametriseerde voor elk uur van gegevens. |Nee |
| Indeling | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set Hallo **type** eigenschap onder indeling tooone van deze waarden. Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. <br><br> Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan. |Nee |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**. Ondersteunde niveaus: **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |
| useBinaryTransfer |Geef binaire overdrachtsmodus of gebruiken. De waarde True voor binaire modus en ONWAAR ASCII. Standaardwaarde: True. Deze eigenschap kan alleen worden gebruikt wanneer de bijbehorende gekoppelde-servicetype is van het type: FtpServer. |Nee |

> [!NOTE]
> bestandsnaam en fileFilter worden niet gelijktijdig gebruikt.

### <a name="using-partionedby-property"></a>Gebruik de eigenschap partionedBy
Zoals vermeld in de vorige sectie hello, kunt u een dynamische folderPath, filename voor time series-gegevens met partitionedBy opgeven. U kunt dit doen met Hallo Data Factory-macro's en Hallo systeemvariabele SliceStart, SliceEnd die wijzen op Hallo logische periode voor een bepaalde gegevenssegment.

toolearn over tijd reeks gegevenssets, planning en segmenten, Zie [gegevenssets maken](data-factory-create-datasets.md), [planning en uitvoering](data-factory-scheduling-and-execution.md), en [pijplijnen maken](data-factory-create-pipelines.md) artikelen.

#### <a name="sample-1"></a>Voorbeeld 1:

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
In dit voorbeeld {segment} is vervangen door de waarde van de Hallo van Data Factory systeemvariabele SliceStart Hallo-indeling (YYYYMMDDHH) opgegeven. Hallo SliceStart verwijst toostart tijd van Hallo segment. Hallo folderPath verschilt voor elk segment. Voorbeeld: wikidatagateway/wikisampledataout/2014100103 of wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Voorbeeld 2:

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
In dit voorbeeld worden jaar, maand, dag en tijd van de SliceStart uitgepakt in verschillende variabelen die worden gebruikt door de eigenschappen voor folderPath en de bestandsnaam.

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.

Terwijl het Hallo-eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype. Voor de kopieeractiviteit, wordt Hallo type-eigenschappen variëren afhankelijk van Hallo soorten gegevensbronnen en Put.

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a>Ondersteunde indelingen voor bestands- en compressie
Zie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel voor meer informatie.

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a>JSON-voorbeeld: Gegevens kopiëren van SFTP server tooAzure blob
Hallo volgende voorbeeld wordt een voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ze geven weer hoe toocopy van SFTP gegevensbron tooAzure Blob Storage. Echter gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.

> [!IMPORTANT]
> Dit voorbeeld bevat JSON-fragmenten. Dit omvat geen stapsgewijze instructies voor het maken van de gegevensfactory Hallo. Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies.

Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:

* Een gekoppelde service van het type [sftp](#linked-service-properties).
* Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Invoer [gegevensset](data-factory-create-datasets.md) van het type [FileShare](#dataset-properties).
* Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [FileSystemSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo-voorbeeld worden gegevens gekopieerd van een SFTP server tooan Azure blob elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

**Gekoppelde SFTP-service**

In dit voorbeeld gebruikt de basisverificatie Hallo met gebruikersnaam en wachtwoord in tekst zonder opmaak. U kunt ook een van de volgende manieren hello gebruiken:

* Basisverificatie met versleutelde referenties
* SSH-verificatie voor openbare sleutel

Zie [FTP gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
**Een gekoppelde Azure Storage-service**

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
**Invoergegevensset SFTP**

Deze gegevensset verwijst toohello SFTP map `mysharedfolder` en de bestandsnaam `test.csv`. Hallo pijplijn kopieert Hallo toohello bestemming.

Instelling 'extern': 'true' informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Azure Blob-uitvoergegevensset**

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Pijplijn met de kopieeractiviteit**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**FileSystemSource** en **sink** type is ingesteld, te**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.

## <a name="next-steps"></a>Volgende stappen
Zie Hallo artikelen te volgen:

* [Zelfstudie voor kopiëren-activiteit](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor het maken van een pijplijn met een Kopieeractiviteit.
