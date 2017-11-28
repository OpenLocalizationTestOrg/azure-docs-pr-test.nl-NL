---
title: aaaResolve gegevens tijdverschil problemen met behulp van Azure Data Lake Tools voor Visual Studio | Microsoft Docs
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
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="3d760-103">Gegevens tijdverschil problemen oplossen met behulp van Azure Data Lake Tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3d760-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="3d760-104">Wat is er gegevens leiden tot onjuiste?</span><span class="sxs-lookup"><span data-stu-id="3d760-104">What is data skew?</span></span>

<span data-ttu-id="3d760-105">Kort gezegd, is gegevens tijdverschil een overmatig vertegenwoordigde waarde.</span><span class="sxs-lookup"><span data-stu-id="3d760-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="3d760-106">Stel dat u hebt toegewezen 50 btw-onderzoekers tooaudit btw berekent, één examinator voor elke status van de Verenigde Staten.</span><span class="sxs-lookup"><span data-stu-id="3d760-106">Imagine that you have assigned 50 tax examiners tooaudit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="3d760-107">Hallo Wyoming examinator, heeft omdat er Hallo populatie klein is, weinig toodo.</span><span class="sxs-lookup"><span data-stu-id="3d760-107">hello Wyoming examiner, because hello population there is small, has little toodo.</span></span> <span data-ttu-id="3d760-108">In Californië, echter wordt Hallo examinator opgeslagen erg druk is vanwege de grote bevolking Hallo-staat.</span><span class="sxs-lookup"><span data-stu-id="3d760-108">In California, however, hello examiner is kept very busy because of hello state's large population.</span></span>
    <span data-ttu-id="3d760-109">![Voorbeeld van gegevens tijdverschil probleem](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="3d760-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="3d760-110">In ons scenario is Hallo gegevens ongelijkmatig verdeeld over alle btw-onderzoekers, wat betekent dat sommige onderzoekers meer dan andere moeten werken.</span><span class="sxs-lookup"><span data-stu-id="3d760-110">In our scenario, hello data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="3d760-111">In uw eigen baan, moet u vaak situaties zoals Hallo btw examinator voorbeeld hier ervaren.</span><span class="sxs-lookup"><span data-stu-id="3d760-111">In your own job, you frequently experience situations like hello tax-examiner example here.</span></span> <span data-ttu-id="3d760-112">Één hoekpunt opgehaald in meer technische voorwaarden veel meer gegevens dan de peers, een situatie die Hallo hoekpunt werken meer dan Hallo anderen en die uiteindelijk vertraagt een hele taak maakt.</span><span class="sxs-lookup"><span data-stu-id="3d760-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes hello vertex work more than hello others and that eventually slows down an entire job.</span></span> <span data-ttu-id="3d760-113">Wat is er slechter, mislukken Hallo taak, omdat de hoekpunten, bijvoorbeeld een beperking 5 uur runtime en een beperking 6 GB geheugen.</span><span class="sxs-lookup"><span data-stu-id="3d760-113">What's worse, hello job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="3d760-114">Het oplossen van problemen met gegevens tijdverschil</span><span class="sxs-lookup"><span data-stu-id="3d760-114">Resolving data-skew problems</span></span>

<span data-ttu-id="3d760-115">Met behulp van Azure Data Lake Tools voor Visual Studio kunt u vaststellen of de taak een probleem gegevens tijdverschil heeft.</span><span class="sxs-lookup"><span data-stu-id="3d760-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="3d760-116">Als er een probleem is, kunt u deze kunt oplossen door de Hallo-oplossingen in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="3d760-116">If a problem exists, you can resolve it by trying hello solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="3d760-117">Oplossing 1: Verbeteren Tabelpartities</span><span class="sxs-lookup"><span data-stu-id="3d760-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a><span data-ttu-id="3d760-118">Optie 1: Filter Hallo vervormd sleutelwaarde van tevoren</span><span class="sxs-lookup"><span data-stu-id="3d760-118">Option 1: Filter hello skewed key value in advance</span></span>

<span data-ttu-id="3d760-119">Als het heeft geen invloed op uw bedrijfslogica, kunt u van tevoren Hallo hogere frequentie waarden filteren.</span><span class="sxs-lookup"><span data-stu-id="3d760-119">If it does not affect your business logic, you can filter hello higher-frequency values in advance.</span></span> <span data-ttu-id="3d760-120">Bijvoorbeeld, als er een groot aantal 000 000 000 in kolom GUID, raadzaam niet tooaggregate die waarde.</span><span class="sxs-lookup"><span data-stu-id="3d760-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want tooaggregate that value.</span></span> <span data-ttu-id="3d760-121">Voordat u cumulatieve, kunt u ' WHERE GUID! '000 000 000' = ' toofilter Hallo hoge frequentie waarde.</span><span class="sxs-lookup"><span data-stu-id="3d760-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” toofilter hello high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="3d760-122">Optie 2: Kies een andere partitie of distributie-sleutel</span><span class="sxs-lookup"><span data-stu-id="3d760-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="3d760-123">In het voorgaande voorbeeld Hallo als u wilt dat alleen toocheck Hallo btw-audit werkbelasting alle via land Hallo, u kunt Hallo gegevensdistributie verbeteren door het Hallo-id-nummer als uw sleutel te selecteren.</span><span class="sxs-lookup"><span data-stu-id="3d760-123">In hello preceding example, if you want only toocheck hello tax-audit workload all over hello country, you can improve hello data distribution by selecting hello ID number as your key.</span></span> <span data-ttu-id="3d760-124">Verzamelen van een andere partitie of distributiesleutel soms beter kunt verdelen Hallo gegevens, maar moet u ervoor dat deze keuze niet van invloed op uw bedrijfslogica toomake.</span><span class="sxs-lookup"><span data-stu-id="3d760-124">Picking a different partition or distribution key can sometimes distribute hello data more evenly, but you need toomake sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="3d760-125">Bijvoorbeeld: toocalculate Hallo btw som voor elke status kunt u toodesignate _status_ als partitiesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="3d760-125">For instance, toocalculate hello tax sum for each state, you might want toodesignate _State_ as hello partition key.</span></span> <span data-ttu-id="3d760-126">Als u tooexperience dit probleem doorgaat, probeert u optie 3.</span><span class="sxs-lookup"><span data-stu-id="3d760-126">If you continue tooexperience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="3d760-127">Optie 3: Meer partitie of distributie sleutels toevoegen</span><span class="sxs-lookup"><span data-stu-id="3d760-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="3d760-128">In plaats van alleen _status_ als een partitiesleutel, kunt u meer dan één sleutel gebruiken voor het partitioneren.</span><span class="sxs-lookup"><span data-stu-id="3d760-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="3d760-129">Overweeg bijvoorbeeld _postcode_ als een extra partitie sleutel tooreduce gegevens partitie groottes en Hallo gegevens beter verdelen.</span><span class="sxs-lookup"><span data-stu-id="3d760-129">For example, consider adding _ZIP Code_ as an additional partition key tooreduce data-partition sizes and distribute hello data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="3d760-130">Optie 4: Round-robin distributie gebruiken</span><span class="sxs-lookup"><span data-stu-id="3d760-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="3d760-131">Als u niet een geschikte sleutel voor partitie en distributie vinden, kunt u proberen toouse round-robin distributie.</span><span class="sxs-lookup"><span data-stu-id="3d760-131">If you cannot find an appropriate key for partition and distribution, you can try toouse round-robin distribution.</span></span> <span data-ttu-id="3d760-132">Round-robin distributie worden alle rijen gelijk behandeld en worden ze willekeurig in bijbehorende buckets geplaatst.</span><span class="sxs-lookup"><span data-stu-id="3d760-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="3d760-133">Hallo-gegevens opgehaald gelijkmatig worden verdeeld, maar een nadeel van het ook zo de prestaties van de taak voor bepaalde bewerkingen plaats informatie verliest.</span><span class="sxs-lookup"><span data-stu-id="3d760-133">hello data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="3d760-134">Bovendien, als u aggregatie voor Hallo asymmetrische sleutel toch doet, bewaard Hallo gegevens tijdverschil probleem.</span><span class="sxs-lookup"><span data-stu-id="3d760-134">Additionally, if you are doing aggregation for hello skewed key anyway, hello data-skew problem will persist.</span></span> <span data-ttu-id="3d760-135">toolearn meer informatie over round-robin distributie Zie Hallo U-SQL-tabel distributies sectie [CREATE TABLE (U-SQL): het maken van een tabel met Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span><span class="sxs-lookup"><span data-stu-id="3d760-135">toolearn more about round-robin distribution, see hello U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-hello-query-plan"></a><span data-ttu-id="3d760-136">Oplossing 2: Het queryplan Hallo verbeteren</span><span class="sxs-lookup"><span data-stu-id="3d760-136">Solution 2: Improve hello query plan</span></span>

### <a name="option-1-use-hello-create-statistics-statement"></a><span data-ttu-id="3d760-137">Optie 1: De instructie CREATE STATISTICS hello gebruiken</span><span class="sxs-lookup"><span data-stu-id="3d760-137">Option 1: Use hello CREATE STATISTICS statement</span></span>

<span data-ttu-id="3d760-138">U-SQL biedt de instructie CREATE STATISTICS hello in tabellen.</span><span class="sxs-lookup"><span data-stu-id="3d760-138">U-SQL provides hello CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="3d760-139">Deze instructie biedt meer informatie toohello queryoptimalisatie over Hallo gegevenskenmerken, zoals distributie waarde, die zijn opgeslagen in een tabel.</span><span class="sxs-lookup"><span data-stu-id="3d760-139">This statement gives more information toohello query optimizer about hello data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="3d760-140">Voor de meeste query's genereert Hallo queryoptimalisatie al Hallo nodig statistieken voor een hoge kwaliteit queryplan.</span><span class="sxs-lookup"><span data-stu-id="3d760-140">For most queries, hello query optimizer already generates hello necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="3d760-141">In sommige gevallen moet u mogelijk tooimprove queryprestaties met het maken van aanvullende statistieken met statistieken maken of te wijzigen Hallo queryontwerp.</span><span class="sxs-lookup"><span data-stu-id="3d760-141">Occasionally, you might need tooimprove query performance by creating additional statistics with CREATE STATISTICS or by modifying hello query design.</span></span> <span data-ttu-id="3d760-142">Zie voor meer informatie, Hallo [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="3d760-142">For more information, see hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="3d760-143">Codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3d760-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="3d760-144">Statistische gegevens wordt niet automatisch bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="3d760-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="3d760-145">Als u gegevens in een tabel Hallo zonder Hallo statistieken worden opnieuw gemaakt bijwerkt, zou kunnen Hallo queryprestaties afnemen.</span><span class="sxs-lookup"><span data-stu-id="3d760-145">If you update hello data in a table without re-creating hello statistics, hello query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="3d760-146">Optie 2: SKEWFACTOR gebruiken</span><span class="sxs-lookup"><span data-stu-id="3d760-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="3d760-147">Als u toosum Hallo belasting voor elke status wilt, moet u GROEPEREN op status, een benadering die niet Hallo gegevens tijdverschil probleem voorkomen.</span><span class="sxs-lookup"><span data-stu-id="3d760-147">If you want toosum hello tax for each state, you must use GROUP BY state, an approach that doesn't avoid hello data-skew problem.</span></span> <span data-ttu-id="3d760-148">U kunt echter een hint gegevens opgeven in uw query tooidentify gegevens leiden tot sleutels onjuiste zodat Hallo optimaliseren een uitvoeringsplan voor u voorbereiden kunt.</span><span class="sxs-lookup"><span data-stu-id="3d760-148">However, you can provide a data hint in your query tooidentify data skew in keys so that hello optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="3d760-149">Meestal kunt u Hallo parameter instellen als 0,5 en 1, met 0,5, wat betekent dat niet veel zware tijdverschil scheeftrekken en 1 betekenis.</span><span class="sxs-lookup"><span data-stu-id="3d760-149">Usually, you can set hello parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="3d760-150">Aangezien Hallo-hint is van invloed op uitvoeringsplan optimalisatie voor de huidige instructie Hallo en alle downstream-instructies, moet u ervoor tooadd Hallo hint voordat potentiële Hallo vervormd key-wise aggregatie.</span><span class="sxs-lookup"><span data-stu-id="3d760-150">Because hello hint affects execution-plan optimization for hello current statement and all downstream statements, be sure tooadd hello hint before hello potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="3d760-151">Codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3d760-151">Code example:</span></span>

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

### <a name="option-3-use-rowcount"></a><span data-ttu-id="3d760-152">Optie 3: ROWCOUNT gebruiken</span><span class="sxs-lookup"><span data-stu-id="3d760-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="3d760-153">Bovendien tooSKEWFACTOR voor specifieke vervormd-sleutel join gevallen, als u weet dat Hallo andere rijenset gekoppelde is klein, kunt u instellen dat Hallo optimaliseren door toe te voegen een ROWCOUNT-hint in Hallo U-SQL-instructie voor samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="3d760-153">In addition tooSKEWFACTOR, for specific skewed-key join cases, if you know that hello other joined row set is small, you can tell hello optimizer by adding a ROWCOUNT hint in hello U-SQL statement before JOIN.</span></span> <span data-ttu-id="3d760-154">Op deze manier optimaliseren kunt ervoor kiezen een toohelp broadcast join-strategie voor de prestaties verbeteren.</span><span class="sxs-lookup"><span data-stu-id="3d760-154">This way, optimizer can choose a broadcast join strategy toohelp improve performance.</span></span> <span data-ttu-id="3d760-155">Let erop dat ROWCOUNT Hallo gegevens tijdverschil probleem niet is opgelost, maar aanvullende hulp kunnen worden aangeboden.</span><span class="sxs-lookup"><span data-stu-id="3d760-155">Be aware that ROWCOUNT does not resolve hello data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="3d760-156">Codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3d760-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a><span data-ttu-id="3d760-157">Oplossing 3: Hallo gebruiker gedefinieerde reducer en combiner verbeteren</span><span class="sxs-lookup"><span data-stu-id="3d760-157">Solution 3: Improve hello user-defined reducer and combiner</span></span>

<span data-ttu-id="3d760-158">U kunt een gebruiker gedefinieerde operator toodeal met ingewikkeld proces logica soms schrijven en een goed geschreven reducer en combiner mogelijk een probleem gegevens tijdverschil in sommige gevallen beperken.</span><span class="sxs-lookup"><span data-stu-id="3d760-158">You can sometimes write a user-defined operator toodeal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="3d760-159">Optie 1: Een reducer recursieve indien mogelijk gebruiken</span><span class="sxs-lookup"><span data-stu-id="3d760-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="3d760-160">Een door de gebruiker gedefinieerde reducer wordt standaard uitgevoerd in de modus voor niet-recursieve, wat betekent dat de hoeveelheid werk voor een sleutel die wordt gedistribueerd in een enkel hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="3d760-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="3d760-161">Maar als uw gegevens is vervormd, Hallo grote gegevenssets mogelijk verwerkt in een enkel hoekpunt en lange tijd worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3d760-161">But if your data is skewed, hello huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="3d760-162">tooimprove prestaties, kunt u een kenmerk toevoegen in uw code toodefine reducer toorun in de recursieve modus.</span><span class="sxs-lookup"><span data-stu-id="3d760-162">tooimprove performance, you can add an attribute in your code toodefine reducer toorun in recursive mode.</span></span> <span data-ttu-id="3d760-163">Vervolgens Hallo grote gegevenssets worden gedistribueerde toomultiple hoekpunten en parallel, die uw taak sneller worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3d760-163">Then, hello huge data sets can be distributed toomultiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="3d760-164">een niet-recursieve reducer toorecursive toochange, moet u ervoor dat de algoritme associatieve toomake.</span><span class="sxs-lookup"><span data-stu-id="3d760-164">toochange a non-recursive reducer toorecursive, you need toomake sure that your algorithm is associative.</span></span> <span data-ttu-id="3d760-165">Bijvoorbeeld Hallo som is associatieve en Hallo mediaan is niet.</span><span class="sxs-lookup"><span data-stu-id="3d760-165">For example, hello sum is associative, and hello median is not.</span></span> <span data-ttu-id="3d760-166">Ook moet u ervoor dat Hallo invoer en uitvoer voor reducer Hallo behoudt toomake hetzelfde schema.</span><span class="sxs-lookup"><span data-stu-id="3d760-166">You also need toomake sure that hello input and output for reducer keep hello same schema.</span></span>

<span data-ttu-id="3d760-167">Kenmerk van recursieve reducer:</span><span class="sxs-lookup"><span data-stu-id="3d760-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="3d760-168">Codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3d760-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="3d760-169">Optie 2: Rijniveau combiner modus gebruiken, indien mogelijk</span><span class="sxs-lookup"><span data-stu-id="3d760-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="3d760-170">Vergelijkbare toohello ROWCOUNT hint op voor specifieke vervormd sleutel join gevallen, combiner modus probeert toodistribute grote vervormd-sleutelwaarde sets toomultiple hoekpunten zodat Hallo werk gelijktijdig kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3d760-170">Similar toohello ROWCOUNT hint for specific skewed-key join cases, combiner mode tries toodistribute huge skewed-key value sets toomultiple vertices so that hello work can be executed concurrently.</span></span> <span data-ttu-id="3d760-171">Gegevens tijdverschil problemen kan niet worden omgezet in combiner modus, maar aanvullende hulp voor grote vervormd-sleutelwaarde sets kunnen worden aangeboden.</span><span class="sxs-lookup"><span data-stu-id="3d760-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="3d760-172">Standaard is Hallo combiner modus volledig, wat betekent dat Hallo rij ingestelde links en rechts rijenset kan niet worden gescheiden.</span><span class="sxs-lookup"><span data-stu-id="3d760-172">By default, hello combiner mode is Full, which means that hello left row set and right row set cannot be separated.</span></span> <span data-ttu-id="3d760-173">Instelling Hallo-modus als rechts-links/interne kunnen rijniveau join.</span><span class="sxs-lookup"><span data-stu-id="3d760-173">Setting hello mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="3d760-174">Hallo systeem scheidt Hallo overeenkomende rij sets en ze worden verdeeld over meerdere hoekpunten die parallel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3d760-174">hello system separates hello corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="3d760-175">Voordat u Hallo combiner modus configureren, let er tooensure die overeenkomstige rij sets Hallo kan worden gescheiden.</span><span class="sxs-lookup"><span data-stu-id="3d760-175">However, before you configure hello combiner mode, be careful tooensure that hello corresponding row sets can be separated.</span></span>

<span data-ttu-id="3d760-176">volgende Hallo voorbeeld ziet u een rijenset gescheiden links.</span><span class="sxs-lookup"><span data-stu-id="3d760-176">hello example that follows shows a separated left row set.</span></span> <span data-ttu-id="3d760-177">Elke rij van de uitvoer, is afhankelijk van één rij invoer van Hallo links en mogelijk afhankelijk is van alle rijen uit Hallo Hallo met dezelfde sleutelwaarde.</span><span class="sxs-lookup"><span data-stu-id="3d760-177">Each output row depends on a single input row from hello left, and it potentially depends on all rows from hello right with hello same key value.</span></span> <span data-ttu-id="3d760-178">Als u links Hallo combiner modus instelt, wordt Hallo systeem scheidt Hallo grote linkerkant-rijenset in kleine netwerken en wijst deze toomultiple hoekpunten.</span><span class="sxs-lookup"><span data-stu-id="3d760-178">If you set hello combiner mode as left, hello system separates hello huge left-row set into small ones and assigns them toomultiple vertices.</span></span>

![Afbeelding van combiner-modus](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="3d760-180">Als u Hallo verkeerde combiner modus instelt, Hallo combinatie is minder efficiënt en Hallo resultaten mis zijn.</span><span class="sxs-lookup"><span data-stu-id="3d760-180">If you set hello wrong combiner mode, hello combination is less efficient, and hello results might be wrong.</span></span>

<span data-ttu-id="3d760-181">De kenmerken van combiner modus:</span><span class="sxs-lookup"><span data-stu-id="3d760-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- <span data-ttu-id="3d760-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Elke rij van de uitvoer is afhankelijk van één rij invoer van Hallo links (en mogelijk alle rijen uit Hallo Hallo met dezelfde sleutelwaarde).</span><span class="sxs-lookup"><span data-stu-id="3d760-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from hello left (and potentially all rows from hello right with hello same key value).</span></span>

- <span data-ttu-id="3d760-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): elke rij van de uitvoer is afhankelijk van één rij invoer van de juiste hello (en mogelijk alle rijen uit Hallo links Hello dezelfde sleutelwaarde).</span><span class="sxs-lookup"><span data-stu-id="3d760-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from hello right (and potentially all rows from hello left with hello same key value).</span></span>

- <span data-ttu-id="3d760-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Elke rij van de uitvoer is afhankelijk van één rij invoer van Hallo links en Hallo Hallo met dezelfde waarde.</span><span class="sxs-lookup"><span data-stu-id="3d760-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from hello left and hello right with hello same value.</span></span>

<span data-ttu-id="3d760-185">Codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3d760-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
