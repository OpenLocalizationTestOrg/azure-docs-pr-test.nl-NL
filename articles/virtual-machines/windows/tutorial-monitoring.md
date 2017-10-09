---
title: aaaAzure bewaking en virtuele Machines van Windows | Microsoft Docs
description: Zelfstudie - Monitor voor een virtuele Windows-Machine met Azure PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="9bd91-103">Een virtuele Windows-Machine met Azure PowerShell bewaken</span><span class="sxs-lookup"><span data-stu-id="9bd91-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="9bd91-104">Agents toocollect opstarten Azure bewaking gebruikt en prestatiegegevens van de virtuele Azure-machines, deze gegevens opslaan in Azure-opslag en om het programma toegankelijk via de portal, Azure PowerShell-module Hallo en hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9bd91-104">Azure monitoring uses agents toocollect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, hello Azure PowerShell module, and hello Azure CLI.</span></span> <span data-ttu-id="9bd91-105">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="9bd91-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9bd91-106">Diagnostische gegevens over opstarten op een virtuele machine inschakelen</span><span class="sxs-lookup"><span data-stu-id="9bd91-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="9bd91-107">Diagnostische gegevens over opstarten bekijken</span><span class="sxs-lookup"><span data-stu-id="9bd91-107">View boot diagnostics</span></span>
> * <span data-ttu-id="9bd91-108">Metrische gegevens weergeven VM-host</span><span class="sxs-lookup"><span data-stu-id="9bd91-108">View VM host metrics</span></span>
> * <span data-ttu-id="9bd91-109">Hallo-extensie voor diagnostische gegevens installeren</span><span class="sxs-lookup"><span data-stu-id="9bd91-109">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="9bd91-110">Metrische gegevens weergeven VM</span><span class="sxs-lookup"><span data-stu-id="9bd91-110">View VM metrics</span></span>
> * <span data-ttu-id="9bd91-111">Maken van een waarschuwing</span><span class="sxs-lookup"><span data-stu-id="9bd91-111">Create an alert</span></span>
> * <span data-ttu-id="9bd91-112">Geavanceerde controle instellen</span><span class="sxs-lookup"><span data-stu-id="9bd91-112">Set up advanced monitoring</span></span>

<span data-ttu-id="9bd91-113">Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="9bd91-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="9bd91-114">Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="9bd91-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="9bd91-115">Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="9bd91-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="9bd91-116">toocomplete hello voorbeeld in deze zelfstudie, moet u een bestaande virtuele machine hebben.</span><span class="sxs-lookup"><span data-stu-id="9bd91-116">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="9bd91-117">Indien nodig, dit [voorbeeldscript](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) kunt maken voor u.</span><span class="sxs-lookup"><span data-stu-id="9bd91-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="9bd91-118">Als u werkt Hallo zelfstudie, vervangen, VM-naam en locatie van resourcegroep Hallo waar nodig.</span><span class="sxs-lookup"><span data-stu-id="9bd91-118">When working through hello tutorial, replace hello resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="9bd91-119">Diagnostische gegevens over opstarten bekijken</span><span class="sxs-lookup"><span data-stu-id="9bd91-119">View boot diagnostics</span></span>

<span data-ttu-id="9bd91-120">Als Windows virtuele machines opstarten, vastgelegd Hallo boot diagnoseagent schermuitvoer die kan worden gebruikt voor het oplossen van doel.</span><span class="sxs-lookup"><span data-stu-id="9bd91-120">As Windows virtual machines boot up, hello boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="9bd91-121">Deze mogelijkheid is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9bd91-121">This capability is enabled by default.</span></span> <span data-ttu-id="9bd91-122">Hallo vastgelegd scherm schermafbeeldingen worden opgeslagen in een Azure storage-account wordt ook standaard gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9bd91-122">hello captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="9bd91-123">U krijgt Hallo opstarten diagnostische gegevens met Hallo [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) opdracht.</span><span class="sxs-lookup"><span data-stu-id="9bd91-123">You can get hello boot diagnostic data with hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="9bd91-124">Diagnostische gegevens over opstarten zijn Hallo voorbeeld te volgen, gedownloade toohello hoofdmap Hallo * c:\* station.</span><span class="sxs-lookup"><span data-stu-id="9bd91-124">In hello following example, boot diagnostics are downloaded toohello root of hello *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="9bd91-125">Metrische gegevens weergeven host</span><span class="sxs-lookup"><span data-stu-id="9bd91-125">View host metrics</span></span>

<span data-ttu-id="9bd91-126">Een virtuele machine van Windows heeft een specifieke Host-virtuele machine in Azure die deze met samenwerkt.</span><span class="sxs-lookup"><span data-stu-id="9bd91-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="9bd91-127">Metrische gegevens worden automatisch verzameld voor Hallo Host, en kunnen worden weergegeven in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9bd91-127">Metrics are automatically collected for hello Host and can be viewed in hello Azure portal.</span></span>

1. <span data-ttu-id="9bd91-128">In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.</span><span class="sxs-lookup"><span data-stu-id="9bd91-128">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="9bd91-129">Klik op **metrische gegevens** op Hallo van VM-blade, en selecteer vervolgens een van de Host metrische gegevens Hallo onder **beschikbare metrische gegevens** toosee hoe Hallo VM-Host wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9bd91-129">Click **Metrics** on hello VM blade, and then select any of hello Host metrics under **Available metrics** toosee how hello Host VM is performing.</span></span>

    ![Metrische gegevens weergeven host](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="9bd91-131">Installeren van de extensie voor diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="9bd91-131">Install diagnostics extension</span></span>

<span data-ttu-id="9bd91-132">Hallo basic host metrische gegevens beschikbaar zijn, maar meer gedetailleerd toosee en VM-specifieke metrische gegevens en u tooneed tooinstall hello Azure extensie voor diagnostische gegevens op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="9bd91-132">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="9bd91-133">Hello Azure diagnostics-extensie kan aanvullende controle en diagnostische gegevens toobe opgehaald uit Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="9bd91-133">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="9bd91-134">U kunt deze maatstaven voor prestaties weergeven en waarschuwingen op basis van hoe Hallo VM wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9bd91-134">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="9bd91-135">Hallo diagnostische uitbreiding wordt geïnstalleerd via hello Azure-portal als volgt:</span><span class="sxs-lookup"><span data-stu-id="9bd91-135">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="9bd91-136">In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.</span><span class="sxs-lookup"><span data-stu-id="9bd91-136">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="9bd91-137">Klik op **diagnose instellingen**.</span><span class="sxs-lookup"><span data-stu-id="9bd91-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="9bd91-138">Hallo lijst ziet u dat *opstarten diagnostics* al uit de vorige sectie Hallo zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9bd91-138">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="9bd91-139">Klik op het selectievakje Hallo voor *basismetrieken*.</span><span class="sxs-lookup"><span data-stu-id="9bd91-139">Click hello check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="9bd91-140">Klik op Hallo **gastniveau bewaking inschakelen** knop.</span><span class="sxs-lookup"><span data-stu-id="9bd91-140">Click hello **Enable guest-level monitoring** button.</span></span>

    ![Diagnostische metrische gegevens weergeven](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="9bd91-142">Metrische gegevens weergeven VM</span><span class="sxs-lookup"><span data-stu-id="9bd91-142">View VM metrics</span></span>

<span data-ttu-id="9bd91-143">U kunt Hallo VM metrische gegevens weergeven in Hallo dezelfde manier dat Hallo host VM metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="9bd91-143">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="9bd91-144">In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.</span><span class="sxs-lookup"><span data-stu-id="9bd91-144">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="9bd91-145">toosee het Hallo VM wordt uitgevoerd, klikt u op **metrische gegevens** op Hallo van VM-blade, en selecteer vervolgens een van de diagnostische gegevens metrische gegevens Hallo onder **beschikbare metrische gegevens**.</span><span class="sxs-lookup"><span data-stu-id="9bd91-145">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Metrische gegevens weergeven VM](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="9bd91-147">Waarschuwingen maken</span><span class="sxs-lookup"><span data-stu-id="9bd91-147">Create alerts</span></span>

<span data-ttu-id="9bd91-148">U kunt waarschuwingen op basis van specifieke prestatiewaarden kunt maken.</span><span class="sxs-lookup"><span data-stu-id="9bd91-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="9bd91-149">Waarschuwingen kunnen bijvoorbeeld gebruikte toonotify u wanneer het gemiddelde CPU-gebruik overschrijdt een bepaalde drempelwaarde of beschikbare vrije schijfruimte onder een bepaalde hoeveelheid zakt.</span><span class="sxs-lookup"><span data-stu-id="9bd91-149">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="9bd91-150">Waarschuwingen worden weergegeven in hello Azure-portal of kunnen worden verzonden via e-mail.</span><span class="sxs-lookup"><span data-stu-id="9bd91-150">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="9bd91-151">U kunt ook Azure Automation-runbooks of Azure Logic Apps activeren in het antwoord tooalerts wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="9bd91-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="9bd91-152">Hallo wordt volgende voorbeeld een waarschuwing voor het gemiddelde CPU-gebruik.</span><span class="sxs-lookup"><span data-stu-id="9bd91-152">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="9bd91-153">In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.</span><span class="sxs-lookup"><span data-stu-id="9bd91-153">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="9bd91-154">Klik op **waarschuwing regels** op Hallo VM blade en klik vervolgens op **metrische waarschuwing toevoegen** aan de bovenkant Hallo van Hallo waarschuwingen-blade.</span><span class="sxs-lookup"><span data-stu-id="9bd91-154">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="9bd91-155">Geef een **naam** voor de waarschuwing, zoals *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="9bd91-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="9bd91-156">een waarschuwing wanneer CPU-percentage 1.0 gedurende vijf minuten overschrijdt tootrigger standaardinstellingen laten staan alle Hallo andere geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="9bd91-156">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="9bd91-157">Eventueel selectievakje Hallo in voor *e-eigenaren, bijdragers en lezers* toosend e-mailmeldingen.</span><span class="sxs-lookup"><span data-stu-id="9bd91-157">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="9bd91-158">Hallo standaardactie is toopresent een melding in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="9bd91-158">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="9bd91-159">Klik op Hallo **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="9bd91-159">Click hello **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="9bd91-160">Geavanceerde controle</span><span class="sxs-lookup"><span data-stu-id="9bd91-160">Advanced monitoring</span></span> 

<span data-ttu-id="9bd91-161">U kunt doen meer geavanceerde bewaking van uw virtuele machine met behulp van [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="9bd91-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="9bd91-162">Als u dit nog niet hebt gedaan, kunt u zich aanmelden voor een [gratis proefversie](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) van Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="9bd91-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="9bd91-163">Wanneer u toegang toohello OMS-portal hebt, kunt u Hallo werkruimte sleutel en de werkruimte-id vinden op de blade instellingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="9bd91-163">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="9bd91-164">Gebruik Hallo [Set AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd Hallo OMS-extensie toohello VM.</span><span class="sxs-lookup"><span data-stu-id="9bd91-164">Use hello [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd hello OMS extension toohello VM.</span></span> <span data-ttu-id="9bd91-165">Update Hallo variabele waarden in Hallo hieronder voorbeeld tooreflect u werkruimtesleutel OMS en werkruimte-id.</span><span class="sxs-lookup"><span data-stu-id="9bd91-165">Update hello variable values in hello below sample tooreflect you OMS workspace key and workspace Id.</span></span>  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

<span data-ttu-id="9bd91-166">Na een paar minuten ziet u nieuwe virtuele machine in de OMS-werkruimte Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="9bd91-166">After a few minutes, you should see hello new VM in hello OMS workspace.</span></span> 

![OMS-blade](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="9bd91-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9bd91-168">Next steps</span></span>
<span data-ttu-id="9bd91-169">In deze zelfstudie hebt geconfigureerd en virtuele machines in Azure Security Center gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="9bd91-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="9bd91-170">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="9bd91-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9bd91-171">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="9bd91-171">Create a virtual network</span></span>
> * <span data-ttu-id="9bd91-172">Een resourcegroep en de virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="9bd91-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="9bd91-173">Diagnostische gegevens over opstarten op Hallo VM inschakelen</span><span class="sxs-lookup"><span data-stu-id="9bd91-173">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="9bd91-174">Diagnostische gegevens over opstarten bekijken</span><span class="sxs-lookup"><span data-stu-id="9bd91-174">View boot diagnostics</span></span>
> * <span data-ttu-id="9bd91-175">Metrische gegevens weergeven host</span><span class="sxs-lookup"><span data-stu-id="9bd91-175">View host metrics</span></span>
> * <span data-ttu-id="9bd91-176">Hallo-extensie voor diagnostische gegevens installeren</span><span class="sxs-lookup"><span data-stu-id="9bd91-176">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="9bd91-177">Metrische gegevens weergeven VM</span><span class="sxs-lookup"><span data-stu-id="9bd91-177">View VM metrics</span></span>
> * <span data-ttu-id="9bd91-178">Maken van een waarschuwing</span><span class="sxs-lookup"><span data-stu-id="9bd91-178">Create an alert</span></span>
> * <span data-ttu-id="9bd91-179">Geavanceerde controle instellen</span><span class="sxs-lookup"><span data-stu-id="9bd91-179">Set up advanced monitoring</span></span>

<span data-ttu-id="9bd91-180">Ga toohello volgende zelfstudie toolearn over Azure security center.</span><span class="sxs-lookup"><span data-stu-id="9bd91-180">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9bd91-181">VM-beveiliging beheren</span><span class="sxs-lookup"><span data-stu-id="9bd91-181">Manage VM security</span></span>](./tutorial-azure-security.md)