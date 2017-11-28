---
title: aaaUsing OMS Log Analytics waarschuwing REST-API
description: Hallo Log Analytics waarschuwing REST-API kunt u toocreate en waarschuwingen beheren in logboekanalyse die deel uitmaakt van de Operations Management Suite (OMS).  Dit artikel bevat de details van Hallo API en enkele voorbeelden voor het uitvoeren van verschillende bewerkingen.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="ba3f1-104">Maken en beheren van waarschuwingsregels in logboekanalyse met REST-API</span><span class="sxs-lookup"><span data-stu-id="ba3f1-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="ba3f1-105">Hallo Log Analytics waarschuwing REST-API kunt u toocreate en waarschuwingen in Operations Management Suite (OMS) beheren.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-105">hello Log Analytics Alert REST API allows you toocreate and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="ba3f1-106">Dit artikel bevat de details van Hallo API en enkele voorbeelden voor het uitvoeren van verschillende bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-106">This article provides details of hello API and several examples for performing different operations.</span></span>

<span data-ttu-id="ba3f1-107">Hallo Log Analytics Search REST-API RESTful is en toegankelijk zijn via Hallo REST-API van Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-107">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager REST API.</span></span> <span data-ttu-id="ba3f1-108">In dit document vindt u voorbeelden waarbij Hallo API worden geopend vanuit een PowerShell-opdrachtregel met [ARMClient](https://github.com/projectkudu/ARMClient), een open-source opdrachtregel-hulpprogramma dat wordt aangeroepen vereenvoudigt hello Azure Resource Manager-API.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-108">In this document you will find examples where hello API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="ba3f1-109">Hallo-gebruik van ARMClient en PowerShell is een van de vele opties tooaccess Hallo Log Analytics zoeken-API.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-109">hello use of ARMClient and PowerShell is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="ba3f1-110">Met deze hulpprogramma's kunt u gebruikmaken van Hallo RESTful API van Azure Resource Manager toomake aanroepen tooOMS werkruimten en zoekvariabelen binnen deze.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-110">With these tools you can utilize hello RESTful Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="ba3f1-111">Hallo API wordt zoeken resultaten tooyou in JSON-indeling, zodat u toouse Hallo zoekresultaten in veel verschillende manieren programmatisch uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-111">hello API will output search results tooyou in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba3f1-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ba3f1-112">Prerequisites</span></span>
<span data-ttu-id="ba3f1-113">Waarschuwingen kunnen op dit moment kunnen alleen worden gemaakt met een opgeslagen zoekopdracht in logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="ba3f1-114">U kunt verwijzen toohello [logboek Search REST-API](log-analytics-log-search-api.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-114">You can refer toohello [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="ba3f1-115">Planningen</span><span class="sxs-lookup"><span data-stu-id="ba3f1-115">Schedules</span></span>
<span data-ttu-id="ba3f1-116">Een opgeslagen zoekopdracht kan een of meer planningen hebben.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="ba3f1-117">Hallo schema wordt gedefinieerd hoe vaak hello zoekopdracht wordt uitgevoerd en de tijdsinterval Hallo via welke criteria hello wordt aangeduid.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-117">hello schedule defines how often hello search is run and hello time interval over which hello criteria is identified.</span></span>
<span data-ttu-id="ba3f1-118">Schema's hebben Hallo eigenschappen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-118">Schedules have hello properties in hello following table.</span></span>

| <span data-ttu-id="ba3f1-119">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ba3f1-119">Property</span></span> | <span data-ttu-id="ba3f1-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ba3f1-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ba3f1-121">Interval</span><span class="sxs-lookup"><span data-stu-id="ba3f1-121">Interval</span></span> |<span data-ttu-id="ba3f1-122">Hoe vaak hello zoekopdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-122">How often hello search is run.</span></span> <span data-ttu-id="ba3f1-123">Gemeten in minuten.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-123">Measured in minutes.</span></span> |
| <span data-ttu-id="ba3f1-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="ba3f1-124">QueryTimeSpan</span></span> |<span data-ttu-id="ba3f1-125">Hallo tijdsinterval welke Hallo criteria wordt geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-125">hello time interval over which hello criteria is evaluated.</span></span> <span data-ttu-id="ba3f1-126">Moet gelijk tooor groter dan het Interval.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-126">Must be equal tooor greater than Interval.</span></span> <span data-ttu-id="ba3f1-127">Gemeten in minuten.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-127">Measured in minutes.</span></span> |
| <span data-ttu-id="ba3f1-128">Versie</span><span class="sxs-lookup"><span data-stu-id="ba3f1-128">Version</span></span> |<span data-ttu-id="ba3f1-129">Hallo API-versie die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-129">hello API version being used.</span></span>  <span data-ttu-id="ba3f1-130">Op dit moment is moet dit altijd worden ingesteld too1.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-130">Currently, this should always be set too1.</span></span> |

<span data-ttu-id="ba3f1-131">Neem bijvoorbeeld een event-query met een Interval van 15 minuten en een TimeSpan-waarde van 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="ba3f1-132">In dit geval Hallo query wilt uitvoeren om de 15 minuten en een waarschuwing zou worden geactiveerd als Hallo criteria nog steeds tooresolve tootrue gedurende een bepaalde 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-132">In this case, hello query would be run every 15 minutes, and an alert would be triggered if hello criteria continued tooresolve tootrue over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="ba3f1-133">Bij het ophalen van schema 's</span><span class="sxs-lookup"><span data-stu-id="ba3f1-133">Retrieving schedules</span></span>
<span data-ttu-id="ba3f1-134">Gebruik Hallo ophalen methode tooretrieve alle schema's voor een opgeslagen zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-134">Use hello Get method tooretrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="ba3f1-135">Gebruik Hallo ophalen methode met een schema-ID tooretrieve een bepaalde planning voor een opgeslagen zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-135">Use hello Get method with a schedule ID tooretrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="ba3f1-136">Hier volgt een voorbeeldantwoord voor een schema.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-136">Following is a sample response for a schedule.</span></span>

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a><span data-ttu-id="ba3f1-137">Een schema maken</span><span class="sxs-lookup"><span data-stu-id="ba3f1-137">Creating a schedule</span></span>
<span data-ttu-id="ba3f1-138">Hallo Put-methode gebruiken met een uniek schema-ID toocreate een nieuw schema.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-138">Use hello Put method with a unique schedule ID toocreate a new schedule.</span></span>  <span data-ttu-id="ba3f1-139">Opmerking dat twee planningen kan niet hebben Hallo dezelfde ID zelfs als ze zijn gekoppeld aan verschillende opgeslagen zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-139">Note that two schedules cannot have hello same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="ba3f1-140">Wanneer u een planning in Hallo OMS-console maakt, wordt een GUID gemaakt voor Hallo-schema.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-140">When you create a schedule in hello OMS console, a GUID is created for hello schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="ba3f1-141">Hallo-naam voor alle opgeslagen zoekopdrachten, schema's en acties die zijn gemaakt met de Hallo Log Analytics-API moet in kleine letters.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-141">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="ba3f1-142">Het bewerken van een planning</span><span class="sxs-lookup"><span data-stu-id="ba3f1-142">Editing a schedule</span></span>
<span data-ttu-id="ba3f1-143">Hallo Put-methode met een bestaand schema-ID voor dezelfde opgeslagen Hallo toomodify die plant zoeken gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-143">Use hello Put method with an existing schedule ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="ba3f1-144">Hallo-hoofdtekst van Hallo-aanvraag moet Hallo etag Hallo schema bevatten.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-144">hello body of hello request must include hello etag of hello schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="ba3f1-145">Schema's verwijderen</span><span class="sxs-lookup"><span data-stu-id="ba3f1-145">Deleting schedules</span></span>
<span data-ttu-id="ba3f1-146">Hallo-Delete-methode gebruiken met een schema-ID toodelete een planning.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-146">Use hello Delete method with a schedule ID toodelete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="ba3f1-147">Acties</span><span class="sxs-lookup"><span data-stu-id="ba3f1-147">Actions</span></span>
<span data-ttu-id="ba3f1-148">Een planning kan meerdere acties hebben.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="ba3f1-149">Een actie kan definiëren een of meer processen tooperform zoals een e-mailbericht verzenden of een runbook starten, of het kan een drempelwaarde die bepaalt wanneer Hallo resultaten van een zoekopdracht voldoen aan bepaalde criteria definiëren.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-149">An action may define one or more processes tooperform such as sending a mail or starting a runbook, or it may define a threshold that determines when hello results of a search match some criteria.</span></span>  <span data-ttu-id="ba3f1-150">Sommige acties definiëren beide zodat Hallo processen worden uitgevoerd wanneer Hallo drempelwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-150">Some actions will define both so that hello processes are performed when hello threshold is met.</span></span>

<span data-ttu-id="ba3f1-151">Alle acties hebben Hallo eigenschappen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-151">All actions have hello properties in hello following table.</span></span>  <span data-ttu-id="ba3f1-152">Verschillende soorten waarschuwingen hebben verschillende aanvullende eigenschappen die hieronder worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="ba3f1-153">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ba3f1-153">Property</span></span> | <span data-ttu-id="ba3f1-154">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ba3f1-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ba3f1-155">Type</span><span class="sxs-lookup"><span data-stu-id="ba3f1-155">Type</span></span> |<span data-ttu-id="ba3f1-156">Type Hallo actie.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-156">Type of hello action.</span></span>  <span data-ttu-id="ba3f1-157">Hallo mogelijke waarden zijn momenteel waarschuwing en Webhook.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-157">Currently hello possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="ba3f1-158">Naam</span><span class="sxs-lookup"><span data-stu-id="ba3f1-158">Name</span></span> |<span data-ttu-id="ba3f1-159">Weergavenaam voor Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-159">Display name for hello alert.</span></span> |
| <span data-ttu-id="ba3f1-160">Versie</span><span class="sxs-lookup"><span data-stu-id="ba3f1-160">Version</span></span> |<span data-ttu-id="ba3f1-161">Hallo API-versie die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-161">hello API version being used.</span></span>  <span data-ttu-id="ba3f1-162">Op dit moment is moet dit altijd worden ingesteld too1.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-162">Currently, this should always be set too1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="ba3f1-163">Bij het ophalen van acties</span><span class="sxs-lookup"><span data-stu-id="ba3f1-163">Retrieving actions</span></span>
<span data-ttu-id="ba3f1-164">Gebruik Hallo ophalen methode tooretrieve alle acties voor een schema.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-164">Use hello Get method tooretrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="ba3f1-165">Gebruik Hallo ophalen methode met Hallo actie-ID tooretrieve een bepaalde actie voor een schema.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-165">Use hello Get method with hello action ID tooretrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="ba3f1-166">Maken of bewerken van acties</span><span class="sxs-lookup"><span data-stu-id="ba3f1-166">Creating or editing actions</span></span>
<span data-ttu-id="ba3f1-167">Hallo Put-methode gebruiken met een actie-ID is uniek toohello planning toocreate een nieuwe actie.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-167">Use hello Put method with an action ID that is unique toohello schedule toocreate a new action.</span></span>  <span data-ttu-id="ba3f1-168">Wanneer u een actie in Hallo OMS-console maakt, is een GUID voor Hallo actie-ID.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-168">When you create an action in hello OMS console, a GUID is for hello action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="ba3f1-169">Hallo-naam voor alle opgeslagen zoekopdrachten, schema's en acties die zijn gemaakt met de Hallo Log Analytics-API moet in kleine letters.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-169">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="ba3f1-170">Hallo Put-methode met een bestaande actie-ID voor dezelfde opgeslagen Hallo toomodify die plant zoeken gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-170">Use hello Put method with an existing action ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="ba3f1-171">Hallo-hoofdtekst van Hallo-aanvraag moet Hallo etag Hallo schema bevatten.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-171">hello body of hello request must include hello etag of hello schedule.</span></span>

<span data-ttu-id="ba3f1-172">De aanvraagindeling Hallo voor het maken van een nieuwe actie varieert per actietype zodat deze voorbeelden u in de volgende secties voor Hallo vindt.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-172">hello request format for creating a new action varies by action type so these examples are provided in hello sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="ba3f1-173">Acties worden verwijderd</span><span class="sxs-lookup"><span data-stu-id="ba3f1-173">Deleting actions</span></span>
<span data-ttu-id="ba3f1-174">Hallo-Delete-methode gebruiken met Hallo actie-ID toodelete een actie.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-174">Use hello Delete method with hello action ID toodelete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="ba3f1-175">Waarschuwing acties</span><span class="sxs-lookup"><span data-stu-id="ba3f1-175">Alert Actions</span></span>
<span data-ttu-id="ba3f1-176">Een planning hebt slechts één meldingsactie.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="ba3f1-177">Waarschuwing acties hebben een of meer van de secties in de volgende tabel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-177">Alert actions have one or more of hello sections in hello following table.</span></span>  <span data-ttu-id="ba3f1-178">Elk wordt nader hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="ba3f1-179">Sectie</span><span class="sxs-lookup"><span data-stu-id="ba3f1-179">Section</span></span> | <span data-ttu-id="ba3f1-180">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ba3f1-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ba3f1-181">Drempelwaarde</span><span class="sxs-lookup"><span data-stu-id="ba3f1-181">Threshold</span></span> |<span data-ttu-id="ba3f1-182">Criteria voor wanneer Hallo actie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-182">Criteria for when hello action is run.</span></span> |
| <span data-ttu-id="ba3f1-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="ba3f1-183">EmailNotification</span></span> |<span data-ttu-id="ba3f1-184">E-mail toomultiple ontvangers verzenden.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-184">Send mail toomultiple recipients.</span></span> |
| <span data-ttu-id="ba3f1-185">Herstel</span><span class="sxs-lookup"><span data-stu-id="ba3f1-185">Remediation</span></span> |<span data-ttu-id="ba3f1-186">Start een runbook in Azure Automation tooattempt toocorrect geïdentificeerd probleem.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-186">Start a runbook in Azure Automation tooattempt toocorrect identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="ba3f1-187">Drempelwaarden</span><span class="sxs-lookup"><span data-stu-id="ba3f1-187">Thresholds</span></span>
<span data-ttu-id="ba3f1-188">Een waarschuwing actie mag slechts één drempelwaarde hebben.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="ba3f1-189">Wanneer resultaten van een opgeslagen zoekopdracht Hallo Hallo drempelwaarde in een actie die is gekoppeld aan die zoekopdracht overeenkomen, worden andere processen in die actie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-189">When hello results of a saved search match hello threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="ba3f1-190">Een actie kan alleen een drempelwaarde ook bevatten, zodat deze kan worden gebruikt met de acties die van andere typen die geen drempelwaarden bevatten.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="ba3f1-191">Drempelwaarden hebben Hallo eigenschappen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-191">Thresholds have hello properties in hello following table.</span></span>

| <span data-ttu-id="ba3f1-192">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ba3f1-192">Property</span></span> | <span data-ttu-id="ba3f1-193">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ba3f1-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ba3f1-194">Operator</span><span class="sxs-lookup"><span data-stu-id="ba3f1-194">Operator</span></span> |<span data-ttu-id="ba3f1-195">De operator voor Hallo drempelwaarde voor vergelijking.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-195">Operator for hello threshold comparison.</span></span> <br> <span data-ttu-id="ba3f1-196">gt = groter dan</span><span class="sxs-lookup"><span data-stu-id="ba3f1-196">gt = Greater Than</span></span> <br> <span data-ttu-id="ba3f1-197">lt = kleiner dan</span><span class="sxs-lookup"><span data-stu-id="ba3f1-197">lt = Less Than</span></span> |
| <span data-ttu-id="ba3f1-198">Waarde</span><span class="sxs-lookup"><span data-stu-id="ba3f1-198">Value</span></span> |<span data-ttu-id="ba3f1-199">Waarde voor Hallo drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-199">Value for hello threshold.</span></span> |

<span data-ttu-id="ba3f1-200">Neem bijvoorbeeld een event-query met een Interval van 15 minuten, een TimeSpan-waarde van 30 minuten en een drempel van meer dan 10.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="ba3f1-201">In dit geval Hallo query wilt uitvoeren om de 15 minuten en een waarschuwing zou worden geactiveerd als het 10 gebeurtenissen die zijn gemaakt via een reeks van 30 minuten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-201">In this case, hello query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="ba3f1-202">Hier volgt een voorbeeldantwoord voor een actie met alleen een drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-202">Following is a sample response for an action with only a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

<span data-ttu-id="ba3f1-203">Hallo Put-methode gebruiken met een unieke actie-ID toocreate een nieuwe drempelwaarde-actie voor een schema.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-203">Use hello Put method with a unique action ID toocreate a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="ba3f1-204">Hallo Put-methode gebruiken met een bestaande actie-ID toomodify een actie drempelwaarde voor een schema.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-204">Use hello Put method with an existing action ID toomodify a threshold action for a schedule.</span></span>  <span data-ttu-id="ba3f1-205">Hallo-hoofdtekst van Hallo-aanvraag moet Hallo etag Hallo actie opnemen.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-205">hello body of hello request must include hello etag of hello action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="ba3f1-206">E-mailmeldingen</span><span class="sxs-lookup"><span data-stu-id="ba3f1-206">Email Notification</span></span>
<span data-ttu-id="ba3f1-207">E-mailmeldingen verzenden van e-mail tooone of meer geadresseerden.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-207">Email Notifications send mail tooone or more recipients.</span></span>  <span data-ttu-id="ba3f1-208">Ze bevatten Hallo eigenschappen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-208">They include hello properties in hello following table.</span></span>

| <span data-ttu-id="ba3f1-209">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ba3f1-209">Property</span></span> | <span data-ttu-id="ba3f1-210">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ba3f1-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ba3f1-211">ontvangers</span><span class="sxs-lookup"><span data-stu-id="ba3f1-211">Recipients</span></span> |<span data-ttu-id="ba3f1-212">Lijst met e-mailadressen.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-212">List of mail addresses.</span></span> |
| <span data-ttu-id="ba3f1-213">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="ba3f1-213">Subject</span></span> |<span data-ttu-id="ba3f1-214">Hallo onderwerp Hallo mail.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-214">hello subject of hello mail.</span></span> |
| <span data-ttu-id="ba3f1-215">Bijlage</span><span class="sxs-lookup"><span data-stu-id="ba3f1-215">Attachment</span></span> |<span data-ttu-id="ba3f1-216">Bijlagen worden momenteel niet ondersteund, zodat dit altijd de waarde 'None'.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="ba3f1-217">Hier volgt een voorbeeldantwoord voor een actie van de melding e-mailbericht met een drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-217">Following is a sample response for an email notification action with a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="ba3f1-218">Hallo Put-methode gebruiken met een unieke actie-ID toocreate een nieuwe e-actie voor een schema.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-218">Use hello Put method with a unique action ID toocreate a new e-mail action for a schedule.</span></span>  <span data-ttu-id="ba3f1-219">Hallo wordt volgende voorbeeld een e-mailbericht met een drempelwaarde daarom Hallo e-mail wordt verzonden wanneer het Hallo-resultaten van de opgeslagen zoekopdracht Hallo Hallo drempelwaarde overschrijden.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-219">hello following example creates an email notification with a threshold so hello mail is sent when hello results of hello saved search exceed hello threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="ba3f1-220">Hallo Put-methode gebruiken met een bestaande actie-ID toomodify een e-actie voor een schema.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-220">Use hello Put method with an existing action ID toomodify an e-mail action for a schedule.</span></span>  <span data-ttu-id="ba3f1-221">Hallo-hoofdtekst van Hallo-aanvraag moet Hallo etag Hallo actie opnemen.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-221">hello body of hello request must include hello etag of hello action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="ba3f1-222">Herstelacties</span><span class="sxs-lookup"><span data-stu-id="ba3f1-222">Remediation actions</span></span>
<span data-ttu-id="ba3f1-223">Herstelbewerkingen starten van een runbook in Azure Automation waarmee wordt geprobeerd toocorrect Hallo probleem geïdentificeerd door Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-223">Remediations start a runbook in Azure Automation that attempts toocorrect hello problem identified by hello alert.</span></span>  <span data-ttu-id="ba3f1-224">U moet een webhook voor Hallo runbook gebruikt in een herstelactie maken en geeft vervolgens Hallo URI in Hallo WebhookUri-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-224">You must create a webhook for hello runbook used in a remediation action and then specify hello URI in hello WebhookUri property.</span></span>  <span data-ttu-id="ba3f1-225">Wanneer u deze actie met Hallo OMS-console maakt, wordt automatisch een nieuwe webhook gemaakt voor runbook Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-225">When you create this action using hello OMS console, a new webhook is automatically created for hello runbook.</span></span>

<span data-ttu-id="ba3f1-226">Hallo-eigenschappen bevatten herstelbewerkingen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-226">Remediations include hello properties in hello following table.</span></span>

| <span data-ttu-id="ba3f1-227">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ba3f1-227">Property</span></span> | <span data-ttu-id="ba3f1-228">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ba3f1-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ba3f1-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="ba3f1-229">RunbookName</span></span> |<span data-ttu-id="ba3f1-230">Naam van Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-230">Name of hello runbook.</span></span> <span data-ttu-id="ba3f1-231">Dit moet overeenkomen met een gepubliceerd runbook in Hallo automation-account is geconfigureerd in Hallo Automation-oplossing in de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-231">This must match a published runbook in hello automation account configured in hello Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="ba3f1-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="ba3f1-232">WebhookUri</span></span> |<span data-ttu-id="ba3f1-233">De URI van de webhook Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-233">URI of hello webhook.</span></span> |
| <span data-ttu-id="ba3f1-234">Verloopdatum</span><span class="sxs-lookup"><span data-stu-id="ba3f1-234">Expiry</span></span> |<span data-ttu-id="ba3f1-235">Hallo datum en tijd van de webhook Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-235">hello expiration date and time of hello webhook.</span></span>  <span data-ttu-id="ba3f1-236">Als Hallo webhook geen een verlopen, kan dit een geldige datum in de toekomst zijn.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-236">If hello webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="ba3f1-237">Hier volgt een voorbeeldantwoord voor een herstelactie met een drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-237">Following is a sample response for a remediation action with a threshold.</span></span>

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

<span data-ttu-id="ba3f1-238">Hallo Put-methode gebruiken met een unieke actie-ID toocreate een nieuwe herstelactie voor een schema.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-238">Use hello Put method with a unique action ID toocreate a new remediation action for a schedule.</span></span>  <span data-ttu-id="ba3f1-239">Hallo wordt volgende voorbeeld een herstelbewerking met een drempelwaarde daarom Hallo runbook wordt gestart wanneer het Hallo-resultaten van de opgeslagen zoekopdracht Hallo Hallo drempelwaarde overschrijden.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-239">hello following example creates a remediation with a threshold so hello runbook is started when hello results of hello saved search exceed hello threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="ba3f1-240">Hallo Put-methode gebruiken met een bestaande actie-ID toomodify een herstelactie voor een schema.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-240">Use hello Put method with an existing action ID toomodify a remediation action for a schedule.</span></span>  <span data-ttu-id="ba3f1-241">Hallo-hoofdtekst van Hallo-aanvraag moet Hallo etag Hallo actie opnemen.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-241">hello body of hello request must include hello etag of hello action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="ba3f1-242">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="ba3f1-242">Example</span></span>
<span data-ttu-id="ba3f1-243">Hier volgt een voorbeeld van de volledige toocreate een nieuw e-mailmelding.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-243">Following is a complete example toocreate a new email alert.</span></span>  <span data-ttu-id="ba3f1-244">Hiermee maakt u een nieuw schema samen met een actie met een drempelwaarde en e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="ba3f1-245">Webhookacties</span><span class="sxs-lookup"><span data-stu-id="ba3f1-245">Webhook actions</span></span>
<span data-ttu-id="ba3f1-246">Een proces starten webhookacties door het aanroepen van een URL en het eventueel geven een nettolading toobe verzonden.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-246">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span>  <span data-ttu-id="ba3f1-247">Ze zijn vergelijkbaar tooRemediation acties maar ze zijn bedoeld voor webhooks die van processen dan Azure Automation-runbooks gebruikmaken mogelijk.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-247">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="ba3f1-248">Ze bieden ook een extra optie Hallo van het bieden van een nettolading toobe bezorgd toohello extern proces.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-248">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="ba3f1-249">Webhookacties hebben geen een drempelwaarde, maar in plaats daarvan moeten tooa schema met de actie van een waarschuwing met een drempelwaarde worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-249">Webhook actions do not have a threshold but instead should be added tooa schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="ba3f1-250">U kunt meerdere webhookacties die al worden uitgevoerd wanneer Hallo drempelwaarde wordt voldaan toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-250">You can add multiple Webhook actions that will all be run when hello threshold is met.</span></span>

<span data-ttu-id="ba3f1-251">Webhookacties bevatten Hallo eigenschappen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-251">Webhook actions include hello properties in hello following table.</span></span>

| <span data-ttu-id="ba3f1-252">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ba3f1-252">Property</span></span> | <span data-ttu-id="ba3f1-253">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ba3f1-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ba3f1-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="ba3f1-254">WebhookUri</span></span> |<span data-ttu-id="ba3f1-255">Hallo onderwerp Hallo mail.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-255">hello subject of hello mail.</span></span> |
| <span data-ttu-id="ba3f1-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="ba3f1-256">CustomPayload</span></span> |<span data-ttu-id="ba3f1-257">Aangepaste nettolading toobe toohello webhook verzonden.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-257">Custom payload toobe sent toohello webhook.</span></span>  <span data-ttu-id="ba3f1-258">Hallo-indeling afhankelijk van welke webhook hello wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-258">hello format will depend on what hello webhook is expecting.</span></span> |

<span data-ttu-id="ba3f1-259">Hier volgt een voorbeeldantwoord voor webhook actie en een bijbehorende waarschuwingen met een drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="ba3f1-260">Maken of bewerken van een webhook-actie</span><span class="sxs-lookup"><span data-stu-id="ba3f1-260">Create or edit a webhook action</span></span>
<span data-ttu-id="ba3f1-261">Hallo Put-methode gebruiken met een unieke actie-ID toocreate een nieuwe webhook-actie voor een schema.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-261">Use hello Put method with a unique action ID toocreate a new webhook action for a schedule.</span></span>  <span data-ttu-id="ba3f1-262">Hallo maakt volgende voorbeeld een actie Webhook en een waarschuwing met een drempelwaarde zodat Hallo webhook wordt geactiveerd wanneer het Hallo-resultaten van de opgeslagen zoekopdracht Hallo Hallo drempelwaarde overschrijden.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-262">hello following example creates a Webhook action and an Alert action with a threshold so that hello webhook will be triggered when hello results of hello saved search exceed hello threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="ba3f1-263">Hallo Put-methode gebruiken met een bestaande actie-ID toomodify een webhook-actie voor een schema.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-263">Use hello Put method with an existing action ID toomodify a webhook action for a schedule.</span></span>  <span data-ttu-id="ba3f1-264">Hallo-hoofdtekst van Hallo-aanvraag moet Hallo etag Hallo actie opnemen.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-264">hello body of hello request must include hello etag of hello action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="ba3f1-265">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ba3f1-265">Next steps</span></span>
* <span data-ttu-id="ba3f1-266">Gebruik Hallo [REST-API tooperform logboek zoekopdrachten](log-analytics-log-search-api.md) in logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="ba3f1-266">Use hello [REST API tooperform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

