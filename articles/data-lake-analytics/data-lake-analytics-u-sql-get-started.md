---
title: Aan de slag met U-SQL-taal | Microsoft Docs
description: Hallo basisbegrippen Hallo U-SQL-taal.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a>Aan de slag met U-SQL
U-SQL is een taal die declaratieve SQL combineert met imperatieve C# toolet u gegevens op elke schaal verwerken. Via Hallo functie schaalbare, gedistribueerde query van U-SQL, kunt u gegevens efficiënt te analyseren in relationele winkels zoals Azure SQL Database. U kunt met de U-SQL, ongestructureerde gegevens verwerken met schema toepassen op lezen en het invoegen van aangepaste regels en UDF's. U-SQL bevat bovendien uitbreidbaarheid waarmee u fijnmazig controle over hoe tooexecute op grote schaal. 

## <a name="learning-resources"></a>Trainingsmateriaal

* Hallo [U-SQL-zelfstudie](http://aka.ms/usqltutorial) biedt aanwijzingen van meest van Hallo U-SQL-taal. Dit document wordt aanbevolen voor alle productiviteitsniveau toolearn U-SQL-ontwikkelaars lezen.
* Voor gedetailleerde informatie over Hallo **U-SQL-syntaxis**, Zie Hallo [naslaginformatie U-SQL-taal](http://go.microsoft.com/fwlink/p/?LinkId=691348).
* Hallo toounderstand **U-SQL-ontwerpplan**, Zie Hallo Visual Studio blogbericht [introductie van U-SQL: een taal die gemakkelijk grote gegevensverwerking](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

## <a name="prerequisites"></a>Vereisten

Voordat u via Hallo U-SQL-voorbeelden in dit document gaat, lezen en voltooien [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Deze zelfstudie wordt uitgelegd hoe Hallo mechanisme van U-SQL met met Azure Data Lake Tools voor Visual Studio.

## <a name="your-first-u-sql-script"></a>Uw eerste U-SQL-script

Hallo volgende U-SQL-script is eenvoudig en kan we veel aspecten Hallo U-SQL-taal verkennen.

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
    USING Extractors.Tsv();

OUTPUT @searchlog   
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

Dit script is geen transformatie stappen. Gelezen uit Hallo bronbestand aangeroepen `SearchLog.tsv`, het schematizes en Hallo rijenset terug naar een bestand met de naam SearchLog-first-u sql.csv schrijft.

Let op Hallo vraagteken volgende toohello gegevenstype in Hallo `Duration` veld. Dit betekent dat Hallo `Duration` veld kan niet null zijn.

### <a name="key-concepts"></a>Belangrijkste concepten
* **Variabelen voor de rijenset**: elke query-expressie die een rijenset produceert tooa variabele kan worden toegewezen. U-SQL volgt Hallo TSQL-variabele naamgevingspatroon (`@searchlog`, bijvoorbeeld) in het Hallo-script.
* Hallo **EXTRAHEREN** sleutelwoord leest de gegevens uit een bestand en definieert Hallo schema bij lezen. `Extractors.Tsv`is een ingebouwde U-SQL zelfstandig uitpakken voor bestanden tabblad's gescheiden waarden. U kunt aangepaste extractie ontwikkelen.
* Hallo **uitvoer** schrijft gegevens uit een rijenset tooa-bestand. `Outputters.Csv()`is een ingebouwde U-SQL outputter toocreate een bestand met door komma's gescheiden waarden. U kunt aangepaste outputters ontwikkelen.

### <a name="file-paths"></a>Bestandspaden

Gebruik bestandspaden Hallo uitpakken en uitvoer-instructies. Absolute of relatieve zijn paden:

Deze volgende absoluut bestandspad verwijst tooa-bestand in een Data Lake Store met de naam `mystore`:

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

Deze volgende bestandspad begint met `"/"`. Het verwijst tooa-bestand in Hallo standaard Data Lake Store-account:

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a>Scalaire variabelen gebruiken

U kunt scalaire variabelen gebruiken als goed toomake uw script onderhoud eenvoudiger. Hallo vorige U-SQL-script kan ook worden opgeslagen als:

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a>Rijensets transformeren

Gebruik **Selecteer** tootransform rijensets:

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

Hallo WHERE-component gebruikt een [C# Boole-expressie](https://msdn.microsoft.com/library/6a71f45d.aspx). U kunt Hallo C#-expressie taal toodo uw eigen expressies en functies. U kunt zelfs uitvoeren complexere filteren ze te combineren met logische voegwoorden (programmapad en) en disjunctions (ORs).

Hallo volgende script gebruikt Hallo DateTime.Parse() methode en een combinatie.

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 >Hallo tweede query wordt uitgevoerd op Hallo resultaat van de eerste rijenset hello, die wordt gemaakt van een samenstelling van Hallo twee filters. U kunt ook een variabelenaam hergebruiken en Hallo namen lexically zijn gericht.

## <a name="aggregate-rowsets"></a>Cumulatieve rijensets
U-SQL kunt u Hallo bekend ORDER BY, GROUP BY en aggregaties.

Hallo volgende query zoekt Hallo totale duur per regio en wordt vervolgens weergegeven Hallo top vijf duur in volgorde.

U-SQL-rijensets blijven niet behouden in de volgorde voor de volgende query Hallo. Dus tooorder een uitvoer, moet u tooadd ORDER BY toohello uitvoer-instructie:

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

Hallo U-SQL ORDER BY-component, moet u Hallo ophalen-component in een SELECT-expressie.

Hallo die van U-SQL-component kan gebruikte toorestrict Hallo uitvoer toogroups die voldoen aan Hallo HAVING voorwaarde zijn:

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

Zie voor aggregatie van geavanceerde scenario's, Hallo Hallo U-SQL-naslagdocumentatie voor [statistische analyse- en verwijzingstypen van functies](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)

## <a name="next-steps"></a>Volgende stappen
* [Overzicht van Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [U-SQL-scripts ontwikkelen met Data Lake-hulpmiddelen voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
