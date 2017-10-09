---
title: aaaScheduling en uitvoering met Data Factory | Microsoft Docs
description: Meer informatie over plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a>Data Factory plannen en uitvoeren
Dit artikel wordt uitgelegd Hallo plannings- en uitvoeringsaspecten van hello Azure Data Factory-toepassingsmodel. In dit artikel wordt ervan uitgegaan dat u van de Data Factory toepassing model concepten basisbeginselen, met inbegrip van activiteiten, pijplijnen, gekoppelde services en gegevenssets. Zie voor de basisconcepten van Azure Data Factory, Hallo artikelen te volgen:

* [Inleiding tooData Factory](data-factory-introduction.md)
* [Pijplijnen](data-factory-create-pipelines.md)
* [Gegevenssets](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a>Begin- en eindtijden van pijplijn
Een pijplijn is active alleen tussen de **start** tijd en **end** tijd. Het is niet uitgevoerd vóór de begintijd Hallo of na de eindtijd Hallo. Als het Hallo-pipeline is onderbroken, is het niet uitgevoerd ongeacht de begin- en -tijd. Voor een toorun pijplijn mag deze niet worden onderbroken. U vinden deze instellingen (start, eindgebruikers, onderbroken) in de definitie van de pijplijn Hallo: 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

Zie voor meer informatie deze eigenschappen [pijplijnen maken](data-factory-create-pipelines.md) artikel. 


## <a name="specify-schedule-for-an-activity"></a>Planning voor een activiteit opgeven
Het is niet Hallo pijplijn die wordt uitgevoerd. Het Hallo-activiteiten in Hallo pijplijn die worden uitgevoerd in Hallo is algehele context van Hallo pijplijn. U kunt een terugkerend schema voor een activiteit opgeven met behulp van Hallo **scheduler** sectie van de JSON van de activiteit. Bijvoorbeeld, kunt u plannen een toorun activiteit per uur als volgt:  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

Zoals u in het volgende diagram hello, opgeven van dat een planning voor een activiteit wordt een reeks van windows met daling in Hallo pipeline-begin- en eindtijden. Windows daling zijn een reeks met vaste grootte niet-overlappende, aaneengesloten tijdsintervallen. Deze logische daling vensters voor een activiteit worden genoemd **activiteitsvensters**.

![Voorbeeld van de activiteit scheduler](media/data-factory-scheduling-and-execution/scheduler-example.png)

Hallo **scheduler** eigenschap voor een activiteit is optioneel. Als u deze eigenschap opgeeft, moet deze Hallo uitgebracht die u in het Hallo-definitie van de uitvoergegevensset voor de activiteit Hallo opgeeft overeenkomen. Uitvoergegevensset is momenteel welke stations Hallo planning. Daarom moet u een uitvoergegevensset maken, zelfs als Hallo activiteit geen uitvoer produceert. 

## <a name="specify-schedule-for-a-dataset"></a>Geef de planning voor een gegevensset
Een activiteit in een Data Factory-pijplijn kan duren voordat de invoer van nul of meer **gegevenssets** en een of meer uitvoergegevenssets te produceren. Voor een activiteit, kunt u Hallo uitgebracht welke Hallo invoergegevens beschikbaar is of uitvoergegevens hello wordt gemaakt met behulp van Hallo **beschikbaarheid** sectie in Hallo gegevensset definities. 

**Frequentie** in Hallo **beschikbaarheid** sectie Hallo tijdseenheid geeft. Hallo toegestane waarden voor de frequentie zijn: minuut, uur, dag, Week en maand. Hallo **interval** eigenschap in de sectie beschikbaarheid Hallo vermenigvuldigingsfactor voor de frequentie. Bijvoorbeeld: als Hallo frequentie tooDay is ingesteld en de interval too1 voor een uitvoergegevensset, Hallo uitvoergegevens dagelijks wordt geproduceerd. Als u Hallo frequentie als minuut opgeeft, raden wij u Hallo interval toono kleiner is dan 15 instellen. 

In Hallo voorbeeld te volgen, Hallo invoergegevens beschikbaar per uur en uitvoergegevens Hallo per uur wordt geproduceerd (`"frequency": "Hour", "interval": 1`). 

**Invoergegevensset:** 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


**Uitvoergegevensset**

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Op dit moment **output dataset stations Hallo planning**. Met andere woorden, is opgegeven voor de uitvoergegevensset Hallo Hallo-upschema gebruikte toorun een activiteit tijdens runtime. Daarom moet u een uitvoergegevensset maken, zelfs als Hallo activiteit geen uitvoer produceert. Als Hallo activiteit geen invoer neemt, kunt u maken Hallo invoergegevensset overslaan. 

In de volgende Hallo pipeline-definitie hello **scheduler** eigenschap gebruikte toospecify planning voor Hallo-activiteit is. Deze eigenschap is optioneel. Op dit moment Hallo-schema voor het Hallo-activiteit moet overeenkomen met opgegeven voor de uitvoergegevensset Hallo Hallo-upschema.
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

In dit voorbeeld Hallo activiteit wordt uitgevoerd per uur tussen Hallo starten en eindtijden van Hallo pijplijn. Hallo uitvoergegevens wordt per uur gemaakt voor drie uur windows (8 AM - 9 uur, 9: 00 uur - 10: 00 uur, en 10: 00 - 11 uur). 

Elke eenheid van gegevens gebruikt of die wordt geproduceerd door een activiteit die wordt uitgevoerd, heet een **gegevenssegment**. Hallo volgende diagram toont een voorbeeld van een activiteit met één invoergegevensset en één uitvoergegevensset: 

![Beschikbaarheid scheduler](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

Hallo diagram toont Hallo per uur in gegevenssegmenten voor Hallo invoer en uitvoer van de gegevensset. Hallo diagram ziet u drie invoer segmenten die gereed voor verwerking zijn. Hallo 10 11 uur activiteit wordt uitgevoerd, het opstellen van Hallo 10 11 uur uitvoer segment. 

U hebt toegang tot Hallo tijdsinterval die is gekoppeld aan het huidige segment Hallo gegevensset JSON Hallo met behulp van variabelen: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) en [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables). Op deze manier kunt u Hallo tijdsinterval die is gekoppeld aan het venster van een activiteit met behulp van Hallo WindowStart en WindowEnd openen. Hallo-schema van een activiteit moet overeenkomen met de Hallo planning van Hallo uitvoergegevensset voor Hallo-activiteit. Daarom Hallo SliceStart en SliceEnd waarden zijn Hallo dezelfde als WindowStart en WindowEnd waarden respectievelijk. Zie voor meer informatie over deze variabelen [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md#data-factory-system-variables) artikelen.  

U kunt deze variabelen voor verschillende doeleinden gebruiken in de JSON van de activiteit. Bijvoorbeeld, kunt u ze tooselect gegevens uit de invoer- en uitvoergegevenssets representatie van time series-gegevens (bijvoorbeeld: 8 AM too9 BEN). Dit voorbeeld wordt tevens **WindowStart** en **WindowEnd** tooselect relevante gegevens voor een activiteit uitvoeren en kopieer het tooa blob met de juiste Hallo **folderPath**. Hallo **folderPath** geparameteriseerde toohave van een afzonderlijke map voor elk uur is.  

In de Hallo voorgaande voorbeeld, Hallo Hallo schema is opgegeven voor de invoer- en uitvoergegevenssets dezelfde (elk uur). Als invoergegevensset voor activiteit Hallo Hallo beschikbaar op een andere frequentie spreek om de 15 minuten is, uitgevoerd Hallo-activiteit die deze uitvoergegevensset produceert nog eens per uur, zoals Hallo uitvoergegevensset is welke stations Hallo activiteitenplanning. Zie voor meer informatie [Model gegevenssets frequentie](#model-datasets-with-different-frequencies).

## <a name="dataset-availability-and-policies"></a>Beschikbaarheid van de gegevensset en het beleid
U hebt al gezien Hallo informatie over het gebruik van eigenschappen voor frequentie en het interval in Hallo beschikbaarheidssectie van de definitie van gegevensset. Er zijn enkele andere eigenschappen die betrekking hebben op Hallo plannen en uitvoeren van een activiteit. 

### <a name="dataset-availability"></a>Beschikbaarheid van gegevensset 
Hallo volgende tabel beschrijft eigenschappen die u in Hallo gebruiken kunt **beschikbaarheid** sectie:

| Eigenschap | Beschrijving | Vereist | Standaard |
| --- | --- | --- | --- |
| frequency |Hiermee geeft u tijdseenheid Hallo voor gegevensset segment productie.<br/><br/><b>Ondersteunde frequentie</b>: minuut, uur, dag, Week, maand |Ja |N.v.t. |
| interval |Hiermee geeft u een vermenigvuldiger voor de frequentie<br/><br/>"Frequentie x-interval" bepaalt hoe vaak hello segment wordt geproduceerd.<br/><br/>Als u de gegevensset toobe gesegmenteerd op uurbasis moet hello, stelt u <b>frequentie</b> te<b>uur</b>, en <b>interval</b> te<b>1</b>.<br/><br/><b>Opmerking</b>: als u de frequentie als minuut opgeeft, raden wij aan dat u Hallo interval toono kleiner is dan 15 |Ja |N.v.t. |
| stijl |Hiermee geeft u op of Hallo segment Hallo beginnen of eindigen van hello-interval moet worden geproduceerd.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Als de frequentie tooMonth is ingesteld en stijl tooEndOfInterval is ingesteld, wordt Hallo segment op Hallo laatste dag van de maand geproduceerd. Als Hallo stijl is ingesteld tooStartOfInterval, wordt Hallo segment geproduceerd op Hallo eerste dag van de maand.<br/><br/>Als frequentie tooDay is ingesteld en stijl tooEndOfInterval is ingesteld, wordt in het afgelopen uur van de dag Hallo HALLO hallo segment geproduceerd.<br/><br/>Als frequentie tooHour is ingesteld en stijl tooEndOfInterval is ingesteld, worden Hallo segment wordt geproduceerd achter Hallo Hallo uur. Voor een segment 1-2 uur gedurende Hallo segment geproduceerd om 2 uur. |Nee |EndOfInterval |
| anchorDateTime |Hiermee definieert u Hallo absolute positie in de tijd die wordt gebruikt door de grenzen van scheduler toocompute gegevensset segment. <br/><br/><b>Opmerking</b>: als Hallo AnchorDateTime bevat de datumonderdelen die meer gedetailleerd dan Hallo frequentie zijn dan hello gedetailleerdere onderdelen worden genegeerd. <br/><br/>Bijvoorbeeld, als hello <b>interval</b> is <b>per uur</b> (frequentie: uur en interval: 1) en Hallo <b>AnchorDateTime</b> bevat <b>minuten en seconden</b>, vervolgens Hallo <b>minuten en seconden</b> delen van Hallo AnchorDateTime worden genegeerd. |Nee |01/01/0001 |
| offset |TimeSpan door welke Hallo begin en einde van alle segmenten van de gegevensset zijn verplaatst. <br/><br/><b>Opmerking</b>: als zowel anchorDateTime als offset worden opgegeven, Hallo resultaat Hallo gecombineerd shift is. |Nee |N.v.t. |

### <a name="offset-example"></a>offset voorbeeld
Standaard dagelijks (`"frequency": "Day", "interval": 1`) segmenten beginnen bij 12: 00 A.M. UTC-tijd (middernacht). Als u Hallo start tijd toobe 06: 00 UTC-tijd in plaats daarvan wilt, stelt u Hallo zoals weergegeven in het volgende codefragment Hallo offset: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>Voorbeeld van anchorDateTime
In de Hallo voorbeeld te volgen, wordt de elke 23 uur in Hallo gegevensset wordt geproduceerd. Hallo eerste cirkelsegment begint bij Hallo tijd die is opgegeven door Hallo anchorDateTime die is ingesteld te`2017-04-19T08:00:00` (UTC-tijd).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>offset/stijl voorbeeld
Hallo volgende gegevensset is een maandelijkse gegevensset en op 3rd van elke maand om 8:00 uur wordt geproduceerd (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a>DataSet beleid
Een dataset kan een validatiebeleid gedefinieerd waarmee wordt aangegeven hoe Hallo-gegevens die zijn gegenereerd door de uitvoering van een segment kan worden gevalideerd voordat deze gereed voor verbruik is hebben. In dergelijke gevallen nadat het Hallo-segment is uitgevoerd, Hallo uitvoer segment de status wordt gewijzigd te**wachten** met een substatus van **validatie**. Nadat Hallo segmenten zijn geverifieerd, Hallo segment status verandert te**gereed**. Als een gegevenssegment is geproduceerd, maar niet gevalideerd hello worden kan, worden de activiteiten bij uitvoering downstream segmenten die afhankelijk van dit segment zijn niet verwerkt. [Bewaken en beheren van pijplijnen](data-factory-monitor-manage-pipelines.md) dekt Hallo verschillende statussen van gegevenssegmenten in Data Factory.

Hallo **beleid** sectie in de definitie van gegevensset definieert Hallo criteria of Hallo-voorwaarde die Hallo segmenten van de gegevensset moet voldoen. Hallo volgende tabel beschrijft eigenschappen die u in Hallo gebruiken kunt **beleid** sectie:

| De naam van beleid | Beschrijving | Te worden toegepast| Vereist | Standaard |
| --- | --- | --- | --- | --- |
| minimumSizeMB | Valideert dat Hallo-gegevens in een **Azure blob** voldoet aan de vereisten van de minimale grootte (in megabytes) Hallo. |Azure Blob |Nee |N.v.t. |
| minimumRows | Valideert dat Hallo-gegevens in een **Azure SQL-database** of een **Azure-tabel** Hallo minimum aantal rijen bevat. |<ul><li>Azure SQL Database</li><li>Azure-tabel</li></ul> |Nee |N.v.t. |

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

**minimumRows**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

Zie voor meer informatie over deze eigenschappen en voorbeelden [gegevenssets maken](data-factory-create-datasets.md) artikel. 

## <a name="activity-policies"></a>Beleidsregels voor activiteiten
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

Zie voor meer informatie [pijplijnen](data-factory-create-pipelines.md) artikel. 

## <a name="parallel-processing-of-data-slices"></a>Parallelle verwerking van gegevenssegmenten
Hallo begindatum voor Hallo pijplijn kunt u instellen in de afgelopen Hallo. Wanneer u doet dit, wordt Data Factory automatisch berekend (back-opvulling) alle gegevenssegmenten Hallo afgelopen en ze worden verwerkt. Bijvoorbeeld: als u een pijplijn met een begindatum 2017-04-01 maken en Hallo de huidige datum 2017-04-10 valt. Als Hallo uitgebracht Hallo uitvoergegevensset dagelijks vervolgens Data Factory wordt gestart voor het verwerken van alle Hallo segmenten van 2017-04-01 is too2017-04-09 onmiddellijk omdat Hallo begindatum in de afgelopen Hallo. Hallo-segment van 2017-04-10 is niet verwerkt nog omdat Hallo-waarde van de eigenschap style in de sectie beschikbaarheid Hallo EndOfInterval standaard. Hallo oudste segment is verwerkt eerst als Hallo standaard waarde van executionPriorityOrder OldestFirst is. Zie voor een beschrijving van de eigenschap style Hallo [gegevensset beschikbaarheid](#dataset-availability) sectie. Zie voor een beschrijving van Hallo executionPriorityOrder sectie Hallo [beleidsregels voor activiteiten](#activity-policies) sectie. 

Kunt u gegevens back gevuld segmenten toobe parallel worden verwerkt door de instelling Hallo **gelijktijdigheid** eigenschap in Hallo **beleid** sectie van de JSON van de Hallo-activiteit. Deze eigenschap bepaalt het aantal parallelle activiteit uitvoeringen die kunnen ontstaan op verschillende segmenten Hallo. de standaardwaarde Hallo voor Hallo gelijktijdigheid eigenschap is 1. Daarom is een segment verwerkt op een tijdstip standaard. Hallo maximale waarde is 10. Wanneer een pijplijn toogo via een groot aantal beschikbare gegevens, een grotere waarde voor gelijktijdigheid van taken moet Hallo gegevensverwerking wordt versneld. 

## <a name="rerun-a-failed-data-slice"></a>Voer een mislukte gegevenssegment
Wanneer een fout optreedt tijdens het verwerken van een gegevenssegment, vindt u waarom de verwerking van een segment Hallo via Azure portal-blades of Monitor and Manage App is mislukt. Zie [controleren en beheren met Azure portal-blades pijplijnen](data-factory-monitor-manage-pipelines.md) of [app voor bewaking en beheer](data-factory-monitor-manage-app.md) voor meer informatie.

Overweeg het volgende voorbeeld ziet u twee activiteiten Hallo. Activiteit1 en activiteit 2. Activiteit1 een segment van Dataset1 verbruikt en een segment van Dataset2 die wordt gebruikt als invoer door activiteit2 tooproduce een segment Hallo laatste gegevensset wordt geproduceerd.

![Mislukte segment](./media/data-factory-scheduling-and-execution/failed-slice.png)

Hallo diagram toont die uit drie recente segmenten, er is een fout produceren Hallo 9 10 uur segment voor Dataset2. Data Factory-afhankelijkheid voor Hallo time series dataset automatisch worden bijgehouden. Hallo activiteit die wordt uitgevoerd voor Hallo 9 10 uur downstream segment worden hierdoor niet gestart.

Data Factory bewaking en beheer-hulpprogramma's kunnen u toodrill in Hallo diagnostische logboeken voor Hallo mislukte segment tooeasily zoeken Hallo hoofdmap voor Hallo probleem veroorzaken en op te lossen. Nadat u Hallo probleem hebt opgelost, kunt u eenvoudig hello activiteit die wordt uitgevoerd tooproduce Hallo mislukte segment te starten. Voor meer informatie over het toorerun en statusovergangen voor gegevenssegmenten begrijpen, Zie [controleren en beheren met Azure portal-blades pijplijnen](data-factory-monitor-manage-pipelines.md) of [app voor bewaking en beheer](data-factory-monitor-manage-app.md).

Nadat u opnieuw Hallo uitvoeren 9 10 uur segmenteren voor **Dataset2**, Data Factory Hallo uitvoeren voor Hallo 9 10 uur afhankelijke segment op Hallo laatste gegevensset wordt gestart.

![Mislukte segment opnieuw uitvoeren](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a>Meerdere activiteiten in een pijplijn
Een pijplijn kan echter meer dan één activiteit hebben. Als er meerdere activiteiten in een pijplijn en Hallo-uitvoer van een activiteit geen invoer van een andere activiteit is, Hallo activiteiten kunnen parallel worden uitgevoerd als invoer gegevenssegmenten voor Hallo activiteiten klaar bent.

U kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Hallo-activiteiten kunnen worden ingesteld in Hallo dezelfde pijplijn of in verschillende pijplijnen. Hallo tweede activiteit wordt uitgevoerd, alleen wanneer hello eerst een succes voltooid wordt.

Denk bijvoorbeeld Hallo geval waarbij een pijplijn twee activiteiten heeft te volgen:

1. A1 activiteit waarvoor externe invoergegevensset D1 en D2 uitvoergegevensset die wordt gegenereerd.
2. Activiteit A2 die invoer uit gegevensset D2 is vereist en produceert uitvoergegevensset D3.

In dit scenario, activiteiten A1 en A2 zijn in Hallo dezelfde pipeline. Hallo activiteit die a1 wordt uitgevoerd als externe gegevens Hallo beschikbaar is en de frequentie van geplande Hallo beschikbaarheid is bereikt. Hallo activiteit A2 wordt uitgevoerd als hello geplande segmenten van D2 beschikbaar en hello frequentie van geplande beschikbaarheid is bereikt. Als er een fout in een van de segmenten in de gegevensset D2 hello, voert A2 niet voor dat segment totdat deze beschikbaar.

Hallo diagramweergave met beide activiteiten in Hallo dezelfde pijplijn eruit zou Hallo-diagram te volgen:

![Activiteiten in Hallo-koppeling met dezelfde pipeline](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

Zoals eerder vermeld, kunnen in verschillende pijplijnen Hallo activiteiten worden. In een dergelijk scenario eruit Hallo diagramweergave als Hallo-diagram te volgen:

![Koppeling van activiteiten in twee pijplijnen](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

Zie Hallo [sequentieel kopiëren](#copy-sequentially) sectie in het Hallo-bijlage voor een voorbeeld.

## <a name="model-datasets-with-different-frequencies"></a>Model gegevenssets frequentie
In de voorbeelden van Hallo zijn Hallo frequenties voor invoer en uitvoer gegevenssets en Hallo activiteit Planningsvenster Hallo dezelfde. Sommige scenario's moet Hallo mogelijkheid tooproduce uitvoer met een frequentie anders dan Hallo frequenties van een of meer invoerwaarden. Data Factory biedt ondersteuning voor het modelleren van deze scenario's.

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a>Voorbeeld 1: Een dagelijkse uitvoer-rapport voor invoergegevens die beschikbaar is om het uur produceren
Neem bijvoorbeeld een scenario waarin u hebt ingevoerd meetgegevens van sensoren beschikbaar om het uur in Azure Blob-opslag. Gewenste tooproduce een dagelijkse cumulatieve rapport met statistieken zoals gemiddelde, maximum en minimum voor Hallo dag met [Data Factory hive-activiteit](data-factory-hive-activity.md).

Hier ziet u hoe u dit scenario met Data Factory kunt model:

**Invoergegevensset**

Hallo invoer per uur bestanden worden verwijderd in de map Hallo voor Hallo opgegeven dag. Beschikbaarheid voor invoer is ingesteld op **uur** (frequentie: uur, interval: 1).

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Uitvoergegevensset**

Een bestand voor uitvoer wordt elke dag in van de dag van het Hallo-map gemaakt. Beschikbaarheid van de uitvoer is ingesteld op **dag** (frequentie: dagen en interval: 1).

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Activiteit: hive-activiteit in een pijplijn**

Hallo hive-script ontvangt Hallo juiste *DateTime* informatie als parameters die gebruikmaken van Hallo **WindowStart** variabele, zoals wordt weergegeven in het volgende codefragment Hallo. Hallo hive-script gebruikt deze variabele tooload Hallo gegevens uit de juiste map Hallo voor Hallo dag en Voer Hallo aggregatie toogenerate Hallo uitvoer.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
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
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

Hallo toont volgende diagram Hallo scenario uit het oogpunt van een gegevens-afhankelijkheid.

![Gegevensafhankelijkheid](./media/data-factory-scheduling-and-execution/data-dependency.png)

Hallo uitvoer segment voor elke dag, is afhankelijk van 24 uur segmenten van een invoergegevensset. Berekent de Data Factory deze afhankelijkheden automatisch door uitzoeken Hallo invoergegevens segmenten die in Hallo vallen dezelfde periode zoals Hallo uitvoer segment toobe geproduceerd. Als een van de invoersegmenten één keer Hallo 24 niet beschikbaar is, wacht de Data Factory Hallo invoersegment toobe gereed is voordat u begint Hallo dagelijkse activiteit die wordt uitgevoerd.

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a>Voorbeeld 2: Geef afhankelijkheid met expressies en functies van de Data Factory
Laten we eens een ander scenario. Stel dat u hebt een hive-activiteit die twee invoergegevenssets verwerkt. Een van deze nieuwe gegevens dagelijks heeft, maar één van deze nieuwe gegevens worden elke week opgehaald. Stel dat u deze wilde toodo een join tussen de twee invoeren Hallo en elke dag wordt een uitvoer geproduceerd.

Hallo eenvoudige benadering waarin cijfers Data Factory automatisch uit de juiste invoerwaarden Hallo segmenten tooprocess door toohello uitvoer gegevens segmenttijd periode niet werkt.

U moet opgeven dat voor elke activiteit die wordt uitgevoerd, Hallo Data Factory gegevenssegment afgelopen week voor wekelijkse invoergegevensset Hallo gebruiken moet. U Azure Data Factory-functies, zoals wordt weergegeven in het volgende codefragment tooimplement Hallo dit gedrag gebruiken.

**Input1: Azure blob**

eerste invoer Hello wordt hello Azure blob wordt dagelijks bijgewerkt.

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Input2: Azure blob**

Input2 is hello Azure blob wekelijks worden bijgewerkt.

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

**Uitvoer: Azure blob**

Een bestand voor uitvoer wordt elke dag gemaakt in de map Hallo Hallo dag. Beschikbaarheid van de uitvoer is ingesteld, te**dag** (frequentie: dag, interval: 1).

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Activiteit: hive-activiteit in een pijplijn**

Hallo hive-activiteit duurt Hallo twee invoeritems en een uitvoer-segment wordt geproduceerd elke dag. U kunt opgeven dat elke dag uitvoer segment toodepend op Hallo invoersegment met de vorige week voor wekelijkse invoer als volgt.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

Zie [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md) voor een lijst met functies en systeemvariabelen die ondersteuning biedt voor Data Factory.

## <a name="appendix"></a>Bijlage

### <a name="example-copy-sequentially"></a>Voorbeeld: sequentieel kopiëren
Het is mogelijk toorun meerdere kopieerbewerkingen achter elkaar op een manier opeenvolgende/gerangschikt. U wellicht bijvoorbeeld twee kopiëren gegevens activiteiten in een pijplijn (CopyActivity1 en CopyActivity2) met Hallo na invoer uitvoergegevenssets:   

CopyActivity1

Invoer: Dataset. Uitvoer: Dataset2.

CopyActivity2

Invoer: Dataset2.  Uitvoer: Dataset3.

CopyActivity2 uitgevoerd alleen als Hallo CopyActivity1 met succes is uitgevoerd en Dataset2 beschikbaar is.

Hier volgt Hallo voorbeeldpijplijn JSON:

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

U ziet dat de uitvoergegevensset Hallo Hallo eerste kopieeractiviteit (Dataset2) in Hallo bijvoorbeeld is opgegeven als invoer voor de tweede activiteit Hallo. Daarom Hallo tweede activiteit wordt alleen uitgevoerd als Hallo uitvoergegevensset van de eerste activiteit Hallo gereed is.  

In voorbeeld Hallo kunt CopyActivity2 een andere invoer, zoals Dataset3, maar u Dataset2 opgeven als een invoer tooCopyActivity2 zodat Hallo activiteit kan niet worden uitgevoerd totdat CopyActivity1 is voltooid. Bijvoorbeeld:

CopyActivity1

Invoer: Dataset1. Uitvoer: Dataset2.

CopyActivity2

Invoer: Dataset3, Dataset2. Uitvoer: Dataset4.

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

U ziet in Hallo voorbeeld worden twee invoergegevenssets opgegeven voor de tweede kopieeractiviteit Hallo. Wanneer meerdere invoer zijn opgegeven, wordt alleen Hallo eerste invoergegevensset wordt gebruikt voor het kopiëren van gegevens, maar andere gegevenssets worden gebruikt als afhankelijkheden. CopyActivity2 zou pas beginnen nadat hello volgende voorwaarden wordt voldaan:

* CopyActivity1 is voltooid en Dataset2 is beschikbaar. Deze gegevensset wordt niet gebruikt bij het kopiëren van gegevens tooDataset4. Deze alleen fungeert als een afhankelijkheid van de planning voor CopyActivity2.   
* Dataset3 is beschikbaar. Deze gegevensset vertegenwoordigt Hallo-gegevens die gekopieerde toohello doel. 
