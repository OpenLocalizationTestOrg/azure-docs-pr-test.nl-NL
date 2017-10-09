---
title: waarschuwingen voor Azure-services - PowerShell aaaCreate | Microsoft Docs
description: Trigger e-mailberichten, meldingen, worden URL's van websites (webhooks) of automation aanroepen wanneer Hallo door u opgegeven voorwaarden wordt voldaan.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="2af0b-103">Metrische waarschuwingen in de Azure-Monitor maken voor Azure-services - PowerShell</span><span class="sxs-lookup"><span data-stu-id="2af0b-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2af0b-104">Portal</span><span class="sxs-lookup"><span data-stu-id="2af0b-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="2af0b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2af0b-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="2af0b-106">CLI</span><span class="sxs-lookup"><span data-stu-id="2af0b-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="2af0b-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2af0b-107">Overview</span></span>
<span data-ttu-id="2af0b-108">Dit artikel laat zien hoe tooset up Azure metriek waarschuwingen met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2af0b-108">This article shows you how tooset up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="2af0b-109">U kunt een waarschuwing op basis van bewaking metrische gegevens voor of gebeurtenissen op uw Azure-services kunt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="2af0b-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="2af0b-110">**Metrische waarden** - hello triggers waarschuwen wanneer Hallo-waarde van een opgegeven metriek overschrijdt de drempelwaarde die u in beide richtingen toewijst.</span><span class="sxs-lookup"><span data-stu-id="2af0b-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="2af0b-111">Dat wil zeggen, deze beide wordt geactiveerd wanneer eerst aan Hallo voorwaarde wordt voldaan en vervolgens later wanneer die voorwaarde wordt niet langer wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="2af0b-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="2af0b-112">**Activiteit logboekgebeurtenissen** -een waarschuwing kunt activeren voor *elke* gebeurtenis of alleen wanneer een bepaalde gebeurtenissen optreden.</span><span class="sxs-lookup"><span data-stu-id="2af0b-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="2af0b-113">meer informatie over de activiteit logboek waarschuwingen toolearn [Klik hier](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="2af0b-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="2af0b-114">Een metriek waarschuwing toodo Hallo volgen wanneer deze wordt geactiveerd, kunt u configureren:</span><span class="sxs-lookup"><span data-stu-id="2af0b-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="2af0b-115">verzenden van e-mailmeldingen toohello servicebeheerder en medebeheerders</span><span class="sxs-lookup"><span data-stu-id="2af0b-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="2af0b-116">e-mail verzenden tooadditional e-mails die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="2af0b-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="2af0b-117">een webhook aanroepen</span><span class="sxs-lookup"><span data-stu-id="2af0b-117">call a webhook</span></span>
* <span data-ttu-id="2af0b-118">starten van de uitvoering van een Azure-runbook (alleen van hello Azure-portal)</span><span class="sxs-lookup"><span data-stu-id="2af0b-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="2af0b-119">U kunt configureren en informatie ophalen over met behulp van regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="2af0b-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="2af0b-120">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2af0b-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="2af0b-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2af0b-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="2af0b-122">opdrachtregelinterface (CLI)</span><span class="sxs-lookup"><span data-stu-id="2af0b-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="2af0b-123">Monitor voor Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="2af0b-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="2af0b-124">Voor meer informatie, kunt u altijd typen ```Get-Help``` en vervolgens Hallo PowerShell-opdracht op het gewenste help.</span><span class="sxs-lookup"><span data-stu-id="2af0b-124">For additional information, you can always type ```Get-Help``` and then hello PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="2af0b-125">Maken van regels voor waarschuwingen in PowerShell</span><span class="sxs-lookup"><span data-stu-id="2af0b-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="2af0b-126">Meld u bij tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2af0b-126">Log in tooAzure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="2af0b-127">Een lijst met abonnementen Hallo er beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="2af0b-127">Get a list of hello subscriptions you have available.</span></span> <span data-ttu-id="2af0b-128">Controleer of u met het juiste abonnement Hallo werkt.</span><span class="sxs-lookup"><span data-stu-id="2af0b-128">Verify that you are working with hello right subscription.</span></span> <span data-ttu-id="2af0b-129">Als niet zo is, stelt u deze toohello rechts een met behulp van de uitvoer van Hallo `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="2af0b-129">If not, set it toohello right one using hello output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="2af0b-130">toolist bestaande regels voor een resourcegroep Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2af0b-130">toolist existing rules on a resource group, use hello following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="2af0b-131">toocreate een regel, moet u toohave belangrijke stukjes informatie eerst.</span><span class="sxs-lookup"><span data-stu-id="2af0b-131">toocreate a rule, you need toohave several important pieces of information first.</span></span>

  * <span data-ttu-id="2af0b-132">Hallo **Resource-ID** voor Hallo resource gewenste tooset een waarschuwing voor</span><span class="sxs-lookup"><span data-stu-id="2af0b-132">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="2af0b-133">Hallo **metrische definities** beschikbaar voor die bron</span><span class="sxs-lookup"><span data-stu-id="2af0b-133">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="2af0b-134">Eenzijdige tooget Hallo Resource-ID is toouse hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2af0b-134">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="2af0b-135">Hallo-bron ervan uitgaande dat al is gemaakt, selecteert u deze in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="2af0b-135">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="2af0b-136">Selecteer in de volgende blade Hallo *eigenschappen* onder Hallo *instellingen* sectie.</span><span class="sxs-lookup"><span data-stu-id="2af0b-136">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="2af0b-137">**De RESOURCE-ID** is een veld in de volgende Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="2af0b-137">**RESOURCE ID** is a field in hello next blade.</span></span> <span data-ttu-id="2af0b-138">Een andere manier is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2af0b-138">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="2af0b-139">Een voorbeeld van de Resource-ID voor een web-app is</span><span class="sxs-lookup"><span data-stu-id="2af0b-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="2af0b-140">U kunt `Get-AzureRmMetricDefinition` tooview Hallo lijst met alle metrische definities voor een specifieke bron.</span><span class="sxs-lookup"><span data-stu-id="2af0b-140">You can use `Get-AzureRmMetricDefinition` tooview hello list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="2af0b-141">Hallo volgende voorbeeld genereert een tabel met Hallo metriek naam en het Hallo eenheid voor deze metriek.</span><span class="sxs-lookup"><span data-stu-id="2af0b-141">hello following example generates a table with hello metric Name and hello Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="2af0b-142">Een volledige lijst met beschikbare opties voor Get-AzureRmMetricDefinition is beschikbaar door het uitvoeren van Get-MetricDefinitions.</span><span class="sxs-lookup"><span data-stu-id="2af0b-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="2af0b-143">Hallo volgende voorbeeld wordt u een waarschuwing voor een bron voor de website.</span><span class="sxs-lookup"><span data-stu-id="2af0b-143">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="2af0b-144">Hallo waarschuwing activeert wanneer het consistent verkeer ontvangt voor 5 minuten en opnieuw wanneer er geen verkeer ontvangen gedurende vijf minuten.</span><span class="sxs-lookup"><span data-stu-id="2af0b-144">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="2af0b-145">toocreate webhook verzenden e-mailadres of wanneer een waarschuwing activeert, maakt u eerst Hallo e-mailadres en/of webhooks.</span><span class="sxs-lookup"><span data-stu-id="2af0b-145">toocreate webhook or send email when an alert triggers, first create hello email and/or webhooks.</span></span> <span data-ttu-id="2af0b-146">Maak vervolgens onmiddellijk Hallo regel daarna met Hallo - tag acties en zoals weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="2af0b-146">Then immediately create hello rule afterwards with hello -Actions tag and as shown in hello following example.</span></span> <span data-ttu-id="2af0b-147">Kan geen koppelt u webhook of e-mailberichten met regels via PowerShell al is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2af0b-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="2af0b-148">tooverify dat uw waarschuwingen correct zijn gemaakt door te kijken Hallo afzonderlijke regels.</span><span class="sxs-lookup"><span data-stu-id="2af0b-148">tooverify that your alerts have been created properly by looking at hello individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="2af0b-149">Uw waarschuwingen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2af0b-149">Delete your alerts.</span></span> <span data-ttu-id="2af0b-150">Deze opdrachten verwijderen Hallo regels eerder hebt gemaakt in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="2af0b-150">These commands delete hello rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="2af0b-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2af0b-151">Next steps</span></span>
* <span data-ttu-id="2af0b-152">[Een overzicht van Azure monitoring](monitoring-overview.md) inclusief Hallo typen gegevens u kunt verzamelen en controleren.</span><span class="sxs-lookup"><span data-stu-id="2af0b-152">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="2af0b-153">Meer informatie over [configureren van webhooks in waarschuwingen](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="2af0b-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="2af0b-154">Meer informatie over [waarschuwingen configureren op activiteit logboekgebeurtenissen](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="2af0b-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="2af0b-155">Meer informatie over [Azure Automation-Runbooks](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="2af0b-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="2af0b-156">Ophalen van een [overzicht van het verzamelen van diagnostische logboeken](monitoring-overview-of-diagnostic-logs.md) toocollect gedetailleerde hoge frequentie metrische gegevens over uw service.</span><span class="sxs-lookup"><span data-stu-id="2af0b-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="2af0b-157">Ophalen van een [overzicht van metrische gegevens verzameling](insights-how-to-customize-monitoring.md) toomake ervoor dat uw service beschikbaar is en reageert.</span><span class="sxs-lookup"><span data-stu-id="2af0b-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
