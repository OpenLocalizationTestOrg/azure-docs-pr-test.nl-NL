---
title: aaaMove gegevens van Web-tabel met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over hoe toomove gegevens uit een tabel in een Web-pagina met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a>Verplaatsen van gegevens uit een tabel Webbron met behulp van Azure Data Factory
In dit artikel bevat een overzicht van hoe toouse hello Kopieeractiviteit in Azure Data Factory toomove gegevens uit een tabel in een webpagina tooa gegevensarchief sink ondersteund. In dit artikel is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel met daarin een algemeen overzicht van de verplaatsing van gegevens kopiëren-activiteit en Hallo lijst met gegevensarchieven ondersteund als bronnen/Put.

Data factory ondersteunt momenteel alleen zwevend gegevens van een Web-tabelgegevens tooother wordt opgeslagen, maar niet verplaatsen van gegevens van andere gegevens worden opgeslagen tooa Web tabel bestemming.

> [!IMPORTANT]
> Deze Web-connector ondersteunt momenteel alleen uitpakken tabelinhoud uit een HTML-pagina. tooretrieve gegevens van een HTTP/s-eindpunt gebruik [HTTP connector](data-factory-http-connector.md) in plaats daarvan.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's. 

- Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren. 
- U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. 
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. 

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een tabel web zijn [JSON-voorbeeld: gegevens kopiëren van Web tabel tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) sectie van dit artikel. 

Hallo volgende secties vindt u informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooa Web tabel zijn:

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooWeb gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **Web** |Ja |
| URL |URL toohello webbron |Ja |
| authenticationType |Anonieme. |Ja |

### <a name="using-anonymous-authentication"></a>Anonieme verificatie

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).

Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo typeProperties sectie voor de gegevensset van het type **WebTable** heeft de volgende eigenschappen Hallo

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| type |Type Hallo gegevensset. te moet worden ingesteld**WebTable** |Ja |
| Pad |Een relatieve URL toohello-bron die Hallo tabel bevat. |Nee. Wanneer het pad niet wordt opgegeven, wordt alleen Hallo URL die is opgegeven in de servicedefinitie Hallo gekoppeld gebruikt. |
| Index |Hallo index van de tabel Hallo in Hallo resource. Zie [Get-index van een tabel in een HTML-pagina](#get-index-of-a-table-in-an-html-page) sectie voor stappen toogetting index van een tabel in een HTML-pagina. |Ja |

**Voorbeeld:**

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
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

Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

Op dit moment wanneer Hallo-bron in de kopieerbewerking is van het type **WebSource**, zonder aanvullende eigenschappen worden ondersteund.


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a>JSON-voorbeeld: gegevens kopiëren van Web tabel tooAzure Blob
Hallo volgende ziet:

1. Een gekoppelde service van het type [Web](#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [WebTable](#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [WebSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo-voorbeeld worden gegevens gekopieerd van een Web tabel tooan Azure blob elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

Hallo volgende voorbeeld ziet u hoe toocopy gegevens van een Web tabel tooan Azure-blob. Echter gegevens kunnen worden gekopieerd direct tooany Hallo sinks vermelde in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel met behulp van Hallo Kopieeractiviteit in Azure Data Factory.

**Web service gekoppelde** in dit voorbeeld gebruikt Hallo Web gekoppelde service met anonieme verificatie. Zie [Web gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
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

**WebTable invoergegevensset** instelling **externe** te**true** Hallo Data Factory-service te informeren dat gegevensset Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in Hallo Data factory.

> [!NOTE]
> Zie [Get-index van een tabel in een HTML-pagina](#get-index-of-a-table-in-an-html-page) sectie voor stappen toogetting index van een tabel in een HTML-pagina.  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


**Azure Blob-uitvoergegevensset**

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



**Pijplijn met de kopieeractiviteit**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**WebSource** en **sink** type is ingesteld, te**BlobSink**.

Zie [WebSource type-eigenschappen](#copy-activity-type-properties) voor Hallo lijst met eigenschappen die ondersteund worden door Hallo WebSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a>Ophalen van de index van een tabel in een HTML-pagina
1. Start **Excel 2016** en switch toohello **gegevens** tabblad.  
2. Klik op **nieuwe Query** op Hallo werkbalk wijst te**van andere bronnen** en klik op **uit Web**.

    ![Power Query-menu](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. In Hallo **uit Web** dialoogvenster Voer **URL** die u wilt gebruiken in de gekoppelde service JSON (bijvoorbeeld: https://en.wikipedia.org/wiki/) samen met u voor de gegevensset Hallo geeft pad (bijvoorbeeld: AFI % 27s_100_Years... 100_Movies), en klik op **OK**.

    ![Dialoogvenster Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    URL die wordt gebruikt in dit voorbeeld: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies
4. Als u ziet **toegang tot webinhoud** in het dialoogvenster, selecteer Hallo rechts **URL**, **verificatie**, en klik op **Connect**.

   ![Dialoogvenster voor toegang tot Web-inhoud](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. Klik op een **tabel** in Hallo structuur weergave toosee inhoud uit de tabel Hallo-item en klik vervolgens op **bewerken** knop Hallo onder aan.  

   ![Dialoogvenster Navigator](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. In Hallo **Query-Editor** venster, klikt u op **geavanceerde Editor** op de werkbalk Hallo.

    ![De knop Geavanceerd Editor](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. Hallo Hallo geavanceerde Editor in het dialoogvenster getal naast te 'Bron' hello index is.

    ![Geavanceerde Editor - Index](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

Als u Excel 2013 gebruikt, gebruikt u [Microsoft Power Query voor Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget Hallo index. Zie [Connect tooa webpagina](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) artikel voor meer informatie. Hallo stappen zijn vergelijkbaar zijn als u [Microsoft Power BI voor bureaublad](https://powerbi.microsoft.com/desktop/).

> [!NOTE]
> toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
