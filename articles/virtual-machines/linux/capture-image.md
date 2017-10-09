---
title: een installatiekopie van een Linux-VM in Azure met CLI 2.0 aaaCapture | Microsoft Docs
description: Een installatiekopie van een virtuele machine van Azure toouse voor grootschalige implementaties met hello Azure CLI 2.0.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="7d0a4-103">Hoe toocreate een installatiekopie van een virtuele machine of de VHD</span><span class="sxs-lookup"><span data-stu-id="7d0a4-103">How toocreate an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of hello tutorial-->

<span data-ttu-id="7d0a4-104">toocreate meerdere exemplaren van een virtuele machine (VM) toouse in Azure, een installatiekopie van Hallo VM of Hallo OS VHD.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-104">toocreate multiple copies of a virtual machine (VM) toouse in Azure, capture an image of hello VM or hello OS VHD.</span></span> <span data-ttu-id="7d0a4-105">een installatiekopie van een toocreate, moet u persoonlijke gegevens die het maakt veiliger toodeploy meerdere keren verwijderen.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-105">toocreate an image, you need remove personal account information which makes it safer toodeploy multiple times.</span></span> <span data-ttu-id="7d0a4-106">Toewijzing in Hallo volgende stappen uit die u een bestaande VM inrichting ervan ongedaan, en een installatiekopie maken.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-106">In hello following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="7d0a4-107">U kunt deze installatiekopie toocreate VM's op elke willekeurige resourcegroep gebruiken in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-107">You can use this image toocreate VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="7d0a4-108">Als u een kopie van uw bestaande Linux VM toocreate voor back-up of foutopsporing wilt of een gespecialiseerde Linux VHD van een lokale virtuele machine uploaden, Zie [uploaden en Linux-VM te maken van aangepaste schijfimage](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="7d0a4-108">If you want toocreate a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="7d0a4-109">U kunt ook **verpakker** toocreate uw aangepaste configuratie.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-109">You can also use **Packer** toocreate your custom configuration.</span></span> <span data-ttu-id="7d0a4-110">Zie voor meer informatie over het gebruik van verpakker [hoe toouse verpakker toocreate virtuele Linux-machine in Azure afbeeldingen](build-image-with-packer.md).</span><span class="sxs-lookup"><span data-stu-id="7d0a4-110">For more information on using Packer, see [How toouse Packer toocreate Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="7d0a4-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="7d0a4-111">Before you begin</span></span>
<span data-ttu-id="7d0a4-112">Zorg ervoor dat u voldoet aan de Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="7d0a4-112">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="7d0a4-113">U moet een Azure VM gemaakt in Hallo Resource Manager-implementatiemodel met beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-113">You need an Azure VM created in hello Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="7d0a4-114">Als u een Linux-VM nog niet hebt gemaakt, kunt u Hallo [portal](quick-create-portal.md), Hallo [Azure CLI](quick-create-cli.md), of [Resource Manager-sjablonen](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="7d0a4-114">If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="7d0a4-115">Configureer Hallo VM indien nodig.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-115">Configure hello VM as needed.</span></span> <span data-ttu-id="7d0a4-116">Bijvoorbeeld: [gegevensschijven toevoegen](add-disk.md), toepassen van updates en toepassingen te installeren.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="7d0a4-117">U moet ook toohave Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en worden vastgelegd in het Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="7d0a4-117">You also need toohave hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="7d0a4-118">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="7d0a4-118">Quick commands</span></span>

<span data-ttu-id="7d0a4-119">Zie voor een vereenvoudigde versie van dit onderwerp voor het testen, evalueren of leren over virtuele machines in Azure, [maken van een aangepaste installatiekopie van een virtuele machine van Azure CLI Hallo met](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="7d0a4-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-hello-vm"></a><span data-ttu-id="7d0a4-120">Stap 1: Deprovision Hallo VM</span><span class="sxs-lookup"><span data-stu-id="7d0a4-120">Step 1: Deprovision hello VM</span></span>
<span data-ttu-id="7d0a4-121">U inrichting ervan ongedaan Hallo VM, met hello Azure VM-agent, toodelete machine specifieke bestanden en gegevens.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-121">You deprovision hello VM, using hello Azure VM agent, toodelete machine specific files and data.</span></span> <span data-ttu-id="7d0a4-122">Gebruik Hallo `waagent` opdracht Hello *-deprovision + user* parameter bij de bron-Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-122">Use hello `waagent` command with hello *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="7d0a4-123">Zie voor meer informatie, Hallo [gebruikershandleiding voor Azure Linux Agent](../windows/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="7d0a4-123">For more information, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="7d0a4-124">Verbinding maken met behulp van een SSH-client voor Linux-VM tooyour.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-124">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="7d0a4-125">Typ in Hallo SSH venster Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7d0a4-125">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="7d0a4-126">Alleen worden uitgevoerd met deze opdracht op een virtuele machine die u van plan toocapture als afbeelding bent.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-126">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="7d0a4-127">Het is geen die installatiekopie Hallo van alle gevoelige informatie is uitgeschakeld of geschikt is voor de herdistributie van garantie.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-127">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="7d0a4-128">Hallo *+ user* parameter Hallo laatste ingerichte gebruikersaccount, worden ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-128">hello *+user* parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="7d0a4-129">Desgewenst kunt u de accountreferenties tookeep in Hallo VM gebruiken *-deprovision* tooleave Hallo-gebruikersaccount in plaats.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-129">If you want tookeep account credentials in hello VM, just use *-deprovision* tooleave hello user account in place.</span></span>
 
3. <span data-ttu-id="7d0a4-130">Type **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-130">Type **y** toocontinue.</span></span> <span data-ttu-id="7d0a4-131">U kunt Hallo toevoegen **-afdwingen** parameter tooavoid deze bevestigingsstap.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-131">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="7d0a4-132">Nadat het Hallo-opdracht is voltooid, typt u **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-132">After hello command completes, type **exit**.</span></span> <span data-ttu-id="7d0a4-133">Deze stap wordt gesloten Hallo SSH-client.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-133">This step closes hello SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="7d0a4-134">Stap 2: Maak een VM-installatiekopie</span><span class="sxs-lookup"><span data-stu-id="7d0a4-134">Step 2: Create VM image</span></span>
<span data-ttu-id="7d0a4-135">Hello Azure CLI 2.0 toomark Hallo VM gebruiken zoals gegeneraliseerd en Hallo installatiekopie vastleggen.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-135">Use hello Azure CLI 2.0 toomark hello VM as generalized and capture hello image.</span></span> <span data-ttu-id="7d0a4-136">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-136">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="7d0a4-137">De namen van de voorbeeld-parameter *myResourceGroup*, *myVnet*, en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="7d0a4-138">Toewijzing van Hallo VM die u gemaakt met [az vm ongedaan](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="7d0a4-138">Deallocate hello VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="7d0a4-139">Hallo volgende voorbeeld deallocates Hallo VM met de naam *myVM* in Hallo resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="7d0a4-139">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="7d0a4-140">Markeren Hallo VM zoals gegeneraliseerd met [az vm generalize](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="7d0a4-140">Mark hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="7d0a4-141">Hallo na voorbeeld aanhalingstekens Hallo Hallo VM met de naam *myVM* in Hallo resourcegroep met de naam *myResourceGroup* zoals gegeneraliseerd:</span><span class="sxs-lookup"><span data-stu-id="7d0a4-141">hello following example marks hello hello VM named *myVM* in hello resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="7d0a4-142">Maak nu een afbeelding van Hallo VM-resource met [az installatiekopie maken](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="7d0a4-142">Now create an image of hello VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="7d0a4-143">Hallo volgende voorbeeld wordt een installatiekopie met de naam *myImage* in Hallo resourcegroep met de naam *myResourceGroup* Hallo VM-resource met de naam met *myVM*:</span><span class="sxs-lookup"><span data-stu-id="7d0a4-143">hello following example creates an image named *myImage* in hello resource group named *myResourceGroup* using hello VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="7d0a4-144">Hallo installatiekopie is gemaakt in Hallo dezelfde resourcegroep bevindt als de bron-VM.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-144">hello image is created in hello same resource group as your source VM.</span></span> <span data-ttu-id="7d0a4-145">U kunt virtuele machines in elke willekeurige resourcegroep maken in uw abonnement vanuit deze installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="7d0a4-146">Vanuit het perspectief van een management, kunt u desgewenst toocreate een specifieke resourcegroep voor uw VM netwerkbronnen en afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-146">From a management perspective, you may wish toocreate a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="7d0a4-147">Stap 3: Een virtuele machine maken vanuit Hallo vastgelegde installatiekopie</span><span class="sxs-lookup"><span data-stu-id="7d0a4-147">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="7d0a4-148">Een virtuele machine maken met Hallo-installatiekopie die u hebt gemaakt met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="7d0a4-148">Create a VM using hello image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="7d0a4-149">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVMDeployed* uit Hallo installatiekopie met de naam *myImage*:</span><span class="sxs-lookup"><span data-stu-id="7d0a4-149">hello following example creates a VM named *myVMDeployed* from hello image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a><span data-ttu-id="7d0a4-150">Hallo VM maken in een andere resourcegroep</span><span class="sxs-lookup"><span data-stu-id="7d0a4-150">Creating hello VM in another resource group</span></span> 

<span data-ttu-id="7d0a4-151">U kunt virtuele machines maken van een installatiekopie in elke willekeurige resourcegroep binnen uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="7d0a4-152">een virtuele machine in een andere resourcegroep dan Hallo-installatiekopie toocreate Hallo volledige resource-ID tooyour afbeelding opgeven.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-152">toocreate a VM in a different resource group than hello image, specify hello full resource ID tooyour image.</span></span> <span data-ttu-id="7d0a4-153">Gebruik [az afbeeldingenlijst](/cli/azure/image#list) tooview een lijst met afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-153">Use [az image list](/cli/azure/image#list) tooview a list of images.</span></span> <span data-ttu-id="7d0a4-154">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7d0a4-154">hello output is similar toohello following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="7d0a4-155">Hallo volgende voorbeeld wordt [az vm maken](/cli/azure/vm#create) toocreate een virtuele machine in een andere resourcegroep dan de broninstallatiekopie Hallo door te geven Hallo Afbeeldingsbron-ID:</span><span class="sxs-lookup"><span data-stu-id="7d0a4-155">hello following example uses [az vm create](/cli/azure/vm#create) toocreate a VM in a different resource group than hello source image by specifying hello image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a><span data-ttu-id="7d0a4-156">Stap 4: Hallo implementatie controleren</span><span class="sxs-lookup"><span data-stu-id="7d0a4-156">Step 4: Verify hello deployment</span></span>

<span data-ttu-id="7d0a4-157">Nu SSH toohello virtuele machine u tooverify Hallo implementatie en begin met behulp van gemaakt Hallo nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-157">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="7d0a4-158">tooconnect via SSH, vinden Hallo IP-adres of FQDN-naam van uw virtuele machine met [az vm weergeven](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="7d0a4-158">tooconnect via SSH, find hello IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="7d0a4-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7d0a4-159">Next steps</span></span>
<span data-ttu-id="7d0a4-160">U kunt meerdere virtuele machines maken van de bron-VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="7d0a4-161">Als u toomake wijzigingen tooyour installatiekopie moet:</span><span class="sxs-lookup"><span data-stu-id="7d0a4-161">If you need toomake changes tooyour image:</span></span> 

- <span data-ttu-id="7d0a4-162">Een virtuele machine maken van uw installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-162">Create a VM from your image.</span></span>
- <span data-ttu-id="7d0a4-163">Controleer op updates of wijzigingen in de configuratie.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="7d0a4-164">Ga als volgt Hallo stappen opnieuw toodeprovision, toewijzing generaliseren en een installatiekopie maken.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-164">Follow hello steps again toodeprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="7d0a4-165">Deze nieuwe installatiekopie gebruiken voor toekomstige implementaties.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-165">Use this new image for future deployments.</span></span> <span data-ttu-id="7d0a4-166">Indien gewenst, verwijder Hallo originele installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="7d0a4-166">If desired, delete hello original image.</span></span>

<span data-ttu-id="7d0a4-167">Zie voor meer informatie over het beheren van uw virtuele machines met Hallo CLI [Azure CLI 2.0](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7d0a4-167">For more information on managing your VMs with hello CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
