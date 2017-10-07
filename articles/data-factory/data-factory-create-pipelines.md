---
title: aaaCreate/planning pijplijnen, keten activiteiten in de Data Factory | Microsoft Docs
description: Informatie over een pijplijn gegevens in Azure Data Factory toomove toocreate en gegevens transformeren. Maak een gegevensgestuurde werkstroomgegevens tooproduce gereed toouse.
keywords: pijplijn voor gegevens, gegevensgestuurde werkstroom
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 13b137c7-1033-406f-aea7-b66f25b313c0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: shlo
ms.openlocfilehash: 4a0fc20f98ce6453c16955e97fddb891926c173a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a>Pijplijnen en activiteiten in Azure Data Factory
In dit artikel helpt u begrijpen pijplijnen en activiteiten in Azure Data Factory en ze tooconstruct end-to-end gegevensgestuurde werkstromen voor de verplaatsing van gegevens en scenario's voor gegevensverwerking gebruiken.  

> [!NOTE]
> In dit artikel wordt ervan uitgegaan dat u hebt doorlopen [inleiding tooAzure Data Factory](data-factory-introduction.md). Als u geen hands-op-ervaring met het maken van data Factory, gaan via [data transformation zelfstudie](data-factory-build-your-first-pipeline.md) en/of [data movement zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) zou u in dit artikel beter inzicht te geven.  

## <a name="overview"></a>Overzicht
Een gegevensfactory kan één of meer pijplijnen hebben. Een pijplijn is een logische groep activiteiten die samen een taak uitvoeren. Hallo-activiteiten in een pijplijn definiëren tooperform acties op uw gegevens. U kunt bijvoorbeeld een kopie toocopy activiteitsgegevens van een lokale SQL Server tooan Azure Blob Storage. Vervolgens gebruikt u een Hive-activiteit die wordt een Hive-script uitgevoerd op gegevens in een Azure HDInsight-cluster tooprocess/transformatie van tooproduce uitvoergegevens voor Hallo blob-opslag. Gebruik tot slot een tweede kopie activiteit toocopy Hallo uitvoer gegevens tooan Azure SQL Data Warehouse boven op welke business intelligence (BI) rapportageoplossingen zijn gebouwd. 

Een activiteit kan nul of meer [invoergegevenssets](data-factory-create-datasets.md) hebben en een of meer [uitvoergegevenssets](data-factory-create-datasets.md) produceren. Hallo volgende diagram toont Hallo relatie tussen pipeline, activiteit en gegevensset in Gegevensfactory: 

![Relatie tussen pipeline, activiteit en gegevensset](media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

Een pijplijn, kunt u activiteiten toomanage als een set in plaats van elk afzonderlijk. U kunt bijvoorbeeld implementeren, plannen, onderbreken en hervatten van een pijplijn, in plaats van het omgaan met activiteiten in de pijplijn Hallo onafhankelijk.

Data Factory ondersteunt twee soorten activiteiten: activiteiten voor gegevensverplaatsing en activiteiten voor gegevenstransformatie. Elke activiteit kunt hebben van nul of meer invoer [gegevenssets](data-factory-create-datasets.md) en een of meer uitvoergegevenssets te produceren.

Een invoergegevensset vertegenwoordigt Hallo invoer voor een activiteit in de pijplijn Hallo en een uitvoergegevensset Hallo uitvoer voor Hallo activiteit vertegenwoordigt. Met gegevenssets worden gegevens binnen andere gegevensarchieven geïdentificeerd, waaronder tabellen, bestanden, mappen en documenten. Nadat u een gegevensset hebt gemaakt, kunt u deze gebruiken voor activiteiten in een pijplijn. Een gegevensset kan bijvoorbeeld een gegevensset voor invoer/uitvoer van een kopieeractiviteit of een HDInsightHive-activiteit zijn. Zie het artikel [Gegevenssets in Azure Data Factory](data-factory-create-datasets.md) voor meer informatie over gegevenssets.

### <a name="data-movement-activities"></a>Activiteiten voor gegevensverplaatsing
Kopieeractiviteit in Data Factory kopieert gegevens van een gegevensarchief bron data store tooa sink. Data Factory ondersteunt Hallo gegevensarchieven te volgen. Gegevens van elke bron kan worden geschreven als tooany sink. Hoe klikt u op een data store toolearn toocopy gegevens tooand van dat archief.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Gegevens worden opgeslagen met * on-premises kan worden of op Azure IaaS en moet u tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) op een op-premises/Azure IaaS-machine.

Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie.

### <a name="data-transformation-activities"></a>Activiteiten voor gegevenstransformatie
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Zie het artikel [Activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) voor meer informatie.

### <a name="custom-net-activities"></a>Aangepaste .NET-activiteiten 
Als u moet toomove gegevens naar/van een data store Hallo Kopieeractiviteit niet ondersteunen, of gegevens met behulp van uw eigen logica transformeren, maken een **aangepaste .NET-activiteit**. Zie [Aangepaste activiteiten gebruiken in een Azure Data Factory-pijplijn](data-factory-use-custom-activities.md) voor meer informatie over het maken en gebruiken van een aangepaste activiteit.

## <a name="schedule-pipelines"></a>Planning pijplijnen
Een pijplijn is active alleen tussen de **start** tijd en **end** tijd. Het is niet uitgevoerd vóór de begintijd Hallo of na de eindtijd Hallo. Als het Hallo-pipeline is onderbroken, wordt deze niet uitgevoerd ongeacht de begin- en -tijd. Voor een toorun pijplijn mag deze niet worden onderbroken. Zie [planning en uitvoering](data-factory-scheduling-and-execution.md) toounderstand hoe plannen en uitvoeren in Azure Data Factory werkt.

## <a name="pipeline-json"></a>Pijplijn in JSON-indeling
We gaan dieper in op hoe een pijplijn wordt gedefinieerd in JSON-indeling. algemene structuur Hallo voor een pijplijn ziet er als volgt uit:

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description" : "pipeline description",
        "activities":
        [

        ],
        "start": "<start date-time>",
        "end": "<end date-time>",
        "isPaused": true/false,
        "pipelineMode": "scheduled/onetime",
        "expirationTime": "15.00:00:00",
        "datasets": 
        [
        ]
    }
}
```

| Label | Beschrijving | Vereist |
| --- | --- | --- |
| naam |Naam van het Hallo-pijplijn. Geef een naam die staat voor Hallo-actie die Hallo pijplijn wordt uitgevoerd. <br/><ul><li>Maximum aantal tekens: 260</li><li>Moet beginnen met een letter, cijfer of onderstrepingsteken (_)</li><li>Volgende tekens zijn niet toegestaan: '. ', '+ ','?', '/', '< ',' >', ' * ', "%", "&", ":","\\'</li></ul> |Ja |
| description | Geef tekst op Hallo beschrijven welke Hallo-pijplijn wordt gebruikt voor. |Ja |
| activities | Hallo **activiteiten** sectie kan een of meer activiteiten die zijn gedefinieerd binnen deze hebben. Zie de volgende sectie Hallo voor meer informatie over Hallo activiteiten JSON-element. | Ja |  
| start | Datum-begintijd voor de Hallo pijplijn. Moet in [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601). Bijvoorbeeld: `2016-10-14T16:32:41Z`. <br/><br/>Het is mogelijk toospecify een plaatselijke tijd, bijvoorbeeld een geschatte tijd. Hier volgt een voorbeeld: `2016-02-27T06:00:00-05:00`", namelijk 6 uur geschatte<br/><br/>Hallo begin- en eigenschappen samen actieve periode opgeven voor Hallo pijplijn. Uitvoer segmenten worden alleen gemaakt met deze actieve periode. |Nee<br/><br/>Als u een waarde voor Hallo end-eigenschap opgeeft, moet u de waarde voor Hallo begineigenschap opgeven.<br/><br/>Hallo kunnen begin- en eindtijden niet leeg toocreate een pijplijn. U moet beide waarden opgeven tooset een actieve periode voor Hallo pijplijn toorun. Als u geen begin- en eindtijden opgeeft wanneer u een pijplijn maakt, kunt u deze instellen met behulp van de cmdlet Set-AzureRmDataFactoryPipelineActivePeriod hello later. |
| Einde | Einddatum en-tijd voor de Hallo pijplijn. Als in de ISO-indeling moet worden opgegeven. Bijvoorbeeld: `2016-10-14T17:32:41Z` <br/><br/>Het is mogelijk toospecify een plaatselijke tijd, bijvoorbeeld een geschatte tijd. Hier volgt een voorbeeld: `2016-02-27T06:00:00-05:00`, namelijk 6 AM EST.<br/><br/>9999-09-09 toorun Hallo pijplijn voor onbepaalde tijd opgeven als waarde voor end-eigenschap Hallo Hallo. <br/><br/> Er is een pijplijn active alleen tussen de begintijd en eindtijd. Het is niet uitgevoerd vóór de begintijd Hallo of na de eindtijd Hallo. Als het Hallo-pipeline is onderbroken, wordt deze niet uitgevoerd ongeacht de begin- en -tijd. Voor een toorun pijplijn mag deze niet worden onderbroken. Zie [planning en uitvoering](data-factory-scheduling-and-execution.md) toounderstand hoe plannen en uitvoeren in Azure Data Factory werkt. |Nee <br/><br/>Als u een waarde voor Hallo start eigenschap opgeeft, moet u de waarde voor end-eigenschap Hallo opgeven.<br/><br/>Zie de opmerkingen voor Hallo **start** eigenschap. |
| isPaused | Als de set tootrue, Hallo pijplijn kan niet worden uitgevoerd. Deze onderbroken in Hallo status. Standaardwaarde = false. U kunt deze eigenschap tooenable gebruiken of een pijplijn uitschakelen. |Nee |
| pipelineMode | Hallo-methode voor het plannen wordt uitgevoerd voor de Hallo pijplijn. Toegestane waarden zijn: (standaard), gepland eenmalige.<br/><br/>De geplande' geeft aan dat Hallo-pijplijn wordt uitgevoerd op een opgegeven tijdsinterval volgens tooits actieve periode (begin- en -tijd). 'Eenmalige' geeft aan dat Hallo-pijplijn wordt slechts één keer uitgevoerd. Eenmalige pijplijnen eenmaal gemaakt kunnen niet worden gewijzigd/bijgewerkt op dit moment. Zie [Onetime pijplijn](#onetime-pipeline) voor meer informatie over het instellen van eenmalige. |Nee |
| expirationTime | Tijdsduur na het maken van welke Hallo [eenmalige pijplijn](#onetime-pipeline) is geldig en moet worden ingericht. Als er geen elk actief is, is mislukt, of in afwachting wordt uitgevoerd, is het Hallo-pijplijn automatisch bereikt één keer verwijderd het Hallo verlooptijd. Hallo standaardwaarde:`"expirationTime": "3.00:00:00"`|Nee |
| Gegevenssets |Lijst met gegevenssets toobe door activiteiten die zijn gedefinieerd in de pijplijn Hallo gebruikt. Deze eigenschap kan worden gebruikt toodefine gegevenssets die specifieke toothis pijplijn en niet gedefinieerd binnen Hallo data factory. Gegevenssets die zijn gedefinieerd in deze pijplijn kan alleen worden gebruikt door deze pipeline en kan niet worden gedeeld. Zie [binnen het bereik van gegevenssets](data-factory-create-datasets.md#scoped-datasets) voor meer informatie. |Nee |

## <a name="activity-json"></a>Activity in JSON
Hallo **activiteiten** sectie kan een of meer activiteiten die zijn gedefinieerd binnen deze hebben. Elke activiteit heeft Hallo op het hoogste niveau structuur te volgen:

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
    },
    "scheduler":
    {
    }
}
```

Volgende tabel beschrijft de eigenschappen van de activiteit Hallo JSON-definitie:

| Label | Beschrijving | Vereist |
| --- | --- | --- |
| naam | Naam van Hallo-activiteit. Geef een naam die aangeeft Hallo-actie die Hallo activiteit uitvoert. <br/><ul><li>Maximum aantal tekens: 260</li><li>Moet beginnen met een letter, cijfer of onderstrepingsteken (_)</li><li>Volgende tekens zijn niet toegestaan: '. ', '+ ','?', '/', '< ',' >', ' * ', "%", "&", ":","\\'</li></ul> |Ja |
| description | Beschrijving van wat Hallo activiteit of wordt gebruikt voor |Ja |
| type | Type Hallo-activiteit. Zie Hallo [activiteiten voor gegevensverplaatsing](#data-movement-activities) en [activiteiten voor gegevenstransformatie](#data-transformation-activities) secties voor verschillende soorten activiteiten. |Ja |
| Invoer |Invoertabellen die worden gebruikt door Hallo-activiteit<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Ja |
| uitvoer |Uitvoergegevens tabellen gebruikt door Hallo-activiteit.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |Ja |
| linkedServiceName |Naam van Hallo gekoppelde service die wordt gebruikt door het Hallo-activiteit. <br/><br/>Een activiteit kan vereisen dat u opgeeft Hallo gekoppelde service die is gekoppeld aan toohello vereist compute-omgeving. |Ja voor HDInsight-activiteit en Azure Machine Learning-score-activiteit <br/><br/>Nee voor alle andere |
| typeProperties |Eigenschappen in Hallo **typeProperties** sectie, is afhankelijk van type Hallo-activiteit. toosee type-eigenschappen voor een activiteit, klikt u op de koppelingen toohello activiteit in de vorige sectie Hallo. | Nee |
| policy |Beleidsregels die invloed hebben op Hallo run-time gedrag van Hallo-activiteit. Als deze niet is opgegeven, worden de standaardbeleidsregels gebruikt. |Nee |
| Scheduler | 'scheduler'-eigenschap is gebruikte toodefine gewenst schema voor het Hallo-activiteit. Bijbehorende subeigenschappen zijn hetzelfde als de waarden in Hallo HALLO hallo [eigenschap beschikbaarheid in een dataset](data-factory-create-datasets.md#dataset-availability). |Nee |


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

## <a name="sample-copy-pipeline"></a>Voorbeeld van kopieerpijplijn
In het Hallo-voorbeeldpijplijn te volgen, wordt een activiteit van het type **kopie** in Hallo **activiteiten** sectie. In dit voorbeeld Hallo [kopieeractiviteit](data-factory-data-movement-activities.md) gegevens worden gekopieerd van een Azure Blob storage tooan Azure SQL database. 

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
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
} 
```

Houd er rekening mee Hallo volgende punten:

* In Hallo gedeelte activiteiten is er slechts één activiteit waarvan **type** te is ingesteld,**kopie**.
* Invoer voor Hallo-activiteit is ingesteld, te**InputDataset** en de uitvoer voor Hallo activiteit te is ingesteld**OutputDataset**. Zie het artikel [Gegevenssets](data-factory-create-datasets.md) voor informatie over het definiëren van gegevenssets in JSON. 
* In Hallo **typeProperties** sectie **BlobSource** is opgegeven als Hallo brontype en **SqlSink** is opgegeven als Hallo sink-type. In Hallo [activiteiten voor gegevensverplaatsing](#data-movement-activities) sectie, klikt u op Hallo gegevensarchief dat u toouse wilt gebruiken als een bron of een toolearn sink meer informatie over het verplaatsen van gegevens van die gegevensarchief. 

Zie voor een volledige procedure voor het maken van deze pipeline [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="sample-transformation-pipeline"></a>Voorbeeld van pijplijn voor transformatie
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
        "start": "2016-04-01T00:00:00Z",
        "end": "2016-04-02T00:00:00Z",
        "isPaused": false
    }
}
```

Houd er rekening mee Hallo volgende punten: 

* In Hallo gedeelte activiteiten is er slechts één activiteit waarvan **type** te is ingesteld,**HDInsightHive**.
* Hallo Hive-scriptbestand **partitionweblogs.hql**, wordt opgeslagen in hello Azure storage-account (Hallo door scriptLinkedService met de opgegeven **AzureStorageLinkedService**), en in  **script** map in container Hallo **adfgetstarted**.
* Hallo `defines` sectie is gebruikte toospecify Hallo runtime-instellingen die toohello hive-script worden doorgegeven als Hive-configuratiewaarden (bijvoorbeeld `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Hallo **typeProperties** sectie verschilt voor elke transformatieactiviteit. toolearn over de eigenschappen van het type ondersteund voor een transformatieactiviteit, klikt u op Hallo transformatieactiviteit in Hallo [activiteiten voor gegevenstransformatie](#data-transformation-activities) tabel. 

Zie voor een volledige procedure voor het maken van deze pipeline [zelfstudie: bouwen van uw eerste pijplijn tooprocess gegevens met Hadoop-cluster](data-factory-build-your-first-pipeline.md). 

## <a name="multiple-activities-in-a-pipeline"></a>Meerdere activiteiten in een pijplijn
de vorige twee steekproeven pijplijnen Hallo zich slechts één activiteit bevinden. Een pijplijn kan echter meer dan één activiteit hebben.  

Als er meerdere activiteiten in een pijplijn en uitvoer van een activiteit geen invoer van een andere activiteit is, Hallo activiteiten kunnen parallel worden uitgevoerd als invoer gegevenssegmenten voor Hallo activiteiten klaar bent. 

U kunt twee activiteiten koppelen door de uitvoergegevensset Hallo van één activiteit als invoergegevensset Hallo Hallo andere activiteit. Hallo tweede activiteit wordt uitgevoerd, alleen wanneer hello eerst een voltooid is.

![Activiteiten in Hallo-koppeling met dezelfde pipeline](./media/data-factory-create-pipelines/chaining-one-pipeline.png)

In dit voorbeeld Hallo pipeline heeft twee activiteiten: activiteit1 en activiteit2. Hallo activiteit1 neemt Dataset1 als invoer en uitvoer produceert Dataset2. Hallo activiteit neemt Dataset2 als invoer en uitvoer produceert Dataset3. Sinds het Hallo-uitvoer van activiteit1 (Dataset2) is Hallo invoer van activiteit2, Hallo activiteit2 alleen wordt uitgevoerd nadat Hallo activiteit voltooid is en produceert Hallo Dataset2 segment. Als Hallo activiteit1 mislukt voor een bepaalde reden geen Hallo Dataset2 segment produceert, Hallo activiteit 2 kan niet worden uitgevoerd voor die segment (bijvoorbeeld: 9 uur too10 BEN). 

U kunt ook de activiteiten in verschillende pijplijnen koppelen.

![Koppeling van activiteiten in twee pijplijnen](./media/data-factory-create-pipelines/chaining-two-pipelines.png)

In dit voorbeeld heeft Pipeline1 slechts één activiteit die ervoor zorgt dat Dataset1 als invoer Dataset2 als uitvoer produceert. Hallo Pipeline2 heeft ook slechts één activiteit die Dataset2 als invoer en Dataset3 als uitvoer neemt. 

Zie voor meer informatie [plannen en uitvoeren](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="create-and-monitor-pipelines"></a>Maken en pijplijnen bewaken
U kunt pijplijnen maken met behulp van een van deze hulpprogramma's of de SDK's. 

- De Wizard kopiëren. 
- Azure Portal
- Visual Studio
- Azure PowerShell
- Azure Resource Manager-sjabloon
- REST API
- .NET API

Zie Hallo-zelfstudies voor stapsgewijze instructies voor het maken van pijplijnen met behulp van een van deze hulpprogramma's of de SDK's te volgen.
 
- [Een pijplijn met een transformatieactiviteit voor gegevens bouwen](data-factory-build-your-first-pipeline.md)
- [Maken van een pijplijn met een activiteit van de verplaatsing van gegevens](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Zodra een pijplijn gemaakt/geïmplementeerd, kunt u beheren en bewaken van uw pijplijnen met behulp van Azure portal-blades of Monitor and Manage App Hallo. Zie de volgende onderwerpen voor stapsgewijze instructies Hallo. 

- [Bewaken en beheren van pijplijnen via Azure portal-blades](data-factory-monitor-manage-pipelines.md).
- [Bewaken en beheren van pijplijnen met behulp van de Monitor and Manage App](data-factory-monitor-manage-app.md)


## <a name="onetime-pipeline"></a>Eenmalige pijplijn
U kunt maken en plannen van een pijplijn toorun regelmatig (bijvoorbeeld: elk uur of dagelijks) binnen Hallo beginnen en eindigen tijden die u in de definitie van de pijplijn Hallo opgeeft. Zie [activiteiten plannen](#scheduling-and-execution) voor meer informatie. Ook kunt u een pijplijn die wordt slechts eenmaal uitgevoerd. toodo dus het instellen van Hallo **pipelineMode** eigenschap in Hallo pipeline-definitie te**eenmalige** zoals weergegeven in de volgende JSON-voorbeeld Hallo. Hallo-standaardwaarde voor deze eigenschap is **geplande**.

```json
{
    "name": "CopyPipeline",
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
                        "name": "InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ]
                "name": "CopyActivity-0"
            }
        ]
        "pipelineMode": "OneTime"
    }
}
```

Let op Hallo volgende:

* **Start** en **end** tijden voor de pijplijn Hallo zijn niet opgegeven.
* **Beschikbaarheid** van invoer en uitvoer gegevenssets is opgegeven (**frequentie** en **interval**), ook al Data Factory maakt geen gebruik van Hallo waarden.  
* Diagramweergave worden geen eenmalige pijplijnen weergegeven. Dit gedrag is standaard.
* Eenmalige pijplijnen kunnen niet worden bijgewerkt. Klonen van een eenmalige pijplijn, wijzigt u de naam, eigenschappen bijwerken en deze toocreate implementeert een andere naam.


## <a name="next-steps"></a>Volgende stappen
- Zie voor meer informatie over gegevenssets [gegevenssets maken](data-factory-create-datasets.md) artikel. 
- Zie voor meer informatie over hoe pijplijnen worden gepland en uitgevoerd, [planning en uitvoering in Azure Data Factory](data-factory-scheduling-and-execution.md) artikel. 
  

