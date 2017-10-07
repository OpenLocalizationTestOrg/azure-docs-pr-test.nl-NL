---
title: aaaStream Azure diagnostische logboeken tooan Event Hubs Namespace | Microsoft Docs
description: Meer informatie over hoe toostream diagnostische Azure Event Hubs-naamruimte tooan registreert.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a><span data-ttu-id="bfbab-103">Tooan diagnostische logboeken van Azure Event Hubs Namespace Stream</span><span class="sxs-lookup"><span data-stu-id="bfbab-103">Stream Azure Diagnostic Logs tooan Event Hubs Namespace</span></span>
<span data-ttu-id="bfbab-104">**[Azure diagnostische logboeken](monitoring-overview-of-diagnostic-logs.md)**  kan worden gestreamd bijna realtime tooany toepassing hello ingebouwde ' tooEvent Hubs ' optie exporteren in Hallo Portal of door in te schakelen Hallo Service Bus-regel-ID in een diagnostische instelling via hello Azure PowerShell Cmdlets of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bfbab-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time tooany application using hello built-in “Export tooEvent Hubs” option in hello Portal, or by enabling hello Service Bus Rule ID in a diagnostic setting via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="bfbab-105">Wat u kunt doen met Logboeken met diagnostische en Event Hubs</span><span class="sxs-lookup"><span data-stu-id="bfbab-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="bfbab-106">Hier volgen slechts enkele manieren waarop u Hallo mogelijkheid streaming voor diagnostische logboeken kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bfbab-106">Here are just a few ways you might use hello streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="bfbab-107">**Stroom logboeken logboekregistratie en telemetrie-systemen van derden too3rd** – gedurende een periode, streaming van Event Hubs wordt Hallo mechanisme toopipe worden uw diagnoselogboeken in toothird derden siem's en meld u analytics-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="bfbab-107">**Stream logs too3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your diagnostic logs in toothird-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="bfbab-108">**Servicestatus weergeven door het streaming 'hot pad' data tooPowerBI** – met behulp van Event Hubs, Stream Analytics en Power BI, u kunt eenvoudig uw diagnostics-gegevens in realtime-inzichten toonear transformeren op uw Azure-services.</span><span class="sxs-lookup"><span data-stu-id="bfbab-108">**View service health by streaming “hot path” data tooPowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in toonear real-time insights on your Azure services.</span></span> <span data-ttu-id="bfbab-109">[Deze documentatie-artikel biedt een goed overzicht van hoe tooset van Event Hubs verwerken van gegevens met Stream Analytics en Power BI te gebruiken als uitvoer](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="bfbab-109">[This documentation article gives a great overview of how tooset up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="bfbab-110">Hier volgen enkele tips voor het ophalen van instellen met Logboeken met diagnostische gegevens:</span><span class="sxs-lookup"><span data-stu-id="bfbab-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="bfbab-111">Een event hub voor een categorie van diagnostische logboeken wordt automatisch gemaakt wanneer u Hallo optie in de portal Hallo controleren of via PowerShell, inschakelen dus u tooselect Hallo event hub in de Hallo-naamruimte met Hallo-naam die met begint wilt **insights**.</span><span class="sxs-lookup"><span data-stu-id="bfbab-111">An event hub for a category of diagnostic logs is created automatically when you check hello option in hello portal or enable it through PowerShell, so you want tooselect hello event hub in hello namespace with hello name that starts with **insights-**.</span></span>
  * <span data-ttu-id="bfbab-112">Hallo volgende SQL-code is een voorbeeld van een Stream Analytics query waarmee u tooparse alle Hallo logboekgegevens in tooa PowerBI-tabel kunt:</span><span class="sxs-lookup"><span data-stu-id="bfbab-112">hello following SQL code is a sample Stream Analytics query that you can use tooparse all hello log data in tooa PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="bfbab-113">**Maken van een aangepaste Telemetrie en logboekregistratie platform** : als u al een op maat gemaakte telemetrie-platform of diagnostische zijn alleen rekening houdt met een uiterst schaalbare Hallo voor publiceren / abonneren gebouw aard van Event Hubs kunt u tooflexibly opnemen de logboeken.</span><span class="sxs-lookup"><span data-stu-id="bfbab-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="bfbab-114">[Zie de Dan Rosanova handleiding toousing Event Hubs in een wereldwijde schaal telemetrie platform hier](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="bfbab-114">[See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="bfbab-115">Streaming van logboeken met diagnostische gegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="bfbab-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="bfbab-116">U kunt inschakelen streaming van diagnostische logboeken programmatisch via Hallo-portal of met behulp van Hallo [Monitor REST-API's van Azure](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span><span class="sxs-lookup"><span data-stu-id="bfbab-116">You can enable streaming of diagnostic logs programmatically, via hello portal, or using hello [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="bfbab-117">In beide gevallen moet u een diagnostische instelling maken waarin u een naamruimte Event Hubs en Hallo logboek categorieën en metrische gegevens die u wilt dat toosend in toohello naamruimte opgeven.</span><span class="sxs-lookup"><span data-stu-id="bfbab-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and hello log categories and metrics you want toosend in toohello namespace.</span></span> <span data-ttu-id="bfbab-118">Een event hub wordt gemaakt in de naamruimte Hallo voor elke categorie logboek is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="bfbab-118">An event hub is created in hello namespace for each log category you enable.</span></span> <span data-ttu-id="bfbab-119">Een diagnose **logboek categorie** is een type-log dat een resource kan verzamelen.</span><span class="sxs-lookup"><span data-stu-id="bfbab-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="bfbab-120">Inschakelen en streaming van diagnostische logboeken van rekenresources (bijvoorbeeld virtuele machines of Service Fabric) [vereist een andere set stappen](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="bfbab-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="bfbab-121">Hello Service Bus- of Event Hubs naamruimte heeft geen toobe in Hallo hetzelfde abonnement als Hallo resource logboeken verzenden zolang Hallo-gebruiker die Hallo instelling configureert de juiste RBAC toegang tooboth abonnementen heeft.</span><span class="sxs-lookup"><span data-stu-id="bfbab-121">hello Service Bus or Event Hubs namespace does not have toobe in hello same subscription as hello resource emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-hello-portal"></a><span data-ttu-id="bfbab-122">Stroom diagnostische logboeken met Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="bfbab-122">Stream diagnostic logs using hello portal</span></span>
1. <span data-ttu-id="bfbab-123">Navigeer tooAzure Monitor in Hallo-portal en klikt u op **diagnostische instellingen**</span><span class="sxs-lookup"><span data-stu-id="bfbab-123">In hello portal, navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Sectie van de Monitor Azure bewaking](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="bfbab-125">Eventueel Hallo lijst filteren op resourcegroep of brontype en klik vervolgens op Hallo resource waarvoor u een diagnostische instelling tooset wilt.</span><span class="sxs-lookup"><span data-stu-id="bfbab-125">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="bfbab-126">Als u geen instellingen bestaat op het Hallo-resource die u hebt geselecteerd, bent u na vragen aan gebruiker toocreate een instelling.</span><span class="sxs-lookup"><span data-stu-id="bfbab-126">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="bfbab-127">Klik op "Diagnostische gegevens inschakelen."</span><span class="sxs-lookup"><span data-stu-id="bfbab-127">Click "Turn on diagnostics."</span></span>

   ![Diagnostische instelling - geen bestaande instellingen toevoegen](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="bfbab-129">Als er bestaande instellingen op Hallo resource, ziet u een lijst met instellingen die al zijn geconfigureerd op deze resource.</span><span class="sxs-lookup"><span data-stu-id="bfbab-129">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="bfbab-130">Klik op 'Diagnostische instelling toevoegen'.</span><span class="sxs-lookup"><span data-stu-id="bfbab-130">Click "Add diagnostic setting."</span></span>

   ![Diagnostische instelling - bestaande instellingen toevoegen](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="bfbab-132">Geef een naam van de instelling en Hallo selectievakje voor **stroom tooan event hub**, selecteer vervolgens een Event Hubs-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="bfbab-132">Give your setting a name and check hello box for **Stream tooan event hub**, then select an Event Hubs namespace.</span></span>
   
   ![Diagnostische instelling - bestaande instellingen toevoegen](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="bfbab-134">Hallo naamruimte hebt geselecteerd, zijn waar Hallo event hub is gemaakt (als dit de eerste keer diagnostische logboeken streaming is) of gestreamd te (als er nog resources die zijn die naamruimte logboek categorie toothis streaming), en beleid Hallo Hallo definieert machtigingen die Hallo streaming mechanisme heeft.</span><span class="sxs-lookup"><span data-stu-id="bfbab-134">hello namespace selected will be where hello event hub is created (if this is your first time streaming diagnostic logs) or streamed too(if there are already resources that are streaming that log category toothis namespace), and hello policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="bfbab-135">Vandaag de dag vereist tooan streaming event hub machtigingen beheren, verzenden en luisteren.</span><span class="sxs-lookup"><span data-stu-id="bfbab-135">Today, streaming tooan event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="bfbab-136">U kunt maken of wijzigen van Event Hubs naamruimte gedeeld toegangsbeleid in Hallo-beheerportal onder tabblad Hallo-configureren voor de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="bfbab-136">You can create or modify Event Hubs namespace shared access policies in hello portal under hello Configure tab for your namespace.</span></span> <span data-ttu-id="bfbab-137">tooupdate een van deze diagnostische instellingen, Hallo-client moet gemachtigd Hallo ListKey op Hallo Event Hubs-autorisatieregel.</span><span class="sxs-lookup"><span data-stu-id="bfbab-137">tooupdate one of these diagnostic settings, hello client must have hello ListKey permission on hello Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="bfbab-138">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bfbab-138">Click **Save**.</span></span>

<span data-ttu-id="bfbab-139">Na enkele ogenblikken Hallo nieuwe instelling wordt weergegeven in de lijst met instellingen voor deze bron en diagnostische logboeken toothat storage-account worden gestreamd zodra er nieuwe gebeurtenisgegevens wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="bfbab-139">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are streamed toothat storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="bfbab-140">Via PowerShell-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="bfbab-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="bfbab-141">streaming via Hallo tooenable [Azure PowerShell-Cmdlets](insights-powershell-samples.md), kunt u Hallo `Set-AzureRmDiagnosticSetting` cmdlet met de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="bfbab-141">tooenable streaming via hello [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use hello `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="bfbab-142">Hallo Service Bus regel-ID is een tekenreeks met deze indeling: `{Service Bus resource ID}/authorizationrules/{key name}`, bijvoorbeeld `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="bfbab-142">hello Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="bfbab-143">Via Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bfbab-143">Via Azure CLI</span></span>
<span data-ttu-id="bfbab-144">streaming via Hallo tooenable [Azure CLI](insights-cli-samples.md), kunt u Hallo `insights diagnostic set` opdracht als volgt:</span><span class="sxs-lookup"><span data-stu-id="bfbab-144">tooenable streaming via hello [Azure CLI](insights-cli-samples.md), you can use hello `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="bfbab-145">Hallo dezelfde notatie voor Service Bus regel-ID, zoals uitgelegd voor Hallo PowerShell-Cmdlet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bfbab-145">Use hello same format for Service Bus Rule ID as explained for hello PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="bfbab-146">Hoe ik Hallo logboekgegevens van Event Hubs verbruiken?</span><span class="sxs-lookup"><span data-stu-id="bfbab-146">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="bfbab-147">Hier volgt een voorbeeld uitvoergegevens van Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="bfbab-147">Here is sample output data from Event Hubs:</span></span>

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| <span data-ttu-id="bfbab-148">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="bfbab-148">Element Name</span></span> | <span data-ttu-id="bfbab-149">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bfbab-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bfbab-150">records</span><span class="sxs-lookup"><span data-stu-id="bfbab-150">records</span></span> |<span data-ttu-id="bfbab-151">Een matrix met alle gebeurtenissen in deze nettolading.</span><span class="sxs-lookup"><span data-stu-id="bfbab-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="bfbab-152">tijd</span><span class="sxs-lookup"><span data-stu-id="bfbab-152">time</span></span> |<span data-ttu-id="bfbab-153">Tijd waarop hello gebeurtenis heeft plaatsgevonden.</span><span class="sxs-lookup"><span data-stu-id="bfbab-153">Time at which hello event occurred.</span></span> |
| <span data-ttu-id="bfbab-154">category</span><span class="sxs-lookup"><span data-stu-id="bfbab-154">category</span></span> |<span data-ttu-id="bfbab-155">De categorie van het logboek voor deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="bfbab-155">Log category for this event.</span></span> |
| <span data-ttu-id="bfbab-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="bfbab-156">resourceId</span></span> |<span data-ttu-id="bfbab-157">Bron-ID van het Hallo-bron die deze gebeurtenis wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="bfbab-157">Resource ID of hello resource that generated this event.</span></span> |
| <span data-ttu-id="bfbab-158">operationName</span><span class="sxs-lookup"><span data-stu-id="bfbab-158">operationName</span></span> |<span data-ttu-id="bfbab-159">Naam van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="bfbab-159">Name of hello operation.</span></span> |
| <span data-ttu-id="bfbab-160">niveau</span><span class="sxs-lookup"><span data-stu-id="bfbab-160">level</span></span> |<span data-ttu-id="bfbab-161">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="bfbab-161">Optional.</span></span> <span data-ttu-id="bfbab-162">Hiermee wordt aangegeven Hallo gebeurtenis logboekniveau.</span><span class="sxs-lookup"><span data-stu-id="bfbab-162">Indicates hello log event level.</span></span> |
| <span data-ttu-id="bfbab-163">properties</span><span class="sxs-lookup"><span data-stu-id="bfbab-163">properties</span></span> |<span data-ttu-id="bfbab-164">Eigenschappen van gebeurtenis Hallo.</span><span class="sxs-lookup"><span data-stu-id="bfbab-164">Properties of hello event.</span></span> |

<span data-ttu-id="bfbab-165">U kunt een lijst weergeven met alle resourceproviders die ondersteuning bieden voor streaming tooEvent Hubs [hier](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="bfbab-165">You can view a list of all resource providers that support streaming tooEvent Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="bfbab-166">Stroomgegevens van rekenresources</span><span class="sxs-lookup"><span data-stu-id="bfbab-166">Stream data from Compute resources</span></span>
<span data-ttu-id="bfbab-167">U kunt ook diagnostische logboeken van rekenresources met behulp van Windows Azure Diagnostics-agent Hallo streamen.</span><span class="sxs-lookup"><span data-stu-id="bfbab-167">You can also stream diagnostic logs from Compute resources using hello Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="bfbab-168">[Raadpleeg dit artikel](../event-hubs/event-hubs-streaming-azure-diags-data.md) voor het tooset die omhoog.</span><span class="sxs-lookup"><span data-stu-id="bfbab-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how tooset that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfbab-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bfbab-169">Next steps</span></span>
* [<span data-ttu-id="bfbab-170">Meer informatie over Azure diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="bfbab-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="bfbab-171">Aan de slag met Event Hubs</span><span class="sxs-lookup"><span data-stu-id="bfbab-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

