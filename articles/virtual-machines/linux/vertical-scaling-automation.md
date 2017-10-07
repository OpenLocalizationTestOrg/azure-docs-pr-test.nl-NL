---
title: aaaVertically scale Azure virtuele machine met Azure Automation | Microsoft Docs
description: Hoe toovertically virtuele Linux-Machine schalen in antwoord toomonitoring waarschuwingen met Azure Automation
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee4c1c33a588bd907d107f1828380a8afdaa725e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a><span data-ttu-id="0dd17-103">Azure Linux virtuele machine met Azure Automation verticaal te schalen</span><span class="sxs-lookup"><span data-stu-id="0dd17-103">Vertically scale Azure Linux virtual machine with Azure Automation</span></span>
<span data-ttu-id="0dd17-104">Verticale schaling is Hallo proces oplopende of aflopende volgorde Hallo resources van een machine in het antwoord toohello werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="0dd17-104">Vertical scaling is hello process of increasing or decreasing hello resources of a machine in response toohello workload.</span></span> <span data-ttu-id="0dd17-105">In Azure kunt dit doen door de tekengrootte Hallo Hallo virtuele Machine te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0dd17-105">In Azure this can be accomplished by changing hello size of hello Virtual Machine.</span></span> <span data-ttu-id="0dd17-106">Dit kan helpen in de volgende scenario's Hallo</span><span class="sxs-lookup"><span data-stu-id="0dd17-106">This can help in hello following scenarios</span></span>

* <span data-ttu-id="0dd17-107">Als de virtuele Machine Hallo niet vaak wordt gebruikt, kunt u het formaat omlaag tooa kleinere grootte tooreduce uw maandelijkse kosten</span><span class="sxs-lookup"><span data-stu-id="0dd17-107">If hello Virtual Machine is not being used frequently, you can resize it down tooa smaller size tooreduce your monthly costs</span></span>
* <span data-ttu-id="0dd17-108">Als Hallo virtuele Machine een piekbelasting ziet is, kan het formaat is gewijzigd tooa groter formaat tooincrease worden de capaciteit</span><span class="sxs-lookup"><span data-stu-id="0dd17-108">If hello Virtual Machine is seeing a peak load, it can be resized tooa larger size tooincrease its capacity</span></span>

<span data-ttu-id="0dd17-109">Hallo-overzicht voor Hallo stappen tooaccomplish dit omdat is hieronder</span><span class="sxs-lookup"><span data-stu-id="0dd17-109">hello outline for hello steps tooaccomplish this is as below</span></span>

1. <span data-ttu-id="0dd17-110">Uw virtuele Machines van Azure Automation tooaccess instellen</span><span class="sxs-lookup"><span data-stu-id="0dd17-110">Setup Azure Automation tooaccess your Virtual Machines</span></span>
2. <span data-ttu-id="0dd17-111">Hallo verticale schaal van Azure Automation-runbooks importeert in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="0dd17-111">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="0dd17-112">Een webhook tooyour runbook toevoegen</span><span class="sxs-lookup"><span data-stu-id="0dd17-112">Add a webhook tooyour runbook</span></span>
4. <span data-ttu-id="0dd17-113">Een waarschuwing tooyour virtuele Machine toevoegen</span><span class="sxs-lookup"><span data-stu-id="0dd17-113">Add an alert tooyour Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="0dd17-114">Vanwege de grootte van Hallo Hallo eerste virtuele Machine, Hallo grootten deze kan worden geschaald, mogelijk beperkt vanwege toohello beschikbaarheid van Hallo andere grootten in Hallo cluster huidige virtuele Machine wordt geïmplementeerd in.</span><span class="sxs-lookup"><span data-stu-id="0dd17-114">Because of hello size of hello first Virtual Machine, hello sizes it can be scaled to, may be limited due toohello availability of hello other sizes in hello cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="0dd17-115">In Hallo gepubliceerd automation-runbooks gebruikt in dit artikel we zorgt voor deze aanvraag en slechts worden opgeschaald binnen Hallo hieronder paren van VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="0dd17-115">In hello published automation runbooks used in this article we take care of this case and only scale within hello below VM size pairs.</span></span> <span data-ttu-id="0dd17-116">Dit betekent dat een Standard_D1v2 virtuele Machine wordt niet plotseling tooStandard_G5 vergroot of verkleind tooBasic_A0.</span><span class="sxs-lookup"><span data-stu-id="0dd17-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up tooStandard_G5 or scaled down tooBasic_A0.</span></span>
> 
> | <span data-ttu-id="0dd17-117">VM-grootten paar schalen</span><span class="sxs-lookup"><span data-stu-id="0dd17-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="0dd17-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="0dd17-118">Basic_A0</span></span> |<span data-ttu-id="0dd17-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="0dd17-119">Basic_A4</span></span> |
> | <span data-ttu-id="0dd17-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="0dd17-120">Standard_A0</span></span> |<span data-ttu-id="0dd17-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="0dd17-121">Standard_A4</span></span> |
> | <span data-ttu-id="0dd17-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="0dd17-122">Standard_A5</span></span> |<span data-ttu-id="0dd17-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="0dd17-123">Standard_A7</span></span> |
> | <span data-ttu-id="0dd17-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="0dd17-124">Standard_A8</span></span> |<span data-ttu-id="0dd17-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="0dd17-125">Standard_A9</span></span> |
> | <span data-ttu-id="0dd17-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="0dd17-126">Standard_A10</span></span> |<span data-ttu-id="0dd17-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="0dd17-127">Standard_A11</span></span> |
> | <span data-ttu-id="0dd17-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="0dd17-128">Standard_D1</span></span> |<span data-ttu-id="0dd17-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="0dd17-129">Standard_D4</span></span> |
> | <span data-ttu-id="0dd17-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="0dd17-130">Standard_D11</span></span> |<span data-ttu-id="0dd17-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="0dd17-131">Standard_D14</span></span> |
> | <span data-ttu-id="0dd17-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="0dd17-132">Standard_DS1</span></span> |<span data-ttu-id="0dd17-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="0dd17-133">Standard_DS4</span></span> |
> | <span data-ttu-id="0dd17-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="0dd17-134">Standard_DS11</span></span> |<span data-ttu-id="0dd17-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="0dd17-135">Standard_DS14</span></span> |
> | <span data-ttu-id="0dd17-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="0dd17-136">Standard_D1v2</span></span> |<span data-ttu-id="0dd17-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="0dd17-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="0dd17-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="0dd17-138">Standard_D11v2</span></span> |<span data-ttu-id="0dd17-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="0dd17-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="0dd17-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="0dd17-140">Standard_G1</span></span> |<span data-ttu-id="0dd17-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="0dd17-141">Standard_G5</span></span> |
> | <span data-ttu-id="0dd17-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="0dd17-142">Standard_GS1</span></span> |<span data-ttu-id="0dd17-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="0dd17-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a><span data-ttu-id="0dd17-144">Uw virtuele Machines van Azure Automation tooaccess instellen</span><span class="sxs-lookup"><span data-stu-id="0dd17-144">Setup Azure Automation tooaccess your Virtual Machines</span></span>
<span data-ttu-id="0dd17-145">u moet toodo Hallo-eerst is een Azure Automation-account die als host Hallo runbooks gebruikt tooscale Hallo VM-Schaalset exemplaren fungeert maken.</span><span class="sxs-lookup"><span data-stu-id="0dd17-145">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="0dd17-146">Hallo Automation-service is onlangs geïntroduceerd Hallo 'Uitvoeren als-account' functie waardoor Hallo Service-Principal instellen voor het automatisch uitvoeren van runbooks Hallo van Hallo gebruiker namens heel eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="0dd17-146">Recently hello Automation service introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on hello user's behalf very easy.</span></span> <span data-ttu-id="0dd17-147">U kunt meer lezen over deze in de onderstaande Hallo-artikel:</span><span class="sxs-lookup"><span data-stu-id="0dd17-147">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="0dd17-148">Runbooks verifiëren met een Azure Uitvoeren als-account</span><span class="sxs-lookup"><span data-stu-id="0dd17-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="0dd17-149">Hallo verticale schaal van Azure Automation-runbooks importeert in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="0dd17-149">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="0dd17-150">Hallo runbooks die nodig zijn voor het verticaal schalen van uw virtuele Machine al in de galerie van Azure Automation-Runbook Hallo zijn gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="0dd17-150">hello runbooks that are needed for Vertically Scaling your Virtual Machine are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="0dd17-151">U moet tooimport bij uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="0dd17-151">You will need tooimport them into your subscription.</span></span> <span data-ttu-id="0dd17-152">U leert hoe tooimport runbooks door te lezen Hallo volgende artikel.</span><span class="sxs-lookup"><span data-stu-id="0dd17-152">You can learn how tooimport runbooks by reading hello following article.</span></span>

* [<span data-ttu-id="0dd17-153">Runbook- en galerieën voor Azure Automation</span><span class="sxs-lookup"><span data-stu-id="0dd17-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="0dd17-154">Hallo-runbooks die toobe geïmporteerd moeten worden weergegeven in onderstaande afbeelding voor Hallo</span><span class="sxs-lookup"><span data-stu-id="0dd17-154">hello runbooks that need toobe imported are shown in hello image below</span></span>

![Importeren van runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="0dd17-156">Een webhook tooyour runbook toevoegen</span><span class="sxs-lookup"><span data-stu-id="0dd17-156">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="0dd17-157">Zodra u Hallo runbooks hebt geïmporteerd moet u een webhook toohello runbook tooadd zodat deze kan worden geactiveerd door een waarschuwing van een virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="0dd17-157">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="0dd17-158">Hallo-details van het maken van een webhook voor uw Runbook kunnen hier worden gelezen</span><span class="sxs-lookup"><span data-stu-id="0dd17-158">hello details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="0dd17-159">Azure Automation-webhooks.</span><span class="sxs-lookup"><span data-stu-id="0dd17-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="0dd17-160">Zorg ervoor dat u Hallo webhook kopiëren voordat het Hallo-webhook dialoogvenster te sluiten als u dit in de volgende sectie Hallo moet.</span><span class="sxs-lookup"><span data-stu-id="0dd17-160">Make sure you copy hello webhook before closing hello webhook dialog as you will need this in hello next section.</span></span>

## <a name="add-an-alert-tooyour-virtual-machine"></a><span data-ttu-id="0dd17-161">Een waarschuwing tooyour virtuele Machine toevoegen</span><span class="sxs-lookup"><span data-stu-id="0dd17-161">Add an alert tooyour Virtual Machine</span></span>
1. <span data-ttu-id="0dd17-162">Instellingen voor virtuele Machine selecteren</span><span class="sxs-lookup"><span data-stu-id="0dd17-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="0dd17-163">Selecteer 'Waarschuwingsregels'</span><span class="sxs-lookup"><span data-stu-id="0dd17-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="0dd17-164">Selecteer 'Waarschuwing toevoegen'</span><span class="sxs-lookup"><span data-stu-id="0dd17-164">Select "Add alert"</span></span>
4. <span data-ttu-id="0dd17-165">Selecteer een waarschuwing voor het Hallo van metrische toofire op</span><span class="sxs-lookup"><span data-stu-id="0dd17-165">Select a metric toofire hello alert on</span></span>
5. <span data-ttu-id="0dd17-166">Selecteer een voorwaarde die tijdens wordt voldaan Hallo waarschuwing toofire veroorzaken</span><span class="sxs-lookup"><span data-stu-id="0dd17-166">Select a condition, which when fulfilled will cause hello alert toofire</span></span>
6. <span data-ttu-id="0dd17-167">Selecteer een drempelwaarde voor Hallo voorwaarde in stap 5.</span><span class="sxs-lookup"><span data-stu-id="0dd17-167">Select a threshold for hello condition in Step 5.</span></span> <span data-ttu-id="0dd17-168">toobe voldaan</span><span class="sxs-lookup"><span data-stu-id="0dd17-168">toobe fulfilled</span></span>
7. <span data-ttu-id="0dd17-169">Selecteer een periode gedurende welke Hallo monitoring-service wordt gecontroleerd voor Hallo voorwaarde en de drempelwaarde in stap 5 en 6</span><span class="sxs-lookup"><span data-stu-id="0dd17-169">Select a period over which hello monitoring service will check for hello condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="0dd17-170">In het Hallo-webhook die u hebt gekopieerd uit de vorige sectie hello te plakken.</span><span class="sxs-lookup"><span data-stu-id="0dd17-170">Paste in hello webhook you copied from hello previous section.</span></span>

![Waarschuwing tooVirtual Machine 1 toevoegen](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Waarschuwing tooVirtual Machine 2 toevoegen](./media/vertical-scaling-automation/add-alert-webhook-2.png)

