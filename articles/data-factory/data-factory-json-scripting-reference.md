---
title: aaaAzure Data Factory - naslaginformatie voor JSON-scriptverwerking | Microsoft Docs
description: JSON-schema's biedt voor Data Factory-entiteiten.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a>Azure Data Factory - JSON-scriptverwerking verwijzing
Dit artikel bevat JSON-schema's en voorbeelden voor het definiëren van Azure Data Factory-entiteiten (pipeline, activiteit, gegevensset en gekoppelde service).  

## <a name="pipeline"></a>Pijplijn 
Hallo op hoog niveau structuur voor de definitie van een pijplijn is als volgt: 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Volgende tabel beschrijft de eigenschappen Hallo binnen Hallo pijplijn JSON-definitie:

| Eigenschap | Beschrijving | Vereist
-------- | ----------- | --------
| naam | Naam van het Hallo-pijplijn. Geef een naam die Hallo-actie die Hallo activiteit vertegenwoordigt of pijplijn geconfigureerde toodo is<br/><ul><li>Maximum aantal tekens: 260</li><li>Moet beginnen met een letter, cijfer of onderstrepingsteken (_)</li><li>Volgende tekens zijn niet toegestaan: '. ', '+ ','?', '/', '< ',' >', ' * ', "%", "&", ":","\\'</li></ul> |Ja |
| description |Beschrijving van wat Hallo activiteit of pijplijn wordt gebruikt voor | Nee |
| activities | Bevat een lijst van activiteiten. | Ja |
| start |Datum-begintijd voor de Hallo pijplijn. Moet in [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601). Bijvoorbeeld: 2014-10-14T16:32:41. <br/><br/>Het is mogelijk toospecify een plaatselijke tijd, bijvoorbeeld een geschatte tijd. Hier volgt een voorbeeld: `2016-02-27T06:00:00**-05:00`, namelijk 6 AM EST.<br/><br/>Hallo begin- en eigenschappen samen actieve periode opgeven voor Hallo pijplijn. Uitvoer segmenten worden alleen gemaakt met deze actieve periode. |Nee<br/><br/>Als u een waarde voor Hallo end-eigenschap opgeeft, moet u de waarde voor Hallo begineigenschap opgeven.<br/><br/>Hallo kunnen begin- en eindtijden niet leeg toocreate een pijplijn. U moet beide waarden opgeven tooset een actieve periode voor Hallo pijplijn toorun. Als u geen begin- en eindtijden opgeeft wanneer u een pijplijn maakt, kunt u deze instellen met behulp van de cmdlet Set-AzureRmDataFactoryPipelineActivePeriod hello later. |
| Einde |Einddatum en-tijd voor de Hallo pijplijn. Als in de ISO-indeling moet worden opgegeven. Bijvoorbeeld: 2014-10-14T17:32:41 <br/><br/>Het is mogelijk toospecify een plaatselijke tijd, bijvoorbeeld een geschatte tijd. Hier volgt een voorbeeld: `2016-02-27T06:00:00**-05:00`, namelijk 6 AM EST.<br/><br/>9999-09-09 toorun Hallo pijplijn voor onbepaalde tijd opgeven als waarde voor end-eigenschap Hallo Hallo. |Nee <br/><br/>Als u een waarde voor Hallo start eigenschap opgeeft, moet u de waarde voor end-eigenschap Hallo opgeven.<br/><br/>Zie de opmerkingen voor Hallo **start** eigenschap. |
| isPaused |Als de set tootrue Hallo pijplijn kan niet worden uitgevoerd. Standaardwaarde = false. U kunt deze eigenschap tooenable gebruiken of uitschakelen. |Nee |
| pipelineMode |Hallo-methode voor het plannen wordt uitgevoerd voor de Hallo pijplijn. Toegestane waarden zijn: (standaard), gepland eenmalige.<br/><br/>De geplande' geeft aan dat Hallo-pijplijn wordt uitgevoerd op een opgegeven tijdsinterval volgens tooits actieve periode (begin- en -tijd). 'Eenmalige' geeft aan dat Hallo-pijplijn wordt slechts één keer uitgevoerd. Eenmalige pijplijnen eenmaal gemaakt kunnen niet worden gewijzigd/bijgewerkt op dit moment. Zie [Onetime pijplijn](data-factory-create-pipelines.md#onetime-pipeline) voor meer informatie over het instellen van eenmalige. |Nee |
| expirationTime |Tijdsduur na het maken voor welke Hallo pijplijn is geldig en moet worden ingericht. Als er geen elk actief is, is mislukt, of in behandeling wordt uitgevoerd, Hallo pijplijn wordt automatisch verwijderd wanneer het Hallo-verlooptijd is bereikt. |Nee |


## <a name="activity"></a>Activiteit 
Hallo op hoog niveau structuur voor een activiteit in de definitie van een pijplijn (activiteiten element) is als volgt:

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

Na de tabel wordt beschreven Hallo eigenschappen binnen Hallo activiteit JSON-definitie:

| Label | Beschrijving | Vereist |
| --- | --- | --- |
| naam |Naam van Hallo-activiteit. Geef een naam die Hallo-actie die Hallo activiteit vertegenwoordigt toodo geconfigureerd<br/><ul><li>Maximum aantal tekens: 260</li><li>Moet beginnen met een letter, cijfer of onderstrepingsteken (_)</li><li>Volgende tekens zijn niet toegestaan: '. ', '+ ','?', '/', '< ',' >', ' * ', "%", "&", ":","\\'</li></ul> |Ja |
| description |Tekst die beschrijft wat Hallo-activiteit wordt gebruikt voor. |Ja |
| type |Hiermee geeft u Hallo Hallo-activiteit. Zie Hallo [GEGEVENSARCHIEVEN](#data-stores) en [activiteiten voor GEGEVENSTRANSFORMATIE](#data-transformation-activities) secties voor verschillende soorten activiteiten. |Ja |
| Invoer |Invoertabellen die worden gebruikt door Hallo-activiteit<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Ja |
| uitvoer |Uitvoergegevens tabellen gebruikt door Hallo-activiteit.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |Ja |
| linkedServiceName |Naam van Hallo gekoppelde service die wordt gebruikt door het Hallo-activiteit. <br/><br/>Een activiteit kan vereisen dat u opgeeft Hallo gekoppelde service die is gekoppeld aan toohello vereist compute-omgeving. |Ja voor HDInsight-activiteiten, Azure Machine Learning-activiteiten en activiteit opgeslagen Procedure. <br/><br/>Nee voor alle andere |
| typeProperties |Eigenschappen in Hallo typeProperties sectie, is afhankelijk van type Hallo-activiteit. |Nee |
| policy |Beleidsregels die invloed hebben op Hallo run-time gedrag van Hallo-activiteit. Als deze niet is opgegeven, worden de standaardbeleidsregels gebruikt. |Nee |
| Scheduler |'scheduler'-eigenschap is gebruikte toodefine gewenst schema voor het Hallo-activiteit. Bijbehorende subeigenschappen zijn hetzelfde als de waarden in Hallo HALLO hallo [eigenschap beschikbaarheid in een dataset](data-factory-create-datasets.md#dataset-availability). |Nee |

### <a name="policies"></a>Beleidsregels
Beleid geldt voor Hallo run-time gedrag van een activiteit specifiek wanneer Hallo segment van een tabel wordt verwerkt. Hallo volgende tabel biedt details Hallo.

| Eigenschap | Toegestane waarden | Standaardwaarde | Beschrijving |
| --- | --- | --- | --- |
| Gelijktijdigheid van taken |Geheel getal <br/><br/>De maximale waarde: 10 |1 |Het aantal gelijktijdige uitvoeringen van Hallo-activiteit.<br/><br/>Bepaalt de Hallo aantal parallelle activiteit uitvoeringen die kunnen ontstaan op verschillende segmenten. Bijvoorbeeld, als een activiteit toogo via moet sneller een groot aantal beschikbare gegevens, een grotere waarde voor gelijktijdigheid Hallo gegevensverwerking. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |Hiermee wordt bepaald Hallo ordening van gegevenssegmenten dat wordt verwerkt.<br/><br/>Als er 2 segmenten (één gebeurt om 4 uur en 17: 00 uur een andere één voor één) en beide zijn in behandeling kan worden uitgevoerd. Als u Hallo executionPriorityOrder toobe NewestFirst instelt, wordt eerst segment hello om 17.00 verwerkt. Op dezelfde manier als u Hallo executionPriorityORder toobe OldestFIrst hebt ingesteld, klikt u vervolgens Hallo segment om 4 uur is verwerkt. |
| retry |Geheel getal<br/><br/>De maximale waarde is 10 |0 |Aantal nieuwe pogingen voordat de gegevensverwerking Hallo voor Hallo segment wordt als mislukt gemarkeerd. Activiteit is uitgevoerd voor een gegevenssegment wordt opnieuw geprobeerd up toohello opgegeven aantal nieuwe pogingen. Hallo nieuwe poging wordt gedaan zo snel mogelijk na een storing Hallo. |
| timeout |TimeSpan |00:00:00 |Time-out voor Hallo-activiteit. Voorbeeld: 00:10:00 (impliceert time-out 10 minuten)<br/><br/>Als een waarde niet opgegeven is of 0 is, is Hallo time-out oneindig.<br/><br/>Hallo gegevensverwerking tijd op een segment overschrijdt de time-outwaarde Hallo, deze wordt geannuleerd als Hallo-systeem probeert tooretry Hallo verwerking. Hallo aantal nieuwe pogingen, is afhankelijk van de eigenschap retry Hallo. Wanneer een time-out optreedt, Hallo status tooTimedOut ingesteld. |
| Vertraging |TimeSpan |00:00:00 |Geef Hallo vertraging optreden voordat de verwerking van Hallo segment wordt gestart.<br/><br/>Hallo-uitvoering van de activiteit voor een gegevenssegment wordt gestart nadat Hallo vertraging is verstreken Hallo uitvoeringstijd verwacht.<br/><br/>Voorbeeld: 00:10:00 (betekent vertraging van 10 minuten) |
| longRetry |Geheel getal<br/><br/>De maximale waarde: 10 |1 |Hallo aantal lang pogingen proberen voordat Hallo segment uitvoering is mislukt.<br/><br/>longRetry pogingen door longRetryInterval gelijkmatig verdeeld. Als u een tijd tussen pogingen toospecify moet, dus longRetry gebruiken. Als zowel de nieuwe pogingen en de longRetry worden opgegeven, elke poging longRetry bevat nieuwe pogingen en Hallo kunt u het maximale aantal pogingen is opnieuw * longRetry.<br/><br/>Bijvoorbeeld, als er Hallo instellingen in Hallo activiteit-beleid te volgen:<br/>Probeer: 3<br/>longRetry: 2<br/>longRetryInterval: 01:00:00 uur<br/><br/>Wordt ervan uitgegaan dat er is slechts één segment tooexecute (status Waiting) en Hallo activiteit is uitgevoerd elke keer mislukt. Er zou worden in eerste instantie 3 opeenvolgende uitvoering pogingen. Na elke poging zijn Hallo segment status probeer het opnieuw. Nadat de eerste 3 pogingen hebben bekeken, zou Hallo segment status LongRetry zijn.<br/><br/>Na een uur (dat wil zeggen, de longRetryInteval waarde), zou er een andere set 3 opeenvolgende uitvoering pogingen. Hallo segment status zou niet hierna is en geen pogingen meer zou worden uitgevoerd. Daarom is algemene 6 geprobeerd.<br/><br/>Als een uitvoering is geslaagd, Hallo segment de status gereed zijn en er worden geen pogingen meer geprobeerd.<br/><br/>longRetry kan worden gebruikt in situaties waarbij afhankelijke gegevens aankomen op niet-deterministische tijdstippen of hello algehele omgeving flaky onder welke gegevensverwerking plaatsvindt. In dergelijke gevallen niet pogingen doen achter elkaar kunt en uitvoer doet na een tijd resulteert in het Hallo-interval gewenst.<br/><br/>Waarschuwing: geen hoge waarden voor de longRetry of longRetryInterval instelt. Hogere waarden dat normaal gesproken andere al problemen. |
| longRetryInterval |TimeSpan |00:00:00 |Hallo vertraging tussen pogingen lang |

### <a name="typeproperties-section"></a>typeProperties sectie
Hallo typeProperties sectie verschilt voor elke activiteit. Activiteiten voor gegevenstransformatie hebben zojuist Hallo-type-eigenschappen. Zie [activiteiten voor GEGEVENSTRANSFORMATIE](#data-transformation-activities) sectie in dit artikel voor JSON-voorbeelden die activiteiten voor gegevenstransformatie in een pijplijn definiëren. 

**Kopieeractiviteit** heeft twee subsecties in Hallo typeProperties sectie: **bron** en **sink**. Zie [GEGEVENSARCHIEVEN](#data-stores) sectie in dit artikel voor JSON-voorbeelden die tonen hoe een data toouse opslaan als een bron-en/of sink. 

### <a name="sample-copy-pipeline"></a>Voorbeeld van kopieerpijplijn
In het Hallo-voorbeeldpijplijn te volgen, wordt een activiteit van het type **kopie** in Hallo **activiteiten** sectie. In dit voorbeeld Hallo [Kopieeractiviteit](data-factory-data-movement-activities.md) gegevens worden gekopieerd van een Azure Blob storage tooan Azure SQL database. 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Houd er rekening mee Hallo volgende punten:

* In Hallo gedeelte activiteiten is er slechts één activiteit waarvan **type** te is ingesteld,**kopie**.
* Invoer voor Hallo-activiteit is ingesteld, te**InputDataset** en de uitvoer voor Hallo activiteit te is ingesteld**OutputDataset**.
* In Hallo **typeProperties** sectie **BlobSource** is opgegeven als Hallo brontype en **SqlSink** is opgegeven als Hallo sink-type.

Zie [GEGEVENSARCHIEVEN](#data-stores) sectie in dit artikel voor JSON-voorbeelden die tonen hoe een data toouse opslaan als een bron-en/of sink.    

Zie voor een volledige procedure voor het maken van deze pipeline [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="sample-transformation-pipeline"></a>Voorbeeld van pijplijn voor transformatie
In het Hallo-voorbeeldpijplijn te volgen, wordt een activiteit van het type **HDInsightHive** in Hallo **activiteiten** sectie. In dit voorbeeld Hallo [HDInsight Hive-activiteit](data-factory-hive-activity.md) transformeert u gegevens uit een Azure Blob-opslag door het uitvoeren van een Hive-scriptbestand op een Azure HDInsight Hadoop-cluster. 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

Houd er rekening mee Hallo volgende punten: 

* In Hallo gedeelte activiteiten is er slechts één activiteit waarvan **type** te is ingesteld,**HDInsightHive**.
* Hallo Hive-scriptbestand **partitionweblogs.hql**, wordt opgeslagen in hello Azure storage-account (Hallo door scriptLinkedService met de opgegeven **AzureStorageLinkedService**), en in  **script** map in container Hallo **adfgetstarted**.
* Hallo **definieert** sectie is gebruikte toospecify Hallo runtime-instellingen die toohello hive-script worden doorgegeven als Hive-configuratiewaarden (bijvoorbeeld `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Zie [activiteiten voor GEGEVENSTRANSFORMATIE](#data-transformation-activities) sectie in dit artikel voor JSON-voorbeelden die activiteiten voor gegevenstransformatie in een pijplijn definiëren.

Zie voor een volledige procedure voor het maken van deze pipeline [zelfstudie: bouwen van uw eerste pijplijn tooprocess gegevens met Hadoop-cluster](data-factory-build-your-first-pipeline.md). 

## <a name="linked-service"></a>Gekoppelde service
Hallo op hoog niveau structuur voor de definitie van een gekoppelde service is als volgt:

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

Na de tabel wordt beschreven Hallo eigenschappen binnen Hallo activiteit JSON-definitie:

| Eigenschap | Beschrijving | Vereist |
| -------- | ----------- | -------- | 
| naam | Naam van Hallo gekoppelde service. | Ja | 
| Eigenschappen - type | Hallo type gekoppelde service. Bijvoorbeeld: Azure Storage, Azure SQL Database. |
| typeProperties | Hallo typeProperties sectie bevat de elementen die zijn verschillend voor elke gegevensopslag of compute-omgeving. Zie [gegevensarchieven](#datastores) sectie voor alle Hallo gegevensarchief gekoppelde services en [omgevingen compute](#compute-environments) voor alle Hallo compute gekoppelde services |   

## <a name="dataset"></a>Gegevensset 
Een gegevensset in Azure Data Factory is als volgt gedefinieerd:

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
| naam | Naam van het Hallo-gegevensset. Zie [Azure Data Factory - naamgevingsregels](data-factory-naming-rules.md) voor naamgevingsregels. |Ja |N.v.t. |
| type | Type Hallo gegevensset. Geef een Hallo die worden ondersteund door Azure Data Factory (bijvoorbeeld: AzureBlob, AzureSqlTable). Zie [GEGEVENSARCHIEVEN](#data-stores) voor alle opgeslagen gegevens en de gegevensset die worden ondersteund door de Data Factory Hallo sectie. | 
| structuur | Schema van Hallo dataset. Het bevat kolommen, de typen, enz. | Nee |N.v.t. |
| typeProperties | Eigenschappen die overeenkomen toohello type geselecteerd. Zie [GEGEVENSARCHIEVEN](#data-stores) sectie voor de ondersteunde typen en hun eigenschappen. |Ja |N.v.t. |
| external | Booleaanse waarde vlag toospecify of een gegevensset wordt expliciet geproduceerd door een data factory-pijplijn of niet. |Nee |ONWAAR |
| availability | Hiermee definieert u Hallo venster of Hallo segmentering model voor Hallo gegevensset productie te verwerken. Zie voor meer informatie op Hallo gegevensset segmentering model [planning en uitvoering](data-factory-scheduling-and-execution.md) artikel. |Ja |N.v.t. |
| policy |Definieert Hallo criteria of Hallo voorwaarde waaraan Hallo gegevensset segmenten moeten voldoen. <br/><br/>Zie voor meer informatie [gegevensset beleid](#Policy) sectie. |Nee |N.v.t. |

Elke kolom in Hallo **structuur** sectie bevat Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| naam |Naam van het Hallo-kolom. |Ja |
| type |Het gegevenstype van kolom Hallo.  |Nee |
| Cultuur |.NET-gebaseerde cultuur toobe gebruikt bij het type is opgegeven en .NET-type `Datetime` of `Datetimeoffset`. Standaard is `en-us`. |Nee |
| Indeling |Indeling van tekenreeks toobe gebruikt bij het type is opgegeven en .NET-type `Datetime` of `Datetimeoffset`. |Nee |

Hallo voorbeeld te volgen, Hallo gegevensset heeft drie kolommen `slicetimestamp`, `projectname`, en `pageviews` en ze zijn van het type: String, String en Decimal respectievelijk.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Hallo volgende tabel beschrijft eigenschappen die u in Hallo gebruiken kunt **beschikbaarheid** sectie:

| Eigenschap | Beschrijving | Vereist | Standaard |
| --- | --- | --- | --- |
| frequency |Hiermee geeft u tijdseenheid Hallo voor gegevensset segment productie.<br/><br/><b>Ondersteunde frequentie</b>: minuut, uur, dag, Week, maand |Ja |N.v.t. |
| interval |Hiermee geeft u een vermenigvuldiger voor de frequentie<br/><br/>"Frequentie x-interval" bepaalt hoe vaak hello segment wordt geproduceerd.<br/><br/>Als u de gegevensset toobe gesegmenteerd op uurbasis moet hello, stelt u <b>frequentie</b> te<b>uur</b>, en <b>interval</b> te<b>1</b>.<br/><br/><b>Opmerking</b>: als u de frequentie als minuut opgeeft, raden wij aan dat u Hallo interval toono kleiner is dan 15 |Ja |N.v.t. |
| stijl |Hiermee geeft u op of Hallo segment Hallo beginnen of eindigen van hello-interval moet worden geproduceerd.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Als de frequentie tooMonth is ingesteld en stijl tooEndOfInterval is ingesteld, wordt Hallo segment op Hallo laatste dag van de maand geproduceerd. Als Hallo stijl is ingesteld tooStartOfInterval, wordt Hallo segment geproduceerd op Hallo eerste dag van de maand.<br/><br/>Als frequentie tooDay is ingesteld en stijl tooEndOfInterval is ingesteld, wordt in het afgelopen uur van de dag Hallo HALLO hallo segment geproduceerd.<br/><br/>Als frequentie tooHour is ingesteld en stijl tooEndOfInterval is ingesteld, worden Hallo segment wordt geproduceerd achter Hallo Hallo uur. Voor een segment 1-2 uur gedurende Hallo segment geproduceerd om 2 uur. |Nee |EndOfInterval |
| anchorDateTime |Hiermee definieert u Hallo absolute positie in de tijd die wordt gebruikt door de grenzen van scheduler toocompute gegevensset segment. <br/><br/><b>Opmerking</b>: als Hallo AnchorDateTime bevat de datumonderdelen die meer gedetailleerd dan Hallo frequentie zijn dan hello gedetailleerdere onderdelen worden genegeerd. <br/><br/>Bijvoorbeeld, als hello <b>interval</b> is <b>per uur</b> (frequentie: uur en interval: 1) en Hallo <b>AnchorDateTime</b> bevat <b>minuten en seconden</b>vervolgens Hallo <b>minuten en seconden</b> delen van Hallo AnchorDateTime worden genegeerd. |Nee |01/01/0001 |
| offset |TimeSpan door welke Hallo begin en einde van alle segmenten van de gegevensset zijn verplaatst. <br/><br/><b>Opmerking</b>: als zowel anchorDateTime als offset worden opgegeven, Hallo resultaat Hallo gecombineerd shift is. |Nee |N.v.t. |

Hallo beschikbaarheidssectie na geeft aan dat uitvoergegevensset Hallo is geproduceerd per uur (of) invoer gegevensset per uur beschikbaar is:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Hallo **beleid** sectie in de definitie van gegevensset definieert Hallo criteria of Hallo-voorwaarde die Hallo segmenten van de gegevensset moet voldoen.

| De naam van beleid | Beschrijving | Te worden toegepast| Vereist | Standaard |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Valideert dat Hallo-gegevens in een **Azure blob** voldoet aan de vereisten van de minimale grootte (in megabytes) Hallo. |Azure Blob |Nee |N.v.t. |
| minimumRows |Valideert dat Hallo-gegevens in een **Azure SQL-database** of een **Azure-tabel** Hallo minimum aantal rijen bevat. |<ul><li>Azure SQL Database</li><li>Azure-tabel</li></ul> |Nee |N.v.t. |

**Voorbeeld:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

Tenzij een gegevensset wordt geproduceerd door Azure Data Factory, moet dit worden gemarkeerd als **externe**. Deze instelling geldt doorgaans toohello input van de eerste activiteit in een pijplijn tenzij activiteit of koppeling van de pijplijn wordt gebruikt.

| Naam | Beschrijving | Vereist | Standaardwaarde |
| --- | --- | --- | --- |
| dataDelay |Controle van de tijd toodelay Hallo Hallo beschikbaarheid van externe gegevens voor het opgegeven segment Hallo Hallo. Bijvoorbeeld, als Hallo gegevens elk uur beschikbaar is, Hallo selectievakje toosee Hallo externe gegevens beschikbaar is en het bijbehorende Hallo segment kan gereed oplopen met behulp van dataDelay.<br/><br/>Is alleen van toepassing toohello huidige tijd.  Bijvoorbeeld, als het is nu om 13:00 uur en deze waarde 10 minuten is, Hallo validatie wordt gestart om 1:10 uur.<br/><br/>Deze instelling heeft geen invloed op de segmenten in de afgelopen hello (segmenten met segment eindtijd + dataDelay < nu) zonder enige vertraging worden verwerkt.<br/><br/>Tijd groter is dan 23:59 uur moeten toospecified met Hallo `day.hours:minutes:seconds` indeling. Bijvoorbeeld: toospecify 24 uur niet gebruiken 24:00:00; Gebruik in plaats daarvan 1.00:00:00. Als u 24:00:00, wordt dit beschouwd als 24 dagen (24.00:00:00). Geef 1:04:00:00 voor 1 dag en 4 uur. |Nee |0 |
| retryInterval |Hallo wachttijd tussen een fout en Hallo volgende nieuwe poging. Als een try mislukt, is het volgende proberen Hallo na retryInterval. <br/><br/>Als het nu om 13:00 uur, beginnen we de eerste poging Hallo. Als Hallo duur toocomplete Hallo eerste validatiecontrole 1 minuut Hallo-bewerking is mislukt is, een nieuwe poging gedaan Hallo is 1:00 + 1 min (duur) + 1 min. (interval voor opnieuw proberen) = 1:02 PM. <br/><br/>Er is geen vertraging segmenten in de afgelopen Hallo. Hallo opnieuw gebeurt onmiddellijk. |Nee |00:01:00 (1 minuut) |
| retryTimeout |Hallo-out voor nieuwe pogingen.<br/><br/>Als deze eigenschap is ingesteld too10 minuten, Hallo validatie behoeften toobe voltooid binnen 10 minuten. Als het duurt langer dan 10 minuten tooperform Hallo validatie, probeer Hallo time-out.<br/><br/>Als alle pogingen voor Hallo validatie een time-out optreedt, wordt als een time-out opgetreden bij Hallo segment gemarkeerd. |Nee |00:10:00 (10 minuten) |
| maximumRetry |Aantal keren dat toocheck voor beschikbaarheid Hallo Hallo externe gegevens. Hallo toegestane maximale waarde is 10. |Nee |3 |


## <a name="data-stores"></a>GEGEVENSOPSLAG
Hallo [gekoppelde service](#linked-service) beschrijvingen van de opgegeven sectie voor de JSON-elementen die algemene tooall typen gekoppelde services zijn. Deze sectie bevat informatie over de JSON-elementen die specifiek tooeach gegevensarchief.

Hallo [gegevensset](#dataset) beschrijvingen van de opgegeven sectie voor de JSON-elementen die algemene tooall typen gegevenssets zijn. Deze sectie bevat informatie over de JSON-elementen die specifiek tooeach gegevensarchief.

Hallo [activiteit](#activity) beschrijvingen van de opgegeven sectie voor de JSON-elementen die algemene tooall soorten activiteiten zijn. Deze sectie bevat informatie over de JSON-elementen die specifiek tooeach gegevensarchief wanneer deze wordt gebruikt als een bron/sink in een kopieeractiviteit.  

Klik op de koppeling Hallo voor Hallo store u geïnteresseerd bent in toosee Hallo JSON-schema voor de gekoppelde service, gegevensset en bron/sink voor de kopieeractiviteit Hallo Hallo.

| Category | Gegevensarchief 
|:--- |:--- |
| **Azure** |[Azure Blob Storage](#azure-blob-storage) |
| &nbsp; |[Azure Data Lake Store](#azure-datalake-store) |
| &nbsp; |[Azure Cosmos DB](#azure-cosmos-db) |
| &nbsp; |[Azure SQL Database](#azure-sql-database) |
| &nbsp; |[Azure SQL Data Warehouse](#azure-sql-data-warehouse) |
| &nbsp; |[Azure Search](#azure-search) |
| &nbsp; |[Azure Table storage](#azure-table-storage) |
| **Databases** |[Amazon Redshift](#amazon-redshift) |
| &nbsp; |[IBM DB2](#ibm-db2) |
| &nbsp; |[MySQL](#mysql) |
| &nbsp; |[Oracle](#oracle) |
| &nbsp; |[PostgreSQL](#postgresql) |
| &nbsp; |[SAP Business Warehouse](#sap-business-warehouse) |
| &nbsp; |[SAP HANA](#sap-hana) |
| &nbsp; |[SQL Server](#sql-server) |
| &nbsp; |[Sybase](#sybase) |
| &nbsp; |[Teradata](#teradata) |
| **NoSQL** |[Cassandra](#cassandra) |
| &nbsp; |[MongoDB](#mongodb) |
| **File** |[Amazon S3](#amazon-s3) |
| &nbsp; |[Bestandssysteem](#file-system) |
| &nbsp; |[FTP](#ftp) |
| &nbsp; |[HDFS](#hdfs) |
| &nbsp; |[SFTP](#sftp) |
| **Andere** |[HTTP](#http) |
| &nbsp; |[OData](#odata) |
| &nbsp; |[ODBC](#odbc) |
| &nbsp; |[Salesforce](#salesforce) |
| &nbsp; |[Web-tabel](#web-table) |

## <a name="azure-blob-storage"></a>Azure Blob Storage

### <a name="linked-service"></a>Gekoppelde service
Er zijn twee soorten gekoppelde services: gekoppelde Azure Storage-service en de gekoppelde Azure Storage SAS-service.

#### <a name="azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service
toolink uw Azure storage-account tooa data factory met behulp van Hallo **accountsleutel**, maak een gekoppelde Azure Storage-service. toodefine een Azure Storage gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureStorage**. U kunt vervolgens opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| connectionString |Geef informatie tooconnect tooAzure opslag voor de eigenschap connectionString Hallo nodig. |Ja |

##### <a name="example"></a>Voorbeeld  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a>Gekoppelde Azure Storage SAS-Service
Hallo SAS van Azure Storage gekoppelde service, kunt u een Azure Storage-Account tooan Azure data factory toolink met behulp van een Shared Access Signature (SAS). Het biedt Hallo data factory toegang beperkt/tijdsgebonden tooall/specifieke bronnen (blobcontainer) / in Hallo-opslag. toolink uw Azure storage-account tooa data factory met behulp van Shared Access Signature maken van een SAS van Azure Storage gekoppelde service. een Azure Storage-SAS toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureStorageSas**. U kunt vervolgens opgeven na eigenschappen in Hallo **typeProperties** sectie:   

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| sasUri |Geef de Shared Access Signature URI toohello Azure Storage-resources zoals blob-container of tabel. |Ja |

##### <a name="example"></a>Voorbeeld

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Zie voor meer informatie over deze gekoppelde services, [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een Azure Blob-gegevensset set Hallo **type** van Hallo gegevensset te**AzureBlob**. Geef vervolgens de volgende specifieke eigenschappen van de Azure-Blob in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| folderPath |Pad toohello container en map in Hallo blob-opslag. Voorbeeld: myblobcontainer\myblobfolder\ |Ja |
| fileName |De naam van Hallo blob. Bestandsnaam is optioneel en is hoofdlettergevoelig.<br/><br/>Als u een bestandsnaam, Hallo activiteit (inclusief kopiëren) werkt opgeeft op Hallo specifieke Blob.<br/><br/>Bestandsnaam is opgegeven, bevat kopiëren alle Blobs Hallo folderPath voor invoergegevensset.<br/><br/>Wanneer fileName niet voor een uitvoergegevensset opgegeven is, Hallo-naam van Hallo gegenereerd bestand in Hallo volgt deze indeling zou worden: gegevens. <Guid>.txt (voorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nee |
| partitionedBy |partitionedBy is een optionele eigenschap. Kunt u deze toospecify een dynamische folderPath en de bestandsnaam voor de reeksgegevens. FolderPath kan bijvoorbeeld parameters worden gebruikt voor elk uur van gegevens. |Nee |
| Indeling | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set Hallo **type** eigenschap onder indeling tooone van deze waarden. Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. <br><br> Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan. |Nee |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**. Ondersteunde niveaus: **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |

#### <a name="example"></a>Voorbeeld

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


Zie voor meer informatie [Azure Blob-connector](data-factory-azure-blob-connector.md#dataset-properties) artikel.

### <a name="blobsource-in-copy-activity"></a>BlobSource in de kopieerbewerking
Als u gegevens uit een Azure Blob Storage kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**BlobSource**, en opgeven na eigenschappen in Hallo ** bron ** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| Recursieve |Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo. |True (standaardwaarde), False |Nee |

#### <a name="example-blobsource"></a>Voorbeeld: BlobSource **
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a>BlobSink in de kopieerbewerking
Als u gegevens tooan Azure Blob-opslag kopiëren wilt, stelt u Hallo **type sink** Hallo kopieeractiviteit te**BlobSink**, en opgeven na eigenschappen in Hallo **sink** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| copyBehavior |Hallo kopie gedrag definieert wanneer Hallo bron BlobSource of bestandssysteem. |<b>PreserveHierarchy</b>: gehandhaafd Hallo bestandshiërarchie in de doelmap Hallo. Hallo relatieve pad van de bestandsmap toosource bron is identiek toohello relatieve pad van de bestandsmap tootarget doel.<br/><br/><b>FlattenHierarchy</b>: alle bestanden uit de bronmap Hallo zijn in Hallo eerst niveau van de doelmap. Hallo doelbestanden hebben automatisch gegenereerde naam. <br/><br/><b>MergeFiles (standaard):</b> alle bestanden uit map Hallo-tooone bronbestand worden samengevoegd. Als Hallo bestand/Blob-naam wordt opgegeven, zou Hallo Samengevoegde bestandsnaam Hallo opgegeven name; zijn anders zou worden automatisch gegenereerde naam. |Nee |

#### <a name="example-blobsink"></a>Voorbeeld: BlobSink

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Zie voor meer informatie [Azure Blob-connector](data-factory-azure-blob-connector.md#copy-activity-properties) artikel. 

## <a name="azure-data-lake-store"></a>Azure Data Lake Store

### <a name="linked-service"></a>Gekoppelde service
een Azure Data Lake Store gekoppelde service toodefine, Hallo set Hallo type gekoppelde service te**AzureDataLakeStore**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| type | Hallo type eigenschap moet worden ingesteld op: **AzureDataLakeStore** | Ja |
| dataLakeStoreUri | Geef informatie op over hello Azure Data Lake Store-account. Het is in de volgende indeling Hallo: `https://[accountname].azuredatalakestore.net/webhdfs/v1` of `adl://[accountname].azuredatalakestore.net/`. | Ja |
| subscriptionId | Azure-abonnement Id toowhich Data Lake Store hoort. | Vereist voor sink |
| resourceGroupName | Azure resource group name toowhich Data Lake Store hoort. | Vereist voor sink |
| servicePrincipalId | Geef Hallo van client-id op. | Ja (voor verificatie voor service-principal) |
| servicePrincipalKey | De sleutel van de toepassing hello opgeven. | Ja (voor verificatie voor service-principal) |
| Tenant | Geef informatie op Hallo tenant (domain name of tenant-ID) in uw toepassing zich bevindt. U kunt deze ophalen door zwevende Hallo muis in Hallo rechterbovenhoek Hallo Azure-portal. | Ja (voor verificatie voor service-principal) |
| Autorisatie | Klik op **autoriseren** knop in Hallo **Data Factory-Editor** en voer uw referenties waarmee eigenschap toothis Hallo automatisch gegenereerde autorisatie-URL worden toegewezen. | Ja (voor verificatie van gebruikersreferenties)|
| sessie-id | OAuth-sessie-id van Hallo OAuth-autorisatie-sessie. Elke sessie-id is uniek en kan slechts eenmaal worden gebruikt. Deze instelling wordt automatisch gegenereerd wanneer u Data Factory-Editor. | Ja (voor verificatie van gebruikersreferenties) |

#### <a name="example-using-service-principal-authentication"></a>Voorbeeld: met behulp van verificatie van de service-principal
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a>Voorbeeld: met behulp van verificatie van gebruikersreferenties
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

Zie voor meer informatie [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset Azure Data Lake Store set Hallo **type** van Hallo gegevensset te**AzureDataLakeStore**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties**sectie: 

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| folderPath |Pad toohello container en map in hello Azure Data Lake opslaan. |Ja |
| fileName |Naam van bestand Hallo in hello Azure Data Lake store. Bestandsnaam is optioneel en is hoofdlettergevoelig. <br/><br/>Als u een filename opgeeft, werkt Hallo activiteit (inclusief kopiëren) op Hallo specifiek bestand.<br/><br/>Bestandsnaam is opgegeven, bevat kopiëren alle bestanden in Hallo folderPath voor invoergegevensset.<br/><br/>Wanneer fileName niet voor een uitvoergegevensset opgegeven is, Hallo-naam van Hallo gegenereerd bestand in Hallo volgt deze indeling zou worden: gegevens. <Guid>.txt (voorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nee |
| partitionedBy |partitionedBy is een optionele eigenschap. Kunt u deze toospecify een dynamische folderPath en de bestandsnaam voor de reeksgegevens. FolderPath kan bijvoorbeeld parameters worden gebruikt voor elk uur van gegevens. |Nee |
| Indeling | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set Hallo **type** eigenschap onder indeling tooone van deze waarden. Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. <br><br> Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan. |Nee |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**. Ondersteunde niveaus: **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |

#### <a name="example"></a>Voorbeeld
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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

Zie voor meer informatie [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) artikel. 

### <a name="azure-data-lake-store-source-in-copy-activity"></a>Azure Data Lake Store-bron in de kopieerbewerking
Als u gegevens uit een Azure Data Lake Store kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**AzureDataLakeStoreSource**, en opgeven na eigenschappen in Hallo **bron**  sectie:

**AzureDataLakeStoreSource** ondersteunt de volgende eigenschappen Hallo **typeProperties** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| Recursieve |Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo. |True (standaardwaarde), False |Nee |

#### <a name="example-azuredatalakestoresource"></a>Voorbeeld: AzureDataLakeStoreSource

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Zie voor meer informatie [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) artikel.

### <a name="azure-data-lake-store-sink-in-copy-activity"></a>Azure Data Lake Store Sink in de kopieerbewerking
Als u gegevens tooan Azure Data Lake Store kopieert, stelt u Hallo **type sink** Hallo kopieeractiviteit te**AzureDataLakeStoreSink**, en opgeven na eigenschappen in Hallo **sink**sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| copyBehavior |Hiermee geeft u Hallo kopie gedrag. |<b>PreserveHierarchy</b>: gehandhaafd Hallo bestandshiërarchie in de doelmap Hallo. Hallo relatieve pad van de bestandsmap toosource bron is identiek toohello relatieve pad van de bestandsmap tootarget doel.<br/><br/><b>FlattenHierarchy</b>: alle bestanden uit de bronmap Hallo worden gemaakt in Hallo eerste niveau van de doelmap. Hallo doelbestanden worden gemaakt met de automatisch gegenereerde naam.<br/><br/><b>MergeFiles</b>: alle bestanden uit map Hallo-tooone bronbestand worden samengevoegd. Als Hallo bestand/Blob-naam wordt opgegeven, zou Hallo Samengevoegde bestandsnaam Hallo opgegeven name; zijn anders zou worden automatisch gegenereerde naam. |Nee |

#### <a name="example-azuredatalakestoresink"></a>Voorbeeld: AzureDataLakeStoreSink
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
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
        }]
    }
}
```

Zie voor meer informatie [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) artikel. 

## <a name="azure-cosmos-db"></a>Azure Cosmos DB  

### <a name="linked-service"></a>Gekoppelde service
een Cosmos Azure DB toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**DocumentDb**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| **Eigenschap** | **Beschrijving** | **Vereist** |
| --- | --- | --- |
| connectionString |Geef informatie nodig tooconnect tooAzure Cosmos-DB-database. |Ja |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
Zie voor meer informatie [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) artikel.

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset Azure Cosmos DB set Hallo **type** van Hallo gegevensset te**DocumentDbCollection**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| **Eigenschap** | **Beschrijving** | **Vereist** |
| --- | --- | --- |
| CollectionName |Naam van hello Azure DB die Cosmos-verzameling. |Ja |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
Zie voor meer informatie [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) artikel.

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a>Azure Cosmos DB verzameling bron in de kopieerbewerking
Als u gegevens uit een Cosmos Azure DB kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**DocumentDbCollectionSource**, en opgeven na eigenschappen in Hallo **bron** sectie:


| **Eigenschap** | **Beschrijving** | **Toegestane waarden** | **Vereist** |
| --- | --- | --- | --- |
| query |Geef gegevens op Hallo query tooread. |Queryreeks wordt ondersteund door Azure Cosmos DB. <br/><br/>Voorbeeld:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Nee <br/><br/>Als niet wordt opgegeven, Hallo SQL-instructie die is uitgevoerd:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Speciaal teken tooindicate dat document Hallo is genest |Willekeurig teken. <br/><br/>Azure Cosmos-database is een NoSQL-opslagplaats voor JSON-documenten, waarbij geneste structuren zijn toegestaan. Azure Data Factory kunt toodenote gebruikershiërarchie via nestingSeparator die "." in hello bovenstaande voorbeelden. Met Hallo scheidingsteken, genereert kopieeractiviteit Hallo Hallo "Name" object met drie onderliggende elementen eerste, middelste en laatste, volgens too"Name.First ', 'Name.Middle' en 'Name.Last' in hello tabeldefinitie. |Nee |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a>Azure Cosmos DB verzameling Sink in de kopieerbewerking
Als u gegevens tooAzure Cosmos DB kopieert, stelt u Hallo **type sink** Hallo kopieeractiviteit te**DocumentDbCollectionSink**, en opgeven na eigenschappen in Hallo **sink**sectie:

| **Eigenschap** | **Beschrijving** | **Toegestane waarden** | **Vereist** |
| --- | --- | --- | --- |
| nestingSeparator |Er is een speciaal teken in Hallo bron kolom naam tooindicate dat document genest nodig. <br/><br/>Zoals hierboven: `Name.First` in Hallo-uitvoer produceert tabel Hallo JSON-structuur in Hallo Cosmos DB document te volgen:<br/><br/>"Name": {<br/>    ' First ': 'John'<br/>}, |Teken gebruikte tooseparate aantal geneste niveaus.<br/><br/>Standaardwaarde is `.` (punt). |Teken gebruikte tooseparate aantal geneste niveaus. <br/><br/>Standaardwaarde is `.` (punt). |
| writeBatchSize |Aantal parallelle aanvragen tooAzure Cosmos DB service toocreate documenten.<br/><br/>Bij het kopiëren van gegevens van Azure DB die Cosmos met behulp van deze eigenschap kunt u de prestaties van Hallo verfijnen. U kunt een betere prestaties verwachten wanneer u writeBatchSize verhogen omdat meer parallelle aanvragen tooAzure Cosmos DB worden verzonden. Maar u moet tooavoid beperking die kunnen genereert fout het Hallo-bericht: 'Vragen snelheid is groot'.<br/><br/>Beperking wordt bepaald door een aantal factoren, onder andere de grootte van documenten, aantal termen in documenten, indexeren beleid van de doelverzameling, enzovoort. Voor het kopiëren van, kunt u een betere verzameling (bijvoorbeeld S3) toohave Hallo meeste doorvoer beschikbaar (2500 aanvragen eenheden/seconde). |Geheel getal |Nee (standaard: 5) |
| writeBatchTimeout |Wachttijd voor Hallo bewerking toocomplete voordat een time-out optreedt. |TimeSpan<br/><br/> Voorbeeld: "00: 30:00 ' (30 minuten). |Nee |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

Zie voor meer informatie [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) artikel.

## <a name="azure-sql-database"></a>Azure SQL Database

### <a name="linked-service"></a>Gekoppelde service
een Azure SQL Database toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureSqlDatabase**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| connectionString |Geef informatie tooconnect toohello Azure SQL Database-exemplaar voor de eigenschap connectionString Hallo nodig. |Ja |

#### <a name="example"></a>Voorbeeld
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Zie voor meer informatie [Azure SQL-connector](data-factory-azure-sql-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset Azure SQL Database set Hallo **type** van Hallo gegevensset te**AzureSqlTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van het Hallo-tabel of weergave in hello Azure SQL Database-exemplaar waarnaar de gekoppelde service verwijst. |Ja |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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
Zie voor meer informatie [Azure SQL-connector](data-factory-azure-sql-connector.md#dataset-properties) artikel. 

### <a name="sql-source-in-copy-activity"></a>SQL-bron in de kopieerbewerking
Als u gegevens uit een Azure SQL Database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**SqlSource**, en opgeven na eigenschappen in Hallo **bron** sectie:


| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| sqlReaderQuery |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Voorbeeld: `select * from MyTable`. |Nee |
| sqlReaderStoredProcedureName |Naam van Hallo opgeslagen procedure die gegevens uit Hallo brontabel leest. |Naam van Hallo opgeslagen procedure. |Nee |
| storedProcedureParameters |Parameters voor Hallo opgeslagen procedure. |Naam/waarde-paren. Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters. |Nee |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
        }]
    }
}
```
Zie voor meer informatie [Azure SQL-connector](data-factory-azure-sql-connector.md#copy-activity-properties) artikel. 

### <a name="sql-sink-in-copy-activity"></a>SQL-Sink in de kopieerbewerking
Als u gegevens tooAzure SQL-Database kopiëren wilt, stelt u Hallo **type sink** Hallo kopieeractiviteit te**SqlSink**, en opgeven na eigenschappen in Hallo **sink** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| writeBatchTimeout |Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt. |TimeSpan<br/><br/> Voorbeeld: "00: 30:00 ' (30 minuten). |Nee |
| writeBatchSize |Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt. |Geheel getal (aantal rijen) |Nee (standaard: 10000) |
| sqlWriterCleanupScript |Geef een query voor de Kopieeractiviteit tooexecute zodat de gegevens van een bepaald segment wordt opgeschoond. |Een query-instructie. |Nee |
| sliceIdentifierColumnName |Geef de naam van een kolom voor de Kopieeractiviteit toofill met segment-ID automatisch gegenereerd en die is gebruikt tooclean van gegevens van een bepaald segment wanneer opnieuw uitgevoerd. |De naam van de kolom van een kolom met gegevenstype binary(32). |Nee |
| sqlWriterStoredProcedureName |Naam van Hallo opgeslagen procedure die upserts (updates/INSERT) gegevens in de doeltabel Hallo. |Naam van Hallo opgeslagen procedure. |Nee |
| storedProcedureParameters |Parameters voor Hallo opgeslagen procedure. |Naam/waarde-paren. Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters. |Nee |
| sqlWriterTableType |Geef een tabel type naam toobe in Hallo opgeslagen procedure gebruikt. Kopieeractiviteit beschikbaar Hallo-gegevens worden verplaatst in een tijdelijke tabel met dit tabeltype. Opgeslagen procedurecode kunt Hallo gegevens wordt gekopieerd met de bestaande gegevens vervolgens samenvoegen. |Een typenaam van de tabel. |Nee |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
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
        }]
    }
}
```

Zie voor meer informatie [Azure SQL-connector](data-factory-azure-sql-connector.md#copy-activity-properties) artikel. 

## <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse

### <a name="linked-service"></a>Gekoppelde service
een Azure SQL Data Warehouse toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureSqlDW**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| connectionString |Geef informatie tooconnect toohello Azure SQL Data Warehouse-exemplaar voor de eigenschap connectionString Hallo nodig. |Ja |



#### <a name="example"></a>Voorbeeld

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Zie voor meer informatie [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset Azure SQL Data Warehouse set Hallo **type** van Hallo gegevensset te**AzureSqlDWTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties**sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van het Hallo-tabel of weergave in hello Azure SQL Data Warehouse-database die Hallo gekoppelde service verwijst. |Ja |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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

Zie voor meer informatie [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) artikel. 

### <a name="sql-dw-source-in-copy-activity"></a>SQL DW-bron in de kopieerbewerking
Als u gegevens uit Azure SQL Data Warehouse kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**SqlDWSource**, en opgeven na eigenschappen in Hallo **bron**sectie:


| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| sqlReaderQuery |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: `select * from MyTable`. |Nee |
| sqlReaderStoredProcedureName |Naam van Hallo opgeslagen procedure die gegevens uit Hallo brontabel leest. |Naam van Hallo opgeslagen procedure. |Nee |
| storedProcedureParameters |Parameters voor Hallo opgeslagen procedure. |Naam/waarde-paren. Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters. |Nee |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
        }]
    }
}
```

Zie voor meer informatie [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) artikel. 

### <a name="sql-dw-sink-in-copy-activity"></a>SQL DW Sink in de kopieerbewerking
Als u gegevens tooAzure SQL Data Warehouse kopiëren wilt, stelt u Hallo **type sink** Hallo kopieeractiviteit te**SqlDWSink**, en opgeven na eigenschappen in Hallo **sink** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Geef een query voor de Kopieeractiviteit tooexecute zodat de gegevens van een bepaald segment wordt opgeschoond. |Een query-instructie. |Nee |
| allowPolyBase |Hiermee wordt aangegeven of toouse PolyBase (indien van toepassing) in plaats van BULKINSERT mechanisme. <br/><br/> **Met PolyBase is Hallo aanbevolen manier tooload gegevens in SQL Data Warehouse.** |True <br/>False (standaard) |Nee |
| polyBaseSettings |Een groep met eigenschappen die kunnen worden opgegeven wanneer hello **allowPolybase** eigenschap is ingesteld, te**true**. |&nbsp; |Nee |
| rejectValue |Hiermee geeft u op Hallo getal of het percentage van de rijen die kunnen worden afgewezen voordat het Hallo-query is mislukt. <br/><br/>Meer informatie over Hallo PolyBase van opties in Hallo afwijzen **argumenten** sectie van [maken EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) onderwerp. |0 (standaard), 1, 2... |Nee |
| rejectType |Hiermee geeft u op of Hallo rejectValue optie is opgegeven als een letterlijke waarde of een percentage. |In waarde (standaard), Percentage |Nee |
| rejectSampleValue |Bepaalt het aantal rijen tooretrieve Hallo voordat Hallo PolyBase Hallo percentage geweigerde rijen opnieuw berekend. |1, 2, … |Ja, als **rejectType** is **percentage** |
| useTypeDefault |Hiermee geeft u op hoe toohandle ontbreken waarden in tekstbestanden gescheiden wanneer PolyBase gegevens uit Hallo tekstbestand ophaalt.<br/><br/>Meer informatie over deze eigenschap in Hallo argumenten sectie [maken EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |True, False (standaard) |Nee |
| writeBatchSize |Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt |Geheel getal (aantal rijen) |Nee (standaard: 10000) |
| writeBatchTimeout |Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt. |TimeSpan<br/><br/> Voorbeeld: "00: 30:00 ' (30 minuten). |Nee |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
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
        }]
    }
}
```

Zie voor meer informatie [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) artikel. 

## <a name="azure-search"></a>Azure Search

### <a name="linked-service"></a>Gekoppelde service
een Azure Search toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureSearch**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| -------- | ----------- | -------- |
| URL | De URL voor hello Azure Search-service. | Ja |
| sleutel | Administratorsleutel voor hello Azure Search-service. | Ja |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

Zie voor meer informatie [Azure Search-connector](data-factory-azure-search-connector.md#linked-service-properties) artikel.

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset Azure Search set Hallo **type** van Hallo gegevensset te**AzureSearchIndex**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie : 

| Eigenschap | Beschrijving | Vereist |
| -------- | ----------- | -------- |
| type | de eigenschap type Hello te moet worden ingesteld**AzureSearchIndex**.| Ja |
| NaamCommunity | Naam van hello Azure Search-index. Data Factory maakt geen Hallo index. Hallo-index moet bestaan in Azure Search. | Ja |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

Zie voor meer informatie [Azure Search-connector](data-factory-azure-search-connector.md#dataset-properties) artikel.

### <a name="azure-search-index-sink-in-copy-activity"></a>Sink voor Azure Search-Index in de kopieerbewerking
Als u gegevens tooan Azure Search-index kopieert, stelt u Hallo **type sink** Hallo kopieeractiviteit te**AzureSearchIndexSink**, en opgeven na eigenschappen in Hallo **sink**sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Hiermee geeft u op of toomerge of vervangen, wanneer een document al in Hallo index bestaat. | samenvoegen (standaard)<br/>Uploaden| Nee |
| writeBatchSize | Gegevens geüpload in hello Azure Search-index wanneer Hallo buffergrootte writeBatchSize bereikt. | 1 too1 000. Standaardwaarde is 1000. | Nee |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
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
        }]
    }
}
```

Zie voor meer informatie [Azure Search-connector](data-factory-azure-search-connector.md#copy-activity-properties) artikel.

## <a name="azure-table-storage"></a>Azure-tabelopslag

### <a name="linked-service"></a>Gekoppelde service
Er zijn twee soorten gekoppelde services: gekoppelde Azure Storage-service en de gekoppelde Azure Storage SAS-service.

#### <a name="azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service
toolink uw Azure storage-account tooa data factory met behulp van Hallo **accountsleutel**, maak een gekoppelde Azure Storage-service. toodefine een Azure Storage gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureStorage**. U kunt vervolgens opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| type |Hallo type eigenschap moet worden ingesteld op: **AzureStorage** |Ja |
| connectionString |Geef informatie tooconnect tooAzure opslag voor de eigenschap connectionString Hallo nodig. |Ja |

**Voorbeeld:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a>Gekoppelde Azure Storage SAS-Service
Hallo SAS van Azure Storage gekoppelde service, kunt u een Azure Storage-Account tooan Azure data factory toolink met behulp van een Shared Access Signature (SAS). Het biedt Hallo data factory toegang beperkt/tijdsgebonden tooall/specifieke bronnen (blobcontainer) / in Hallo-opslag. toolink uw Azure storage-account tooa data factory met behulp van Shared Access Signature maken van een SAS van Azure Storage gekoppelde service. een Azure Storage-SAS toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureStorageSas**. U kunt vervolgens opgeven na eigenschappen in Hallo **typeProperties** sectie:   

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| type |Hallo type eigenschap moet worden ingesteld op: **AzureStorageSas** |Ja |
| sasUri |Geef de Shared Access Signature URI toohello Azure Storage-resources zoals blob-container of tabel. |Ja |

**Voorbeeld:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Zie voor meer informatie over deze gekoppelde services, [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset Azure Table set Hallo **type** van Hallo gegevensset te**AzureTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van de tabel Hallo in hello Azure Table-Database-instantie waarnaar de gekoppelde service verwijst. |Ja. Wanneer een tabelnaam is opgegeven zonder een azureTableSourceQuery, worden alle records uit de tabel Hallo gekopieerde toohello bestemming. Als een azureTableSourceQuery ook is opgegeven, worden records uit de tabel Hallo die voldoet aan de query Hallo gekopieerde toohello bestemming. |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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

Zie voor meer informatie over deze gekoppelde services, [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) artikel. 

### <a name="azure-table-source-in-copy-activity"></a>Bron van de Azure-tabel in de kopieerbewerking
Als u gegevens uit Azure Table Storage kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**AzureTableSource**, en opgeven na eigenschappen in Hallo **bron**sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| azureTableSourceQuery |Hallo aangepaste query tooread gegevens worden gebruikt. |Azure-tabel queryreeks. Zie de voorbeelden in de volgende sectie Hallo. |Nee. Wanneer een tabelnaam is opgegeven zonder een azureTableSourceQuery, worden alle records uit de tabel Hallo gekopieerde toohello bestemming. Als een azureTableSourceQuery ook is opgegeven, worden records uit de tabel Hallo die voldoet aan de query Hallo gekopieerde toohello bestemming. |
| azureTableSourceIgnoreTableNotFound |Geef aan of slikken Hallo uitzondering van de tabel niet bestaat. |DE WAARDE TRUE<br/>DE WAARDE FALSE |Nee |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
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
        }]
    }
}
```

Zie voor meer informatie over deze gekoppelde services, [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) artikel. 

### <a name="azure-table-sink-in-copy-activity"></a>Azure-tabel Sink in de kopieerbewerking
Als u gegevens tooAzure Table Storage kopieert, stelt u Hallo **type sink** Hallo kopieeractiviteit te**AzureTableSink**, en opgeven na eigenschappen in Hallo **sink** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Standaardwaarde voor de partitiesleutel die kan worden gebruikt door Hallo sink. |Een string-waarde. |Nee |
| azureTablePartitionKeyName |Naam van het Hallo-kolom waarvan de waarden worden gebruikt als partitiesleutels opgeven. Als niet wordt opgegeven, wordt AzureTableDefaultPartitionKeyValue gebruikt als partitiesleutel Hallo. |De naam van een kolom. |Nee |
| azureTableRowKeyName |Naam van het Hallo-kolom waarvan de kolomwaarden worden gebruikt als de rijsleutel opgeven. Als niet wordt opgegeven, gebruikt u een GUID voor elke rij. |De naam van een kolom. |Nee |
| azureTableInsertType |Hallo modus tooinsert gegevens in Azure-tabel.<br/><br/>Deze eigenschap bepaalt of bestaande rijen in de uitvoertabel Hallo met partitie-als rijsleutels die overeenkomt met de waarden vervangen of samenvoegen van hebben. <br/><br/>toolearn over hoe deze instellingen (merge en vervangen) werken, Zie [invoegen of Merge entiteit](https://msdn.microsoft.com/library/azure/hh452241.aspx) en [invoegen of vervangen entiteit](https://msdn.microsoft.com/library/azure/hh452242.aspx) onderwerpen. <br/><br> Deze instelling is van toepassing op Hallo rijniveau niet Hallo-tabelniveau, en geen van beide optie worden de rijen in de uitvoertabel Hallo die niet bestaan in de invoer Hallo verwijderd. |samenvoegen (standaard)<br/>vervangen |Nee |
| writeBatchSize |Voegt de gegevens in hello Azure-tabel wanneer Hallo writeBatchSize of writeBatchTimeout is bereikt. |Geheel getal (aantal rijen) |Nee (standaard: 10000) |
| writeBatchTimeout |Voegt de gegevens in hello Azure-tabel wanneer Hallo writeBatchSize of writeBatchTimeout is bereikt. |TimeSpan<br/><br/>Voorbeeld: "00: 20:00 ' (20 minuten) |Nee (standaard toostorage client standaardtime-out waarde 90 sec) |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
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
        }]
    }
}
```
Zie voor meer informatie over deze gekoppelde services, [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) artikel. 

## <a name="amazon-redshift"></a>Amazon RedShift

### <a name="linked-service"></a>Gekoppelde service
een Redshift Amazon toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AmazonRedshift**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| server |IP-naam adres of de hostnaam van Hallo Amazon Redshift server. |Ja |
| poort |toolisten Hello aantal Hallo TCP-poort die Hallo Amazon Redshift server gebruikt voor clientverbindingen. |Nee, de standaardwaarde: 5439 |
| database |Naam van Hallo Amazon Redshift database. |Ja |
| gebruikersnaam |Naam van de gebruiker die toegang toohello database heeft. |Ja |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo. |Ja |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

Zie voor meer informatie [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset Amazon Redshift set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van de tabel Hallo in Hallo Amazon Redshift database waarnaar de gekoppelde service verwijst. |Nee (als **query** van **RelationalSource** is opgegeven) |


#### <a name="example"></a>Voorbeeld

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Zie voor meer informatie [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) artikel.

### <a name="relational-source-in-copy-activity"></a>Relationele gegevensbron in de kopieerbewerking 
Als u gegevens vanaf Amazon Redshift kopieert, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: `select * from MyTable`. |Nee (als **tableName** van **gegevensset** is opgegeven) |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Zie voor meer informatie [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) artikel.

## <a name="ibm-db2"></a>IBM DB2

### <a name="linked-service"></a>Gekoppelde service
een IBM DB2 toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesDB2**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| server |Naam van Hallo DB2-server. |Ja |
| database |Naam van Hallo DB2-database. |Ja |
| Schema |Naam van Hallo schema in Hallo-database. Hallo-schemanaam is hoofdlettergevoelig. |Nee |
| authenticationType |Type verificatie gebruikt tooconnect toohello DB2-database. Mogelijke waarden zijn: anoniem, basis en Windows. |Ja |
| gebruikersnaam |Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt. |Nee |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven. |Nee |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale DB2-database gebruiken. |Ja |

#### <a name="example"></a>Voorbeeld
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
Zie voor meer informatie [IBM DB2-connector](#data-factory-onprem-db2-connector.md#linked-service-properties) artikel.

### <a name="dataset"></a>Gegevensset
toodefine een DB2-gegevensset, set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van het Hallo-tabel in Hallo DB2-Database-instantie waarnaar de gekoppelde service verwijst. Hallo tableName is hoofdlettergevoelig. |Nee (als **query** van **RelationalSource** is opgegeven) 

#### <a name="example"></a>Voorbeeld
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

Zie voor meer informatie [IBM DB2-connector](#data-factory-onprem-db2-connector.md#dataset-properties) artikel.

### <a name="relational-source-in-copy-activity"></a>Relationele gegevensbron in de kopieerbewerking
Als u gegevens uit IBM DB2 kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:


| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: `"query": "select * from "MySchema"."MyTable""`. |Nee (als **tableName** van **gegevensset** is opgegeven) |

#### <a name="example"></a>Voorbeeld
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
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
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Zie voor meer informatie [IBM DB2-connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) artikel.

## <a name="mysql"></a>MySQL

### <a name="linked-service"></a>Gekoppelde service
een MySQL toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesMySql**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| server |Naam van Hallo MySQL-server. |Ja |
| database |Naam van Hallo MySQL-database. |Ja |
| Schema |Naam van Hallo schema in Hallo-database. |Nee |
| authenticationType |Type verificatie gebruikt tooconnect toohello MySQL-database. Mogelijke waarden zijn: `Basic`. |Ja |
| gebruikersnaam |Geef de gebruiker de naam van tooconnect toohello MySQL-database. |Ja |
| wachtwoord |Geef het wachtwoord voor Hallo-gebruikersaccount die u hebt opgegeven. |Ja |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale MySQL-database gebruiken. |Ja |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

Zie voor meer informatie [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset MySQL set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van de tabel Hallo in Hallo MySQL-Database-instantie waarnaar de gekoppelde service verwijst. |Nee (als **query** van **RelationalSource** is opgegeven) |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
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
Zie voor meer informatie [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) artikel. 

### <a name="relational-source-in-copy-activity"></a>Relationele gegevensbron in de kopieerbewerking
Als u gegevens uit een MySQL-database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:


| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: `select * from MyTable`. |Nee (als **tableName** van **gegevensset** is opgegeven) |


#### <a name="example"></a>Voorbeeld
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Zie voor meer informatie [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) artikel. 

## <a name="oracle"></a>Oracle 

### <a name="linked-service"></a>Gekoppelde service
een Oracle toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesOracle**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| driverType | Geef op welke stuurprogramma toouse toocopy gegevens uit / tooOracle Database. Toegestane waarden zijn **Microsoft** of **ODP** (standaard). Zie [ondersteunde versie en installatieopties](#supported-versions-and-installation) gedeelte stuurprogrammagegevens. | Nee |
| connectionString | Geef informatie tooconnect toohello Oracle-Database-exemplaar voor de eigenschap connectionString Hallo nodig. | Ja |
| gatewayName | Naam van Hallo gateway die die gebruikte tooconnect toohello lokale Oracle-server |Ja |

#### <a name="example"></a>Voorbeeld
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Zie voor meer informatie [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) artikel.

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset Oracle set Hallo **type** van Hallo gegevensset te**OracleTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van de tabel Hallo in Hallo Oracle-Database die Hallo gekoppelde service verwijst. |Nee (als **oracleReaderQuery** van **OracleSource** is opgegeven) |

#### <a name="example"></a>Voorbeeld

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
            "anchorDateTime": "2016-02-27T12:00:00",
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
Zie voor meer informatie [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) artikel.

### <a name="oracle-source-in-copy-activity"></a>Oracle-bron in de kopieerbewerking
Als u gegevens uit een Oracle-database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**OracleSource**, en opgeven na eigenschappen in Hallo **bron** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| oracleReaderQuery |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: `select * from MyTable` <br/><br/>Als niet wordt opgegeven, Hallo SQL-instructie die is uitgevoerd:`select * from MyTable` |Nee (als **tableName** van **gegevensset** is opgegeven) |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }]
    }
}
```

Zie voor meer informatie [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) artikel.

### <a name="oracle-sink-in-copy-activity"></a>Oracle-Sink in de kopieerbewerking
Als u gegevens tooam Oracle-database kopiëren wilt, stelt u Hallo **type sink** Hallo kopieeractiviteit te**OracleSink**, en opgeven na eigenschappen in Hallo **sink** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| writeBatchTimeout |Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt. |TimeSpan<br/><br/> Voorbeeld: 00:30:00 (30 minuten). |Nee |
| writeBatchSize |Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt. |Geheel getal (aantal rijen) |Nee (standaard: 100) |
| sqlWriterCleanupScript |Geef een query voor de Kopieeractiviteit tooexecute zodat de gegevens van een bepaald segment wordt opgeschoond. |Een query-instructie. |Nee |
| sliceIdentifierColumnName |Geef kolomnaam voor Kopieeractiviteit toofill met segment-ID automatisch gegenereerd en die is gebruikt tooclean van gegevens van een bepaald segment wanneer opnieuw uitgevoerd. |De naam van de kolom van een kolom met gegevenstype binary(32). |Nee |

#### <a name="example"></a>Voorbeeld
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
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
        }]
    }
}
```
Zie voor meer informatie [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) artikel.

## <a name="postgresql"></a>PostgreSQL

### <a name="linked-service"></a>Gekoppelde service
een PostgreSQL toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesPostgreSql**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| server |Naam van Hallo PostgreSQL-server. |Ja |
| database |Naam van Hallo PostgreSQL-database. |Ja |
| Schema |Naam van Hallo schema in Hallo-database. Hallo-schemanaam is hoofdlettergevoelig. |Nee |
| authenticationType |Type verificatie gebruikt tooconnect toohello PostgreSQL-database. Mogelijke waarden zijn: anoniem, basis en Windows. |Ja |
| gebruikersnaam |Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt. |Nee |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven. |Nee |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale PostgreSQL-database gebruiken. |Ja |

#### <a name="example"></a>Voorbeeld

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
Zie voor meer informatie [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) artikel.

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset PostgreSQL set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van de tabel Hallo in Hallo PostgreSQL-Database-instantie waarnaar de gekoppelde service verwijst. Hallo tableName is hoofdlettergevoelig. |Nee (als **query** van **RelationalSource** is opgegeven) |

#### <a name="example"></a>Voorbeeld
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
Zie voor meer informatie [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) artikel.

### <a name="relational-source-in-copy-activity"></a>Relationele gegevensbron in de kopieerbewerking
Als u gegevens uit een PostgreSQL-database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron**sectie:


| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: "query": "Selecteer * uit \"MySchema\".\" MyTable\"'. |Nee (als **tableName** van **gegevensset** is opgegeven) |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
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
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Zie voor meer informatie [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) artikel.

## <a name="sap-business-warehouse"></a>SAP Business Warehouse


### <a name="linked-service"></a>Gekoppelde service
een SAP Business Warehouse (BW) toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**SapBw**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:  

Eigenschap | Beschrijving | Toegestane waarden | Vereist
-------- | ----------- | -------------- | --------
server | Naam van het Hallo-server op welke Hallo SAP BW exemplaar zich bevindt. | Tekenreeks | Ja
systemNumber | Systeem aantal Hallo SAP BW-systeem. | Twee cijfers decimaal getal weergegeven als een tekenreeks. | Ja
clientId | Client-ID van de client Hallo in Hallo SAP W system. | Drie cijfers decimaal getal weergegeven als een tekenreeks. | Ja
gebruikersnaam | Naam van het Hallo-gebruiker met toegang toohello SAP-server | Tekenreeks | Ja
wachtwoord | Wachtwoord voor gebruiker Hallo. | Tekenreeks | Ja
gatewayName | Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale SAP BW exemplaar gebruiken. | Tekenreeks | Ja
encryptedCredential | Hallo versleutelde referentie-tekenreeks. | Tekenreeks | Nee

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Zie voor meer informatie [SAP Business Warehouse-connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset SAP BW set Hallo **type** van Hallo gegevensset te**RelationalTable**. Er zijn geen type-specifieke eigenschappen ondersteund voor SAP BW-gegevensset Hallo van het type **RelationalTable**.  

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Zie voor meer informatie [SAP Business Warehouse-connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) artikel. 

### <a name="relational-source-in-copy-activity"></a>Relationele gegevensbron in de kopieerbewerking
Als u gegevens uit een SAP Business Warehouse kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron**sectie:


| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query | Hiermee geeft u Hallo MDX-query tooread gegevens van Hallo SAP BW-exemplaar. | MDX-query. | Ja |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Zie voor meer informatie [SAP Business Warehouse-connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) artikel. 

## <a name="sap-hana"></a>SAP HANA

### <a name="linked-service"></a>Gekoppelde service
een SAP HANA toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**SapHana**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

Eigenschap | Beschrijving | Toegestane waarden | Vereist
-------- | ----------- | -------------- | --------
server | Naam van het Hallo-server op welke Hallo SAP HANA exemplaar zich bevindt. Als de server een aangepaste poort gebruikt is, geeft u `server:port`. | Tekenreeks | Ja
authenticationType | Het type verificatie. | De tekenreeks. 'Basic' of 'Windows' | Ja 
gebruikersnaam | Naam van het Hallo-gebruiker met toegang toohello SAP-server | Tekenreeks | Ja
wachtwoord | Wachtwoord voor gebruiker Hallo. | Tekenreeks | Ja
gatewayName | Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale SAP HANA-exemplaar gebruiken. | Tekenreeks | Ja
encryptedCredential | Hallo versleutelde referentie-tekenreeks. | Tekenreeks | Nee

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
Zie voor meer informatie [SAP HANA-connector](data-factory-sap-hana-connector.md#linked-service-properties) artikel.
 
### <a name="dataset"></a>Gegevensset
toodefine een SAP HANA-gegevensset set Hallo **type** van Hallo gegevensset te**RelationalTable**. Er zijn geen type-specifieke eigenschappen ondersteund voor SAP HANA-gegevensset Hallo van het type **RelationalTable**. 

#### <a name="example"></a>Voorbeeld

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
Zie voor meer informatie [SAP HANA-connector](data-factory-sap-hana-connector.md#dataset-properties) artikel. 

### <a name="relational-source-in-copy-activity"></a>Relationele gegevensbron in de kopieerbewerking
Als u gegevens uit een SAP HANA-gegevensarchief kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron**sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query | Hiermee geeft u Hallo SQL query tooread gegevens van Hallo SAP HANA-exemplaar. | SQL-query. | Ja |


#### <a name="example"></a>Voorbeeld


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
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
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Zie voor meer informatie [SAP HANA-connector](data-factory-sap-hana-connector.md#copy-activity-properties) artikel.


## <a name="sql-server"></a>SQL Server

### <a name="linked-service"></a>Gekoppelde service
Maken van een gekoppelde service van het type **OnPremisesSqlServer** toolink een lokale SQL Server-database tooa data factory. Hallo volgende tabel biedt een beschrijving voor de service voor JSON-elementen specifieke tooon-premises SQL Server gekoppeld.

Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooSQL gekoppelde Server-service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **OnPremisesSqlServer**. |Ja |
| connectionString |Geef connectionString informatie nodig tooconnect toohello lokale SQL Server-database met behulp van de SQL-verificatie of de Windows-verificatie. |Ja |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale SQL Server-database gebruiken. |Ja |
| gebruikersnaam |Geef de gebruikersnaam als u Windows-verificatie gebruikt. Voorbeeld: **domainname\\gebruikersnaam**. |Nee |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven. |Nee |

U kunt referenties met een Hallo versleutelen **nieuw AzureRmDataFactoryEncryptValue** cmdlet en in de verbindingsreeks hello gebruiken, zoals wordt weergegeven in het volgende voorbeeld Hallo (**EncryptedCredential** eigenschap):  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Voorbeeld: JSON voor het gebruik van SQL-verificatie

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Voorbeeld: JSON voor het gebruik van Windows-verificatie

Als de gebruikersnaam en wachtwoord zijn opgegeven, gateway maakt gebruik van deze tooimpersonate Hallo opgegeven gebruiker account tooconnect toohello lokale SQL Server-database. Gatewayserver verbindt anders toohello SQL-Server rechtstreeks met de beveiligingscontext Hallo van Gateway (het starten van de account).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Zie voor meer informatie [SQL Server-connector](data-factory-sqlserver-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een SQL Server-gegevensset set Hallo **type** van Hallo gegevensset te**SqlServerTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van het Hallo-tabel of weergave in Hallo SQL Server Database-instantie waarnaar de gekoppelde service verwijst. |Ja |

#### <a name="example"></a>Voorbeeld
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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

Zie voor meer informatie [SQL Server-connector](data-factory-sqlserver-connector.md#dataset-properties) artikel. 

### <a name="sql-source-in-copy-activity"></a>SQL-bron in de kopieerbewerking
Als u gegevens uit een SQL Server-database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**SqlSource**, en opgeven na eigenschappen in Hallo **bron** sectie:


| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| sqlReaderQuery |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: `select * from MyTable`. Kan naar meerdere tabellen uit Hallo database waarnaar wordt verwezen door de invoergegevensset Hallo verwijzen. Als niet wordt opgegeven, Hallo SQL-instructie die is uitgevoerd: Selecteer een van de MyTable. |Nee |
| sqlReaderStoredProcedureName |Naam van Hallo opgeslagen procedure die gegevens uit Hallo brontabel leest. |Naam van Hallo opgeslagen procedure. |Nee |
| storedProcedureParameters |Parameters voor Hallo opgeslagen procedure. |Naam/waarde-paren. Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters. |Nee |

Als hello **sqlReaderQuery** is opgegeven voor Hallo SqlSource, hello Kopieeractiviteit deze query wordt uitgevoerd tegen Hallo SQL Server-Database tooget Hallo brongegevens.

U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).

Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, zijn gedefinieerd in de sectie structuur Hallo Hallo-kolommen gebruikte toobuild een toorun selectiequery tegen Hallo SQL Server-Database. Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.

> [!NOTE]
> Als u werkt met **sqlReaderStoredProcedureName**, moet u nog steeds toospecify een waarde voor Hallo **tableName** eigenschap in de gegevensset Hallo JSON. Er zijn geen controles uitgevoerd voor deze tabel al.


#### <a name="example"></a>Voorbeeld
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
        }]
    }
}
```

In dit voorbeeld **sqlReaderQuery** voor Hallo SqlSource is opgegeven. Deze query Hallo Kopieeractiviteit uitgevoerd tegen Hallo tooget SQL Server-Database-Hallo brongegevens. U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist). Hallo sqlReaderQuery kunt verwijzen naar meerdere tabellen in Hallo database waarnaar wordt verwezen door Hallo invoergegevensset. Het is niet beperkt tooonly Hallo tabel van deze dataset tableName typeProperty Hallo ingesteld.

Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, zijn gedefinieerd in de sectie structuur Hallo Hallo-kolommen gebruikte toobuild een toorun selectiequery tegen Hallo SQL Server-Database. Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.

Zie voor meer informatie [SQL Server-connector](data-factory-sqlserver-connector.md#copy-activity-properties) artikel. 

### <a name="sql-sink-in-copy-activity"></a>SQL-Sink in de kopieerbewerking
Als u gegevens tooa SQL Server-database kopiëren wilt, stelt u Hallo **type sink** Hallo kopieeractiviteit te**SqlSink**, en opgeven na eigenschappen in Hallo **sink** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| writeBatchTimeout |Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt. |TimeSpan<br/><br/> Voorbeeld: "00: 30:00 ' (30 minuten). |Nee |
| writeBatchSize |Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt. |Geheel getal (aantal rijen) |Nee (standaard: 10000) |
| sqlWriterCleanupScript |Query voor de Kopieeractiviteit tooexecute opgeven zodat de gegevens van een bepaald segment wordt opgeschoond. Zie voor meer informatie [herhaalbaarheid](#repeatability-during-copy) sectie. |Een query-instructie. |Nee |
| sliceIdentifierColumnName |Geef kolomnaam voor Kopieeractiviteit toofill met segment-ID automatisch gegenereerd en die is gebruikt tooclean van gegevens van een bepaald segment wanneer opnieuw uitgevoerd. Zie voor meer informatie [herhaalbaarheid](#repeatability-during-copy) sectie. |De naam van de kolom van een kolom met gegevenstype binary(32). |Nee |
| sqlWriterStoredProcedureName |Naam van Hallo opgeslagen procedure die upserts (updates/INSERT) gegevens in de doeltabel Hallo. |Naam van Hallo opgeslagen procedure. |Nee |
| storedProcedureParameters |Parameters voor Hallo opgeslagen procedure. |Naam/waarde-paren. Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters. |Nee |
| sqlWriterTableType |Geef tabel type naam toobe in Hallo opgeslagen procedure gebruikt. Kopieeractiviteit beschikbaar Hallo-gegevens worden verplaatst in een tijdelijke tabel met dit tabeltype. Opgeslagen procedurecode kunt Hallo gegevens wordt gekopieerd met de bestaande gegevens vervolgens samenvoegen. |Een typenaam van de tabel. |Nee |

#### <a name="example"></a>Voorbeeld
Hallo pijplijn bevat een Kopieeractiviteit die is geconfigureerd toouse deze invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en **sink** type is ingesteld, te**SqlSink**.

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
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
        }]
    }
}
```

Zie voor meer informatie [SQL Server-connector](data-factory-sqlserver-connector.md#copy-activity-properties) artikel. 

## <a name="sybase"></a>Sybase

### <a name="linked-service"></a>Gekoppelde service
toodefine een Sybase gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesSybase**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| server |Naam van Hallo Sybase-server. |Ja |
| database |Naam van Hallo Sybase-database. |Ja |
| Schema |Naam van Hallo schema in Hallo-database. |Nee |
| authenticationType |Type verificatie gebruikt tooconnect toohello Sybase-database. Mogelijke waarden zijn: anoniem, basis en Windows. |Ja |
| gebruikersnaam |Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt. |Nee |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven. |Nee |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale Sybase-database gebruiken. |Ja |

#### <a name="example"></a>Voorbeeld
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
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

Zie voor meer informatie [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset Sybase set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van de tabel Hallo in Hallo Sybase-Database-instantie waarnaar de gekoppelde service verwijst. |Nee (als **query** van **RelationalSource** is opgegeven) |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
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

Zie voor meer informatie [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) artikel. 

### <a name="relational-source-in-copy-activity"></a>Relationele gegevensbron in de kopieerbewerking
Als u gegevens uit een Sybase-database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:


| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: `select * from MyTable`. |Nee (als **tableName** van **gegevensset** is opgegeven) |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Zie voor meer informatie [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) artikel.

## <a name="teradata"></a>Teradata

### <a name="linked-service"></a>Gekoppelde service
een Teradata toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesTeradata**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| server |Naam van Hallo Teradata-server. |Ja |
| authenticationType |Type verificatie gebruikt tooconnect toohello Teradata-database. Mogelijke waarden zijn: anoniem, basis en Windows. |Ja |
| gebruikersnaam |Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt. |Nee |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven. |Nee |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale Teradata-database gebruiken. |Ja |

#### <a name="example"></a>Voorbeeld
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Zie voor meer informatie [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) artikel.

### <a name="dataset"></a>Gegevensset
toodefine een Teradata-Blob-gegevensset set Hallo **type** van Hallo gegevensset te**RelationalTable**. Er zijn momenteel geen type-eigenschappen voor Hallo Teradata gegevensset ondersteund. 

#### <a name="example"></a>Voorbeeld
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
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

Zie voor meer informatie [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) artikel.

### <a name="relational-source-in-copy-activity"></a>Relationele gegevensbron in de kopieerbewerking
Als u gegevens uit een Teradata-database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron**sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: `select * from MyTable`. |Ja |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

Zie voor meer informatie [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) artikel.

## <a name="cassandra"></a>Cassandra


### <a name="linked-service"></a>Gekoppelde service
een Cassandra toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesCassandra**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| host |Een of meer IP-adressen of hostnamen van Cassandra servers.<br/><br/>Geef een door komma's gescheiden lijst met IP-adressen of namen tooconnect tooall hostservers gelijktijdig. |Ja |
| poort |toolisten Hello TCP-poort die Hallo Cassandra server gebruikt voor clientverbindingen. |Nee, de standaardwaarde: 9042 |
| authenticationType |Basic- of anonieme |Ja |
| gebruikersnaam |Geef de gebruikersnaam voor Hallo-gebruikersaccount. |Ja, als authenticationType tooBasic is ingesteld. |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo opgeven. |Ja, als authenticationType tooBasic is ingesteld. |
| gatewayName |Hallo-naam van Hallo-gateway die is gebruikt tooconnect toohello lokale Cassandra-database. |Ja |
| encryptedCredential |Referentie versleuteld door Hallo-gateway. |Nee |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Zie voor meer informatie [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset Cassandra set Hallo **type** van Hallo gegevensset te**CassandraTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| met keyspace |Naam van Hallo keyspace of het schema in Cassandra-database. |Ja (als **query** voor **CassandraSource** is niet gedefinieerd). |
| tableName |Naam van de tabel Hallo in Cassandra-database. |Ja (als **query** voor **CassandraSource** is niet gedefinieerd). |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
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

Zie voor meer informatie [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) artikel. 

### <a name="cassandra-source-in-copy-activity"></a>Cassandra-bron in de kopieerbewerking
Als u gegevens uit Cassandra kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**CassandraSource**, en opgeven na eigenschappen in Hallo **bron** sectie :

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-92 query of CQL query. Zie [CQL verwijzing](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>Wanneer u SQL-query gebruikt, geef **keyspace name.table naam** toorepresent Hallo tabel gewenste tooquery. |Nee (als tableName en keyspace op gegevensset zijn gedefinieerd). |
| consistencyLevel |Hallo consistentieniveau geeft het aantal replica's tooa leesaanvraag moet reageren voordat gegevens toohello clienttoepassing wordt geretourneerd. Cassandra controles Hallo opgegeven aantal replica's voor gegevens toosatisfy Hallo leesaanvraag. |EEN, TWEE, DRIE, QUORUM, ALL, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE. Zie [gegevensconsistentie configureren](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) voor meer informatie. |Nee. Standaardwaarde is een. |

#### <a name="example"></a>Voorbeeld
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
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
        }]
    }
}
```

Zie voor meer informatie [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) artikel.

## <a name="mongodb"></a>MongoDB

### <a name="linked-service"></a>Gekoppelde service
een MongoDB toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesMongoDB**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| server |IP-adres of de hostnaam de naam van Hallo MongoDB-server. |Ja |
| poort |Toolisten TCP-poort die Hallo MongoDB-server gebruikt voor clientverbindingen. |Optionele standaardwaarde: 27017 |
| authenticationType |Basic of anonieme. |Ja |
| gebruikersnaam |Gebruiker account tooaccess MongoDB. |Ja (als u basisverificatie wordt gebruikt). |
| wachtwoord |Wachtwoord voor gebruiker Hallo. |Ja (als u basisverificatie wordt gebruikt). |
| authSource |Naam van Hallo MongoDB-database dat u wilt dat toouse toocheck uw referenties voor verificatie. |Optioneel (als basisverificatie wordt gebruikt). Standaard: maakt gebruik van Hallo-beheerdersaccount en Hallo database die is opgegeven met de eigenschap databaseName. |
| DatabaseName |Naam van Hallo MongoDB-database die u tooaccess wilt. |Ja |
| gatewayName |Naam van het Hallo-gateway die toegang heeft tot Hallo-gegevensarchief. |Ja |
| encryptedCredential |Referentie versleuteld door de gateway. |Optioneel |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Zie voor meer informatie [MongoDB-connector artikel](data-factory-on-premises-mongodb-connector.md#linked-service-properties)

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset MongoDB set Hallo **type** van Hallo gegevensset te**MongoDbCollection**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| CollectionName |Naam van de verzameling Hallo in MongoDB-database. |Ja |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

Zie voor meer informatie [MongoDB-connector artikel](data-factory-on-premises-mongodb-connector.md#dataset-properties)

#### <a name="mongodb-source-in-copy-activity"></a>MongoDB-bron in de kopieerbewerking
Als u gegevens uit MongoDB kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**MongoDbSource**, en opgeven na eigenschappen in Hallo **bron** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-92 queryreeks. Bijvoorbeeld: `select * from MyTable`. |Nee (als **collectionName** van **gegevensset** is opgegeven) |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Zie voor meer informatie [MongoDB-connector artikel](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)

## <a name="amazon-s3"></a>Amazon S3


### <a name="linked-service"></a>Gekoppelde service
een Amazon S3 toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AwsAccessKey**, en opgeven na eigenschappen in Hallo **typeProperties** sectie :  

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| accessKeyID |ID van de geheime toegangssleutel Hallo. |Tekenreeks |Ja |
| secretAccessKey |Hallo geheime toegangssleutel zelf. |Versleutelde geheime tekenreeks |Ja |

#### <a name="example"></a>Voorbeeld
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

Zie voor meer informatie [Amazon S3 connector artikel](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).

### <a name="dataset"></a>Gegevensset
een Amazon S3 toodefine dataset set Hallo **type** van Hallo gegevensset te**AmazonS3**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| bucketName |Hallo S3-Bucketnaam. |Tekenreeks |Ja |
| sleutel |Hallo S3 objectsleutel. |Tekenreeks |Nee |
| voorvoegsel |Voorvoegsel voor Hallo S3 objectsleutel. Objecten waarvan sleutels met dit voorvoegsel beginnen worden geselecteerd. Geldt alleen als sleutel is leeg. |Tekenreeks |Nee |
| Versie |Hallo-versie van S3-object als S3 versiebeheer is ingeschakeld. |Tekenreeks |Nee |
| Indeling | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set Hallo **type** eigenschap onder indeling tooone van deze waarden. Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. <br><br> Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan. |Nee | |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**. Hallo ondersteund niveaus zijn: **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee | |


> [!NOTE]
> bucketName + sleutel geeft Hallo-locatie van Hallo S3 object waarbij bucket Hallo hoofdcontainer voor S3-objecten en sleutel Hallo volledig pad tooS3 object.

#### <a name="example-sample-dataset-with-prefix"></a>Voorbeeld: Voorbeeldgegevensset met voorvoegsel

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
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
#### <a name="example-sample-data-set-with-version"></a>Voorbeeld: Voorbeeldgegevensset (met versie)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
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

#### <a name="example-dynamic-paths-for-s3"></a>Voorbeeld: Dynamische paden voor S3
In het Hallo-voorbeeld gebruiken we vaste waarden voor eigenschappen van sleutel en bucketName in Hallo Amazon S3 gegevensset.

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

U kunt Data Factory Hallo-sleutel en bucketName dynamisch tijdens runtime berekenen met behulp van systeemvariabelen zoals SliceStart hebben.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

U kunt doen hello dezelfde voor Hallo voorvoegsel-eigenschap van een gegevensset Amazon S3. Zie [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md) voor een lijst van ondersteunde functies en variabelen.

Zie voor meer informatie [Amazon S3 connector artikel](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Systeem bronnen in de kopieerbewerking
Als u gegevens vanaf Amazon S3 kopieert, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**FileSystemSource**, en opgeven na eigenschappen in Hallo **bron** sectie :


| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| Recursieve |Hiermee geeft u op of toorecursively lijst S3 onder Hallo directory-objecten. |waar/onwaar |Nee |


#### <a name="example"></a>Voorbeeld


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
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
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

Zie voor meer informatie [Amazon S3 connector artikel](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).

## <a name="file-system"></a>Bestandssysteem


### <a name="linked-service"></a>Gekoppelde service
U kunt een lokaal bestand system tooan Azure data factory Hello koppelen **On-Premises bestandsserver** gekoppelde service. Hallo volgende tabel bevat beschrijvingen van JSON-elementen die specifiek toohello bestandsserver On-Premises gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Zorg ervoor dat de eigenschap type hello te is ingesteld**OnPremisesFileServer**. |Ja |
| host |Hiermee geeft u het hoofdpad Hallo van Hallo map die u toocopy wilt. Gebruik Hallo escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks. Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden. |Ja |
| gebruikers-id |Hallo-ID van het Hallo-gebruiker met toegang toohello server opgeven. |Nee (als u ervoor encryptedCredential kiest) |
| wachtwoord |Hallo-wachtwoord voor gebruiker hello (gebruikersnaam) opgeven. |Nee (als u encryptedCredential kiezen |
| encryptedCredential |Geef referenties op Hallo versleuteld die u door de cmdlet New-AzureRmDataFactoryEncryptValue Hallo kunt ophalen. |Nee (als u toospecify gebruikersnaam en wachtwoord als tekst zonder opmaak kiezen) |
| gatewayName |Geeft de naam Hallo van Hallo gateway dat Data Factory tooconnect toohello lokale bestandsserver moeten gebruiken. |Ja |

#### <a name="sample-folder-path-definitions"></a>Voorbeeld map pad definities 
| Scenario | In de definitie van de gekoppelde service host | folderPath in de definitie van gegevensset |
| --- | --- | --- |
| Lokale map op de Data Management Gateway-apparaat: <br/><br/>Voorbeelden: D:\\ \* of D:\folder\subfolder\\* |D:\\ \\ (voor Data Management Gateway 2.0 en hoger) <br/><br/> localhost (voor oudere versies dan Data Management Gateway 2.0) |. \\ \\ of de map\\\\submap (voor Data Management Gateway 2.0 en hoger) <br/><br/>D:\\ \\ of D:\\\\map\\\\submap (voor gatewayversie lager dan 2.0) |
| Externe gedeelde map: <br/><br/>Voorbeelden: \\ \\MijnServer\\delen\\ \* of \\ \\MijnServer\\delen\\map\\submap\\* |\\\\\\\\MijnServer\\\\delen |. \\ \\ of de map\\\\submap |


#### <a name="example-using-username-and-password-in-plain-text"></a>Voorbeeld: Met behulp van gebruikersnaam en wachtwoord in tekst zonder opmaak

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a>Voorbeeld: Encryptedcredential gebruiken

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Zie voor meer informatie [bestandssysteem connector artikel](data-factory-onprem-file-system-connector.md#linked-service-properties).

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset bestandssysteem set Hallo **type** van Hallo gegevensset te**FileShare**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| folderPath |Hiermee geeft u Hallo subpad toohello map. Gebruik Hallo escape-teken ' \' voor speciale tekens in Hallo-tekenreeks. Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.<br/><br/>U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden. |Ja |
| fileName |Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo. Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.<br/><br/>FileName is opgegeven voor een uitvoergegevensset, heeft Hallo naam van Hallo gegenereerd bestand Hallo na indeling: <br/><br/>`Data.<Guid>.txt`(Voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Nee |
| fileFilter |Geef dat een filter toobe tooselect gebruikt een subset van de bestanden in Hallo folderPath in plaats van alle bestanden. <br/><br/>Toegestane waarden zijn: `*` (meerdere tekens) en `?` (willekeurig teken).<br/><br/>Voorbeeld 1: 'fileFilter":" * .log '<br/>Voorbeeld 2: 'fileFilter': 2016 - 1-?. txt'<br/><br/>Houd er rekening mee dat fileFilter is van toepassing op een bestandsshare-invoergegevensset. |Nee |
| partitionedBy |U kunt partitionedBy toospecify een dynamische folderPath/bestandsnaam gebruiken voor timeseries gegevens. Een voorbeeld is folderPath geparametriseerde voor elk uur van gegevens. |Nee |
| Indeling | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set Hallo **type** eigenschap onder indeling tooone van deze waarden. Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. <br><br> Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan. |Nee |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**; en ondersteunde niveaus: **optimale** en **snelst**. Zie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |

> [!NOTE]
> U kunt geen bestandsnaam en fileFilter gelijktijdig gebruiken.

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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

Zie voor meer informatie [bestandssysteem connector artikel](data-factory-onprem-file-system-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Systeem bronnen in de kopieerbewerking
Als u gegevens uit bestandssysteem kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**FileSystemSource**, en opgeven na eigenschappen in Hallo **bron** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| Recursieve |Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo. |True, False (standaard) |Nee |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Zie voor meer informatie [bestandssysteem connector artikel](data-factory-onprem-file-system-connector.md#copy-activity-properties).

### <a name="file-system-sink-in-copy-activity"></a>Bestandssysteem Sink in de kopieerbewerking
Als u gegevens tooFile System kopieert, stelt u Hallo **type sink** Hallo kopieeractiviteit te**FileSystemSink**, en opgeven na eigenschappen in Hallo **sink** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| copyBehavior |Hallo kopie gedrag definieert wanneer Hallo bron BlobSource of bestandssysteem. |**PreserveHierarchy:** Hallo bestandshiërarchie in de doelmap Hallo behouden blijft. Dat wil zeggen, is relatief pad Hallo van Hallo bestand toohello bron bronmap hetzelfde als het relatieve pad van Hallo bestand toohello doel doelmap Hallo Hallo.<br/><br/>**FlattenHierarchy:** alle bestanden uit de bronmap Hallo worden gemaakt in Hallo eerste niveau van de doelmap. Hallo doelbestanden worden gemaakt met een automatisch gegenereerde naam.<br/><br/>**MergeFiles:** alle bestanden uit map Hallo-tooone bronbestand worden samengevoegd. Als Hallo bestand naam/blob-naam wordt opgegeven, is Hallo Samengevoegde bestandsnaam Hallo opgegeven naam. Anders is het een automatisch gegenereerde naam. |Nee |
Automatische-

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Zie voor meer informatie [bestandssysteem connector artikel](data-factory-onprem-file-system-connector.md#copy-activity-properties).

## <a name="ftp"></a>FTP

### <a name="linked-service"></a>Gekoppelde service
toodefine een FTP-service, set Hallo gekoppeld **type** Hallo gekoppelde service te**FtpServer**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist | Standaard |
| --- | --- | --- | --- |
| host |Naam of IP-adres van Hallo FTP-Server |Ja |&nbsp; |
| authenticationType |Geef een verificatie |Ja |Basic, anonieme |
| gebruikersnaam |Gebruiker met toegang toohello FTP-server |Nee |&nbsp; |
| wachtwoord |Wachtwoord voor gebruiker hello (username) |Nee |&nbsp; |
| encryptedCredential |Versleutelde referentie tooaccess Hallo FTP-server |Nee |&nbsp; |
| gatewayName |Naam van Hallo Data Management Gateway gateway tooconnect tooan lokale FTP-server |Nee |&nbsp; |
| poort |Poort op welke Hallo FTP-server luistert |Nee |21 |
| enableSsl |Opgeven of toouse FTP via SSL/TLS-kanaal |Nee |De waarde True |
| enableServerCertificateValidation |Opgeven of tooenable server SSL certificaatcontrole wanneer FTP via SSL/TLS-kanaal |Nee |De waarde True |

#### <a name="example-using-anonymous-authentication"></a>Voorbeeld: Anonieme verificatie gebruikt

```json
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

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a>Voorbeeld: Met behulp van gebruikersnaam en wachtwoord in tekst zonder opmaak voor basisverificatie

```json
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

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a>Voorbeeld: Met behulp van poort, enableSsl, enableServerCertificateValidation

```json
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

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a>Voorbeeld: EncryptedCredential gebruiken voor verificatie en gateway

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

Zie voor meer informatie [FTP-connector](data-factory-ftp-connector.md#linked-service-properties) artikel.

### <a name="dataset"></a>Gegevensset
toodefine een FTP-gegevensset, set Hallo **type** van Hallo gegevensset te**FileShare**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| folderPath |Submap pad toohello. Gebruik van escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks. Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.<br/><br/>U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden. |Ja 
| fileName |Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo. Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.<br/><br/>Wanneer fileName niet voor een uitvoergegevensset opgegeven is, zou Hallo van Hallo gegenereerd bestand in worden Hallo volgt deze indeling: <br/><br/>Gegevens. <Guid>.txt (voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nee |
| fileFilter |Geef dat een filter toobe tooselect gebruikt een subset van de bestanden in Hallo folderPath in plaats van alle bestanden.<br/><br/>Toegestane waarden zijn: `*` (meerdere tekens) en `?` (willekeurig teken).<br/><br/>Voorbeelden 1:`"fileFilter": "*.log"`<br/>Voorbeeld 2:`"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter geldt voor een invoergegevensset bestandsshare. Deze eigenschap wordt niet ondersteund met HDFS. |Nee |
| partitionedBy |partitionedBy mag gebruikte toospecify een dynamische folderPath bestandsnaam op van de reeksgegevens. Bijvoorbeeld, folderPath geparametriseerde voor elk uur van gegevens. |Nee |
| Indeling | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set Hallo **type** eigenschap onder indeling tooone van deze waarden. Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. <br><br> Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan. |Nee |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**; en ondersteunde niveaus: **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |
| useBinaryTransfer |Geef binaire overdrachtsmodus of gebruiken. De waarde True voor binaire modus en ONWAAR ASCII. Standaardwaarde: True. Deze eigenschap kan alleen worden gebruikt wanneer de bijbehorende gekoppelde-servicetype is van het type: FtpServer. |Nee |

> [!NOTE]
> bestandsnaam en fileFilter worden niet gelijktijdig gebruikt.

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

Zie voor meer informatie [FTP-connector](data-factory-ftp-connector.md#dataset-properties) artikel.

### <a name="file-system-source-in-copy-activity"></a>Systeem bronnen in de kopieerbewerking
Als u gegevens uit een FTP-server kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**FileSystemSource**, en opgeven na eigenschappen in Hallo **bron** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| Recursieve |Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo. |True, False (standaard) |Nee |

#### <a name="example"></a>Voorbeeld

```json
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
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

Zie voor meer informatie [FTP-connector](data-factory-ftp-connector.md#copy-activity-properties) artikel.


## <a name="hdfs"></a>HDFS

### <a name="linked-service"></a>Gekoppelde service
een HDFS toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**Hdfs**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **Hdfs** |Ja |
| URL |URL toohello HDFS |Ja |
| authenticationType |Anoniem, of Windows. <br><br> toouse **Kerberos-verificatie** voor HDFS-connector te verwijzen[in deze sectie](#use-kerberos-authentication-for-hdfs-connector) tooset van uw on-premises omgeving dienovereenkomstig. |Ja |
| Gebruikersnaam |Gebruikersnaam voor Windows-verificatie. |Ja (voor Windows-verificatie) |
| wachtwoord |Wachtwoord voor Windows-verificatie. |Ja (voor Windows-verificatie) |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello HDFS gebruiken. |Ja |
| encryptedCredential |[Nieuwe AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) uitvoer van de referentie voor Hallo-toegang. |Nee |

#### <a name="example-using-anonymous-authentication"></a>Voorbeeld: Anonieme verificatie gebruikt

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a>Voorbeeld: Met behulp van Windows-verificatie

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Zie voor meer informatie [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset HDFS set Hallo **type** van Hallo gegevensset te**FileShare**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| folderPath |Pad toohello map. Voorbeeld:`myfolder`<br/><br/>Gebruik van escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks. Bijvoorbeeld: map opgeven voor folder\subfolder,\\\\submap en geef voor d:\samplefolder, d:\\\\Voorbeeldmap.<br/><br/>U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden. |Ja |
| fileName |Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo. Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.<br/><br/>Wanneer fileName niet voor een uitvoergegevensset opgegeven is, zou Hallo van Hallo gegenereerd bestand in worden Hallo volgt deze indeling: <br/><br/>Gegevens. <Guid>.txt (voorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nee |
| partitionedBy |partitionedBy mag gebruikte toospecify een dynamische folderPath bestandsnaam op van de reeksgegevens. Voorbeeld: folderPath geparametriseerde voor elk uur van gegevens. |Nee |
| Indeling | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set Hallo **type** eigenschap onder indeling tooone van deze waarden. Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. <br><br> Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan. |Nee |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**. Ondersteunde niveaus: **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |

> [!NOTE]
> bestandsnaam en fileFilter worden niet gelijktijdig gebruikt.

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Zie voor meer informatie [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) artikel. 

### <a name="file-system-source-in-copy-activity"></a>Systeem bronnen in de kopieerbewerking
Als u gegevens uit HDFS kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**FileSystemSource**, en opgeven na eigenschappen in Hallo **bron** sectie:

**FileSystemSource** ondersteunt Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| Recursieve |Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo. |True, False (standaard) |Nee |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
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
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Zie voor meer informatie [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) artikel.

## <a name="sftp"></a>SFTP


### <a name="linked-service"></a>Gekoppelde service
toodefine een SFTP gekoppelde service, set Hallo **type** Hallo gekoppelde service te**Sftp**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- | --- |
| host | Naam of IP-adres van Hallo SFTP-server. |Ja |
| poort |De poort op welke Hallo SFTP-server luistert. de standaardwaarde Hallo is: 21 |Nee |
| authenticationType |Geef het verificatietype. Toegestane waarden: **Basic**, **SshPublicKey**. <br><br> Raadpleeg te[Using basisverificatie](#using-basic-authentication) en [met behulp van SSH openbare-sleutelauthenticatie](#using-ssh-public-key-authentication) respectievelijk secties over meer eigenschappen en voorbeelden van JSON. |Ja |
| skipHostKeyValidation | Geef op of tooskip sleutel validatie hosten. | Nee. standaardwaarde Hallo: false |
| hostKeyFingerprint | Hallo-vingerafdruk van Hallo hostsleutel opgeven. | Ja als hello `skipHostKeyValidation` toofalse is ingesteld.  |
| gatewayName |Naam van Hallo Data Management Gateway tooconnect tooan een on-premises SFTP-server. | Ja als u kopiëren van gegevens uit een on-premises SFTP-server. |
| encryptedCredential | Versleutelde referentie tooaccess Hallo SFTP-server. Automatisch gegenereerd als u basisverificatie (gebruikersnaam en wachtwoord) of SshPublicKey verificatie (gebruikersnaam + pad naar de persoonlijke sleutel of inhoud) in kopiëren wizard of Hallo ClickOnce pop-up dialoogvenster opgeven. | Nee. Alleen van toepassing wanneer het kopiëren van gegevens uit een on-premises SFTP-server. |

#### <a name="example-using-basic-authentication"></a>Voorbeeld: Met behulp van basisverificatie

Basisverificatie toouse ingesteld `authenticationType` als `Basic`, en geef de volgende eigenschappen afgezien van SFTP connector algemene die zijn geïntroduceerd in de laatste sectie Hallo HALLO hallo:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- | --- |
| gebruikersnaam | Gebruiker met toegang toohello SFTP-server. |Ja |
| wachtwoord | Wachtwoord voor gebruiker hello (gebruikersnaam). | Ja |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Voorbeeld: Basisverificatie met versleutelde referentie **

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a>Met behulp van de openbare-sleutelauthenticatie SSH: **

Basisverificatie toouse ingesteld `authenticationType` als `SshPublicKey`, en geef de volgende eigenschappen afgezien van SFTP connector algemene die zijn geïntroduceerd in de laatste sectie Hallo HALLO hallo:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- | --- |
| gebruikersnaam |Gebruiker met toegang toohello SFTP-server |Ja |
| privateKeyPath | Geef het absolute pad toohello persoonlijke sleutelbestand dat gateway kunt openen. | Geef beide Hallo `privateKeyPath` of `privateKeyContent`. <br><br> Alleen van toepassing wanneer het kopiëren van gegevens uit een on-premises SFTP-server. |
| privateKeyContent | Een geserialiseerde tekenreeks Hallo-inhoud met persoonlijke sleutel. Hallo Wizard kopiëren kunt Hallo persoonlijke sleutelbestand lezen inhoud en extraheren Hallo persoonlijke sleutel automatisch. Als u van andere hulpprogramma/SDK gebruikmaakt, gebruikt u de Hallo privateKeyPath eigenschap. | Geef beide Hallo `privateKeyPath` of `privateKeyContent`. |
| Wachtwoordzin | Hallo pass woordgroep en het wachtwoord toodecrypt Hallo persoonlijke sleutel opgeven als Hallo-sleutelbestand is beveiligd met een wachtwoordzin. | Ja als Hallo-bestand met persoonlijke sleutel wordt beveiligd door een wachtwoordzin. |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Voorbeeld: SshPublicKey verificatie met persoonlijke sleutel inhoud **

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

Zie voor meer informatie [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset SFTP set Hallo **type** van Hallo gegevensset te**FileShare**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| folderPath |Submap pad toohello. Gebruik van escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks. Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.<br/><br/>U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden. |Ja |
| fileName |Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo. Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.<br/><br/>Wanneer fileName niet voor een uitvoergegevensset opgegeven is, zou Hallo van Hallo gegenereerd bestand in worden Hallo volgt deze indeling: <br/><br/>Gegevens. <Guid>.txt (voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nee |
| fileFilter |Geef dat een filter toobe tooselect gebruikt een subset van de bestanden in Hallo folderPath in plaats van alle bestanden.<br/><br/>Toegestane waarden zijn: `*` (meerdere tekens) en `?` (willekeurig teken).<br/><br/>Voorbeelden 1:`"fileFilter": "*.log"`<br/>Voorbeeld 2:`"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter geldt voor een invoergegevensset bestandsshare. Deze eigenschap wordt niet ondersteund met HDFS. |Nee |
| partitionedBy |partitionedBy mag gebruikte toospecify een dynamische folderPath bestandsnaam op van de reeksgegevens. Bijvoorbeeld, folderPath geparametriseerde voor elk uur van gegevens. |Nee |
| Indeling | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set Hallo **type** eigenschap onder indeling tooone van deze waarden. Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. <br><br> Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan. |Nee |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**. Ondersteunde niveaus: **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |
| useBinaryTransfer |Geef binaire overdrachtsmodus of gebruiken. De waarde True voor binaire modus en ONWAAR ASCII. Standaardwaarde: True. Deze eigenschap kan alleen worden gebruikt wanneer de bijbehorende gekoppelde-servicetype is van het type: FtpServer. |Nee |

> [!NOTE]
> bestandsnaam en fileFilter worden niet gelijktijdig gebruikt.

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

Zie voor meer informatie [SFTP connector](data-factory-sftp-connector.md#dataset-properties) artikel. 

### <a name="file-system-source-in-copy-activity"></a>Systeem bronnen in de kopieerbewerking
Als u gegevens uit een bron SFTP kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**FileSystemSource**, en opgeven na eigenschappen in Hallo **bron** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| Recursieve |Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo. |True, False (standaard) |Nee |



#### <a name="example"></a>Voorbeeld

```json
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
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

Zie voor meer informatie [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) artikel.


## <a name="http"></a>HTTP

### <a name="linked-service"></a>Gekoppelde service
een HTTP toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**Http**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| URL | Basis-URL toohello webserver | Ja |
| authenticationType | Hiermee geeft u het verificatietype Hallo. Toegestane waarden zijn: **anoniem**, **Basic**, **Digest**, **Windows**, **ClientCertificate**. <br><br> Raadpleeg toosections onder deze tabel over meer eigenschappen en voorbeelden van JSON respectievelijk voor deze verificatietypen. | Ja |
| enableServerCertificateValidation | Opgeven of tooenable server SSL certificaatcontrole als bron is een HTTPS-webserver | Nee, de standaardwaarde is true |
| gatewayName | Naam van Hallo Data Management Gateway tooconnect tooan lokale HTTP-bron. | Ja als u gegevens kopiëren van een lokale HTTP-bron. |
| encryptedCredential | Versleutelde referentie tooaccess Hallo HTTP-eindpunt. Automatisch wordt gegenereerd wanneer u Hallo verificatiegegevens in kopiëren wizard of Hallo ClickOnce pop-up dialoogvenster configureert. | Nee. Alleen van toepassing wanneer het kopiëren van gegevens uit een lokale HTTP-server. |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Voorbeeld: Met behulp van basisverificatie, verificatiesamenvatting of Windows-verificatie
Stel `authenticationType` als `Basic`, `Digest`, of `Windows`, en geef de volgende eigenschappen afgezien van HTTP-connector algemene werden geïntroduceerd hierboven Hallo Hallo:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| gebruikersnaam | Gebruikersnaam tooaccess Hallo HTTP-eindpunt. | Ja |
| wachtwoord | Wachtwoord voor gebruiker hello (gebruikersnaam). | Ja |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a>Voorbeeld: ClientCertificate verificatie gebruiken

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

**Voorbeeld: met behulp van clientcertificaat:** deze gekoppelde service wordt uw data factory tooan lokale HTTP-webserver. Dit maakt gebruik van een clientcertificaat dat is geïnstalleerd op machine Hallo met Data Management Gateway is geïnstalleerd.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
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

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

Zie voor meer informatie [HTTP connector](data-factory-http-connector.md#linked-service-properties) artikel.

### <a name="dataset"></a>Gegevensset
toodefine een HTTP-gegevensset, set Hallo **type** van Hallo gegevensset te**Http**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| relativeUrl | Een relatieve URL toohello-bron die Hallo gegevens bevat. Wanneer het pad niet wordt opgegeven, wordt alleen Hallo URL die is opgegeven in de servicedefinitie Hallo gekoppeld gebruikt. <br><br> dynamische tooconstruct-URL, kunt u [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md), bijvoorbeeld: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`. | Nee |
| requestMethod | HTTP-methode. Toegestane waarden zijn **ophalen** of **POST**. | Nee. Standaard is `GET`. |
| additionalHeaders | Aanvullende HTTP-aanvraagheaders. | Nee |
| requestBody | Instantie voor HTTP-aanvraag. | Nee |
| Indeling | Als u wilt dat toosimply **Hallo-gegevens ophalen van HTTP-eindpunt als-is** overslaan zonder deze parseren, deze instellingen. <br><br> Als u tooparse Hallo HTTP-antwoord inhoud tijdens het kopiëren wilt, Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. |Nee |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**. Ondersteunde niveaus: **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |

#### <a name="example-using-hello-get-default-method"></a>Voorbeeld: via Hallo GET (standaard)-methode

```json
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
            "interval": 1
        }
    }
}
```

#### <a name="example-using-hello-post-method"></a>Voorbeeld: via Hallo POST-methode

```json
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
            "interval": 1
        }
    }
}
```
Zie voor meer informatie [HTTP connector](data-factory-http-connector.md#dataset-properties) artikel.

### <a name="http-source-in-copy-activity"></a>HTTP-bron in de kopieerbewerking
Als u gegevens van een HTTP-bron kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**HttpSource**, en opgeven na eigenschappen in Hallo **bron** sectie:

| Eigenschap | Beschrijving | Vereist |
| -------- | ----------- | -------- |
| httpRequestTimeout | Hallo-out (TimeSpan) voor Hallo HTTP-aanvraag tooget een antwoord. Hallo time-out tooget een antwoord niet Hallo time-out tooread antwoordgegevens is. | Nee. Standaardwaarde: 00:01:40 |


#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }]
    }
}
```

Zie voor meer informatie [HTTP connector](data-factory-http-connector.md#copy-activity-properties) artikel.

## <a name="odata"></a>OData

### <a name="linked-service"></a>Gekoppelde service
een OData-toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OData**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| URL |URL van Hallo OData-service. |Ja |
| authenticationType |Type verificatie gebruikt tooconnect toohello OData-bron. <br/><br/> Mogelijke waarden zijn voor OData-cloud, anoniem, basis en OAuth (Opmerking momenteel alleen ondersteuning voor Azure Data Factory Azure Active Directory op basis van OAuth). <br/><br/> Mogelijke waarden zijn voor lokale OData, anoniem, basis en Windows. |Ja |
| gebruikersnaam |Geef de gebruikersnaam als u basisverificatie gebruikt. |Ja (alleen als u basisverificatie gebruikt) |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven. |Ja (alleen als u basisverificatie gebruikt) |
| authorizedCredential |Als u van OAuth gebruikmaakt, klikt u op **autoriseren** knop op Hallo Data Factory-Wizard kopiëren of Editor en voer uw referenties wordt Hallo-waarde van deze eigenschap automatisch wordt gegenereerd. |Ja (alleen als u OAuth-verificatie gebruikt) |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello on-premises OData-service gebruiken. Geef alleen als u gegevens uit een on-premises OData-bron kopiëren wilt. |Nee |

#### <a name="example---using-basic-authentication"></a>Voorbeeld: met behulp van basisverificatie
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a>Voorbeeld: anonieme verificatie

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a>Voorbeeld: met behulp van Windows-verificatie toegang tot lokale OData-bron

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a>Voorbeeld: met behulp van OAuth-verificatie toegang tot de cloud OData-bron
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

Zie voor meer informatie [OData-connector](data-factory-odata-connector.md#linked-service-properties) artikel.

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset OData set Hallo **type** van Hallo gegevensset te**ODataResource**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| Pad |Pad toohello OData-bron |Nee |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

Zie voor meer informatie [OData-connector](data-factory-odata-connector.md#dataset-properties) artikel.

### <a name="relational-source-in-copy-activity"></a>Relationele gegevensbron in de kopieerbewerking
Als u gegevens uit een OData-bron kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:

| Eigenschap | Beschrijving | Voorbeeld | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |'? $select = naam, beschrijving & $top = 5 ' |Nee |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

Zie voor meer informatie [OData-connector](data-factory-odata-connector.md#copy-activity-properties) artikel.


## <a name="odbc"></a>ODBC


### <a name="linked-service"></a>Gekoppelde service
toodefine ODBC gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesOdbc**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| connectionString |Hallo niet access credential gedeelte van het Hallo-verbindingsreeks en een optionele versleuteld referentie. Zie de voorbeelden in Hallo uit te voeren. |Ja |
| referentie |Hallo toegang referentie gedeelte van het Hallo-verbindingsreeks die is opgegeven in de indeling van de eigenschapswaarde specifieke stuurprogramma's. Voorbeeld: "Uid =<user ID>; Pwd =<password>; RefreshToken =<secret refresh token>; '. |Nee |
| authenticationType |Type verificatie gebruikt tooconnect toohello ODBC-gegevensarchief. Mogelijke waarden zijn: anonieme en Basic. |Ja |
| gebruikersnaam |Geef de gebruikersnaam als u basisverificatie gebruikt. |Nee |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven. |Nee |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello ODBC-gegevensarchief gebruiken. |Ja |

#### <a name="example---using-basic-authentication"></a>Voorbeeld: met behulp van basisverificatie

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a>Voorbeeld: met behulp van basisverificatie met versleutelde referenties
U kunt versleutelen Hallo-referenties met een Hallo [nieuw AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (versie 1.0 van Azure PowerShell) of [nieuw AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 of een eerdere versie van Hallo Azure PowerShell).  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a>Voorbeeld: Anonieme verificatie gebruikt

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Zie voor meer informatie [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset ODBC set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |Naam van de tabel Hallo in Hallo ODBC-gegevensarchief. |Ja |


#### <a name="example"></a>Voorbeeld

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
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

Zie voor meer informatie [ODBC connector](data-factory-odbc-connector.md#dataset-properties) artikel. 

### <a name="relational-source-in-copy-activity"></a>Relationele gegevensbron in de kopieerbewerking
Als u gegevens uit een ODBC data store kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: `select * from MyTable`. |Ja |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

Zie voor meer informatie [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) artikel.

## <a name="salesforce"></a>SalesForce


### <a name="linked-service"></a>Gekoppelde service
een Salesforce toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**Salesforce**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| environmentUrl | Hallo-URL van de Salesforce-exemplaar opgeven. <br><br> -Standaard is 'https://login.salesforce.com'. <br> -toocopy gegevens van de sandbox, 'https://test.salesforce.com' opgeven. <br> -toocopy gegevens van aangepast domein opgeven, bijvoorbeeld 'https://[domain].my.salesforce.com'. |Nee |
| gebruikersnaam |Geef een gebruikersnaam voor Hallo-gebruikersaccount. |Ja |
| wachtwoord |Geef een wachtwoord voor gebruikersaccount Hallo. |Ja |
| securityToken |Geef een beveiligingstoken voor Hallo-gebruikersaccount. Zie [security token ophalen](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) voor instructies over het tooreset of ophalen van een beveiligingstoken. toolearn over beveiligingstokens in het algemeen Zie [beveiligings- en Hallo API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Ja |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

Zie voor meer informatie [Salesforce-connector](data-factory-salesforce-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een Salesforce-gegevensset set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |Naam van de tabel Hallo in Salesforce. |Nee (als een **query** van **RelationalSource** is opgegeven) |

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
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

Zie voor meer informatie [Salesforce-connector](data-factory-salesforce-connector.md#dataset-properties) artikel. 

### <a name="relational-source-in-copy-activity"></a>Relationele gegevensbron in de kopieerbewerking
Als u gegevens uit Salesforce kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |Een SQL-92-query of [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query. Bijvoorbeeld `select * from MyTable__c`. |Nee (als hello **tableName** Hallo **gegevensset** is opgegeven) |

#### <a name="example"></a>Voorbeeld  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
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
        }]
    }
}
```

> [!IMPORTANT]
> Hallo '__c' onderdeel Hallo API-naam is vereist voor elk object dat aangepast.

Zie voor meer informatie [Salesforce-connector](data-factory-salesforce-connector.md#copy-activity-properties) artikel. 

## <a name="web-data"></a>Web-gegevens 

### <a name="linked-service"></a>Gekoppelde service
een Web toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**Web**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| URL |URL toohello webbron |Ja |
| authenticationType |Anonieme. |Ja |
 

#### <a name="example"></a>Voorbeeld


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

Zie voor meer informatie [Web tabel connector](data-factory-web-table-connector.md#linked-service-properties) artikel. 

### <a name="dataset"></a>Gegevensset
toodefine een gegevensset Web set Hallo **type** van Hallo gegevensset te**WebTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie: 

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| type |Type Hallo gegevensset. te moet worden ingesteld**WebTable** |Ja |
| Pad |Een relatieve URL toohello-bron die Hallo tabel bevat. |Nee. Wanneer het pad niet wordt opgegeven, wordt alleen Hallo URL die is opgegeven in de servicedefinitie Hallo gekoppeld gebruikt. |
| Index |Hallo index van de tabel Hallo in Hallo resource. Zie [Get-index van een tabel in een HTML-pagina](#get-index-of-a-table-in-an-html-page) sectie voor stappen toogetting index van een tabel in een HTML-pagina. |Ja |

#### <a name="example"></a>Voorbeeld

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
            "interval": 1
        }
    }
}
```

Zie voor meer informatie [Web tabel connector](data-factory-web-table-connector.md#dataset-properties) artikel. 

### <a name="web-source-in-copy-activity"></a>Webbron in kopieerbewerking
Als u gegevens uit een tabel web kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**WebSource**. Op dit moment wanneer Hallo-bron in de kopieerbewerking is van het type **WebSource**, zonder aanvullende eigenschappen worden ondersteund.

#### <a name="example"></a>Voorbeeld

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }]
    }
}
```

Zie voor meer informatie [Web tabel connector](data-factory-web-table-connector.md#copy-activity-properties) artikel. 

## <a name="compute-environments"></a>COMPUTE-OMGEVINGEN
Hallo bevat volgende tabel berekeningsomgevingen hello wordt ondersteund door de Data Factory en Hallo transformatie-activiteiten die kunnen worden uitgevoerd op deze. Klik op de koppeling Hallo voor Hallo compute u bent geïnteresseerd in toosee Hallo JSON-schema voor de gekoppelde service toolink het tooa data factory. 

| Compute-omgeving | Activiteiten |
| --- | --- |
| [HDInsight-cluster op aanvraag](#on-demand-azure-hdinsight-cluster) of [uw eigen HDInsight-cluster](#existing-azure-hdinsight-cluster) |[Aangepaste activiteit .NET](#net-custom-activity), [Hive-activiteit](#hdinsight-hive-activity), [activiteit varkens] (#hdinsight-pig-activiteit, [MapReduce-activiteit](#hdinsight-mapreduce-activity), [Hadoop-streaming activiteit](#hdinsight-streaming-activityd), [Spark activiteit](#hdinsight-spark-activity) |
| [Azure Batch](#azure-batch) |[.NET aangepaste activiteit](#net-custom-activity) |
| [Azure Machine Learning](#azure-machine-learning) | [Machine Learning-Batchuitvoeringsactiviteit](#machine-learning-batch-execution-activity), [Machine Learning eigen Update Resourceactiviteit](#machine-learning-update-resource-activity) |
| [Azure Data Lake Analytics](#azure-data-lake-analytics) |[Data Lake Analytics U-SQL](#data-lake-analytics-u-sql-activity) |
| [Azure SQL Database](#azure-sql-database-1), [Azure SQL datawarehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1) |[Opgeslagen procedure](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a>Azure HDInsight-cluster op aanvraag
Hello Azure Data Factory-service kan een Windows, Linux-gebaseerde bellen op HDInsight-cluster tooprocess gegevens automatisch worden gemaakt. Hallo-cluster wordt gemaakt in dezelfde regio bevinden als Hallo storage-account (de eigenschap linkedServiceName in Hallo JSON) die zijn gekoppeld aan cluster Hallo Hallo. U kunt uitvoeren Hallo activiteiten voor gegevenstransformatie volgen op deze gekoppelde service: [aangepaste activiteit .NET](#net-custom-activity), [Hive-activiteit](#hdinsight-hive-activity), [varkens activiteit] (#hdinsight-pig-activiteit, [MapReduce-activiteit ](#hdinsight-mapreduce-activity), [Hadoop-streaming activiteit](#hdinsight-streaming-activityd), [Spark activiteit](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Gekoppelde service 
Hallo volgende tabel bevat beschrijvingen van Hallo-eigenschappen die in hello Azure JSON-definitie van een gekoppelde HDInsight-service op aanvraag gebruikt.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |de eigenschap type Hello te moet worden ingesteld**HDInsightOnDemand**. |Ja |
| De clustergrootte |Aantal knooppunten in cluster Hallo worker/gegevens. Hallo HDInsight-cluster wordt gemaakt met 2 hoofdknooppunten samen met het aantal worker-knooppunten die u voor deze eigenschap opgeeft Hallo. Hallo-knooppunten zijn met een grootte van Standard_D3 met 4 kernen, zodat een cluster met 4 worker-knooppunten 24 kernen duurt (4\*4 = 16 cores voor worker-knooppunten plus 2\*4 = 8 cores voor hoofdknooppunten). Zie [maken Linux gebaseerde Hadoop-clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) voor meer informatie over Hallo Standard_D3 laag. |Ja |
| TimeToLive |Hallo toegestane niet-actieve tijd voor Hallo bellen op HDInsight-cluster. Hiermee geeft u op hoe lang Hallo bellen op HDInsight-cluster na voltooiing van een activiteit die wordt uitgevoerd als er geen actieve taken in het cluster Hallo actief blijft.<br/><br/>Bijvoorbeeld, als een activiteit die wordt uitgevoerd, 6 minuten en timetolive duurt is ingesteld too5 minuten, Hallo cluster blijft actief gedurende vijf minuten na Hallo 6 minuten van de verwerking van Hallo activiteit die wordt uitgevoerd. Als een andere activiteit die wordt uitgevoerd met Hallo 6 minuten venster wordt uitgevoerd, wordt verwerkt door Hallo hetzelfde cluster.<br/><br/>Maken van een HDInsight-cluster op aanvraag is een dure bewerking (kan even duren), dus gebruik deze instelling als de prestaties van een gegevensfactory nodig tooimprove door een HDInsight-cluster op aanvraag opnieuw te gebruiken.<br/><br/>Als u timetolive waarde too0 instelt, wordt Hallo cluster verwijderd zodra Hallo activiteit worden uitgevoerd verwerkt. Op Hallo anderzijds, als u een hoge waarde instelt Hallo cluster mogelijk blijven inactief onnodig wat resulteert in hoge kosten. Het is daarom belangrijk dat u Hallo geschikte waarde op basis van uw behoeften.<br/><br/>Meerdere pijplijnen kunnen delen hetzelfde exemplaar van Hallo bellen op HDInsight-cluster Hallo als de waarde van de eigenschap timetolive Hallo op de juiste wijze is ingesteld |Ja |
| Versie |De versie van Hallo HDInsight-cluster. Zie voor meer informatie [HDInsight-versies ondersteund in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). |Nee |
| linkedServiceName |Een gekoppelde Azure Storage-service toobe door Hallo op aanvraag cluster gebruikt voor het opslaan en verwerken van gegevens. <p>Op dit moment kunt maken u een HDInsight-cluster op aanvraag die gebruikmaakt van een Azure Data Lake Store als Hallo opslag niet. Als u toostore Hallo resultaatgegevens uit HDInsight worden verwerkt in een Azure Data Lake Store wilt, gebruikt u een Kopieeractiviteit toocopy Hallo gegevens van hello Azure Blob Storage toohello Azure Data Lake Store.</p>  | Ja |
| additionalLinkedServiceNames |Hiermee geeft u extra opslagaccounts voor Hallo HDInsight gekoppelde service zodat Hallo Data Factory-service namens jou registreren kunt. |Nee |
| besturingssysteemtype |Type besturingssysteem. Toegestane waarden zijn: (standaard) voor Windows en Linux |Nee |
| hcatalogLinkedServiceName |Hallo-naam van de Azure SQL gekoppelde service die punt toohello HCatalog-database. Hallo bellen op HDInsight-cluster is gemaakt met behulp van hello Azure SQL-database als Hallo metastore. |Nee |

### <a name="json-example"></a>JSON-voorbeeld
Hallo volgende JSON definieert een service op aanvraag een gekoppelde HDInsight op basis van Linux. Hallo Data Factory-service maakt automatisch een **op basis van Linux** HDInsight-cluster bij het verwerken van een gegevenssegment. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

Zie voor meer informatie [gekoppelde services berekenen](data-factory-compute-linked-services.md) artikel. 

## <a name="existing-azure-hdinsight-cluster"></a>Bestaande Azure HDInsight-cluster
U kunt een gekoppelde HDInsight-service tooregister uw eigen HDInsight-cluster maken met Data Factory. U kunt uitvoeren Hallo activiteiten voor gegevenstransformatie volgen op deze gekoppelde service: [aangepaste activiteit .NET](#net-custom-activity), [Hive-activiteit](#hdinsight-hive-activity), [varkens activiteit] (#hdinsight-pig-activiteit, [MapReduce activiteit](#hdinsight-mapreduce-activity), [Hadoop-streaming activiteit](#hdinsight-streaming-activityd), [Spark activiteit](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Gekoppelde service
Hallo volgende tabel bevat beschrijvingen van Hallo-eigenschappen die in hello Azure JSON-definitie van een gekoppelde HDInsight-service gebruikt.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |de eigenschap type Hello te moet worden ingesteld**HDInsight**. |Ja |
| clusterUri |Hallo-URI van Hallo HDInsight-cluster. |Ja |
| gebruikersnaam |Geef het Hallo-naam van Hallo gebruiker toobe tooconnect tooan bestaand HDInsight-cluster gebruikt. |Ja |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo opgeven. |Ja |
| linkedServiceName | Naam van Hallo gekoppelde Azure Storage-service die toohello Azure blob-opslag verwijst gebruikt door Hallo HDInsight-cluster. <p>Op dit moment kunt opgeven u niet dat een Azure Data Lake Store gekoppelde service voor deze eigenschap. U mogelijk toegang tot gegevens in Azure Data Lake Store Hallo van Hive/Pig-scripts als Hallo HDInsight-cluster toegang tot toohello Data Lake Store heeft. </p>  |Ja |

Zie voor versies van HDInsight-clusters ondersteund [ondersteunde versies van HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). 

#### <a name="json-example"></a>JSON-voorbeeld

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a>Azure Batch
U kunt een Azure Batch gekoppelde service tooregister een Batch-pool van virtuele machines (VM's) maken met een data factory. U kunt aangepaste .NET-activiteiten met behulp van Azure Batch of Azure HDInsight kunt uitvoeren. U kunt uitvoeren een [aangepaste activiteit .NET](#net-custom-activity) op deze gekoppelde service. 

### <a name="linked-service"></a>Gekoppelde service
Hallo volgende tabel bevat beschrijvingen van Hallo-eigenschappen die in hello Azure JSON-definitie van een gekoppelde Azure-Batch-service gebruikt.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |de eigenschap type Hello te moet worden ingesteld**AzureBatch**. |Ja |
| Accountnaam |Naam van hello Azure Batch-account. |Ja |
| accessKey |De toegangssleutel voor hello Azure Batch-account. |Ja |
| Groepsnaam |Naam van het Hallo-pool van virtuele machines. |Ja |
| linkedServiceName |Naam van Hallo gekoppelde Azure Storage-service die is gekoppeld aan deze gekoppelde Azure-Batch-service. Deze gekoppelde service wordt gebruikt voor tijdelijke bestanden toorun Hallo activiteit en opslaan van logboekbestanden voor het uitvoeren van activiteit Hallo vereist. |Ja |


#### <a name="json-example"></a>JSON-voorbeeld

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a>Azure Machine Learning
U een Azure Machine Learning gekoppelde service tooregister op een Machine Learning score-eindpunt met een gegevensfactory maken. Twee activiteiten voor gegevenstransformatie die kunnen worden uitgevoerd op deze gekoppelde service: [Machine Learning-Batchuitvoeringsactiviteit](#machine-learning-batch-execution-activity), [Resourceactiviteit voor Machine Learning Update](#machine-learning-update-resource-activity). 

### <a name="linked-service"></a>Gekoppelde service
Hallo volgende tabel bevat beschrijvingen van Hallo-eigenschappen die in hello Azure JSON-definitie van een Azure Machine Learning gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| Type |Hallo type eigenschap moet worden ingesteld op: **AzureML**. |Ja |
| mlEndpoint |Hallo URL voor batchscores. |Ja |
| apiKey |Hallo gepubliceerde werkruimtemodel op de API. |Ja |

#### <a name="json-example"></a>JSON-voorbeeld

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a>Azure Data Lake Analytics
U maakt een **Azure Data Lake Analytics** service toolink een Azure Data Lake Analytics compute-service tooan Azure data factory gekoppeld voordat u Hallo [Data Lake Analytics U-SQL-activiteit](data-factory-usql-activity.md) in een pijplijn .

### <a name="linked-service"></a>Gekoppelde service

Hallo volgende tabel bevat beschrijvingen van Hallo-eigenschappen die in Hallo JSON-definitie van een service van Azure Data Lake Analytics is gekoppeld. 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| Type |Hallo type eigenschap moet worden ingesteld op: **AzureDataLakeAnalytics**. |Ja |
| Accountnaam |Azure Data Lake Analytics-accountnaam. |Ja |
| dataLakeAnalyticsUri |Azure Data Lake Analytics-URI. |Nee |
| Autorisatie |Autorisatiecode wordt automatisch opgehaald nadat te klikken op **autoriseren** knop in Hallo Data Factory-Editor en voltooit Hallo OAuth-aanmelding. |Ja |
| subscriptionId |Azure-abonnement-id |Nee (als dit niet is opgegeven, abonnement van Hallo data factory wordt gebruikt). |
| resourceGroupName |Naam van een Azure-resourcegroep |Nee (als dit niet is opgegeven, brongroep van Hallo data factory wordt gebruikt). |
| sessie-id |sessie-id van Hallo OAuth-autorisatie-sessie. Elke sessie-id is uniek en kan slechts eenmaal worden gebruikt. Wanneer u Hallo Data Factory-Editor gebruikt, wordt deze ID is automatisch gegenereerd. |Ja |


#### <a name="json-example"></a>JSON-voorbeeld
Hallo volgende voorbeeld bevat JSON-definitie voor een service van Azure Data Lake Analytics is gekoppeld.

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a>Azure SQL Database
U een Azure SQL gekoppelde service maken en deze gebruiken met Hallo [activiteit opgeslagen Procedure](#stored-procedure-activity) tooinvoke een opgeslagen procedure uit een Data Factory-pijplijn. 

### <a name="linked-service"></a>Gekoppelde service
een Azure SQL Database toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureSqlDatabase**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| connectionString |Geef informatie tooconnect toohello Azure SQL Database-exemplaar voor de eigenschap connectionString Hallo nodig. |Ja |

#### <a name="json-example"></a>JSON-voorbeeld

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Zie [Azure SQL-Connector](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over deze gekoppelde service.

## <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse
U een Azure SQL Data Warehouse gekoppelde service maken en deze gebruiken met Hallo [activiteit opgeslagen Procedure](data-factory-stored-proc-activity.md) tooinvoke een opgeslagen procedure uit een Data Factory-pijplijn. 

### <a name="linked-service"></a>Gekoppelde service
een Azure SQL Data Warehouse toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureSqlDW**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:  

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| connectionString |Geef informatie tooconnect toohello Azure SQL Data Warehouse-exemplaar voor de eigenschap connectionString Hallo nodig. |Ja |

#### <a name="json-example"></a>JSON-voorbeeld

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Zie voor meer informatie [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) artikel. 

## <a name="sql-server"></a>SQL Server 
U een SQL Server gekoppelde service maken en deze gebruiken met Hallo [activiteit opgeslagen Procedure](data-factory-stored-proc-activity.md) tooinvoke een opgeslagen procedure uit een Data Factory-pijplijn. 

### <a name="linked-service"></a>Gekoppelde service
Maken van een gekoppelde service van het type **OnPremisesSqlServer** toolink een lokale SQL Server-database tooa data factory. Hallo volgende tabel biedt een beschrijving voor de service voor JSON-elementen specifieke tooon-premises SQL Server gekoppeld.

Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooSQL gekoppelde Server-service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **OnPremisesSqlServer**. |Ja |
| connectionString |Geef connectionString informatie nodig tooconnect toohello lokale SQL Server-database met behulp van de SQL-verificatie of de Windows-verificatie. |Ja |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale SQL Server-database gebruiken. |Ja |
| gebruikersnaam |Geef de gebruikersnaam als u Windows-verificatie gebruikt. Voorbeeld: **domainname\\gebruikersnaam**. |Nee |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven. |Nee |

U kunt referenties met een Hallo versleutelen **nieuw AzureRmDataFactoryEncryptValue** cmdlet en in de verbindingsreeks hello gebruiken, zoals wordt weergegeven in het volgende voorbeeld Hallo (**EncryptedCredential** eigenschap):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Voorbeeld: JSON voor het gebruik van SQL-verificatie

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Voorbeeld: JSON voor het gebruik van Windows-verificatie

Als de gebruikersnaam en wachtwoord zijn opgegeven, gateway maakt gebruik van deze tooimpersonate Hallo opgegeven gebruiker account tooconnect toohello lokale SQL Server-database. Gatewayserver verbindt anders toohello SQL-Server rechtstreeks met de beveiligingscontext Hallo van Gateway (het starten van de account).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Zie voor meer informatie [SQL Server-connector](data-factory-sqlserver-connector.md#linked-service-properties) artikel.

## <a name="data-transformation-activities"></a>ACTIVITEITEN VOOR GEGEVENSTRANSFORMATIE

Activiteit | Beschrijving
-------- | -----------
[HDInsight Hive-activiteit](#hdinsight-hive-activity) | Hallo HDInsight Hive-activiteit in een Data Factory-pijplijn voert Hive-query's op uw eigen of op aanvraag Windows, Linux-gebaseerde HDInsight-cluster. 
[HDInsight Pig-activiteit](#hdinsight-pig-activity) | Hallo HDInsight Pig-activiteit in een Data Factory-pijplijn voert Pig-query's in uw eigen of op aanvraag Windows, Linux-gebaseerde HDInsight-cluster.
[HDInsight MapReduce-activiteit](#hdinsight-mapreduce-activity) | Hallo HDInsight MapReduce-activiteit in een Data Factory-pijplijn voert MapReduce-programma's op uw eigen of op aanvraag Windows, Linux-gebaseerde HDInsight-cluster.
[HDInsight Streaming-activiteit](#hdinsight-streaming-activity) | Hallo Streaming HDInsight-activiteit in een Data Factory-pijplijn voert Hadoop-Streaming programma's op uw eigen of op aanvraag Windows, Linux-gebaseerde HDInsight-cluster.
[HDInsight Spark-activiteit](#hdinsight-spark-activity) | Hallo HDInsight Spark-activiteit in een Data Factory-pijplijn Spark-programma's op uw eigen HDInsight-cluster wordt uitgevoerd. 
[Machine Learning-batchuitvoeringsactiviteit](#machine-learning-batch-execution-activity) | Azure Data Factory kunt u tooeasily maken pijplijnen die gebruikmaken van een gepubliceerde Azure Machine Learning-webservice voor predictive analytics. Hallo-Batchuitvoeringsactiviteit in een Azure Data Factory-pijplijn kunt u een Machine Learning web service toomake voorspellingen op Hallo-gegevens in een batch aanroepen. 
[Machine Learning-activiteit resources bijwerken](#machine-learning-update-resource-activity) | Na verloop van tijd invoer Hallo voorspellende modellen in Machine Learning-score experimenten moeten toobe retrained met nieuwe Hallo gegevenssets. Wanneer u klaar bent met de retraining, wilt u tooupdate Hallo score berekenen voor webservice Hello retrained Machine Learning-model. Met de Hallo zojuist getraind model kunt u Hallo Update Resourceactiviteit tooupdate Hallo-webservice.
[Opgeslagen procedureactiviteit](#stored-procedure-activity) | U kunt de activiteit opgeslagen Procedure hello gebruiken in een Data Factory-pijplijn tooinvoke een opgeslagen procedure in een van volgende gegevensarchieven Hallo: Azure SQL Database, Azure SQL Data Warehouse, SQL Server-Database in uw onderneming of een Azure VM. 
[Data Lake Analytics U-SQL-activiteit](#data-lake-analytics-u-sql-activity) | Data Lake Analytics U-SQL-activiteit wordt een U-SQL-script uitgevoerd op een Azure Data Lake Analytics-cluster.  
[.NET aangepaste activiteit](#net-custom-activity) | Als u gegevens op een manier die niet wordt ondersteund door Data Factory tootransform moet, kunt u een aangepaste activiteit maken met uw eigen logica gegevensverwerking en Hallo activiteit in de pijplijn hello gebruiken. U kunt Hallo aangepaste .NET activiteit toorun met behulp van een Azure Batch-service of een Azure HDInsight-cluster configureren. 

     
## <a name="hdinsight-hive-activity"></a>HDInsight Hive-activiteit
Kunt u de volgende eigenschappen in de definitie van een Hive-activiteit JSON Hallo opgeven. eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **HDInsightHive**. Moet u eerst een gekoppelde HDInsight-service maken en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap. Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooHDInsightHive Hallo:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| Script |Hallo Hive-script inline opgeven |Nee |
| scriptpad |Hallo archief Hive-script in een Azure blob storage en geef Hallo pad toohello bestand. Gebruik de eigenschap 'script' of 'scriptPath'. Beide kunnen niet samen worden gebruikt. Hallo-bestandsnaam is hoofdlettergevoelig. |Nee |
| Hiermee worden gedefinieerd |Geef parameters op als sleutel-waardeparen voor verwijzende binnen Hallo Hive-script met behulp van 'hiveconf' |Nee |

Deze eigenschappen zijn specifieke toohello Hive-activiteit. Andere eigenschappen (buiten Hallo typeProperties sectie) worden ondersteund voor alle activiteiten.   

### <a name="json-example"></a>JSON-voorbeeld
Hallo volgende JSON definieert een HDInsight Hive-activiteit in een pijplijn.  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

Zie voor meer informatie [Hive-activiteit](data-factory-hive-activity.md) artikel. 

## <a name="hdinsight-pig-activity"></a>HDInsight Pig-activiteit
Kunt u de volgende eigenschappen in de definitie van een Pig activiteit JSON Hallo opgeven. eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **HDInsightPig**. Moet u eerst een gekoppelde HDInsight-service maken en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap. Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooHDInsightPig Hallo: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| Script |Hallo Pig-script inline opgeven |Nee |
| scriptpad |Hallo Pig-script opslaat in Azure blob storage en geef Hallo pad toohello-bestand. Gebruik de eigenschap 'script' of 'scriptPath'. Beide kunnen niet samen worden gebruikt. Hallo-bestandsnaam is hoofdlettergevoelig. |Nee |
| Hiermee worden gedefinieerd |Geef parameters op als sleutel-waardeparen voor verwijzende binnen Hallo Pig-script |Nee |

Deze eigenschappen zijn specifieke toohello Pig-activiteit. Andere eigenschappen (buiten Hallo typeProperties sectie) worden ondersteund voor alle activiteiten.   

### <a name="json-example"></a>JSON-voorbeeld

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

Zie voor meer informatie [Pig activiteit](#data-factory-pig-activity.md) artikel. 

## <a name="hdinsight-mapreduce-activity"></a>HDInsight MapReduce-activiteit
Kunt u de volgende eigenschappen in de definitie van een MapReduce-activiteit JSON Hallo opgeven. eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **HDInsightMapReduce**. Moet u eerst een gekoppelde HDInsight-service maken en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap. Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooHDInsightMapReduce Hallo: 

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| jarLinkedService | Naam van Hallo gekoppelde service voor hello Azure Storage dat Hallo JAR-bestand bevat. | Ja |
| jarFilePath | Pad toohello JAR-bestand in hello Azure Storage. | Ja | 
| className | Naam van de hoofdklasse Hallo in Hallo JAR-bestand. | Ja | 
| Argumenten | Een lijst met door komma's gescheiden argumenten voor Hallo MapReduce-programma. Tijdens runtime, ziet u enkele extra argumenten (bijvoorbeeld: mapreduce.job.tags) van Hallo MapReduce-framework. toodifferentiate uw argumenten met Hallo MapReduce argumenten, overweeg het gebruik van zowel de optie als de waarde als argumenten, zoals wordt weergegeven in het volgende voorbeeld Hallo (- s,--invoer,--uitvoer enz., zijn opties onmiddellijk wordt gevolgd door hun waarden) | Nee | 

### <a name="json-example"></a>JSON-voorbeeld

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

Zie voor meer informatie [MapReduce-activiteit](data-factory-map-reduce.md) artikel. 

## <a name="hdinsight-streaming-activity"></a>HDInsight-streamingactiviteit
Kunt u de volgende eigenschappen in de definitie van een Hadoop Streaming activiteit JSON Hallo opgeven. eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **HDInsightStreaming**. Moet u eerst een gekoppelde HDInsight-service maken en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap. Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooHDInsightStreaming Hallo: 

| Eigenschap | Beschrijving | 
| --- | --- |
| toewijzen | Naam van Hallo mapper uitvoerbare. In voorbeeld Hallo is cat.exe Hallo mapper uitvoerbare.| 
| reducer | Naam van Hallo reducer uitvoerbare. In voorbeeld Hallo is wc.exe hello reducer uitvoerbare. | 
| Invoer | Invoerbestand (inclusief locatie) voor Hallo toewijzen. In Hallo-voorbeeld: ' wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt ': adfsample is Hallo blob-container, gegevens-voorbeeld/Gutenberg Hallo-map en davinci.txt Hallo blob is. |
| Uitvoer | Uitvoerbestand (inclusief locatie) voor Hallo reducer. Hallo-uitvoer van Hallo Hadoop streamingtaak geschreven toohello locatie die is opgegeven voor deze eigenschap. |
| filePaths | Paden voor Hallo toewijzen en reducer uitvoerbare bestanden. In Hallo-voorbeeld: 'adfsample/example/apps/wc.exe' adfsample is Hallo blob-container, voorbeeld/apps Hallo-map en wc.exe Hallo uitvoerbare is. | 
| fileLinkedService | Gekoppelde Azure Storage-service die hello Azure-opslag met Hallo-bestanden die zijn opgegeven in Hallo filePaths sectie vertegenwoordigt. | 
| Argumenten | Een lijst met door komma's gescheiden argumenten voor Hallo MapReduce-programma. Tijdens runtime, ziet u enkele extra argumenten (bijvoorbeeld: mapreduce.job.tags) van Hallo MapReduce-framework. toodifferentiate uw argumenten met Hallo MapReduce argumenten, overweeg het gebruik van zowel de optie als de waarde als argumenten, zoals wordt weergegeven in het volgende voorbeeld Hallo (- s,--invoer,--uitvoer enz., zijn opties onmiddellijk wordt gevolgd door hun waarden) | 
| getDebugInfo | Een optioneel element. Wanneer deze tooFailure is ingesteld, worden alleen op fout Hallo logboeken gedownload. Wanneer deze tooAll is ingesteld, worden altijd logboeken ongeacht de uitvoeringsstatus van Hallo gedownload. | 

> [!NOTE]
> Geef een uitvoergegevensset voor Hadoop-Streamingactiviteit Hallo voor Hallo **levert** eigenschap. Deze gegevensset mag alleen een dummy gegevensset die is vereist toodrive Hallo pijplijn planning (elk uur, dagelijks, enz.). Als Hallo activiteit geen invoer nemen, kunt u overslaan geven een invoergegevensset voor de activiteit voor Hallo Hallo **invoer** eigenschap.  

## <a name="json-example"></a>JSON-voorbeeld

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

Zie voor meer informatie [Hadoop-Streamingactiviteit](data-factory-hadoop-streaming-activity.md) artikel. 

## <a name="hdinsight-spark-activity"></a>HDInsight Spark-activiteit
Kunt u de volgende eigenschappen in de definitie van een Spark activiteit JSON Hallo opgeven. eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **HDInsightSpark**. Moet u eerst een gekoppelde HDInsight-service maken en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap. Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooHDInsightSpark Hallo: 

| Eigenschap | Beschrijving | Vereist |
| -------- | ----------- | -------- |
| rootPath | Hello Azure Blob-container en map met Hallo Spark-bestand. Hallo-bestandsnaam is hoofdlettergevoelig. | Ja |
| entryFilePath | Relatief pad toohello Hallo Spark codepakket hoofdmap. | Ja |
| className | Belangrijkste Java/Spark-klasse van de toepassing | Nee | 
| Argumenten | Een lijst met opdrachtregelargumenten toohello Spark programma. | Nee | 
| proxyUser | Hallo account tooimpersonate tooexecute Hallo Spark programma door de gebruiker | Nee | 
| sparkConfig | Configuratie-eigenschappen van Spark. | Nee | 
| getDebugInfo | Geeft aan wanneer Hallo Spark logboekbestanden gekopieerde toohello Azure-opslag die wordt gebruikt door HDInsight-cluster zijn (of) opgegeven door sparkJobLinkedService. Toegestane waarden: None, altijd of fout. Standaardwaarde: geen. | Nee | 
| sparkJobLinkedService | Hallo gekoppelde Azure Storage-service die Hallo Spark taakbestand, afhankelijkheden en Logboeken bevat.  Als u een waarde op voor deze eigenschap niet opgeeft, wordt Hallo opslag die is gekoppeld aan de HDInsight-cluster gebruikt. | Nee |

### <a name="json-example"></a>JSON-voorbeeld

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
Houd er rekening mee Hallo volgende punten: 

- Hallo **type** eigenschap is ingesteld, te**HDInsightSpark**.
- Hallo **rootPath** te is ingesteld,**adfspark\\pyFiles** waarbij adfspark hello Azure Blob-container en pyFiles is map in de container. In dit voorbeeld is hello Azure Blob Storage Hallo die is gekoppeld aan Hallo Spark-cluster. U kunt uploaden Hallo bestand tooa andere Azure-opslag. Als u doet dit, wordt een gekoppelde Azure Storage-service toolink die storage account toohello een gegevensfactory maken. Hallo-naam van gekoppelde Hallo-service vervolgens opgeven als een waarde voor Hallo **sparkJobLinkedService** eigenschap. Zie [Spark activiteitseigenschappen](#spark-activity-properties) voor meer informatie over deze eigenschap en andere eigenschappen die ondersteund worden door Hallo Spark-activiteit.
- Hallo **entryFilePath** toohello is ingesteld **test.py**, namelijk Hallo python-bestand. 
- Hallo **getDebugInfo** eigenschap is ingesteld, te**altijd**, wat betekent dat het Hallo-logboekbestanden zijn altijd gegenereerd (slagen of mislukken).  

    > [!IMPORTANT]
    > U kunt het beste instellen de tooAlways van deze eigenschap niet in een productieomgeving tenzij u een probleem wilt oplossen. 
- Hallo **levert** sectie heeft één uitvoergegevensset. U kunt een uitvoergegevensset moet opgeven, zelfs als Hallo spark programma geen uitvoer produceert. Hallo output dataset stations Hallo planning voor Hallo pijplijn (elk uur, dagelijks, enz.).

Zie voor meer informatie over de activiteit Hallo [Spark activiteit](data-factory-spark.md) artikel.  

## <a name="machine-learning-batch-execution-activity"></a>Machine Learning-batchuitvoeringsactiviteit
Kunt u de volgende eigenschappen in de definitie van een Azure ML-Batch uitvoering activiteit JSON Hallo opgeven. eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **AzureMLBatchExecution**. Moet u een Azure Machine Learning gekoppelde service eerst maakt en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap. Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooAzureMLBatchExecution Hallo:

Eigenschap | Beschrijving | Vereist 
-------- | ----------- | --------
webServiceInput | Hallo gegevensset toobe doorgegeven als invoer voor hello Azure ML webservice. Deze gegevensset moet ook zijn opgenomen in de invoer voor de activiteit Hallo Hallo. |WebServiceInput of webServiceInputs gebruiken. | 
webServiceInputs | Geef gegevenssets toobe doorgegeven als invoer voor hello Azure ML webservice. Als webservice Hallo meerdere invoer neemt, moet u Hallo webServiceInputs eigenschap gebruiken in plaats van Hallo webServiceInput eigenschap. Gegevenssets waarnaar wordt verwezen door Hallo **webServiceInputs** moet ook zijn opgenomen in Hallo activiteit **invoer**. | WebServiceInput of webServiceInputs gebruiken. | 
webServiceOutputs | Hallo gegevenssets die zijn toegewezen als uitvoer voor hello Azure ML-webservice. Hallo-webservice retourneert uitvoergegevens in deze dataset. | Ja | 
globalParameters | Geef waarden voor Hallo web serviceparameters in deze sectie. | Nee | 

### <a name="json-example"></a>JSON-voorbeeld
In dit voorbeeld heeft Hallo activiteit Hallo gegevensset **MLSqlInput** als invoer en **MLSqlOutput** als Hallo uitvoer. Hallo **MLSqlInput** is doorgegeven als een webservice van invoer toohello door Hallo met **webServiceInput** JSON-eigenschap. Hallo **MLSqlOutput** wordt doorgegeven als uitvoer toohello webservice door met de Hallo **webServiceOutputs** JSON-eigenschap. 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

In Hallo JSON voorbeeld hello Azure Machine Learning Web service een lezer en een writer module tooread/gegevens schrijven van gebruikt geïmplementeerd / tooan Azure SQL Database. Deze webservice beschrijft Hallo na vier parameters: servernaam, databasenaam, servergebruikersnaam en wachtwoord voor gebruikersaccount Server-Database.

> [!NOTE]
> Alleen invoer en uitvoer van Hallo AzureMLBatchExecution activiteit kunnen worden doorgegeven als parameters toohello webservice. In Hallo hierboven JSON-codefragment is MLSqlInput bijvoorbeeld een invoer toohello AzureMLBatchExecution activiteit, die is doorgegeven als een invoer toohello webservice via webServiceInput-parameter.

## <a name="machine-learning-update-resource-activity"></a>Machine Learning-activiteit resources bijwerken
Kunt u de volgende eigenschappen in de definitie van een Azure ML Update Resource activiteit JSON Hallo opgeven. eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **AzureMLUpdateResource**. Moet u een Azure Machine Learning gekoppelde service eerst maakt en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap. Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooAzureMLUpdateResource Hallo:

Eigenschap | Beschrijving | Vereist 
-------- | ----------- | --------
trainedModelName | Naam van Hallo retrained model. | Ja |  
trainedModelDatasetName | DataSet aanwijsapparaat toohello iLearner-bestand wordt geretourneerd door Hallo retraining bewerking. | Ja | 

### <a name="json-example"></a>JSON-voorbeeld
Hallo pipeline heeft twee activiteiten: **AzureMLBatchExecution** en **AzureMLUpdateResource**. Hello Azure ML-Batchuitvoering activiteit duurt Hallo trainingsgegevens als invoer en een iLearner-bestand als uitvoer produceert. Hallo activiteit roept Hallo training webservice (trainingsexperiment weergegeven als een webservice) met Hallo invoer trainen van gegevens en Hallo ilearner-bestand van de webservice Hallo ontvangt. Hallo placeholderBlob is een dummy output dataset is vereist door hello Azure Data Factory-service toorun Hallo pijplijn.


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a>Data Lake Analytics U-SQL-activiteit
Kunt u de volgende eigenschappen in de definitie van een U-SQL-activiteit JSON Hallo opgeven. eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **DataLakeAnalyticsU SQL**. Moet u een Azure Data Lake Analytics gekoppelde service maken en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap. Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van Hallo type activiteit tooDataLakeAnalyticsU-SQL: 

| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| scriptPath |Pad toofolder met Hallo U-SQL-script. Naam van bestand Hallo is hoofdlettergevoelig. |Nee (als u een script gebruiken) |
| scriptLinkedService |Gekoppelde service die is gekoppeld aan Hallo-opslag met Hallo script toohello data factory |Nee (als u een script gebruiken) |
| Script |Geef in plaats van het opgeven van scriptPath en scriptLinkedService inline-script. Bijvoorbeeld: 'script': 'Test DATABASE maken'. |Nee (als u scriptPath en scriptLinkedService gebruiken) |
| degreeOfParallelism |maximum aantal knooppunten Hallo toorun Hallo taak tegelijkertijd worden gebruikt. |Nee |
| Prioriteit |Hiermee wordt bepaald welke taken uit in de wachtrij moeten geselecteerde toorun eerst. Hallo Hallo minder, Hallo hogere Hallo prioriteit. |Nee |
| parameters |Parameters voor Hallo U-SQL-script |Nee |

### <a name="json-example"></a>JSON-voorbeeld

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

Zie voor meer informatie [Data Lake Analytics U-SQL-activiteit](data-factory-usql-activity.md). 

## <a name="stored-procedure-activity"></a>Opgeslagen procedureactiviteit
U kunt Hallo volgende eigenschappen in een opgeslagen Procedure activiteit JSON-definitie opgeven. eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **SqlServerStoredProcedure**. U moet een een Hallo na gekoppelde services maken en Hallo naam opgeven van Hallo gekoppelde service als een waarde voor Hallo **linkedServiceName** eigenschap:

- SQL Server 
- Azure SQL Database
- Azure SQL Data Warehouse

Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooSqlServerStoredProcedure Hallo:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| storedProcedureName |Hallo naam opgeven van Hallo opgeslagen procedure in hello Azure SQL database- of Azure SQL Data Warehouse die wordt vertegenwoordigd door Hallo gekoppelde service die Hallo uitvoer tabel gebruikt. |Ja |
| storedProcedureParameters |Geef waarden op voor parameters van opgeslagen procedure. Als u toopass null voor een parameter moet, Hallo syntaxis gebruiken: "param1": null (alle kleine letter). Zie Hallo toolearn voorbeeld over het gebruik van deze eigenschap te volgen. |Nee |

Als u een invoergegevensset opgeeft, moet dit beschikbaar is (in de status 'Gereed') voor Hallo opgeslagen procedure activiteit toorun. Hallo invoergegevensset kan niet worden gebruikt in Hallo opgeslagen procedure als een parameter. Het is alleen gebruikte toocheck Hallo afhankelijkheid voordat begin Hallo procedure-activiteit opgeslagen. U moet een uitvoergegevensset voor een activiteit opgeslagen procedure opgeven. 

Uitvoergegevensset geeft Hallo **planning** voor Hallo opgeslagen procedure activiteit (elk uur, wekelijks, maandelijks, enzovoort). Hallo uitvoergegevensset moet gebruiken een **gekoppelde service** die tooan Azure SQL Database of een Azure SQL Data Warehouse of een SQL Server-Database die u wilt opgeslagen procedure toorun Hallo verwijst. Hallo uitvoergegevensset kan fungeren als een manier toopass Hallo resultaat van Hallo opgeslagen procedure voor verdere verwerking door een andere activiteit ([activiteiten chaining](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in de pijplijn Hallo. Data Factory biedt Hallo-uitvoer van een gegevensset met de opgeslagen procedure toothis echter automatisch niet schrijven. Het is Hallo opgeslagen procedure dat SQL-tabel voor schrijfbewerkingen tooa Hallo uitvoer gegevensset verwijst naar. In sommige gevallen Hallo uitvoergegevensset mag een **dummy gegevensset**, waarmee alleen toospecify Hallo schema voor het uitvoeren van Hallo procedure-activiteit opgeslagen.  

### <a name="json-example"></a>JSON-voorbeeld

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

Zie voor meer informatie [activiteit opgeslagen Procedure](data-factory-stored-proc-activity.md) artikel. 

## <a name="net-custom-activity"></a>Aangepaste .NET-activiteit
U kunt Hallo volgende eigenschappen in een aangepaste activiteit .NET JSON-definitie opgeven. eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **DotNetActivity**. Moet u een gekoppelde HDInsight-service maken of een Azure Batch gekoppelde service en Hallo-naam van Hallo gekoppelde service opgeven als een waarde voor Hallo **linkedServiceName** eigenschap. Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooDotNetActivity Hallo:
 
| Eigenschap | Beschrijving | Vereist |
|:--- |:--- |:--- |
| AssemblyName | Naam van assembly Hallo. In voorbeeld Hallo is: **MyDotnetActivity.dll**. | Ja |
| EntryPoint |Naam van het Hallo-klasse die Hallo IDotNetActivity interface implementeert. In voorbeeld Hallo is: **MyDotNetActivityNS.MyDotNetActivity** waarbij MyDotNetActivityNS Hallo-naamruimte en MyDotNetActivity Hallo-klasse.  | Ja | 
| PackageLinkedService | Naam van Hallo gekoppelde Azure Storage-service die toohello blob-opslag met Hallo aangepaste activiteit zip-bestand verwijst. In voorbeeld Hallo is: **AzureStorageLinkedService**.| Ja |
| PackageFile | Naam van Hallo zip-bestand. In voorbeeld Hallo is: **customactivitycontainer/MyDotNetActivity.zip**. | Ja |
| extendedProperties | Uitgebreide eigenschappen die u kunt definiëren en geeft op toohello .NET-code. In dit voorbeeld Hallo **SliceStart** variabele tooa-waarde op basis van Hallo SliceStart systeemvariabele is ingesteld. | Nee | 

### <a name="json-example"></a>JSON-voorbeeld

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

Zie voor gedetailleerde informatie [gebruik van aangepaste activiteiten in de Data Factory](data-factory-use-custom-activities.md) artikel. 

## <a name="next-steps"></a>Volgende stappen
Zie de volgende zelfstudies Hallo: 

- [Zelfstudie: een pijplijn maken met een kopieeractiviteit](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [Zelfstudie: een pijplijn maken met een hive-activiteit](data-factory-build-your-first-pipeline-using-editor.md)