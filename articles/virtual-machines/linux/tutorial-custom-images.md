---
title: "Maken van aangepaste installatiekopieën voor virtuele machine met de Azure CLI | Microsoft Docs"
description: Zelfstudie - maken van een aangepaste VM-installatiekopie met de Azure CLI.
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
ms.openlocfilehash: d32980f05ad17a76793021d0a5355d597974a4e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-the-cli"></a><span data-ttu-id="f85e0-103">Een aangepaste installatiekopie van een virtuele machine met behulp van de CLI van Azure maken</span><span class="sxs-lookup"><span data-stu-id="f85e0-103">Create a custom image of an Azure VM using the CLI</span></span>

<span data-ttu-id="f85e0-104">Aangepaste installatiekopieën zijn zoals marketplace-installatiekopieën, maar u deze zelf maken.</span><span class="sxs-lookup"><span data-stu-id="f85e0-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="f85e0-105">Aangepaste installatiekopieën kunnen worden gebruikt voor de bootstrap configuraties, zoals het vooraf laden van toepassingen, toepassingsconfiguraties en andere configuraties OS.</span><span class="sxs-lookup"><span data-stu-id="f85e0-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="f85e0-106">In deze zelfstudie maakt u uw eigen aangepaste installatiekopie van een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="f85e0-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="f85e0-107">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="f85e0-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f85e0-108">Inrichting ervan ongedaan en generalize van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="f85e0-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="f85e0-109">Een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f85e0-109">Create a custom image</span></span>
> * <span data-ttu-id="f85e0-110">Een virtuele machine van een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f85e0-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="f85e0-111">Lijst van alle installatiekopieën in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="f85e0-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="f85e0-112">Een afbeelding verwijderen</span><span class="sxs-lookup"><span data-stu-id="f85e0-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f85e0-113">Als u wilt installeren en gebruiken van de CLI lokaal, in deze zelfstudie vereist dat u de Azure CLI versie 2.0.4 zijn uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="f85e0-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f85e0-114">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="f85e0-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="f85e0-115">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f85e0-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="f85e0-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f85e0-116">Before you begin</span></span>

<span data-ttu-id="f85e0-117">De onderstaande stappen worden in detail beschreven hoe moet worden overgenomen van een bestaande virtuele machine en schakelt u deze in een herbruikbare aangepaste installatiekopie die u gebruiken kunt om nieuwe VM-exemplaren te maken.</span><span class="sxs-lookup"><span data-stu-id="f85e0-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="f85e0-118">Als u het voorbeeld in deze zelfstudie, moet u een bestaande virtuele machine hebben.</span><span class="sxs-lookup"><span data-stu-id="f85e0-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="f85e0-119">Indien nodig, dit [voorbeeldscript](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) kunt maken voor u.</span><span class="sxs-lookup"><span data-stu-id="f85e0-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="f85e0-120">Wanneer het uitvoeren van de zelfstudie vervangt benoemt de resourcegroep en de virtuele machine waar nodig.</span><span class="sxs-lookup"><span data-stu-id="f85e0-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="f85e0-121">Een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f85e0-121">Create a custom image</span></span>

<span data-ttu-id="f85e0-122">Voor het maken van een installatiekopie van een virtuele machine, moet u de virtuele machine voorbereiden door opheffen van inrichting, toewijzing en vervolgens de bron-VM als gegeneraliseerd markeren.</span><span class="sxs-lookup"><span data-stu-id="f85e0-122">To create an image of a virtual machine, you need to prepare the VM by deprovisioning, deallocating, and then marking the source VM as generalized.</span></span> <span data-ttu-id="f85e0-123">Zodra de VM is voorbereid, kunt u een installatiekopie maken.</span><span class="sxs-lookup"><span data-stu-id="f85e0-123">Once the VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-the-vm"></a><span data-ttu-id="f85e0-124">De virtuele machine identiteitsgegevens</span><span class="sxs-lookup"><span data-stu-id="f85e0-124">Deprovision the VM</span></span> 

<span data-ttu-id="f85e0-125">Opheffen van inrichting de virtuele machine generaliseert door machine-specifieke informatie te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f85e0-125">Deprovisioning generalizes the VM by removing machine-specific information.</span></span> <span data-ttu-id="f85e0-126">Deze generaliseren maakt het mogelijk om te veel virtuele machines van één installatiekopie implementeren.</span><span class="sxs-lookup"><span data-stu-id="f85e0-126">This generalization makes it possible to deploy many VMs from a single image.</span></span> <span data-ttu-id="f85e0-127">Tijdens het opheffen van inrichting, de naam van de host opnieuw is ingesteld op *localhost.localdomain*.</span><span class="sxs-lookup"><span data-stu-id="f85e0-127">During deprovisioning, the host name is reset to *localhost.localdomain*.</span></span> <span data-ttu-id="f85e0-128">Host-SSH-sleutels, naamserver configuraties hoofdwachtwoord en in de cache DHCP-leases worden ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f85e0-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="f85e0-129">Voor de inrichting ervan ongedaan maakt de virtuele machine, gebruikt u de Azure VM-agent (waagent).</span><span class="sxs-lookup"><span data-stu-id="f85e0-129">To deprovision the VM, use the Azure VM agent (waagent).</span></span> <span data-ttu-id="f85e0-130">De Azure VM-agent is geïnstalleerd op de virtuele machine en inrichting en interactie met de Azure-Infrastructuurcontroller beheert.</span><span class="sxs-lookup"><span data-stu-id="f85e0-130">The Azure VM agent is installed on the VM and manages provisioning and interacting with the Azure Fabric Controller.</span></span> <span data-ttu-id="f85e0-131">Zie voor meer informatie de [gebruikershandleiding voor Azure Linux Agent](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="f85e0-131">For more information, see the [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="f85e0-132">Verbinding maken met uw virtuele machine via SSH en voer de opdracht voor de inrichting ervan ongedaan maakt de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f85e0-132">Connect to your VM using SSH and run the command to deprovision the VM.</span></span> <span data-ttu-id="f85e0-133">Met de `+user` argument, de laatste ingerichte gebruiker-account en alle bijbehorende gegevens worden ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f85e0-133">With the `+user` argument, the last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="f85e0-134">De voorbeeld-IP-adres vervangen door het openbare IP-adres van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f85e0-134">Replace the example IP address with the public IP address of your VM.</span></span>

<span data-ttu-id="f85e0-135">SSH naar de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f85e0-135">SSH to the VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="f85e0-136">Inrichting ervan ongedaan maakt de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f85e0-136">Deprovision the VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="f85e0-137">De SSH-sessie te sluiten.</span><span class="sxs-lookup"><span data-stu-id="f85e0-137">Close the SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="f85e0-138">Toewijzing ongedaan maken en de virtuele machine niet markeren als gegeneraliseerd</span><span class="sxs-lookup"><span data-stu-id="f85e0-138">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="f85e0-139">Voor het maken van een installatiekopie, moet de VM ongedaan.</span><span class="sxs-lookup"><span data-stu-id="f85e0-139">To create an image, the VM needs to be deallocated.</span></span> <span data-ttu-id="f85e0-140">Het gebruik van de VM ongedaan [az vm ongedaan](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="f85e0-140">Deallocate the VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f85e0-141">Tot slot stelt de status van de virtuele machine als gegeneraliseerd met [az vm generalize](/cli//azure/vm#generalize) zodat de Azure-platform weet de VM is gegeneraliseerd.</span><span class="sxs-lookup"><span data-stu-id="f85e0-141">Finally, set the state of the VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so the Azure platform knows the VM has been generalized.</span></span> <span data-ttu-id="f85e0-142">U kunt alleen een installatiekopie van het maken van een gegeneraliseerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f85e0-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-the-image"></a><span data-ttu-id="f85e0-143">De installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f85e0-143">Create the image</span></span>

<span data-ttu-id="f85e0-144">Nu u een installatiekopie van de virtuele machine maken met behulp van kunt [az installatiekopie maken](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="f85e0-144">Now you can create an image of the VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="f85e0-145">Het volgende voorbeeld wordt een installatiekopie met de naam *myImage* van een virtuele machine met de naam *myVM*.</span><span class="sxs-lookup"><span data-stu-id="f85e0-145">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="f85e0-146">Virtuele machines van de installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f85e0-146">Create VMs from the image</span></span>

<span data-ttu-id="f85e0-147">Nu dat u een installatiekopie hebt, kunt u een of meer nieuwe virtuele machines van de installatiekopie met behulp [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f85e0-147">Now that you have an image, you can create one or more new VMs from the image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="f85e0-148">Het volgende voorbeeld wordt een virtuele machine met de naam *myVMfromImage* van de installatiekopie met de naam *myImage*.</span><span class="sxs-lookup"><span data-stu-id="f85e0-148">The following example creates a VM named *myVMfromImage* from the image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="f85e0-149">Beheer van installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="f85e0-149">Image management</span></span> 

<span data-ttu-id="f85e0-150">Hier volgen enkele voorbeelden van algemene beheertaken voor de installatiekopie en hoe ze met de Azure CLI te voltooien.</span><span class="sxs-lookup"><span data-stu-id="f85e0-150">Here are some examples of common image management tasks and how to complete them using the Azure CLI.</span></span>

<span data-ttu-id="f85e0-151">Lijst van alle installatiekopieën met de naam in een tabel.</span><span class="sxs-lookup"><span data-stu-id="f85e0-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="f85e0-152">Een afbeelding verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f85e0-152">Delete an image.</span></span> <span data-ttu-id="f85e0-153">Dit voorbeeld wordt verwijderd van de installatiekopie met de naam *myOldImage* van de *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="f85e0-153">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f85e0-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f85e0-154">Next steps</span></span>

<span data-ttu-id="f85e0-155">In deze zelfstudie maakt u een aangepaste installatiekopie van de virtuele machine gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f85e0-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="f85e0-156">U leert hoe naar:</span><span class="sxs-lookup"><span data-stu-id="f85e0-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f85e0-157">Inrichting ervan ongedaan en generalize van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="f85e0-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="f85e0-158">Een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f85e0-158">Create a custom image</span></span>
> * <span data-ttu-id="f85e0-159">Een virtuele machine van een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f85e0-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="f85e0-160">Lijst van alle installatiekopieën in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="f85e0-160">List all the images in your subscription</span></span>
> * <span data-ttu-id="f85e0-161">Een afbeelding verwijderen</span><span class="sxs-lookup"><span data-stu-id="f85e0-161">Delete an image</span></span>

<span data-ttu-id="f85e0-162">Ga naar de volgende zelfstudie voor meer informatie over de maximaal beschikbare virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f85e0-162">Advance to the next tutorial to learn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="f85e0-163">[Maximaal beschikbare virtuele machines maken](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="f85e0-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

