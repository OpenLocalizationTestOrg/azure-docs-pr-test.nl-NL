---
title: functies voor gegevens in een Hadoop-cluster met behulp van Hive-query's aaaCreate | Microsoft Docs
description: Voorbeelden van Hive-query's die functies in de gegevens die zijn opgeslagen in een Azure HDInsight Hadoop-cluster genereren.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a><span data-ttu-id="6e171-103">Met Hive-query’s functies maken voor gegevens in een Hadoop-cluster</span><span class="sxs-lookup"><span data-stu-id="6e171-103">Create features for data in an Hadoop cluster using Hive queries</span></span>
<span data-ttu-id="6e171-104">Dit document ziet u hoe de functies toocreate voor gegevens wordt opgeslagen in een Azure HDInsight Hadoop-cluster met behulp van Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="6e171-104">This document shows how toocreate features for data stored in an Azure HDInsight Hadoop cluster using Hive queries.</span></span> <span data-ttu-id="6e171-105">Deze Hive-query gebruikt ingesloten Hive gebruiker gedefinieerde functies (UDF's), Hallo scripts die worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="6e171-105">These Hive queries use embedded Hive User Defined Functions (UDFs), hello scripts for which are provided.</span></span>

<span data-ttu-id="6e171-106">Hallo bewerkingen die nodig zijn toocreate functies kunnen geheugenintensief zijn.</span><span class="sxs-lookup"><span data-stu-id="6e171-106">hello operations needed toocreate features can be memory intensive.</span></span> <span data-ttu-id="6e171-107">Hallo-prestaties van Hive-query's wordt meer kritieke in dergelijke gevallen en kan worden verbeterd door het afstemmen van bepaalde parameters.</span><span class="sxs-lookup"><span data-stu-id="6e171-107">hello performance of Hive queries becomes more critical in such cases and can be improved by tuning certain parameters.</span></span> <span data-ttu-id="6e171-108">Hallo afstemming van deze parameters wordt besproken in het laatste gedeelte Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e171-108">hello tuning of these parameters is discussed in hello final section.</span></span>

<span data-ttu-id="6e171-109">Voorbeelden van Hallo-query's die worden aangeboden zijn specifieke toohello [NYC Taxi reis gegevens](http://chriswhong.com/open-data/foil_nyc_taxi/) scenario's zijn ook beschikbaar [GitHub-opslagplaats](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="6e171-109">Examples of hello queries that are presented are specific toohello [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="6e171-110">Deze query's al gegevensschema dat is opgegeven en zijn gereed toobe verzonden toorun.</span><span class="sxs-lookup"><span data-stu-id="6e171-110">These queries already have data schema specified and are ready toobe submitted toorun.</span></span> <span data-ttu-id="6e171-111">In het laatste gedeelte hello, worden ook parameters die gebruikers afstemmen kunnen zodat Hallo prestaties van Hive-query's kunnen worden verbeterd besproken.</span><span class="sxs-lookup"><span data-stu-id="6e171-111">In hello final section, parameters that users can tune so that hello performance of Hive queries can be improved are  also discussed.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="6e171-112">Dit **menu** koppelingen tootopics waarin wordt beschreven hoe toocreate functies voor gegevens in verschillende omgevingen.</span><span class="sxs-lookup"><span data-stu-id="6e171-112">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="6e171-113">Deze taak is een stap in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="6e171-113">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e171-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6e171-114">Prerequisites</span></span>
<span data-ttu-id="6e171-115">In dit artikel wordt ervan uitgegaan dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="6e171-115">This article assumes that you have:</span></span>

* <span data-ttu-id="6e171-116">Een Azure storage-account gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e171-116">Created an Azure storage account.</span></span> <span data-ttu-id="6e171-117">Als u instructies nodig hebt, raadpleegt u [een Azure Storage-account maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="6e171-117">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="6e171-118">Een aangepaste Hadoop-cluster met Hallo HDInsight-service wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="6e171-118">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="6e171-119">Als u instructies nodig hebt, raadpleegt u [aanpassen Azure HDInsight Hadoop-Clusters voor geavanceerde analyses](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6e171-119">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="6e171-120">Hallo-gegevens zijn geüpload tooHive tabellen in Azure HDInsight Hadoop-clusters.</span><span class="sxs-lookup"><span data-stu-id="6e171-120">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="6e171-121">Als dit niet het geval is, voert u [maken en de belasting tooHive gegevenstabellen](machine-learning-data-science-move-hive-tables.md) tooupload gegevens tooHive eerst tabellen.</span><span class="sxs-lookup"><span data-stu-id="6e171-121">If it has not, please follow [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="6e171-122">Externe toegang toohello cluster ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6e171-122">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="6e171-123">Als u instructies nodig hebt, raadpleegt u [toegang Hallo Head knooppunt van Hadoop-Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="6e171-123">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <span data-ttu-id="6e171-124"><a name="hive-featureengineering"></a>Functie generatie</span><span class="sxs-lookup"><span data-stu-id="6e171-124"><a name="hive-featureengineering"></a>Feature Generation</span></span>
<span data-ttu-id="6e171-125">In deze sectie vindt u enkele voorbeelden van Hallo manieren waarin functies kunnen genereren met behulp van Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="6e171-125">In this section, several examples of hello ways in which features can be generating using Hive queries are described.</span></span> <span data-ttu-id="6e171-126">Nadat u extra functies hebt gegenereerd, kunt u hen toevoegen als kolommen toohello bestaande tabel of een nieuwe tabel maken met de Hallo extra functies en primaire sleutel, die vervolgens kan worden samengevoegd met de oorspronkelijke tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e171-126">Once you have generated additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, which can then be joined with hello original table.</span></span> <span data-ttu-id="6e171-127">Hier volgen voorbeelden Hallo:</span><span class="sxs-lookup"><span data-stu-id="6e171-127">Here are hello examples presented:</span></span>

1. [<span data-ttu-id="6e171-128">De frequentie op basis van functie generatie</span><span class="sxs-lookup"><span data-stu-id="6e171-128">Frequency based Feature Generation</span></span>](#hive-frequencyfeature)
2. [<span data-ttu-id="6e171-129">Risico's van Categorische variabelen in binaire classificatie</span><span class="sxs-lookup"><span data-stu-id="6e171-129">Risks of Categorical Variables in Binary Classification</span></span>](#hive-riskfeature)
3. [<span data-ttu-id="6e171-130">Functies van Datetime Field uitpakken</span><span class="sxs-lookup"><span data-stu-id="6e171-130">Extract features from Datetime Field</span></span>](#hive-datefeatures)
4. [<span data-ttu-id="6e171-131">Functies van tekstveld uitpakken</span><span class="sxs-lookup"><span data-stu-id="6e171-131">Extract features from Text Field</span></span>](#hive-textfeatures)
5. [<span data-ttu-id="6e171-132">Afstand tussen GPS-coördinaten berekenen</span><span class="sxs-lookup"><span data-stu-id="6e171-132">Calculate distance between GPS coordinates</span></span>](#hive-gpsdistance)

### <span data-ttu-id="6e171-133"><a name="hive-frequencyfeature"></a>De frequentie op basis van functie generatie</span><span class="sxs-lookup"><span data-stu-id="6e171-133"><a name="hive-frequencyfeature"></a>Frequency based Feature Generation</span></span>
<span data-ttu-id="6e171-134">Is het vaak nuttig toocalculate Hallo frequenties van Hallo niveaus van een categorische variabele of Hallo frequenties van bepaalde combinaties van niveaus uit meerdere categorische variabelen.</span><span class="sxs-lookup"><span data-stu-id="6e171-134">It is often useful toocalculate hello frequencies of hello levels of a categorical variable, or hello frequencies of certain combinations of levels from multiple categorical variables.</span></span> <span data-ttu-id="6e171-135">Gebruikers kunnen Hallo script toocalculate na deze frequenties gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6e171-135">Users can use hello following script toocalculate these frequencies:</span></span>

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <span data-ttu-id="6e171-136"><a name="hive-riskfeature"></a>Risico's van Categorische variabelen in binaire classificatie</span><span class="sxs-lookup"><span data-stu-id="6e171-136"><a name="hive-riskfeature"></a>Risks of Categorical Variables in Binary Classification</span></span>
<span data-ttu-id="6e171-137">In binaire indeling moeten we tooconvert niet-numerieke categorische variabelen in de numerieke onderdelen waarbinnen Hallo modellen wordt alleen gebruikt numerieke functies worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6e171-137">In binary classification, we need tooconvert non-numeric categorical variables into numeric features when hello models being used only take numeric features.</span></span> <span data-ttu-id="6e171-138">Dit wordt gedaan door elk niet-numerieke niveau vervangen door een numerieke risico.</span><span class="sxs-lookup"><span data-stu-id="6e171-138">This is done by replacing each non-numeric level with a numeric risk.</span></span> <span data-ttu-id="6e171-139">In deze sectie laten we zien sommige algemene Hive-query's die Hallo risico waarden (logboek kans) van een variabele categorische berekenen.</span><span class="sxs-lookup"><span data-stu-id="6e171-139">In this section, we show some generic Hive queries that calculate hello risk values (log odds) of a categorical variable.</span></span>

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

<span data-ttu-id="6e171-140">In dit voorbeeld variabelen `smooth_param1` en `smooth_param2` zijn toosmooth Hallo risico waarden berekend op basis van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="6e171-140">In this example, variables `smooth_param1` and `smooth_param2` are set toosmooth hello risk values calculated from hello data.</span></span> <span data-ttu-id="6e171-141">Risico's hebben een bereik tussen -Inf en inf-bestand.</span><span class="sxs-lookup"><span data-stu-id="6e171-141">Risks have a range between -Inf and Inf.</span></span> <span data-ttu-id="6e171-142">Een risico's > 0 geeft aan dat Hallo waarschijnlijkheid dat doel Hallo gelijk too1 groter dan 0,5 is.</span><span class="sxs-lookup"><span data-stu-id="6e171-142">A risks > 0 indicates that hello probability that hello target is equal too1 is greater than 0.5.</span></span>

<span data-ttu-id="6e171-143">Nadat het Hallo risico tabel wordt berekend, kunnen gebruikers risico waarden tooa tabel lid maakt van met de Hallo risico tabel toewijzen.</span><span class="sxs-lookup"><span data-stu-id="6e171-143">After hello risk table is calculated, users can assign risk values tooa table by joining it with hello risk table.</span></span> <span data-ttu-id="6e171-144">gekoppelde Hallo Hive-query is opgegeven in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="6e171-144">hello Hive joining query was provided in previous section.</span></span>

### <span data-ttu-id="6e171-145"><a name="hive-datefeatures"></a>Functies van Datetime-Fields uitpakken</span><span class="sxs-lookup"><span data-stu-id="6e171-145"><a name="hive-datefeatures"></a>Extract features from Datetime Fields</span></span>
<span data-ttu-id="6e171-146">Hive wordt geleverd met een reeks UDF's voor het verwerken van datetime-velden.</span><span class="sxs-lookup"><span data-stu-id="6e171-146">Hive comes with a set of UDFs for processing datetime fields.</span></span> <span data-ttu-id="6e171-147">In Hive, is het Hallo-standaardnotatie voor datum/tijd is jjjj-MM-dd 00:00:00 ' ('01-01-1970 12:21:32 ' bijvoorbeeld).</span><span class="sxs-lookup"><span data-stu-id="6e171-147">In Hive, hello default datetime format is 'yyyy-MM-dd 00:00:00' ('1970-01-01 12:21:32' for example).</span></span> <span data-ttu-id="6e171-148">In deze sectie laten we zien voorbeelden die dag van een maand, de maand van een datetime-veld Hallo Hallo uitpakken en andere voorbeelden die een datum/tijd-tekenreeks in een indeling geconverteerd andere dan Hallo standaard tooa datetime indelingstekenreeks opmaken in standaard.</span><span class="sxs-lookup"><span data-stu-id="6e171-148">In this section, we show examples that extract hello day of a month, hello month from a datetime field, and other examples that convert a datetime string in a format other than hello default format tooa datetime string in default format.</span></span>

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

<span data-ttu-id="6e171-149">Deze Hive-query wordt ervan uitgegaan dat Hallo *&#60; datetime-veld >* Hallo standaard datum/tijd-indeling.</span><span class="sxs-lookup"><span data-stu-id="6e171-149">This Hive query assumes that hello *&#60;datetime field>* is in hello default datetime format.</span></span>

<span data-ttu-id="6e171-150">Als een datetime-veld niet in de standaardindeling hello is, u tooconvert Hallo datetime-veld in Unix tijdstempel eerst moet en vervolgens converteren Hallo Unix tijd stempel tooa datetime tekenreeks die is standaard Hallo indeling.</span><span class="sxs-lookup"><span data-stu-id="6e171-150">If a datetime field is not in hello default format, you need tooconvert hello datetime field into Unix time stamp first, and then convert hello Unix time stamp tooa datetime string that is in hello default format.</span></span> <span data-ttu-id="6e171-151">Wanneer Hallo datetime in standaard indeling is, kunnen gebruikers Hallo ingesloten datetime UDF's tooextract functies toepassen.</span><span class="sxs-lookup"><span data-stu-id="6e171-151">When hello datetime is in default format, users can apply hello embedded datetime UDFs tooextract features.</span></span>

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

<span data-ttu-id="6e171-152">In deze query als hello *&#60; datetime-veld >* heeft Hallo patroon zoals *03/26/2015 12:04:39*, Hallo *' &#60; patroon van Hallo datetime-veld >'* moet `'MM/dd/yyyy HH:mm:ss'`.</span><span class="sxs-lookup"><span data-stu-id="6e171-152">In this query, if hello *&#60;datetime field>* has hello pattern like *03/26/2015 12:04:39*, hello *'&#60;pattern of hello datetime field>'* should be `'MM/dd/yyyy HH:mm:ss'`.</span></span> <span data-ttu-id="6e171-153">tootest, gebruikers kunnen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6e171-153">tootest it, users can run</span></span>

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

<span data-ttu-id="6e171-154">Hallo *hivesampletable* in deze query vooraf is geïnstalleerd op alle Azure HDInsight Hadoop-clusters standaard wanneer Hallo clusters zijn ingericht.</span><span class="sxs-lookup"><span data-stu-id="6e171-154">hello *hivesampletable* in this query comes preinstalled on all Azure HDInsight Hadoop clusters by default when hello clusters are provisioned.</span></span>

### <span data-ttu-id="6e171-155"><a name="hive-textfeatures"></a>Functies van tekstvelden uitpakken</span><span class="sxs-lookup"><span data-stu-id="6e171-155"><a name="hive-textfeatures"></a>Extract features from Text Fields</span></span>
<span data-ttu-id="6e171-156">Wanneer Hallo Hive-tabel een tekstveld die een tekenreeks met woorden die worden gescheiden door spaties bevat heeft, haalt hello volgende query Hallo-lengte van tekenreeks Hallo en Hallo aantal woorden in Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="6e171-156">When hello Hive table has a text field that contains a string of words that are delimited by spaces, hello following query extracts hello length of hello string, and hello number of words in hello string.</span></span>

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <span data-ttu-id="6e171-157"><a name="hive-gpsdistance"></a>Afstand tussen sets GPS-coördinaten berekenen</span><span class="sxs-lookup"><span data-stu-id="6e171-157"><a name="hive-gpsdistance"></a>Calculate distances between sets of GPS coordinates</span></span>
<span data-ttu-id="6e171-158">Hallo-query is opgegeven in deze sectie kan rechtstreeks toegepaste toohello NYC Taxi reis gegevens zijn.</span><span class="sxs-lookup"><span data-stu-id="6e171-158">hello query given in this section can be directly applied toohello NYC Taxi Trip Data.</span></span> <span data-ttu-id="6e171-159">Hallo-doel van deze query is tooshow hoe tooapply ingesloten wiskundige functies in Hive toogenerate onderdelen.</span><span class="sxs-lookup"><span data-stu-id="6e171-159">hello purpose of this query is tooshow how tooapply an embedded mathematical functions in Hive toogenerate features.</span></span>

<span data-ttu-id="6e171-160">Hallo velden die worden gebruikt in deze query zijn Hallo GPS-coördinaten van ophalen en dropoff locaties, met de naam *ophalen\_lengtegraad*, *ophalen\_breedtegraad*,  *dropoff\_lengtegraad*, en *dropoff\_breedtegraad*.</span><span class="sxs-lookup"><span data-stu-id="6e171-160">hello fields that are used in this query are hello GPS coordinates of pickup and dropoff locations, named *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude*, and *dropoff\_latitude*.</span></span> <span data-ttu-id="6e171-161">Hallo-query's die direct afstand tussen Hallo ophalen en dropoff coördinaten Hallo berekenen zijn:</span><span class="sxs-lookup"><span data-stu-id="6e171-161">hello queries that calculate hello direct distance between hello pickup and dropoff coordinates are:</span></span>

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

<span data-ttu-id="6e171-162">Hallo wiskundige vergelijkingen die Hallo afstand tussen twee GPS-coördinaten berekenen vindt u op Hallo <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">MovableType Scripts</a> geschreven door Peter Lapisu-site.</span><span class="sxs-lookup"><span data-stu-id="6e171-162">hello mathematical equations that calculate hello distance between two GPS coordinates can be found on hello <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> site, authored by Peter Lapisu.</span></span> <span data-ttu-id="6e171-163">Hallo in diens Javascript functie `toRad()` is zojuist *lat_or_lon*pi/180 *, die graden tooradians converteert.</span><span class="sxs-lookup"><span data-stu-id="6e171-163">In his Javascript, hello function `toRad()` is just *lat_or_lon*pi/180*, which converts degrees tooradians.</span></span> <span data-ttu-id="6e171-164">Hier *lat_or_lon* Hallo breedtegraad of lengtegraad is.</span><span class="sxs-lookup"><span data-stu-id="6e171-164">Here, *lat_or_lon* is hello latitude or longitude.</span></span> <span data-ttu-id="6e171-165">Aangezien Hive geen Hallo functie biedt `atan2`, maar biedt Hallo functie `atan`, Hallo `atan2` functie wordt geïmplementeerd door `atan` functie in Hallo hierboven Hive-query met Hallo definitie is opgegeven in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Wikipedia</a>.</span><span class="sxs-lookup"><span data-stu-id="6e171-165">Since Hive does not provide hello function `atan2`, but provides hello function `atan`, hello `atan2` function is implemented by `atan` function in hello above Hive query using hello definition provided in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-create-features-hive/atan2new.png)

<span data-ttu-id="6e171-167">Een volledige lijst met Hive ingesloten UDF's u in Hallo vinden kunnen **ingebouwde functies** sectie op Hallo <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span><span class="sxs-lookup"><span data-stu-id="6e171-167">A full list of Hive embedded UDFs can be found in hello **Built-in Functions** section on hello <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span></span>  

## <span data-ttu-id="6e171-168"><a name="tuning"></a>Onderwerpen over geavanceerde: stemmen Hive Parameters tooImprove Query snelheid</span><span class="sxs-lookup"><span data-stu-id="6e171-168"><a name="tuning"></a> Advanced topics: Tune Hive Parameters tooImprove Query Speed</span></span>
<span data-ttu-id="6e171-169">Hallo standaardparameter instellingen van Hive-cluster niet mogelijk geschikt voor Hallo Hive-query's en Hallo-gegevens die Hallo query's worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="6e171-169">hello default parameter settings of Hive cluster might not be suitable for hello Hive queries and hello data that hello queries are processing.</span></span> <span data-ttu-id="6e171-170">In deze sectie bespreken we een aantal parameters die gebruikers kunnen afstemmen Hallo prestaties van Hive-query's verbeteren.</span><span class="sxs-lookup"><span data-stu-id="6e171-170">In this section, we discuss some parameters that users can tune that improve hello performance of Hive queries.</span></span> <span data-ttu-id="6e171-171">Gebruikers moeten tooadd Hallo parameter afstemmen van query's voordat Hallo query's van het verwerken van gegevens.</span><span class="sxs-lookup"><span data-stu-id="6e171-171">Users need tooadd hello parameter tuning queries before hello queries of processing data.</span></span>

1. <span data-ttu-id="6e171-172">**Java-heap ruimte**: voor query's met betrekking tot lid te worden grote gegevenssets of verwerken van lange records **bijna vol heap** is een algemene fout Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e171-172">**Java heap space**: For queries involving joining large datasets, or processing long records, **running out of heap space** is one of hello common error.</span></span> <span data-ttu-id="6e171-173">Dit door het instellen van de parameters kan worden afgestemd *mapreduce.map.java.opts* en *mapreduce.task.io.sort.mb* toodesired waarden.</span><span class="sxs-lookup"><span data-stu-id="6e171-173">This can be tuned by setting parameters *mapreduce.map.java.opts* and *mapreduce.task.io.sort.mb* toodesired values.</span></span> <span data-ttu-id="6e171-174">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6e171-174">Here is an example:</span></span>
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    <span data-ttu-id="6e171-175">Deze parameter wordt 4GB geheugen tooJava heap ruimte en maakt ook sorteren efficiënter door meer geheugen toewijzen voor het.</span><span class="sxs-lookup"><span data-stu-id="6e171-175">This parameter allocates 4GB memory tooJava heap space and also makes sorting more efficient by allocating more memory for it.</span></span> <span data-ttu-id="6e171-176">Als er een taak mislukt fouten gerelateerde tooheap ruimte is een goed idee tooplay met deze toewijzingen.</span><span class="sxs-lookup"><span data-stu-id="6e171-176">It is a good idea tooplay with these allocations if there are any job failure errors related tooheap space.</span></span>

1. <span data-ttu-id="6e171-177">**DFS-blokgrootte** : deze parameter stelt Hallo kleinste gegevenseenheid die Hallo system bestandsopslag.</span><span class="sxs-lookup"><span data-stu-id="6e171-177">**DFS block size** : This parameter sets hello smallest unit of data that hello file system stores.</span></span> <span data-ttu-id="6e171-178">Bijvoorbeeld als Hallo DFS-blokgrootte 128MB is, wordt geen gegevens van de grootte van minder dan en omhoog in too128MB opgeslagen in één blok, terwijl de gegevens die groter is dan 128MB extra blokken wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6e171-178">As an example, if hello DFS block size is 128MB, then any data of size less than and up too128MB is stored in a single block, while data that is larger than 128MB is allotted extra blocks.</span></span> <span data-ttu-id="6e171-179">Het kiezen van een zeer kleine blokgrootte zorgt ervoor dat grote overhead in Hadoop omdat Hallo naam knooppunt tooprocess veel meer aanvragen toofind Hallo relevante blok met toohello bestand betrekking heeft.</span><span class="sxs-lookup"><span data-stu-id="6e171-179">Choosing a very small block size causes large overheads in Hadoop since hello name node has tooprocess many more requests toofind hello relevant block pertaining toohello file.</span></span> <span data-ttu-id="6e171-180">Een aanbevolen instelling als betreft gigabyte (of groter) gegevens:</span><span class="sxs-lookup"><span data-stu-id="6e171-180">A recommended setting when dealing with gigabytes (or larger) data is :</span></span>
   
        set dfs.block.size=128m;
2. <span data-ttu-id="6e171-181">**Join-bewerking in Hive optimaliseren** : terwijl joinbewerkingen in Hallo kaart/verminderen framework doorgaans plaatsvinden in Hallo verminderen soms fase, enorm veel toeneemt kunnen worden bereikt door het plannen van joins in Hallo kaart fase (ook wel 'mapjoins' genoemd).</span><span class="sxs-lookup"><span data-stu-id="6e171-181">**Optimizing join operation in Hive** : While join operations in hello map/reduce framework typically take place in hello reduce phase, sometimes, enormous gains can be achieved by scheduling joins in hello map phase (also called "mapjoins").</span></span> <span data-ttu-id="6e171-182">toodirect Hive toodo dit zo veel mogelijk we kunt instellen:</span><span class="sxs-lookup"><span data-stu-id="6e171-182">toodirect Hive toodo this whenever possible, we can set :</span></span>
   
        set hive.auto.convert.join=true;
3. <span data-ttu-id="6e171-183">**Aantal mappers tooHive Hallo geven** : terwijl Hadoop kunnen Hallo gebruiker tooset Hallo aantal verkleiningstoestellen, Hallo aantal mappers is doorgaans niet worden ingesteld door de gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e171-183">**Specifying hello number of mappers tooHive** : While Hadoop allows hello user tooset hello number of reducers, hello number of mappers is typically not be set by hello user.</span></span> <span data-ttu-id="6e171-184">Een truc waarmee bepaalde mate van controle op dit nummer is toochoose hello Hadoop variabelen *mapred.min.split.size* en *mapred.max.split.size* als Hallo grootte van elke kaart taak wordt bepaald door:</span><span class="sxs-lookup"><span data-stu-id="6e171-184">A trick that allows some degree of control on this number is toochoose hello Hadoop variables, *mapred.min.split.size* and *mapred.max.split.size* as hello size of each map task is determined by :</span></span>
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    <span data-ttu-id="6e171-185">Normaal gesproken Hallo standaardwaarde van *mapred.min.split.size* is ingesteld op 0 van *mapred.max.split.size* is **Long.MAX** , evenals *dfs.block.size* is 64MB.</span><span class="sxs-lookup"><span data-stu-id="6e171-185">Typically, hello default value of *mapred.min.split.size* is 0, that of *mapred.max.split.size* is **Long.MAX** and that of *dfs.block.size* is 64MB.</span></span> <span data-ttu-id="6e171-186">Zoals we zien, gegevensgrootte van het gegeven Hallo afstemming van deze parameters door 'instelling' ze kunt u ons tootune Hallo aantal mappers gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6e171-186">As we can see, given hello data size, tuning these parameters by "setting" them allows us tootune hello number of mappers used.</span></span>
4. <span data-ttu-id="6e171-187">Enkele andere meer **geavanceerde opties voor** voor het optimaliseren van Hive prestaties hieronder worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="6e171-187">A few other more **advanced options** for optimizing Hive performance are mentioned below.</span></span> <span data-ttu-id="6e171-188">Dit kunnen u tooset Hallo toegewezen geheugen toomap taken verminderen en nuttig kunnen zijn bij het afstemmen van de prestaties.</span><span class="sxs-lookup"><span data-stu-id="6e171-188">These allow you tooset hello memory allocated toomap and reduce tasks, and can be useful in tweaking performance.</span></span> <span data-ttu-id="6e171-189">Houd er rekening mee dat Hallo *mapreduce.reduce.memory.mb* mag niet groter dan de grootte van fysiek geheugen Hallo van elk knooppunt van de werknemer in Hallo Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="6e171-189">Please keep in mind that hello *mapreduce.reduce.memory.mb* cannot be greater than hello physical memory size of each worker node in hello Hadoop cluster.</span></span>
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

