---
title: aaaMigrate Azure waarschuwingen op gebeurtenissen Management tooActivity logboek waarschuwingen | Microsoft Docs
description: Waarschuwingen op gebeurtenissen management worden op 1 oktober verwijderd. Voorbereiden door te migreren bestaande waarschuwingen.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: johnkem
ms.openlocfilehash: e00bc4f0bad4e8f97443310770c333d250e343ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a><span data-ttu-id="7e0b0-104">Waarschuwingen van Azure op management tooActivity logboek waarschuwingen migreren</span><span class="sxs-lookup"><span data-stu-id="7e0b0-104">Migrate Azure alerts on management events tooActivity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="7e0b0-105">Waarschuwingen op gebeurtenissen management worden uitgeschakeld op of na oktober 1.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="7e0b0-106">Gebruik onderstaande toounderstand Hallo aanwijzingen als u deze waarschuwingen hebt en als dat het geval migreert.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-106">Use hello directions below toounderstand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="7e0b0-107">Wat wordt gewijzigd</span><span class="sxs-lookup"><span data-stu-id="7e0b0-107">What is changing</span></span>

<span data-ttu-id="7e0b0-108">Monitor voor Azure (voorheen Azure Insights) aangeboden een mogelijkheid toocreate een waarschuwing geactiveerd op gebeurtenissen en meldingen tooa webhook-URL of e-mailadressen gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-108">Azure Monitor (formerly Azure Insights) offered a capability toocreate an alert that triggered off of management events and generated notifications tooa webhook URL or email addresses.</span></span> <span data-ttu-id="7e0b0-109">U hebt gemaakt een van deze waarschuwingen van de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="7e0b0-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="7e0b0-110">In de Azure-portal voor bepaalde brontypen hello, onder bewaking -> waarschuwingen-waarschuwing toevoegen, waarbij 'Waarschuwen' is ingesteld te > 'Gebeurtenissen'</span><span class="sxs-lookup"><span data-stu-id="7e0b0-110">In hello Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set too“Events”</span></span>
* <span data-ttu-id="7e0b0-111">Door actieve Hallo toevoegen AzureRmLogAlertRule PowerShell-cmdlet</span><span class="sxs-lookup"><span data-stu-id="7e0b0-111">By running hello Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="7e0b0-112">Met behulp van rechtstreeks [waarschuwing REST-API Hallo](http://docs.microsoft.com/rest/api/monitor/alertrules) met odata.type = 'ManagementEventRuleCondition' en dataSource.odata.type = "RuleManagementEventDataSource"</span><span class="sxs-lookup"><span data-stu-id="7e0b0-112">By directly using [hello alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="7e0b0-113">Hallo retourneert volgende PowerShell-script een lijst met alle waarschuwingen op gebeurtenissen die u in uw abonnement, evenals de Hallo voorwaarden instellen voor elke waarschuwing hebt.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-113">hello following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as hello conditions set on each alert.</span></span>

```powershell
Login-AzureRmAccount
$alerts = $null
foreach ($rg in Get-AzureRmResourceGroup ) {
  $alerts += Get-AzureRmAlertRule -ResourceGroup $rg.ResourceGroupName
}
foreach ($alert in $alerts) {
  if($alert.Properties.Condition.DataSource.GetType().Name.Equals("RuleManagementEventDataSource")) {
    "Alert Name: " + $alert.Name
    "Alert Resource ID: " + $alert.Id
    "Alert conditions:"
    $alert.Properties.Condition.DataSource
    "---------------------------------"
  }
} 
```

<span data-ttu-id="7e0b0-114">Als er geen waarschuwingen voor van Beheergebeurtenissen, wordt een reeks waarschuwingsberichten zoals deze uitvoervenster het bovenstaande Hallo PowerShell-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7e0b0-114">If you have no alerts on management events, hello PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

<span data-ttu-id="7e0b0-115">Deze waarschuwingsberichten kunnen worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-115">These warning messages can be ignored.</span></span> <span data-ttu-id="7e0b0-116">Als u waarschuwingen op gebeurtenissen management hebt, Hallo-uitvoer van deze PowerShell-cmdlet ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="7e0b0-116">If you do have alerts on management events, hello output of this PowerShell cmdlet will look like this:</span></span>

```
Alert Name: webhookEvent1
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/webhookEvent1
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : microsoft.web/sites/start/action
ResourceGroupName    : 
ResourceProviderName : 
Status               : succeeded
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Web/sites/samplealertapp

---------------------------------
Alert Name: someclilogalert
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/someclilogalert
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : Start
ResourceGroupName    : 
ResourceProviderName : 
Status               : 
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Compute/virtualMachines/Seaofclouds

---------------------------------
```

<span data-ttu-id="7e0b0-117">Elke waarschuwing wordt gescheiden door een gestreepte lijn en details opnemen Hallo resource-ID van Hallo waarschuwing en de specifieke regel hello wordt bewaakt.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-117">Each alert is separated by a dashed line and details include hello resource ID of hello alert and hello specific rule being monitored.</span></span>

<span data-ttu-id="7e0b0-118">Deze functionaliteit is overgegaan te[waarschuwingen van Azure controleren activiteit logboek](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7e0b0-118">This functionality has been transitioned too[Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="7e0b0-119">Deze nieuwe waarschuwingen kunnen u een voorwaarde op activiteit logboekgebeurtenissen tooset en een melding ontvangen wanneer een nieuwe gebeurtenis overeenkomt met de Hallo voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-119">These new alerts enable you tooset a condition on Activity Log events and receive a notification when a new event matches hello condition.</span></span> <span data-ttu-id="7e0b0-120">Ze bieden ook verschillende verbeteringen van waarschuwingen op gebeurtenissen management:</span><span class="sxs-lookup"><span data-stu-id="7e0b0-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="7e0b0-121">U kunt uw groep geadresseerden voor meldingen ('acties') hergebruiken over veel waarschuwingen met [actiegroepen](monitoring-action-groups.md), waardoor de Hallo complexiteit van het wijzigen van wie een waarschuwing moet ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing hello complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="7e0b0-122">U kunt een melding ontvangen rechtstreeks op uw telefoon met SMS met groepen in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="7e0b0-123">U kunt [activiteit logboek waarschuwingen maken met Resource Manager-sjablonen](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="7e0b0-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="7e0b0-124">U kunt voorwaarden maken met meer flexibiliteit en complexiteit toomeet uw specifieke behoeften.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-124">You can create conditions with greater flexibility and complexity toomeet your specific needs.</span></span>
* <span data-ttu-id="7e0b0-125">Meldingen worden sneller afgeleverd.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-toomigrate"></a><span data-ttu-id="7e0b0-126">Hoe toomigrate</span><span class="sxs-lookup"><span data-stu-id="7e0b0-126">How toomigrate</span></span>
 
<span data-ttu-id="7e0b0-127">een nieuwe activiteit logboek waarschuwing toocreate, kunt u:</span><span class="sxs-lookup"><span data-stu-id="7e0b0-127">toocreate a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="7e0b0-128">Ga als volgt [onze richtlijnen voor hoe toocreate een waarschuwing in hello Azure-portal](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="7e0b0-128">Follow [our guide on how toocreate an alert in hello Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="7e0b0-129">Meer informatie over hoe te[een waarschuwing met een Resource Manager-sjabloon maken](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="7e0b0-129">Learn how too[create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="7e0b0-130">Waarschuwingen op het van Beheergebeurtenissen die u eerder hebt gemaakt, worden niet automatisch gemigreerd tooActivity logboek waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-130">Alerts on management events that you have previously created will not be automatically migrated tooActivity Log Alerts.</span></span> <span data-ttu-id="7e0b0-131">U moet toouse Hallo vóór het PowerShell-script toolist Hallo waarschuwingen op gebeurtenissen voor dat u momenteel hebt geconfigureerd en deze handmatig opnieuw als de activiteit logboek waarschuwingen maken.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-131">You need toouse hello preceding PowerShell script toolist hello alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="7e0b0-132">Dit moet worden uitgevoerd vóór oktober 1, waarna waarschuwingen op gebeurtenissen management niet langer zichtbaar zijn in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="7e0b0-133">Andere typen waarschuwingen van Azure, met inbegrip van metrische waarschuwingen van Azure controleren, Application Insights-waarschuwingen en Log Analytics waarschuwingen worden hierdoor niet beïnvloed door deze wijziging.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="7e0b0-134">Als u vragen hebt, kunt u boeken in Hallo opmerkingen hieronder.</span><span class="sxs-lookup"><span data-stu-id="7e0b0-134">If you have any questions, post in hello comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7e0b0-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7e0b0-135">Next steps</span></span>

* <span data-ttu-id="7e0b0-136">Meer informatie over [Activity Log](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="7e0b0-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="7e0b0-137">Configureer [activiteit logboek waarschuwingen per Azure-portal](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="7e0b0-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="7e0b0-138">Configureer [activiteit logboek waarschuwingen via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="7e0b0-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="7e0b0-139">Bekijk Hallo [activiteit logboek waarschuwing webhook schema](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="7e0b0-139">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="7e0b0-140">Meer informatie over [servicemeldingen](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="7e0b0-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="7e0b0-141">Meer informatie over [actiegroepen](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="7e0b0-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
