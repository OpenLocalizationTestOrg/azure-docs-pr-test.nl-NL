---
title: aaaResponses tooalerts in OMS Log Analytics | Microsoft Docs
description: Waarschuwingen in logboekanalyse belangrijke informatie in de OMS-opslagplaats te identificeren en op de proactief kunnen zullen u informeren over problemen of acties tooattempt toocorrect aanroepen ze.  Dit artikel wordt beschreven hoe een waarschuwingsregel toocreate en details Hallo verschillende acties kunnen nemen.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a><span data-ttu-id="5f19d-104">Acties tooalert regels in logboekanalyse toevoegen</span><span class="sxs-lookup"><span data-stu-id="5f19d-104">Add actions tooalert rules in Log Analytics</span></span>
<span data-ttu-id="5f19d-105">Wanneer een [waarschuwing is gemaakt in logboekanalyse](log-analytics-alerts.md), hebt u de optie Hallo van [configureren Hallo waarschuwingsregel](log-analytics-alerts.md) tooperform een of meer acties.</span><span class="sxs-lookup"><span data-stu-id="5f19d-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have hello option of [configuring hello alert rule](log-analytics-alerts.md) tooperform one or more actions.</span></span>  <span data-ttu-id="5f19d-106">In dit artikel beschrijft Hallo verschillende acties die beschikbaar zijn en meer informatie over het configureren van elk type.</span><span class="sxs-lookup"><span data-stu-id="5f19d-106">This article describes hello different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="5f19d-107">Actie</span><span class="sxs-lookup"><span data-stu-id="5f19d-107">Action</span></span> | <span data-ttu-id="5f19d-108">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5f19d-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="5f19d-109">E-mail</span><span class="sxs-lookup"><span data-stu-id="5f19d-109">Email</span></span>](#email-actions) | <span data-ttu-id="5f19d-110">Stuur een e-mail met Hallo details van de waarschuwing tooone Hallo of meer geadresseerden.</span><span class="sxs-lookup"><span data-stu-id="5f19d-110">Send an e-mail with hello details of hello alert tooone or more recipients.</span></span> |
| [<span data-ttu-id="5f19d-111">Webhook</span><span class="sxs-lookup"><span data-stu-id="5f19d-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="5f19d-112">Een extern proces via één HTTP POST-aanvraag worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5f19d-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="5f19d-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="5f19d-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="5f19d-114">Starten van een runbook in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="5f19d-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="5f19d-115">E-acties</span><span class="sxs-lookup"><span data-stu-id="5f19d-115">Email actions</span></span>
<span data-ttu-id="5f19d-116">E-acties Stuur een e-mail met Hallo details van de waarschuwing tooone Hallo of meer geadresseerden.</span><span class="sxs-lookup"><span data-stu-id="5f19d-116">Email actions send an e-mail with hello details of hello alert tooone or more recipients.</span></span>  <span data-ttu-id="5f19d-117">U kunt Hallo onderwerp van e-mail Hallo opgeven, maar de inhoud is een standaardindeling samengesteld door logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="5f19d-117">You can specify hello subject of hello mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="5f19d-118">Samenvattende informatie zoals de naam van de Hallo van Hallo waarschuwing in toodetails toevoeging van tooten records geretourneerd door de zoekfunctie Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="5f19d-118">It includes summary information such as hello name of hello alert in addition toodetails of up tooten records returned by hello log search.</span></span>  <span data-ttu-id="5f19d-119">Het bevat ook een koppeling tooa logboek zoekopdracht logboekanalyse dat Hallo volledige set van records uit deze query wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5f19d-119">It also includes a link tooa log search in Log Analytics that will return hello entire set of records from that query.</span></span>   <span data-ttu-id="5f19d-120">Hallo afzender Hallo mail *Microsoft Operations Management Suite-Team &lt; noreply@oms.microsoft.com &gt;* .</span><span class="sxs-lookup"><span data-stu-id="5f19d-120">hello sender of hello mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="5f19d-121">E-acties vereisen Hallo eigenschappen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f19d-121">Email actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="5f19d-122">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="5f19d-122">Property</span></span> | <span data-ttu-id="5f19d-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5f19d-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f19d-124">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="5f19d-124">Subject</span></span> |<span data-ttu-id="5f19d-125">Onderwerpen in Hallo e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="5f19d-125">Subject in hello email.</span></span>  <span data-ttu-id="5f19d-126">U kunt Hallo hoofdtekst van e-mail Hallo niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5f19d-126">You cannot modify hello body of hello mail.</span></span> |
| <span data-ttu-id="5f19d-127">ontvangers</span><span class="sxs-lookup"><span data-stu-id="5f19d-127">Recipients</span></span> |<span data-ttu-id="5f19d-128">De adressen van alle e-mailgeadresseerden.</span><span class="sxs-lookup"><span data-stu-id="5f19d-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="5f19d-129">Als u meer dan één adres vervolgens afzonderlijke hello-mailadressen opgeven met een puntkomma (;).</span><span class="sxs-lookup"><span data-stu-id="5f19d-129">If you specify more than one address, then separate hello addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="5f19d-130">Webhookacties</span><span class="sxs-lookup"><span data-stu-id="5f19d-130">Webhook actions</span></span>

<span data-ttu-id="5f19d-131">Webhookacties kunnen u tooinvoke een extern proces via één HTTP POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="5f19d-131">Webhook actions allow you tooinvoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="5f19d-132">Hallo-service wordt aangeroepen moet webhooks ondersteunen en bepaal hoe het door middel van elke nettolading wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="5f19d-132">hello service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="5f19d-133">U kunt ook een REST-API die niet specifiek webhooks ondersteunt, zolang het Hallo-aanvraag heeft een indeling die Hallo API begrijpt aanroepen.</span><span class="sxs-lookup"><span data-stu-id="5f19d-133">You could also call a REST API that doesn't specifically support webhooks as long as hello request is in a format that hello API understands.</span></span>  <span data-ttu-id="5f19d-134">Voorbeelden van het gebruik van een webhook in antwoord tooan waarschuwing een bericht verzendt [Slack](http://slack.com) of het maken van een incident in [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="5f19d-134">Examples of using a webhook in response tooan alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="5f19d-135">Een volledige procedure voor het maken van een waarschuwingsregel met een webhook toocall Slack is beschikbaar op [Webhooks in logboekanalyse waarschuwingen](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="5f19d-135">A complete walkthrough of creating an alert rule with a webhook toocall Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="5f19d-136">Webhookacties vereisen Hallo eigenschappen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f19d-136">Webhook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="5f19d-137">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="5f19d-137">Property</span></span> | <span data-ttu-id="5f19d-138">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5f19d-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f19d-139">Webhook-URL</span><span class="sxs-lookup"><span data-stu-id="5f19d-139">Webhook URL</span></span> |<span data-ttu-id="5f19d-140">Hallo-URL van de webhook Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f19d-140">hello URL of hello webhook.</span></span> |
| <span data-ttu-id="5f19d-141">Aangepaste JSON-nettolading</span><span class="sxs-lookup"><span data-stu-id="5f19d-141">Custom JSON payload</span></span> |<span data-ttu-id="5f19d-142">Aangepaste nettolading toosend met Hallo webhook.</span><span class="sxs-lookup"><span data-stu-id="5f19d-142">Custom payload toosend with hello webhook.</span></span>  <span data-ttu-id="5f19d-143">Zie hieronder voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5f19d-143">See below for details.</span></span> |


<span data-ttu-id="5f19d-144">Een URL opnemen naar Webhooks en een nettolading opgemaakt in JSON is Hallo gegevens toohello externe service verzonden.</span><span class="sxs-lookup"><span data-stu-id="5f19d-144">Webhooks include a URL and a payload formatted in JSON that is hello data sent toohello external service.</span></span>  <span data-ttu-id="5f19d-145">Standaard wordt Hallo nettolading in de volgende tabel Hallo Hallo waarden bevatten.</span><span class="sxs-lookup"><span data-stu-id="5f19d-145">By default, hello payload will include hello values in hello following table.</span></span>  <span data-ttu-id="5f19d-146">U kunt deze nettolading met een van uw eigen aangepaste tooreplace.</span><span class="sxs-lookup"><span data-stu-id="5f19d-146">You can choose tooreplace this payload with a custom one of your own.</span></span>  <span data-ttu-id="5f19d-147">In dat geval kunt u variabelen in de tabel Hallo Hallo voor elk Hallo parameters tooinclude hun waarde in de aangepaste nettolading.</span><span class="sxs-lookup"><span data-stu-id="5f19d-147">In that case you can use hello variables in hello table for each of hello parameters tooinclude their value in your custom payload.</span></span>

| <span data-ttu-id="5f19d-148">Parameter</span><span class="sxs-lookup"><span data-stu-id="5f19d-148">Parameter</span></span> | <span data-ttu-id="5f19d-149">Variabele</span><span class="sxs-lookup"><span data-stu-id="5f19d-149">Variable</span></span> | <span data-ttu-id="5f19d-150">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5f19d-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="5f19d-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="5f19d-151">AlertRuleName</span></span> |<span data-ttu-id="5f19d-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="5f19d-152">#alertrulename</span></span> |<span data-ttu-id="5f19d-153">Naam van de waarschuwingsregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f19d-153">Name of hello alert rule.</span></span> |
| <span data-ttu-id="5f19d-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="5f19d-154">AlertThresholdOperator</span></span> |<span data-ttu-id="5f19d-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="5f19d-155">#thresholdoperator</span></span> |<span data-ttu-id="5f19d-156">Drempelwaarde voor de operator voor Hallo waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="5f19d-156">Threshold operator for hello alert rule.</span></span>  <span data-ttu-id="5f19d-157">*Groter dan* of *minder dan*.</span><span class="sxs-lookup"><span data-stu-id="5f19d-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="5f19d-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="5f19d-158">AlertThresholdValue</span></span> |<span data-ttu-id="5f19d-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="5f19d-159">#thresholdvalue</span></span> |<span data-ttu-id="5f19d-160">Drempelwaarde voor het Hallo-waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="5f19d-160">Threshold value for hello alert rule.</span></span> |
| <span data-ttu-id="5f19d-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="5f19d-161">LinkToSearchResults</span></span> |<span data-ttu-id="5f19d-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="5f19d-162">#linktosearchresults</span></span> |<span data-ttu-id="5f19d-163">Koppeling tooLog Analytics logboek zoekquery waarmee Hallo records in de Hallo-query die Hallo waarschuwing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f19d-163">Link tooLog Analytics log search that returns hello records from hello query that created hello alert.</span></span> |
| <span data-ttu-id="5f19d-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="5f19d-164">ResultCount</span></span> |<span data-ttu-id="5f19d-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="5f19d-165">#searchresultcount</span></span> |<span data-ttu-id="5f19d-166">Het aantal records in de zoekresultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f19d-166">Number of records in hello search results.</span></span> |
| <span data-ttu-id="5f19d-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="5f19d-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="5f19d-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="5f19d-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="5f19d-169">De eindtijd voor de query Hallo in UTC-notatie.</span><span class="sxs-lookup"><span data-stu-id="5f19d-169">End time for hello query in UTC format.</span></span> |
| <span data-ttu-id="5f19d-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="5f19d-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="5f19d-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="5f19d-171">#searchinterval</span></span> |<span data-ttu-id="5f19d-172">Tijdvenster voor Hallo waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="5f19d-172">Time window for hello alert rule.</span></span> |
| <span data-ttu-id="5f19d-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="5f19d-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="5f19d-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="5f19d-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="5f19d-175">Begintijd voor de query Hallo in UTC-notatie.</span><span class="sxs-lookup"><span data-stu-id="5f19d-175">Start time for hello query in UTC format.</span></span> |
| <span data-ttu-id="5f19d-176">searchQuery</span><span class="sxs-lookup"><span data-stu-id="5f19d-176">SearchQuery</span></span> |<span data-ttu-id="5f19d-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="5f19d-177">#searchquery</span></span> |<span data-ttu-id="5f19d-178">Logboek zoekquery gebruikt door de waarschuwingsregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f19d-178">Log search query used by hello alert rule.</span></span> |
| <span data-ttu-id="5f19d-179">Zoekresultaten</span><span class="sxs-lookup"><span data-stu-id="5f19d-179">SearchResults</span></span> |<span data-ttu-id="5f19d-180">Hieronder vindt u de</span><span class="sxs-lookup"><span data-stu-id="5f19d-180">See below</span></span> |<span data-ttu-id="5f19d-181">Records geretourneerd door de query Hallo in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="5f19d-181">Records returned by hello query in JSON format.</span></span>  <span data-ttu-id="5f19d-182">Beperkte toohello eerste 5000 records.</span><span class="sxs-lookup"><span data-stu-id="5f19d-182">Limited toohello first 5,000 records.</span></span> |
| <span data-ttu-id="5f19d-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="5f19d-183">WorkspaceID</span></span> |<span data-ttu-id="5f19d-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="5f19d-184">#workspaceid</span></span> |<span data-ttu-id="5f19d-185">ID van de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="5f19d-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="5f19d-186">Bijvoorbeeld, kunt u opgeven Hallo aangepaste nettolading met een enkele parameter aangeroepen na *tekst*.</span><span class="sxs-lookup"><span data-stu-id="5f19d-186">For example, you might specify hello following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="5f19d-187">Hallo-service die deze webhook aanroept, zou deze parameter worden verwacht.</span><span class="sxs-lookup"><span data-stu-id="5f19d-187">hello service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="5f19d-188">De nettolading van dit voorbeeld zou oplossen toosomething zoals Hallo volgen wanneer toohello webhook verzonden.</span><span class="sxs-lookup"><span data-stu-id="5f19d-188">This example payload would resolve toosomething like hello following when sent toohello webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="5f19d-189">tooinclude zoekresultaten in een aangepaste nettolading toevoegen Hallo volgt regel als een eigenschap van het hoogste niveau in de json-nettolading Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f19d-189">tooinclude search results in a custom payload, add hello following line as a top level property in hello json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="5f19d-190">Bijvoorbeeld, toocreate een aangepaste nettolading met NET Hallo naam van waarschuwing en Hallo zoekresultaten, u kunt hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="5f19d-190">For example, toocreate a custom payload that includes just hello alert name and hello search results, you could use hello following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="5f19d-191">U kunt een compleet voorbeeld van een waarschuwingsregel maken met een toostart webhook met een externe service op doorlopen [maakt een actie waarschuwing webhook in OMS Log Analytics toosend bericht tooSlack](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="5f19d-191">You can walk through a complete example of creating an alert rule with a webhook toostart an external service at [Create an alert webhook action in OMS Log Analytics toosend message tooSlack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="5f19d-192">Runbook-acties</span><span class="sxs-lookup"><span data-stu-id="5f19d-192">Runbook actions</span></span>
<span data-ttu-id="5f19d-193">Runbook-acties starten van een runbook in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="5f19d-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="5f19d-194">In volgorde toouse dit type actie, moet u hebben Hallo [Automation-oplossing](log-analytics-add-solutions.md) geïnstalleerd en geconfigureerd in de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="5f19d-194">In order toouse this type of action, you must have hello [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="5f19d-195">U kunt kiezen uit runbooks Hallo in Hallo automation-account die u hebt geconfigureerd in Hallo Automation-oplossing.</span><span class="sxs-lookup"><span data-stu-id="5f19d-195">You can select from hello runbooks in hello automation account that you configured in hello Automation solution.</span></span>

<span data-ttu-id="5f19d-196">Runbook-bewerkingen moet Hallo eigenschappen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f19d-196">Runbook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="5f19d-197">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="5f19d-197">Property</span></span> | <span data-ttu-id="5f19d-198">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5f19d-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="5f19d-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="5f19d-199">Runbook</span></span> | <span data-ttu-id="5f19d-200">Het Runbook dat het gewenste toostart wanneer een waarschuwing wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f19d-200">Runbook that you want toostart when an alert is created.</span></span> |
| <span data-ttu-id="5f19d-201">Voer op</span><span class="sxs-lookup"><span data-stu-id="5f19d-201">Run on</span></span> | <span data-ttu-id="5f19d-202">Geef **Azure** toorun hello runbook in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f19d-202">Specify **Azure** toorun hello runbook in hello cloud.</span></span>  <span data-ttu-id="5f19d-203">Geef **hybride worker** toorun hello runbook op een agent met [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5f19d-203">Specify **Hybrid worker** toorun hello runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="5f19d-204">Runbook-acties aan de slag Hallo runbook met een [webhook](../automation/automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="5f19d-204">Runbook actions start hello runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="5f19d-205">Wanneer u een waarschuwingsregel Hallo maakt, wordt deze automatisch een nieuwe webhook voor Hallo runbook maken met Hallo naam **OMS waarschuwing herstel** gevolgd door een GUID.</span><span class="sxs-lookup"><span data-stu-id="5f19d-205">When you create hello alert rule, it will automatically create a new webhook for hello runbook with hello name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="5f19d-206">U kan niet rechtstreeks vullen van de parameters van Hallo runbook maar Hallo [$WebhookData parameter](../automation/automation-webhooks.md) bevat details op Hallo van Hallo waarschuwing, met inbegrip van Hallo resultaten van Hallo logboek zoekopdracht waarvan deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f19d-206">You cannot directly populate any parameters of hello runbook, but hello [$WebhookData parameter](../automation/automation-webhooks.md) will include hello details of hello alert, including hello results of hello log search that created it.</span></span>  <span data-ttu-id="5f19d-207">Hallo runbook moet toodefine **$WebhookData** als parameter voor deze tooaccess eigenschappen van de waarschuwing Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f19d-207">hello runbook will need toodefine **$WebhookData** as a parameter for it tooaccess hello properties of hello alert.</span></span>  <span data-ttu-id="5f19d-208">Hallo waarschuwingsgegevens is beschikbaar in json-indeling in één eigenschap aangeroepen **zoekresultaten** in Hallo **RequestBody** eigenschap van **$WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="5f19d-208">hello alert data is available in json format in a single property called **SearchResults** in hello **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="5f19d-209">Dit heeft met de eigenschappen in de volgende tabel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f19d-209">This will have with hello properties in hello following table.</span></span>

| <span data-ttu-id="5f19d-210">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="5f19d-210">Node</span></span> | <span data-ttu-id="5f19d-211">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5f19d-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f19d-212">id</span><span class="sxs-lookup"><span data-stu-id="5f19d-212">id</span></span> |<span data-ttu-id="5f19d-213">Pad en de GUID van Hallo zoeken.</span><span class="sxs-lookup"><span data-stu-id="5f19d-213">Path and GUID of hello search.</span></span> |
| <span data-ttu-id="5f19d-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="5f19d-214">__metadata</span></span> |<span data-ttu-id="5f19d-215">Informatie over Hallo waarschuwing inclusief Hallo aantal records en status van Hallo zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="5f19d-215">Information about hello alert including hello number of records and status of hello search results.</span></span> |
| <span data-ttu-id="5f19d-216">waarde</span><span class="sxs-lookup"><span data-stu-id="5f19d-216">value</span></span> |<span data-ttu-id="5f19d-217">Afzonderlijke vermelding voor elke record in de zoekresultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f19d-217">Separate entry for each record in hello search results.</span></span>  <span data-ttu-id="5f19d-218">Hallo-details van Hallo vermelding komt overeen met Hallo eigenschappen en waarden van Hallo record.</span><span class="sxs-lookup"><span data-stu-id="5f19d-218">hello details of hello entry will match hello properties and values of hello record.</span></span> |

<span data-ttu-id="5f19d-219">Bijvoorbeeld zou hello volgende runbook pak Hallo records geretourneerd door Hallo logboek zoeken en toewijzen van verschillende eigenschappen die zijn gebaseerd op het Hallo-type van elke record.</span><span class="sxs-lookup"><span data-stu-id="5f19d-219">For example, hello following runbook would extract hello records returned by hello log search  and assign different properties based on hello type of each record.</span></span>  <span data-ttu-id="5f19d-220">Houd er rekening mee dat runbook Hallo begint met het converteren van **RequestBody** van json zodanig dat deze kan worden gewerkt met als een object in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f19d-220">Note that hello runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a><span data-ttu-id="5f19d-221">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f19d-221">Next steps</span></span>
- <span data-ttu-id="5f19d-222">Een stapsgewijze Kennismaking voltooien [configureren van een webook](log-analytics-alerts-webhooks.md) met een waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="5f19d-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="5f19d-223">Meer informatie over hoe toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problemen geïdentificeerd met waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="5f19d-223">Learn how toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problems identified by alerts.</span></span>
