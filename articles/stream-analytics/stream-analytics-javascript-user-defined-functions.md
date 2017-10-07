---
title: aaaAzure Stream Analytics JavaScript gebruiker gedefinieerde functies | Microsoft Docs
description: Geavanceerde query mechanisme met de gebruiker gedefinieerde functies van JavaScript uitvoeren
keywords: JavaScript, de gebruiker gedefinieerde functies, udf
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a>Azure Stream Analytics JavaScript gebruiker gedefinieerde functies
Azure Stream Analytics ondersteunt de gebruiker gedefinieerde functies die zijn geschreven in JavaScript. Met uitgebreide set Hallo **tekenreeks**, **RegExp**, **Math**, **matrix**, en **datum** methoden die JavaScript biedt, complexe gegevenstransformaties met Stream Analytics-taken toocreate eenvoudiger geworden.

## <a name="javascript-user-defined-functions"></a>De gebruiker gedefinieerde functies JavaScript
De gebruiker gedefinieerde functies JavaScript ondersteuning voor stateless, compute-alleen scalaire functies die niet nodig voor externe verbinding hebt. Hallo retourneren van een functie mag alleen een scalaire waarde (single). Nadat u een taak JavaScript gebruiker gedefinieerde functie tooa toevoegt, kunt u Hallo functie overal in Hallo query, zoals een ingebouwde scalaire functie gebruiken.

Hier volgen enkele scenario's waar JavaScript gebruiker gedefinieerde functies interessant mogelijk:
* Parseren en manipuleren van tekenreeksen die functies van de reguliere expressie, bijvoorbeeld hebben **Regexp_Replace()** en **Regexp_Extract()**
* Decoderen en gegevens, bijvoorbeeld conversie van binair naar hexadecimale codering
* Rekenkundige berekeningen met JavaScript uitvoeren **Math** functies
* Uitvoeren van bewerkingen zoals sorteren, join, zoeken en opvulling matrix

Hier volgen enkele dingen die u met een JavaScript gebruiker gedefinieerde functie in Stream Analytics kan niet doen:
* Vestigen op externe REST-eindpunten, bijvoorbeeld: uitvoeren van IP-lookup- of opvragen referentiegegevens omkeren van een externe bron
* Indeling van aangepaste gebeurtenisserialisatie uitvoeren of deserialiseren van de invoer/uitvoer
* Maken van aangepaste statistische functies

Hoewel u functies zoals **Date.GetDate()** of **Math.random()** worden niet geblokkeerd in definitie van de functies van Hallo Vermijd het gebruik ervan. Deze functies **niet** return Hallo dezelfde leiden telkens wanneer u deze aanroept en hello Azure Stream Analytics-service geen logboek van de functie aanroepen houdt en resultaten geretourneerd. Als een functie verschillende resultaten op Hallo dezelfde gebeurtenissen retourneert, herhaalbaarheid niet worden gegarandeerd wanneer een taak opnieuw wordt gestart door u of door Hallo Stream Analytics-service.

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a>Toevoegen van een gebruiker gedefinieerde functie van JavaScript in hello Azure-portal
een eenvoudige op JavaScript gebruiker gedefinieerde functie onder een bestaande Stream Analytics-taak toocreate Voer deze stappen uit:

1.  Zoek in hello Azure-portal, Stream Analytics-taak.
2.  Onder **taak TOPOLOGIE**, selecteert u de functie. Een lege lijst met functies wordt weergegeven.
3.  Selecteer een nieuwe gebruiker gedefinieerde functie toocreate **toevoegen**.
4.  Op Hallo **nieuwe functie** blade voor **functietype**, selecteer **JavaScript**. Een standaardsjabloon voor de functie wordt weergegeven in Hallo-editor.
5.  Voor Hallo **UDF alias**, voer **hex2Int**, en implementatie van de functie Hallo als volgt wijzigen:

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  Selecteer **Opslaan**. De functie wordt weergegeven in de lijst met functies Hallo.
7.  Selecteer nieuwe Hallo **hex2Int** functioneren en controleren van de functiedefinitie Hallo. Alle functies een **UDF** voorvoegsel toegevoegde toohello functie alias. U moet te*Hallo voorvoegsel* wanneer u Hallo functie aanroepen in de Stream Analytics-query. In dit geval u aanroepen **UDF.hex2Int**.

## <a name="call-a-javascript-user-defined-function-in-a-query"></a>Een gebruiker gedefinieerde functie van JavaScript-aanroep in een query

1. In Hallo-query-editor, onder **taak TOPOLOGIE**, selecteer **Query**.
2.  Uw query bewerken en vervolgens Hallo gebruiker gedefinieerde functie aanroept als volgt:

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  tooupload hello voorbeeldgegevensbestand, klik met de rechtermuisknop Hallo taak invoer.
4.  tootest uw query, selecteer **Test**.


## <a name="supported-javascript-objects"></a>Ondersteunde JavaScript-objecten
Azure Stream Analytics JavaScript gebruiker gedefinieerde functies ondersteuning voor ingebouwde JavaScript-objecten. Zie voor een lijst van deze objecten [globale objecten](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).

### <a name="stream-analytics-and-javascript-type-conversion"></a>Conversie van stream Analytics en JavaScript

Er zijn verschillen in Hallo-typen die ondersteuning bieden voor Hallo Stream Analytics query language- en JavaScript. Deze tabel bevat Hallo conversie toewijzingen tussen Hallo twee:

Stream Analytics | Javascript
--- | ---
bigint | Nummer (JavaScript kan alleen bestaan uit gehele getallen up tooprecisely 2 ^ 53)
Datum/tijd | Datum (JavaScript alleen ondersteund in milliseconden)
dubbele | Aantal
nvarchar(max) | Tekenreeks
Record | Object
Matrix | Matrix
NULL | Null


Hier volgen JavaScript aan Stream Analytics-conversies:


Javascript | Stream Analytics
--- | ---
Aantal | Bigint (als Hallo getal ronde en tussen lang is. MinValue en een lange. MaxValue; anders is de dubbele)
Date | Datum/tijd
Tekenreeks | nvarchar(max)
Object | Record
Matrix | Matrix
Null is en niet-gedefinieerd | NULL
Een ander type (bijvoorbeeld, een functie of fout) | Niet ondersteund (resulteert in een runtime-fout)

## <a name="troubleshooting"></a>Problemen oplossen
JavaScript-runtime-fouten worden beschouwd als onherstelbare en via het activiteitenlogboek Hallo worden opgehaald. tooretrieve hello log in hello Azure-portal, Ga tooyour taak en selecteert u **activiteitenlogboek**.


## <a name="other-javascript-user-defined-function-patterns"></a>Andere patronen van de gebruiker gedefinieerde functie JavaScript

### <a name="write-nested-json-toooutput"></a>Geneste JSON toooutput schrijven
Als er een vervolgactie verwerkingsstap die gebruikmaakt van een Stream Analytics-taak uitvoer als invoer en hiervoor een JSON-indeling, kunt u een JSON-tekenreeks toooutput schrijven. het volgende voorbeeld Hallo Hallo roept **JSON.stringify()** werken toopack alle naam/waarde-paren Hallo invoer en vervolgens als één enkele tekenreekswaarde in de uitvoer geschreven.

**Definitie van de gebruiker gedefinieerde functie JavaScript:**

```
function main(x) {
return JSON.stringify(x);
}
```

**Voorbeeldquery:**
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a>Help opvragen
Voor aanvullende hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics management REST API-referentiemateriaal](https://msdn.microsoft.com/library/azure/dn835031.aspx)
