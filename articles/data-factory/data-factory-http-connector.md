---
title: gegevens van de bron van een HTTP - Azure aaaMove | Microsoft Docs
description: Meer informatie over hoe toomove uit een on-premises of in een cloud HTTP gegevensbron met behulp van Azure Data Factory.
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
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a>Gegevens verplaatsen van een HTTP-bron met behulp van Azure Data Factory
In dit artikel bevat een overzicht van hoe toouse hello Kopieeractiviteit in Azure Data Factory toomove gegevens uit een on-premises/cloudtoepassing HTTP-eindpunt tooa gegevensarchief sink ondersteund. In dit artikel is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel met daarin een algemeen overzicht van de verplaatsing van gegevens kopiëren-activiteit en Hallo lijst met gegevensarchieven ondersteund als bronnen/Put.

Data factory momenteel ondersteunt alleen het verplaatsen van gegevens van een HTTP tooother gegevensarchieven bron, maar niet verplaatsen van gegevens van andere gegevens worden opgeslagen tooan HTTP bestemming.

## <a name="supported-scenarios-and-authentication-types"></a>Ondersteunde scenario's en verificatietypen
U kunt deze gegevens HTTP connector tooretrieve uit **zowel cloud als on-premises HTTP/s-eindpunt** met behulp van HTTP **ophalen** of **POST** methode. Hallo verificatietypen volgende worden ondersteund: **anoniem**, **Basic**, **Digest**, **Windows**, en  **ClientCertificate**. Houd er rekening mee Hallo verschil tussen deze connector en Hallo [Web tabel connector](data-factory-web-table-connector.md) is: laatste Hallo gebruikte tooextract tabelinhoud van HTML-webpagina is.

Bij het kopiëren van gegevens uit een lokale HTTP-eindpunt, moet u een Data Management Gateway installeren in Hallo lokale omgeving/Azure VM. Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens van een HTTP-bron verplaatst met behulp van verschillende hulpprogramma's voor API's.

- Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

- U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. Zie voor JSON-toocopy gegevens uit de HTTP-bron tooAzure Blob Storage voorbeelden, [JSON voorbeelden](#json-examples) sectie van dit artikel.

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooHTTP gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type | Hallo type eigenschap moet worden ingesteld op: `Http`. | Ja |
| URL | Basis-URL toohello webserver | Ja |
| authenticationType | Hiermee geeft u het verificatietype Hallo. Toegestane waarden zijn: **anoniem**, **Basic**, **Digest**, **Windows**, **ClientCertificate**. <br><br> Raadpleeg toosections onder deze tabel over meer eigenschappen en voorbeelden van JSON respectievelijk voor deze verificatietypen. | Ja |
| enableServerCertificateValidation | Opgeven of tooenable server SSL certificaatcontrole als bron is een HTTPS-webserver | Nee, de standaardwaarde is true |
| gatewayName | Naam van Hallo Data Management Gateway tooconnect tooan lokale HTTP-bron. | Ja als u gegevens kopiëren van een lokale HTTP-bron. |
| encryptedCredential | Versleutelde referentie tooaccess Hallo HTTP-eindpunt. Automatisch wordt gegenereerd wanneer u Hallo verificatiegegevens in kopiëren wizard of Hallo ClickOnce pop-up dialoogvenster configureert. | Nee. Alleen van toepassing wanneer het kopiëren van gegevens uit een lokale HTTP-server. |

Zie [gegevens verplaatsen tussen lokale bronnen en Hallo cloud met Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) voor meer informatie over het instellen van referenties voor on-premises HTTP connector-gegevensbron.

### <a name="using-basic-digest-or-windows-authentication"></a>Met behulp van basisverificatie, verificatiesamenvatting of Windows-verificatie

Stel `authenticationType` als `Basic`, `Digest`, of `Windows`, en geef de volgende eigenschappen afgezien van HTTP-connector algemene werden geïntroduceerd hierboven Hallo Hallo:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| gebruikersnaam | Gebruikersnaam tooaccess Hallo HTTP-eindpunt. | Ja |
| wachtwoord | Wachtwoord voor gebruiker hello (gebruikersnaam). | Ja |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Voorbeeld: met behulp van basisverificatie, verificatiesamenvatting of Windows-verificatie

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a>ClientCertificate-verificatie

Basisverificatie toouse ingesteld `authenticationType` als `ClientCertificate`, en geef de volgende eigenschappen afgezien van HTTP-connector algemene werden geïntroduceerd hierboven Hallo Hallo:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| embeddedCertData | Hallo Base64-gecodeerde inhoud van de binaire gegevens van Hallo Personal Information Exchange (PFX)-bestand. | Geef beide Hallo `embeddedCertData` of `certThumbprint`. |
| certThumbprint | Hallo vingerafdruk van certificaat Hallo die is geïnstalleerd op de gatewaycomputer certificaatarchief. Alleen van toepassing wanneer het kopiëren van gegevens van een lokale HTTP-bron. | Geef beide Hallo `embeddedCertData` of `certThumbprint`. |
| wachtwoord | Het wachtwoord die zijn gekoppeld aan het Hallo-certificaat. | Nee |

Als u `certThumbprint` voor verificatie en Hallo-certificaat is geïnstalleerd in het persoonlijke archief van de lokale computer Hallo hello, moet u toogrant Hallo leesmachtiging toohello gateway-service:

1. Start Microsoft Management Console (MMC). Hallo toevoegen **certificaten** -module die Hallo doelen **lokale Computer**.
2. Vouw **certificaten**, **persoonlijke**, en klik op **certificaten**.
3. Met de rechtermuisknop op het Hallo-certificaat uit het persoonlijke archief Hallo en selecteer **alle taken**->**persoonlijke sleutels beheren...**
3. Op Hallo **beveiliging** tabblad, waaronder Data Management Gateway Host Service wordt uitgevoerd met Hallo leestoegang toohello certificaat Hallo-gebruikersaccount toevoegen.  

#### <a name="example-using-client-certificate"></a>Voorbeeld: met behulp van clientcertificaat
Deze gekoppelde service wordt uw data factory tooan lokale HTTP-webserver. Dit maakt gebruik van een clientcertificaat dat is geïnstalleerd op machine Hallo met Data Management Gateway is geïnstalleerd.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Voorbeeld: clientcertificaat gebruiken in een bestand
Deze gekoppelde service wordt uw data factory tooan lokale HTTP-webserver. Een certificaatbestand op Hallo machine wordt met Data Management Gateway is geïnstalleerd.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).

Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo typeProperties sectie voor de gegevensset van het type **Http** heeft de volgende eigenschappen Hallo

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| type | Hallo Hallo gegevensset type opgegeven. te moet worden ingesteld`Http`. | Ja |
| relativeUrl | Een relatieve URL toohello-bron die Hallo gegevens bevat. Wanneer het pad niet wordt opgegeven, wordt alleen Hallo URL die is opgegeven in de servicedefinitie Hallo gekoppeld gebruikt. <br><br> dynamische tooconstruct-URL, kunt u [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md), bijvoorbeeld 'relativeUrl': ' $$Text.Format ('/ Mijn/rapport? maand = {0:yyyy}-{0:MM} & fmt csv =', SliceStart) '. | Nee |
| requestMethod | HTTP-methode. Toegestane waarden zijn **ophalen** of **POST**. | Nee. Standaard is `GET`. |
| additionalHeaders | Aanvullende HTTP-aanvraagheaders. | Nee |
| requestBody | Instantie voor HTTP-aanvraag. | Nee |
| Indeling | Als u wilt dat toosimply **Hallo-gegevens ophalen van HTTP-eindpunt als-is** overslaan zonder deze parseren, deze instellingen. <br><br> Als u tooparse Hallo HTTP-antwoord inhoud tijdens het kopiëren wilt, Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. |Nee |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**. Ondersteunde niveaus: **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |

### <a name="example-using-hello-get-default-method"></a>Voorbeeld: via Hallo GET (standaard)-methode

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a>Voorbeeld: via Hallo POST-methode

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.

Eigenschappen die beschikbaar zijn in Hallo **typeProperties** sectie Hallo-activiteit op Hallo daarentegen variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

Op dit moment wanneer Hallo-bron in de kopieerbewerking is van het type **HttpSource**, Hallo volgende eigenschappen worden ondersteund.

| Eigenschap | Beschrijving | Vereist |
| -------- | ----------- | -------- |
| httpRequestTimeout | Hallo-out (TimeSpan) voor Hallo HTTP-aanvraag tooget een antwoord. Hallo time-out tooget een antwoord niet Hallo time-out tooread antwoordgegevens is. | Nee. Standaardwaarde: 00:01:40 |

## <a name="supported-file-and-compression-formats"></a>Ondersteunde indelingen voor bestands- en compressie
Zie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel voor meer informatie.

## <a name="json-examples"></a>JSON-voorbeelden
Hallo volgt voorbeeld JSON definities bieden dat u een pijplijn toocreate gebruiken met behulp van kunt [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ze geven weer hoe toocopy van HTTP gegevensbron tooAzure Blob Storage. Echter gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a>Voorbeeld: Gegevens kopiëren van de HTTP-bron tooAzure Blob-opslag
Hallo Data Factory-oplossing voor dit voorbeeld bevat Hallo Data Factory-entiteiten te volgen:

1. Een gekoppelde service van het type [HTTP](#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [Http](#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [HttpSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo-voorbeeld worden gegevens gekopieerd van een HTTP-bron tooan Azure blob elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

### <a name="http-linked-service"></a>Gekoppelde HTTP-service
In dit voorbeeld maakt gebruik van HTTP Hallo gekoppelde service met anonieme verificatie. Zie [HTTP gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
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

### <a name="http-input-dataset"></a>HTTP-invoergegevensset
Instelling **externe** te**true** informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a>Azure Blob-uitvoergegevensset

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a>Pijplijn met de kopieeractiviteit

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**HttpSource** en **sink** type is ingesteld, te**BlobSink**.

Zie [HttpSource](#copy-activity-properties) voor Hallo lijst met eigenschappen die ondersteund worden door Hallo HttpSource.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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

> [!NOTE]
> toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
