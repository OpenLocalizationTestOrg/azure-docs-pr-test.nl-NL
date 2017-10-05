---
title: Gegevens tijdverschil problemen oplossen met behulp van Azure Data Lake Tools voor Visual Studio | Microsoft Docs
description: Het oplossen van problemen die gegevens tijdverschil mogelijke oplossingen met behulp van Azure Data Lake Tools voor Visual Studio.
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 9b284ef33be4b935569fc368d81ddf040b2c2b7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d31f0-103">Gegevens tijdverschil problemen oplossen met behulp van Azure Data Lake Tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d31f0-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="d31f0-104">Wat is er gegevens leiden tot onjuiste?</span><span class="sxs-lookup"><span data-stu-id="d31f0-104">What is data skew?</span></span>

<span data-ttu-id="d31f0-105">Kort gezegd, is gegevens tijdverschil een overmatig vertegenwoordigde waarde.</span><span class="sxs-lookup"><span data-stu-id="d31f0-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="d31f0-106">Stel dat u 50 btw-onderzoekers btw berekent, één examinator voor elke status VS controleren hebt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d31f0-106">Imagine that you have assigned 50 tax examiners to audit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="d31f0-107">Wyoming name op toezien, heeft omdat er in de populatie klein is, weinig van doen.</span><span class="sxs-lookup"><span data-stu-id="d31f0-107">The Wyoming examiner, because the population there is small, has little to do.</span></span> <span data-ttu-id="d31f0-108">In Californië, echter wordt name op toezien opgeslagen erg druk is vanwege de grote bevolking van de status.</span><span class="sxs-lookup"><span data-stu-id="d31f0-108">In California, however, the examiner is kept very busy because of the state's large population.</span></span>
    <span data-ttu-id="d31f0-109">![Voorbeeld van gegevens tijdverschil probleem](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="d31f0-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="d31f0-110">In ons scenario, is de gegevens ongelijkmatig verdeeld over alle btw-onderzoekers, wat betekent dat sommige onderzoekers meer dan andere moeten werken.</span><span class="sxs-lookup"><span data-stu-id="d31f0-110">In our scenario, the data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="d31f0-111">In uw eigen baan, moet u vaak situaties zoals in het voorbeeld BTW-examinator hier ervaren.</span><span class="sxs-lookup"><span data-stu-id="d31f0-111">In your own job, you frequently experience situations like the tax-examiner example here.</span></span> <span data-ttu-id="d31f0-112">In meer technische voorwaarden één hoekpunt ontvangt veel meer gegevens dan de peers, een situatie waarin het hoekpunt werken meer dan de andere en die uiteindelijk vertraagt een volledige-taak.</span><span class="sxs-lookup"><span data-stu-id="d31f0-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes the vertex work more than the others and that eventually slows down an entire job.</span></span> <span data-ttu-id="d31f0-113">Wat is er slechter, kan de taak mislukken, omdat de hoekpunten, bijvoorbeeld een beperking 5 uur runtime en een beperking 6 GB geheugen.</span><span class="sxs-lookup"><span data-stu-id="d31f0-113">What's worse, the job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="d31f0-114">Het oplossen van problemen met gegevens tijdverschil</span><span class="sxs-lookup"><span data-stu-id="d31f0-114">Resolving data-skew problems</span></span>

<span data-ttu-id="d31f0-115">Met behulp van Azure Data Lake Tools voor Visual Studio kunt u vaststellen of de taak een probleem gegevens tijdverschil heeft.</span><span class="sxs-lookup"><span data-stu-id="d31f0-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="d31f0-116">Als er een probleem is, kunt u deze kunt oplossen door de oplossingen in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="d31f0-116">If a problem exists, you can resolve it by trying the solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="d31f0-117">Oplossing 1: Verbeteren Tabelpartities</span><span class="sxs-lookup"><span data-stu-id="d31f0-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-the-skewed-key-value-in-advance"></a><span data-ttu-id="d31f0-118">Optie 1: De waarde van de asymmetrische sleutel van tevoren filteren</span><span class="sxs-lookup"><span data-stu-id="d31f0-118">Option 1: Filter the skewed key value in advance</span></span>

<span data-ttu-id="d31f0-119">Als het heeft geen invloed op uw bedrijfslogica, kunt u de waarden van de hogere frequentie van tevoren filteren.</span><span class="sxs-lookup"><span data-stu-id="d31f0-119">If it does not affect your business logic, you can filter the higher-frequency values in advance.</span></span> <span data-ttu-id="d31f0-120">Bijvoorbeeld, als er een groot aantal 000 000 000 in kolom GUID, raadzaam niet om samen te voegen die waarde.</span><span class="sxs-lookup"><span data-stu-id="d31f0-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want to aggregate that value.</span></span> <span data-ttu-id="d31f0-121">Voordat u cumulatieve, kunt u ' WHERE GUID! '000 000 000' = ' voor het filteren van de hoge frequentie-waarde.</span><span class="sxs-lookup"><span data-stu-id="d31f0-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” to filter the high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="d31f0-122">Optie 2: Kies een andere partitie of distributie-sleutel</span><span class="sxs-lookup"><span data-stu-id="d31f0-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="d31f0-123">In het voorgaande voorbeeld, als u wilt dat alleen voor het controleren van de werkbelasting btw-controle over het land, kunt u verbeteren de gegevensdistributie door het id-nummer als uw sleutel.</span><span class="sxs-lookup"><span data-stu-id="d31f0-123">In the preceding example, if you want only to check the tax-audit workload all over the country, you can improve the data distribution by selecting the ID number as your key.</span></span> <span data-ttu-id="d31f0-124">Verzamelen van een andere partitie of distributiesleutel soms beter kunt verdelen de gegevens, maar u moet ervoor zorgen dat deze keuze niet van invloed op uw bedrijfslogica.</span><span class="sxs-lookup"><span data-stu-id="d31f0-124">Picking a different partition or distribution key can sometimes distribute the data more evenly, but you need to make sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="d31f0-125">Voor de instantie voor het berekenen van de som van de belasting voor elke status kunt u aanwijzen _status_ als de partitiesleutel.</span><span class="sxs-lookup"><span data-stu-id="d31f0-125">For instance, to calculate the tax sum for each state, you might want to designate _State_ as the partition key.</span></span> <span data-ttu-id="d31f0-126">Als u dit probleem zich voordoet, probeert u optie 3 blijven.</span><span class="sxs-lookup"><span data-stu-id="d31f0-126">If you continue to experience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="d31f0-127">Optie 3: Meer partitie of distributie sleutels toevoegen</span><span class="sxs-lookup"><span data-stu-id="d31f0-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="d31f0-128">In plaats van alleen _status_ als een partitiesleutel, kunt u meer dan één sleutel gebruiken voor het partitioneren.</span><span class="sxs-lookup"><span data-stu-id="d31f0-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="d31f0-129">Overweeg bijvoorbeeld _postcode_ als een extra partitiesleutel verminderen van de grootte van gegevens partities en de gegevens beter verdelen.</span><span class="sxs-lookup"><span data-stu-id="d31f0-129">For example, consider adding _ZIP Code_ as an additional partition key to reduce data-partition sizes and distribute the data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="d31f0-130">Optie 4: Round-robin distributie gebruiken</span><span class="sxs-lookup"><span data-stu-id="d31f0-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="d31f0-131">Als u niet een geschikte sleutel voor partitie en distributie vinden, kunt u proberen om te gebruiken van round-robin distributie.</span><span class="sxs-lookup"><span data-stu-id="d31f0-131">If you cannot find an appropriate key for partition and distribution, you can try to use round-robin distribution.</span></span> <span data-ttu-id="d31f0-132">Round-robin distributie worden alle rijen gelijk behandeld en worden ze willekeurig in bijbehorende buckets geplaatst.</span><span class="sxs-lookup"><span data-stu-id="d31f0-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="d31f0-133">De gegevens opgehaald gelijkmatig worden verdeeld, maar een nadeel van het ook zo de prestaties van de taak voor bepaalde bewerkingen plaats informatie verliest.</span><span class="sxs-lookup"><span data-stu-id="d31f0-133">The data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="d31f0-134">Bovendien, als u aggregatie voor de asymmetrische sleutel toch doet, bewaard het probleem gegevens tijdverschil.</span><span class="sxs-lookup"><span data-stu-id="d31f0-134">Additionally, if you are doing aggregation for the skewed key anyway, the data-skew problem will persist.</span></span> <span data-ttu-id="d31f0-135">Voor meer informatie over round-robin distributie, Zie de sectie distributies van U-SQL-tabel in [CREATE TABLE (U-SQL): het maken van een tabel met Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span><span class="sxs-lookup"><span data-stu-id="d31f0-135">To learn more about round-robin distribution, see the U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-the-query-plan"></a><span data-ttu-id="d31f0-136">Oplossing 2: Het queryplan verbeteren</span><span class="sxs-lookup"><span data-stu-id="d31f0-136">Solution 2: Improve the query plan</span></span>

### <a name="option-1-use-the-create-statistics-statement"></a><span data-ttu-id="d31f0-137">Optie 1: De instructie CREATE STATISTICS gebruiken</span><span class="sxs-lookup"><span data-stu-id="d31f0-137">Option 1: Use the CREATE STATISTICS statement</span></span>

<span data-ttu-id="d31f0-138">U-SQL biedt de instructie CREATE STATISTICS voor tabellen.</span><span class="sxs-lookup"><span data-stu-id="d31f0-138">U-SQL provides the CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="d31f0-139">Deze instructie biedt meer informatie naar de queryoptimalisatie over de gegevens kenmerken, zoals distributie waarde, die zijn opgeslagen in een tabel.</span><span class="sxs-lookup"><span data-stu-id="d31f0-139">This statement gives more information to the query optimizer about the data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="d31f0-140">Voor de meeste query's genereert de queryoptimalisatie al de benodigde statistieken voor een hoge kwaliteit queryplan.</span><span class="sxs-lookup"><span data-stu-id="d31f0-140">For most queries, the query optimizer already generates the necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="d31f0-141">Soms moet u mogelijk queryprestaties verbeteren door het maken van aanvullende statistieken met CREATE STATISTICS of door het ontwerp van de query wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d31f0-141">Occasionally, you might need to improve query performance by creating additional statistics with CREATE STATISTICS or by modifying the query design.</span></span> <span data-ttu-id="d31f0-142">Zie voor meer informatie de [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="d31f0-142">For more information, see the [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="d31f0-143">Codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d31f0-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="d31f0-144">Statistische gegevens wordt niet automatisch bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="d31f0-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="d31f0-145">Als u de gegevens in een tabel bijwerken zonder de statistieken worden opnieuw gemaakt, kan de queryprestaties weigeren.</span><span class="sxs-lookup"><span data-stu-id="d31f0-145">If you update the data in a table without re-creating the statistics, the query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="d31f0-146">Optie 2: SKEWFACTOR gebruiken</span><span class="sxs-lookup"><span data-stu-id="d31f0-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="d31f0-147">Als u optellen van de belasting voor elke status wilt, moet u GROEPEREN op status, een benadering die niet voorkomen het probleem gegevens tijdverschil dat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d31f0-147">If you want to sum the tax for each state, you must use GROUP BY state, an approach that doesn't avoid the data-skew problem.</span></span> <span data-ttu-id="d31f0-148">U kunt echter een hint gegevens opgeven in uw query voor het identificeren van gegevens tijdverschil-sleutels, zodat de optimalisatie van een uitvoeringsplan voor u voorbereiden kunt.</span><span class="sxs-lookup"><span data-stu-id="d31f0-148">However, you can provide a data hint in your query to identify data skew in keys so that the optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="d31f0-149">Meestal kunt u de parameter instellen als 0,5 en 1, met 0,5, wat betekent dat niet veel zware tijdverschil scheeftrekken en 1 betekenis.</span><span class="sxs-lookup"><span data-stu-id="d31f0-149">Usually, you can set the parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="d31f0-150">Omdat de hint gevolgen heeft voor uitvoering plan optimalisatie voor de huidige instructie en alle downstream-instructies, zorg er dan voor dat de hint toevoegen voordat u de mogelijkheid vervormd key-wise aggregatie.</span><span class="sxs-lookup"><span data-stu-id="d31f0-150">Because the hint affects execution-plan optimization for the current statement and all downstream statements, be sure to add the hint before the potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that the given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="d31f0-151">Codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d31f0-151">Code example:</span></span>

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a><span data-ttu-id="d31f0-152">Optie 3: ROWCOUNT gebruiken</span><span class="sxs-lookup"><span data-stu-id="d31f0-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="d31f0-153">Naast SKEWFACTOR, kunt specifieke vervormd sleutel join gevallen, als u weet dat de andere gekoppelde rijenset klein is, u zien het optimalisatieprogramma door toe te voegen een ROWCOUNT-hint in de U-SQL-instructie voor samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="d31f0-153">In addition to SKEWFACTOR, for specific skewed-key join cases, if you know that the other joined row set is small, you can tell the optimizer by adding a ROWCOUNT hint in the U-SQL statement before JOIN.</span></span> <span data-ttu-id="d31f0-154">Op deze manier kunt optimaliseren een broadcast-join-strategie om prestaties te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="d31f0-154">This way, optimizer can choose a broadcast join strategy to help improve performance.</span></span> <span data-ttu-id="d31f0-155">Let erop dat ROWCOUNT niet de gegevens tijdverschil probleem is opgelost, maar aanvullende hulp kunnen worden aangeboden.</span><span class="sxs-lookup"><span data-stu-id="d31f0-155">Be aware that ROWCOUNT does not resolve the data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="d31f0-156">Codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d31f0-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information to determine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-the-user-defined-reducer-and-combiner"></a><span data-ttu-id="d31f0-157">Oplossing 3: De gebruiker gedefinieerde reducer en combiner verbeteren</span><span class="sxs-lookup"><span data-stu-id="d31f0-157">Solution 3: Improve the user-defined reducer and combiner</span></span>

<span data-ttu-id="d31f0-158">U kunt een door de gebruiker gedefinieerde operator om te gaan met een complex proces logica soms schrijven en een goed geschreven reducer en combiner mogelijk een probleem gegevens tijdverschil in sommige gevallen beperken.</span><span class="sxs-lookup"><span data-stu-id="d31f0-158">You can sometimes write a user-defined operator to deal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="d31f0-159">Optie 1: Een reducer recursieve indien mogelijk gebruiken</span><span class="sxs-lookup"><span data-stu-id="d31f0-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="d31f0-160">Een door de gebruiker gedefinieerde reducer wordt standaard uitgevoerd in de modus voor niet-recursieve, wat betekent dat de hoeveelheid werk voor een sleutel die wordt gedistribueerd in een enkel hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="d31f0-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="d31f0-161">Maar als u uw gegevens is vervormd, de grote gegevenssets mogelijk verwerkt in een één hoekpunt en lange tijd worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d31f0-161">But if your data is skewed, the huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="d31f0-162">Om prestaties te verbeteren, kunt u een kenmerk toevoegen in uw code voor het definiëren van reducer in recursieve modus uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d31f0-162">To improve performance, you can add an attribute in your code to define reducer to run in recursive mode.</span></span> <span data-ttu-id="d31f0-163">De grote gegevenssets kunnen vervolgens worden gedistribueerd naar meerdere hoekpunten en parallel, die uw taak sneller worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d31f0-163">Then, the huge data sets can be distributed to multiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="d31f0-164">Als u een niet-recursieve reducer recursieve, moet u ervoor zorgen dat uw algoritme associatieve.</span><span class="sxs-lookup"><span data-stu-id="d31f0-164">To change a non-recursive reducer to recursive, you need to make sure that your algorithm is associative.</span></span> <span data-ttu-id="d31f0-165">Bijvoorbeeld, de som associatieve is en de mediaan is niet.</span><span class="sxs-lookup"><span data-stu-id="d31f0-165">For example, the sum is associative, and the median is not.</span></span> <span data-ttu-id="d31f0-166">U moet ook om ervoor te zorgen dat de invoer en uitvoer voor reducer, hetzelfde schema behoudt.</span><span class="sxs-lookup"><span data-stu-id="d31f0-166">You also need to make sure that the input and output for reducer keep the same schema.</span></span>

<span data-ttu-id="d31f0-167">Kenmerk van recursieve reducer:</span><span class="sxs-lookup"><span data-stu-id="d31f0-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="d31f0-168">Codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d31f0-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="d31f0-169">Optie 2: Rijniveau combiner modus gebruiken, indien mogelijk</span><span class="sxs-lookup"><span data-stu-id="d31f0-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="d31f0-170">Net als bij de ROWCOUNT-hint voor specifieke vervormd sleutel join gevallen, combiner modus probeert te grote vervormd-sleutelwaarde sets op meerdere hoekpunten distribueren, zodat het werk gelijktijdig kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d31f0-170">Similar to the ROWCOUNT hint for specific skewed-key join cases, combiner mode tries to distribute huge skewed-key value sets to multiple vertices so that the work can be executed concurrently.</span></span> <span data-ttu-id="d31f0-171">Gegevens tijdverschil problemen kan niet worden omgezet in combiner modus, maar aanvullende hulp voor grote vervormd-sleutelwaarde sets kunnen worden aangeboden.</span><span class="sxs-lookup"><span data-stu-id="d31f0-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="d31f0-172">Standaard is de modus combiner volledig, wat betekent dat de rij links en rechts rij kunnen niet worden gescheiden.</span><span class="sxs-lookup"><span data-stu-id="d31f0-172">By default, the combiner mode is Full, which means that the left row set and right row set cannot be separated.</span></span> <span data-ttu-id="d31f0-173">De modus instellen als rechts-links/interne kunt rijniveau join.</span><span class="sxs-lookup"><span data-stu-id="d31f0-173">Setting the mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="d31f0-174">Het systeem scheidt de bijbehorende rij sets en ze worden verdeeld over meerdere hoekpunten die parallel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d31f0-174">The system separates the corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="d31f0-175">Voordat u de modus combiner configureren, let er om ervoor te zorgen dat de bijbehorende rij sets kunnen worden gescheiden.</span><span class="sxs-lookup"><span data-stu-id="d31f0-175">However, before you configure the combiner mode, be careful to ensure that the corresponding row sets can be separated.</span></span>

<span data-ttu-id="d31f0-176">Het volgende voorbeeld ziet u een rijenset gescheiden links.</span><span class="sxs-lookup"><span data-stu-id="d31f0-176">The example that follows shows a separated left row set.</span></span> <span data-ttu-id="d31f0-177">Elke rij van de uitvoer is afhankelijk van één rij invoer vanaf de linkerkant en mogelijk afhankelijk is van alle rijen uit de rechts met dezelfde sleutelwaarde.</span><span class="sxs-lookup"><span data-stu-id="d31f0-177">Each output row depends on a single input row from the left, and it potentially depends on all rows from the right with the same key value.</span></span> <span data-ttu-id="d31f0-178">Als u de modus combiner als links instelt, wordt het systeem scheidt de enorme links-rijenset in kleine netwerken en ze worden toegewezen aan meerdere hoekpunten.</span><span class="sxs-lookup"><span data-stu-id="d31f0-178">If you set the combiner mode as left, the system separates the huge left-row set into small ones and assigns them to multiple vertices.</span></span>

![Afbeelding van combiner-modus](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="d31f0-180">Als u de verkeerde combiner modus instelt, wordt de combinatie is minder efficiënt en de resultaten mogelijk onjuist.</span><span class="sxs-lookup"><span data-stu-id="d31f0-180">If you set the wrong combiner mode, the combination is less efficient, and the results might be wrong.</span></span>

<span data-ttu-id="d31f0-181">De kenmerken van combiner modus:</span><span class="sxs-lookup"><span data-stu-id="d31f0-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all the input rows from left and right with the same key value.

- <span data-ttu-id="d31f0-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Elke rij van de uitvoer hangt af van één rij invoer van links (en mogelijk alle rijen uit de rechts met dezelfde sleutelwaarde).</span><span class="sxs-lookup"><span data-stu-id="d31f0-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from the left (and potentially all rows from the right with the same key value).</span></span>

- <span data-ttu-id="d31f0-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): elke rij van de uitvoer is afhankelijk van één rij invoer van het recht (en mogelijk alle rijen uit de linkerkant met dezelfde sleutelwaarde).</span><span class="sxs-lookup"><span data-stu-id="d31f0-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from the right (and potentially all rows from the left with the same key value).</span></span>

- <span data-ttu-id="d31f0-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Elke rij van de uitvoer hangt af van één rij invoer vanaf de linkerkant en het recht met dezelfde waarde.</span><span class="sxs-lookup"><span data-stu-id="d31f0-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from the left and the right with the same value.</span></span>

<span data-ttu-id="d31f0-185">Codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d31f0-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
