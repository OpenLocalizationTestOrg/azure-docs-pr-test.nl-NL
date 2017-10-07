---
title: een installatiekopie van een Linux-VM aaaCapture | Microsoft Docs
description: Meer informatie over hoe toocapture een installatiekopie van een Linux-gebaseerde Azure virtuele machine (VM) gemaakt met het klassieke implementatiemodel Hallo.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="6bf1f-103">Hoe toocapture klassieke virtuele Linux-machine als afbeelding</span><span class="sxs-lookup"><span data-stu-id="6bf1f-103">How toocapture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6bf1f-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6bf1f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6bf1f-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="6bf1f-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="6bf1f-107">Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6bf1f-107">Learn how too[perform these steps using hello Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6bf1f-108">Dit artikel ziet u hoe toocapture een klassieke Azure virtuele machine (VM) met Linux als een installatiekopie toocreate andere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-108">This article shows you how toocapture a classic Azure virtual machine (VM) running Linux as an image toocreate other virtual machines.</span></span> <span data-ttu-id="6bf1f-109">Deze installatiekopie bevat Hallo besturingssysteemschijf en gegevensschijven toohello VM gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-109">This image includes hello OS disk and data disks attached toohello VM.</span></span> <span data-ttu-id="6bf1f-110">Zijn niet opgenomen netwerkconfiguratie, dus u tooconfigure moet die bij het maken van Hallo andere virtuele machine uit Hallo-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-110">It doesn't include networking configuration, so you need tooconfigure that when you create hello other VM from hello image.</span></span>

<span data-ttu-id="6bf1f-111">Azure winkels Hallo afbeelding onder **installatiekopieën**, samen met alle installatiekopieën die u hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-111">Azure stores hello image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="6bf1f-112">Zie voor meer informatie over installatiekopieën [over installatiekopieën van virtuele machines in Azure][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="6bf1f-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6bf1f-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="6bf1f-113">Before you begin</span></span>
<span data-ttu-id="6bf1f-114">Deze stappen wordt ervan uitgegaan dat u een virtuele machine in Azure met behulp van Hallo klassieke implementatiemodel en geconfigureerde Hallo-besturingssysteem, met inbegrip van eventuele gegevensschijven koppelen al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-114">These steps assume that you've already created an Azure VM using hello Classic deployment model and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="6bf1f-115">Als u een virtuele machine toocreate nodig hebt, leest u [hoe tooCreate virtuele Linux-Machine][How tooCreate a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="6bf1f-115">If you need toocreate a VM, read [How tooCreate a Linux Virtual Machine][How tooCreate a Linux Virtual Machine].</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="6bf1f-116">Hallo-machine vastleggen</span><span class="sxs-lookup"><span data-stu-id="6bf1f-116">Capture hello virtual machine</span></span>
1. <span data-ttu-id="6bf1f-117">[Verbinding maken met toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) met behulp van een SSH-client van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-117">[Connect toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="6bf1f-118">Typ in Hallo SSH venster Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-118">In hello SSH window, type hello following command.</span></span> <span data-ttu-id="6bf1f-119">Hallo de uitvoer van `waagent` enigszins kunnen variëren afhankelijk van Hallo-versie van dit hulpprogramma:</span><span class="sxs-lookup"><span data-stu-id="6bf1f-119">hello output from `waagent` may vary slightly depending on hello version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="6bf1f-120">Hallo voorgaande opdracht tooclean Hallo systeem probeert, waardoor het geschikt is voor reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-120">hello preceding command attempts tooclean hello system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="6bf1f-121">Deze bewerking uitvoert Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="6bf1f-121">This operation performs hello following tasks:</span></span>

   * <span data-ttu-id="6bf1f-122">Hiermee verwijdert u SSH-sleutels voor host (als Provisioning.RegenerateSshHostKeyPair 'y' in het configuratiebestand Hallo)</span><span class="sxs-lookup"><span data-stu-id="6bf1f-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="6bf1f-123">Hiermee wist u de configuratie van de naamserver in /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="6bf1f-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="6bf1f-124">Hiermee verwijdert u Hallo `root` gebruikerswachtwoord uit/etc/shadow (als Provisioning.DeleteRootPassword 'y' in het configuratiebestand Hallo)</span><span class="sxs-lookup"><span data-stu-id="6bf1f-124">Removes hello `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="6bf1f-125">Verwijdering van DHCP-clientlease uit de cache</span><span class="sxs-lookup"><span data-stu-id="6bf1f-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="6bf1f-126">Opnieuw instellen van hosten naam toolocalhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="6bf1f-126">Resets host name toolocalhost.localdomain</span></span>
   * <span data-ttu-id="6bf1f-127">Hallo laatste ingerichte gebruikersaccount (verkregen uit /var/lib/waagent) verwijdert **en bijbehorende gegevens**.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-127">Deletes hello last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6bf1f-128">Opheffen van inrichting verwijdert u bestanden en gegevens te 'generaliseer' hello installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-128">Deprovisioning deletes files and data too"generalize" hello image.</span></span> <span data-ttu-id="6bf1f-129">Met deze opdracht op een virtuele machine die u van plan toocapture als een nieuwe sjabloon voor de installatiekopie bent alleen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-129">Only run this command on a VM that you intend toocapture as a new image template.</span></span> <span data-ttu-id="6bf1f-130">Er is geen garantie die installatiekopie Hallo van alle gevoelige informatie is uitgeschakeld of geschikt is voor de herdistributie toothird partijen.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-130">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution toothird parties.</span></span>

3. <span data-ttu-id="6bf1f-131">Type **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-131">Type **y** toocontinue.</span></span> <span data-ttu-id="6bf1f-132">U kunt toevoegen Hallo `-force` parameter tooavoid deze bevestigingsstap.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-132">You can add hello `-force` parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="6bf1f-133">Type **afsluiten** tooclose Hallo SSH-client.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-133">Type **Exit** tooclose hello SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6bf1f-134">Hallo resterende stappen wordt ervan uitgegaan dat u al hebt [geïnstalleerd hello Azure CLI](../../../cli-install-nodejs.md) op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-134">hello remaining steps assume you have already [installed hello Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="6bf1f-135">Alle Hallo stappen te volgen kan ook worden uitgevoerd in Hallo [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6bf1f-135">All hello following steps can also be done in hello [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="6bf1f-136">Open Azure CLI en aanmelding tooyour Azure-abonnement op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-136">From your client computer, open Azure CLI and login tooyour Azure subscription.</span></span> <span data-ttu-id="6bf1f-137">Voor meer informatie lezen [tooan Azure-abonnement verbinden van hello Azure CLI](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6bf1f-137">For details, read [Connect tooan Azure subscription from hello Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="6bf1f-138">Aanmelden in hello Azure-portal, toohello-portal.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-138">In hello Azure portal, log in toohello portal.</span></span>

6. <span data-ttu-id="6bf1f-139">Zorg ervoor dat u in Service Management-modus:</span><span class="sxs-lookup"><span data-stu-id="6bf1f-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="6bf1f-140">Schakel Hallo VM die is al gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-140">Shut down hello VM that is already deprovisioned.</span></span> <span data-ttu-id="6bf1f-141">Hallo volgende voorbeeld wordt afgesloten Hallo VM met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="6bf1f-141">hello following example shuts down hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="6bf1f-142">Indien nodig, kunt u een lijst alle Hallo VM's in uw abonnement worden gemaakt met behulp van weergeven`azure vm list`</span><span class="sxs-lookup"><span data-stu-id="6bf1f-142">If needed, you can view a list all hello VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="6bf1f-143">Als u hello Azure-portal, selecteert u Hallo VM en klikt u op **stoppen** de Hallo VM af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-143">If you're using hello Azure portal, select hello VM and click **Stop** to shut down hello VM.</span></span>

8. <span data-ttu-id="6bf1f-144">Wanneer Hallo VM is gestopt, kunt u Hallo installatiekopie vastleggen.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-144">When hello VM is stopped, capture hello image.</span></span> <span data-ttu-id="6bf1f-145">Hallo na voorbeeld opnamen Hallo VM met de naam `myVM` en maakt u een algemene installatiekopie met de naam `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="6bf1f-145">hello following example captures hello VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="6bf1f-146">Hallo `-t` subopdracht verwijderingen Hallo oorspronkelijke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-146">hello `-t` subcommand deletes hello original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6bf1f-147">In hello Azure-portal, kunt u een installatiekopie vastleggen selecteren **installatiekopie** van Hallo hub-menu.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-147">In hello Azure portal, you can capture an image by selecting **Image** from hello hub menu.</span></span> <span data-ttu-id="6bf1f-148">U moet toosupply Hallo volgende informatie voor de installatiekopie van het Hallo: naam, resourcegroep, locatie, het besturingssysteemtype en pad van opslag-blob.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-148">You need toosupply hello following information for hello image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="6bf1f-149">de nieuwe installatiekopie Hallo is nu beschikbaar in de lijst Hallo van installatiekopieën die kunnen worden gebruikt tooconfigure een nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-149">hello new image is now available in hello list of images that can be used tooconfigure any new VM.</span></span> <span data-ttu-id="6bf1f-150">Hallo-opdracht kunt u deze bekijken:</span><span class="sxs-lookup"><span data-stu-id="6bf1f-150">You can view it with hello command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="6bf1f-151">Op Hallo [Azure-portal](http://portal.azure.com), nieuwe Hallo-afbeelding wordt weergegeven in Hallo **VM-installatiekopieën (klassiek)** die behoort toohello **Compute** services.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-151">On hello [Azure portal](http://portal.azure.com), hello new image appears in hello **VM images (classic)** that belongs toohello **Compute** services.</span></span> <span data-ttu-id="6bf1f-152">U hebt toegang tot **VM-installatiekopieën (klassiek)** door te klikken op _meer services_ service Hallo hello Azure onderaan in de lijst en bekijkt hello **Compute** services.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-152">You can access **VM images (classic)** by clicking _More services_ at hello bottom of hello Azure service list, and then looking in hello **Compute** services.</span></span>   

   ![De installatiekopie is geslaagd](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="6bf1f-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6bf1f-154">Next steps</span></span>
<span data-ttu-id="6bf1f-155">Hallo-installatiekopie is gereed toobe gebruikt toocreate virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-155">hello image is ready toobe used toocreate VMs.</span></span> <span data-ttu-id="6bf1f-156">U kunt Azure CLI-opdracht Hallo `azure vm create` en geef Hallo installatiekopie-naam die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-156">You can use hello Azure CLI command `azure vm create` and supply hello image name you created.</span></span> <span data-ttu-id="6bf1f-157">Zie voor meer informatie [Using hello Azure CLI met het klassieke implementatiemodel](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="6bf1f-157">For more information, see [Using hello Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="6bf1f-158">Ook gebruiken Hallo [Azure-portal](http://portal.azure.com) toocreate een aangepaste virtuele machine met behulp van Hallo **installatiekopie** methode en het selecteren van Hallo installatiekopie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bf1f-158">Alternatively, use hello [Azure portal](http://portal.azure.com) toocreate a custom VM by using hello **Image** method and selecting hello image you created.</span></span> <span data-ttu-id="6bf1f-159">Zie voor meer informatie [hoe een aangepaste VM tooCreate][How tooCreate a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="6bf1f-159">For more information, see [How tooCreate a Custom VM][How tooCreate a Custom Virtual Machine].</span></span>

<span data-ttu-id="6bf1f-160">**Zie ook:** [gebruikershandleiding voor Azure Linux-Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="6bf1f-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
