---
title: aaaUsing hello logboek zoeken portal in Azure Log Analytics | Microsoft Docs
description: Dit artikel bevat een zelfstudie waarin wordt beschreven hoe toocreate Meld u zoekopdrachten en analyseren van gegevens die zijn opgeslagen in de werkruimte voor logboekanalyse met Hallo logboek zoeken portal.  Hallo-zelfstudie bevat enkele eenvoudige query's uitgevoerd tooreturn verschillende soorten gegevens en analyseren van resultaten.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a><span data-ttu-id="f358e-104">Logboek zoekacties in de Azure-logboekanalyse met Hallo logboek zoeken portal maken</span><span class="sxs-lookup"><span data-stu-id="f358e-104">Create log searches in Azure Log Analytics using hello Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="f358e-105">Dit artikel wordt beschreven in Azure-logboekanalyse met behulp van de nieuwe querytaal Hallo Hallo logboek zoeken-portal.</span><span class="sxs-lookup"><span data-stu-id="f358e-105">This article describes hello Log Search portal in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="f358e-106">U kunt meer informatie over de nieuwe taal Hallo en uw werkruimte op Hallo procedure tooupgrade ophalen [Upgrade van uw Azure-logboekanalyse werkruimte toonew logboek zoekopdracht](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="f358e-106">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="f358e-107">Als uw werkruimte niet bijgewerkte toohello nieuwe querytaal is, raadpleegt u te[vinden van gegevens met behulp van logboek zoekopdrachten in logboekanalyse](log-analytics-log-searches.md) voor meer informatie over de huidige versie Hallo van Hallo logboek zoeken portal.</span><span class="sxs-lookup"><span data-stu-id="f358e-107">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on hello current version of hello Log Search portal.</span></span>

<span data-ttu-id="f358e-108">Dit artikel bevat een zelfstudie waarin wordt beschreven hoe toocreate Meld u zoekopdrachten en analyseren van gegevens die zijn opgeslagen in de werkruimte voor logboekanalyse met Hallo logboek zoeken portal.</span><span class="sxs-lookup"><span data-stu-id="f358e-108">This article includes a tutorial that describes how toocreate log searches and analyze data stored in your Log Analytics workspace using hello Log Search portal.</span></span>  <span data-ttu-id="f358e-109">Hallo-zelfstudie bevat enkele eenvoudige query's uitgevoerd tooreturn verschillende soorten gegevens en analyseren van resultaten.</span><span class="sxs-lookup"><span data-stu-id="f358e-109">hello tutorial includes running some simple queries tooreturn different types of data and analyzing results.</span></span>  <span data-ttu-id="f358e-110">Dit artikel gaat over functies in Hallo logboek zoeken portal voor Hallo query te wijzigen in plaats van rechtstreeks wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f358e-110">It focuses on features in hello Log Search portal for modifying hello query rather than modifying it directly.</span></span>  <span data-ttu-id="f358e-111">Zie voor informatie over het Hallo-query rechtstreeks te bewerken, Hallo [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="f358e-111">For details on directly editing hello query, see hello [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="f358e-112">toocreate zoekopdrachten in Hallo Advanced Analytics-portal in plaats van Hallo logboek zoeken portal, Zie [aan de slag met Hallo Analytics-Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span><span class="sxs-lookup"><span data-stu-id="f358e-112">toocreate searches in hello Advanced Analytics portal instead of hello Log Search portal, see [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="f358e-113">Beide portals hello gebruiken dezelfde query language tooaccess dezelfde gegevens in de werkruimte voor logboekanalyse Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f358e-113">Both portals use hello same query language tooaccess hello same data in hello Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f358e-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f358e-114">Prerequisites</span></span>
<span data-ttu-id="f358e-115">Deze zelfstudie wordt ervan uitgegaan dat u hebt al een werkruimte voor logboekanalyse met ten minste één verbonden bron die gegevens voor Hallo query's tooanalyze genereert.</span><span class="sxs-lookup"><span data-stu-id="f358e-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for hello queries tooanalyze.</span></span>  

- <span data-ttu-id="f358e-116">Als u een werkruimte geen hebt, kunt u een gratis account maken met behulp van de procedure Hallo op [aan de slag met een werkruimte voor logboekanalyse](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f358e-116">If you don't have a workspace, you can create a free one using hello procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="f358e-117">Verbinding maken met ten minste één [Windows-agent](log-analytics-windows-agents.md) of één [Linux-agent](log-analytics-linux-agents.md) toohello werkruimte.</span><span class="sxs-lookup"><span data-stu-id="f358e-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) toohello workspace.</span></span>  

## <a name="open-hello-log-search-portal"></a><span data-ttu-id="f358e-118">Open Hallo logboek zoeken portal</span><span class="sxs-lookup"><span data-stu-id="f358e-118">Open hello Log Search portal</span></span>
<span data-ttu-id="f358e-119">Starten door het Hallo logboek zoeken portal te openen.</span><span class="sxs-lookup"><span data-stu-id="f358e-119">Start by opening hello Log Search portal.</span></span>  <span data-ttu-id="f358e-120">U kunt openen in hello Azure-portal of Hallo OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="f358e-120">You can access it in either hello Azure portal or hello OMS portal.</span></span>

1. <span data-ttu-id="f358e-121">Open hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f358e-121">Open hello Azure portal.</span></span>
2. <span data-ttu-id="f358e-122">Navigeer tooLog Analytics en selecteer uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="f358e-122">Navigate tooLog Analytics and select your workspace.</span></span>
3. <span data-ttu-id="f358e-123">Selecteer **logboek zoeken** toostay in Azure portal of starten Hallo OMS-portal door te selecteren Hallo **OMS-Portal** Hallo logboek zoekknop te klikken.</span><span class="sxs-lookup"><span data-stu-id="f358e-123">Either select **Log Search** toostay in hello Azure portal or launch hello OMS portal by selecting **OMS Portal** and then clicking hello Log Search button.</span></span>

![Meld u knop Zoeken](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="f358e-125">Maken van een eenvoudige zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="f358e-125">Create a simple search</span></span>
<span data-ttu-id="f358e-126">de snelste manier tooretrieve Hallo sommige gegevens toowork met is een eenvoudige query waarin alle records in de tabel retourneert.</span><span class="sxs-lookup"><span data-stu-id="f358e-126">hello quickest way tooretrieve some data toowork with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="f358e-127">Als u een Windows- of Linux-clients verbonden tooyour werkruimte hebt, hebt u gegevens in ofwel Hallo gebeurtenis (Windows) of Syslog (Linux) tabel.</span><span class="sxs-lookup"><span data-stu-id="f358e-127">If you have any Windows or Linux clients connected tooyour workspace, then you'll have data in either hello Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="f358e-128">Typ een Hallo query's in het zoekvak hello te volgen en klik op Hallo zoeken.</span><span class="sxs-lookup"><span data-stu-id="f358e-128">Type one hello following queries in hello search box and click hello search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="f358e-129">Gegevens worden geretourneerd in de lijst Standaardweergave Hallo en kunt u zien hoeveel totale records geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="f358e-129">Data is returned in hello default list view, and you can see how many total records were returned.</span></span>

![Eenvoudige query](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="f358e-131">Alleen hello eerste enkele eigenschappen van elke record worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f358e-131">Only hello first few properties of each record are displayed.</span></span>  <span data-ttu-id="f358e-132">Klik op **meer** toodisplay alle eigenschappen voor een bepaalde record.</span><span class="sxs-lookup"><span data-stu-id="f358e-132">Click **show more** toodisplay all properties for a particular record.</span></span>

![Details van de records](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a><span data-ttu-id="f358e-134">Hallo tijd bereik instellen</span><span class="sxs-lookup"><span data-stu-id="f358e-134">Set hello time scope</span></span>
<span data-ttu-id="f358e-135">Elke record die is verzameld door Log Analytics is een **TimeGenerated** eigenschap met de Hallo datum en tijd die Hallo-record is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f358e-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains hello date and time that hello record was created.</span></span>  <span data-ttu-id="f358e-136">Een query in Hallo logboek zoeken portal retourneert alleen records met een **TimeGenerated** binnen Hallo tijd bereik dat wordt weergegeven op Hallo linkerkant van het welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="f358e-136">A query in hello Log Search portal only returns records with a **TimeGenerated** within hello time scope that's displayed on hello left side of hello screen.</span></span>  

<span data-ttu-id="f358e-137">U kunt Hallo tijdfilter wijzigen door het Hallo vervolgkeuzelijst selecteren of door het wijzigen van de schuifregelaar Hallo.</span><span class="sxs-lookup"><span data-stu-id="f358e-137">You can change hello time filter either by selecting hello dropdown or by modifying hello slider.</span></span>  <span data-ttu-id="f358e-138">Hallo schuifregelaar wordt een staafdiagram waarin de relatieve aantal records voor elk segment tijd binnen het bereik van Hallo Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f358e-138">hello slider displays a bar graph that shows hello relative number of records for each time segment within hello range.</span></span>  <span data-ttu-id="f358e-139">Hallo-bereik is afhankelijk van dit segment.</span><span class="sxs-lookup"><span data-stu-id="f358e-139">This segment will vary depending on hello range.</span></span>

<span data-ttu-id="f358e-140">Hallo tijd standaardbereik is **1 dag**.</span><span class="sxs-lookup"><span data-stu-id="f358e-140">hello default time scope is **1 day**.</span></span>  <span data-ttu-id="f358e-141">Deze waarde te wijzigen**7 dagen**, en het totale aantal records Hallo moet verhogen.</span><span class="sxs-lookup"><span data-stu-id="f358e-141">Change this value too**7 days**, and hello total number of records should increase.</span></span>

![Datum tijd bereik](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a><span data-ttu-id="f358e-143">Resultaten van Hallo query filteren</span><span class="sxs-lookup"><span data-stu-id="f358e-143">Filter results of hello query</span></span>
<span data-ttu-id="f358e-144">Op Hallo is links in het welkomstscherm Hallo filterdeelvenster waarmee u tooadd toohello query filteren zonder te rechtstreeks wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f358e-144">On hello left side of hello screen is hello filter pane which allows you tooadd filtering toohello query without modifying it directly.</span></span>  <span data-ttu-id="f358e-145">Verschillende eigenschappen van Hallo records geretourneerd worden met de top tien waarden met hun aantal records weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f358e-145">Several properties of hello records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="f358e-146">Als u met werkt **gebeurtenis**, selecteer Hallo selectievakje in naast te**fout** onder **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="f358e-146">If you're working with **Event**, select hello checkbox next too**Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="f358e-147">Als u met werkt **Syslog**, selecteer Hallo selectievakje in naast te**err** onder **FOUTCODE**.</span><span class="sxs-lookup"><span data-stu-id="f358e-147">If you're working with **Syslog**, select hello checkbox next too**err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="f358e-148">Hiermee wijzigt u Hallo query tooone na toolimit Hallo Hallo resulteert tooerror gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="f358e-148">This changes hello query tooone of hello following toolimit hello results tooerror events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filteren](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="f358e-150">Add eigenschappen toohello filterdeelvenster door te selecteren **toofilters toevoegen** in Hallo eigenschap menu op een van de Hallo records.</span><span class="sxs-lookup"><span data-stu-id="f358e-150">Add properties toohello filter pane by selecting **Add toofilters** from hello property menu on one of hello records.</span></span>

![Toofilter menu toevoegen](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="f358e-152">U kunt instellen Hallo dezelfde door te selecteren filteren **Filter** van Hallo eigenschap menu naar een record met Hallo-waarde die u wilt toofilter.</span><span class="sxs-lookup"><span data-stu-id="f358e-152">You can set hello same filter by selecting **Filter** from hello property menu for a record with hello value you want toofilter.</span></span>  

<span data-ttu-id="f358e-153">U hoeft alleen Hallo **Filter** optie voor eigenschappen met de naam in blauw.</span><span class="sxs-lookup"><span data-stu-id="f358e-153">You only have hello **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="f358e-154">Dit zijn *doorzoekbare* velden die zijn geïndexeerd voor voorwaarden zoeken.</span><span class="sxs-lookup"><span data-stu-id="f358e-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="f358e-155">Velden grijs zijn *vrije tekst doorzoekbare* velden waarvoor alleen Hallo **verwijzingen** optie.</span><span class="sxs-lookup"><span data-stu-id="f358e-155">Fields in grey are *free text searchable* fields which only have hello **Show references** option.</span></span>  <span data-ttu-id="f358e-156">Deze optie retourneert records die deze waarde in een eigenschap.</span><span class="sxs-lookup"><span data-stu-id="f358e-156">This option returns records that have that value in any property.</span></span>

![Filtermenu](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="f358e-158">U kunt Hallo resultaten op één eigenschap groeperen op Hallo selecteren **groeperen op** optie in het menu Hallo-record.</span><span class="sxs-lookup"><span data-stu-id="f358e-158">You can group hello results on a single property by selecting hello **Group by** option in hello record menu.</span></span>  <span data-ttu-id="f358e-159">Hiermee voegt u toe een [samenvatten](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour query die Hallo resultaten in een grafiek weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f358e-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour query that displays hello results in a chart.</span></span>  <span data-ttu-id="f358e-160">U kunt groeperen op meer dan één eigenschap, maar moet u tooedit Hallo query rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="f358e-160">You can group on more than one property, but you would need tooedit hello query directly.</span></span>  <span data-ttu-id="f358e-161">Selecteer Hallo record menu volgende Hallo Hallo **Computer** eigenschap en selecteer **groeperen op 'Computer'**.</span><span class="sxs-lookup"><span data-stu-id="f358e-161">Select hello record menu next hello hello **Computer** property and select **Group by 'Computer'**.</span></span>  

![Groeperen op computer](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="f358e-163">Werken met resultaten</span><span class="sxs-lookup"><span data-stu-id="f358e-163">Work with results</span></span>
<span data-ttu-id="f358e-164">Hallo logboek zoeken portal heeft een aantal functies voor het werken met Hallo resultaten van een query.</span><span class="sxs-lookup"><span data-stu-id="f358e-164">hello Log Search portal has a variety of features for working with hello results of a query.</span></span>  <span data-ttu-id="f358e-165">U kunt sorteren en filteren en groeperen resulteert tooanalyze Hallo gegevens zonder Hallo werkelijke query te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f358e-165">You can sort, filter, and group results tooanalyze hello data without modifying hello actual query.</span></span>  <span data-ttu-id="f358e-166">Resultaten van een query worden niet standaard gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="f358e-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="f358e-167">tooview hello gegevens in tabelvorm, wat zorgt voor extra opties voor filteren en sorteren, klikt u op **tabel**.</span><span class="sxs-lookup"><span data-stu-id="f358e-167">tooview hello data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Tabelweergave](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="f358e-169">Klik op Hallo pijl door een record tooview Hallo details voor deze record.</span><span class="sxs-lookup"><span data-stu-id="f358e-169">Click hello arrow by a record tooview hello details for that record.</span></span>

![Resultaten sorteren](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="f358e-171">Sorteren op elk veld door te klikken op de kolomkop.</span><span class="sxs-lookup"><span data-stu-id="f358e-171">Sort on any field by clicking on its column header.</span></span>

![Resultaten sorteren](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="f358e-173">Hallo resultaten op een specifieke waarde in kolom Hallo door te klikken op de knop filteren Hallo en het leveren van een filtervoorwaarde filteren.</span><span class="sxs-lookup"><span data-stu-id="f358e-173">Filter hello results on a specific value in hello column by clicking hello filter button and providing a filter condition.</span></span>

![Resultaten filteren](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="f358e-175">Groeperen op een kolom door de kolom header toohello bovenaan Hallo resultaten te slepen.</span><span class="sxs-lookup"><span data-stu-id="f358e-175">Group on a column by dragging its column header toohello top of hello results.</span></span>  <span data-ttu-id="f358e-176">U kunt meerdere velden groeperen door meerdere kolommen toohello boven te slepen.</span><span class="sxs-lookup"><span data-stu-id="f358e-176">You can group on multiple fields by dragging multiple columns toohello top.</span></span>

![Resultaten van Groepsbeleid](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="f358e-178">Werken met prestatiegegevens</span><span class="sxs-lookup"><span data-stu-id="f358e-178">Work with performance data</span></span>
<span data-ttu-id="f358e-179">Prestatiegegevens voor Windows- en Linux-agents wordt opgeslagen in de werkruimte voor logboekanalyse Hallo maken in Hallo **Perf** tabel.</span><span class="sxs-lookup"><span data-stu-id="f358e-179">Performance data for both Windows and Linux agents is stored in hello Log Analytics workspace in hello **Perf** table.</span></span>  <span data-ttu-id="f358e-180">Prestatiegegevens net als elke andere record zoeken en we een eenvoudige query waarin retourneert dat alle records van de prestaties op dezelfde manier als met gebeurtenissen kunt schrijven.</span><span class="sxs-lookup"><span data-stu-id="f358e-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Prestatiegegevens](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="f358e-182">Hoewel miljoenen records voor alle prestatieobjecten en prestatiemeteritems retourneren is niet erg nuttig.</span><span class="sxs-lookup"><span data-stu-id="f358e-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="f358e-183">Query uitvoeren op dezelfde methoden die u gebruikte boven toofilter Hallo gegevens of alleen typt u de volgende Hallo Hallo kunt u rechtstreeks in het zoekvak Hallo-logboek.</span><span class="sxs-lookup"><span data-stu-id="f358e-183">You can use hello same methods you used above toofilter hello data or just type hello following query directly into hello log search box.</span></span>  <span data-ttu-id="f358e-184">Hiermee wordt alleen processor gebruik records voor zowel Windows- en Linux-computers.</span><span class="sxs-lookup"><span data-stu-id="f358e-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Processorgebruik](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="f358e-186">Dit beperkt Hallo gegevens tooa bepaald item, maar deze nog niet plaatsen in een formulier dat is bijzonder nuttig.</span><span class="sxs-lookup"><span data-stu-id="f358e-186">This limits hello data tooa particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="f358e-187">U kunt Hallo gegevens weergeven in een lijndiagram, maar moet u eerst de toogroup door de Computer en TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="f358e-187">You can display hello data in a line chart, but first need toogroup it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="f358e-188">toogroup op meerdere velden, moet u toomodify Hallo query rechtstreeks Hallo query toohello volgende zodanig te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f358e-188">toogroup on multiple fields, you need toomodify hello query directly, so modify hello query toohello following.</span></span>  <span data-ttu-id="f358e-189">Dit maakt gebruik van Hallo [Gem](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) functie op Hallo **tegenwaarde** eigenschap toocalculate Hallo gemiddelde waarde over elk uur.</span><span class="sxs-lookup"><span data-stu-id="f358e-189">This uses hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on hello **CounterValue** property toocalculate hello average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Prestaties van een grafiek gegevensbron](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="f358e-191">Nu dat Hallo gegevens worden naar behoren gegroepeerd, kunt u deze weergeven in een grafiek visual door toe te voegen Hallo [renderen](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span><span class="sxs-lookup"><span data-stu-id="f358e-191">Now that hello data is suitably grouped, you can display it in a visual chart by adding hello [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Lijndiagram](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="f358e-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f358e-193">Next steps</span></span>

- <span data-ttu-id="f358e-194">Meer informatie over Hallo Log Analytics-querytaal op [aan de slag met Hallo Analytics-Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="f358e-194">Learn more about hello Log Analytics query language at [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="f358e-195">Een zelfstudie met Hallo doorlopen [Advanced Analytics-portal](https://go.microsoft.com/fwlink/?linkid=856587) waarmee u toorun Hallo dezelfde query's en toegang tot dezelfde gegevens als Hallo logboek zoeken portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="f358e-195">Walk through a tutorial using hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you toorun hello same queries and access hello same data as hello Log Search portal.</span></span>
