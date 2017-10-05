---
title: Azure PowerShell Monitor snel starten-voorbeelden. | Microsoft Docs
description: PowerShell gebruiken voor toegang tot Azure Monitor functies zoals automatisch schalen, waarschuwingen, webhooks en activiteitenlogboeken zoeken.
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
ms.openlocfilehash: 48f064884c2a6d0a55cc58a44169ed03c62de46d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="25d2d-104">Azure PowerShell Monitor snel starten-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="25d2d-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="25d2d-105">In dit artikel worden steekproef van PowerShell-opdrachten kunt u toegang tot Azure Monitor functies.</span><span class="sxs-lookup"><span data-stu-id="25d2d-105">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="25d2d-106">Monitor voor Azure kunt u voor automatisch schalen Cloud Services, virtuele Machines en Web-Apps en voor het verzenden van meldingen van waarschuwingen of web-URL's op basis van waarden van de geconfigureerde telemetriegegevens aanroepen.</span><span class="sxs-lookup"><span data-stu-id="25d2d-106">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="25d2d-107">Monitor voor Azure is de nieuwe naam voor wat 'Azure Insights' is aangeroepen tot 25 september 2016.</span><span class="sxs-lookup"><span data-stu-id="25d2d-107">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="25d2d-108">Echter bevatten de naamruimten, en daarom de volgende opdrachten nog steeds de 'inzichten'.</span><span class="sxs-lookup"><span data-stu-id="25d2d-108">However, the namespaces and thus the following commands still contain the "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="25d2d-109">Instellen van PowerShell</span><span class="sxs-lookup"><span data-stu-id="25d2d-109">Set up PowerShell</span></span>
<span data-ttu-id="25d2d-110">Als u nog niet gedaan hebt, kunt u PowerShell uitvoeren op uw computer instellen.</span><span class="sxs-lookup"><span data-stu-id="25d2d-110">If you haven't already, set up PowerShell to run on your computer.</span></span> <span data-ttu-id="25d2d-111">Zie voor meer informatie [installeren en configureren van PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="25d2d-111">For more information, see [How to Install and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="25d2d-112">Voorbeelden in dit artikel</span><span class="sxs-lookup"><span data-stu-id="25d2d-112">Examples in this article</span></span>
<span data-ttu-id="25d2d-113">De voorbeelden in het artikel ziet hoe u Azure Monitor cmdlets kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25d2d-113">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="25d2d-114">U kunt ook de volledige lijst met Azure Monitor PowerShell-cmdlets op bekijken [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="25d2d-114">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="25d2d-115">Aanmelden en abonnementen gebruiken</span><span class="sxs-lookup"><span data-stu-id="25d2d-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="25d2d-116">Eerst aanmelden bij uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="25d2d-116">First, log in to your Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="25d2d-117">Hiervoor moet u zich kunt aanmelden.</span><span class="sxs-lookup"><span data-stu-id="25d2d-117">This requires you to sign in.</span></span> <span data-ttu-id="25d2d-118">Zodra u dit, uw Account doet worden TenantID en standaard abonnements-ID weergegeven.</span><span class="sxs-lookup"><span data-stu-id="25d2d-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="25d2d-119">Alle Azure-cmdlets werkt in de context van uw standaardabonnement.</span><span class="sxs-lookup"><span data-stu-id="25d2d-119">All the Azure cmdlets work in the context of your default subscription.</span></span> <span data-ttu-id="25d2d-120">U hebt toegang tot de volgende opdracht gebruiken om de lijst met abonnementen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="25d2d-120">To view the list of subscriptions you have access to, use the following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="25d2d-121">Als u wilt uw werkende context wijzigen naar een ander abonnement, moet u de volgende opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25d2d-121">To change your working context to a different subscription, use the following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="25d2d-122">Activiteitenlogboek voor een abonnement ophalen</span><span class="sxs-lookup"><span data-stu-id="25d2d-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="25d2d-123">Gebruik de `Get-AzureRmLog` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25d2d-123">Use the `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="25d2d-124">Hier volgen enkele algemene voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="25d2d-124">The following are some common examples.</span></span>

<span data-ttu-id="25d2d-125">Logboekvermeldingen ophalen uit deze tijd/datum om weer te geven:</span><span class="sxs-lookup"><span data-stu-id="25d2d-125">Get log entries from this time/date to present:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="25d2d-126">Logboekvermeldingen tussen een bereik van tijd/datum ophalen:</span><span class="sxs-lookup"><span data-stu-id="25d2d-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="25d2d-127">Logboekvermeldingen ophalen uit een specifieke resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="25d2d-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="25d2d-128">Logboekvermeldingen ophalen van een bepaalde resourceprovider tussen een bereik van tijd/datum:</span><span class="sxs-lookup"><span data-stu-id="25d2d-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="25d2d-129">Alle logboekvermeldingen met een specifieke aanroeper ophalen:</span><span class="sxs-lookup"><span data-stu-id="25d2d-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="25d2d-130">De volgende opdracht haalt de laatste 1000 gebeurtenissen uit het activiteitenlogboek:</span><span class="sxs-lookup"><span data-stu-id="25d2d-130">The following command retrieves the last 1000 events from the activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="25d2d-131">`Get-AzureRmLog`biedt ondersteuning voor veel andere parameters.</span><span class="sxs-lookup"><span data-stu-id="25d2d-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="25d2d-132">Zie de `Get-AzureRmLog` documentatie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="25d2d-132">See the `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="25d2d-133">`Get-AzureRmLog`biedt alleen 15 dagen van de geschiedenis.</span><span class="sxs-lookup"><span data-stu-id="25d2d-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="25d2d-134">Met behulp van de **- MaxEvents** parameter kunt u de laatste N-gebeurtenissen na 15 dagen een query.</span><span class="sxs-lookup"><span data-stu-id="25d2d-134">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span></span> <span data-ttu-id="25d2d-135">Gebruik de REST-API of de SDK (C# voorbeeld met de SDK) op toegangsgebeurtenissen die ouder zijn dan 15 dagen.</span><span class="sxs-lookup"><span data-stu-id="25d2d-135">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span></span> <span data-ttu-id="25d2d-136">Als u geen **StartTime**, dan is de standaardwaarde **EndTime** min één uur.</span><span class="sxs-lookup"><span data-stu-id="25d2d-136">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="25d2d-137">Als u geen **EndTime**, en vervolgens de standaardwaarde is de huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="25d2d-137">If you do not include **EndTime**, then the default value is current time.</span></span> <span data-ttu-id="25d2d-138">Alle tijden zijn in UTC.</span><span class="sxs-lookup"><span data-stu-id="25d2d-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="25d2d-139">Ophalen van de geschiedenis van waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="25d2d-139">Retrieve alerts history</span></span>
<span data-ttu-id="25d2d-140">Alle waarschuwingen als gebeurtenissen wilt weergeven, kunt u de Azure Resource Manager-logboeken met behulp van de volgende voorbeelden kunt opvragen.</span><span class="sxs-lookup"><span data-stu-id="25d2d-140">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="25d2d-141">Als u wilt weergeven in de geschiedenis voor een specifieke waarschuwingsregel, kunt u de `Get-AzureRmAlertHistory` cmdlet in de resource-ID van de waarschuwingsregel wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="25d2d-141">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="25d2d-142">De `Get-AzureRmAlertHistory` cmdlet ondersteunt verschillende parameters.</span><span class="sxs-lookup"><span data-stu-id="25d2d-142">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="25d2d-143">Meer informatie Zie [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="25d2d-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="25d2d-144">Ophalen van informatie over de regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="25d2d-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="25d2d-145">Alle van de volgende opdrachten fungeren op een resourcegroep met de naam 'montest'.</span><span class="sxs-lookup"><span data-stu-id="25d2d-145">All of the following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="25d2d-146">De eigenschappen van de waarschuwingsregel weergeven:</span><span class="sxs-lookup"><span data-stu-id="25d2d-146">View all the properties of the alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="25d2d-147">Alle waarschuwingen voor een resourcegroep ophalen:</span><span class="sxs-lookup"><span data-stu-id="25d2d-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="25d2d-148">Alle regels voor waarschuwingen instellen voor een doelresource worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="25d2d-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="25d2d-149">Bijvoorbeeld instellen alle regels voor waarschuwingen op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="25d2d-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="25d2d-150">`Get-AzureRmAlertRule`biedt ondersteuning voor andere parameters.</span><span class="sxs-lookup"><span data-stu-id="25d2d-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="25d2d-151">Zie [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="25d2d-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="25d2d-152">Metrische waarschuwingen maken</span><span class="sxs-lookup"><span data-stu-id="25d2d-152">Create metric alerts</span></span>
<span data-ttu-id="25d2d-153">U kunt de `Add-AlertRule` cmdlet maken, bijwerken of een waarschuwingsregel uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="25d2d-153">You can use the `Add-AlertRule` cmdlet to create, update or disable an alert rule.</span></span>

<span data-ttu-id="25d2d-154">Kunt u e-mail en -webhook eigenschappen met behulp van `New-AzureRmAlertRuleEmail` en `New-AzureRmAlertRuleWebhook`respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="25d2d-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="25d2d-155">In de cmdlet waarschuwingsregel toewijzen deze poorten als acties voor de **acties** eigenschap van de waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="25d2d-155">In the Alert rule cmdlet, assign these as actions to the **Actions** property of the Alert Rule.</span></span>

<span data-ttu-id="25d2d-156">De volgende tabel beschrijft de parameters en waarden die worden gebruikt voor het maken van een waarschuwing met behulp van een metriek.</span><span class="sxs-lookup"><span data-stu-id="25d2d-156">The following table describes the parameters and values used to create an alert using a metric.</span></span>

| <span data-ttu-id="25d2d-157">Parameter</span><span class="sxs-lookup"><span data-stu-id="25d2d-157">parameter</span></span> | <span data-ttu-id="25d2d-158">waarde</span><span class="sxs-lookup"><span data-stu-id="25d2d-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="25d2d-159">Naam</span><span class="sxs-lookup"><span data-stu-id="25d2d-159">Name</span></span> |<span data-ttu-id="25d2d-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="25d2d-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="25d2d-161">Locatie van deze waarschuwingsregel</span><span class="sxs-lookup"><span data-stu-id="25d2d-161">Location of this alert rule</span></span> |<span data-ttu-id="25d2d-162">VS - oost</span><span class="sxs-lookup"><span data-stu-id="25d2d-162">East US</span></span> |
| <span data-ttu-id="25d2d-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="25d2d-163">ResourceGroup</span></span> |<span data-ttu-id="25d2d-164">montest</span><span class="sxs-lookup"><span data-stu-id="25d2d-164">montest</span></span> |
| <span data-ttu-id="25d2d-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="25d2d-165">TargetResourceId</span></span> |<span data-ttu-id="25d2d-166">/Subscriptions/S1/resourceGroups/montest/providers/Microsoft.COMPUTE/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="25d2d-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="25d2d-167">MetricName van de waarschuwing die wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="25d2d-167">MetricName of the alert that is created</span></span> |<span data-ttu-id="25d2d-168">\Disk \PhysicalDisk (_Totaal) per seconde. Zie de `Get-MetricDefinitions` cmdlet over het ophalen van de exacte metrische namen</span><span class="sxs-lookup"><span data-stu-id="25d2d-168">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet about how to retrieve the exact metric names</span></span> |
| <span data-ttu-id="25d2d-169">Operator</span><span class="sxs-lookup"><span data-stu-id="25d2d-169">operator</span></span> |<span data-ttu-id="25d2d-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="25d2d-170">GreaterThan</span></span> |
| <span data-ttu-id="25d2d-171">Drempelwaarde (aantal per seconde in voor deze metrische gegevens)</span><span class="sxs-lookup"><span data-stu-id="25d2d-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="25d2d-172">1</span><span class="sxs-lookup"><span data-stu-id="25d2d-172">1</span></span> |
| <span data-ttu-id="25d2d-173">Venstergrootte (indeling: mm: SS)</span><span class="sxs-lookup"><span data-stu-id="25d2d-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="25d2d-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="25d2d-174">00:05:00</span></span> |
| <span data-ttu-id="25d2d-175">aggregator (statistiek van de metrische gegevens die in dit geval gemiddeld aantal gebruikt)</span><span class="sxs-lookup"><span data-stu-id="25d2d-175">aggregator (statistic of the metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="25d2d-176">Gemiddelde</span><span class="sxs-lookup"><span data-stu-id="25d2d-176">Average</span></span> |
| <span data-ttu-id="25d2d-177">aangepaste e-mailberichten (string array)</span><span class="sxs-lookup"><span data-stu-id="25d2d-177">custom emails (string array)</span></span> |<span data-ttu-id="25d2d-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="25d2d-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="25d2d-179">e-mail verzenden aan eigenaren, bijdragers en lezers</span><span class="sxs-lookup"><span data-stu-id="25d2d-179">send email to owners, contributors and readers</span></span> |<span data-ttu-id="25d2d-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="25d2d-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="25d2d-181">Een e-actie maken</span><span class="sxs-lookup"><span data-stu-id="25d2d-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="25d2d-182">Maken van een Webhook-actie</span><span class="sxs-lookup"><span data-stu-id="25d2d-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="25d2d-183">De waarschuwingsregel maken op de CPU % metrische gegevens op een klassieke virtuele machine</span><span class="sxs-lookup"><span data-stu-id="25d2d-183">Create the alert rule on the CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="25d2d-184">De waarschuwingsregel ophalen</span><span class="sxs-lookup"><span data-stu-id="25d2d-184">Retrieve the alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="25d2d-185">De regel de waarschuwing toevoegen-cmdlet ook bijgewerkt als er al een waarschuwingsregel voor de opgegeven eigenschappen bestaat.</span><span class="sxs-lookup"><span data-stu-id="25d2d-185">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span></span> <span data-ttu-id="25d2d-186">Als u wilt een waarschuwingsregel uitschakelen, bevatten de parameter **- DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="25d2d-186">To disable an alert rule, include the parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="25d2d-187">Een lijst met beschikbare metrische gegevens ophalen voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="25d2d-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="25d2d-188">U kunt de `Get-AzureRmMetricDefinition` cmdlet om de lijst met alle metrische gegevens voor een specifieke bron weer te geven.</span><span class="sxs-lookup"><span data-stu-id="25d2d-188">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="25d2d-189">Het volgende voorbeeld wordt een tabel met de naam van de metriek en de eenheid voor het gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="25d2d-189">The following example generates a table with the metric Name and the Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="25d2d-190">Een volledige lijst met beschikbare opties voor `Get-AzureRmMetricDefinition` is beschikbaar op [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="25d2d-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="25d2d-191">Maken en beheren van instellingen voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="25d2d-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="25d2d-192">Een resource, zoals een Web-app, VM, Cloudservice of virtuele-Machineschaalset kan slechts één instelling voor automatisch schalen geconfigureerd hebben.</span><span class="sxs-lookup"><span data-stu-id="25d2d-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="25d2d-193">Elke instelling voor automatisch schalen kunt echter meerdere profielen hebben.</span><span class="sxs-lookup"><span data-stu-id="25d2d-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="25d2d-194">Bijvoorbeeld, een voor een profiel schalen op basis van prestaties en een tweede voor een profiel op basis van een planning.</span><span class="sxs-lookup"><span data-stu-id="25d2d-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="25d2d-195">Elk profiel kan meerdere regels die zijn geconfigureerd op deze hebben.</span><span class="sxs-lookup"><span data-stu-id="25d2d-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="25d2d-196">Zie voor meer informatie over automatisch schalen, [hoe een toepassing voor automatisch schalen](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="25d2d-196">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="25d2d-197">Hier volgen de stappen die zullen worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="25d2d-197">Here are the steps we will use:</span></span>

1. <span data-ttu-id="25d2d-198">Regel (s) maken.</span><span class="sxs-lookup"><span data-stu-id="25d2d-198">Create rule(s).</span></span>
2. <span data-ttu-id="25d2d-199">Profielen die eerder toewijzing van de regels die u hebt gemaakt om de profielen te maken.</span><span class="sxs-lookup"><span data-stu-id="25d2d-199">Create profile(s) mapping the rules that you created previously to the profiles.</span></span>
3. <span data-ttu-id="25d2d-200">Optioneel: Maak meldingen voor automatisch schalen door webhook en e-eigenschappen te configureren.</span><span class="sxs-lookup"><span data-stu-id="25d2d-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="25d2d-201">Een instelling voor automatisch schalen met een naam voor de doelbron maken via het toewijzen van de profielen en meldingen die u in de vorige stappen hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="25d2d-201">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span></span>

<span data-ttu-id="25d2d-202">De volgende voorbeelden ziet u hoe u een instelling voor automatisch schalen voor een virtuele-Machineschaalset voor een Windows-besturingssysteem op basis van met behulp van de CPU-gebruik metrische gegevens kunt maken.</span><span class="sxs-lookup"><span data-stu-id="25d2d-202">The following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using the CPU utilization metric.</span></span>

<span data-ttu-id="25d2d-203">Maak eerst een regel voor het scale-out met de toename van een exemplaar count.</span><span class="sxs-lookup"><span data-stu-id="25d2d-203">First, create a rule to scale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="25d2d-204">Maak vervolgens een regel voor het scale-in, met een aantal exemplaar verlagen.</span><span class="sxs-lookup"><span data-stu-id="25d2d-204">Next, create a rule to scale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="25d2d-205">Vervolgens maakt u een profiel voor de regels.</span><span class="sxs-lookup"><span data-stu-id="25d2d-205">Then, create a profile for the rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="25d2d-206">Maak een webhook-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="25d2d-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="25d2d-207">Maken van de eigenschap melding voor de instelling voor automatisch schalen, met inbegrip van e-mailadres en de webhook die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="25d2d-207">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="25d2d-208">Maak ten slotte de instelling voor automatisch schalen om toe te voegen van het profiel dat u hierboven hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="25d2d-208">Finally, create the autoscale setting to add the profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="25d2d-209">Zie voor meer informatie over het beheren van instellingen voor automatisch schalen [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="25d2d-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="25d2d-210">Geschiedenis van automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="25d2d-210">Autoscale history</span></span>
<span data-ttu-id="25d2d-211">Het volgende voorbeeld ziet u hoe u recente automatisch schalen en waarschuwingsgebeurtenissen kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="25d2d-211">The following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="25d2d-212">Gebruik de activiteit logboek zoekopdracht om de geschiedenis voor automatisch schalen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="25d2d-212">Use the activity log search to view the autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="25d2d-213">U kunt de `Get-AzureRmAutoScaleHistory` cmdlet voor het ophalen van de geschiedenis voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="25d2d-213">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="25d2d-214">Zie voor meer informatie [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="25d2d-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="25d2d-215">Details weergeven voor een instelling voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="25d2d-215">View details for an autoscale setting</span></span>
<span data-ttu-id="25d2d-216">U kunt de `Get-Autoscalesetting` cmdlet meer informatie over de instelling voor automatisch schalen op te halen.</span><span class="sxs-lookup"><span data-stu-id="25d2d-216">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span></span>

<span data-ttu-id="25d2d-217">Het volgende voorbeeld worden details weergegeven over alle instellingen voor automatisch schalen in de resource-groep 'myrg1'.</span><span class="sxs-lookup"><span data-stu-id="25d2d-217">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="25d2d-218">Het volgende voorbeeld worden details weergegeven over alle instellingen voor automatisch schalen in de resource-groep 'myrg1' en specifiek de instelling voor automatisch schalen met de naam 'MyScaleVMSSSetting'.</span><span class="sxs-lookup"><span data-stu-id="25d2d-218">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="25d2d-219">Verwijderen van een instelling voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="25d2d-219">Remove an autoscale setting</span></span>
<span data-ttu-id="25d2d-220">U kunt de `Remove-Autoscalesetting` cmdlet verwijderen van een instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="25d2d-220">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="25d2d-221">Logboek profielen beheert voor activiteitenlogboek</span><span class="sxs-lookup"><span data-stu-id="25d2d-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="25d2d-222">Kunt u een *Meld profiel* en gegevens uit uw activiteitenlogboek exporteren naar een opslagaccount en u kunt bewaren van gegevens voor het configureren.</span><span class="sxs-lookup"><span data-stu-id="25d2d-222">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span></span> <span data-ttu-id="25d2d-223">U kunt eventueel ook de gegevens naar uw Event Hub streamen.</span><span class="sxs-lookup"><span data-stu-id="25d2d-223">Optionally, you can also stream the data to your Event Hub.</span></span> <span data-ttu-id="25d2d-224">Let op: deze functie momenteel in Preview en u is kunt slechts één log-profiel per abonnement maken.</span><span class="sxs-lookup"><span data-stu-id="25d2d-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="25d2d-225">U kunt de volgende cmdlets met uw huidige abonnement logboek-profielen maken en beheren.</span><span class="sxs-lookup"><span data-stu-id="25d2d-225">You can use the following cmdlets with your current subscription to create and manage log profiles.</span></span> <span data-ttu-id="25d2d-226">U kunt ook een bepaald abonnement.</span><span class="sxs-lookup"><span data-stu-id="25d2d-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="25d2d-227">Hoewel PowerShell wordt standaard ingesteld op het huidige abonnement, kunt u altijd wijzigen die met `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="25d2d-227">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="25d2d-228">U kunt configureren activiteitenlogboek van gegevens voor het routeren naar een opslagaccount of Event Hub binnen dat abonnement.</span><span class="sxs-lookup"><span data-stu-id="25d2d-228">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="25d2d-229">Gegevens worden geschreven als blob-bestanden in de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="25d2d-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="25d2d-230">Een profiel voor een logboek ophalen</span><span class="sxs-lookup"><span data-stu-id="25d2d-230">Get a log profile</span></span>
<span data-ttu-id="25d2d-231">Voor het ophalen van de profielen van uw bestaande logboek, gebruiken de `Get-AzureRmLogProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25d2d-231">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="25d2d-232">Een profiel logboek zonder bewaren van gegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="25d2d-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="25d2d-233">Een logboek-profiel verwijderen</span><span class="sxs-lookup"><span data-stu-id="25d2d-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="25d2d-234">Een profiel van het logboek met bewaren van gegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="25d2d-234">Add a log profile with data retention</span></span>
<span data-ttu-id="25d2d-235">U kunt opgeven de **- RetentionInDays** eigenschap met het aantal dagen, als een positief geheel getal, waar de gegevens worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="25d2d-235">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="25d2d-236">Logboek-profiel met bewaren en EventHub toevoegen</span><span class="sxs-lookup"><span data-stu-id="25d2d-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="25d2d-237">Bovendien uw gegevens naar het opslagaccount kunt u deze ook stream naar een Event Hub.</span><span class="sxs-lookup"><span data-stu-id="25d2d-237">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span></span> <span data-ttu-id="25d2d-238">Houd er rekening mee dat in deze preview-versie en de opslag accountconfiguratie verplicht is, maar de configuratie van de Event Hub optioneel is.</span><span class="sxs-lookup"><span data-stu-id="25d2d-238">Note that in this preview release and the storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="25d2d-239">Logboeken met diagnostische gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="25d2d-239">Configure diagnostics logs</span></span>
<span data-ttu-id="25d2d-240">Veel Azure-services bieden extra logboeken en telemetrie die kan worden geconfigureerd voor het opslaan van gegevens in uw Azure Storage-account, verzenden naar Event Hubs en/of verzonden naar een logboekanalyse OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="25d2d-240">Many Azure services provide additional logs and telemetry that can be configured to save data in your Azure Storage account, send to Event Hubs, and/or sent to an OMS Log Analytics workspace.</span></span> <span data-ttu-id="25d2d-241">Deze bewerking kan alleen worden uitgevoerd op het niveau van een resource en de storage-account of event hub moet aanwezig zijn in dezelfde regio bevinden als de doelresource waar de diagnostics-instelling is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="25d2d-241">That operation can only be performed at a resource level and the storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="25d2d-242">De diagnostische instelling niet ophalen</span><span class="sxs-lookup"><span data-stu-id="25d2d-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="25d2d-243">Diagnostische instelling uitschakelen</span><span class="sxs-lookup"><span data-stu-id="25d2d-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="25d2d-244">Schakel diagnostische instelling zonder bewaren</span><span class="sxs-lookup"><span data-stu-id="25d2d-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="25d2d-245">Schakel diagnostische instelling met bewaren</span><span class="sxs-lookup"><span data-stu-id="25d2d-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="25d2d-246">Schakel diagnostische instelling met de bewaarperiode voor een specifieke logboek-categorie</span><span class="sxs-lookup"><span data-stu-id="25d2d-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="25d2d-247">Schakel diagnostische instelling voor Event Hubs</span><span class="sxs-lookup"><span data-stu-id="25d2d-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="25d2d-248">Diagnostische instelling voor OMS inschakelen</span><span class="sxs-lookup"><span data-stu-id="25d2d-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
