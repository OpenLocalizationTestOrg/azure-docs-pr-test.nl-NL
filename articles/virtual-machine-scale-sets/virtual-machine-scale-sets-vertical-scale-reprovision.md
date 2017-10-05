---
title: Virtuele machine van Azure-schaalsets verticaal te schalen | Microsoft Docs
description: Een virtuele Machine verticaal te schalen in reactie op waarschuwingen met Azure Automation bewaken
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
ms.openlocfilehash: 9159a5a9041864fe06785829121233379c46bb03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="d7894-103">Verticale automatisch geschaald met de virtuele Machine-schaalsets</span><span class="sxs-lookup"><span data-stu-id="d7894-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="d7894-104">Dit artikel wordt beschreven hoe u Azure verticaal te schalen [virtuele-Machineschaalsets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) met of zonder reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="d7894-104">This article describes how to vertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="d7894-105">Raadpleeg voor verticale schaling van virtuele machines die niet in-schaalsets [verticaal schalen Azure virtuele machine met Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d7894-105">For vertical scaling of VMs which are not in scale sets, refer to [Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="d7894-106">Verticale schaling, ook wel bekend als *opschalen* en *omlaag schalen*houdt in oplopende of aflopende volgorde van de grootte van de virtuele machines (VM) in reactie op een werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="d7894-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response to a workload.</span></span> <span data-ttu-id="d7894-107">Vergelijk deze met [horizontaal schalen](virtual-machine-scale-sets-autoscale-overview.md), ook wel *uitschalen* en *schalen*, waarbij het aantal VM's afhankelijk van de werkbelasting wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="d7894-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred to as *scale out* and *scale in*, where the number of VMs is altered depending on the workload.</span></span>

<span data-ttu-id="d7894-108">Reprovisioning betekent het verwijderen van een bestaande VM te vervangen door een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="d7894-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="d7894-109">Wanneer u vergroten of verkleinen van de grootte van virtuele machines in een VM-Schaalset, in sommige gevallen wilt u de grootte van bestaande virtuele machines wijzigen en uw gegevens behouden, terwijl in andere gevallen moet u nieuwe virtuele machines van de nieuwe grootte implementeren.</span><span class="sxs-lookup"><span data-stu-id="d7894-109">When you increase or decrease the size of VMs in a VM Scale Set, in some cases you want to resize existing VMs and retain your data, while in other cases you need to deploy new VMs of the new size.</span></span> <span data-ttu-id="d7894-110">Dit document bevat informatie over beide gevallen.</span><span class="sxs-lookup"><span data-stu-id="d7894-110">This document covers both cases.</span></span>

<span data-ttu-id="d7894-111">Verticale schaling kan handig zijn wanneer:</span><span class="sxs-lookup"><span data-stu-id="d7894-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="d7894-112">Een service die is gebaseerd op virtuele machines is onder gebruikt (bijvoorbeeld in het weekend).</span><span class="sxs-lookup"><span data-stu-id="d7894-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="d7894-113">De VM-grootte verminderen kunt maandelijkse kosten te verlagen.</span><span class="sxs-lookup"><span data-stu-id="d7894-113">Reducing the VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="d7894-114">VM-grootte toenemend omgaan met grotere verzoek zonder extra virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="d7894-114">Increasing VM size to cope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="d7894-115">U kunt instellen verticaal schalen om te worden geactiveerd op basis van metrische waarschuwingen op basis van uw VM-Schaalset.</span><span class="sxs-lookup"><span data-stu-id="d7894-115">You can set up vertical scaling to be triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="d7894-116">Wanneer de waarschuwing is geactiveerd. Deze gebeurtenis wordt gestart een webhook die een runbook die kan worden geschaald schaal omhoog of omlaag ingesteld triggers.</span><span class="sxs-lookup"><span data-stu-id="d7894-116">When the alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="d7894-117">Verticale schaling kan worden geconfigureerd met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="d7894-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="d7894-118">Een Azure Automation-account maken met run as-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="d7894-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="d7894-119">Verticale schaal van Azure Automation-runbooks voor VM-Schaalsets importeren in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="d7894-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="d7894-120">Een webhook toevoegen aan uw runbook.</span><span class="sxs-lookup"><span data-stu-id="d7894-120">Add a webhook to your runbook.</span></span>
4. <span data-ttu-id="d7894-121">Een waarschuwing toevoegen aan uw VM-Schaalset met behulp van een webhook-melding.</span><span class="sxs-lookup"><span data-stu-id="d7894-121">Add an alert to your VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="d7894-122">Verticale automatisch schalen kan alleen plaatsvinden binnen een bepaalde adresbereiken van VM-formaten.</span><span class="sxs-lookup"><span data-stu-id="d7894-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="d7894-123">Vergelijk de specificaties van elke grootte voordat u besluit om te schalen van een aan een andere (hoger de waarde niet altijd wordt aangegeven in de VM-grootte groter).</span><span class="sxs-lookup"><span data-stu-id="d7894-123">Compare the specifications of each size before deciding to scale from one to another (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="d7894-124">U kunt kiezen tussen de volgende paren van grootte schalen:</span><span class="sxs-lookup"><span data-stu-id="d7894-124">You can choose to scale between the following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="d7894-125">VM-grootten paar schalen</span><span class="sxs-lookup"><span data-stu-id="d7894-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="d7894-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="d7894-126">Standard_A0</span></span> |<span data-ttu-id="d7894-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="d7894-127">Standard_A11</span></span> |
> | <span data-ttu-id="d7894-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="d7894-128">Standard_D1</span></span> |<span data-ttu-id="d7894-129">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="d7894-129">Standard_D14</span></span> |
> | <span data-ttu-id="d7894-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="d7894-130">Standard_DS1</span></span> |<span data-ttu-id="d7894-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="d7894-131">Standard_DS14</span></span> |
> | <span data-ttu-id="d7894-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="d7894-132">Standard_D1v2</span></span> |<span data-ttu-id="d7894-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="d7894-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="d7894-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="d7894-134">Standard_G1</span></span> |<span data-ttu-id="d7894-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="d7894-135">Standard_G5</span></span> |
> | <span data-ttu-id="d7894-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="d7894-136">Standard_GS1</span></span> |<span data-ttu-id="d7894-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="d7894-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="d7894-138">Een Azure Automation-Account maken met run as-functionaliteit</span><span class="sxs-lookup"><span data-stu-id="d7894-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="d7894-139">Het eerste wat dat u moet doen is een Azure Automation-account die als host voor de runbooks gebruikt fungeert voor het schalen van de VM-Schaalset exemplaren maken.</span><span class="sxs-lookup"><span data-stu-id="d7894-139">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale the VM Scale Set instances.</span></span> <span data-ttu-id="d7894-140">Recent [Azure Automation](https://azure.microsoft.com/services/automation/) geïntroduceerd van de functie 'Run As-account', waardoor de instelling van de Service-Principal voor het automatisch uitvoeren van de runbooks namens een gebruiker heel eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="d7894-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="d7894-141">U kunt meer lezen over deze in het artikel hieronder:</span><span class="sxs-lookup"><span data-stu-id="d7894-141">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="d7894-142">Runbooks verifiëren met een Azure Uitvoeren als-account</span><span class="sxs-lookup"><span data-stu-id="d7894-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="d7894-143">Verticale schaal van Azure Automation-runbooks importeert in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="d7894-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="d7894-144">De runbooks die nodig zijn voor uw VM-Schaalsets verticaal te schalen zijn al gepubliceerd in de galerie van Azure Automation Runbook.</span><span class="sxs-lookup"><span data-stu-id="d7894-144">The runbooks needed to vertically scale your VM Scale Sets are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="d7894-145">Als u wilt importeren stappen in uw abonnement de in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="d7894-145">To import them into your subscription follow the steps in this article:</span></span>

* [<span data-ttu-id="d7894-146">Runbook- en galerieën voor Azure Automation</span><span class="sxs-lookup"><span data-stu-id="d7894-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="d7894-147">Kies de optie Galerij bladeren in het menu Runbooks:</span><span class="sxs-lookup"><span data-stu-id="d7894-147">Choose the Browse Gallery option from the Runbooks menu:</span></span>

![Runbooks moeten worden geïmporteerd][runbooks]

<span data-ttu-id="d7894-149">De runbooks die moeten worden geïmporteerd, worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d7894-149">The runbooks that need to be imported are shown.</span></span> <span data-ttu-id="d7894-150">Selecteer het runbook op basis van of u wilt dat verticale met of zonder reprovisioning schalen:</span><span class="sxs-lookup"><span data-stu-id="d7894-150">Select the runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Galerie met Runbooks][gallery]

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="d7894-152">Een webhook toevoegen aan uw runbook</span><span class="sxs-lookup"><span data-stu-id="d7894-152">Add a webhook to your runbook</span></span>
<span data-ttu-id="d7894-153">Zodra u hebt geïmporteerd toevoegen de runbooks u moet een webhook aan het runbook, zodat deze kan worden geactiveerd door een waarschuwing van een VM-Schaalset.</span><span class="sxs-lookup"><span data-stu-id="d7894-153">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="d7894-154">De details van het maken van een webhook voor uw Runbook worden beschreven in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="d7894-154">The details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="d7894-155">Azure Automation-webhooks.</span><span class="sxs-lookup"><span data-stu-id="d7894-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="d7894-156">Zorg ervoor dat u de webhook URI kopiëren voordat u sluit het dialoogvenster webhook want u dit in de volgende sectie moet.</span><span class="sxs-lookup"><span data-stu-id="d7894-156">Make sure you copy the webhook URI before closing the webhook dialog as you will need this in the next section.</span></span>
> 
> 

## <a name="add-an-alert-to-your-vm-scale-set"></a><span data-ttu-id="d7894-157">Een waarschuwing toevoegen aan uw VM-Schaalset</span><span class="sxs-lookup"><span data-stu-id="d7894-157">Add an alert to your VM Scale Set</span></span>
<span data-ttu-id="d7894-158">Hieronder vindt u een PowerShell-script die laat zien hoe een waarschuwing toevoegt aan een VM-Schaalset.</span><span class="sxs-lookup"><span data-stu-id="d7894-158">Below is a PowerShell script which shows how to add an alert to a VM Scale Set.</span></span> <span data-ttu-id="d7894-159">Raadpleeg het volgende artikel om op te halen van de naam van de metrische gegevens voor het starten van de waarschuwing in: [Azure Monitor automatisch schalen algemene metrische gegevens](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d7894-159">Refer to the following article to get the name of the metric to fire the alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

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
> <span data-ttu-id="d7894-160">Het verdient aanbeveling voor het configureren van een redelijke tijdvenster voor de waarschuwing om te voorkomen dat verticaal schalen en de bijbehorende service-onderbreking, te vaak activering.</span><span class="sxs-lookup"><span data-stu-id="d7894-160">It is recommended to configure a reasonable time window for the alert in order to avoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="d7894-161">U kunt een venster van minimaal 20-30 minuten of langer.</span><span class="sxs-lookup"><span data-stu-id="d7894-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="d7894-162">U kunt een horizontale schaal als u wilt vermijden.</span><span class="sxs-lookup"><span data-stu-id="d7894-162">Consider horizontal scaling if you need to avoid any interruption.</span></span>
> 
> 

<span data-ttu-id="d7894-163">Raadpleeg de volgende artikelen voor meer informatie over het maken van waarschuwingen:</span><span class="sxs-lookup"><span data-stu-id="d7894-163">For more information on how to create alerts refer to the following articles:</span></span>

* [<span data-ttu-id="d7894-164">Azure PowerShell Monitor snel starten-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="d7894-164">Azure Monitor PowerShell quick start samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="d7894-165">Azure Monitor platformoverschrijdende CLI snel starten-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="d7894-165">Azure Monitor Cross-platform CLI quick start samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="d7894-166">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d7894-166">Summary</span></span>
<span data-ttu-id="d7894-167">In dit artikel hebt u geleerd eenvoudige verticaal vergroten/verkleinen voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="d7894-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="d7894-168">Met deze bouwstenen - Automation-account, runbooks, webhooks, waarschuwingen - kunt u een uitgebreide scala aan gebeurtenissen met een aangepaste set acties.</span><span class="sxs-lookup"><span data-stu-id="d7894-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
