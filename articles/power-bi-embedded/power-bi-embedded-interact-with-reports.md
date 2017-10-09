---
title: aaaInteract met rapporten die met behulp van Hallo JavaScript-API | Microsoft Docs
description: Power BI Embedded, communiceren met de rapporten met behulp van Hallo JavaScript-API
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a><span data-ttu-id="04ddf-103">Interactie met Power BI-rapporten met Hallo JavaScript-API</span><span class="sxs-lookup"><span data-stu-id="04ddf-103">Interact with Power BI reports using hello JavaScript API</span></span>
<span data-ttu-id="04ddf-104">Hallo Power BI JavaScript API waarmee inventarisaties tooeasily u Power BI-rapporten insluiten in uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="04ddf-104">hello Power BI JavaScript API enables you tooeasily embed Power BI reports into your applications.</span></span> <span data-ttu-id="04ddf-105">Uw toepassingen kunnen programmatisch met Hallo API communiceren met andere rapportelementen zoals pagina's en filters.</span><span class="sxs-lookup"><span data-stu-id="04ddf-105">With hello API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="04ddf-106">Door deze interactiviteit zijn Power BI-rapporten een meer geïntegreerd onderdeel van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="04ddf-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="04ddf-107">U kunt een Power BI-rapport insluiten in uw toepassing met behulp van een iframe die wordt gehost als onderdeel van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="04ddf-107">You embed a Power BI report in your application by using an iframe that is hosted as part of hello application.</span></span> <span data-ttu-id="04ddf-108">Hallo iframe fungeert als een grens tussen de toepassing en het Hallo-rapport, zoals u ziet in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="04ddf-108">hello iframe acts as a boundary between your application and hello report, as you can see in hello following image.</span></span> 

![Ingesloten Power BI-iframe zonder Javascript-API](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="04ddf-110">Hallo iframe Hallo insluiten van het proces is veel eenvoudiger maakt, maar zonder Hallo JavaScript API Hallo rapport en uw toepassing kunnen niet communiceren met elkaar.</span><span class="sxs-lookup"><span data-stu-id="04ddf-110">hello iframe makes hello embedding process a lot easier, but without hello JavaScript API hello report and your application can't interact with each other.</span></span> <span data-ttu-id="04ddf-111">Dit gebrek aan interactie kunt u vindt dat Hallo rapport niet echt onderdeel van de toepassing hello is.</span><span class="sxs-lookup"><span data-stu-id="04ddf-111">This lack of interaction can make it feel like hello report is not really part of hello application.</span></span> <span data-ttu-id="04ddf-112">Hallo-rapport en de toepassing echt nodig toocommunicate heen en weer in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="04ddf-112">hello report and application really need toocommunicate back and forth, as in hello following image.</span></span>

![Ingesloten Power BI-iframe met Javascript-API](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="04ddf-114">Hallo Power BI JavaScript-API kunt u toowrite-code die Hallo iframe grens veilig kunt doorgeven.</span><span class="sxs-lookup"><span data-stu-id="04ddf-114">hello Power BI JavaScript API enables you toowrite code that can securely pass through hello iframe boundary.</span></span> <span data-ttu-id="04ddf-115">Deze kan uw toepassing tooprogrammatically een actie uitvoert in een rapport en toolisten voor gebeurtenissen van acties die gebruikers in Hallo-rapport maken.</span><span class="sxs-lookup"><span data-stu-id="04ddf-115">This enables your application tooprogrammatically perform an action in a report, and toolisten for events from actions that users make within hello report.</span></span>

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a><span data-ttu-id="04ddf-116">Wat kunt u doen met Hallo Power BI JavaScript-API</span><span class="sxs-lookup"><span data-stu-id="04ddf-116">What can you do with hello Power BI JavaScript API?</span></span>
<span data-ttu-id="04ddf-117">Hello JavaScript-API kunt u rapporten beheren, gaat u toopages in een rapport, een rapport filteren en insluiten gebeurtenissen verwerken.</span><span class="sxs-lookup"><span data-stu-id="04ddf-117">With hello JavaScript API you can manage reports, navigate toopages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="04ddf-118">Hallo toont volgende diagram Hallo-structuur van Hallo API.</span><span class="sxs-lookup"><span data-stu-id="04ddf-118">hello following diagram shows hello structure of hello API.</span></span>

![Diagram van JavaScript-API van Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="04ddf-120">Rapporten beheren</span><span class="sxs-lookup"><span data-stu-id="04ddf-120">Manage reports</span></span>
<span data-ttu-id="04ddf-121">Hallo Javascript-API kunt u toomanage gedrag op Hallo rapport en pagina niveau:</span><span class="sxs-lookup"><span data-stu-id="04ddf-121">hello Javascript API enables you toomanage behavior at hello report and page level:</span></span>

* <span data-ttu-id="04ddf-122">Een specifieke Power BI-rapport veilig insluiten in uw toepassing - Hallo probeer [voorbeeldtoepassing insluiten](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="04ddf-122">Embed a specific Power BI Report securely in your application - try hello [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="04ddf-123">Toegangstoken instellen</span><span class="sxs-lookup"><span data-stu-id="04ddf-123">Set access token</span></span>
* <span data-ttu-id="04ddf-124">Hallo rapport configureren</span><span class="sxs-lookup"><span data-stu-id="04ddf-124">Configure hello report</span></span>
  * <span data-ttu-id="04ddf-125">Inschakelen en uitschakelen Hallo filterdeelvenster en het navigatiedeelvenster van pagina - probeer het Hallo [instellingen demo toepassing bijwerken](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="04ddf-125">Enable and disable hello filter pane and page navigation pane - try hello [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="04ddf-126">Standaardopties voor pagina's en filters instellen - Hallo probeer [set standaardwaarden demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="04ddf-126">Set defaults for pages and filters - try hello [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="04ddf-127">De schermvullende modus openen en sluiten</span><span class="sxs-lookup"><span data-stu-id="04ddf-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="04ddf-128">Meer informatie over het insluiten van een rapport</span><span class="sxs-lookup"><span data-stu-id="04ddf-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a><span data-ttu-id="04ddf-129">Navigeer toopages in een rapport</span><span class="sxs-lookup"><span data-stu-id="04ddf-129">Navigate toopages in a report</span></span>
<span data-ttu-id="04ddf-130">Hallo JavaScript API enbales u toodiscover alle pagina's in een rapport en tooset Hallo huidige pagina.</span><span class="sxs-lookup"><span data-stu-id="04ddf-130">hello JavaScript API enbales you toodiscover all pages in a report and tooset hello current page.</span></span> <span data-ttu-id="04ddf-131">Probeer Hallo [navigatie-voorbeeldtoepassing](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span><span class="sxs-lookup"><span data-stu-id="04ddf-131">Try hello [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="04ddf-132">Meer informatie over paginanavigatie</span><span class="sxs-lookup"><span data-stu-id="04ddf-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="04ddf-133">Een rapport filteren</span><span class="sxs-lookup"><span data-stu-id="04ddf-133">Filter a report</span></span>
<span data-ttu-id="04ddf-134">Hallo JavaScript-API biedt basiseigenschappen en geavanceerde mogelijkheden voor ingesloten rapporten en rapportpagina's filteren.</span><span class="sxs-lookup"><span data-stu-id="04ddf-134">hello JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="04ddf-135">Probeer Hallo [filteren voorbeeldtoepassing](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), en sommige inleidende code hier bekijken.</span><span class="sxs-lookup"><span data-stu-id="04ddf-135">Try hello [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="04ddf-136">Basisfilters</span><span class="sxs-lookup"><span data-stu-id="04ddf-136">Basic filters</span></span>
<span data-ttu-id="04ddf-137">Een basic-filter op een kolom of de hiërarchie een niveau wordt geplaatst en bevat een lijst met waarden tooinclude of uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="04ddf-137">A basic filter is placed on a column or hierarchy level and contains a list of values tooinclude or exclude.</span></span>

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a><span data-ttu-id="04ddf-138">Geavanceerde filters</span><span class="sxs-lookup"><span data-stu-id="04ddf-138">Advanced filters</span></span>
<span data-ttu-id="04ddf-139">Geavanceerde filters gebruiken Hallo logische operator en of OR en een of twee voorwaarden, elk met hun eigen operator en een waarde te accepteren.</span><span class="sxs-lookup"><span data-stu-id="04ddf-139">Advanced filters use hello logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="04ddf-140">Ondersteunde voorwaarden zijn:</span><span class="sxs-lookup"><span data-stu-id="04ddf-140">Supported conditions are:</span></span>

* <span data-ttu-id="04ddf-141">None</span><span class="sxs-lookup"><span data-stu-id="04ddf-141">None</span></span>
* <span data-ttu-id="04ddf-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="04ddf-142">LessThan</span></span>
* <span data-ttu-id="04ddf-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="04ddf-143">LessThanOrEqual</span></span>
* <span data-ttu-id="04ddf-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="04ddf-144">GreaterThan</span></span>
* <span data-ttu-id="04ddf-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="04ddf-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="04ddf-146">Contains</span><span class="sxs-lookup"><span data-stu-id="04ddf-146">Contains</span></span>
* <span data-ttu-id="04ddf-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="04ddf-147">DoesNotContain</span></span>
* <span data-ttu-id="04ddf-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="04ddf-148">StartsWith</span></span>
* <span data-ttu-id="04ddf-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="04ddf-149">DoesNotStartWith</span></span>
* <span data-ttu-id="04ddf-150">Is</span><span class="sxs-lookup"><span data-stu-id="04ddf-150">Is</span></span>
* <span data-ttu-id="04ddf-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="04ddf-151">IsNot</span></span>
* <span data-ttu-id="04ddf-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="04ddf-152">IsBlank</span></span>
* <span data-ttu-id="04ddf-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="04ddf-153">IsNotBlank</span></span>

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[<span data-ttu-id="04ddf-154">Meer informatie over filteren</span><span class="sxs-lookup"><span data-stu-id="04ddf-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="04ddf-155">Gebeurtenissen verwerken</span><span class="sxs-lookup"><span data-stu-id="04ddf-155">Handling events</span></span>
<span data-ttu-id="04ddf-156">Bovendien toosending informatie naar Hallo iframe, uw toepassing kunt ook informatie ontvangen over Hallo gebeurtenissen die afkomstig zijn van Hallo iframe te volgen:</span><span class="sxs-lookup"><span data-stu-id="04ddf-156">In addition toosending information into hello iframe, your application can also receive information on hello following events coming from hello iframe:</span></span>

* <span data-ttu-id="04ddf-157">Embed</span><span class="sxs-lookup"><span data-stu-id="04ddf-157">Embed</span></span>
  * <span data-ttu-id="04ddf-158">loaded</span><span class="sxs-lookup"><span data-stu-id="04ddf-158">loaded</span></span>
  * <span data-ttu-id="04ddf-159">error</span><span class="sxs-lookup"><span data-stu-id="04ddf-159">error</span></span>
* <span data-ttu-id="04ddf-160">Rapporten</span><span class="sxs-lookup"><span data-stu-id="04ddf-160">Reports</span></span>
  * <span data-ttu-id="04ddf-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="04ddf-161">pageChanged</span></span>
  * <span data-ttu-id="04ddf-162">dataSelected (binnenkort)</span><span class="sxs-lookup"><span data-stu-id="04ddf-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="04ddf-163">Meer informatie over het verwerken van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="04ddf-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="04ddf-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="04ddf-164">Next steps</span></span>
<span data-ttu-id="04ddf-165">Bekijk voor meer informatie over Power BI JavaScript API Hallo Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="04ddf-165">For more information about hello Power BI JavaScript API, check out hello following links:</span></span>

* [<span data-ttu-id="04ddf-166">Wiki over JavaScript-API</span><span class="sxs-lookup"><span data-stu-id="04ddf-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="04ddf-167">Naslaginformatie over objectmodel</span><span class="sxs-lookup"><span data-stu-id="04ddf-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="04ddf-168">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="04ddf-168">Samples</span></span>
  * [<span data-ttu-id="04ddf-169">Angular</span><span class="sxs-lookup"><span data-stu-id="04ddf-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="04ddf-170">Ember</span><span class="sxs-lookup"><span data-stu-id="04ddf-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="04ddf-171">Livedemo</span><span class="sxs-lookup"><span data-stu-id="04ddf-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)

