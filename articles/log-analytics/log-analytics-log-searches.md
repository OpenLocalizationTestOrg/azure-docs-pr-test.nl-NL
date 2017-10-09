---
title: aaaFind gegevens met logboek van zoekopdrachten in Azure Log Analytics | Microsoft Docs
description: Logboek zoekopdrachten kunnen u toocombine en correleren machinegegevens uit meerdere bronnen binnen uw omgeving.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="23c26-103">Gegevens met behulp van logboek zoekopdrachten in logboekanalyse zoeken</span><span class="sxs-lookup"><span data-stu-id="23c26-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="23c26-104">Dit artikel wordt beschreven logboek zoekopdrachten met het huidige querytaal Hallo in logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="23c26-104">This article describes log searches using hello current query language in Log Analytics.</span></span>  <span data-ttu-id="23c26-105">Als uw werkruimte bijgewerkte toohello is [querytaal van nieuwe logboekanalyse](log-analytics-log-search-upgrade.md), en u dient te raadplegen[Understanding logboek zoekt in logboekanalyse (nieuw)](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="23c26-105">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer too[Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="23c26-106">Hallo-kern van logboekanalyse is Hallo logboek zoekfunctie waarmee u toocombine en correleren machinegegevens uit meerdere bronnen binnen uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="23c26-106">At hello core of Log Analytics is hello log search feature which allows you toocombine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="23c26-107">Oplossingen worden ook aangedreven door logboek zoeken toobring u metrische gegevens om een bepaald probleemgebied gedraaid.</span><span class="sxs-lookup"><span data-stu-id="23c26-107">Solutions are also powered by log search toobring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="23c26-108">Op de zoekpagina hello, kunt u een query maken en vervolgens wanneer u zoekt, kunt u filteren Hallo resultaten met facet besturingselementen.</span><span class="sxs-lookup"><span data-stu-id="23c26-108">On hello Search page, you can create a query, and then when you search, you can filter hello results by using facet controls.</span></span> <span data-ttu-id="23c26-109">U kunt ook tootransform geavanceerde query's, te filteren en rapport maken op de resultaten.</span><span class="sxs-lookup"><span data-stu-id="23c26-109">You can also create advanced queries tootransform, filter, and report on your results.</span></span>

<span data-ttu-id="23c26-110">Algemene logboek zoekquery's weergegeven op de meeste oplossing's.</span><span class="sxs-lookup"><span data-stu-id="23c26-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="23c26-111">U kunt in de gehele Hallo OMS-console tegels klikt u op of inzoomen in tooother items tooview details over Hallo item met logboek zoeken.</span><span class="sxs-lookup"><span data-stu-id="23c26-111">Throughout hello OMS console, you can click tiles or drill in tooother items tooview details about hello item by using log search.</span></span>

<span data-ttu-id="23c26-112">In deze zelfstudie doorlopen we voorbeelden toocover alle Hallo basisbeginselen wanneer u logboek zoeken gebruikt.</span><span class="sxs-lookup"><span data-stu-id="23c26-112">In this tutorial, we'll walk through examples toocover all hello basics when you use log search.</span></span>

<span data-ttu-id="23c26-113">We beginnen met eenvoudige, praktische voorbeelden en klik vervolgens op deze bouwen zodat u kunt een goed begrip van praktische gebruiksdoeleinden over hoe toouse Hallo syntaxis tooextract Hallo inzichten u van Hallo-gegevens wilt ophalen.</span><span class="sxs-lookup"><span data-stu-id="23c26-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how toouse hello syntax tooextract hello insights you want from hello data.</span></span>

<span data-ttu-id="23c26-114">Nadat u nagegaan wat de zoektechnieken hebt, kunt u controleren Hallo [logboekanalyse Meld zoeken verwijzing](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="23c26-114">After you've familiar with search techniques, you can review hello [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="23c26-115">Basic-filters gebruiken</span><span class="sxs-lookup"><span data-stu-id="23c26-115">Use basic filters</span></span>
<span data-ttu-id="23c26-116">Hallo eerst te beginnen tooknow die Hallo eerste deel uitmaakt van een zoekopdracht, voordat een ' | ' verticale pipe-teken is altijd een *filter*.</span><span class="sxs-lookup"><span data-stu-id="23c26-116">hello first thing tooknow is that hello first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="23c26-117">U kunt dit beschouwen als een WHERE-component in TSQL--bepaalt *wat* subset van gegevens toopull buiten Hallo OMS-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="23c26-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data toopull out of hello OMS data store.</span></span> <span data-ttu-id="23c26-118">Zoeken in het gegevensarchief Hallo is grotendeels over het opgeven van Hallo kenmerken van Hallo-gegevens die u tooextract, wilt dus is het natuurlijke dat een query met Hallo WHERE-component beginnen wilt.</span><span class="sxs-lookup"><span data-stu-id="23c26-118">Searching in hello data store is largely about specifying hello characteristics of hello data that you want tooextract, so it is natural that a query would start with hello WHERE clause.</span></span>

<span data-ttu-id="23c26-119">Hallo meest eenvoudige filters kunt u zijn *trefwoorden*, zoals 'fout' of 'out' of een computernaam op.</span><span class="sxs-lookup"><span data-stu-id="23c26-119">hello most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="23c26-120">Deze typen van eenvoudige query's in het algemeen diverse vormen retourneren van gegevens binnen Hallo dezelfde resultaatset.</span><span class="sxs-lookup"><span data-stu-id="23c26-120">These types of simple queries generally return diverse shapes of data within hello same result set.</span></span> <span data-ttu-id="23c26-121">Dit komt doordat Log Analytics uit verschillende *typen* van gegevens in Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="23c26-121">This is because Log Analytics has different *types* of data in hello system.</span></span>

### <a name="tooconduct-a-simple-search"></a><span data-ttu-id="23c26-122">een eenvoudige zoekopdrachten tooconduct</span><span class="sxs-lookup"><span data-stu-id="23c26-122">tooconduct a simple search</span></span>
1. <span data-ttu-id="23c26-123">Klik in de OMS-portal Hallo **logboek zoeken**.</span><span class="sxs-lookup"><span data-stu-id="23c26-123">In hello OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="23c26-124">![tegel Search](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="23c26-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="23c26-125">Typ in Hallo queryveld `error` en klik vervolgens op **Search**.</span><span class="sxs-lookup"><span data-stu-id="23c26-125">In hello query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="23c26-126">![Fout bij zoeken](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="23c26-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="23c26-127">Bijvoorbeeld Hallo query voor `error` in Hallo geretourneerd de volgende afbeelding 100.000 **gebeurtenis** records (verzameld door Log-beheer), 18 **ConfigurationAlert** records (gegenereerd door de configuratie Beoordeling) en 12 **ConfigurationChange** records (vastgelegd door Hallo bijhouden).</span><span class="sxs-lookup"><span data-stu-id="23c26-127">For example, hello query for `error` in hello following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by hello Change Tracking).</span></span>   
    <span data-ttu-id="23c26-128">![zoekresultaten](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="23c26-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="23c26-129">Deze filters zijn niet echt objectklassen typen.</span><span class="sxs-lookup"><span data-stu-id="23c26-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="23c26-130">*Type* is slechts een label of een eigenschap of een tekenreeks/naam/categorie, die is gekoppeld tooa gegevensitem.</span><span class="sxs-lookup"><span data-stu-id="23c26-130">*Type* is just a tag, or a property, or a string/name/category, that is attached tooa piece of data.</span></span> <span data-ttu-id="23c26-131">Een aantal documenten in Hallo system zijn gelabeld als **Type: ConfigurationAlert** en sommige zijn gelabeld als **Type: Perf**, of **gebeurtenistype:**, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="23c26-131">Some documents in hello system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="23c26-132">Elke zoekresultaat, document, record of vermelding geeft alle onbewerkte Hallo-eigenschappen en hun waarden voor elk van deze onderdelen van gegevens en kunt u deze namen veld toospecify in Hallo filter als u wilt dat tooretrieve alleen Hallo records waar Hallo veld heeft die gegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="23c26-132">Each search result, document, record, or entry displays all hello raw properties and their values for each of those pieces of data, and you can use those field names toospecify in hello filter when you want tooretrieve only hello records where hello field has that given value.</span></span>

<span data-ttu-id="23c26-133">*Type* is gewoon een veld dat alle records hebt, is niet anders dan een ander veld.</span><span class="sxs-lookup"><span data-stu-id="23c26-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="23c26-134">Dit is vastgesteld op basis van het Hallo-waarde van veld Hallo-Type.</span><span class="sxs-lookup"><span data-stu-id="23c26-134">This was established based on hello value of hello Type field.</span></span> <span data-ttu-id="23c26-135">Deze record heeft een andere vorm of vorm.</span><span class="sxs-lookup"><span data-stu-id="23c26-135">That record will have a different shape or form.</span></span> <span data-ttu-id="23c26-136">Incidenteel, **Type = Perf**, of **Type gebeurtenis =** is ook moet u toolearn tooquery prestatiegegevens of gebeurtenissen Hallo-syntaxis.</span><span class="sxs-lookup"><span data-stu-id="23c26-136">Incidentally, **Type=Perf**, or **Type=Event** is also hello syntax that you need toolearn tooquery for performance data or events.</span></span>

<span data-ttu-id="23c26-137">U kunt een dubbele punt (:) of een gelijkteken (=) na Hallo veldnaam en voor Hallo waarde gebruiken.</span><span class="sxs-lookup"><span data-stu-id="23c26-137">You can use either a colon (:) or an equal sign (=) after hello field name and before hello value.</span></span> <span data-ttu-id="23c26-138">**Gebeurtenistype:** en **Type gebeurtenis =** vergelijkbaar zijn met het betekenis, kunt u Hallo u liever stijl.</span><span class="sxs-lookup"><span data-stu-id="23c26-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose hello style you prefer.</span></span>

<span data-ttu-id="23c26-139">Dus als hello typt = Perf records hebben een veld met de naam 'CounterName' en vervolgens kunt u een query die lijkt op `Type=Perf CounterName="% Processor Time"`.</span><span class="sxs-lookup"><span data-stu-id="23c26-139">So, if hello Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="23c26-140">Hiermee krijgt u alleen Hallo prestatiegegevens als naam Prestatiemeter Hallo is '% processortijd'.</span><span class="sxs-lookup"><span data-stu-id="23c26-140">This will give you only hello performance data where hello performance counter name is "% Processor Time".</span></span>

### <a name="toosearch-for-processor-time-performance-data"></a><span data-ttu-id="23c26-141">toosearch voor prestatiegegevens van processor time</span><span class="sxs-lookup"><span data-stu-id="23c26-141">toosearch for processor time performance data</span></span>
* <span data-ttu-id="23c26-142">Typ in het Hallo-zoekveld query`Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="23c26-142">In hello search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="23c26-143">U kunt ook niet meer specifiek en **InstanceName = _ 'Totaal'** in Hallo-query die een Windows-prestatiemeteritem is.</span><span class="sxs-lookup"><span data-stu-id="23c26-143">You can also be more specific and use **InstanceName=_'Total'** in hello query, which is a Windows performance counter.</span></span> <span data-ttu-id="23c26-144">U kunt ook een facet en een andere selecteren **veldwaarde:**.</span><span class="sxs-lookup"><span data-stu-id="23c26-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="23c26-145">Hallo-filter wordt automatisch tooyour filter toegevoegd op Hallo query-balk.</span><span class="sxs-lookup"><span data-stu-id="23c26-145">hello filter is automatically added tooyour filter in hello query bar.</span></span> <span data-ttu-id="23c26-146">U kunt dit zien in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="23c26-146">You can see this in hello following image.</span></span> <span data-ttu-id="23c26-147">Er wordt aangegeven waar tooclick tooadd **InstanceName: '_Totaal'** toohello query zonder iets te typen.</span><span class="sxs-lookup"><span data-stu-id="23c26-147">It shows you where tooclick tooadd **InstanceName:’_Total’** toohello query without typing anything.</span></span>

![facet zoeken](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="23c26-149">Er wordt nu uw query`Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="23c26-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="23c26-150">In dit voorbeeld wordt er geen toospecify **Type = Perf** tooget toothis resultaat.</span><span class="sxs-lookup"><span data-stu-id="23c26-150">In this example, you don't have toospecify **Type=Perf** tooget toothis result.</span></span> <span data-ttu-id="23c26-151">Omdat Hallo velden CounterName en InstanceName bestaan alleen voor records van het Type = Perf, Hallo-query is specifiek genoeg tooreturn Hallo als langer vorige een Hallo dezelfde resultaten:</span><span class="sxs-lookup"><span data-stu-id="23c26-151">Because hello fields CounterName and InstanceName only exist for records of Type=Perf, hello query is specific enough tooreturn hello same results as hello longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="23c26-152">Dit komt doordat alle Hallo filters in Hallo query worden geëvalueerd als *en* met elkaar.</span><span class="sxs-lookup"><span data-stu-id="23c26-152">This is because all hello filters in hello query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="23c26-153">Effectief hello meer velden u toohello criteria toevoegen, krijgt u minder specifiek en verfijnd resultaten.</span><span class="sxs-lookup"><span data-stu-id="23c26-153">Effectively, hello more fields you add toohello criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="23c26-154">Bijvoorbeeld Hallo query `Type=Event EventLog="Windows PowerShell"` is identiek te`Type=Event AND EventLog="Windows PowerShell"`.</span><span class="sxs-lookup"><span data-stu-id="23c26-154">For example, hello query `Type=Event EventLog="Windows PowerShell"` is identical too`Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="23c26-155">Retourneert alle gebeurtenissen die zijn aangemeld en verzameld uit Hallo Windows PowerShell-gebeurtenislogboek.</span><span class="sxs-lookup"><span data-stu-id="23c26-155">It returns all events that were logged in and collected from hello Windows PowerShell event log.</span></span> <span data-ttu-id="23c26-156">Als u een filter meerdere keren toevoegen door te selecteren herhaaldelijk Hallo dezelfde beperkingsfacet, klikt u vervolgens Hallo probleem puur cosmetisch--het Hallo zoekbalk bruikbaar mogelijk blijft, maar nog steeds retourneert Hallo dezelfde resultaten Hallo impliciete AND-operator is er altijd is.</span><span class="sxs-lookup"><span data-stu-id="23c26-156">If you add a filter multiple times by repeatedly selecting hello same facet, then hello issue is purely cosmetic--it might clutter hello Search bar, but it still returns hello same results because hello implicit AND operator is always there.</span></span>

<span data-ttu-id="23c26-157">U kunt eenvoudig hello impliciete AND-operator met behulp van een niet-operator expliciet omkeren.</span><span class="sxs-lookup"><span data-stu-id="23c26-157">You can easily reverse hello implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="23c26-158">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="23c26-158">For example:</span></span>

<span data-ttu-id="23c26-159">`Type:Event NOT(EventLog:"Windows PowerShell")`of de bijbehorende equivalent `Type=Event EventLog!="Windows PowerShell"` alle gebeurtenissen van andere logboeken die geen Windows PowerShell-logboek Hallo retourneren.</span><span class="sxs-lookup"><span data-stu-id="23c26-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT hello Windows PowerShell log.</span></span>

<span data-ttu-id="23c26-160">Of u kunt andere Booleaanse operator gebruikt, zoals 'Of'.</span><span class="sxs-lookup"><span data-stu-id="23c26-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="23c26-161">Hallo volgende query retourneert records met welke Hallo EventLog een toepassing of het systeem is.</span><span class="sxs-lookup"><span data-stu-id="23c26-161">hello following query returns records for which hello EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="23c26-162">Hallo hierboven query gebruikt, krijgt u vermeldingen voor beide logboeken in Hallo dezelfde set leiden.</span><span class="sxs-lookup"><span data-stu-id="23c26-162">Using hello above query, you’ll get entries for both logs in hello same result set.</span></span>

<span data-ttu-id="23c26-163">Echter, als u hello of door Hallo impliciete en in plaats verwijdert, vervolgens hello volgende query wordt geen queryplan geen resultaten omdat er een logboekvermelding die deel uitmaakt van tooBOTH Logboeken niet.</span><span class="sxs-lookup"><span data-stu-id="23c26-163">However, if you remove hello OR by leaving hello implicit AND in place, then hello following query will not produce any results because there isn’t an event log entry that belongs tooBOTH logs.</span></span> <span data-ttu-id="23c26-164">Elke logboekvermelding is tooonly een van twee Hallo-Logboeken geschreven.</span><span class="sxs-lookup"><span data-stu-id="23c26-164">Each event log entry was written tooonly one of hello two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="23c26-165">Aanvullende filters gebruiken</span><span class="sxs-lookup"><span data-stu-id="23c26-165">Use additional filters</span></span>
<span data-ttu-id="23c26-166">Hallo retourneert volgende query vermeldingen voor 2 gebeurtenislogboeken voor alle Hallo-computers die gegevens verzonden.</span><span class="sxs-lookup"><span data-stu-id="23c26-166">hello following query returns entries for 2 event logs for all hello computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![zoekresultaten](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="23c26-168">Selecteer een van de Hallo velden of filters wordt Hallo query tooa specifieke computer, met uitzondering van alle andere protocollen beperken.</span><span class="sxs-lookup"><span data-stu-id="23c26-168">Selecting one of hello fields or filters will narrow hello query tooa specific computer, excluding all other ones.</span></span> <span data-ttu-id="23c26-169">de resulterende query Hallo zou lijken op Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="23c26-169">hello resulting query would resemble hello following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="23c26-170">Dit volgende gelijkwaardige toohello, is vanwege Hallo impliciete AND.</span><span class="sxs-lookup"><span data-stu-id="23c26-170">Which is equivalent toohello following, because of hello implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="23c26-171">Elke query wordt geëvalueerd in Hallo expliciete volgorde.</span><span class="sxs-lookup"><span data-stu-id="23c26-171">Each query is evaluated in hello following explicit order.</span></span> <span data-ttu-id="23c26-172">Opmerking Hallo haakje.</span><span class="sxs-lookup"><span data-stu-id="23c26-172">Note hello parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="23c26-173">Net als Hallo gebeurtenislogboek veld, kunt u alleen gegevens voor een set specifieke computers ophalen door toe te voegen of.</span><span class="sxs-lookup"><span data-stu-id="23c26-173">Just like hello event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="23c26-174">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="23c26-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="23c26-175">Op deze manier deze query return na Hallo **% CPU-tijd** voor Hallo slechts twee computers geselecteerde.</span><span class="sxs-lookup"><span data-stu-id="23c26-175">Similarly, this hello following query return **% CPU Time** for hello selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="23c26-176">Veldtypen</span><span class="sxs-lookup"><span data-stu-id="23c26-176">Field types</span></span>
<span data-ttu-id="23c26-177">Wanneer u filters maakt, moet u Hallo verschillen bij het werken met verschillende typen velden die zijn geretourneerd door het logboek zoekopdrachten begrijpen.</span><span class="sxs-lookup"><span data-stu-id="23c26-177">When creating filters, you should understand hello differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="23c26-178">**De doorzoekbare velden** weergeven in blauw weergegeven in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="23c26-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="23c26-179">U kunt de doorzoekbare velden in voorwaarden specifieke toohello zoekveld zoals Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="23c26-179">You can use searchable fields in search conditions specific toohello field such as hello following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="23c26-180">**Vrije tekst doorzoekbare velden** grijs in de zoekresultaten worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="23c26-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="23c26-181">Ze kunnen niet worden gebruikt met voorwaarden specifieke toohello zoekveld zoals doorzoekbare velden.</span><span class="sxs-lookup"><span data-stu-id="23c26-181">They cannot be used with search conditions specific toohello field like searchable fields.</span></span>  <span data-ttu-id="23c26-182">Ze worden alleen bij het uitvoeren van een query op alle gebieden zoals Hallo volgende doorzocht.</span><span class="sxs-lookup"><span data-stu-id="23c26-182">They are only searched when performing a query across all fields such as hello following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="23c26-183">Booleaanse operators</span><span class="sxs-lookup"><span data-stu-id="23c26-183">Boolean operators</span></span>
<span data-ttu-id="23c26-184">Met datetime en numerieke velden, kunt u zoeken naar waarden die *groter is dan*, *minder dan*, en *kleiner dan of gelijk*.</span><span class="sxs-lookup"><span data-stu-id="23c26-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="23c26-185">U kunt eenvoudig operators zoals >, <>, =, < =,! = in Hallo query zoekbalk.</span><span class="sxs-lookup"><span data-stu-id="23c26-185">You can use simple operators such as >, < , >=, <= , != in hello query search bar.</span></span>

<span data-ttu-id="23c26-186">U kunt een specifiek gebeurtenislogboek opvragen voor een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="23c26-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="23c26-187">Bijvoorbeeld, wordt Hallo afgelopen 24 uur uitgedrukt Hello symbool expressie te volgen.</span><span class="sxs-lookup"><span data-stu-id="23c26-187">For example, hello last 24 hours is expressed with hello following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a><span data-ttu-id="23c26-188">met behulp van een Booleaanse operator toosearch</span><span class="sxs-lookup"><span data-stu-id="23c26-188">toosearch using a boolean operator</span></span>
* <span data-ttu-id="23c26-189">Typ in het Hallo-zoekveld query`EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="23c26-189">In hello search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="23c26-190">![zoeken met Booleaanse waarde](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="23c26-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="23c26-191">Hoewel u kunt beheren tijdsinterval grafisch Hallo en meestal kunt u toodo, zijn er voordelen tooincluding een tijdfilter rechtstreeks in het Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="23c26-191">Although you can control hello time interval graphically, and most times you might want toodo that, there are advantages tooincluding a time filter directly into hello query.</span></span> <span data-ttu-id="23c26-192">Bijvoorbeeld: dit goed werkt met dashboards waar u tijd voor elke tegel, ongeacht Hallo Hallo kunt negeren *globale* tijd selector op Hallo dashboardpagina.</span><span class="sxs-lookup"><span data-stu-id="23c26-192">For example, this works great with dashboards where you can override hello time for each tile, regardless of hello *global* time selector on hello dashboard page.</span></span> <span data-ttu-id="23c26-193">Zie voor meer informatie [tijd belangrijk is in het Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span><span class="sxs-lookup"><span data-stu-id="23c26-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="23c26-194">Bij het filteren door de tijd, houd er rekening mee dat u resultaten voor Hallo krijgen *snijpunt* Hallo twee perioden: Hallo hebt opgegeven in Hallo OMS-portal (S1) en Hallo hebt opgegeven in het Hallo-query (S2).</span><span class="sxs-lookup"><span data-stu-id="23c26-194">When filtering by time, keep in mind that you get results for hello *intersection* of hello two time periods: hello one specified in hello OMS portal (S1) and hello one specified in hello query (S2).</span></span>

![snijpunt](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="23c26-196">Dit betekent dat, als hello perioden elkaar niet overlappen, bijvoorbeeld in Hallo OMS-portal waar u desgewenst **deze week** en in Hallo query waarin u definiëren **afgelopen week**, is er geen snijpunt en u won't alle resultaten krijgen.</span><span class="sxs-lookup"><span data-stu-id="23c26-196">This means, if hello time periods don’t intersect, for example in hello OMS portal where you choose **This week** and in hello query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="23c26-197">Vergelijkingsoperators voor Hallo TimeGenerated veld gebruikt, zijn ook nuttig zijn in andere gevallen.</span><span class="sxs-lookup"><span data-stu-id="23c26-197">Comparison operators used for hello TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="23c26-198">Bijvoorbeeld, met numerieke velden.</span><span class="sxs-lookup"><span data-stu-id="23c26-198">For example, with numeric fields.</span></span>

<span data-ttu-id="23c26-199">Bijvoorbeeld opgegeven dat van de beoordeling van de configuratie waarschuwingen Hallo ernstwaarden volgende hebben:</span><span class="sxs-lookup"><span data-stu-id="23c26-199">For example, given that Configuration Assessment’s alerts have hello following severity values:</span></span>

* <span data-ttu-id="23c26-200">0 = informatie</span><span class="sxs-lookup"><span data-stu-id="23c26-200">0 = Information</span></span>
* <span data-ttu-id="23c26-201">1 = waarschuwing</span><span class="sxs-lookup"><span data-stu-id="23c26-201">1 = Warning</span></span>
* <span data-ttu-id="23c26-202">2 = kritiek</span><span class="sxs-lookup"><span data-stu-id="23c26-202">2 = Critical</span></span>

<span data-ttu-id="23c26-203">U kunt doorzoeken op waarschuwingen en kritieke waarschuwingen en informatieve netwerken met de volgende query Hallo ook uitsluiten:</span><span class="sxs-lookup"><span data-stu-id="23c26-203">You can query for both warning and critical alerts and also exclude informational ones with hello following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="23c26-204">U kunt ook query's bereik gebruiken.</span><span class="sxs-lookup"><span data-stu-id="23c26-204">You can also use range queries.</span></span> <span data-ttu-id="23c26-205">Dit betekent dat u Hallo begin en einde bereik van waarden in een reeks kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="23c26-205">This means that you can provide hello beginning and end range of values in a sequence.</span></span> <span data-ttu-id="23c26-206">Bijvoorbeeld, als u wilt dat gebeurtenissen uit Operations Manager-gebeurtenislogboek Hallo waar hello EventID is too2100 groter dan of gelijk zijn, maar niet groter zijn dan 2199, en vervolgens Hallo na query wilt retourneren.</span><span class="sxs-lookup"><span data-stu-id="23c26-206">For example, if you want events from hello Operations Manager event log where hello EventID is greater than or equal too2100 but not greater than 2199, then hello following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="23c26-207">moet u de syntaxis van de Hallo bereik is Hallo dubbele punt (:) veldwaarde: scheidingsteken en *niet* Hallo gelijkteken (=).</span><span class="sxs-lookup"><span data-stu-id="23c26-207">hello range syntax you must use is hello colon (:) field:value separator and *not* hello equal sign (=).</span></span> <span data-ttu-id="23c26-208">Zet de boven- en ondergrenzen einde Hallo van Hallo-bereik tussen vierkante haken en scheiden met twee punten (.).</span><span class="sxs-lookup"><span data-stu-id="23c26-208">Enclose hello lower and upper end of hello range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="23c26-209">Zoekresultaten manipuleren</span><span class="sxs-lookup"><span data-stu-id="23c26-209">Manipulate search results</span></span>
<span data-ttu-id="23c26-210">Wanneer u gegevens zoekt, gaat u wilt toorefine uw zoekopdracht en een goede beheerniveau Hallo resultaten hebben.</span><span class="sxs-lookup"><span data-stu-id="23c26-210">When you're searching for data, you'll want toorefine your search query and have a good level of control over hello results.</span></span> <span data-ttu-id="23c26-211">Wanneer resultaten worden opgehaald, kunt u opdrachten tootransform toepassen ze.</span><span class="sxs-lookup"><span data-stu-id="23c26-211">When results are retrieved, you can apply commands tootransform them.</span></span>

<span data-ttu-id="23c26-212">Opdrachten in logboekanalyse zoekopdrachten *moet* Volg na het teken van Hallo verticale pipe (|).</span><span class="sxs-lookup"><span data-stu-id="23c26-212">Commands in Log Analytics searches *must* follow after hello vertical pipe character (|).</span></span> <span data-ttu-id="23c26-213">Een filter moet altijd Hallo eerste deel van een queryreeks.</span><span class="sxs-lookup"><span data-stu-id="23c26-213">A filter must always be hello first part of a query string.</span></span> <span data-ttu-id="23c26-214">Hallo-gegevensset waarmee u samenwerkt definieert en vervolgens 'doorgesluisd' de resultaten in een opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="23c26-214">It defines hello data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="23c26-215">U kunt vervolgens Hallo pipe tooadd aanvullende opdrachten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="23c26-215">You can then use hello pipe tooadd additional commands.</span></span> <span data-ttu-id="23c26-216">Dit is los vergelijkbare toohello Windows PowerShell-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="23c26-216">This is loosely similar toohello Windows PowerShell pipeline.</span></span>

<span data-ttu-id="23c26-217">In het algemeen Hallo logboekanalyse zoektaal toofollow PowerShell stijl en richtlijnen toomake probeert it vergelijkbare toohello IT-professionals en tooease Hallo leerproces.</span><span class="sxs-lookup"><span data-stu-id="23c26-217">In general, hello Log Analytics search language tries toofollow PowerShell style and guidelines toomake it similar toohello IT pros, and tooease hello learning curve.</span></span>

<span data-ttu-id="23c26-218">Opdrachten hebben namen van termen, zodat u kunt in één oogopslag zien wat ze doen.</span><span class="sxs-lookup"><span data-stu-id="23c26-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="23c26-219">Sorteren</span><span class="sxs-lookup"><span data-stu-id="23c26-219">Sort</span></span>
<span data-ttu-id="23c26-220">Hallo sorteren opdracht kunt u toodefine Hallo sorteervolgorde op een of meer velden.</span><span class="sxs-lookup"><span data-stu-id="23c26-220">hello sort command allows you toodefine hello sorting order by one or multiple fields.</span></span> <span data-ttu-id="23c26-221">Zelfs als u niet, standaard gebruikt, wordt een tijd aflopende volgorde afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="23c26-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="23c26-222">de meest recente resultaten Hallo zijn altijd boven Hallo zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="23c26-222">hello most recent results are always at hello top of search results.</span></span> <span data-ttu-id="23c26-223">Dit betekent dat wanneer u een zoekopdracht met uitvoert `Type=Event EventID=1234` wat daadwerkelijk wordt uitgevoerd voor u is:</span><span class="sxs-lookup"><span data-stu-id="23c26-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="23c26-224">Dat is omdat het Hallo-type van de gebruikerservaring die u bekend met in Logboeken bent.</span><span class="sxs-lookup"><span data-stu-id="23c26-224">That's because it is hello type of experience you are familiar with in logs.</span></span> <span data-ttu-id="23c26-225">Bijvoorbeeld, in de logboeken van Windows hello.</span><span class="sxs-lookup"><span data-stu-id="23c26-225">For example, in hello Windows Event Viewer.</span></span>

<span data-ttu-id="23c26-226">U kunt sorteren toochange Hallo manier resultaten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="23c26-226">You can use Sort toochange hello way results are returned.</span></span> <span data-ttu-id="23c26-227">Hallo volgende voorbeelden laten zien hoe dit werkt.</span><span class="sxs-lookup"><span data-stu-id="23c26-227">hello following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="23c26-228">Hello eenvoudige voorbeelden hierboven ziet u hoe opdrachten werken--ze Hallo vorm van Hallo resultaten gefilterd als resultaat gegeven Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="23c26-228">hello simple examples above show you how commands work--they change hello shape of hello results that hello filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="23c26-229">Limiet en boven</span><span class="sxs-lookup"><span data-stu-id="23c26-229">Limit and top</span></span>
<span data-ttu-id="23c26-230">Een andere minder bekende opdracht is een LIMIET.</span><span class="sxs-lookup"><span data-stu-id="23c26-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="23c26-231">De limiet is een PowerShell-achtige term.</span><span class="sxs-lookup"><span data-stu-id="23c26-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="23c26-232">De limiet is identiek toohello bovenste opdracht.</span><span class="sxs-lookup"><span data-stu-id="23c26-232">Limit is functionally identical toohello TOP command.</span></span> <span data-ttu-id="23c26-233">Hallo volgende query's Hallo dezelfde resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="23c26-233">hello following queries return hello same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a><span data-ttu-id="23c26-234">met behulp van de bovenste toosearch</span><span class="sxs-lookup"><span data-stu-id="23c26-234">toosearch using top</span></span>
* <span data-ttu-id="23c26-235">Typ in het Hallo-zoekveld query`Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="23c26-235">In hello search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="23c26-236">![Zoek boven](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="23c26-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="23c26-237">In het Hallo-afbeelding hierboven, zijn er 358 duizend records met gebeurtenis-id = 600.</span><span class="sxs-lookup"><span data-stu-id="23c26-237">In hello image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="23c26-238">Hallo velden, facetten en filters op Hallo links altijd informatie weergeven over Hallo resultaten geretourneerd *door Hallo filter gedeelte* van Hallo query, die deel uitmaakt Hallo voordat een pipe-teken.</span><span class="sxs-lookup"><span data-stu-id="23c26-238">hello fields, facets, and filters on hello left always show information about hello results returned *by hello filter portion* of hello query, which is hello part before any pipe character.</span></span> <span data-ttu-id="23c26-239">Hallo **resultaten** deelvenster alleen resultaat Hallo meest recente 1, omdat Hallo voorbeeldopdracht vorm en getransformeerd Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="23c26-239">hello **Results** pane only returns hello most recent 1 result, because hello example command shaped and transformed hello results.</span></span>

### <a name="select"></a><span data-ttu-id="23c26-240">Selecteer</span><span class="sxs-lookup"><span data-stu-id="23c26-240">Select</span></span>
<span data-ttu-id="23c26-241">Hallo SELECT-opdracht gedraagt zich als Select-Object in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23c26-241">hello SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="23c26-242">Het resultaat gefilterde resultaten die niet beschikt over alle hun oorspronkelijke eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="23c26-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="23c26-243">In plaats daarvan wordt geselecteerd Hallo alleen eigenschappen die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="23c26-243">Instead, it selects only hello properties that you specify.</span></span>

#### <a name="toorun-a-search-using-hello-select-command"></a><span data-ttu-id="23c26-244">toorun een zoeken met de Hallo select-opdracht</span><span class="sxs-lookup"><span data-stu-id="23c26-244">toorun a search using hello select command</span></span>
1. <span data-ttu-id="23c26-245">Typ in zoeken `Type=Event` en klik vervolgens op **Search**.</span><span class="sxs-lookup"><span data-stu-id="23c26-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="23c26-246">Klik op **+ meer** in een Hallo resultaten tooview alle Hallo-eigenschappen die Hallo resultaten hebben.</span><span class="sxs-lookup"><span data-stu-id="23c26-246">Click **+ show more** in one of hello results tooview all hello properties that hello results have.</span></span>
3. <span data-ttu-id="23c26-247">Selecteer een aantal van deze expliciet en hello wijzigingen in query's te`Type=Event | Select Computer,EventID,RenderedDescription`.</span><span class="sxs-lookup"><span data-stu-id="23c26-247">Select some of those explicitly, and hello query changes too`Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="23c26-248">![Selecteer zoeken](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="23c26-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="23c26-249">Met deze opdracht is bijzonder nuttig wanneer u zoeken dat uitvoer toocontrol wilt en kiest alleen Hallo delen van gegevens die echt belangrijk voor uw onderzoek, die vaak geen volledige Hallo-record.</span><span class="sxs-lookup"><span data-stu-id="23c26-249">This command is particularly useful when you want toocontrol search output and choose only hello portions of data that really matter for your exploration, which often isn’t hello full record.</span></span> <span data-ttu-id="23c26-250">Dit is ook handig wanneer de records van verschillende typen hebben *sommige* algemene eigenschappen, maar niet *alle* van hun eigenschappen gelden.</span><span class="sxs-lookup"><span data-stu-id="23c26-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="23c26-251">De uitvoer genereren die meer toe op een tabel lijkt of geschikt voor tooa CSV-bestand exporteren en vervolgens massaged in Excel.</span><span class="sxs-lookup"><span data-stu-id="23c26-251">The, you can generate output that looks more naturally like a table, or work well when exported tooa CSV file and then massaged in Excel.</span></span>

## <a name="use-hello-measure-command"></a><span data-ttu-id="23c26-252">Hallo meting opdracht gebruiken</span><span class="sxs-lookup"><span data-stu-id="23c26-252">Use hello measure command</span></span>
<span data-ttu-id="23c26-253">METING is een van de meest veelzijdige opdrachten Hallo in logboekanalyse zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="23c26-253">MEASURE is one of hello most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="23c26-254">Hiermee kunt u tooapply statistische *functies* tooyour gegevens en statistische resultaten gegroepeerd op een bepaald veld.</span><span class="sxs-lookup"><span data-stu-id="23c26-254">It allows you tooapply statistical *functions* tooyour data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="23c26-255">Er zijn meerdere statistische functies die ondersteuning biedt voor meting.</span><span class="sxs-lookup"><span data-stu-id="23c26-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="23c26-256">Meting count()</span><span class="sxs-lookup"><span data-stu-id="23c26-256">Measure count()</span></span>
<span data-ttu-id="23c26-257">Hallo eerste statistische functie toowork met en een van de eenvoudigste toounderstand Hallo Hallo is *count()* functie.</span><span class="sxs-lookup"><span data-stu-id="23c26-257">hello first statistical function toowork with, and one of hello simplest toounderstand is hello *count()* function.</span></span>

<span data-ttu-id="23c26-258">Resultaat is van een zoekopdracht zoals `Type=Event`, ook wel facetten op Hallo linkerkant zoekresultaten filters weer.</span><span class="sxs-lookup"><span data-stu-id="23c26-258">Results from any search query such as `Type=Event`, show filters also called facets on hello left side of search results.</span></span> <span data-ttu-id="23c26-259">Hallo filters zien een verdeling van waarden met een bepaald veld voor de Hallo resultaten in Hallo-zoekopdracht uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="23c26-259">hello filters show a distribution of values by a given field for hello results in hello search executed.</span></span>

![zoeken maateenheid count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="23c26-261">Bijvoorbeeld in Hallo bovenstaande u afbeelding ziet Hallo **Computer** veld en geeft aan dat in de Hallo bijna 739 duizend gebeurtenissen in de resultaten hello, 68 uniek en anders waarden voor Hallo **Computer** het veld in deze records.</span><span class="sxs-lookup"><span data-stu-id="23c26-261">For example, in hello image above you'll see hello **Computer** field and it shows that within hello almost 739 thousand events in hello results, there are 68 unique and distinct values for hello **Computer** field in those records.</span></span> <span data-ttu-id="23c26-262">Hallo-tegel bevat alleen Hallo bovenste 5 die zich Hallo meest voorkomende 5 waarden die zijn geschreven in Hallo **Computer** velden), gesorteerd op Hallo aantal documenten dat die specifieke waarde in het veld bevatten.</span><span class="sxs-lookup"><span data-stu-id="23c26-262">hello tile only shows hello top 5, which are hello most common 5 values that are written in hello **Computer** fields), sorted by hello number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="23c26-263">In het Hallo-afbeelding ziet u dat-tussen deze gebeurtenissen bijna 369 duizend – 90 duizend afkomstig zijn van Hallo OpsInsights04.contoso.com computer, 83 duizend van Hallo DB03.contoso.com computer, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="23c26-263">In hello image you can see that – among those almost 369 thousand events – 90 thousand come from hello OpsInsights04.contoso.com computer, 83 thousand from hello DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="23c26-264">Wat gebeurt er als u wilt dat toosee alle waarden, omdat het Hallo-tegel alleen toont alleen Hallo top 5?</span><span class="sxs-lookup"><span data-stu-id="23c26-264">What if you want toosee all values, since hello tile only shows only hello top 5?</span></span>

<span data-ttu-id="23c26-265">Dat is de meting van welke Hallo opdracht kunt doen met de Hallo count() functie.</span><span class="sxs-lookup"><span data-stu-id="23c26-265">That’s what hello measure command can do with hello count() function.</span></span> <span data-ttu-id="23c26-266">Deze functie heeft geen parameters gebruikt.</span><span class="sxs-lookup"><span data-stu-id="23c26-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="23c26-267">U zojuist hebt waarop u toogroup door – Hallo wilt Hallo-veld opgeven **Computer** veld in dit geval:</span><span class="sxs-lookup"><span data-stu-id="23c26-267">You just specify hello field by which you want toogroup by – hello **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![zoeken maateenheid count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="23c26-269">Echter **Computer** is slechts een veld gebruikt *in* elke stukje informatie: Er zijn geen relationele databases die zijn betrokken, en er is geen afzonderlijke **Computer** overal object.</span><span class="sxs-lookup"><span data-stu-id="23c26-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="23c26-270">NET Hallo waarden *in* Hallo gegevens kunt beschrijven welke entiteit gegenereerd deze, en een aantal andere kenmerken en aspecten van de gegevens in Hallo Hallo daarom term *facet*.</span><span class="sxs-lookup"><span data-stu-id="23c26-270">Just hello values *in* hello data can describe which entity generated them, and a number of other characteristics and aspects of hello data – hence hello term *facet*.</span></span> <span data-ttu-id="23c26-271">U kunt echter alleen ook groeperen op andere velden.</span><span class="sxs-lookup"><span data-stu-id="23c26-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="23c26-272">Omdat de oorspronkelijke resultaten Hallo bijna 739 duizend gebeurtenissen die zijn doorgesluisd naar Hallo meting opdracht ook een veld met de naam **EventID**, u kunt toepassen Hallo dezelfde techniek toogroup door dat veld en krijgt u een aantal gebeurtenissen dat door de gebeurtenis-id:</span><span class="sxs-lookup"><span data-stu-id="23c26-272">Because hello original results of almost 739 thousand events that are piped into hello measure command also have a field called **EventID**, you can apply hello same technique toogroup by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="23c26-273">Als u niet bent geïnteresseerd in Hallo record zelf aantal die een specifieke waarde bevatten, maar in plaats daarvan als u alleen een lijst met Hallo zelf waarden, kunt u toevoegen een *Selecteer* opdracht aan Hallo einde van deze en selecteer Hallo eerste kolom:</span><span class="sxs-lookup"><span data-stu-id="23c26-273">If you're not interested in hello actual record count that contain a specific value, but instead if you only want a list of hello values themselves, you can add a *Select* command at hello end of it and just select hello first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="23c26-274">Vervolgens kunt u meer geavanceerde ophalen en vóór sorteren Hallo resulteert in het Hallo-query of hoeft u alleen op Hallo kolommen in Hallo raster te.</span><span class="sxs-lookup"><span data-stu-id="23c26-274">Then you can get more intricate and pre-sort hello results in hello query, or you can just click hello columns in hello grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a><span data-ttu-id="23c26-275">toosearch met behulp van de maateenheid count</span><span class="sxs-lookup"><span data-stu-id="23c26-275">toosearch using measure count</span></span>
* <span data-ttu-id="23c26-276">Typ in het Hallo-zoekveld query`Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="23c26-276">In hello search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="23c26-277">Append `| Select EventID` toohello einde van Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="23c26-277">Append `| Select EventID` toohello end of hello query.</span></span>
* <span data-ttu-id="23c26-278">Ten slotte toevoegen `| Sort EventID asc` toohello einde van Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="23c26-278">Finally, append `| Sort EventID asc` toohello end of hello query.</span></span>

<span data-ttu-id="23c26-279">Er zijn een aantal belangrijke punten toonotice en leg de nadruk op:</span><span class="sxs-lookup"><span data-stu-id="23c26-279">There are a couple important points toonotice and emphasize:</span></span>

<span data-ttu-id="23c26-280">Eerst Hallo u ziet geen zijn resultaten oorspronkelijke onbewerkte resultaten Hallo meer.</span><span class="sxs-lookup"><span data-stu-id="23c26-280">First, hello results you see are not hello original raw results anymore.</span></span> <span data-ttu-id="23c26-281">In plaats daarvan zijn ze cumulatieve resultaten – in wezen groepen van de resultaten.</span><span class="sxs-lookup"><span data-stu-id="23c26-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="23c26-282">Dit geen probleem, maar moet u weten dat u bent interactie met een heel andere vorm van gegevens die afwijkt van Hallo oorspronkelijke onbewerkte vorm die wordt gemaakt op Hallo snel als gevolg van Hallo aggregatie/statistische functie.</span><span class="sxs-lookup"><span data-stu-id="23c26-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from hello original raw shape that gets created on hello fly as a result of hello aggregation/statistical function.</span></span>

<span data-ttu-id="23c26-283">Tweede, **aantal meten** retourneert Hallo momenteel alleen top 100 verschillende resultaten.</span><span class="sxs-lookup"><span data-stu-id="23c26-283">Second, **Measure count** currently returns only hello top 100 distinct results.</span></span> <span data-ttu-id="23c26-284">Deze limiet niet van toepassing toohello andere statistische functies.</span><span class="sxs-lookup"><span data-stu-id="23c26-284">This limit does not apply toohello other statistical functions.</span></span> <span data-ttu-id="23c26-285">U hebt dus meestal toouse een nauwkeurigere filter eerste toosearch nodig voor specifieke items voordat u een meting count() toepassen.</span><span class="sxs-lookup"><span data-stu-id="23c26-285">So, you'll usually need toouse a more precise filter first toosearch for specific items before you apply measure count().</span></span>

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a><span data-ttu-id="23c26-286">Hallo max en min-functies gebruiken met Hallo meting opdracht</span><span class="sxs-lookup"><span data-stu-id="23c26-286">Use hello max and min functions with hello measure command</span></span>
<span data-ttu-id="23c26-287">Er zijn verschillende scenario's waarbij **meting Max()** en **meting zijn** zijn nuttig.</span><span class="sxs-lookup"><span data-stu-id="23c26-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="23c26-288">Echter, omdat elke functie tegengestelde laten we van elkaar hebt Max() zien en u kunt experimenteren met zijn zelf.</span><span class="sxs-lookup"><span data-stu-id="23c26-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="23c26-289">Als u een query voor beveiligingsgebeurtenissen, hebben ze een **niveau** eigenschap die kan verschillen.</span><span class="sxs-lookup"><span data-stu-id="23c26-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="23c26-290">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="23c26-290">For example:</span></span>

```
Type=SecurityEvent
```

![zoeken maatregel telling starten](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="23c26-292">Als u tooview Hallo hoogste waarde voor alle Hallo beveiliging wilt kunt gebeurtenissen krijgt een gemeenschappelijke Computer Hallo group by-veld, u</span><span class="sxs-lookup"><span data-stu-id="23c26-292">If you want tooview hello highest value for all of hello security events given a common Computer, hello group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![maximale computer zoeken meting](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="23c26-294">Die wordt weergegeven voor Hallo-computers waarop **niveau** records, de meeste van deze hebben ten minste 8, niveau veel had een niveau van 16.</span><span class="sxs-lookup"><span data-stu-id="23c26-294">It will display that for hello computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![maximale zoektijd meting gegenereerd computer](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="23c26-296">Deze functie werkt goed samen met de getallen, maar het werkt ook met DateTime-velden.</span><span class="sxs-lookup"><span data-stu-id="23c26-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="23c26-297">Laatste is handig toocheck voor Hallo of de meest recente tijdstempel van elk deel van de gegevens die zijn geïndexeerd voor elke computer.</span><span class="sxs-lookup"><span data-stu-id="23c26-297">It is useful toocheck for hello last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="23c26-298">Bijvoorbeeld: wanneer is het meest recente beveiligingsgebeurtenis Hallo gerapporteerd voor elke computer?</span><span class="sxs-lookup"><span data-stu-id="23c26-298">For example: When was hello most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="23c26-299">De functie Avg. hello gebruiken met Hallo meting opdracht</span><span class="sxs-lookup"><span data-stu-id="23c26-299">Use hello avg function with hello measure command</span></span>
<span data-ttu-id="23c26-300">Hallo Avg() statistische functie gebruikt in combinatie met een meting kunt u toocalculate Hallo gemiddelde waarde van een veld en groep resulteert door Hallo dezelfde of een ander veld.</span><span class="sxs-lookup"><span data-stu-id="23c26-300">hello Avg() statistical function used with measure allows you toocalculate hello average value for some field, and group results by hello same or other field.</span></span> <span data-ttu-id="23c26-301">Dit is handig in tal van gevallen, zoals de prestatiegegevens.</span><span class="sxs-lookup"><span data-stu-id="23c26-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="23c26-302">We beginnen met de prestatiegegevens.</span><span class="sxs-lookup"><span data-stu-id="23c26-302">We'll start with performance data.</span></span> <span data-ttu-id="23c26-303">Houd er rekening mee dat OMS momenteel prestatiemeteritems voor Windows- en Linux-machines verzamelt.</span><span class="sxs-lookup"><span data-stu-id="23c26-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="23c26-304">toosearch voor *alle* prestatiegegevens, de meest eenvoudige query Hallo is:</span><span class="sxs-lookup"><span data-stu-id="23c26-304">toosearch for *all* performance data, hello most basic query is:</span></span>

```
Type=Perf
```

![Gem. start zoeken](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="23c26-306">Hallo eerste wat u kunt zien is dat Log Analytics u drie perspectieven ziet: lijst ziet u waarin de werkelijke records Hallo achter Hallo grafieken. Tabel waarin een tabellarische weergave van gegevens van prestatiemeteritems; metrische gegevens en geeft en grafieken voor Hallo prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="23c26-306">hello first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows hello actual records behind hello charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for hello performance counters.</span></span>

<span data-ttu-id="23c26-307">In Hallo afbeelding hierboven zijn er twee sets met velden die zijn gemarkeerd die wijzen op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="23c26-307">In hello image above, there are two sets of fields marked that indicate hello following:</span></span>

* <span data-ttu-id="23c26-308">de eerste set Hallo identificeert naam Windows Prestatiemeter, objectnaam en exemplaarnaam in Hallo queryfilter.</span><span class="sxs-lookup"><span data-stu-id="23c26-308">hello first set identifies Windows Performance Counter Name, Object Name, and Instance Name in hello query filter.</span></span> <span data-ttu-id="23c26-309">Dit zijn Hallo velden die u waarschijnlijk meest worden gebruikt als facetten/filters</span><span class="sxs-lookup"><span data-stu-id="23c26-309">These are hello fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="23c26-310">**Tegenwaarde** Hallo werkelijke waarde van Hallo teller.</span><span class="sxs-lookup"><span data-stu-id="23c26-310">**CounterValue** is hello actual value of hello counter.</span></span> <span data-ttu-id="23c26-311">In dit voorbeeld Hallo-waarde is *75*.</span><span class="sxs-lookup"><span data-stu-id="23c26-311">In this example, hello value is *75*.</span></span>
* <span data-ttu-id="23c26-312">**TimeGenerated** 12:51, in 24-uurs tijdnotatie is.</span><span class="sxs-lookup"><span data-stu-id="23c26-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="23c26-313">Hier volgt een overzicht van Hallo metrische gegevens in een grafiek.</span><span class="sxs-lookup"><span data-stu-id="23c26-313">Here's a view of hello metrics in a graph.</span></span>

![Gem. start zoeken](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="23c26-315">Na het lezen over Hallo Perf record shape en hebben meer informatie over andere zoektechnieken, kunt u meting Avg() tooaggregate gebruiken dit soort numerieke gegevens.</span><span class="sxs-lookup"><span data-stu-id="23c26-315">After reading about hello Perf record shape, and having read about other search techniques, you can use measure Avg() tooaggregate this type of numerical data.</span></span>

<span data-ttu-id="23c26-316">Hier volgt een voorbeeld van een eenvoudige:</span><span class="sxs-lookup"><span data-stu-id="23c26-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![Gem. samplevalue zoeken](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="23c26-318">In dit voorbeeld selecteert u Hallo totale CPU-tijd prestatiemeteritem en gemiddelde per Computer.</span><span class="sxs-lookup"><span data-stu-id="23c26-318">In this example, you select hello CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="23c26-319">Als u wilt dat toonarrow omlaag uw resultaten tooonly Hallo laatste 6 uur, kunt u Hallo tijd filterbesturingselement gebruiken of Geef in de query als volgt:</span><span class="sxs-lookup"><span data-stu-id="23c26-319">If you want toonarrow down your results tooonly hello last 6 hours, you can either use hello time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="23c26-320">met behulp van de functie Avg. Hallo met Hallo meting opdracht toosearch</span><span class="sxs-lookup"><span data-stu-id="23c26-320">toosearch using hello avg function with hello measure command</span></span>
* <span data-ttu-id="23c26-321">Typ in het Hallo-query in het zoekvak `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span><span class="sxs-lookup"><span data-stu-id="23c26-321">In hello Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="23c26-322">U kunt aggregeren en correleren van gegevens *over* computers.</span><span class="sxs-lookup"><span data-stu-id="23c26-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="23c26-323">Stel bijvoorbeeld dat u hebt een set van hosts in een bepaald soort farm waar elk knooppunt is gelijk tooany andere en ze alleen alle Hallo hetzelfde type werk en load moet ongeveer in evenwicht doen.</span><span class="sxs-lookup"><span data-stu-id="23c26-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal tooany other one and they just do all hello same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="23c26-324">U kunt hun items die in een gaan Hello volgende opvragen en gemiddelden ophalen voor de gehele farm Hallo kan ophalen.</span><span class="sxs-lookup"><span data-stu-id="23c26-324">You could get their counters all in one go with hello following query and get averages for hello entire farm.</span></span> <span data-ttu-id="23c26-325">U kunt starten door te kiezen Hallo computers Hello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="23c26-325">You can start by choosing hello computers with hello following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="23c26-326">Nu dat u Hallo computers hebt, wilt u ook alleen tooselect twee prestatie-indicatoren (KPI's): % CPU-gebruik en % vrije schijfruimte.</span><span class="sxs-lookup"><span data-stu-id="23c26-326">Now that you have hello computers, you also only want tooselect two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="23c26-327">Zo, dat deel van het Hallo-query wordt:</span><span class="sxs-lookup"><span data-stu-id="23c26-327">So, that part of hello query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="23c26-328">U kunt nu computers en prestatiemeteritems toevoegen Hello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="23c26-328">Now you can add computers and counters with hello following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="23c26-329">Omdat u een zeer specifieke selectie hebt, Hallo **Avg() meten** opdracht kunt terugkeren Hallo gemiddelde niet door de computer, maar in de farm hello, gewoon door groepering door CounterName.</span><span class="sxs-lookup"><span data-stu-id="23c26-329">Because you have a very specific selection, hello **measure Avg()** command can return hello average not by computer, but across hello farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="23c26-330">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="23c26-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="23c26-331">Hiermee krijgt u een handig compacte weergave van een aantal KPI's voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="23c26-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![groepering van Search Gem.](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="23c26-333">U kunt eenvoudig hello zoekquery gebruiken in een dashboard.</span><span class="sxs-lookup"><span data-stu-id="23c26-333">You can easily use hello search query in a dashboard.</span></span> <span data-ttu-id="23c26-334">U kan bijvoorbeeld Hallo zoekopdracht opslaan en een dashboard maken vanuit deze met de naam *Web Farm KPI's*.</span><span class="sxs-lookup"><span data-stu-id="23c26-334">For example, you could save hello search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="23c26-335">toolearn meer over het gebruik van dashboards, Zie [maken van een aangepast dashboard in logboekanalyse](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="23c26-335">toolearn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![Search-dashboard, Gem.](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a><span data-ttu-id="23c26-337">De functie sum Hallo met Hallo meting opdracht gebruiken</span><span class="sxs-lookup"><span data-stu-id="23c26-337">Use hello sum function with hello measure command</span></span>
<span data-ttu-id="23c26-338">de functie sum Hallo is soortgelijke tooother functies van Hallo meting opdracht.</span><span class="sxs-lookup"><span data-stu-id="23c26-338">hello sum function is similar tooother functions of hello measure command.</span></span> <span data-ttu-id="23c26-339">U ziet een voorbeeld over hoe toouse sum-functie op Hallo [W3C IIS-logboeken zoeken in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="23c26-339">You can see an example about how toouse hello sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="23c26-340">U kunt Max() en zijn met de getallen, datums en tijden en tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="23c26-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="23c26-341">Met tekenreeksen, ze alfabetische volgorde worden gesorteerd en u eerste en laatste.</span><span class="sxs-lookup"><span data-stu-id="23c26-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="23c26-342">U kunt de bladwijzers echter niet gebruiken met iets anders dan numerieke velden.</span><span class="sxs-lookup"><span data-stu-id="23c26-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="23c26-343">Dit geldt ook tooAvg().</span><span class="sxs-lookup"><span data-stu-id="23c26-343">This also applies tooAvg().</span></span>

### <a name="use-hello-percentile-function-with-hello-measure-command"></a><span data-ttu-id="23c26-344">Hallo percentielfunctie met Hallo meting opdracht gebruiken</span><span class="sxs-lookup"><span data-stu-id="23c26-344">Use hello percentile function with hello measure command</span></span>
<span data-ttu-id="23c26-345">Hallo percentielfunctie is vergelijkbaar tooAvg() of bladwijzers in die u het alleen voor numerieke velden gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="23c26-345">hello percentile function is similar tooAvg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="23c26-346">U kunt percentiel tussen 1 too99 op een numeriek veld gebruiken.</span><span class="sxs-lookup"><span data-stu-id="23c26-346">You can use any percentile between 1 too99 on a numeric field.</span></span> <span data-ttu-id="23c26-347">U kunt ook beide **percentiel** en **pct** opdrachten.</span><span class="sxs-lookup"><span data-stu-id="23c26-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="23c26-348">Hier volgen enkele voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="23c26-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a><span data-ttu-id="23c26-349">Hallo gebruiken wanneer de opdracht</span><span class="sxs-lookup"><span data-stu-id="23c26-349">Use hello where command</span></span>
<span data-ttu-id="23c26-350">Hallo waarbij opdracht werkt als een filter, maar deze kan worden toegepast in Hallo pijplijn toofurther filter geaggregeerd resultaten die zijn gemaakt door een opdracht meting – als tegengestelde tooraw resultaten die zijn gefilterd op Hallo begin van een query.</span><span class="sxs-lookup"><span data-stu-id="23c26-350">hello where command works like a filter, but it can be applied in hello pipeline toofurther filter aggregated results that have been produced by a Measure command – as opposed tooraw results that are filtered at hello beginning of a query.</span></span>

<span data-ttu-id="23c26-351">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="23c26-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="23c26-352">U kunt een andere pipe toevoegen ' | ' teken en het Hallo waar opdracht tooonly computers waarvan gemiddelde CPU hoger is dan 80% met krijgen Hallo volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="23c26-352">You can add another pipe "|" character and hello Where command tooonly get computers whose average CPU is above 80%, with hello following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="23c26-353">Als u bekend met de Microsoft System Center - Operations Manager bent, kunt u Hallo zien wanneer de opdracht in termen van management pack.</span><span class="sxs-lookup"><span data-stu-id="23c26-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of hello where command in management pack terms.</span></span> <span data-ttu-id="23c26-354">Als voorbeeld Hallo was van een regel, Hallo eerste deel van de query Hallo worden Hallo gegevensbron en Hallo waar opdracht detectie van conditie voor Hallo zou zijn.</span><span class="sxs-lookup"><span data-stu-id="23c26-354">If hello example were a rule, hello first part of hello query would be hello data source and hello where command would be hello condition detection.</span></span>

<span data-ttu-id="23c26-355">U kunt query hello gebruiken als een tegel in **mijn Dashboard**, als een monitor van sorteerbewerkingen toosee wanneer computer CPU's zijn te veel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="23c26-355">You can use hello query as a tile in **My Dashboard**, as a monitor of sorts, toosee when computer CPUs are over-utilized.</span></span> <span data-ttu-id="23c26-356">toolearn meer informatie over dashboards, Zie [maken van een aangepast dashboard in logboekanalyse](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="23c26-356">toolearn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="23c26-357">U kunt ook maken en dashboards met Hallo mobiele app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="23c26-357">You can also create and use dashboards using hello mobile app.</span></span> <span data-ttu-id="23c26-358">Zie voor meer informatie [OMS mobiele App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span><span class="sxs-lookup"><span data-stu-id="23c26-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="23c26-359">In Hallo onder twee tegels Hallo volgende afbeelding ziet u Hallo monitor een lijst weergegeven en als een getal.</span><span class="sxs-lookup"><span data-stu-id="23c26-359">In hello bottom two tiles of hello following image, you can see hello monitor displayed a list and as a number.</span></span> <span data-ttu-id="23c26-360">In wezen altijd gewenste Hallo nummer toobe nul en Hallo lijst toobe leeg.</span><span class="sxs-lookup"><span data-stu-id="23c26-360">Essentially, you always want hello number toobe zero and hello list toobe empty.</span></span> <span data-ttu-id="23c26-361">Anders geeft een meldingsvoorwaarde aan.</span><span class="sxs-lookup"><span data-stu-id="23c26-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="23c26-362">Indien nodig, kunt u deze tootake kijken welke computers zijn onder druk.</span><span class="sxs-lookup"><span data-stu-id="23c26-362">If needed, you can use it tootake a look at which machines are under pressure.</span></span>

![mobiele dashboard](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a><span data-ttu-id="23c26-364">Hallo gebruiken in de operator</span><span class="sxs-lookup"><span data-stu-id="23c26-364">Use hello in operator</span></span>
<span data-ttu-id="23c26-365">Hallo *IN* -operator, samen met *NOT IN* kunt u toouse subsearches die zoekopdrachten met een andere zoekopdracht als argument.</span><span class="sxs-lookup"><span data-stu-id="23c26-365">hello *IN* operator, along with *NOT IN* allows you toouse subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="23c26-366">Ze zijn opgenomen in de accolades {} binnen een andere *primaire* of *buitenste* zoeken.</span><span class="sxs-lookup"><span data-stu-id="23c26-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="23c26-367">Hallo-resultaat van een subsearch, vaak een lijst met verschillende resultaten, wordt vervolgens gebruikt als argument voor de primaire zoekactie.</span><span class="sxs-lookup"><span data-stu-id="23c26-367">hello result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="23c26-368">U kunt subsearches toomatch subsets van uw gegevens dat u een beschrijving kan niet rechtstreeks in een zoekexpressie, maar die kunnen worden gegenereerd vanuit een zoekopdracht kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="23c26-368">You can use subsearches toomatch subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="23c26-369">Bijvoorbeeld, als u geïnteresseerd bent in het gebruik van een zoekopdracht toofind alle gebeurtenissen uit *computers met ontbrekende beveiligingsupdates*, moet u een subsearch die eerst dat identificeert toodesign *computers met ontbrekende beveiligingsupdates*  voordat er gebeurtenissen behoren toothose hosts.</span><span class="sxs-lookup"><span data-stu-id="23c26-369">For example, if you’re interested in using one search toofind all events from *computers missing security updates*, then you need toodesign a subsearch that first identifies that *computers missing security updates* before it finds events belonging toothose hosts.</span></span>

<span data-ttu-id="23c26-370">Ja, u kan express *computers momenteel ontbreekt vereiste beveiligingsupdates* Hello query te volgen:</span><span class="sxs-lookup"><span data-stu-id="23c26-370">So, you could express *computers currently missing required security updates* with hello following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![IN voorbeeld zoeken](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="23c26-372">Zodra u Hallo lijst hebt, kunt u Hallo zoeken als een binnenste zoeken toofeed Hallo lijst van computers in een buitenste (primaire) zoeken die wordt gezocht naar gebeurtenissen voor deze computers.</span><span class="sxs-lookup"><span data-stu-id="23c26-372">Once you have hello list, you can use hello search as an inner search toofeed hello list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="23c26-373">U doen dit door Hallo binnenste zoeken insluitende accolades en de resultaten als mogelijke waarden voor een filterveld in buitenste Hallo-search met behulp van de IN-operator Hallo voeding.</span><span class="sxs-lookup"><span data-stu-id="23c26-373">You do this by enclosing hello inner search in braces and feeding its results as possible values for a filter/field in hello outer search using hello IN operator.</span></span> <span data-ttu-id="23c26-374">Hallo query zou zijn vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="23c26-374">hello query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![IN voorbeeld zoeken](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="23c26-376">Kennisgeving Hallo tijd filter dat wordt gebruikt in de interne zoekopdracht Hallo omdat Hallo System Update-evaluatie maakt een momentopname van alle computers ook elke 24 uur.</span><span class="sxs-lookup"><span data-stu-id="23c26-376">Also notice hello time filter used in hello inner search because hello System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="23c26-377">U maken Hallo binnenste query meer licht en nauwkeurige, zoekt alleen naar een dag.</span><span class="sxs-lookup"><span data-stu-id="23c26-377">You can make hello inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="23c26-378">Hallo buitenste zoeken in plaats daarvan maakt gebruik van Tijdselectie Hallo Hallo-gebruikersinterface, ophalen van gebeurtenissen van Hallo afgelopen 7 dagen.</span><span class="sxs-lookup"><span data-stu-id="23c26-378">hello outer search instead uses hello time selection in hello user interface, retrieving events from hello last 7 days.</span></span> <span data-ttu-id="23c26-379">Zie [Booleaanse operators](#boolean-operators) voor meer informatie over tijd operators.</span><span class="sxs-lookup"><span data-stu-id="23c26-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="23c26-380">Omdat u echt alleen gebruik Hallo resultaten van de binnenste zoekopdracht Hallo als de filterwaarde van een voor een outer Hallo, kunt u opdrachten in een buitenste zoeken Hallo nog steeds toepassen.</span><span class="sxs-lookup"><span data-stu-id="23c26-380">Because you really only use hello results of hello inner search as a filter value for hello outer one, you can still apply commands in hello outer search.</span></span> <span data-ttu-id="23c26-381">U kunt bijvoorbeeld nog steeds groep Hallo hierboven gebeurtenissen met een andere meting-opdracht:</span><span class="sxs-lookup"><span data-stu-id="23c26-381">For example, you can still group hello above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![IN voorbeeld zoeken](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="23c26-383">In het algemeen wilt u dat uw interne query tooexecute snel omdat logboekanalyse aan servicezijde time-outs voor het en ook tooreturn een kleine hoeveelheid resultaten heeft.</span><span class="sxs-lookup"><span data-stu-id="23c26-383">Generally, you want your inner query tooexecute quickly because Log Analytics has service-side timeouts for it and also tooreturn a small amount of results.</span></span> <span data-ttu-id="23c26-384">Als interne query Hallo meer resultaten oplevert, Hallo resultatenlijst afgekapt, die kan veroorzaken Hallo buitenste zoeken tooreturn onjuiste resultaten.</span><span class="sxs-lookup"><span data-stu-id="23c26-384">If hello inner query returns more results, hello result list gets truncated, which could potentially cause hello outer search tooreturn incorrect results.</span></span>

<span data-ttu-id="23c26-385">Een andere regel is die Hallo binnenste zoekopdracht moet momenteel tooprovide *geaggregeerde* resultaten.</span><span class="sxs-lookup"><span data-stu-id="23c26-385">Another rule is that hello inner search currently needs tooprovide *aggregated* results.</span></span> <span data-ttu-id="23c26-386">Met andere woorden, deze moet bevatten een *meting* opdracht; u kan niet op dit moment onbewerkte resultaten in een buitenste zoekopdracht feed.</span><span class="sxs-lookup"><span data-stu-id="23c26-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="23c26-387">Ook kan er slechts één IN-operator en het laatste filter Hallo in Hallo-query moet worden.</span><span class="sxs-lookup"><span data-stu-id="23c26-387">Also, there can be only one IN operator and it must be hello last filter in hello query.</span></span> <span data-ttu-id="23c26-388">Meerdere IN operators kunnen niet worden of zou – hierdoor in principe kan meerdere subsearches uitgevoerd: Hallo belangrijk punt wordt die slechts één sub/interne zoekopdracht is mogelijk dat elke buitenste zoeken.</span><span class="sxs-lookup"><span data-stu-id="23c26-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: hello important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="23c26-389">Zelfs met deze limieten IN kunnen veel soorten gecorreleerde zoekopdrachten en kunt u toodefine iets dergelijks toogroups zoals computers, gebruikers of bestanden – ongeacht Hallo velden in uw gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="23c26-389">Even with these limits, IN enables many kinds of correlated searches, and allows you toodefine something similar toogroups such as computers, users, or files – whatever hello fields in your data contain.</span></span> <span data-ttu-id="23c26-390">Hier vindt u meer voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="23c26-390">Here are more examples:</span></span>

<span data-ttu-id="23c26-391">**Alle updates ontbreken van computers waarop automatische updates-instelling wordt uitgeschakeld**</span><span class="sxs-lookup"><span data-stu-id="23c26-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="23c26-392">**Alle foutgebeurtenissen van computers met SQL Server (= waar SQL-analyse is uitgevoerd)**</span><span class="sxs-lookup"><span data-stu-id="23c26-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="23c26-393">**Alle beveiligingsgebeurtenissen van computers die domeincontrollers (= waar AD analyse is uitgevoerd)**</span><span class="sxs-lookup"><span data-stu-id="23c26-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="23c26-394">**Die andere accounts zich aangemeld hebben toohello dezelfde computers waarbij BACONLAND\jochan account heeft aangemeld?**</span><span class="sxs-lookup"><span data-stu-id="23c26-394">**Which other accounts have logged on toohello same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a><span data-ttu-id="23c26-395">Gebruik afzonderlijke opdracht Hallo</span><span class="sxs-lookup"><span data-stu-id="23c26-395">Use hello distinct command</span></span>
<span data-ttu-id="23c26-396">Als de naam van de Hallo wordt voorgesteld, biedt deze opdracht een lijst met verschillende waarden voor een veld.</span><span class="sxs-lookup"><span data-stu-id="23c26-396">As hello name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="23c26-397">Het is verrassend eenvoudige maar wel handig.</span><span class="sxs-lookup"><span data-stu-id="23c26-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="23c26-398">Hallo die dezelfde kan worden verkregen met meting count() opdracht ook, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="23c26-398">hello same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![Voorbeeld van de opdracht DISTINCT zoeken](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="23c26-400">Als u geïnteresseerd bent in een lijst van de afzonderlijke waarden en niet Hallo aantal documenten waarvoor die waarden, kan vervolgens DISTINCT evenwel schonere en gemakkelijker tooread uitvoer en kortere syntaxis, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="23c26-400">However, if all you're interested in is just a list of distinct values and not hello count of documents that have that values, then DISTINCT can provide cleaner and easier tooread output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![Voorbeeld van de opdracht DISTINCT zoeken](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a><span data-ttu-id="23c26-402">Hallo countdistinct functie gebruiken met Hallo meting opdracht</span><span class="sxs-lookup"><span data-stu-id="23c26-402">Use hello countdistinct function with hello measure command</span></span>
<span data-ttu-id="23c26-403">Hallo countdistinct functie telt Hallo aantal afzonderlijke waarden in elke groep.</span><span class="sxs-lookup"><span data-stu-id="23c26-403">hello countdistinct function counts hello number of distinct values within each group.</span></span> <span data-ttu-id="23c26-404">Het kan bijvoorbeeld worden gebruikt toocount Hallo aantal unieke computers melden voor elk Type:</span><span class="sxs-lookup"><span data-stu-id="23c26-404">For example, it could be used toocount hello number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a><span data-ttu-id="23c26-406">Hallo meting interval opdracht gebruiken</span><span class="sxs-lookup"><span data-stu-id="23c26-406">Use hello measure interval command</span></span>
<span data-ttu-id="23c26-407">Met bijna Realtime prestatiegegevens verzamelen, kunt u verzamelen en visualiseren van elk prestatiemeteritem in logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="23c26-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="23c26-408">Gewoon invoeren Hallo query **Type: Perf** duizenden metrische grafieken op basis van Hallo aantal items en servers in uw omgeving Log Analytics wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="23c26-408">Simply entering hello query **Type:Perf** will return thousands of metric graphs based on hello number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="23c26-409">Met metrische aggregatie op aanvraag, kunt u bekijken op Hallo algemene metrische gegevens in uw omgeving op een hoog niveau en diepgaand naar meer gedetailleerde gegevens als nodig is voor.</span><span class="sxs-lookup"><span data-stu-id="23c26-409">With on-demand metric aggregation, you can look at hello overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="23c26-410">Stel dat u wilt dat tooknow wat Hallo gemiddelde CPU is voor alle computers.</span><span class="sxs-lookup"><span data-stu-id="23c26-410">Let’s say that you want tooknow what is hello average CPU across all your computers.</span></span> <span data-ttu-id="23c26-411">Bekijkt hello gemiddelde CPU voor elke computer mogelijk niet meer nuttig zijn omdat resultaten kunnen ophalen vloeiend moeten worden gemaakt. toolook naar meer informatie, u kunt samenvoegen in uw resultaat in een kleinere tijd venster segmenten gedownload en zoek een tijdreeks over verschillende dimensies.</span><span class="sxs-lookup"><span data-stu-id="23c26-411">Looking at hello average CPU for every computer might not be helpful because results may get smoothed out. toolook into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="23c26-412">Bijvoorbeeld, kunt u uitvoeren Hallo per uur gemiddelde CPU-gebruik op alle computers als volgt:</span><span class="sxs-lookup"><span data-stu-id="23c26-412">For example, you can perform hello hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![gemiddelde interval meting](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="23c26-414">Standaard worden deze resultaten worden weergegeven in een lijndiagram met meerdere reeksen interactieve.</span><span class="sxs-lookup"><span data-stu-id="23c26-414">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="23c26-415">Dit diagram ondersteunt reeks schakelen (met y-as schaling aanpassen), zoomen en aanwijzen.</span><span class="sxs-lookup"><span data-stu-id="23c26-415">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="23c26-416">Hallo weergave tabeloptie nog steeds beschikbaar voor het weergeven van Hallo onbewerkte gegevens, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="23c26-416">hello table display option is still available for viewing hello raw data if necessary.</span></span>

<span data-ttu-id="23c26-417">U kunt ook andere velden groeperen.</span><span class="sxs-lookup"><span data-stu-id="23c26-417">You can also group by other fields.</span></span> <span data-ttu-id="23c26-418">In dit voorbeeld ik zoek alle Hallo % prestatiemeteritems voor een specifieke computer en tooknow wat is er elk uur 70 percentielen Hallo van elke teller wilt:</span><span class="sxs-lookup"><span data-stu-id="23c26-418">In this example, I am looking at all hello % counters for one specific computer, and I want tooknow what is hello hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="23c26-419">Een ding toonote is deze query's zijn niet beperkt tooperformance tellers.</span><span class="sxs-lookup"><span data-stu-id="23c26-419">One thing toonote is that these queries are not limited tooperformance counters.</span></span> <span data-ttu-id="23c26-420">U kunt deze toepassen tooany metriek.</span><span class="sxs-lookup"><span data-stu-id="23c26-420">You can apply them tooany metric.</span></span> <span data-ttu-id="23c26-421">In dit voorbeeld zoek ik op de W3C-IIS-logboeken.</span><span class="sxs-lookup"><span data-stu-id="23c26-421">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="23c26-422">Ik wil tooknow wat Hallo maximale tijd die nodig is tijdens een interval van 5 minuten voor het verwerken van elke aanvraag is:</span><span class="sxs-lookup"><span data-stu-id="23c26-422">I want tooknow what is hello maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="23c26-423">Gebruik van meerdere statistische functies in één query</span><span class="sxs-lookup"><span data-stu-id="23c26-423">Use multiple aggregates in one query</span></span>
<span data-ttu-id="23c26-424">U kunt meerdere cumulatieve componenten opgeven in de opdracht van een meting.</span><span class="sxs-lookup"><span data-stu-id="23c26-424">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="23c26-425">Elk criterium kan alias onafhankelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="23c26-425">Each one can be aliased independently.</span></span>  <span data-ttu-id="23c26-426">Als er geen een alias Hallo resulterende opgegeven is veldnaam zich Hallo statistische functie die is gebruikt (dat wil zeggen ' avg(CounterValue)' voor avg(CounterValue)).</span><span class="sxs-lookup"><span data-stu-id="23c26-426">If it is not given an alias hello resulting field name will be hello aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="23c26-428">Hier volgt nog een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="23c26-428">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="23c26-429">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="23c26-429">Next steps</span></span>
<span data-ttu-id="23c26-430">Zie voor meer informatie over logboek zoekopdrachten:</span><span class="sxs-lookup"><span data-stu-id="23c26-430">For additional information about log searches, see:</span></span>

* <span data-ttu-id="23c26-431">Gebruik [aangepaste velden in logboekanalyse](log-analytics-custom-fields.md) tooextend logboek zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="23c26-431">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) tooextend log searches.</span></span>
* <span data-ttu-id="23c26-432">Bekijk Hallo [logboekanalyse Meld zoeken verwijzing](log-analytics-search-reference.md) tooview alle Hallo velden en beschikbaar zijn in logboekanalyse facetten zoeken.</span><span class="sxs-lookup"><span data-stu-id="23c26-432">Review hello [Log Analytics log search reference](log-analytics-search-reference.md) tooview all of hello search fields and facets available in Log Analytics.</span></span>
