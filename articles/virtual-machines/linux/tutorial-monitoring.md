---
title: aaaMonitor Linux virtuele machines in Azure | Microsoft Docs
description: Meer informatie over hoe toomonitor diagnostische gegevens en maatstaven voor prestaties opstarten op een virtuele Linux-machine in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="e36e7-103">Hoe toomonitor virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="e36e7-103">How toomonitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="e36e7-104">tooensure die uw virtuele machines (VM's) in Azure correct worden uitgevoerd, kunt u diagnostische gegevens over opstarten en maatstaven voor prestaties bekijken.</span><span class="sxs-lookup"><span data-stu-id="e36e7-104">tooensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="e36e7-105">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="e36e7-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e36e7-106">Diagnostische gegevens over opstarten op Hallo VM inschakelen</span><span class="sxs-lookup"><span data-stu-id="e36e7-106">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="e36e7-107">Diagnostische gegevens over opstarten bekijken</span><span class="sxs-lookup"><span data-stu-id="e36e7-107">View boot diagnostics</span></span>
> * <span data-ttu-id="e36e7-108">Metrische gegevens weergeven host</span><span class="sxs-lookup"><span data-stu-id="e36e7-108">View host metrics</span></span>
> * <span data-ttu-id="e36e7-109">Extensie voor diagnostische gegevens op Hallo VM inschakelen</span><span class="sxs-lookup"><span data-stu-id="e36e7-109">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="e36e7-110">Metrische gegevens weergeven VM</span><span class="sxs-lookup"><span data-stu-id="e36e7-110">View VM metrics</span></span>
> * <span data-ttu-id="e36e7-111">Waarschuwingen op basis van diagnostische gegevens maken</span><span class="sxs-lookup"><span data-stu-id="e36e7-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="e36e7-112">Geavanceerde controle instellen</span><span class="sxs-lookup"><span data-stu-id="e36e7-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e36e7-113">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="e36e7-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e36e7-114">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="e36e7-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e36e7-115">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e36e7-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="e36e7-116">VM maken</span><span class="sxs-lookup"><span data-stu-id="e36e7-116">Create VM</span></span>

<span data-ttu-id="e36e7-117">toosee diagnostische gegevens en metrische gegevens in te grijpen, moet u een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e36e7-117">toosee diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="e36e7-118">Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e36e7-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e36e7-119">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupMonitor* in Hallo *eastus* locatie.</span><span class="sxs-lookup"><span data-stu-id="e36e7-119">hello following example creates a resource group named *myResourceGroupMonitor* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="e36e7-120">Maak nu een virtuele machine met [az vm maken](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e36e7-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="e36e7-121">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM*:</span><span class="sxs-lookup"><span data-stu-id="e36e7-121">hello following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="e36e7-122">Diagnostische gegevens over opstarten inschakelen</span><span class="sxs-lookup"><span data-stu-id="e36e7-122">Enable boot diagnostics</span></span>

<span data-ttu-id="e36e7-123">Virtuele Linux-machines opstart, boot-uitvoer worden vastgelegd en opgeslagen in Azure storage Hallo opstarten diagnostische extensie.</span><span class="sxs-lookup"><span data-stu-id="e36e7-123">As Linux VMs boot, hello boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="e36e7-124">Deze gegevens kunnen worden gebruikt tootroubleshoot VM opstartproblemen.</span><span class="sxs-lookup"><span data-stu-id="e36e7-124">This data can be used tootroubleshoot VM boot issues.</span></span> <span data-ttu-id="e36e7-125">Diagnostische gegevens over opstarten zijn niet automatisch ingeschakeld wanneer u een Linux-VM met behulp van Azure CLI Hallo maakt.</span><span class="sxs-lookup"><span data-stu-id="e36e7-125">Boot diagnostics are not automatically enabled when you create a Linux VM using hello Azure CLI.</span></span>

<span data-ttu-id="e36e7-126">Voordat u diagnostische gegevens over opstarten inschakelt, moet een opslagaccount toobe gemaakt voor het opslaan van de logboeken van de opstartinstallatiekopie.</span><span class="sxs-lookup"><span data-stu-id="e36e7-126">Before enabling boot diagnostics, a storage account needs toobe created for storing boot logs.</span></span> <span data-ttu-id="e36e7-127">Storage-accounts moeten een globaal unieke naam hebben, tussen 3 en 24 tekens bevatten en mogen alleen cijfers en kleine letters bevatten.</span><span class="sxs-lookup"><span data-stu-id="e36e7-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="e36e7-128">Een opslagaccount maken met de Hallo [az storage-account maken](/cli/azure/storage/account#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e36e7-128">Create a storage account with hello [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="e36e7-129">In dit voorbeeld wordt een willekeurige tekenreeks gebruikte toocreate een unieke opslagaccountnaam.</span><span class="sxs-lookup"><span data-stu-id="e36e7-129">In this example, a random string is used toocreate a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="e36e7-130">Bij het inschakelen van diagnostische gegevens over opstarten is Hallo URI toohello blob storage-container vereist.</span><span class="sxs-lookup"><span data-stu-id="e36e7-130">When enabling boot diagnostics, hello URI toohello blob storage container is needed.</span></span> <span data-ttu-id="e36e7-131">Hallo Hallo volgende opdracht query's storage account tooreturn deze URI.</span><span class="sxs-lookup"><span data-stu-id="e36e7-131">hello following command queries hello storage account tooreturn this URI.</span></span> <span data-ttu-id="e36e7-132">Hallo URI-waarde wordt opgeslagen in een variabelenamen *bloburi*, die wordt gebruikt in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="e36e7-132">hello URI value is stored in a variable names *bloburi*, which is used in hello next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="e36e7-133">Nu inschakelen diagnostische gegevens over opstarten met [az vm-diagnostische gegevens over opstarten inschakelen](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="e36e7-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="e36e7-134">Hallo `--storage` waarde Hallo blob URI verzameld in de vorige stap Hallo is.</span><span class="sxs-lookup"><span data-stu-id="e36e7-134">hello `--storage` value is hello blob URI collected in hello previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="e36e7-135">Diagnostische gegevens over opstarten bekijken</span><span class="sxs-lookup"><span data-stu-id="e36e7-135">View boot diagnostics</span></span>

<span data-ttu-id="e36e7-136">Wanneer diagnostische gegevens over opstarten zijn ingeschakeld, telkens wanneer u stoppen en starten Hallo VM, informatie over het opstartproces Hallo geschreven tooa logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="e36e7-136">When boot diagnostics are enabled, each time you stop and start hello VM, information about hello boot process is written tooa log file.</span></span> <span data-ttu-id="e36e7-137">Voor dit voorbeeld moet u eerst Hallo VM Hello ongedaan [az vm ongedaan](/cli/azure/vm#deallocate) opdracht als volgt:</span><span class="sxs-lookup"><span data-stu-id="e36e7-137">For this example, first deallocate hello VM with hello [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="e36e7-138">Hallo VM nu beginnen met Hallo [az vm start]( /cli/azure/vm#stop) opdracht als volgt:</span><span class="sxs-lookup"><span data-stu-id="e36e7-138">Now start hello VM with hello [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="e36e7-139">U krijgt Hallo opstarten diagnostische gegevens voor *myVM* Hello [az vm diagnostische gegevens over opstarten get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) opdracht als volgt:</span><span class="sxs-lookup"><span data-stu-id="e36e7-139">You can get hello boot diagnostic data for *myVM* with hello [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="e36e7-140">Metrische gegevens weergeven host</span><span class="sxs-lookup"><span data-stu-id="e36e7-140">View host metrics</span></span>

<span data-ttu-id="e36e7-141">Een Linux-VM heeft toegewezen host in Azure die deze met samenwerkt.</span><span class="sxs-lookup"><span data-stu-id="e36e7-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="e36e7-142">Metrische gegevens worden automatisch verzameld voor Hallo host en kan worden bekeken in hello Azure-portal als volgt:</span><span class="sxs-lookup"><span data-stu-id="e36e7-142">Metrics are automatically collected for hello host and can be viewed in hello Azure portal as follows:</span></span>

1. <span data-ttu-id="e36e7-143">In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroupMonitor**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.</span><span class="sxs-lookup"><span data-stu-id="e36e7-143">In hello Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="e36e7-144">toosee het Hallo host VM wordt uitgevoerd, klikt u op **metrische gegevens** op Hallo VM blade en selecteer vervolgens een Hallo *[Host]* metrische gegevens onder **beschikbare metrische gegevens**.</span><span class="sxs-lookup"><span data-stu-id="e36e7-144">toosee how hello host VM is performing, click **Metrics** on hello VM blade, then select any of hello *[Host]* metrics under **Available metrics**.</span></span>

    ![Metrische gegevens weergeven host](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="e36e7-146">Installeren van de extensie voor diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="e36e7-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e36e7-147">Dit document beschrijft versie 2.3 Hallo Linux diagnostische extensie, die is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="e36e7-147">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="e36e7-148">Versie 2.3 worden tot en met 30 juni 2018 ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e36e7-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="e36e7-149">Versie 3.0 Hallo diagnostische Linux-extensie kan in plaats daarvan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e36e7-149">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="e36e7-150">Zie voor meer informatie [Hallo documentatie](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e36e7-150">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="e36e7-151">Hallo basic host metrische gegevens beschikbaar zijn, maar meer gedetailleerd toosee en VM-specifieke metrische gegevens en u tooneed tooinstall hello Azure extensie voor diagnostische gegevens op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="e36e7-151">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="e36e7-152">Hello Azure diagnostics-extensie kan aanvullende controle en diagnostische gegevens toobe opgehaald uit Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="e36e7-152">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="e36e7-153">U kunt deze maatstaven voor prestaties weergeven en waarschuwingen op basis van hoe Hallo VM wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e36e7-153">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="e36e7-154">Hallo diagnostische uitbreiding wordt geïnstalleerd via hello Azure-portal als volgt:</span><span class="sxs-lookup"><span data-stu-id="e36e7-154">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="e36e7-155">In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.</span><span class="sxs-lookup"><span data-stu-id="e36e7-155">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="e36e7-156">Klik op **diagnose instellingen**.</span><span class="sxs-lookup"><span data-stu-id="e36e7-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="e36e7-157">Hallo lijst ziet u dat *opstarten diagnostics* al uit de vorige sectie Hallo zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e36e7-157">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="e36e7-158">Klik op het selectievakje Hallo voor *basismetrieken*.</span><span class="sxs-lookup"><span data-stu-id="e36e7-158">Click hello check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="e36e7-159">In Hallo *opslagaccount* sectie, selecteer Hallo tooand Bladeren *mydiagdata [1234]* account gemaakt in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="e36e7-159">In hello *Storage account* section, browse tooand select hello *mydiagdata[1234]* account created in hello previous section.</span></span>
1. <span data-ttu-id="e36e7-160">Klik op Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e36e7-160">Click hello **Save** button.</span></span>

    ![Diagnostische metrische gegevens weergeven](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="e36e7-162">Metrische gegevens weergeven VM</span><span class="sxs-lookup"><span data-stu-id="e36e7-162">View VM metrics</span></span>

<span data-ttu-id="e36e7-163">U kunt Hallo VM metrische gegevens weergeven in Hallo dezelfde manier dat Hallo host VM metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="e36e7-163">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="e36e7-164">In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.</span><span class="sxs-lookup"><span data-stu-id="e36e7-164">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="e36e7-165">toosee het Hallo VM wordt uitgevoerd, klikt u op **metrische gegevens** op Hallo van VM-blade, en selecteer vervolgens een van de diagnostische gegevens metrische gegevens Hallo onder **beschikbare metrische gegevens**.</span><span class="sxs-lookup"><span data-stu-id="e36e7-165">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Metrische gegevens weergeven VM](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="e36e7-167">Waarschuwingen maken</span><span class="sxs-lookup"><span data-stu-id="e36e7-167">Create alerts</span></span>

<span data-ttu-id="e36e7-168">U kunt waarschuwingen op basis van specifieke prestatiewaarden kunt maken.</span><span class="sxs-lookup"><span data-stu-id="e36e7-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="e36e7-169">Waarschuwingen kunnen bijvoorbeeld gebruikte toonotify u wanneer het gemiddelde CPU-gebruik overschrijdt een bepaalde drempelwaarde of beschikbare vrije schijfruimte onder een bepaalde hoeveelheid zakt.</span><span class="sxs-lookup"><span data-stu-id="e36e7-169">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="e36e7-170">Waarschuwingen worden weergegeven in hello Azure-portal of kunnen worden verzonden via e-mail.</span><span class="sxs-lookup"><span data-stu-id="e36e7-170">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="e36e7-171">U kunt ook Azure Automation-runbooks of Azure Logic Apps activeren in het antwoord tooalerts wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="e36e7-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="e36e7-172">Hallo wordt volgende voorbeeld een waarschuwing voor het gemiddelde CPU-gebruik.</span><span class="sxs-lookup"><span data-stu-id="e36e7-172">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="e36e7-173">In hello Azure-portal, klikt u op **resourcegroepen**, selecteer **myResourceGroup**, en selecteer vervolgens **myVM** in de lijst met resources Hallo.</span><span class="sxs-lookup"><span data-stu-id="e36e7-173">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="e36e7-174">Klik op **waarschuwing regels** op Hallo VM blade en klik vervolgens op **metrische waarschuwing toevoegen** aan de bovenkant Hallo van Hallo waarschuwingen-blade.</span><span class="sxs-lookup"><span data-stu-id="e36e7-174">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="e36e7-175">Geef een **naam** voor de waarschuwing, zoals *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="e36e7-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="e36e7-176">een waarschuwing wanneer CPU-percentage 1.0 gedurende vijf minuten overschrijdt tootrigger standaardinstellingen laten staan alle Hallo andere geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="e36e7-176">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="e36e7-177">Eventueel selectievakje Hallo in voor *e-eigenaren, bijdragers en lezers* toosend e-mailmeldingen.</span><span class="sxs-lookup"><span data-stu-id="e36e7-177">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="e36e7-178">Hallo standaardactie is toopresent een melding in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="e36e7-178">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="e36e7-179">Klik op Hallo **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="e36e7-179">Click hello **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="e36e7-180">Geavanceerde controle</span><span class="sxs-lookup"><span data-stu-id="e36e7-180">Advanced monitoring</span></span> 

<span data-ttu-id="e36e7-181">U kunt doen meer geavanceerde bewaking van uw virtuele machine met behulp van [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="e36e7-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="e36e7-182">Als u dit nog niet hebt gedaan, kunt u zich aanmelden voor een [gratis proefversie](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) van Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="e36e7-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="e36e7-183">Wanneer u toegang toohello OMS-portal hebt, kunt u Hallo werkruimte sleutel en de werkruimte-id vinden op de blade instellingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="e36e7-183">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="e36e7-184">Vervang < werkruimtesleutel > en < werkruimte-id > Hallo waarden voor uit uw OMS werkruimte en u vervolgens kunt gebruiken **az vm-extensie set** tooadd Hallo OMS-extensie toohello VM:</span><span class="sxs-lookup"><span data-stu-id="e36e7-184">Replace <workspace-key> and <workspace-id> with hello values for from your OMS workspace and then you can use **az vm extension set** tooadd hello OMS extension toohello VM:</span></span>

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

<span data-ttu-id="e36e7-185">Op Hallo logboek Search-blade van Hallo OMS-portal, ziet u *myVM* zoals wat wordt weergegeven in de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="e36e7-185">On hello Log Search blade of hello OMS portal, you should see *myVM* such as what is shown in hello following picture:</span></span>

![OMS-blade](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="e36e7-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e36e7-187">Next steps</span></span>

<span data-ttu-id="e36e7-188">In deze zelfstudie hebt geconfigureerd en virtuele machines in Azure Security Center gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="e36e7-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="e36e7-189">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="e36e7-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e36e7-190">Diagnostische gegevens over opstarten op Hallo VM inschakelen</span><span class="sxs-lookup"><span data-stu-id="e36e7-190">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="e36e7-191">Diagnostische gegevens over opstarten bekijken</span><span class="sxs-lookup"><span data-stu-id="e36e7-191">View boot diagnostics</span></span>
> * <span data-ttu-id="e36e7-192">Metrische gegevens weergeven host</span><span class="sxs-lookup"><span data-stu-id="e36e7-192">View host metrics</span></span>
> * <span data-ttu-id="e36e7-193">Extensie voor diagnostische gegevens op Hallo VM inschakelen</span><span class="sxs-lookup"><span data-stu-id="e36e7-193">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="e36e7-194">Metrische gegevens weergeven VM</span><span class="sxs-lookup"><span data-stu-id="e36e7-194">View VM metrics</span></span>
> * <span data-ttu-id="e36e7-195">Waarschuwingen op basis van diagnostische gegevens maken</span><span class="sxs-lookup"><span data-stu-id="e36e7-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="e36e7-196">Geavanceerde controle instellen</span><span class="sxs-lookup"><span data-stu-id="e36e7-196">Set up advanced monitoring</span></span>

<span data-ttu-id="e36e7-197">Ga toohello volgende zelfstudie toolearn over Azure security center.</span><span class="sxs-lookup"><span data-stu-id="e36e7-197">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e36e7-198">VM-beveiliging beheren</span><span class="sxs-lookup"><span data-stu-id="e36e7-198">Manage VM security</span></span>](./tutorial-azure-security.md)