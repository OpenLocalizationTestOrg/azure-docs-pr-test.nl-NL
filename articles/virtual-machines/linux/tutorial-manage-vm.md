---
title: aaaCreate- en Linux VM's beheren met Azure CLI Hallo | Microsoft Docs
description: Zelfstudie - maken en beheren van virtuele Linux-machines met hello Azure CLI
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a><span data-ttu-id="afedf-103">Maken en beheren van virtuele Linux-machines met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="afedf-103">Create and Manage Linux VMs with hello Azure CLI</span></span>

<span data-ttu-id="afedf-104">Virtuele machines van Azure bieden een volledig worden geconfigureerd en flexibele computeromgeving.</span><span class="sxs-lookup"><span data-stu-id="afedf-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="afedf-105">Deze zelfstudie bevat informatie over basic virtuele machine van Azure-implementatie items zoals het selecteren van een VM-grootte, een VM-installatiekopie te selecteren en implementeren van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="afedf-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="afedf-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="afedf-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="afedf-107">Maken en koppelen tooa VM</span><span class="sxs-lookup"><span data-stu-id="afedf-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="afedf-108">Selecteer en gebruik van VM-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="afedf-108">Select and use VM images</span></span>
> * <span data-ttu-id="afedf-109">Weergeven en gebruiken van specifieke VM-grootten</span><span class="sxs-lookup"><span data-stu-id="afedf-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="afedf-110">De grootte van een virtuele machine wijzigen</span><span class="sxs-lookup"><span data-stu-id="afedf-110">Resize a VM</span></span>
> * <span data-ttu-id="afedf-111">Bekijken en te begrijpen status virtuele machine</span><span class="sxs-lookup"><span data-stu-id="afedf-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="afedf-112">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="afedf-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="afedf-113">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="afedf-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="afedf-114">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="afedf-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="afedf-115">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="afedf-115">Create resource group</span></span>

<span data-ttu-id="afedf-116">Een resourcegroep maken met de Hallo [az groep maken](https://docs.microsoft.com/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="afedf-116">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="afedf-117">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="afedf-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="afedf-118">Een resourcegroep moet worden gemaakt voordat een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="afedf-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="afedf-119">In dit voorbeeld wordt een resourcegroep met de naam *myResourceGroupVM* wordt gemaakt in Hallo *eastus* regio.</span><span class="sxs-lookup"><span data-stu-id="afedf-119">In this example, a resource group named *myResourceGroupVM* is created in hello *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="afedf-120">Hallo-resourcegroep is opgegeven bij het maken of wijzigen van een virtuele machine die in deze zelfstudie kan worden gezien.</span><span class="sxs-lookup"><span data-stu-id="afedf-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="afedf-121">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="afedf-121">Create virtual machine</span></span>

<span data-ttu-id="afedf-122">Een virtuele machine maken met de Hallo [az vm maken](https://docs.microsoft.com/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="afedf-122">Create a virtual machine with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="afedf-123">Wanneer u een virtuele machine maakt, er zijn diverse opties beschikbaar zoals besturingssysteemkopie schijf sizing en administratieve referenties.</span><span class="sxs-lookup"><span data-stu-id="afedf-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="afedf-124">In dit voorbeeld wordt een virtuele machine gemaakt met de naam *myVM* Ubuntu Server uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="afedf-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="afedf-125">Eenmaal Hallo die VM is gemaakt, levert hello Azure CLI informatie over Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="afedf-125">Once hello VM has been created, hello Azure CLI outputs information about hello VM.</span></span> <span data-ttu-id="afedf-126">Let op Hallo `publicIpAddress`, dit adres mag gebruikte tooaccess Hallo virtuele machine...</span><span class="sxs-lookup"><span data-stu-id="afedf-126">Take note of hello `publicIpAddress`, this address can be used tooaccess hello virtual machine..</span></span> 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a><span data-ttu-id="afedf-127">Verbinding maken met tooVM</span><span class="sxs-lookup"><span data-stu-id="afedf-127">Connect tooVM</span></span>

<span data-ttu-id="afedf-128">U kunt nu verbinding toohello VM via SSH.</span><span class="sxs-lookup"><span data-stu-id="afedf-128">You can now connect toohello VM using SSH.</span></span> <span data-ttu-id="afedf-129">Hallo voorbeeld IP-adres vervangen door Hallo `publicIpAddress` in Hallo vorige stap hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="afedf-129">Replace hello example IP address with hello `publicIpAddress` noted in hello previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="afedf-130">Zodra u klaar bent met de Hallo VM, sluit u Hallo SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="afedf-130">Once finished with hello VM, close hello SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="afedf-131">VM-installatiekopieën begrijpen</span><span class="sxs-lookup"><span data-stu-id="afedf-131">Understand VM images</span></span>

<span data-ttu-id="afedf-132">Hello Azure marketplace bevat veel afbeeldingen die gebruikt toocreate virtuele machines worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="afedf-132">hello Azure marketplace includes many images that can be used toocreate VMs.</span></span> <span data-ttu-id="afedf-133">In de vorige stappen hello, is een virtuele machine gemaakt met behulp van een installatiekopie van een virtuele Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="afedf-133">In hello previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="afedf-134">Hello die Azure CLI gebruikte toosearch Hallo marketplace voor een installatiekopie CentOS, die vervolgens wordt gebruikt in deze stap toodeploy een tweede virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="afedf-134">In this step, hello Azure CLI is used toosearch hello marketplace for a CentOS image, which is then used toodeploy a second virtual machine.</span></span>  

<span data-ttu-id="afedf-135">een lijst met Hallo toosee meest gebruikte afbeeldingen, gebruikt u Hallo [az vm afbeeldingenlijst](/cli/azure/vm/image#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="afedf-135">toosee a list of hello most commonly used images, use hello [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="afedf-136">Hallo-opdrachtuitvoer retourneert de meest populaire VM-installatiekopieën Hallo op Azure.</span><span class="sxs-lookup"><span data-stu-id="afedf-136">hello command output returns hello most popular VM images on Azure.</span></span>

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

<span data-ttu-id="afedf-137">Een volledige lijst ziet door toe te voegen Hallo `--all` argument.</span><span class="sxs-lookup"><span data-stu-id="afedf-137">A full list can be seen by adding hello `--all` argument.</span></span> <span data-ttu-id="afedf-138">lijst met Hallo afbeeldingen kan ook worden gefilterd door `--publisher` of `–-offer`.</span><span class="sxs-lookup"><span data-stu-id="afedf-138">hello image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="afedf-139">In dit voorbeeld wordt Hallo lijst gefilterd voor alle afbeeldingen met een aanbieding die overeenkomt met *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="afedf-139">In this example, hello list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="afedf-140">Gedeeltelijke uitvoer:</span><span class="sxs-lookup"><span data-stu-id="afedf-140">Partial output:</span></span>

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

<span data-ttu-id="afedf-141">een virtuele machine met de installatiekopie van een specifieke toodeploy Noteer van Hallo-waarde in Hallo *Urn* kolom.</span><span class="sxs-lookup"><span data-stu-id="afedf-141">toodeploy a VM using a specific image, take note of hello value in hello *Urn* column.</span></span> <span data-ttu-id="afedf-142">Bij het opgeven van de installatiekopie van het Hallo kan versienummer Hallo-installatiekopie worden vervangen door 'nieuwste', die Hallo meest recente versie van Hallo-distributiepunt selecteert.</span><span class="sxs-lookup"><span data-stu-id="afedf-142">When specifying hello image, hello image version number can be replaced with “latest”, which selects hello latest version of hello distribution.</span></span> <span data-ttu-id="afedf-143">In dit voorbeeld Hallo `--image` argument gebruikte toospecify Hallo meest recente versie van de installatiekopie van een CentOS 6.5 is.</span><span class="sxs-lookup"><span data-stu-id="afedf-143">In this example, hello `--image` argument is used toospecify hello latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="afedf-144">VM-grootten begrijpen</span><span class="sxs-lookup"><span data-stu-id="afedf-144">Understand VM sizes</span></span>

<span data-ttu-id="afedf-145">De grootte van een virtuele machine bepaalt Hallo hoeveelheid rekenresources zoals CPU en GPU geheugen die beschikbaar toohello virtuele machine zijn aangebracht.</span><span class="sxs-lookup"><span data-stu-id="afedf-145">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="afedf-146">Toobe de juiste grootte voor de werklast Hallo verwacht, moeten virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="afedf-146">Virtual machines need toobe sized appropriately for hello expected work load.</span></span> <span data-ttu-id="afedf-147">Als de werkbelasting toeneemt, kan een bestaande virtuele machine kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="afedf-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="afedf-148">VM-grootten</span><span class="sxs-lookup"><span data-stu-id="afedf-148">VM Sizes</span></span>

<span data-ttu-id="afedf-149">Hallo tabel categoriseert grootten in gebruiksvoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="afedf-149">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="afedf-150">Type</span><span class="sxs-lookup"><span data-stu-id="afedf-150">Type</span></span>                     | <span data-ttu-id="afedf-151">Grootten</span><span class="sxs-lookup"><span data-stu-id="afedf-151">Sizes</span></span>           |    <span data-ttu-id="afedf-152">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="afedf-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="afedf-153">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="afedf-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="afedf-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0 7</span><span class="sxs-lookup"><span data-stu-id="afedf-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="afedf-155">Taakverdeling CPU-naar-geheugen.</span><span class="sxs-lookup"><span data-stu-id="afedf-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="afedf-156">Ideaal voor dev / test- en kleine toomedium toepassingen en gegevens oplossingen.</span><span class="sxs-lookup"><span data-stu-id="afedf-156">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| [<span data-ttu-id="afedf-157">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="afedf-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="afedf-158">FS, F</span><span class="sxs-lookup"><span data-stu-id="afedf-158">Fs, F</span></span>             | <span data-ttu-id="afedf-159">Hoog CPU-naar-geheugen.</span><span class="sxs-lookup"><span data-stu-id="afedf-159">High CPU-to-memory.</span></span> <span data-ttu-id="afedf-160">Goede voor gemiddeld verkeer toepassingen, netwerkapparatuur en batchprocessen.</span><span class="sxs-lookup"><span data-stu-id="afedf-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="afedf-161">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="afedf-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="afedf-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="afedf-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="afedf-163">Hoge geheugen-naar-core.</span><span class="sxs-lookup"><span data-stu-id="afedf-163">High memory-to-core.</span></span> <span data-ttu-id="afedf-164">Ideaal voor relationele databases, gemiddeld toolarge caches en in het geheugen analytics.</span><span class="sxs-lookup"><span data-stu-id="afedf-164">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="afedf-165">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="afedf-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="afedf-166">Ls</span><span class="sxs-lookup"><span data-stu-id="afedf-166">Ls</span></span>                | <span data-ttu-id="afedf-167">Snelle doorvoer van schijfgegevens en IO.</span><span class="sxs-lookup"><span data-stu-id="afedf-167">High disk throughput and IO.</span></span> <span data-ttu-id="afedf-168">Ideaal voor big data-, SQL- en NoSQL-databases.</span><span class="sxs-lookup"><span data-stu-id="afedf-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="afedf-169">GPU</span><span class="sxs-lookup"><span data-stu-id="afedf-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="afedf-170">NV, NC</span><span class="sxs-lookup"><span data-stu-id="afedf-170">NV, NC</span></span>            | <span data-ttu-id="afedf-171">Gespecialiseerde VMs gericht voor zware grafische weergave en het bewerken van video's.</span><span class="sxs-lookup"><span data-stu-id="afedf-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="afedf-172">Hoge prestaties</span><span class="sxs-lookup"><span data-stu-id="afedf-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="afedf-173">H, A8 11</span><span class="sxs-lookup"><span data-stu-id="afedf-173">H, A8-11</span></span>          | <span data-ttu-id="afedf-174">De krachtigste CPU VMs met optionele hoge gegevensdoorvoer netwerkinterfaces (RDMA).</span><span class="sxs-lookup"><span data-stu-id="afedf-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="afedf-175">Zoeken naar beschikbare VM-grootten</span><span class="sxs-lookup"><span data-stu-id="afedf-175">Find available VM sizes</span></span>

<span data-ttu-id="afedf-176">een lijst met VM toosee groottes beschikbaar in een bepaalde regio, gebruikt u Hallo [az vm-lijst-groottes](/cli/azure/vm#list-sizes) opdracht.</span><span class="sxs-lookup"><span data-stu-id="afedf-176">toosee a list of VM sizes available in a particular region, use hello [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="afedf-177">Gedeeltelijke uitvoer:</span><span class="sxs-lookup"><span data-stu-id="afedf-177">Partial output:</span></span>

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="afedf-178">Virtuele machine maken met een specifieke grootte</span><span class="sxs-lookup"><span data-stu-id="afedf-178">Create VM with specific size</span></span>

<span data-ttu-id="afedf-179">In Hallo vorige VM maken bijvoorbeeld is een grootte niet opgegeven, waardoor het een standaardgrootte.</span><span class="sxs-lookup"><span data-stu-id="afedf-179">In hello previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="afedf-180">Een VM-grootte kan worden geselecteerd maken met behulp van tijd [az vm maken](/cli/azure/vm#create) en Hallo `--size` argument.</span><span class="sxs-lookup"><span data-stu-id="afedf-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and hello `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="afedf-181">De grootte van een virtuele machine wijzigen</span><span class="sxs-lookup"><span data-stu-id="afedf-181">Resize a VM</span></span>

<span data-ttu-id="afedf-182">Nadat een virtuele machine is geïmplementeerd, kan het formaat is gewijzigd tooincrease of resourcetoewijzing verlagen.</span><span class="sxs-lookup"><span data-stu-id="afedf-182">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="afedf-183">Voordat het formaat van een virtuele machine, controleren als hello gewenste grootte beschikbaar op Hallo huidige Azure-cluster is.</span><span class="sxs-lookup"><span data-stu-id="afedf-183">Before resizing a VM, check if hello desired size is available on hello current Azure cluster.</span></span> <span data-ttu-id="afedf-184">Hallo [az vm-vm-formaat-opties voor](/cli/azure/vm#list-vm-resize-options) opdracht retourneert de lijst met grootten Hallo.</span><span class="sxs-lookup"><span data-stu-id="afedf-184">hello [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns hello list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="afedf-185">Desgewenst Hallo grootte is beschikbaar kan hello VM worden gewijzigd vanuit een status ingeschakeld op maar deze opnieuw wordt opgestart tijdens het Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="afedf-185">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span> <span data-ttu-id="afedf-186">Gebruik Hallo [az vm vergroten of verkleinen]( /cli/azure/vm#resize) opdracht tooperform Hallo formaat.</span><span class="sxs-lookup"><span data-stu-id="afedf-186">Use hello [az vm resize]( /cli/azure/vm#resize) command tooperform hello resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="afedf-187">Desgewenst Hallo grootte is niet op Hallo huidig cluster Hallo VM behoeften toobe ongedaan voordat Hallo vergroten of verkleinen van de bewerking kan zich voordoen.</span><span class="sxs-lookup"><span data-stu-id="afedf-187">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="afedf-188">Gebruik Hallo [az vm ongedaan]( /cli/azure/vm#deallocate) opdracht toostop en Hallo VM ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="afedf-188">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span> <span data-ttu-id="afedf-189">Let op wanneer hello VM weer is ingeschakeld, worden alle gegevens op de tijdelijke schijf Hallo mogelijk verwijderd.</span><span class="sxs-lookup"><span data-stu-id="afedf-189">Note, when hello VM is powered back on, any data on hello temp disk may be removed.</span></span> <span data-ttu-id="afedf-190">Hallo openbaar IP-adres verandert ook tenzij een statisch IP-adres wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="afedf-190">hello public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="afedf-191">Zodra de toewijzing opgeheven, kan Hallo formaat optreden.</span><span class="sxs-lookup"><span data-stu-id="afedf-191">Once deallocated, hello resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="afedf-192">Nadat het Hallo vergroten of verkleinen, kunnen Hallo VM kan worden gestart.</span><span class="sxs-lookup"><span data-stu-id="afedf-192">After hello resize, hello VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="afedf-193">VM-energiestatus</span><span class="sxs-lookup"><span data-stu-id="afedf-193">VM power states</span></span>

<span data-ttu-id="afedf-194">Een Azure VM kan een van de vele energiestatussen hebben.</span><span class="sxs-lookup"><span data-stu-id="afedf-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="afedf-195">Deze status vertegenwoordigt de huidige status Hallo Hallo VM Hallo verwerkt Hallo hypervisor.</span><span class="sxs-lookup"><span data-stu-id="afedf-195">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="afedf-196">Energiestatus</span><span class="sxs-lookup"><span data-stu-id="afedf-196">Power states</span></span>

| <span data-ttu-id="afedf-197">Energieniveau</span><span class="sxs-lookup"><span data-stu-id="afedf-197">Power State</span></span> | <span data-ttu-id="afedf-198">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="afedf-198">Description</span></span>
|----|----|
| <span data-ttu-id="afedf-199">Starting</span><span class="sxs-lookup"><span data-stu-id="afedf-199">Starting</span></span> | <span data-ttu-id="afedf-200">Hiermee wordt aangegeven op Hallo virtuele machine wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="afedf-200">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="afedf-201">Running</span><span class="sxs-lookup"><span data-stu-id="afedf-201">Running</span></span> | <span data-ttu-id="afedf-202">Hiermee wordt aangegeven dat de Hallo virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="afedf-202">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="afedf-203">Stopping</span><span class="sxs-lookup"><span data-stu-id="afedf-203">Stopping</span></span> | <span data-ttu-id="afedf-204">Hiermee wordt aangegeven dat de virtuele machine hello wordt gestopt.</span><span class="sxs-lookup"><span data-stu-id="afedf-204">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="afedf-205">Stopped</span><span class="sxs-lookup"><span data-stu-id="afedf-205">Stopped</span></span> | <span data-ttu-id="afedf-206">Geeft aan dat de virtuele machine Hallo is gestopt.</span><span class="sxs-lookup"><span data-stu-id="afedf-206">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="afedf-207">Virtuele machines in de status gestopt Hallo nog steeds kosten compute.</span><span class="sxs-lookup"><span data-stu-id="afedf-207">Virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="afedf-208">Toewijzing</span><span class="sxs-lookup"><span data-stu-id="afedf-208">Deallocating</span></span> | <span data-ttu-id="afedf-209">Hiermee wordt aangegeven dat de virtuele machine hello wordt opgeheven.</span><span class="sxs-lookup"><span data-stu-id="afedf-209">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="afedf-210">De toewijzing ongedaan gemaakt</span><span class="sxs-lookup"><span data-stu-id="afedf-210">Deallocated</span></span> | <span data-ttu-id="afedf-211">Hiermee wordt aangegeven dat de virtuele machine Hallo wordt verwijderd uit het Hallo-hypervisor, maar nog steeds beschikbaar in Hallo besturingselement vlak.</span><span class="sxs-lookup"><span data-stu-id="afedf-211">Indicates that hello virtual machine is removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="afedf-212">Virtuele machines in Hallo Deallocated status kan niet worden compute-kosten in rekening.</span><span class="sxs-lookup"><span data-stu-id="afedf-212">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="afedf-213">Geeft aan dat de energiestatus Hallo van Hallo virtuele machine onbekend.</span><span class="sxs-lookup"><span data-stu-id="afedf-213">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="afedf-214">Energieniveau vinden</span><span class="sxs-lookup"><span data-stu-id="afedf-214">Find power state</span></span>

<span data-ttu-id="afedf-215">tooretrieve hello status van een bepaalde virtuele machine, gebruik Hallo [az vm-instantieweergave ophalen](/cli/azure/vm#get-instance-view) opdracht.</span><span class="sxs-lookup"><span data-stu-id="afedf-215">tooretrieve hello state of a particular VM, use hello [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="afedf-216">Niet zeker toospecify een geldige naam voor een virtuele machine en de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="afedf-216">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="afedf-217">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="afedf-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="afedf-218">Beheertaken</span><span class="sxs-lookup"><span data-stu-id="afedf-218">Management tasks</span></span>

<span data-ttu-id="afedf-219">Tijdens het Hallo-levenscyclus van een virtuele machine kunt u beheertaken toorun zoals starten, stoppen of een virtuele machine wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="afedf-219">During hello life-cycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="afedf-220">U kunt bovendien toocreate scripts tooautomate herhalende of complexe taken.</span><span class="sxs-lookup"><span data-stu-id="afedf-220">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="afedf-221">Met behulp van Azure CLI Hallo kunnen veel algemene beheertaken worden uitgevoerd vanaf de opdrachtregel hello, hetzij in scripts.</span><span class="sxs-lookup"><span data-stu-id="afedf-221">Using hello Azure CLI, many common management tasks can be run from hello command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="afedf-222">IP-adres</span><span class="sxs-lookup"><span data-stu-id="afedf-222">Get IP address</span></span>

<span data-ttu-id="afedf-223">Deze opdracht retourneert Hallo persoonlijke en openbare IP-adressen van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="afedf-223">This command returns hello private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="afedf-224">Virtuele machine stoppen</span><span class="sxs-lookup"><span data-stu-id="afedf-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="afedf-225">Virtuele machine starten</span><span class="sxs-lookup"><span data-stu-id="afedf-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="afedf-226">Verwijderen van resourcegroep</span><span class="sxs-lookup"><span data-stu-id="afedf-226">Delete resource group</span></span>

<span data-ttu-id="afedf-227">Verwijderen van een resourcegroep, worden ook alle resources binnen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="afedf-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="afedf-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="afedf-228">Next steps</span></span>

<span data-ttu-id="afedf-229">In deze zelfstudie hebt u geleerd over basic VM maken en beheren zoals het:</span><span class="sxs-lookup"><span data-stu-id="afedf-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="afedf-230">Maken en koppelen tooa VM</span><span class="sxs-lookup"><span data-stu-id="afedf-230">Create and connect tooa VM</span></span>
> * <span data-ttu-id="afedf-231">Selecteer en gebruik van VM-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="afedf-231">Select and use VM images</span></span>
> * <span data-ttu-id="afedf-232">Weergeven en gebruiken van specifieke VM-grootten</span><span class="sxs-lookup"><span data-stu-id="afedf-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="afedf-233">De grootte van een virtuele machine wijzigen</span><span class="sxs-lookup"><span data-stu-id="afedf-233">Resize a VM</span></span>
> * <span data-ttu-id="afedf-234">Bekijken en te begrijpen status virtuele machine</span><span class="sxs-lookup"><span data-stu-id="afedf-234">View and understand VM state</span></span>

<span data-ttu-id="afedf-235">Ga toohello volgende zelfstudie toolearn over VM-schijven.</span><span class="sxs-lookup"><span data-stu-id="afedf-235">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="afedf-236">Maken en beheren van VM-schijven</span><span class="sxs-lookup"><span data-stu-id="afedf-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
