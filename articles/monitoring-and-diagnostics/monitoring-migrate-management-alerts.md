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
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a>Waarschuwingen van Azure op management tooActivity logboek waarschuwingen migreren


> [!WARNING]
> Waarschuwingen op gebeurtenissen management worden uitgeschakeld op of na oktober 1. Gebruik onderstaande toounderstand Hallo aanwijzingen als u deze waarschuwingen hebt en als dat het geval migreert.
>
> 

## <a name="what-is-changing"></a>Wat wordt gewijzigd

Monitor voor Azure (voorheen Azure Insights) aangeboden een mogelijkheid toocreate een waarschuwing geactiveerd op gebeurtenissen en meldingen tooa webhook-URL of e-mailadressen gegenereerd. U hebt gemaakt een van deze waarschuwingen van de volgende manieren:
* In de Azure-portal voor bepaalde brontypen hello, onder bewaking -> waarschuwingen-waarschuwing toevoegen, waarbij 'Waarschuwen' is ingesteld te > 'Gebeurtenissen'
* Door actieve Hallo toevoegen AzureRmLogAlertRule PowerShell-cmdlet
* Met behulp van rechtstreeks [waarschuwing REST-API Hallo](http://docs.microsoft.com/rest/api/monitor/alertrules) met odata.type = 'ManagementEventRuleCondition' en dataSource.odata.type = "RuleManagementEventDataSource"
 
Hallo retourneert volgende PowerShell-script een lijst met alle waarschuwingen op gebeurtenissen die u in uw abonnement, evenals de Hallo voorwaarden instellen voor elke waarschuwing hebt.

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

Als er geen waarschuwingen voor van Beheergebeurtenissen, wordt een reeks waarschuwingsberichten zoals deze uitvoervenster het bovenstaande Hallo PowerShell-cmdlet:

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

Deze waarschuwingsberichten kunnen worden genegeerd. Als u waarschuwingen op gebeurtenissen management hebt, Hallo-uitvoer van deze PowerShell-cmdlet ziet er als volgt:

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

Elke waarschuwing wordt gescheiden door een gestreepte lijn en details opnemen Hallo resource-ID van Hallo waarschuwing en de specifieke regel hello wordt bewaakt.

Deze functionaliteit is overgegaan te[waarschuwingen van Azure controleren activiteit logboek](monitoring-activity-log-alerts.md). Deze nieuwe waarschuwingen kunnen u een voorwaarde op activiteit logboekgebeurtenissen tooset en een melding ontvangen wanneer een nieuwe gebeurtenis overeenkomt met de Hallo voorwaarde. Ze bieden ook verschillende verbeteringen van waarschuwingen op gebeurtenissen management:
* U kunt uw groep geadresseerden voor meldingen ('acties') hergebruiken over veel waarschuwingen met [actiegroepen](monitoring-action-groups.md), waardoor de Hallo complexiteit van het wijzigen van wie een waarschuwing moet ontvangen.
* U kunt een melding ontvangen rechtstreeks op uw telefoon met SMS met groepen in te grijpen.
* U kunt [activiteit logboek waarschuwingen maken met Resource Manager-sjablonen](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
* U kunt voorwaarden maken met meer flexibiliteit en complexiteit toomeet uw specifieke behoeften.
* Meldingen worden sneller afgeleverd.
 
## <a name="how-toomigrate"></a>Hoe toomigrate
 
een nieuwe activiteit logboek waarschuwing toocreate, kunt u:
* Ga als volgt [onze richtlijnen voor hoe toocreate een waarschuwing in hello Azure-portal](monitoring-activity-log-alerts.md)
* Meer informatie over hoe te[een waarschuwing met een Resource Manager-sjabloon maken](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
 
Waarschuwingen op het van Beheergebeurtenissen die u eerder hebt gemaakt, worden niet automatisch gemigreerd tooActivity logboek waarschuwingen. U moet toouse Hallo vóór het PowerShell-script toolist Hallo waarschuwingen op gebeurtenissen voor dat u momenteel hebt geconfigureerd en deze handmatig opnieuw als de activiteit logboek waarschuwingen maken. Dit moet worden uitgevoerd vóór oktober 1, waarna waarschuwingen op gebeurtenissen management niet langer zichtbaar zijn in uw Azure-abonnement. Andere typen waarschuwingen van Azure, met inbegrip van metrische waarschuwingen van Azure controleren, Application Insights-waarschuwingen en Log Analytics waarschuwingen worden hierdoor niet beïnvloed door deze wijziging. Als u vragen hebt, kunt u boeken in Hallo opmerkingen hieronder.


## <a name="next-steps"></a>Volgende stappen

* Meer informatie over [Activity Log](monitoring-overview-activity-logs.md)
* Configureer [activiteit logboek waarschuwingen per Azure-portal](monitoring-activity-log-alerts.md)
* Configureer [activiteit logboek waarschuwingen via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Bekijk Hallo [activiteit logboek waarschuwing webhook schema](monitoring-activity-log-alerts-webhook.md)
* Meer informatie over [servicemeldingen](monitoring-service-notifications.md)
* Meer informatie over [actiegroepen](monitoring-action-groups.md)
