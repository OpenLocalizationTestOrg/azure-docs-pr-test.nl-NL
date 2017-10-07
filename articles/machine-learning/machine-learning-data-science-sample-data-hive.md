---
title: aaaSample gegevens in Azure HDInsight Hive-tabellen | Microsoft Docs
description: Omlaag steekproef nemen van gegevens in Azure HDInsight (Hadopop) Hive-tabellen
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="725ea-103">Voorbeeldgegevens in Hive-tabellen in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="725ea-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="725ea-104">In dit artikel wordt beschreven hoe toodown-voorbeeldgegevens opgeslagen in Azure HDInsight Hive-tabellen met Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="725ea-104">In this article, we describe how toodown-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="725ea-105">We hebben betrekking op dit gebruikte steekproeven op drie manieren:</span><span class="sxs-lookup"><span data-stu-id="725ea-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="725ea-106">Uniform steekproeven</span><span class="sxs-lookup"><span data-stu-id="725ea-106">Uniform random sampling</span></span>
* <span data-ttu-id="725ea-107">Steekproeven door groepen</span><span class="sxs-lookup"><span data-stu-id="725ea-107">Random sampling by groups</span></span>
* <span data-ttu-id="725ea-108">Toepassing stratificatie steekproeven</span><span class="sxs-lookup"><span data-stu-id="725ea-108">Stratified sampling</span></span>

<span data-ttu-id="725ea-109">Hallo volgende **menu** koppelingen tootopics waarin wordt beschreven hoe toosample gegevens uit verschillende omgevingen voor opslag.</span><span class="sxs-lookup"><span data-stu-id="725ea-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="725ea-110">**Waarom een steekproef nemen uit uw gegevens?**</span><span class="sxs-lookup"><span data-stu-id="725ea-110">**Why sample your data?**</span></span>
<span data-ttu-id="725ea-111">Als u van plan bent tooanalyze Hallo-gegevensset te groot is, is het meestal een goed idee Hallo toodown-sample data tooreduce het tooa kleiner, maar representatief en gemakkelijker grootte.</span><span class="sxs-lookup"><span data-stu-id="725ea-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="725ea-112">Dit vereenvoudigt het begrip van de gegevens, exploratie en functie-engineering.</span><span class="sxs-lookup"><span data-stu-id="725ea-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="725ea-113">De rol in Hallo Team gegevens wetenschappelijke processen is tooenable snel maken van een prototype van Hallo gegevensverwerking functies en machine learning-modellen.</span><span class="sxs-lookup"><span data-stu-id="725ea-113">Its role in hello Team Data Science Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="725ea-114">Deze taak steekproeven is een stap in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="725ea-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-toosubmit-hive-queries"></a><span data-ttu-id="725ea-115">Hoe toosubmit Hive-query's</span><span class="sxs-lookup"><span data-stu-id="725ea-115">How toosubmit Hive queries</span></span>
<span data-ttu-id="725ea-116">Hive-query's kunnen worden verzonden in Hallo Hadoop-opdrachtregel-console op Hallo hoofdknooppunt van Hallo Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="725ea-116">Hive queries can be submitted from hello Hadoop Command Line console on hello head node of hello Hadoop cluster.</span></span> <span data-ttu-id="725ea-117">toodo dit, meld u aan bij de hoofdknooppunt Hallo van Hallo Hadoop-cluster, opent u Hallo Hadoop-opdrachtregel-console, en het Hallo Hive-query's van daaruit verzenden.</span><span class="sxs-lookup"><span data-stu-id="725ea-117">toodo this, log into hello head node of hello Hadoop cluster, open hello Hadoop Command Line console, and submit hello Hive queries from there.</span></span> <span data-ttu-id="725ea-118">Zie voor instructies voor het indienen van Hive-query's in de Hadoop-opdrachtregel-console Hallo [hoe tooSubmit Hive-query's](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="725ea-118">For instructions on submitting Hive queries in hello Hadoop Command Line console, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="725ea-119"><a name="uniform"></a>Uniform steekproeven</span><span class="sxs-lookup"><span data-stu-id="725ea-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="725ea-120">Uniform steekproeven betekent dat elke rij in de gegevensset Hallo evenveel kans wordt door actieve heeft.</span><span class="sxs-lookup"><span data-stu-id="725ea-120">Uniform random sampling means that each row in hello data set has an equal chance of being sampled.</span></span> <span data-ttu-id="725ea-121">Dit kan worden geïmplementeerd door een extra veld ASELECT() toohello-gegevensset toe te voegen in binnenste 'select' Hallo-query en Hallo in buitenste 'select'-query die voorwaarde op dat willekeurige veld.</span><span class="sxs-lookup"><span data-stu-id="725ea-121">This can be implemented by adding an extra field rand() toohello data set in hello inner "select" query, and in hello outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="725ea-122">Hier volgt een voorbeeldquery:</span><span class="sxs-lookup"><span data-stu-id="725ea-122">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

<span data-ttu-id="725ea-123">Hier `<sample rate, 0-1>` Hallo deel van de records die gebruikers Hallo toosample wilt bevat.</span><span class="sxs-lookup"><span data-stu-id="725ea-123">Here, `<sample rate, 0-1>` specifies hello proportion of records that hello users want toosample.</span></span>

## <span data-ttu-id="725ea-124"><a name="group"></a>Steekproeven door groepen</span><span class="sxs-lookup"><span data-stu-id="725ea-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="725ea-125">Wanneer steekproeven categorische gegevens, kunt u wordt tooeither opnemen of uitsluiten van alle exemplaren van een bepaalde waarde van een variabele categorische Hallo.</span><span class="sxs-lookup"><span data-stu-id="725ea-125">When sampling categorical data, you may want tooeither include or exclude all of hello instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="725ea-126">Dit is wat door 'steekproeven per groep'.</span><span class="sxs-lookup"><span data-stu-id="725ea-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="725ea-127">Bijvoorbeeld als er een categorische variabele 'Status', die waarden NY, MA, CA, NJ, PA, enzovoort, u wilt dat records Hallo dezelfde status worden altijd samen, of ze of niet worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="725ea-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of hello same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="725ea-128">Hier volgt een voorbeeldquery die voorbeelden per groep:</span><span class="sxs-lookup"><span data-stu-id="725ea-128">Here is an example query that samples by group:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <span data-ttu-id="725ea-129"><a name="stratified"></a>Toepassing stratificatie steekproeven</span><span class="sxs-lookup"><span data-stu-id="725ea-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="725ea-130">Steekproeven van toepassing is stratificatie met opzicht tooa categorische variabele wanneer Hallo voorbeelden verkregen waarden van dat categorische hebben die zich in Hallo dezelfde verhouding zoals in Hallo bovenliggende populatie van welke Hallo voorbeelden zijn verkregen.</span><span class="sxs-lookup"><span data-stu-id="725ea-130">Random sampling is stratified with respect tooa categorical variable when hello samples obtained have values of that categorical that are in hello same ratio as in hello parent population from which hello samples were obtained.</span></span> <span data-ttu-id="725ea-131">Met behulp van Hallo hetzelfde voorbeeld zoals hierboven, Stel dat uw gegevens altijd onderliggende populaties door statussen, spreek NJ 100 waarnemingen heeft, NY is 60 opmerkingen en WA is 300 opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="725ea-131">Using hello same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="725ea-132">Als u Hallo frequentie van opgeeft toepassing stratificatie steekproeven toobe 0,5 vervolgens hello voorbeeld verkregen moet hebben ongeveer 50, 30 en 150 opmerkingen van NJ NY en WA respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="725ea-132">If you specify hello rate of stratified sampling toobe 0.5, then hello sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="725ea-133">Hier volgt een voorbeeldquery:</span><span class="sxs-lookup"><span data-stu-id="725ea-133">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


<span data-ttu-id="725ea-134">Zie voor meer informatie over meer geavanceerde steekproeven methoden die beschikbaar in de component zijn [LanguageManual steekproeven](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="725ea-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

