---
title: aaaExtend U-SQL-scripts met behulp van Python in Azure Data Lake Analytics | Microsoft Docs
description: Meer informatie over hoe toorun Python code in de U-SQL-Scripts
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="4465c-103">Zelfstudie: Aan de slag met het uitbreiden van U-SQL met behulp van Python</span><span class="sxs-lookup"><span data-stu-id="4465c-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="4465c-104">Python-uitbreidingen voor de U-SQL kunt ontwikkelaars tooperform massively parallelle uitvoering van Python-code.</span><span class="sxs-lookup"><span data-stu-id="4465c-104">Python Extensions for U-SQL enable developers tooperform massively parallel execution of Python code.</span></span> <span data-ttu-id="4465c-105">Hallo volgende voorbeeld illustreert Hallo eenvoudige stappen:</span><span class="sxs-lookup"><span data-stu-id="4465c-105">hello following example illustrates hello basic steps:</span></span>

* <span data-ttu-id="4465c-106">Gebruik Hallo `REFERENCE ASSEMBLY` instructie tooenable Python-extensies voor Hallo U-SQL-Script</span><span class="sxs-lookup"><span data-stu-id="4465c-106">Use hello `REFERENCE ASSEMBLY` statement tooenable Python extensions for hello U-SQL Script</span></span>
* <span data-ttu-id="4465c-107">Met behulp van Hallo `REDUCE` bewerking toopartition Hallo invoergegevens voor een sleutel</span><span class="sxs-lookup"><span data-stu-id="4465c-107">Using hello `REDUCE` operation toopartition hello input data on a key</span></span>
* <span data-ttu-id="4465c-108">Hallo Python-uitbreidingen voor de U-SQL bevatten een ingebouwde reducer (`Extension.Python.Reducer`) die op elke hoekpunt toegewezen toohello reducer Python-code wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="4465c-108">hello Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned toohello reducer</span></span>
* <span data-ttu-id="4465c-109">Hallo U-SQL-script bevat Hallo ingesloten Python-code die een functie die wordt aangeroepen `usqlml_main` die een pandas DataFrame als invoer accepteert en retourneert een pandas DataFrame als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4465c-109">hello U-SQL script contains hello embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="4465c-110">Hoe Python integreert met U-SQL</span><span class="sxs-lookup"><span data-stu-id="4465c-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="4465c-111">Gegevenstypen</span><span class="sxs-lookup"><span data-stu-id="4465c-111">Datatypes</span></span>

* <span data-ttu-id="4465c-112">Zo worden geconverteerd als tekenreeks en numerieke kolommen uit de U-SQL-tussen Pandas en U-SQL</span><span class="sxs-lookup"><span data-stu-id="4465c-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="4465c-113">U-SQL null-waarden zijn geconverteerde tooand van Pandas `NA` waarden</span><span class="sxs-lookup"><span data-stu-id="4465c-113">U-SQL Nulls are converted tooand from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="4465c-114">Schema 's</span><span class="sxs-lookup"><span data-stu-id="4465c-114">Schemas</span></span>

* <span data-ttu-id="4465c-115">Index aanvalsvectoren in Pandas worden niet ondersteund in de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4465c-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="4465c-116">Alle ingevoerde gegevensframes in Hallo Python functie hebben altijd een 64-bits numerieke index 0 tot en met Hallo aantal rijen min 1.</span><span class="sxs-lookup"><span data-stu-id="4465c-116">All input data frames in hello Python function always have a 64-bit numerical index from 0 through hello number of rows minus 1.</span></span> 
* <span data-ttu-id="4465c-117">U-SQL-gegevenssets kan geen dubbele kolomnamen hebben</span><span class="sxs-lookup"><span data-stu-id="4465c-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="4465c-118">U-SQL gegevenssets kolomnamen die geen tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="4465c-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="4465c-119">Python-versies</span><span class="sxs-lookup"><span data-stu-id="4465c-119">Python Versions</span></span>
<span data-ttu-id="4465c-120">Alleen Python 3.5.1 (gecompileerd voor Windows) wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4465c-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="4465c-121">Standaard Python-modules</span><span class="sxs-lookup"><span data-stu-id="4465c-121">Standard Python modules</span></span>
<span data-ttu-id="4465c-122">Alle Hallo standaard Python-modules zijn opgenomen.</span><span class="sxs-lookup"><span data-stu-id="4465c-122">All hello standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="4465c-123">Extra Python-modules</span><span class="sxs-lookup"><span data-stu-id="4465c-123">Additional Python modules</span></span>
<span data-ttu-id="4465c-124">Afgezien van Python standaardbibliotheken hello, is enkele veelgebruikte python-bibliotheken zijn opgenomen:</span><span class="sxs-lookup"><span data-stu-id="4465c-124">Besides hello standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="4465c-125">Uitzondering berichten</span><span class="sxs-lookup"><span data-stu-id="4465c-125">Exception Messages</span></span>
<span data-ttu-id="4465c-126">Op dit moment is een uitzondering in Python-code wordt weergegeven als algemene hoekpunt mislukt.</span><span class="sxs-lookup"><span data-stu-id="4465c-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="4465c-127">In toekomstige hello weergegeven Hallo U-SQL-taak foutberichten Hallo Python uitzonderingsbericht.</span><span class="sxs-lookup"><span data-stu-id="4465c-127">In hello future, hello U-SQL Job error messages will display hello Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="4465c-128">Invoer en uitvoer groottebeperkingen</span><span class="sxs-lookup"><span data-stu-id="4465c-128">Input and Output size limitations</span></span>
<span data-ttu-id="4465c-129">Elke hoekpunt heeft een beperkte hoeveelheid geheugen die tooit is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="4465c-129">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="4465c-130">Deze limiet is momenteel 6 GB voor een AU.</span><span class="sxs-lookup"><span data-stu-id="4465c-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="4465c-131">Omdat hello invoer en uitvoer DataFrames moet bestaan in het geheugen van Hallo Python-code, kan niet Hallo totale voor Hallo invoer en uitvoer groter zijn dan 6 GB.</span><span class="sxs-lookup"><span data-stu-id="4465c-131">Because hello input and output DataFrames must exist in memory in hello Python code, hello total size for hello input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="4465c-132">Zie ook</span><span class="sxs-lookup"><span data-stu-id="4465c-132">See also</span></span>
* [<span data-ttu-id="4465c-133">Overzicht van Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4465c-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="4465c-134">U-SQL-scripts ontwikkelen met Data Lake-hulpmiddelen voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4465c-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="4465c-135">U-SQL-vensterfuncties gebruiken voor Azure Data Lake Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="4465c-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

