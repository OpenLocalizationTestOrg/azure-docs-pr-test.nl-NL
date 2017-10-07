---
title: aaaData Factory functies en systeemvariabelen | Microsoft Docs
description: Geeft een lijst van Azure Data Factory-functies en systeemvariabelen
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a>Azure Data Factory - functies en systeemvariabelen
Dit artikel bevat informatie over functies en variabelen die worden ondersteund door Azure Data Factory.

## <a name="data-factory-system-variables"></a>Data Factory-systeemvariabelen
| Naam variabele | Beschrijving | Bereik van het object | JSON-bereik en gebruiksvoorbeelden |
| --- | --- | --- | --- |
| WindowStart |Begin van het tijdsinterval voor de huidige activiteit venster uitvoeren |Activiteit |<ol><li>Geef op query's voor selectie. Zie connector artikelen waarnaar wordt verwezen in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel.</li> |
| WindowEnd |Einde van het tijdsinterval voor de huidige activiteit venster uitvoeren |Activiteit |hetzelfde als WindowStart. |
| SliceStart |Begin van het tijdsinterval voor het segment wordt geproduceerd |Activiteit<br/>Gegevensset |<ol><li>Geef dynamische paden en bestandsnamen tijdens het werken met [Azure Blob](data-factory-azure-blob-connector.md) en [bestandssysteem gegevenssets](data-factory-onprem-file-system-connector.md).</li><li>Invoer afhankelijkheden data factory-functies in activiteit invoer verzameling opgeven.</li></ol> |
| SliceEnd |Einde van de tijdsinterval voor het huidige segment. |Activiteit<br/>Gegevensset |hetzelfde als SliceStart. |

> [!NOTE]
> Op dit moment gegevensfactory vereist dat Hallo plannen opgegeven in de Hallo Hallo schema is opgegeven in de beschikbaarheid van de uitvoergegevensset Hallo exact overeenkomt met de activiteit. Daarom WindowStart, WindowEnd, en SliceStart en SliceEnd worden altijd toegewezen toohello dezelfde periode en een segment één uitvoer time.
> 

### <a name="example-for-using-a-system-variable"></a>Voorbeeld voor het gebruik van een systeemvariabele
In het volgende voorbeeld, jaar, maand, dag en tijd van Hallo **SliceStart** worden uitgepakt in verschillende variabelen die worden gebruikt door **folderPath** en **fileName** eigenschappen.

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

## <a name="data-factory-functions"></a>Data Factory-functies
U kunt functies gebruiken in gegevensfactory samen met systeemvariabelen voor Hallo volgende doeleinden:

1. Query's voor selectie opgeven (Zie connector artikelen waarnaar wordt verwezen door Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel.
   
   Hallo syntaxis tooinvoke een data factory-functie is:  **$$ <function>**  voor selectie van query's en andere eigenschappen in het Hallo-activiteit en gegevenssets.  
2. Invoer afhankelijkheden opgeven data factory-functies in activiteit invoer verzameling.
   
    $$ is niet nodig voor het opgeven van invoer afhankelijkheid expressies.     

In het volgende voorbeeld Hallo **sqlReaderQuery** eigenschap in een JSON-bestand is toegewezen tooa-waarde geretourneerd door Hallo `Text.Format` functie. Dit voorbeeld gebruikt ook een systeemvariabele met de naam **WindowStart**, die staat voor Hallo-begintijd van Hallo-activiteit venster uitvoeren.

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

Zie [aangepaste datum en tijd-indeling tekenreeksen](https://msdn.microsoft.com/library/8kb3ddd4.aspx) onderwerp dat beschrijft de verschillende opmaakopties die u kunt gebruiken (bijvoorbeeld: ay versus jjjj). 

### <a name="functions"></a>Functies
Hallo tabellen na een overzicht van alle Hallo-functies in Azure Data Factory:

| Category | Functie | Parameters | Beschrijving |
| --- | --- | --- | --- |
| Time |AddHours(X,Y) |X: datum/tijd <br/><br/>Y: int |Voegt Y uren toohello gelegenheid X. <br/><br/>Voorbeeld:`9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM` |
| Time |AddMinutes(X,Y) |X: datum/tijd <br/><br/>Y: int |Y minuten tooX toegevoegd.<br/><br/>Voorbeeld:`9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM` |
| Time |StartOfHour(X) |X: datum/tijd |Opgehaald Hallo begintijd voor Hallo uur dat wordt vertegenwoordigd door Hallo uurgedeelte van X. <br/><br/>Voorbeeld:`StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM` |
| Date |AddDays(X,Y) |X: datum/tijd<br/><br/>Y: int |Y dagen tooX toegevoegd. <br/><br/>Voorbeeld: 9, 15/2013 12:00:00 PM + 2 dagen = 9/17/2013 12:00:00 PM.<br/><br/>U kunt dagen te aftrekken door te geven Y als een negatief getal.<br/><br/>Voorbeeld: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`. |
| Date |AddMonths(X,Y) |X: datum/tijd<br/><br/>Y: int |Y maanden tooX toegevoegd.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.<br/><br/>U kunt maanden te aftrekken door te geven Y als een negatief getal.<br/><br/>Voorbeeld: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.|
| Date |AddQuarters(X,Y) |X: datum/tijd <br/><br/>Y: int |Voegt Y * tooX 3 maanden.<br/><br/>Voorbeeld:`9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM` |
| Date |AddWeeks(X,Y) |X: datum/tijd<br/><br/>Y: int |Voegt Y * tooX 7 dagen<br/><br/>Voorbeeld: 9, 15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 uur<br/><br/>U kunt de weken te aftrekken door te geven Y als een negatief getal.<br/><br/>Voorbeeld: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`. |
| Date |AddYears(X,Y) |X: datum/tijd<br/><br/>Y: int |Y jaar tooX toegevoegd.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/>U kunt jaar te aftrekken door te geven Y als een negatief getal.<br/><br/>Voorbeeld: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`. |
| Date |Day(X) |X: datum/tijd |Hiermee haalt u Hallo daggedeelte van X.<br/><br/>Voorbeeld: `Day of 9/15/2013 12:00:00 PM is 9`. |
| Date |DayOfWeek(X) |X: datum/tijd |Hiermee haalt u Hallo dag van het onderdeel van de week van X.<br/><br/>Voorbeeld: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`. |
| Date |DayOfYear(X) |X: datum/tijd |Hiermee haalt u Hallo dag in Hallo jaar, uitgedrukt in Hallo jaargedeelte van X.<br/><br/>Voorbeelden:<br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| Date |DaysInMonth(X) |X: datum/tijd |Hallo dagen in Hallo maand dat wordt vertegenwoordigd door Hallo maandgedeelte van de parameter X opgehaald.<br/><br/>Voorbeeld: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`. |
| Date |EndOfDay(X) |X: datum/tijd |Hiermee haalt u Hallo datum-tijd die Hallo-einde van Hallo dag (daggedeelte) van X aangeeft.<br/><br/>Voorbeeld: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`. |
| Date |EndOfMonth(X) |X: datum/tijd |Hallo-einde van Hallo maand dat wordt vertegenwoordigd door maandgedeelte van de parameter X opgehaald. <br/><br/>Voorbeeld: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (datum / tijd die Hallo einde van September maand vertegenwoordigt) |
| Date |StartOfDay(X) |X: datum/tijd |Hiermee haalt u Hallo Hallo dag dat wordt vertegenwoordigd door Hallo daggedeelte van de parameter X is gestart.<br/><br/>Voorbeeld: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`. |
| Datum/tijd |FROM(X) |X: de tekenreeks |Parseren van tekenreeks X tooa datum / tijd. |
| Datum/tijd |Ticks(X) |X: datum/tijd |Hallo ticks eigenschap van de parameter Hallo X opgehaald. Eén tik is gelijk aan 100 nanoseconden. Hallo-waarde van deze eigenschap vertegenwoordigt Hallo aantal maatstreepjes dat is verstreken sinds 12:00:00 middernacht, 1 januari 0001. |
| Tekst |Format(X) |X: tekenreeksvariabele |Indelingen tekst hello (Gebruik `\\'` combinatie tooescape `'` teken).|

> [!IMPORTANT]
> Wanneer u een functie binnen een andere functie, hoeft u niet toouse  **$$**  voorvoegsel voor de interne Hallo-functie. Bijvoorbeeld: $$Text.Format ('PartitionKey eq \\' my_pkey_filter_value\\' en RowKey ge \\' {0: jjjj-MM-dd: mm: SS}\\'', Time.AddHours (SliceStart -6)). U ziet dat in dit voorbeeld  **$$**  voorvoegsel wordt niet gebruikt voor Hallo **Time.AddHours** functie. 

#### <a name="example"></a>Voorbeeld
In Hallo volgende bijvoorbeeld invoer en uitvoer parameters voor Hallo Hive-activiteit worden bepaald met behulp van Hallo `Text.Format` functie en SliceStart systeemvariabele. 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a>Voorbeeld 2

Hallo in Hallo voorbeeld te volgen, DateTime-parameter voor de activiteit opgeslagen Procedure is bepaald met behulp van de tekst hello Hallo. Functie formatteren en Hallo SliceStart-variabele. 

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
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a>Voorbeeld 3
tooread gegevens uit de vorige dag in plaats van de dag dat wordt vertegenwoordigd door Hallo SliceStart, gebruik de functie AddDays Hallo zoals getoond in Hallo voorbeeld te volgen: 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
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

Zie [aangepaste datum en tijd-indeling tekenreeksen](https://msdn.microsoft.com/library/8kb3ddd4.aspx) onderwerp dat beschrijft de verschillende opmaakopties die u kunt gebruiken (bijvoorbeeld: jj versus jjjj). 

