---
title: aaaVertically scale Azure virtuele-machineschaalsets | Microsoft Docs
description: Hoe toovertically schaal van een virtuele Machine in antwoord toomonitoring waarschuwingen met Azure Automation
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a>Verticale automatisch geschaald met de virtuele Machine-schaalsets
Dit artikel wordt beschreven hoe toovertically Azure schalen [virtuele-Machineschaalsets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) met of zonder reprovisioning. Raadpleeg te voor verticale schaling van virtuele machines die niet in-schaalsets[verticaal schalen Azure virtuele machine met Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Verticale schaling, ook wel bekend als *opschalen* en *omlaag schalen*houdt in oplopende of aflopende volgorde grootten van virtuele machine (VM) op antwoord tooa werkbelasting. Vergelijk deze met [horizontaal schalen](virtual-machine-scale-sets-autoscale-overview.md), ook wel aangeduid tooas *uitschalen* en *schalen*, waarbij Hallo aantal VM's afhankelijk van de werkbelasting hello wordt gewijzigd.

Reprovisioning betekent het verwijderen van een bestaande VM te vervangen door een nieuwe. Wanneer u vergroten of Hallo grootte van virtuele machines in een VM-Schaalset verkleinen, in sommige gevallen u wilt tooresize bestaande virtuele machines en uw gegevens behouden, terwijl in andere gevallen u toodeploy moet nieuwe virtuele machines van de nieuwe grootte Hallo. Dit document bevat informatie over beide gevallen.

Verticale schaling kan handig zijn wanneer:

* Een service die is gebaseerd op virtuele machines is onder gebruikt (bijvoorbeeld in het weekend). Hallo VM verkleinen kunt maandelijkse kosten te verlagen.
* VM-grootte toocope met grotere vraag te vergroten zonder dat er extra virtuele machines.

U kunt een verticale instellen toobe geactiveerd schalen op basis van metrische waarschuwingen op basis van uw VM-Schaalset. Wanneer Hallo waarschuwing is geactiveerd. Deze gebeurtenis wordt gestart een webhook die een runbook die kan worden geschaald schaal omhoog of omlaag ingesteld triggers. Verticale schaling kan worden geconfigureerd met de volgende stappen:

1. Een Azure Automation-account maken met run as-functionaliteit.
2. Verticale schaal van Azure Automation-runbooks voor VM-Schaalsets importeren in uw abonnement.
3. Toevoegen van een webhook tooyour runbook.
4. Een waarschuwing tooyour VM-Schaalset met behulp van een webhook melding toevoegen.

> [!NOTE]
> Verticale automatisch schalen kan alleen plaatsvinden binnen een bepaalde adresbereiken van VM-formaten. Hallo-specificaties van elke grootte vergelijken voordat u besluit tooscale van één tooanother (hoger de waarde niet altijd wordt aangegeven in de VM-grootte groter). U kunt tooscale tussen Hallo paren van grootte te volgen:
> 
> | VM-grootten paar schalen |  |
> | --- | --- |
> | Standard_A0 |Standard_A11 |
> | Standard_D1 |Standard_D14 |
> | Standard_DS1 |Standard_DS14 |
> | Standard_D1v2 |Standard_D15v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a>Een Azure Automation-Account maken met run as-functionaliteit
u moet toodo Hallo-eerst is een Azure Automation-account die als host Hallo runbooks gebruikt tooscale Hallo VM-Schaalset exemplaren fungeert maken. Recent [Azure Automation](https://azure.microsoft.com/services/automation/) Hallo 'Uitvoeren als-account' functie waardoor Hallo Service-Principal instellen voor het automatisch uitvoeren van runbooks Hallo namens een gebruiker heel eenvoudig geïntroduceerd. U kunt meer lezen over deze in de onderstaande Hallo-artikel:

* [Runbooks verifiëren met een Azure Uitvoeren als-account](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Verticale schaal van Azure Automation-runbooks importeert in uw abonnement
Hallo runbooks nodig toovertically schaal die uw VM-Schaalsets al zijn gepubliceerd in de galerie van Azure Automation-Runbook Hallo. tooimport deze in uw abonnement Hallo Volg de stappen in dit artikel:

* [Runbook- en galerieën voor Azure Automation](../automation/automation-runbook-gallery.md)

Hallo bladeren galerie optie kiezen uit Hallo Runbooks menu:

![Runbooks toobe geïmporteerd][runbooks]

Hallo-runbooks die toobe geïmporteerd moeten worden weergegeven. Hallo runbook op basis van of u verticale schalen met of zonder reprovisioning wilt selecteren:

![Galerie met Runbooks][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a>Een webhook tooyour runbook toevoegen
Zodra u Hallo runbooks hebt geïmporteerd moet u een webhook toohello runbook tooadd zodat deze kan worden geactiveerd door een waarschuwing van een VM-Schaalset. Hallo-details van het maken van een webhook voor uw Runbook worden beschreven in dit artikel:

* [Azure Automation-webhooks.](../automation/automation-webhooks.md)

> [!NOTE]
> Zorg ervoor dat u Hallo webhook URI kopiëren voordat het Hallo-webhook dialoogvenster te sluiten als u dit in de volgende sectie Hallo moet.
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a>Toevoegen van een waarschuwing tooyour VM-Schaalset
Hieronder vindt u een PowerShell-script waaruit blijkt hoe tooadd een waarschuwing tooa VM-Schaalset. Raadpleeg toohello tooget Hallo artikelnaam van Hallo metrische toofire Hallo waarschuwing op te volgen: [Azure Monitor automatisch schalen algemene metrische gegevens](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> Het is aanbevolen tooconfigure een redelijke tijdvenster voor Hallo waarschuwing in volgorde tooavoid activerende verticaal schalen en alle gekoppelde service wordt onderbroken, te vaak. U kunt een venster van minimaal 20-30 minuten of langer. U kunt een horizontale schaal als u tooavoid onderbreking moet.
> 
> 

Voor meer informatie over hoe waarschuwingen toocreate verwijzen toohello volgende artikelen:

* [Azure PowerShell Monitor snel starten-voorbeelden](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [Azure Monitor platformoverschrijdende CLI snel starten-voorbeelden](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a>Samenvatting
In dit artikel hebt u geleerd eenvoudige verticaal vergroten/verkleinen voorbeelden. Met deze bouwstenen - Automation-account, runbooks, webhooks, waarschuwingen - kunt u een uitgebreide scala aan gebeurtenissen met een aangepaste set acties.

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
