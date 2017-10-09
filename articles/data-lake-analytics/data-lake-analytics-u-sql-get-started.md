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
# <a name="get-started-with-u-sql"></a><span data-ttu-id="7b9bf-103">Aan de slag met U-SQL</span><span class="sxs-lookup"><span data-stu-id="7b9bf-103">Get started with U-SQL</span></span>
<span data-ttu-id="7b9bf-104">U-SQL is een taal die declaratieve SQL combineert met imperatieve C# toolet u gegevens op elke schaal verwerken.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-104">U-SQL is a language that combines declarative SQL with imperative C# toolet you process data at any scale.</span></span> <span data-ttu-id="7b9bf-105">Via Hallo functie schaalbare, gedistribueerde query van U-SQL, kunt u gegevens efficiënt te analyseren in relationele winkels zoals Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-105">Through hello scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="7b9bf-106">U kunt met de U-SQL, ongestructureerde gegevens verwerken met schema toepassen op lezen en het invoegen van aangepaste regels en UDF's.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="7b9bf-107">U-SQL bevat bovendien uitbreidbaarheid waarmee u fijnmazig controle over hoe tooexecute op grote schaal.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how tooexecute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="7b9bf-108">Trainingsmateriaal</span><span class="sxs-lookup"><span data-stu-id="7b9bf-108">Learning resources</span></span>

* <span data-ttu-id="7b9bf-109">Hallo [U-SQL-zelfstudie](http://aka.ms/usqltutorial) biedt aanwijzingen van meest van Hallo U-SQL-taal.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-109">hello [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of hello U-SQL language.</span></span> <span data-ttu-id="7b9bf-110">Dit document wordt aanbevolen voor alle productiviteitsniveau toolearn U-SQL-ontwikkelaars lezen.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-110">This document is recommended reading for all developers wanting toolearn U-SQL.</span></span>
* <span data-ttu-id="7b9bf-111">Voor gedetailleerde informatie over Hallo **U-SQL-syntaxis**, Zie Hallo [naslaginformatie U-SQL-taal](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="7b9bf-111">For detailed information about hello **U-SQL language syntax**, see hello [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="7b9bf-112">Hallo toounderstand **U-SQL-ontwerpplan**, Zie Hallo Visual Studio blogbericht [introductie van U-SQL: een taal die gemakkelijk grote gegevensverwerking](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="7b9bf-112">toounderstand hello **U-SQL design philosophy**, see hello Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b9bf-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7b9bf-113">Prerequisites</span></span>

<span data-ttu-id="7b9bf-114">Voordat u via Hallo U-SQL-voorbeelden in dit document gaat, lezen en voltooien [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7b9bf-114">Before you go through hello U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="7b9bf-115">Deze zelfstudie wordt uitgelegd hoe Hallo mechanisme van U-SQL met met Azure Data Lake Tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-115">That tutorial explains hello mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="7b9bf-116">Uw eerste U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="7b9bf-116">Your first U-SQL script</span></span>

<span data-ttu-id="7b9bf-117">Hallo volgende U-SQL-script is eenvoudig en kan we veel aspecten Hallo U-SQL-taal verkennen.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-117">hello following U-SQL script is simple and lets us explore many aspects hello U-SQL language.</span></span>

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

<span data-ttu-id="7b9bf-118">Dit script is geen transformatie stappen.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="7b9bf-119">Gelezen uit Hallo bronbestand aangeroepen `SearchLog.tsv`, het schematizes en Hallo rijenset terug naar een bestand met de naam SearchLog-first-u sql.csv schrijft.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-119">It reads from hello source file called `SearchLog.tsv`, schematizes it, and writes hello rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="7b9bf-120">Let op Hallo vraagteken volgende toohello gegevenstype in Hallo `Duration` veld.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-120">Notice hello question mark next toohello data type in hello `Duration` field.</span></span> <span data-ttu-id="7b9bf-121">Dit betekent dat Hallo `Duration` veld kan niet null zijn.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-121">It means that hello `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="7b9bf-122">Belangrijkste concepten</span><span class="sxs-lookup"><span data-stu-id="7b9bf-122">Key concepts</span></span>
* <span data-ttu-id="7b9bf-123">**Variabelen voor de rijenset**: elke query-expressie die een rijenset produceert tooa variabele kan worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-123">**Rowset variables**: Each query expression that produces a rowset can be assigned tooa variable.</span></span> <span data-ttu-id="7b9bf-124">U-SQL volgt Hallo TSQL-variabele naamgevingspatroon (`@searchlog`, bijvoorbeeld) in het Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-124">U-SQL follows hello T-SQL variable naming pattern (`@searchlog`, for example) in hello script.</span></span>
* <span data-ttu-id="7b9bf-125">Hallo **EXTRAHEREN** sleutelwoord leest de gegevens uit een bestand en definieert Hallo schema bij lezen.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-125">hello **EXTRACT** keyword reads data from a file and defines hello schema on read.</span></span> <span data-ttu-id="7b9bf-126">`Extractors.Tsv`is een ingebouwde U-SQL zelfstandig uitpakken voor bestanden tabblad's gescheiden waarden.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="7b9bf-127">U kunt aangepaste extractie ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="7b9bf-128">Hallo **uitvoer** schrijft gegevens uit een rijenset tooa-bestand.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-128">hello **OUTPUT** writes data from a rowset tooa file.</span></span> <span data-ttu-id="7b9bf-129">`Outputters.Csv()`is een ingebouwde U-SQL outputter toocreate een bestand met door komma's gescheiden waarden.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-129">`Outputters.Csv()` is a built-in U-SQL outputter toocreate a comma-separated-value file.</span></span> <span data-ttu-id="7b9bf-130">U kunt aangepaste outputters ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="7b9bf-131">Bestandspaden</span><span class="sxs-lookup"><span data-stu-id="7b9bf-131">File paths</span></span>

<span data-ttu-id="7b9bf-132">Gebruik bestandspaden Hallo uitpakken en uitvoer-instructies.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-132">hello EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="7b9bf-133">Absolute of relatieve zijn paden:</span><span class="sxs-lookup"><span data-stu-id="7b9bf-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="7b9bf-134">Deze volgende absoluut bestandspad verwijst tooa-bestand in een Data Lake Store met de naam `mystore`:</span><span class="sxs-lookup"><span data-stu-id="7b9bf-134">This following absolute file path refers tooa file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="7b9bf-135">Deze volgende bestandspad begint met `"/"`.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="7b9bf-136">Het verwijst tooa-bestand in Hallo standaard Data Lake Store-account:</span><span class="sxs-lookup"><span data-stu-id="7b9bf-136">It refers tooa file in hello default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="7b9bf-137">Scalaire variabelen gebruiken</span><span class="sxs-lookup"><span data-stu-id="7b9bf-137">Use scalar variables</span></span>

<span data-ttu-id="7b9bf-138">U kunt scalaire variabelen gebruiken als goed toomake uw script onderhoud eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-138">You can use scalar variables as well toomake your script maintenance easier.</span></span> <span data-ttu-id="7b9bf-139">Hallo vorige U-SQL-script kan ook worden opgeslagen als:</span><span class="sxs-lookup"><span data-stu-id="7b9bf-139">hello previous U-SQL script can also be written as:</span></span>

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

## <a name="transform-rowsets"></a><span data-ttu-id="7b9bf-140">Rijensets transformeren</span><span class="sxs-lookup"><span data-stu-id="7b9bf-140">Transform rowsets</span></span>

<span data-ttu-id="7b9bf-141">Gebruik **Selecteer** tootransform rijensets:</span><span class="sxs-lookup"><span data-stu-id="7b9bf-141">Use **SELECT** tootransform rowsets:</span></span>

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

<span data-ttu-id="7b9bf-142">Hallo WHERE-component gebruikt een [C# Boole-expressie](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b9bf-142">hello WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="7b9bf-143">U kunt Hallo C#-expressie taal toodo uw eigen expressies en functies.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-143">You can use hello C# expression language toodo your own expressions and functions.</span></span> <span data-ttu-id="7b9bf-144">U kunt zelfs uitvoeren complexere filteren ze te combineren met logische voegwoorden (programmapad en) en disjunctions (ORs).</span><span class="sxs-lookup"><span data-stu-id="7b9bf-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="7b9bf-145">Hallo volgende script gebruikt Hallo DateTime.Parse() methode en een combinatie.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-145">hello following script uses hello DateTime.Parse() method and a conjunction.</span></span>

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
 ><span data-ttu-id="7b9bf-146">Hallo tweede query wordt uitgevoerd op Hallo resultaat van de eerste rijenset hello, die wordt gemaakt van een samenstelling van Hallo twee filters.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-146">hello second query is operating on hello result of hello first rowset, which creates a composite of hello two filters.</span></span> <span data-ttu-id="7b9bf-147">U kunt ook een variabelenaam hergebruiken en Hallo namen lexically zijn gericht.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-147">You can also reuse a variable name, and hello names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="7b9bf-148">Cumulatieve rijensets</span><span class="sxs-lookup"><span data-stu-id="7b9bf-148">Aggregate rowsets</span></span>
<span data-ttu-id="7b9bf-149">U-SQL kunt u Hallo bekend ORDER BY, GROUP BY en aggregaties.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-149">U-SQL gives you hello familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="7b9bf-150">Hallo volgende query zoekt Hallo totale duur per regio en wordt vervolgens weergegeven Hallo top vijf duur in volgorde.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-150">hello following query finds hello total duration per region, and then displays hello top five durations in order.</span></span>

<span data-ttu-id="7b9bf-151">U-SQL-rijensets blijven niet behouden in de volgorde voor de volgende query Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-151">U-SQL rowsets do not preserve their order for hello next query.</span></span> <span data-ttu-id="7b9bf-152">Dus tooorder een uitvoer, moet u tooadd ORDER BY toohello uitvoer-instructie:</span><span class="sxs-lookup"><span data-stu-id="7b9bf-152">Thus, tooorder an output, you need tooadd ORDER BY toohello OUTPUT statement:</span></span>

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

<span data-ttu-id="7b9bf-153">Hallo U-SQL ORDER BY-component, moet u Hallo ophalen-component in een SELECT-expressie.</span><span class="sxs-lookup"><span data-stu-id="7b9bf-153">hello U-SQL ORDER BY clause requires using hello FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="7b9bf-154">Hallo die van U-SQL-component kan gebruikte toorestrict Hallo uitvoer toogroups die voldoen aan Hallo HAVING voorwaarde zijn:</span><span class="sxs-lookup"><span data-stu-id="7b9bf-154">hello U-SQL HAVING clause can be used toorestrict hello output toogroups that satisfy hello HAVING condition:</span></span>

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

<span data-ttu-id="7b9bf-155">Zie voor aggregatie van geavanceerde scenario's, Hallo Hallo U-SQL-naslagdocumentatie voor [statistische analyse- en verwijzingstypen van functies](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="7b9bf-155">For advanced aggregation scenarios, see hello hello U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b9bf-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7b9bf-156">Next steps</span></span>
* [<span data-ttu-id="7b9bf-157">Overzicht van Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7b9bf-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="7b9bf-158">U-SQL-scripts ontwikkelen met Data Lake-hulpmiddelen voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b9bf-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
