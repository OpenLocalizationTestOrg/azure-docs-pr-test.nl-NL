---
title: "aangepaste VM-installatiekopieën aaaCreate Hello Azure CLI | Microsoft Docs"
description: Zelfstudie - een aangepaste VM-installatiekopie met behulp van Azure CLI Hallo maken.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a><span data-ttu-id="fe519-103">Een aangepaste installatiekopie van een virtuele machine in Azure met behulp van Hallo CLI maken</span><span class="sxs-lookup"><span data-stu-id="fe519-103">Create a custom image of an Azure VM using hello CLI</span></span>

<span data-ttu-id="fe519-104">Aangepaste installatiekopieën zijn zoals marketplace-installatiekopieën, maar u deze zelf maken.</span><span class="sxs-lookup"><span data-stu-id="fe519-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="fe519-105">Aangepaste installatiekopieën kunnen worden gebruikt toobootstrap configuraties zoals vooraf laden van toepassingen, toepassingsconfiguraties en andere configuraties OS.</span><span class="sxs-lookup"><span data-stu-id="fe519-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="fe519-106">In deze zelfstudie maakt u uw eigen aangepaste installatiekopie van een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="fe519-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="fe519-107">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="fe519-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fe519-108">Inrichting ervan ongedaan en generalize van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="fe519-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="fe519-109">Een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="fe519-109">Create a custom image</span></span>
> * <span data-ttu-id="fe519-110">Een virtuele machine van een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="fe519-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="fe519-111">Lijst van alle Hallo-installatiekopieën in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="fe519-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="fe519-112">Een afbeelding verwijderen</span><span class="sxs-lookup"><span data-stu-id="fe519-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fe519-113">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="fe519-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="fe519-114">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="fe519-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fe519-115">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fe519-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="fe519-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="fe519-116">Before you begin</span></span>

<span data-ttu-id="fe519-117">Hallo stappen hieronder wordt beschreven hoe tootake een bestaande virtuele machine en schakel dit in een herbruikbare aangepaste installatiekopie die u hebt de nieuwe VM-instanties toocreate kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fe519-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="fe519-118">toocomplete hello voorbeeld in deze zelfstudie, moet u een bestaande virtuele machine hebben.</span><span class="sxs-lookup"><span data-stu-id="fe519-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="fe519-119">Indien nodig, dit [voorbeeldscript](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) kunt maken voor u.</span><span class="sxs-lookup"><span data-stu-id="fe519-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="fe519-120">Wanneer werkende Hallo-zelfstudie vervangt benoemt Hallo resourcegroep en de VM waar nodig.</span><span class="sxs-lookup"><span data-stu-id="fe519-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="fe519-121">Een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="fe519-121">Create a custom image</span></span>

<span data-ttu-id="fe519-122">toocreate een installatiekopie van een virtuele machine, moet u tooprepare Hallo VM opheffen van inrichting, toewijzing en wordt vervolgens markeren Hallo bron-VM als gegeneraliseerd.</span><span class="sxs-lookup"><span data-stu-id="fe519-122">toocreate an image of a virtual machine, you need tooprepare hello VM by deprovisioning, deallocating, and then marking hello source VM as generalized.</span></span> <span data-ttu-id="fe519-123">Eenmaal Hallo die VM is voorbereid, kunt u een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="fe519-123">Once hello VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-hello-vm"></a><span data-ttu-id="fe519-124">Identiteitsgegevens Hallo VM</span><span class="sxs-lookup"><span data-stu-id="fe519-124">Deprovision hello VM</span></span> 

<span data-ttu-id="fe519-125">Opheffen van inrichting Hallo VM generaliseert door machine-specifieke informatie te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="fe519-125">Deprovisioning generalizes hello VM by removing machine-specific information.</span></span> <span data-ttu-id="fe519-126">Deze generaliseren maakt het mogelijk toodeploy veel virtuele machines van één installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="fe519-126">This generalization makes it possible toodeploy many VMs from a single image.</span></span> <span data-ttu-id="fe519-127">Tijdens het opheffen van inrichting, Hallo hostnaam op te stellen*localhost.localdomain*.</span><span class="sxs-lookup"><span data-stu-id="fe519-127">During deprovisioning, hello host name is reset too*localhost.localdomain*.</span></span> <span data-ttu-id="fe519-128">Host-SSH-sleutels, naamserver configuraties hoofdwachtwoord en in de cache DHCP-leases worden ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fe519-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="fe519-129">toodeprovision hello virtuele machine, gebruik hello Azure VM-agent (waagent).</span><span class="sxs-lookup"><span data-stu-id="fe519-129">toodeprovision hello VM, use hello Azure VM agent (waagent).</span></span> <span data-ttu-id="fe519-130">Hello Azure VM-agent is geïnstalleerd op Hallo VM en inrichting en interactie met hello Azure-Infrastructuurcontroller beheert.</span><span class="sxs-lookup"><span data-stu-id="fe519-130">hello Azure VM agent is installed on hello VM and manages provisioning and interacting with hello Azure Fabric Controller.</span></span> <span data-ttu-id="fe519-131">Zie voor meer informatie, Hallo [gebruikershandleiding voor Azure Linux Agent](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="fe519-131">For more information, see hello [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="fe519-132">Tooyour VM verbinding maken met behulp van SSH en Voer Hallo opdracht toodeprovision Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="fe519-132">Connect tooyour VM using SSH and run hello command toodeprovision hello VM.</span></span> <span data-ttu-id="fe519-133">Hello `+user` argument, Hallo laatste ingerichte gebruikersaccount en alle bijbehorende gegevens worden ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fe519-133">With hello `+user` argument, hello last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="fe519-134">Hallo voorbeeld IP-adres vervangen door Hallo openbare IP-adres van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fe519-134">Replace hello example IP address with hello public IP address of your VM.</span></span>

<span data-ttu-id="fe519-135">SSH toohello VM.</span><span class="sxs-lookup"><span data-stu-id="fe519-135">SSH toohello VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="fe519-136">Identiteitsgegevens hello VM.</span><span class="sxs-lookup"><span data-stu-id="fe519-136">Deprovision hello VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="fe519-137">Hallo SSH-sessie te sluiten.</span><span class="sxs-lookup"><span data-stu-id="fe519-137">Close hello SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="fe519-138">Toewijzing ongedaan maken en Hallo VM zoals gegeneraliseerd markeren</span><span class="sxs-lookup"><span data-stu-id="fe519-138">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="fe519-139">een installatiekopie van een toocreate, Hallo VM moet toobe toewijzing ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fe519-139">toocreate an image, hello VM needs toobe deallocated.</span></span> <span data-ttu-id="fe519-140">Toewijzing virtuele machine met behulp van Hallo [az vm ongedaan](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="fe519-140">Deallocate hello VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fe519-141">Tot slot stelt Hallo status Hallo VM zoals gegeneraliseerd met [az vm generalize](/cli//azure/vm#generalize) zodat hello Azure-platform Hallo VM is gegeneraliseerd.</span><span class="sxs-lookup"><span data-stu-id="fe519-141">Finally, set hello state of hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so hello Azure platform knows hello VM has been generalized.</span></span> <span data-ttu-id="fe519-142">U kunt alleen een installatiekopie van het maken van een gegeneraliseerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fe519-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a><span data-ttu-id="fe519-143">Hallo installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="fe519-143">Create hello image</span></span>

<span data-ttu-id="fe519-144">Nu u een installatiekopie van Hallo VM maken met behulp van kunt [az installatiekopie maken](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="fe519-144">Now you can create an image of hello VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="fe519-145">Hallo volgende voorbeeld wordt een installatiekopie met de naam *myImage* van een virtuele machine met de naam *myVM*.</span><span class="sxs-lookup"><span data-stu-id="fe519-145">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="fe519-146">Virtuele machines uit Hallo installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="fe519-146">Create VMs from hello image</span></span>

<span data-ttu-id="fe519-147">Nu dat u een installatiekopie hebt, kunt u een of meer nieuwe virtuele machines kunt maken van het Hallo-installatiekopie met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fe519-147">Now that you have an image, you can create one or more new VMs from hello image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="fe519-148">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVMfromImage* uit Hallo installatiekopie met de naam *myImage*.</span><span class="sxs-lookup"><span data-stu-id="fe519-148">hello following example creates a VM named *myVMfromImage* from hello image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="fe519-149">Beheer van installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="fe519-149">Image management</span></span> 

<span data-ttu-id="fe519-150">Hier volgen enkele voorbeelden van algemene beheertaken voor de installatiekopie en hoe toocomplete ze met behulp van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fe519-150">Here are some examples of common image management tasks and how toocomplete them using hello Azure CLI.</span></span>

<span data-ttu-id="fe519-151">Lijst van alle installatiekopieën met de naam in een tabel.</span><span class="sxs-lookup"><span data-stu-id="fe519-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="fe519-152">Een afbeelding verwijderen.</span><span class="sxs-lookup"><span data-stu-id="fe519-152">Delete an image.</span></span> <span data-ttu-id="fe519-153">In dit voorbeeld verwijderingen Hallo installatiekopie met de naam *myOldImage* van Hallo *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="fe519-153">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="fe519-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fe519-154">Next steps</span></span>

<span data-ttu-id="fe519-155">In deze zelfstudie maakt u een aangepaste installatiekopie van de virtuele machine gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fe519-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="fe519-156">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="fe519-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fe519-157">Inrichting ervan ongedaan en generalize van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="fe519-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="fe519-158">Een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="fe519-158">Create a custom image</span></span>
> * <span data-ttu-id="fe519-159">Een virtuele machine van een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="fe519-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="fe519-160">Lijst van alle Hallo-installatiekopieën in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="fe519-160">List all hello images in your subscription</span></span>
> * <span data-ttu-id="fe519-161">Een afbeelding verwijderen</span><span class="sxs-lookup"><span data-stu-id="fe519-161">Delete an image</span></span>

<span data-ttu-id="fe519-162">Ga toohello volgende zelfstudie toolearn over maximaal beschikbare virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="fe519-162">Advance toohello next tutorial toolearn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="fe519-163">[Maximaal beschikbare virtuele machines maken](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="fe519-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

