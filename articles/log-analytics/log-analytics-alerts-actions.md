---
title: Antwoorden op waarschuwingen in OMS Log Analytics | Microsoft Docs
description: Waarschuwingen in logboekanalyse kunnen belangrijke informatie in de OMS-opslagplaats te identificeren en proactief zullen u informeren over problemen of acties uit om te proberen op te lossen ze aanroepen.  In dit artikel beschrijft het maken van een waarschuwingsregel en details van de verschillende acties die ze kunnen ondernemen.
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
ms.openlocfilehash: b8731e1fe48b7d809b113eb5273e3962542b8f34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-actions-to-alert-rules-in-log-analytics"></a><span data-ttu-id="ea64a-104">Acties toevoegen aan de regels voor waarschuwingen in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ea64a-104">Add actions to alert rules in Log Analytics</span></span>
<span data-ttu-id="ea64a-105">Wanneer een [waarschuwing is gemaakt in logboekanalyse](log-analytics-alerts.md), hebt u de optie [configureren van de waarschuwingsregel](log-analytics-alerts.md) een of meer acties uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ea64a-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have the option of [configuring the alert rule](log-analytics-alerts.md) to perform one or more actions.</span></span>  <span data-ttu-id="ea64a-106">In dit artikel beschrijft de verschillende acties die beschikbaar zijn en meer informatie over het configureren van elk type.</span><span class="sxs-lookup"><span data-stu-id="ea64a-106">This article describes the different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="ea64a-107">Actie</span><span class="sxs-lookup"><span data-stu-id="ea64a-107">Action</span></span> | <span data-ttu-id="ea64a-108">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ea64a-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="ea64a-109">E-mail</span><span class="sxs-lookup"><span data-stu-id="ea64a-109">Email</span></span>](#email-actions) | <span data-ttu-id="ea64a-110">Verzend een e-mailbericht met de details van de waarschuwing naar een of meer geadresseerden.</span><span class="sxs-lookup"><span data-stu-id="ea64a-110">Send an e-mail with the details of the alert to one or more recipients.</span></span> |
| [<span data-ttu-id="ea64a-111">Webhook</span><span class="sxs-lookup"><span data-stu-id="ea64a-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="ea64a-112">Een extern proces via één HTTP POST-aanvraag worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ea64a-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="ea64a-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="ea64a-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="ea64a-114">Starten van een runbook in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ea64a-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="ea64a-115">E-acties</span><span class="sxs-lookup"><span data-stu-id="ea64a-115">Email actions</span></span>
<span data-ttu-id="ea64a-116">E-acties verzend een e-mailbericht met de details van de waarschuwing naar een of meer geadresseerden.</span><span class="sxs-lookup"><span data-stu-id="ea64a-116">Email actions send an e-mail with the details of the alert to one or more recipients.</span></span>  <span data-ttu-id="ea64a-117">Kunt u het onderwerp van het e-mailbericht, maar de inhoud is een standaardindeling samengesteld door logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="ea64a-117">You can specify the subject of the mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="ea64a-118">Dit omvat samenvattende informatie zoals de naam van de waarschuwing naast de details van maximaal tien records geretourneerd door het logboek zoeken.</span><span class="sxs-lookup"><span data-stu-id="ea64a-118">It includes summary information such as the name of the alert in addition to details of up to ten records returned by the log search.</span></span>  <span data-ttu-id="ea64a-119">Het bevat ook een koppeling naar een zoekopdracht logboek logboekanalyse dat de volledige set van records uit de query die wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ea64a-119">It also includes a link to a log search in Log Analytics that will return the entire set of records from that query.</span></span>   <span data-ttu-id="ea64a-120">De afzender van het e-mailbericht is *Microsoft Operations Management Suite-Team &lt; noreply@oms.microsoft.com &gt;* .</span><span class="sxs-lookup"><span data-stu-id="ea64a-120">The sender of the mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="ea64a-121">E-bewerkingen moet de eigenschappen in de volgende tabel.</span><span class="sxs-lookup"><span data-stu-id="ea64a-121">Email actions require the properties in the following table.</span></span>

| <span data-ttu-id="ea64a-122">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ea64a-122">Property</span></span> | <span data-ttu-id="ea64a-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ea64a-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ea64a-124">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="ea64a-124">Subject</span></span> |<span data-ttu-id="ea64a-125">Onderwerpen in het e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="ea64a-125">Subject in the email.</span></span>  <span data-ttu-id="ea64a-126">U kunt de hoofdtekst van het e-mailbericht niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ea64a-126">You cannot modify the body of the mail.</span></span> |
| <span data-ttu-id="ea64a-127">ontvangers</span><span class="sxs-lookup"><span data-stu-id="ea64a-127">Recipients</span></span> |<span data-ttu-id="ea64a-128">De adressen van alle e-mailgeadresseerden.</span><span class="sxs-lookup"><span data-stu-id="ea64a-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="ea64a-129">Als u meer dan één adres opgeeft, scheidt u de adressen met een puntkomma (;).</span><span class="sxs-lookup"><span data-stu-id="ea64a-129">If you specify more than one address, then separate the addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="ea64a-130">Webhookacties</span><span class="sxs-lookup"><span data-stu-id="ea64a-130">Webhook actions</span></span>

<span data-ttu-id="ea64a-131">Webhookacties kunnen u een extern proces via één HTTP POST-aanvraag worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ea64a-131">Webhook actions allow you to invoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="ea64a-132">De service die wordt aangeroepen moet webhooks ondersteunen en bepaal hoe het door middel van elke nettolading wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="ea64a-132">The service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="ea64a-133">U kunt ook een REST-API die niet specifiek webhooks ondersteunt, zolang de aanvraag heeft een indeling die werkt met de API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="ea64a-133">You could also call a REST API that doesn't specifically support webhooks as long as the request is in a format that the API understands.</span></span>  <span data-ttu-id="ea64a-134">Voorbeelden van het gebruik van een webhook in reactie op een waarschuwing een bericht verzendt [Slack](http://slack.com) of het maken van een incident in [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="ea64a-134">Examples of using a webhook in response to an alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="ea64a-135">Een volledige procedure voor het maken van een waarschuwingsregel met een webhook aanroepen Slack is beschikbaar op [Webhooks in logboekanalyse waarschuwingen](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="ea64a-135">A complete walkthrough of creating an alert rule with a webhook to call Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="ea64a-136">Webhookacties vereisen de eigenschappen in de volgende tabel.</span><span class="sxs-lookup"><span data-stu-id="ea64a-136">Webhook actions require the properties in the following table.</span></span>

| <span data-ttu-id="ea64a-137">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ea64a-137">Property</span></span> | <span data-ttu-id="ea64a-138">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ea64a-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ea64a-139">Webhook-URL</span><span class="sxs-lookup"><span data-stu-id="ea64a-139">Webhook URL</span></span> |<span data-ttu-id="ea64a-140">De URL van de webhook.</span><span class="sxs-lookup"><span data-stu-id="ea64a-140">The URL of the webhook.</span></span> |
| <span data-ttu-id="ea64a-141">Aangepaste JSON-nettolading</span><span class="sxs-lookup"><span data-stu-id="ea64a-141">Custom JSON payload</span></span> |<span data-ttu-id="ea64a-142">Aangepaste nettolading met de webhook moeten worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="ea64a-142">Custom payload to send with the webhook.</span></span>  <span data-ttu-id="ea64a-143">Zie hieronder voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ea64a-143">See below for details.</span></span> |


<span data-ttu-id="ea64a-144">Webhooks omvatten een URL en een nettolading opgemaakt in JSON is de gegevens naar de externe service verzonden.</span><span class="sxs-lookup"><span data-stu-id="ea64a-144">Webhooks include a URL and a payload formatted in JSON that is the data sent to the external service.</span></span>  <span data-ttu-id="ea64a-145">De nettolading van de neemt standaard de waarden in de volgende tabel.</span><span class="sxs-lookup"><span data-stu-id="ea64a-145">By default, the payload will include the values in the following table.</span></span>  <span data-ttu-id="ea64a-146">U kunt deze nettolading vervangen door een aangepaste van uzelf.</span><span class="sxs-lookup"><span data-stu-id="ea64a-146">You can choose to replace this payload with a custom one of your own.</span></span>  <span data-ttu-id="ea64a-147">In dat geval kunt u de variabelen in de tabel voor elk van de parameters voor hun waarde bevatten in de aangepaste nettolading.</span><span class="sxs-lookup"><span data-stu-id="ea64a-147">In that case you can use the variables in the table for each of the parameters to include their value in your custom payload.</span></span>

| <span data-ttu-id="ea64a-148">Parameter</span><span class="sxs-lookup"><span data-stu-id="ea64a-148">Parameter</span></span> | <span data-ttu-id="ea64a-149">Variabele</span><span class="sxs-lookup"><span data-stu-id="ea64a-149">Variable</span></span> | <span data-ttu-id="ea64a-150">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ea64a-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ea64a-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="ea64a-151">AlertRuleName</span></span> |<span data-ttu-id="ea64a-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="ea64a-152">#alertrulename</span></span> |<span data-ttu-id="ea64a-153">Naam van de waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="ea64a-153">Name of the alert rule.</span></span> |
| <span data-ttu-id="ea64a-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="ea64a-154">AlertThresholdOperator</span></span> |<span data-ttu-id="ea64a-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="ea64a-155">#thresholdoperator</span></span> |<span data-ttu-id="ea64a-156">Drempelwaarde voor de operator voor de waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="ea64a-156">Threshold operator for the alert rule.</span></span>  <span data-ttu-id="ea64a-157">*Groter dan* of *minder dan*.</span><span class="sxs-lookup"><span data-stu-id="ea64a-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="ea64a-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="ea64a-158">AlertThresholdValue</span></span> |<span data-ttu-id="ea64a-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="ea64a-159">#thresholdvalue</span></span> |<span data-ttu-id="ea64a-160">Drempelwaarde voor de waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="ea64a-160">Threshold value for the alert rule.</span></span> |
| <span data-ttu-id="ea64a-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="ea64a-161">LinkToSearchResults</span></span> |<span data-ttu-id="ea64a-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="ea64a-162">#linktosearchresults</span></span> |<span data-ttu-id="ea64a-163">Koppelen aan logboekanalyse logboek zoeken waarmee de records geretourneerd van de query die de waarschuwing wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ea64a-163">Link to Log Analytics log search that returns the records from the query that created the alert.</span></span> |
| <span data-ttu-id="ea64a-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="ea64a-164">ResultCount</span></span> |<span data-ttu-id="ea64a-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="ea64a-165">#searchresultcount</span></span> |<span data-ttu-id="ea64a-166">Het aantal records in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="ea64a-166">Number of records in the search results.</span></span> |
| <span data-ttu-id="ea64a-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="ea64a-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="ea64a-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="ea64a-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="ea64a-169">De eindtijd voor de query in UTC-notatie.</span><span class="sxs-lookup"><span data-stu-id="ea64a-169">End time for the query in UTC format.</span></span> |
| <span data-ttu-id="ea64a-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="ea64a-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="ea64a-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="ea64a-171">#searchinterval</span></span> |<span data-ttu-id="ea64a-172">Tijdvenster voor de waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="ea64a-172">Time window for the alert rule.</span></span> |
| <span data-ttu-id="ea64a-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="ea64a-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="ea64a-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="ea64a-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="ea64a-175">Begintijd voor de query in UTC-notatie.</span><span class="sxs-lookup"><span data-stu-id="ea64a-175">Start time for the query in UTC format.</span></span> |
| <span data-ttu-id="ea64a-176">searchQuery</span><span class="sxs-lookup"><span data-stu-id="ea64a-176">SearchQuery</span></span> |<span data-ttu-id="ea64a-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="ea64a-177">#searchquery</span></span> |<span data-ttu-id="ea64a-178">Logboek zoekquery gebruikt door de waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="ea64a-178">Log search query used by the alert rule.</span></span> |
| <span data-ttu-id="ea64a-179">Zoekresultaten</span><span class="sxs-lookup"><span data-stu-id="ea64a-179">SearchResults</span></span> |<span data-ttu-id="ea64a-180">Hieronder vindt u de</span><span class="sxs-lookup"><span data-stu-id="ea64a-180">See below</span></span> |<span data-ttu-id="ea64a-181">Records geretourneerd door de query in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="ea64a-181">Records returned by the query in JSON format.</span></span>  <span data-ttu-id="ea64a-182">Beperkt tot de eerste 5000 records.</span><span class="sxs-lookup"><span data-stu-id="ea64a-182">Limited to the first 5,000 records.</span></span> |
| <span data-ttu-id="ea64a-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="ea64a-183">WorkspaceID</span></span> |<span data-ttu-id="ea64a-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="ea64a-184">#workspaceid</span></span> |<span data-ttu-id="ea64a-185">ID van de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="ea64a-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="ea64a-186">Bijvoorbeeld, kunt u opgeven de volgende aangepaste nettolading met een enkele parameter aangeroepen *tekst*.</span><span class="sxs-lookup"><span data-stu-id="ea64a-186">For example, you might specify the following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="ea64a-187">De service die deze webhook aanroepen, zou deze parameter worden verwacht.</span><span class="sxs-lookup"><span data-stu-id="ea64a-187">The service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="ea64a-188">De nettolading van dit voorbeeld zou worden omgezet naar ongeveer het volgende wanneer u naar de webhook verzonden.</span><span class="sxs-lookup"><span data-stu-id="ea64a-188">This example payload would resolve to something like the following when sent to the webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="ea64a-189">Als u wilt opnemen zoekresultaten in een aangepaste nettolading, voeg de volgende regel als een eigenschap van het hoogste niveau in de json-nettolading.</span><span class="sxs-lookup"><span data-stu-id="ea64a-189">To include search results in a custom payload, add the following line as a top level property in the json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="ea64a-190">Bijvoorbeeld: voor het maken van een aangepaste nettolading met alleen de naam van de waarschuwing en de zoekresultaten, u kunt de volgende.</span><span class="sxs-lookup"><span data-stu-id="ea64a-190">For example, to create a custom payload that includes just the alert name and the search results, you could use the following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="ea64a-191">U kunt een compleet voorbeeld van een waarschuwingsregel maken met een webhook om een externe service op te starten doorlopen [maken van een actie waarschuwing webhook in OMS Log Analytics bericht te verzenden naar Slack](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="ea64a-191">You can walk through a complete example of creating an alert rule with a webhook to start an external service at [Create an alert webhook action in OMS Log Analytics to send message to Slack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="ea64a-192">Runbook-acties</span><span class="sxs-lookup"><span data-stu-id="ea64a-192">Runbook actions</span></span>
<span data-ttu-id="ea64a-193">Runbook-acties starten van een runbook in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ea64a-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="ea64a-194">Om dit type actie gebruiken, hebt u de [Automation-oplossing](log-analytics-add-solutions.md) geïnstalleerd en geconfigureerd in de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="ea64a-194">In order to use this type of action, you must have the [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="ea64a-195">U kunt kiezen uit de runbooks in het automation-account die u hebt geconfigureerd in de Automation-oplossing.</span><span class="sxs-lookup"><span data-stu-id="ea64a-195">You can select from the runbooks in the automation account that you configured in the Automation solution.</span></span>

<span data-ttu-id="ea64a-196">Runbook-bewerkingen moet de eigenschappen in de volgende tabel.</span><span class="sxs-lookup"><span data-stu-id="ea64a-196">Runbook actions require the properties in the following table.</span></span>

| <span data-ttu-id="ea64a-197">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ea64a-197">Property</span></span> | <span data-ttu-id="ea64a-198">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ea64a-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="ea64a-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="ea64a-199">Runbook</span></span> | <span data-ttu-id="ea64a-200">Een Runbook dat u starten wilt wanneer een waarschuwing wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ea64a-200">Runbook that you want to start when an alert is created.</span></span> |
| <span data-ttu-id="ea64a-201">Voer op</span><span class="sxs-lookup"><span data-stu-id="ea64a-201">Run on</span></span> | <span data-ttu-id="ea64a-202">Geef **Azure** voor het uitvoeren van het runbook in de cloud.</span><span class="sxs-lookup"><span data-stu-id="ea64a-202">Specify **Azure** to run the runbook in the cloud.</span></span>  <span data-ttu-id="ea64a-203">Geef **hybride worker** voor het uitvoeren van het runbook op een agent met [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ea64a-203">Specify **Hybrid worker** to run the runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="ea64a-204">Runbook-acties, start het runbook met behulp van een [webhook](../automation/automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="ea64a-204">Runbook actions start the runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="ea64a-205">Wanneer u de waarschuwingsregel maakt, wordt deze automatisch een nieuwe webhook voor het runbook maken met de naam **OMS waarschuwing herstel** gevolgd door een GUID.</span><span class="sxs-lookup"><span data-stu-id="ea64a-205">When you create the alert rule, it will automatically create a new webhook for the runbook with the name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="ea64a-206">U kan niet rechtstreeks vullen met de parameters van het runbook, maar de [$WebhookData parameter](../automation/automation-webhooks.md) bevat de details van de waarschuwing, met inbegrip van de resultaten van de zoekopdracht logboek waarvan deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ea64a-206">You cannot directly populate any parameters of the runbook, but the [$WebhookData parameter](../automation/automation-webhooks.md) will include the details of the alert, including the results of the log search that created it.</span></span>  <span data-ttu-id="ea64a-207">Het runbook moet definiëren **$WebhookData** als parameter voor deze toegang krijgt tot de eigenschappen van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="ea64a-207">The runbook will need to define **$WebhookData** as a parameter for it to access the properties of the alert.</span></span>  <span data-ttu-id="ea64a-208">Gegevens van de waarschuwing is beschikbaar in json-indeling in één eigenschap aangeroepen **zoekresultaten** in de **RequestBody** eigenschap van **$WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="ea64a-208">The alert data is available in json format in a single property called **SearchResults** in the **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="ea64a-209">Dit heeft met de eigenschappen in de volgende tabel.</span><span class="sxs-lookup"><span data-stu-id="ea64a-209">This will have with the properties in the following table.</span></span>

| <span data-ttu-id="ea64a-210">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="ea64a-210">Node</span></span> | <span data-ttu-id="ea64a-211">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ea64a-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ea64a-212">id</span><span class="sxs-lookup"><span data-stu-id="ea64a-212">id</span></span> |<span data-ttu-id="ea64a-213">Pad en de GUID van de zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="ea64a-213">Path and GUID of the search.</span></span> |
| <span data-ttu-id="ea64a-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="ea64a-214">__metadata</span></span> |<span data-ttu-id="ea64a-215">Informatie over de waarschuwing waaronder het aantal records en status van de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="ea64a-215">Information about the alert including the number of records and status of the search results.</span></span> |
| <span data-ttu-id="ea64a-216">waarde</span><span class="sxs-lookup"><span data-stu-id="ea64a-216">value</span></span> |<span data-ttu-id="ea64a-217">Afzonderlijke vermelding voor elke record in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="ea64a-217">Separate entry for each record in the search results.</span></span>  <span data-ttu-id="ea64a-218">De details van het item komt overeen met de eigenschappen en waarden van de record.</span><span class="sxs-lookup"><span data-stu-id="ea64a-218">The details of the entry will match the properties and values of the record.</span></span> |

<span data-ttu-id="ea64a-219">De volgende runbook zou bijvoorbeeld uitpakken van de records geretourneerd door het logboek zoeken en toewijzen van andere eigenschappen op basis van het type van elke record.</span><span class="sxs-lookup"><span data-stu-id="ea64a-219">For example, the following runbook would extract the records returned by the log search  and assign different properties based on the type of each record.</span></span>  <span data-ttu-id="ea64a-220">Denk eraan dat het runbook met het converteren van begint **RequestBody** van json zodanig dat deze kan worden gewerkt met als een object in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea64a-220">Note that the runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="ea64a-221">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ea64a-221">Next steps</span></span>
- <span data-ttu-id="ea64a-222">Een stapsgewijze Kennismaking voltooien [configureren van een webook](log-analytics-alerts-webhooks.md) met een waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="ea64a-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="ea64a-223">Meer informatie over het schrijven van [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) oplossen van problemen die worden aangeduid met waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="ea64a-223">Learn how to write [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) to remediate problems identified by alerts.</span></span>