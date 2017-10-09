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
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="e8be4-103">Verticale automatisch geschaald met de virtuele Machine-schaalsets</span><span class="sxs-lookup"><span data-stu-id="e8be4-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="e8be4-104">Dit artikel wordt beschreven hoe toovertically Azure schalen [virtuele-Machineschaalsets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) met of zonder reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="e8be4-104">This article describes how toovertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="e8be4-105">Raadpleeg te voor verticale schaling van virtuele machines die niet in-schaalsets[verticaal schalen Azure virtuele machine met Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8be4-105">For vertical scaling of VMs which are not in scale sets, refer too[Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="e8be4-106">Verticale schaling, ook wel bekend als *opschalen* en *omlaag schalen*houdt in oplopende of aflopende volgorde grootten van virtuele machine (VM) op antwoord tooa werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="e8be4-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response tooa workload.</span></span> <span data-ttu-id="e8be4-107">Vergelijk deze met [horizontaal schalen](virtual-machine-scale-sets-autoscale-overview.md), ook wel aangeduid tooas *uitschalen* en *schalen*, waarbij Hallo aantal VM's afhankelijk van de werkbelasting hello wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e8be4-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred tooas *scale out* and *scale in*, where hello number of VMs is altered depending on hello workload.</span></span>

<span data-ttu-id="e8be4-108">Reprovisioning betekent het verwijderen van een bestaande VM te vervangen door een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="e8be4-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="e8be4-109">Wanneer u vergroten of Hallo grootte van virtuele machines in een VM-Schaalset verkleinen, in sommige gevallen u wilt tooresize bestaande virtuele machines en uw gegevens behouden, terwijl in andere gevallen u toodeploy moet nieuwe virtuele machines van de nieuwe grootte Hallo.</span><span class="sxs-lookup"><span data-stu-id="e8be4-109">When you increase or decrease hello size of VMs in a VM Scale Set, in some cases you want tooresize existing VMs and retain your data, while in other cases you need toodeploy new VMs of hello new size.</span></span> <span data-ttu-id="e8be4-110">Dit document bevat informatie over beide gevallen.</span><span class="sxs-lookup"><span data-stu-id="e8be4-110">This document covers both cases.</span></span>

<span data-ttu-id="e8be4-111">Verticale schaling kan handig zijn wanneer:</span><span class="sxs-lookup"><span data-stu-id="e8be4-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="e8be4-112">Een service die is gebaseerd op virtuele machines is onder gebruikt (bijvoorbeeld in het weekend).</span><span class="sxs-lookup"><span data-stu-id="e8be4-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="e8be4-113">Hallo VM verkleinen kunt maandelijkse kosten te verlagen.</span><span class="sxs-lookup"><span data-stu-id="e8be4-113">Reducing hello VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="e8be4-114">VM-grootte toocope met grotere vraag te vergroten zonder dat er extra virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e8be4-114">Increasing VM size toocope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="e8be4-115">U kunt een verticale instellen toobe geactiveerd schalen op basis van metrische waarschuwingen op basis van uw VM-Schaalset.</span><span class="sxs-lookup"><span data-stu-id="e8be4-115">You can set up vertical scaling toobe triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="e8be4-116">Wanneer Hallo waarschuwing is geactiveerd. Deze gebeurtenis wordt gestart een webhook die een runbook die kan worden geschaald schaal omhoog of omlaag ingesteld triggers.</span><span class="sxs-lookup"><span data-stu-id="e8be4-116">When hello alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="e8be4-117">Verticale schaling kan worden geconfigureerd met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="e8be4-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="e8be4-118">Een Azure Automation-account maken met run as-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="e8be4-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="e8be4-119">Verticale schaal van Azure Automation-runbooks voor VM-Schaalsets importeren in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="e8be4-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="e8be4-120">Toevoegen van een webhook tooyour runbook.</span><span class="sxs-lookup"><span data-stu-id="e8be4-120">Add a webhook tooyour runbook.</span></span>
4. <span data-ttu-id="e8be4-121">Een waarschuwing tooyour VM-Schaalset met behulp van een webhook melding toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e8be4-121">Add an alert tooyour VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="e8be4-122">Verticale automatisch schalen kan alleen plaatsvinden binnen een bepaalde adresbereiken van VM-formaten.</span><span class="sxs-lookup"><span data-stu-id="e8be4-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="e8be4-123">Hallo-specificaties van elke grootte vergelijken voordat u besluit tooscale van één tooanother (hoger de waarde niet altijd wordt aangegeven in de VM-grootte groter).</span><span class="sxs-lookup"><span data-stu-id="e8be4-123">Compare hello specifications of each size before deciding tooscale from one tooanother (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="e8be4-124">U kunt tooscale tussen Hallo paren van grootte te volgen:</span><span class="sxs-lookup"><span data-stu-id="e8be4-124">You can choose tooscale between hello following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="e8be4-125">VM-grootten paar schalen</span><span class="sxs-lookup"><span data-stu-id="e8be4-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="e8be4-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="e8be4-126">Standard_A0</span></span> |<span data-ttu-id="e8be4-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="e8be4-127">Standard_A11</span></span> |
> | <span data-ttu-id="e8be4-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="e8be4-128">Standard_D1</span></span> |<span data-ttu-id="e8be4-129">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="e8be4-129">Standard_D14</span></span> |
> | <span data-ttu-id="e8be4-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="e8be4-130">Standard_DS1</span></span> |<span data-ttu-id="e8be4-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="e8be4-131">Standard_DS14</span></span> |
> | <span data-ttu-id="e8be4-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="e8be4-132">Standard_D1v2</span></span> |<span data-ttu-id="e8be4-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="e8be4-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="e8be4-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="e8be4-134">Standard_G1</span></span> |<span data-ttu-id="e8be4-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="e8be4-135">Standard_G5</span></span> |
> | <span data-ttu-id="e8be4-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="e8be4-136">Standard_GS1</span></span> |<span data-ttu-id="e8be4-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="e8be4-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="e8be4-138">Een Azure Automation-Account maken met run as-functionaliteit</span><span class="sxs-lookup"><span data-stu-id="e8be4-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="e8be4-139">u moet toodo Hallo-eerst is een Azure Automation-account die als host Hallo runbooks gebruikt tooscale Hallo VM-Schaalset exemplaren fungeert maken.</span><span class="sxs-lookup"><span data-stu-id="e8be4-139">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="e8be4-140">Recent [Azure Automation](https://azure.microsoft.com/services/automation/) Hallo 'Uitvoeren als-account' functie waardoor Hallo Service-Principal instellen voor het automatisch uitvoeren van runbooks Hallo namens een gebruiker heel eenvoudig geïntroduceerd.</span><span class="sxs-lookup"><span data-stu-id="e8be4-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="e8be4-141">U kunt meer lezen over deze in de onderstaande Hallo-artikel:</span><span class="sxs-lookup"><span data-stu-id="e8be4-141">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="e8be4-142">Runbooks verifiëren met een Azure Uitvoeren als-account</span><span class="sxs-lookup"><span data-stu-id="e8be4-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="e8be4-143">Verticale schaal van Azure Automation-runbooks importeert in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="e8be4-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="e8be4-144">Hallo runbooks nodig toovertically schaal die uw VM-Schaalsets al zijn gepubliceerd in de galerie van Azure Automation-Runbook Hallo.</span><span class="sxs-lookup"><span data-stu-id="e8be4-144">hello runbooks needed toovertically scale your VM Scale Sets are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="e8be4-145">tooimport deze in uw abonnement Hallo Volg de stappen in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="e8be4-145">tooimport them into your subscription follow hello steps in this article:</span></span>

* [<span data-ttu-id="e8be4-146">Runbook- en galerieën voor Azure Automation</span><span class="sxs-lookup"><span data-stu-id="e8be4-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="e8be4-147">Hallo bladeren galerie optie kiezen uit Hallo Runbooks menu:</span><span class="sxs-lookup"><span data-stu-id="e8be4-147">Choose hello Browse Gallery option from hello Runbooks menu:</span></span>

![Runbooks toobe geïmporteerd][runbooks]

<span data-ttu-id="e8be4-149">Hallo-runbooks die toobe geïmporteerd moeten worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e8be4-149">hello runbooks that need toobe imported are shown.</span></span> <span data-ttu-id="e8be4-150">Hallo runbook op basis van of u verticale schalen met of zonder reprovisioning wilt selecteren:</span><span class="sxs-lookup"><span data-stu-id="e8be4-150">Select hello runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Galerie met Runbooks][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="e8be4-152">Een webhook tooyour runbook toevoegen</span><span class="sxs-lookup"><span data-stu-id="e8be4-152">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="e8be4-153">Zodra u Hallo runbooks hebt geïmporteerd moet u een webhook toohello runbook tooadd zodat deze kan worden geactiveerd door een waarschuwing van een VM-Schaalset.</span><span class="sxs-lookup"><span data-stu-id="e8be4-153">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="e8be4-154">Hallo-details van het maken van een webhook voor uw Runbook worden beschreven in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="e8be4-154">hello details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="e8be4-155">Azure Automation-webhooks.</span><span class="sxs-lookup"><span data-stu-id="e8be4-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="e8be4-156">Zorg ervoor dat u Hallo webhook URI kopiëren voordat het Hallo-webhook dialoogvenster te sluiten als u dit in de volgende sectie Hallo moet.</span><span class="sxs-lookup"><span data-stu-id="e8be4-156">Make sure you copy hello webhook URI before closing hello webhook dialog as you will need this in hello next section.</span></span>
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a><span data-ttu-id="e8be4-157">Toevoegen van een waarschuwing tooyour VM-Schaalset</span><span class="sxs-lookup"><span data-stu-id="e8be4-157">Add an alert tooyour VM Scale Set</span></span>
<span data-ttu-id="e8be4-158">Hieronder vindt u een PowerShell-script waaruit blijkt hoe tooadd een waarschuwing tooa VM-Schaalset.</span><span class="sxs-lookup"><span data-stu-id="e8be4-158">Below is a PowerShell script which shows how tooadd an alert tooa VM Scale Set.</span></span> <span data-ttu-id="e8be4-159">Raadpleeg toohello tooget Hallo artikelnaam van Hallo metrische toofire Hallo waarschuwing op te volgen: [Azure Monitor automatisch schalen algemene metrische gegevens](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e8be4-159">Refer toohello following article tooget hello name of hello metric toofire hello alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

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
> <span data-ttu-id="e8be4-160">Het is aanbevolen tooconfigure een redelijke tijdvenster voor Hallo waarschuwing in volgorde tooavoid activerende verticaal schalen en alle gekoppelde service wordt onderbroken, te vaak.</span><span class="sxs-lookup"><span data-stu-id="e8be4-160">It is recommended tooconfigure a reasonable time window for hello alert in order tooavoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="e8be4-161">U kunt een venster van minimaal 20-30 minuten of langer.</span><span class="sxs-lookup"><span data-stu-id="e8be4-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="e8be4-162">U kunt een horizontale schaal als u tooavoid onderbreking moet.</span><span class="sxs-lookup"><span data-stu-id="e8be4-162">Consider horizontal scaling if you need tooavoid any interruption.</span></span>
> 
> 

<span data-ttu-id="e8be4-163">Voor meer informatie over hoe waarschuwingen toocreate verwijzen toohello volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="e8be4-163">For more information on how toocreate alerts refer toohello following articles:</span></span>

* [<span data-ttu-id="e8be4-164">Azure PowerShell Monitor snel starten-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="e8be4-164">Azure Monitor PowerShell quick start samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="e8be4-165">Azure Monitor platformoverschrijdende CLI snel starten-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="e8be4-165">Azure Monitor Cross-platform CLI quick start samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="e8be4-166">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="e8be4-166">Summary</span></span>
<span data-ttu-id="e8be4-167">In dit artikel hebt u geleerd eenvoudige verticaal vergroten/verkleinen voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="e8be4-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="e8be4-168">Met deze bouwstenen - Automation-account, runbooks, webhooks, waarschuwingen - kunt u een uitgebreide scala aan gebeurtenissen met een aangepaste set acties.</span><span class="sxs-lookup"><span data-stu-id="e8be4-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
