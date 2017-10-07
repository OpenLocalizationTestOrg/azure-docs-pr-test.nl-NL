---
title: Voorbeelden van aaaAzure Monitor PowerShell snel starten. | Microsoft Docs
description: Gebruik PowerShell tooaccess Azure Monitor functies zoals automatisch schalen, waarschuwingen, webhooks en activiteitenlogboeken zoeken.
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="96b3f-104">Azure PowerShell Monitor snel starten-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="96b3f-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="96b3f-105">In dit artikel worden steekproef van PowerShell-opdrachten toohelp u toegang tot Azure Monitor functies.</span><span class="sxs-lookup"><span data-stu-id="96b3f-105">This article shows you sample PowerShell commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="96b3f-106">Monitor voor Azure kunt u tooAutoScale Cloudservices, virtuele Machines en Web-Apps en toosend waarschuwingsmeldingen of een aanroep van web-URL's op basis van waarden van de geconfigureerde telemetrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="96b3f-106">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="96b3f-107">Nieuwe naam op voor het zogenoemde 'Azure Insights' hello is Azure Monitor tot 25 september 2016.</span><span class="sxs-lookup"><span data-stu-id="96b3f-107">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="96b3f-108">Hallo-naamruimten en dus Hallo na opdrachten nog steeds echter bevatten Hallo 'insights'.</span><span class="sxs-lookup"><span data-stu-id="96b3f-108">However, hello namespaces and thus hello following commands still contain hello "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="96b3f-109">Instellen van PowerShell</span><span class="sxs-lookup"><span data-stu-id="96b3f-109">Set up PowerShell</span></span>
<span data-ttu-id="96b3f-110">Als u nog niet gedaan hebt, stelt u PowerShell toorun op uw computer.</span><span class="sxs-lookup"><span data-stu-id="96b3f-110">If you haven't already, set up PowerShell toorun on your computer.</span></span> <span data-ttu-id="96b3f-111">Zie voor meer informatie [hoe tooInstall en PowerShell configureren](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96b3f-111">For more information, see [How tooInstall and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="96b3f-112">Voorbeelden in dit artikel</span><span class="sxs-lookup"><span data-stu-id="96b3f-112">Examples in this article</span></span>
<span data-ttu-id="96b3f-113">Hallo-voorbeelden in Hallo artikel ziet u hoe u Azure Monitor cmdlets kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="96b3f-113">hello examples in hello article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="96b3f-114">U kunt ook de volledige lijst van Azure Monitor PowerShell-cmdlets op Hallo bekijken [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="96b3f-114">You can also review hello entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="96b3f-115">Aanmelden en abonnementen gebruiken</span><span class="sxs-lookup"><span data-stu-id="96b3f-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="96b3f-116">Meld u eerst in tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="96b3f-116">First, log in tooyour Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="96b3f-117">Hiervoor moet u toosign in.</span><span class="sxs-lookup"><span data-stu-id="96b3f-117">This requires you toosign in.</span></span> <span data-ttu-id="96b3f-118">Zodra u dit, uw Account doet worden TenantID en standaard abonnements-ID weergegeven.</span><span class="sxs-lookup"><span data-stu-id="96b3f-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="96b3f-119">Alle Hallo Azure-cmdlets werk in de context van uw standaardabonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="96b3f-119">All hello Azure cmdlets work in hello context of your default subscription.</span></span> <span data-ttu-id="96b3f-120">tooview hello lijst met abonnementen die u hebt toegang tot, Hallo volgende opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="96b3f-120">tooview hello list of subscriptions you have access to, use hello following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="96b3f-121">toochange uw werkende context tooa verschillende abonnement, gebruik Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="96b3f-121">toochange your working context tooa different subscription, use hello following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="96b3f-122">Activiteitenlogboek voor een abonnement ophalen</span><span class="sxs-lookup"><span data-stu-id="96b3f-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="96b3f-123">Gebruik Hallo `Get-AzureRmLog` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96b3f-123">Use hello `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="96b3f-124">Hallo hieronder vindt u enkele algemene voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="96b3f-124">hello following are some common examples.</span></span>

<span data-ttu-id="96b3f-125">Logboekvermeldingen ophalen uit deze toopresent tijd/datum:</span><span class="sxs-lookup"><span data-stu-id="96b3f-125">Get log entries from this time/date toopresent:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="96b3f-126">Logboekvermeldingen tussen een bereik van tijd/datum ophalen:</span><span class="sxs-lookup"><span data-stu-id="96b3f-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="96b3f-127">Logboekvermeldingen ophalen uit een specifieke resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="96b3f-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="96b3f-128">Logboekvermeldingen ophalen van een bepaalde resourceprovider tussen een bereik van tijd/datum:</span><span class="sxs-lookup"><span data-stu-id="96b3f-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="96b3f-129">Alle logboekvermeldingen met een specifieke aanroeper ophalen:</span><span class="sxs-lookup"><span data-stu-id="96b3f-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="96b3f-130">Hallo opdracht haalt de laatste 1000 gebeurtenissen van activiteitenlogboek Hallo Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="96b3f-130">hello following command retrieves hello last 1000 events from hello activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="96b3f-131">`Get-AzureRmLog`biedt ondersteuning voor veel andere parameters.</span><span class="sxs-lookup"><span data-stu-id="96b3f-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="96b3f-132">Zie Hallo `Get-AzureRmLog` documentatie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="96b3f-132">See hello `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="96b3f-133">`Get-AzureRmLog`biedt alleen 15 dagen van de geschiedenis.</span><span class="sxs-lookup"><span data-stu-id="96b3f-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="96b3f-134">Met behulp van Hallo **- MaxEvents** parameter kunt u tooquery Hallo laatste N gebeurtenissen, afgezien van 15 dagen.</span><span class="sxs-lookup"><span data-stu-id="96b3f-134">Using hello **-MaxEvents** parameter allows you tooquery hello last N events, beyond 15 days.</span></span> <span data-ttu-id="96b3f-135">tooaccess gebeurtenissen die ouder zijn dan 15 dagen Hallo REST-API of de SDK (C# voorbeeld met Hallo SDK) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="96b3f-135">tooaccess events older than 15 days, use hello REST API or SDK (C# sample using hello SDK).</span></span> <span data-ttu-id="96b3f-136">Als u geen **StartTime**, dan is de standaardwaarde Hallo **EndTime** min één uur.</span><span class="sxs-lookup"><span data-stu-id="96b3f-136">If you do not include **StartTime**, then hello default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="96b3f-137">Als u geen **EndTime**, dan is de standaardwaarde Hallo huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="96b3f-137">If you do not include **EndTime**, then hello default value is current time.</span></span> <span data-ttu-id="96b3f-138">Alle tijden zijn in UTC.</span><span class="sxs-lookup"><span data-stu-id="96b3f-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="96b3f-139">Ophalen van de geschiedenis van waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="96b3f-139">Retrieve alerts history</span></span>
<span data-ttu-id="96b3f-140">alle waarschuwingen gebeurtenissen, u kunt een query tooview Hallo Hallo volgen voorbeelden met Azure Resource Manager-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="96b3f-140">tooview all alert events, you can query hello Azure Resource Manager logs using hello following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="96b3f-141">tooview hello geschiedenis voor een specifieke waarschuwing sluiten, kunt u Hallo `Get-AzureRmAlertHistory` doorgeven in een resource-ID van de waarschuwingsregel Hallo Hallo-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96b3f-141">tooview hello history for a specific alert rule, you can use hello `Get-AzureRmAlertHistory` cmdlet, passing in hello resource ID of hello alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="96b3f-142">Hallo `Get-AzureRmAlertHistory` cmdlet ondersteunt verschillende parameters.</span><span class="sxs-lookup"><span data-stu-id="96b3f-142">hello `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="96b3f-143">Meer informatie Zie [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="96b3f-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="96b3f-144">Ophalen van informatie over de regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="96b3f-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="96b3f-145">Alle volgende opdrachten Hallo fungeren voor een resourcegroep met de naam 'montest'.</span><span class="sxs-lookup"><span data-stu-id="96b3f-145">All of hello following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="96b3f-146">Alle Hallo-eigenschappen van de waarschuwingsregel Hallo weergeven:</span><span class="sxs-lookup"><span data-stu-id="96b3f-146">View all hello properties of hello alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="96b3f-147">Alle waarschuwingen voor een resourcegroep ophalen:</span><span class="sxs-lookup"><span data-stu-id="96b3f-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="96b3f-148">Alle regels voor waarschuwingen instellen voor een doelresource worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="96b3f-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="96b3f-149">Bijvoorbeeld instellen alle regels voor waarschuwingen op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="96b3f-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="96b3f-150">`Get-AzureRmAlertRule`biedt ondersteuning voor andere parameters.</span><span class="sxs-lookup"><span data-stu-id="96b3f-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="96b3f-151">Zie [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="96b3f-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="96b3f-152">Metrische waarschuwingen maken</span><span class="sxs-lookup"><span data-stu-id="96b3f-152">Create metric alerts</span></span>
<span data-ttu-id="96b3f-153">U kunt Hallo `Add-AlertRule` cmdlet toocreate, bijwerken of een waarschuwingsregel uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="96b3f-153">You can use hello `Add-AlertRule` cmdlet toocreate, update or disable an alert rule.</span></span>

<span data-ttu-id="96b3f-154">Kunt u e-mail en -webhook eigenschappen met behulp van `New-AzureRmAlertRuleEmail` en `New-AzureRmAlertRuleWebhook`respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="96b3f-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="96b3f-155">Wijs in Hallo waarschuwingsregel cmdlet, deze poorten als acties toohello **acties** eigenschap Hallo waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="96b3f-155">In hello Alert rule cmdlet, assign these as actions toohello **Actions** property of hello Alert Rule.</span></span>

<span data-ttu-id="96b3f-156">Hallo volgende tabel beschrijft Hallo parameters en waarden gebruikte toocreate een waarschuwing met behulp van een metriek.</span><span class="sxs-lookup"><span data-stu-id="96b3f-156">hello following table describes hello parameters and values used toocreate an alert using a metric.</span></span>

| <span data-ttu-id="96b3f-157">Parameter</span><span class="sxs-lookup"><span data-stu-id="96b3f-157">parameter</span></span> | <span data-ttu-id="96b3f-158">waarde</span><span class="sxs-lookup"><span data-stu-id="96b3f-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="96b3f-159">Naam</span><span class="sxs-lookup"><span data-stu-id="96b3f-159">Name</span></span> |<span data-ttu-id="96b3f-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="96b3f-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="96b3f-161">Locatie van deze waarschuwingsregel</span><span class="sxs-lookup"><span data-stu-id="96b3f-161">Location of this alert rule</span></span> |<span data-ttu-id="96b3f-162">VS - oost</span><span class="sxs-lookup"><span data-stu-id="96b3f-162">East US</span></span> |
| <span data-ttu-id="96b3f-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="96b3f-163">ResourceGroup</span></span> |<span data-ttu-id="96b3f-164">montest</span><span class="sxs-lookup"><span data-stu-id="96b3f-164">montest</span></span> |
| <span data-ttu-id="96b3f-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="96b3f-165">TargetResourceId</span></span> |<span data-ttu-id="96b3f-166">/Subscriptions/S1/resourceGroups/montest/providers/Microsoft.COMPUTE/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="96b3f-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="96b3f-167">MetricName van Hallo waarschuwing die wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="96b3f-167">MetricName of hello alert that is created</span></span> |<span data-ttu-id="96b3f-168">\Disk \PhysicalDisk (_Totaal) per seconde. Zie Hallo `Get-MetricDefinitions` cmdlet over hoe tooretrieve Hallo exacte metrische namen</span><span class="sxs-lookup"><span data-stu-id="96b3f-168">\PhysicalDisk(_Total)\Disk Writes/sec. See hello `Get-MetricDefinitions` cmdlet about how tooretrieve hello exact metric names</span></span> |
| <span data-ttu-id="96b3f-169">Operator</span><span class="sxs-lookup"><span data-stu-id="96b3f-169">operator</span></span> |<span data-ttu-id="96b3f-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="96b3f-170">GreaterThan</span></span> |
| <span data-ttu-id="96b3f-171">Drempelwaarde (aantal per seconde in voor deze metrische gegevens)</span><span class="sxs-lookup"><span data-stu-id="96b3f-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="96b3f-172">1</span><span class="sxs-lookup"><span data-stu-id="96b3f-172">1</span></span> |
| <span data-ttu-id="96b3f-173">Venstergrootte (indeling: mm: SS)</span><span class="sxs-lookup"><span data-stu-id="96b3f-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="96b3f-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="96b3f-174">00:05:00</span></span> |
| <span data-ttu-id="96b3f-175">aggregator (statistiek van Hallo metrische gegevens, die in dit geval gemiddeld aantal gebruikt)</span><span class="sxs-lookup"><span data-stu-id="96b3f-175">aggregator (statistic of hello metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="96b3f-176">Gemiddelde</span><span class="sxs-lookup"><span data-stu-id="96b3f-176">Average</span></span> |
| <span data-ttu-id="96b3f-177">aangepaste e-mailberichten (string array)</span><span class="sxs-lookup"><span data-stu-id="96b3f-177">custom emails (string array)</span></span> |<span data-ttu-id="96b3f-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="96b3f-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="96b3f-179">e-mailadres tooowners, bijdragers en lezers verzenden</span><span class="sxs-lookup"><span data-stu-id="96b3f-179">send email tooowners, contributors and readers</span></span> |<span data-ttu-id="96b3f-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="96b3f-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="96b3f-181">Een e-actie maken</span><span class="sxs-lookup"><span data-stu-id="96b3f-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="96b3f-182">Maken van een Webhook-actie</span><span class="sxs-lookup"><span data-stu-id="96b3f-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="96b3f-183">Hallo waarschuwingsregel maken op Hallo CPU % metriek op een klassieke virtuele machine</span><span class="sxs-lookup"><span data-stu-id="96b3f-183">Create hello alert rule on hello CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="96b3f-184">De waarschuwingsregel Hallo ophalen</span><span class="sxs-lookup"><span data-stu-id="96b3f-184">Retrieve hello alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="96b3f-185">Hallo regel Hallo toevoegen waarschuwing cmdlet ook bijgewerkt als er al een waarschuwingsregel voor Hallo eigenschappen bestaat.</span><span class="sxs-lookup"><span data-stu-id="96b3f-185">hello Add alert cmdlet also updates hello rule if an alert rule already exists for hello given properties.</span></span> <span data-ttu-id="96b3f-186">een waarschuwingsregel toodisable Hallo-parameter opnemen **- DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="96b3f-186">toodisable an alert rule, include hello parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="96b3f-187">Een lijst met beschikbare metrische gegevens ophalen voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="96b3f-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="96b3f-188">U kunt Hallo `Get-AzureRmMetricDefinition` cmdlet tooview Hallo lijst met alle metrische gegevens voor een specifieke bron.</span><span class="sxs-lookup"><span data-stu-id="96b3f-188">You can use hello `Get-AzureRmMetricDefinition` cmdlet tooview hello list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="96b3f-189">Hallo volgende voorbeeld genereert een tabel met Hallo metriek naam en het Hallo eenheid voor.</span><span class="sxs-lookup"><span data-stu-id="96b3f-189">hello following example generates a table with hello metric Name and hello Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="96b3f-190">Een volledige lijst met beschikbare opties voor `Get-AzureRmMetricDefinition` is beschikbaar op [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="96b3f-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="96b3f-191">Maken en beheren van instellingen voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="96b3f-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="96b3f-192">Een resource, zoals een Web-app, VM, Cloudservice of virtuele-Machineschaalset kan slechts één instelling voor automatisch schalen geconfigureerd hebben.</span><span class="sxs-lookup"><span data-stu-id="96b3f-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="96b3f-193">Elke instelling voor automatisch schalen kunt echter meerdere profielen hebben.</span><span class="sxs-lookup"><span data-stu-id="96b3f-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="96b3f-194">Bijvoorbeeld, een voor een profiel schalen op basis van prestaties en een tweede voor een profiel op basis van een planning.</span><span class="sxs-lookup"><span data-stu-id="96b3f-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="96b3f-195">Elk profiel kan meerdere regels die zijn geconfigureerd op deze hebben.</span><span class="sxs-lookup"><span data-stu-id="96b3f-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="96b3f-196">Zie voor meer informatie over automatisch schalen, [hoe een toepassing tooAutoscale](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="96b3f-196">For more information about Autoscale, see [How tooAutoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="96b3f-197">Hier volgen Hallo stappen die zullen worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="96b3f-197">Here are hello steps we will use:</span></span>

1. <span data-ttu-id="96b3f-198">Regel (s) maken.</span><span class="sxs-lookup"><span data-stu-id="96b3f-198">Create rule(s).</span></span>
2. <span data-ttu-id="96b3f-199">Maken van profielen toewijzing Hallo regels die u eerder toohello profielen gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96b3f-199">Create profile(s) mapping hello rules that you created previously toohello profiles.</span></span>
3. <span data-ttu-id="96b3f-200">Optioneel: Maak meldingen voor automatisch schalen door webhook en e-eigenschappen te configureren.</span><span class="sxs-lookup"><span data-stu-id="96b3f-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="96b3f-201">Een instelling voor automatisch schalen met een naam voor de doelbron Hallo maken via het Hallo-profielen en meldingen die u hebt gemaakt in de vorige stappen Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="96b3f-201">Create an autoscale setting with a name on hello target resource by mapping hello profiles and notifications that you created in hello previous steps.</span></span>

<span data-ttu-id="96b3f-202">Hallo volgende voorbeelden ziet u hoe u een instelling voor automatisch schalen voor een virtuele-Machineschaalset voor een Windows-besturingssysteem op basis van met behulp van Hallo CPU-gebruik metrische gegevens kunt maken.</span><span class="sxs-lookup"><span data-stu-id="96b3f-202">hello following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using hello CPU utilization metric.</span></span>

<span data-ttu-id="96b3f-203">Maak eerst een regel tooscale-out, met een verhoging van het aantal exemplaar.</span><span class="sxs-lookup"><span data-stu-id="96b3f-203">First, create a rule tooscale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="96b3f-204">Maak vervolgens een regel tooscale in, met een aantal exemplaar verlagen.</span><span class="sxs-lookup"><span data-stu-id="96b3f-204">Next, create a rule tooscale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="96b3f-205">Vervolgens maakt u een profiel voor Hallo regels.</span><span class="sxs-lookup"><span data-stu-id="96b3f-205">Then, create a profile for hello rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="96b3f-206">Maak een webhook-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="96b3f-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="96b3f-207">Maak Hallo melding eigenschap voor de instelling voor Hallo automatisch schalen, zoals e-mail en Hallo webhook die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96b3f-207">Create hello notification property for hello autoscale setting, including email and hello webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="96b3f-208">Maak ten slotte Hallo automatisch schalen instellen tooadd Hallo van het profiel dat u hierboven hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96b3f-208">Finally, create hello autoscale setting tooadd hello profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="96b3f-209">Zie voor meer informatie over het beheren van instellingen voor automatisch schalen [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="96b3f-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="96b3f-210">Geschiedenis van automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="96b3f-210">Autoscale history</span></span>
<span data-ttu-id="96b3f-211">Hallo volgende voorbeeld ziet u hoe u recente gebeurtenissen voor automatisch schalen en waarschuwing kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="96b3f-211">hello following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="96b3f-212">Hallo activiteit zoeken tooview Hallo automatisch schalen Logboekgeschiedenis gebruiken.</span><span class="sxs-lookup"><span data-stu-id="96b3f-212">Use hello activity log search tooview hello autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="96b3f-213">U kunt Hallo `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve historie van automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="96b3f-213">You can use hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="96b3f-214">Zie voor meer informatie [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="96b3f-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="96b3f-215">Details weergeven voor een instelling voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="96b3f-215">View details for an autoscale setting</span></span>
<span data-ttu-id="96b3f-216">U kunt Hallo `Get-Autoscalesetting` cmdlet tooretrieve meer informatie over het Hallo-instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="96b3f-216">You can use hello `Get-Autoscalesetting` cmdlet tooretrieve more information about hello autoscale setting.</span></span>

<span data-ttu-id="96b3f-217">Hallo volgende voorbeeld worden details weergegeven over alle instellingen voor automatisch schalen in myrg1' hello resource group'.</span><span class="sxs-lookup"><span data-stu-id="96b3f-217">hello following example shows details about all autoscale settings in hello resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="96b3f-218">Hallo volgende voorbeeld worden details weergegeven over alle instellingen voor automatisch schalen in myrg1' hello resource groep' en specifiek Hallo instelling voor automatisch schalen met de naam 'MyScaleVMSSSetting'.</span><span class="sxs-lookup"><span data-stu-id="96b3f-218">hello following example shows details about all autoscale settings in hello resource group 'myrg1' and specifically hello autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="96b3f-219">Verwijderen van een instelling voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="96b3f-219">Remove an autoscale setting</span></span>
<span data-ttu-id="96b3f-220">U kunt Hallo `Remove-Autoscalesetting` cmdlet toodelete een instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="96b3f-220">You can use hello `Remove-Autoscalesetting` cmdlet toodelete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="96b3f-221">Logboek profielen beheert voor activiteitenlogboek</span><span class="sxs-lookup"><span data-stu-id="96b3f-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="96b3f-222">Kunt u een *Meld profiel* en het exporteren van gegevens van uw opslagaccount activiteit logboek tooa en u kunt bewaren van gegevens voor het configureren.</span><span class="sxs-lookup"><span data-stu-id="96b3f-222">You can create a *log profile* and export data from your activity log tooa storage account and you can configure data retention for it.</span></span> <span data-ttu-id="96b3f-223">U kunt eventueel ook Hallo gegevens tooyour Event Hub streamen.</span><span class="sxs-lookup"><span data-stu-id="96b3f-223">Optionally, you can also stream hello data tooyour Event Hub.</span></span> <span data-ttu-id="96b3f-224">Let op: deze functie momenteel in Preview en u is kunt slechts één log-profiel per abonnement maken.</span><span class="sxs-lookup"><span data-stu-id="96b3f-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="96b3f-225">U kunt gebruiken Hallo cmdlets met uw huidige abonnement toocreate te volgen en log-profielen te beheren.</span><span class="sxs-lookup"><span data-stu-id="96b3f-225">You can use hello following cmdlets with your current subscription toocreate and manage log profiles.</span></span> <span data-ttu-id="96b3f-226">U kunt ook een bepaald abonnement.</span><span class="sxs-lookup"><span data-stu-id="96b3f-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="96b3f-227">Hoewel PowerShell standaard toohello huidige abonnement, kunt u altijd wijzigen die met `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="96b3f-227">Although PowerShell defaults toohello current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="96b3f-228">U kunt een activiteit logboek tooroute gegevens tooany storage-account of Event Hub configureren binnen dat abonnement.</span><span class="sxs-lookup"><span data-stu-id="96b3f-228">You can configure activity log tooroute data tooany storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="96b3f-229">Gegevens worden geschreven als blob-bestanden in de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="96b3f-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="96b3f-230">Een profiel voor een logboek ophalen</span><span class="sxs-lookup"><span data-stu-id="96b3f-230">Get a log profile</span></span>
<span data-ttu-id="96b3f-231">toofetch uw bestaande logboek-profielen maken gebruik van Hallo `Get-AzureRmLogProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96b3f-231">toofetch your existing log profiles, use hello `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="96b3f-232">Een profiel logboek zonder bewaren van gegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="96b3f-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="96b3f-233">Een logboek-profiel verwijderen</span><span class="sxs-lookup"><span data-stu-id="96b3f-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="96b3f-234">Een profiel van het logboek met bewaren van gegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="96b3f-234">Add a log profile with data retention</span></span>
<span data-ttu-id="96b3f-235">U kunt opgeven dat Hallo **- RetentionInDays** eigenschap met de Hallo aantal dagen, als een positief geheel getal, waarbij Hallo gegevens moeten worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="96b3f-235">You can specify hello **-RetentionInDays** property with hello number of days, as a positive integer, where hello data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="96b3f-236">Logboek-profiel met bewaren en EventHub toevoegen</span><span class="sxs-lookup"><span data-stu-id="96b3f-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="96b3f-237">In aanvulling toorouting uw gegevens toostorage-account, u kunt ook streamen deze tooan Event Hub.</span><span class="sxs-lookup"><span data-stu-id="96b3f-237">In addition toorouting your data toostorage account, you can also stream it tooan Event Hub.</span></span> <span data-ttu-id="96b3f-238">Houd er rekening mee dat in deze preview release en Hallo account opslagconfiguratie verplicht is maar Event Hub-configuratie optioneel is.</span><span class="sxs-lookup"><span data-stu-id="96b3f-238">Note that in this preview release and hello storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="96b3f-239">Logboeken met diagnostische gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="96b3f-239">Configure diagnostics logs</span></span>
<span data-ttu-id="96b3f-240">Veel Azure-services bieden extra logboeken en telemetrie die geconfigureerd toosave gegevens in uw Azure Storage-account worden kan, sturen tooEvent Hubs en/of tooan logboekanalyse OMS-werkruimte verzonden.</span><span class="sxs-lookup"><span data-stu-id="96b3f-240">Many Azure services provide additional logs and telemetry that can be configured toosave data in your Azure Storage account, send tooEvent Hubs, and/or sent tooan OMS Log Analytics workspace.</span></span> <span data-ttu-id="96b3f-241">Deze bewerking kan alleen worden uitgevoerd op het niveau van een resource en Hallo storage-account of event hub moet aanwezig zijn in Hallo dezelfde regio bevinden als de doelbron Hallo waarop Hallo diagnostische instelling is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="96b3f-241">That operation can only be performed at a resource level and hello storage account or event hub should be present in hello same region as hello target resource where hello diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="96b3f-242">De diagnostische instelling niet ophalen</span><span class="sxs-lookup"><span data-stu-id="96b3f-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="96b3f-243">Diagnostische instelling uitschakelen</span><span class="sxs-lookup"><span data-stu-id="96b3f-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="96b3f-244">Schakel diagnostische instelling zonder bewaren</span><span class="sxs-lookup"><span data-stu-id="96b3f-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="96b3f-245">Schakel diagnostische instelling met bewaren</span><span class="sxs-lookup"><span data-stu-id="96b3f-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="96b3f-246">Schakel diagnostische instelling met de bewaarperiode voor een specifieke logboek-categorie</span><span class="sxs-lookup"><span data-stu-id="96b3f-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="96b3f-247">Schakel diagnostische instelling voor Event Hubs</span><span class="sxs-lookup"><span data-stu-id="96b3f-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="96b3f-248">Diagnostische instelling voor OMS inschakelen</span><span class="sxs-lookup"><span data-stu-id="96b3f-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
