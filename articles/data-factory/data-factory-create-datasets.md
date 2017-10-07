---
title: aaaCreate gegevenssets in Azure Data Factory | Microsoft Docs
description: Informatie over hoe toocreate gegevenssets in Azure Data Factory met voorbeelden die gebruikmaken van eigenschappen zoals offset en anchorDateTime.
keywords: dataset gegevensset voorbeeld maken, voorbeeld van de offset
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a>Gegevenssets in Azure Data Factory
In dit artikel wordt beschreven welke gegevenssets zijn, hoe ze worden gedefinieerd in JSON-indeling, en hoe ze worden gebruikt Azure Data Factory-pijplijnen. Het biedt details over elke sectie (bijvoorbeeld, structuur, beschikbaarheid en beleid) in Hallo gegevensset JSON-definitie. Hallo artikel biedt ook voorbeelden voor het gebruik van Hallo **offset**, **anchorDateTime**, en **stijl** eigenschappen in de JSON-definitie van een dataset.

> [!NOTE]
> Als u nieuwe tooData Factory, Zie [inleiding tooAzure Data Factory](data-factory-introduction.md) voor een overzicht. Als u praktische ervaring met het maken van gegevensfactory niet hebt, kunt u toegang een beter inzicht door Hallo lezen [data transformation zelfstudie](data-factory-build-your-first-pipeline.md) en Hallo [data movement zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="overview"></a>Overzicht
Een gegevensfactory kan één of meer pijplijnen hebben. Een **pijplijn** is een logische groepering van **activiteiten** die samen een taak uitvoeren. Hallo-activiteiten in een pijplijn definiëren tooperform acties op uw gegevens. U kunt bijvoorbeeld een kopie toocopy activiteitsgegevens van een lokale SQL Server tooAzure Blob-opslag. Vervolgens kunt u een Hive-activiteit die wordt een Hive-script uitgevoerd op een Azure HDInsight-cluster tooprocess gegevens uit Blob storage tooproduce uitvoergegevens. Ten slotte kunt u een tweede kopie activiteit toocopy Hallo uitvoer gegevens tooAzure SQL Data Warehouse boven op welke business intelligence (BI) reporting oplossingen zijn gebouwd. Zie voor meer informatie over de pijplijnen en activiteiten [pijplijnen en activiteiten in Azure Data Factory](data-factory-create-pipelines.md).

Een activiteit kan duren voordat de invoer van nul of meer **gegevenssets**, en een of meer uitvoergegevenssets te produceren. Een invoergegevensset Hallo invoer voor een activiteit in de pijplijn Hallo vertegenwoordigt, en een uitvoergegevensset Hallo uitvoer voor Hallo activiteit vertegenwoordigt. Met gegevenssets worden gegevens binnen andere gegevensarchieven geïdentificeerd, waaronder tabellen, bestanden, mappen en documenten. Een Azure Blob-gegevensset bevat bijvoorbeeld Hallo blob-container en map in Blob storage uit welke Hallo pijplijn Hallo gegevens moet lezen. 

Voordat u een gegevensset maakt, maakt u een **gekoppelde service** toolink uw gegevens opslaan toohello data factory. Gekoppelde services zijn veel zoals verbindingsreeksen die Hallo verbindingsinformatie die nodig is voor Data Factory tooconnect tooexternal bronnen definiëren. Gegevenssets identificeren gegevens in de gegevensarchieven Hallo gekoppeld, zoals SQL-tabellen, bestanden, mappen en documenten. Bijvoorbeeld, gekoppelde een Azure Storage service een gegevensfactory storage account toohello. Een Azure Blob-gegevensset vertegenwoordigt Hallo blob-container en Hallo-map met de Hallo invoer blobs toobe verwerkt. 

Hier volgt een voorbeeldscenario. toocopy gegevens uit Blob storage tooa SQL-database, hebt u twee gekoppelde services: Azure Storage en Azure SQL Database. Vervolgens maakt u twee gegevenssets: Azure Blob-gegevensset (die verwijst naar de toohello gekoppelde Azure Storage-service) en Azure SQL-tabel dataset (die verwijst naar de toohello Azure SQL Database gekoppeld service). Hallo Azure Storage en Azure SQL Database, gekoppelde services verbindingstekenreeksen bevatten die Data Factory maakt gebruik van op runtime tooconnect tooyour Azure Storage en Azure SQL Database, respectievelijk. Hello Azure Blob-gegevensset bevat Hallo blob-container en de blob map Hallo invoer blobs in de Blob-opslag bevat. Hello Azure SQL-tabel gegevensset geeft Hallo SQL-tabel in uw SQL-database toowhich Hallo-gegevens is toobe gekopieerd.

Hallo volgende diagram toont Hallo relaties tussen pipeline, de activiteit, de gegevensset en de gekoppelde service in de Data Factory: 

![Relatie tussen een pijplijn, activiteit, gegevensset, gekoppelde services](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a>JSON van de gegevensset
Een gegevensset in Gegevensfactory is gedefinieerd in JSON-indeling als volgt:

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

Hallo volgende tabel beschrijft de eigenschappen in Hallo hierboven JSON:   

| Eigenschap | Beschrijving | Vereist | Standaard |
| --- | --- | --- | --- |
| naam |Naam van het Hallo-gegevensset. Zie [Azure Data Factory - naamgevingsregels](data-factory-naming-rules.md) voor naamgevingsregels. |Ja |N.v.t. |
| type |Type Hallo gegevensset. Geef een Hallo die worden ondersteund door de Data Factory (bijvoorbeeld: AzureBlob, AzureSqlTable). <br/><br/>Zie voor meer informatie [gegevensettype](#Type). |Ja |N.v.t. |
| structuur |Schema van Hallo dataset.<br/><br/>Zie voor meer informatie [gegevenssetstructuur](#Structure). |Nee |N.v.t. |
| typeProperties | Hallo-eigenschappen zijn verschillend voor elk type (bijvoorbeeld: Azure Blob, Azure SQL-tabel). Zie voor informatie over de typen Hallo ondersteund en hun eigenschappen, [gegevensettype](#Type). |Ja |N.v.t. |
| external | Booleaanse waarde vlag toospecify of een gegevensset wordt expliciet geproduceerd door een data factory-pijplijn of niet. Als het Hallo-invoergegevensset voor een activiteit wordt niet door de huidige pipeline Hallo geproduceerd, stelt u deze vlag tootrue. Deze vlag tootrue voor invoergegevensset van de eerste activiteit Hallo Hallo in Hallo pijplijn instellen.  |Nee |ONWAAR |
| availability | Hallo venster verwerken (bijvoorbeeld per uur of dagelijks) of model voor Hallo gegevensset productie segmentering Hallo definieert. Elke eenheid gegevens verbruikt en die wordt geproduceerd door het uitvoeren van een activiteit wordt een gegevenssegment genoemd. Als een uitvoergegevensset Hallo beschikbaarheid is set toodaily (frequentie - dag, interval - 1), wordt dagelijks een segment geproduceerd. <br/><br/>Zie voor meer informatie [gegevensset beschikbaarheid](#Availability). <br/><br/>Zie voor informatie over Hallo gegevensset segmentering model Hallo [planning en uitvoering](data-factory-scheduling-and-execution.md) artikel. |Ja |N.v.t. |
| policy |Definieert Hallo criteria of Hallo voorwaarde waaraan Hallo gegevensset segmenten moeten voldoen. <br/><br/>Zie voor meer informatie, Hallo [gegevensset beleid](#Policy) sectie. |Nee |N.v.t. |

## <a name="dataset-example"></a>Voorbeeld van de gegevensset
In Hallo voorbeeld te volgen, Hallo gegevensset vertegenwoordigt een tabel met de naam **MyTable** in een SQL-database.

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

Houd er rekening mee Hallo volgende punten:

* **type** tooAzureSqlTable is ingesteld.
* **tableName** tooMyTable is ingesteld door de eigenschap type (specifieke tooAzureSqlTable type).
* **linkedServiceName** tooa gekoppelde service van het type AzureSqlDatabase die is gedefinieerd in de volgende JSON-codefragment Hallo verwijst. 
* **beschikbaarheid frequentie** tooDay, is ingesteld en **interval** too1 is ingesteld. Dit betekent dat Hallo gegevensset segment dagelijks wordt geproduceerd.  

**AzureSqlLinkedService** wordt als volgt gedefinieerd:

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

In Hallo voorafgaand aan JSON-fragment:

* **type** tooAzureSqlDatabase is ingesteld.
* **connectionString** type-eigenschap geeft u informatie tooconnect tooa SQL-database.  

Zoals u ziet, hello gekoppelde service definieert hoe tooconnect tooa SQL-database. Hallo gegevensset definieert welke tabel wordt gebruikt als invoer en uitvoer van activiteit in een pijplijn Hallo.   

> [!IMPORTANT]
> Tenzij een gegevensset wordt geproduceerd door de pijplijn hello, moet dit worden gemarkeerd als **externe**. Deze instelling geldt doorgaans tooinputs van de eerste activiteit in een pijplijn.   


## <a name="Type"></a>Gegevensettype
Hallo type Hallo dataset is afhankelijk van Hallo-gegevensarchief die u gebruikt. Zie Hallo volgende tabel voor een lijst met opgeslagen gegevens die door Data Factory worden ondersteund. Klik op een data store toolearn hoe toocreate een gekoppelde service en een gegevensset voor dat de gegevens worden opgeslagen.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Gegevens worden opgeslagen met * on-premises kan worden of op Azure-infrastructuur als een service (IaaS). Deze gegevensarchieven moeten u tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).

In voorbeeld in de vorige sectie Hallo HALLO hallo type Hallo gegevensset te is ingesteld**AzureSqlTable**. Op deze manier voor een Azure Blob-gegevensset Hallo type Hallo dataset is ingesteld te**AzureBlob**, zoals weergegeven in de volgende JSON Hallo:

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <a name="Structure"></a>Structuur van de gegevensset
Hallo **structuur** sectie is optioneel. Hallo-schema van Hallo gegevensset wordt gedefinieerd door dat een verzameling van namen en gegevenstypen van de kolommen bevat. U Hallo structuur sectie tooprovide type informatie die is gebruikt tooconvert typen en kaart kolommen uit Hallo bron toohello doel gebruiken. Hallo voorbeeld te volgen, Hallo gegevensset heeft drie kolommen: `slicetimestamp`, `projectname`, en `pageviews`. Zijn van het type String, String en Decimal, respectievelijk.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Elke kolom in het Hallo-structuur bevat Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| naam |Naam van het Hallo-kolom. |Ja |
| type |Het gegevenstype van kolom Hallo.  |Nee |
| Cultuur |. NET-gebaseerde cultuur toobe gebruikt wanneer Hallo type een .NET-type is: `Datetime` of `Datetimeoffset`. Hallo standaardwaarde is `en-us`. |Nee |
| Indeling |Indeling van tekenreeks toobe gebruikt wanneer Hallo type een .NET-type is: `Datetime` of `Datetimeoffset`. |Nee |

Hallo volgende richtlijnen te bepalen wanneer tooinclude structuur, gegevens en welke tooinclude in Hallo **structuur** sectie.

* **Voor gestructureerde gegevensbronnen**, Hallo structuur sectie alleen opgeven als u wilt toewijzen bronkolommen kolommen toosink en hun namen zijn niet dezelfde Hallo. Dit soort gegevensbron gestructureerde slaat schema en het type informatie samen met de Hallo gegevens zelf. Voorbeelden van gestructureerde gegevensbronnen zijn SQL Server, Oracle en Azure-tabel. 
  
    Als het type informatie is al beschikbaar voor gestructureerde gegevensbronnen, moet u type-informatie niet opnemen wanneer u Hallo structuur sectie opneemt.
* **Voor schema op lezen gegevensbronnen (specifiek Blob-opslag)**, kunt u toostore gegevens zonder schema of het type informatie met Hallo gegevens opslaan. Voor deze typen gegevensbronnen, structuur opnemen wanneer u wilt dat toomap bron kolommen toosink kolommen. Structuur wordt ook toevoegen wanneer Hallo gegevensset de invoer voor een kopieeractiviteit vormt en gegevenstypen van de bron-gegevensset geconverteerde toonative typen voor Hallo sink moet. 
    
    Data Factory ondersteunt Hallo waarden voor het ontwikkelen van type-informatie in de structuur te volgen: **Int16, Int32, Int64, Single, Double, Decimal, Byte [], Booleaanse waarde, String, Guid, Datetime, Datetimeoffset en Timespan**. Deze waarden zijn Common Language Specification (CLS)-compatibel zijn,. NET-type op basis van waarden.

Data Factory voert automatisch typeconversies bij het verplaatsen van gegevens uit een brongegevens tooa sink data store opslaan. 
  

## <a name="dataset-availability"></a>Beschikbaarheid van gegevensset
Hallo **beschikbaarheid** onderdeel in een gegevensset gedefinieerd Hallo verwerking venster (bijvoorbeeld elk uur, dagelijks of wekelijks) voor het Hallo-gegevensset. Zie voor meer informatie over windows activiteit [planning en uitvoering](data-factory-scheduling-and-execution.md).

Hallo beschikbaarheidssectie na bepaalt dat hello uitvoergegevensset wordt ofwel geproduceerd per uur, of het Hallo invoergegevensset per uur beschikbaar is:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Als Hallo pipeline Hallo begin- en eindtijden te volgen heeft:  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

Hallo uitvoergegevensset wordt geproduceerd per uur binnen Hallo pijplijn start- en eindtijd. Er zijn daarom vijf gegevensset gegevenssegmenten geproduceerd door deze pipeline, één voor elke activiteitvenster (12: 00 A.M. - 1 uur, 01: 00 - 2 uur, 2 uur - 3 uur, 3 uur - 4 AM, 4 uur - 5 uur). 

Hallo beschrijft volgende tabel eigenschappen die u in de sectie beschikbaarheid Hallo gebruiken kunt:

| Eigenschap | Beschrijving | Vereist | Standaard |
| --- | --- | --- | --- |
| frequency |Hiermee geeft u tijdseenheid Hallo voor gegevensset segment productie.<br/><br/><b>Ondersteunde frequentie</b>: minuut, uur, dag, Week, maand |Ja |N.v.t. |
| interval |Hiermee geeft u een vermenigvuldiger voor de frequentie.<br/><br/>"Frequentie x-interval" bepaalt hoe vaak hello segment wordt geproduceerd. Bijvoorbeeld, als u moet de gegevensset toobe gesegmenteerd op uurbasis hello, u stelt <b>frequentie</b> te<b>uur</b>, en <b>interval</b> te<b>1</b>.<br/><br/>Houd er rekening mee dat als u opgeeft **frequentie** als **minuut**, moet u Hallo interval toono kleiner is dan 15 instellen. |Ja |N.v.t. |
| stijl |Hiermee geeft u op of Hallo segment moet worden geproduceerd op Hallo begin of einde van hello-interval.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul>Als **frequentie** te is ingesteld,**maand**, en **stijl** te is ingesteld,**EndOfInterval**, op Hallo laatste dag van de maand Hallo segment wordt geproduceerd. Als **stijl** te is ingesteld,**StartOfInterval**, Hallo segment eerste dag van de maand op Hallo wordt geproduceerd.<br/><br/>Als **frequentie** te is ingesteld,**dag**, en **stijl** te is ingesteld,**EndOfInterval**, in Hallo afgelopen uur van de dag Hallo Hallo segment wordt geproduceerd.<br/><br/>Als **frequentie** te is ingesteld,**uur**, en **stijl** te is ingesteld,**EndOfInterval**, Hallo segment wordt geproduceerd achter Hallo Hallo uur. Voor een segment voor 1-2 uur periode Hallo Hallo segment geproduceerd om 2 uur. |Nee |EndOfInterval |
| anchorDateTime |Hallo absolute positie in de tijd die wordt gebruikt door Hallo scheduler toocompute gegevensset segmentgrenzen definieert. <br/><br/>Let op: als deze propoerty bevat de datumonderdelen die zijn meer granulair Hallo opgegeven frequentie, Hallo gedetailleerdere onderdelen worden genegeerd. Bijvoorbeeld, als hello **interval** is **per uur** (frequentie: uur en interval: 1), en Hallo **anchorDateTime** bevat **minuten en seconden**, vervolgens Hallo minuten en seconden delen van **anchorDateTime** worden genegeerd. |Nee |01/01/0001 |
| offset |TimeSpan door welke Hallo begin en einde van alle segmenten van de gegevensset zijn verplaatst. <br/><br/>Houd er rekening mee dat als beide **anchorDateTime** en **offset** zijn opgegeven, Hallo resultaat Hallo gecombineerd shift is. |Nee |N.v.t. |

### <a name="offset-example"></a>offset voorbeeld
Standaard dagelijks (`"frequency": "Day", "interval": 1`) segmenten beginnen bij 12: 00 A.M. (middernacht) Coordinated Universal Time (UTC). Als u Hallo start tijd toobe 06: 00 UTC-tijd in plaats daarvan wilt, stelt u Hallo zoals weergegeven in het volgende codefragment Hallo offset: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>Voorbeeld van anchorDateTime
In de Hallo voorbeeld te volgen, wordt de elke 23 uur in Hallo gegevensset wordt geproduceerd. Hallo eerste cirkelsegment begint bij Hallo tijd die is opgegeven door **anchorDateTime**, die is ingesteld te`2017-04-19T08:00:00` (UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>Voorbeeld van de offset/style
Hallo volgende gegevensset is maandelijks, en op Hallo wordt geproduceerd 3rd van elke maand om 8:00 AM (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <a name="Policy"></a>DataSet beleid
Hallo **beleid** sectie in de definitie van de gegevensset Hallo Hallo criteria bepaalt of Hallo-voorwaarde die Hallo segmenten van de gegevensset moet voldoen.

### <a name="validation-policies"></a>Van validatiebeleid
| De naam van beleid | Beschrijving | Te worden toegepast| Vereist | Standaard |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Valideert dat gegevens Hallo in **Azure Blob storage** voldoet aan de vereisten van de minimale grootte (in megabytes) Hallo. |Azure Blob Storage |Nee |N.v.t. |
| minimumRows |Valideert dat Hallo-gegevens in een **Azure SQL-database** of een **Azure-tabel** Hallo minimum aantal rijen bevat. |<ul><li>Azure SQL-database</li><li>Azure-tabel</li></ul> |Nee |N.v.t. |

#### <a name="examples"></a>Voorbeelden
**minimumSizeMB:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

**minimumRows:**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a>Externe gegevenssets
Externe gegevenssets zijn Hallo waarden die niet worden geproduceerd door een actieve pijplijn in Hallo data factory. Als Hallo dataset is gemarkeerd als **externe**, Hallo **ExternalData** beleid mogelijk gedefinieerde tooinfluence Hallo gedrag van Hallo gegevensset segment beschikbaarheid.

Tenzij een gegevensset wordt geproduceerd door Data Factory, moet dit worden gemarkeerd als **externe**. Deze instelling geldt doorgaans toohello input van de eerste activiteit in een pijplijn, tenzij activiteit of koppeling van de pijplijn wordt gebruikt.

| Naam | Beschrijving | Vereist | Standaardwaarde |
| --- | --- | --- | --- |
| dataDelay |Hallo tijd toodelay Hallo controleren op Hallo beschikbaarheid van de externe gegevens Hallo voor Hallo gegeven segment. Bijvoorbeeld, kunt u een controle per uur uitstellen met deze instelling.<br/><br/>Hallo-instelling is alleen van toepassing toohello huidige tijd.  Bijvoorbeeld, als het is nu om 13:00 uur en deze waarde 10 minuten is, Hallo validatie wordt gestart om 1:10 uur.<br/><br/>Houd er rekening mee dat deze instelling heeft geen invloed op segmenten in de afgelopen Hallo. Segmenten met **segment eindtijd** + **dataDelay** < **nu** zonder enige vertraging worden verwerkt.<br/><br/>Tijden groter is dan 23:59 uur moeten worden opgegeven met behulp van Hallo `day.hours:minutes:seconds` indeling. Gebruik geen 24:00:00 bijvoorbeeld toospecify 24 uur. Gebruik in plaats daarvan 1.00:00:00. Als u 24:00:00, wordt dit beschouwd als 24 dagen (24.00:00:00). Geef 1:04:00:00 voor 1 dag en 4 uur. |Nee |0 |
| retryInterval |Hallo wachttijd tussen een fout en Hallo opnieuw probeert. Deze instelling geldt toopresent tijd. Als de vorige probeer Hallo is mislukt, Hallo volgende probeer is na Hallo **retryInterval** periode. <br/><br/>Als het nu om 13:00 uur, beginnen we de eerste poging Hallo. Als Hallo duur toocomplete Hallo eerste validatiecontrole 1 minuut Hallo-bewerking is mislukt is, een nieuwe poging gedaan Hallo is 1:00 + 1 min (duur) + 1 min. (interval voor opnieuw proberen) = 1:02 PM. <br/><br/>Er is geen vertraging segmenten in de afgelopen Hallo. Hallo opnieuw gebeurt onmiddellijk. |Nee |00:01:00 (1 minuut) |
| retryTimeout |Hallo-out voor nieuwe pogingen.<br/><br/>Als deze eigenschap is ingesteld too10 minuten, Hallo validatie moet worden voltooid binnen 10 minuten. Als het duurt langer dan 10 minuten tooperform Hallo validatie, probeer Hallo time-out.<br/><br/>Als alle pogingen voor validatie time-out Hallo Hallo segment is gemarkeerd als **time-out**. |Nee |00:10:00 (10 minuten) |
| maximumRetry |Hallo aantal keren dat toocheck voor beschikbaarheid Hallo Hallo externe gegevens. Hallo maximaal toegestane waarde is 10. |Nee |3 |


## <a name="create-datasets"></a>Gegevenssets maken
U kunt de gegevenssets maken met behulp van een van deze hulpprogramma's of de SDK's: 

- De wizard Kopiëren 
- Azure Portal
- Visual Studio
- PowerShell
- Azure Resource Manager-sjabloon
- REST API
- .NET API

Zie Hallo-zelfstudies voor stapsgewijze instructies voor het maken van de pijplijnen en gegevenssets met behulp van een van deze hulpprogramma's of de SDK's te volgen:
 
- [Een pijplijn met een transformatieactiviteit voor gegevens bouwen](data-factory-build-your-first-pipeline.md)
- [Maken van een pijplijn met een activiteit van de verplaatsing van gegevens](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Nadat een pijplijn is gemaakt en geïmplementeerd, kunt u beheren en bewaken van uw pijplijnen met behulp van hello Azure portal-blades of Hallo-app voor bewaking en beheer. Zie de volgende onderwerpen voor stapsgewijze instructies Hallo: 

- [Bewaken en beheren van pijplijnen via Azure portal-blades](data-factory-monitor-manage-pipelines.md)
- [Bewaken en beheren van pijplijnen met Hallo-app voor bewaking en beheer](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a>Bereik gegevenssets
Kunt u gegevenssets die zich binnen het bereik tooa pijplijn met Hallo **gegevenssets** eigenschap. Deze gegevenssets kan alleen worden gebruikt door activiteiten binnen deze pipeline, niet door de activiteiten in andere pijplijnen. Hallo volgende voorbeeld definieert een pijplijn met twee gegevenssets (InputDataset rdc en OutputDataset rdc) toobe binnen Hallo pijplijn gebruikt.  

> [!IMPORTANT]
> Bereik gegevenssets worden alleen ondersteund voor eenmalige pijplijnen (waarbij **pipelineMode** te is ingesteld,**OneTime**). Zie [Onetime pijplijn](data-factory-create-pipelines.md#onetime-pipeline) voor meer informatie.
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a>Volgende stappen
- Zie voor meer informatie over pijplijnen [pijplijnen maken](data-factory-create-pipelines.md). 
- Zie voor meer informatie over hoe pijplijnen worden gepland en uitgevoerd, [planning en uitvoering in Azure Data Factory](data-factory-scheduling-and-execution.md). 
