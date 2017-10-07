---
title: een Azure Linux VM toouse als sjabloon aaaCapture | Microsoft Docs
description: Meer informatie over hoe toocapture en een installatiekopie van een Linux-gebaseerde Azure virtuele machine (VM) gemaakt met Azure Resource Manager-implementatiemodel Hallo generalize.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="f7eaa-103">Vastleggen van een virtuele Linux-machine uitgevoerd op Azure</span><span class="sxs-lookup"><span data-stu-id="f7eaa-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="f7eaa-104">Hallo-stappen in dit artikel toogeneralize en vastleggen van uw Azure Linux virtuele machine (VM) in Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-104">Follow hello steps in this article toogeneralize and capture your Azure Linux virtual machine (VM) in hello Resource Manager deployment model.</span></span> <span data-ttu-id="f7eaa-105">Wanneer u generalize Hallo VM, kunt u persoonlijke gegevens te verwijderen en Hallo VM toobe gebruikt als een installatiekopie van het voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-105">When you generalize hello VM, you remove personal account information and prepare hello VM toobe used as an image.</span></span> <span data-ttu-id="f7eaa-106">U vervolgens een installatiekopie van een gegeneraliseerde virtuele harde schijf (VHD) voor Hallo OS VHD's voor bijgesloten gegevensschijven, vastleggen en een [Resource Manager-sjabloon](../../azure-resource-manager/resource-group-overview.md) voor nieuwe VM-implementaties.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-106">You then capture a generalized virtual hard disk (VHD) image for hello OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="f7eaa-107">Dit artikel wordt uitgelegd hoe toocapture een virtuele machine de installatiekopie met de Azure CLI 1.0 Hallo voor een virtuele machine met niet-beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-107">This article details how toocapture a VM image with hello Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="f7eaa-108">U kunt ook [vastleggen van een VM die gebruikmaakt van Azure beheerd schijven Hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7eaa-108">You can also [capture a VM using Azure Managed Disks with hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f7eaa-109">Beheerde schijven worden afgehandeld door hello Azure-platform en hoeven niet alle toostore voorbereidings- of locatie ze.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-109">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="f7eaa-110">Zie [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Overzicht van Azure Managed Disks) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="f7eaa-111">toocreate VM's met behulp van de installatiekopie hello, netwerkbronnen instellen voor elke nieuwe virtuele machine en gebruik Hallo sjabloon (een JavaScript Object Notation of JSON,-bestand) toodeploy op Hallo VHD-installatiekopieën vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-111">toocreate VMs using hello image, set up network resources for each new VM, and use hello template (a JavaScript Object Notation, or JSON, file) toodeploy it from hello captured VHD images.</span></span> <span data-ttu-id="f7eaa-112">Op deze manier kunt u een virtuele machine met de huidige softwareconfiguratie kan vergelijkbare toohello manier als u installatiekopieën gebruiken in Azure Marketplace Hallo repliceren.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-112">In this way, you can replicate a VM with its current software configuration, similar toohello way you use images in hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="f7eaa-113">Als u een kopie van uw bestaande Linux-VM met de speciale status toocreate voor back-up of foutopsporing wilt, Zie [een kopie maken van een virtuele Linux-machine uitgevoerd op Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7eaa-113">If you want toocreate a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f7eaa-114">En als u een VHD van een lokale virtuele machine met Linux tooupload wilt, Zie [uploaden en Linux-VM te maken van aangepaste schijfimage](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7eaa-114">And if you want tooupload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="f7eaa-115">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="f7eaa-115">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="f7eaa-116">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f7eaa-116">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="f7eaa-117">[Azure CLI 1.0](#before-you-begin) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="f7eaa-117">[Azure CLI 1.0](#before-you-begin) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f7eaa-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="f7eaa-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f7eaa-119">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f7eaa-119">Before you begin</span></span>
<span data-ttu-id="f7eaa-120">Zorg ervoor dat u voldoet aan de Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="f7eaa-120">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="f7eaa-121">**Azure virtuele machine gemaakt in de Resource Manager-implementatiemodel Hallo** -als u een Linux-VM nog niet hebt gemaakt, kunt u Hallo [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), Hallo [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), of [Resource Manager sjablonen](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="f7eaa-121">**Azure VM created in hello Resource Manager deployment model** - If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="f7eaa-122">Configureer Hallo VM indien nodig.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-122">Configure hello VM as needed.</span></span> <span data-ttu-id="f7eaa-123">Bijvoorbeeld: [gegevensschijven toevoegen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), toepassen van updates en toepassingen te installeren.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="f7eaa-124">**Azure CLI** -installatie Hallo [Azure CLI](../../cli-install-nodejs.md) op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-124">**Azure CLI** - Install hello [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-hello-azure-linux-agent"></a><span data-ttu-id="f7eaa-125">Stap 1: Hello Azure Linux-agent verwijderen</span><span class="sxs-lookup"><span data-stu-id="f7eaa-125">Step 1: Remove hello Azure Linux agent</span></span>
<span data-ttu-id="f7eaa-126">Voer eerst Hallo **waagent** opdracht Hello **deprovision** parameter op Hallo Linux VM.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-126">First, run hello **waagent** command with hello **deprovision** parameter on hello Linux VM.</span></span> <span data-ttu-id="f7eaa-127">Deze opdracht verwijdert u bestanden en gegevens toomake Hallo VM gereed is voor het generaliseren.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-127">This command deletes files and data toomake hello VM ready for generalizing.</span></span> <span data-ttu-id="f7eaa-128">Zie voor meer informatie, Hallo [gebruikershandleiding voor Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7eaa-128">For details, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="f7eaa-129">Verbinding maken met behulp van een SSH-client voor Linux-VM tooyour.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-129">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="f7eaa-130">Typ in Hallo SSH venster Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f7eaa-130">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="f7eaa-131">Alleen worden uitgevoerd met deze opdracht op een virtuele machine die u van plan toocapture als afbeelding bent.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-131">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="f7eaa-132">Het is geen die installatiekopie Hallo van alle gevoelige informatie is uitgeschakeld of geschikt is voor de herdistributie van garantie.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-132">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="f7eaa-133">Type **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-133">Type **y** toocontinue.</span></span> <span data-ttu-id="f7eaa-134">U kunt Hallo toevoegen **-afdwingen** parameter tooavoid deze bevestigingsstap.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-134">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="f7eaa-135">Nadat het Hallo-opdracht is voltooid, typt u **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-135">After hello command completes, type **exit**.</span></span> <span data-ttu-id="f7eaa-136">Deze stap wordt gesloten Hallo SSH-client.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-136">This step closes hello SSH client.</span></span>

## <a name="step-2-capture-hello-vm"></a><span data-ttu-id="f7eaa-137">Stap 2: Hallo VM vastleggen</span><span class="sxs-lookup"><span data-stu-id="f7eaa-137">Step 2: Capture hello VM</span></span>
<span data-ttu-id="f7eaa-138">Gebruik hello Azure CLI toogeneralize en Hallo VM vastleggen.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-138">Use hello Azure CLI toogeneralize and capture hello VM.</span></span> <span data-ttu-id="f7eaa-139">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-139">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f7eaa-140">De namen van de voorbeeld-parameter **myResourceGroup**, **myVnet**, en **myVM**.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="f7eaa-141">Open in uw lokale computer hello Azure CLI en [aanmelding tooyour Azure-abonnement](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f7eaa-141">From your local computer, open hello Azure CLI and [login tooyour Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="f7eaa-142">Zorg ervoor dat u in de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="f7eaa-143">Virtuele machine die u al gemaakt met behulp van de volgende opdracht Hallo Hallo afsluiten:</span><span class="sxs-lookup"><span data-stu-id="f7eaa-143">Shut down hello VM that you already deprovisioned by using hello following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="f7eaa-144">Generalize Hallo VM Hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f7eaa-144">Generalize hello VM with hello following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="f7eaa-145">Voer nu Hallo **azure vm vastleggen** opdracht, welke opnamen Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-145">Now run hello **azure vm capture** command, which captures hello VM.</span></span> <span data-ttu-id="f7eaa-146">In Hallo voorbeeld te volgen, Hallo installatiekopie van VHD's met vastleggen namen die beginnen met **MyVHDNamePrefix**, en Hallo **-t** optie geeft u een pad toohello sjabloon **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-146">In hello following example, hello image VHDs are captured with names beginning with **MyVHDNamePrefix**, and hello **-t** option specifies a path toohello template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="f7eaa-147">Hallo installatiekopie VHD-bestanden gemaakt in hetzelfde opslagaccount die oorspronkelijke VM Hallo gebruikt Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-147">hello image VHD files get created by default in hello same storage account that hello original VM used.</span></span> <span data-ttu-id="f7eaa-148">Gebruik Hallo *hetzelfde opslagaccount* toostore Hallo VHD's voor een nieuwe virtuele machines die u uit Hallo installatiekopie maken.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-148">Use hello *same storage account* toostore hello VHDs for any new VMs you create from hello image.</span></span> 

6. <span data-ttu-id="f7eaa-149">toofind hello locatie van een vastgelegde installatiekopie open Hallo JSON-sjabloon in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-149">toofind hello location of a captured image, open hello JSON template in a text editor.</span></span> <span data-ttu-id="f7eaa-150">In Hallo **storageProfile**, Hallo zoeken **uri** Hallo **installatiekopie** zich in Hallo **system** container.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-150">In hello **storageProfile**, find hello **uri** of hello **image** located in hello **system** container.</span></span> <span data-ttu-id="f7eaa-151">Bijvoorbeeld: hello URI Hallo OS schijfkopie lijkt te`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="f7eaa-151">For example, hello URI of hello OS disk image is similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="f7eaa-152">Stap 3: Een virtuele machine maken vanuit Hallo vastgelegde installatiekopie</span><span class="sxs-lookup"><span data-stu-id="f7eaa-152">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="f7eaa-153">Nu Hallo installatiekopie gebruiken met een sjabloon toocreate een Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-153">Now use hello image with a template toocreate a Linux VM.</span></span> <span data-ttu-id="f7eaa-154">Deze stappen ziet u hoe toouse hello Azure CLI en Hallo JSON-bestandssjabloon vastgelegd van toocreate Hallo VM in een nieuw virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-154">These steps show you how toouse hello Azure CLI and hello JSON file template you captured toocreate hello VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="f7eaa-155">Maken van netwerkbronnen</span><span class="sxs-lookup"><span data-stu-id="f7eaa-155">Create network resources</span></span>
<span data-ttu-id="f7eaa-156">toouse hello sjabloon, moet u eerst tooset van een virtueel netwerk en de NIC voor uw nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-156">toouse hello template, you first need tooset up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="f7eaa-157">U wordt aangeraden maken van een resourcegroep voor deze resources op Hallo-locatie waar uw VM-installatiekopie is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-157">We recommend you create a resource group for these resources in hello location where your VM image is stored.</span></span> <span data-ttu-id="f7eaa-158">Voer de opdrachten vergelijkbare toohello te volgen, vervangen door namen voor uw resources en juiste Azure locatie ('centralus' in deze opdrachten):</span><span class="sxs-lookup"><span data-stu-id="f7eaa-158">Run commands similar toohello following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a><span data-ttu-id="f7eaa-159">Hallo Hallo NIC-Id ophalen</span><span class="sxs-lookup"><span data-stu-id="f7eaa-159">Get hello Id of hello NIC</span></span>
<span data-ttu-id="f7eaa-160">toodeploy een virtuele machine uit Hallo installatiekopie met behulp van Hallo JSON die u hebt opgeslagen tijdens het vastleggen, moet u Hallo-Id van Hallo NIC.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-160">toodeploy a VM from hello image by using hello JSON you saved during capture, you need hello Id of hello NIC.</span></span> <span data-ttu-id="f7eaa-161">Het door het uitvoeren van de volgende opdracht Hallo verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="f7eaa-161">Obtain it by running hello following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="f7eaa-162">Hallo **Id** in Hallo uitvoer ziet er ongeveer te`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="f7eaa-162">hello **Id** in hello output is similar too`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="f7eaa-163">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="f7eaa-163">Create a VM</span></span>
<span data-ttu-id="f7eaa-164">Nu uitvoeren Hallo volgende toocreate opdracht vastgelegd uw VM van Hallo VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-164">Now run hello following command toocreate your VM from hello captured VM image.</span></span> <span data-ttu-id="f7eaa-165">Gebruik Hallo **-f** parameter toospecify Hallo pad toohello sjabloon JSON bestand opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-165">Use hello **-f** parameter toospecify hello path toohello template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="f7eaa-166">In de opdrachtuitvoer hello, vraag toosupply zijn een nieuwe VM-naam, Hallo beheerdersgebruikersnaam en wachtwoord en Hallo-Id van Hallo NIC die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-166">In hello command output, you are prompted toosupply a new VM name, hello admin user name and password, and hello Id of hello NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="f7eaa-167">Hallo volgende voorbeeld ziet u wat u voor een geslaagde implementatie zien:</span><span class="sxs-lookup"><span data-stu-id="f7eaa-167">hello following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="f7eaa-168">Hallo-implementatie controleren</span><span class="sxs-lookup"><span data-stu-id="f7eaa-168">Verify hello deployment</span></span>
<span data-ttu-id="f7eaa-169">Nu SSH toohello virtuele machine u tooverify Hallo implementatie en begin met behulp van gemaakt Hallo nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-169">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="f7eaa-170">tooconnect via SSH, Hallo IP-adres van de virtuele machine die u hebt gemaakt door het uitvoeren van de volgende opdracht Hallo Hallo vinden:</span><span class="sxs-lookup"><span data-stu-id="f7eaa-170">tooconnect via SSH, find hello IP address of hello VM you created by running hello following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="f7eaa-171">Hallo openbaar IP-adres wordt vermeld in de opdrachtuitvoer Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-171">hello public IP address is listed in hello command output.</span></span> <span data-ttu-id="f7eaa-172">U maken standaard verbinding toohello Linux-VM met SSH op poort 22.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-172">By default you connect toohello Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="f7eaa-173">Aanvullende virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="f7eaa-173">Create additional VMs</span></span>
<span data-ttu-id="f7eaa-174">Gebruik Hallo vastgelegde installatiekopie en de sjabloon toodeploy extra virtuele machines met Hallo stappen in de voorgaande sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-174">Use hello captured image and template toodeploy additional VMs using hello steps in hello preceding section.</span></span> <span data-ttu-id="f7eaa-175">Andere opties toocreate virtuele machines van de installatiekopie van het Hallo opnemen met behulp van een sjabloon Quick Start of Hallo uitgevoerd **azure vm maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-175">Other options toocreate VMs from hello image include using a quickstart template or running hello **azure vm create** command.</span></span>

### <a name="use-hello-captured-template"></a><span data-ttu-id="f7eaa-176">Vastgelegde Hallo-sjabloon gebruiken</span><span class="sxs-lookup"><span data-stu-id="f7eaa-176">Use hello captured template</span></span>
<span data-ttu-id="f7eaa-177">Hallo toouse vastgelegde installatiekopie en de sjabloon, als volgt te werk (beschreven in voorgaande sectie Hallo):</span><span class="sxs-lookup"><span data-stu-id="f7eaa-177">toouse hello captured image and template, follow these steps (detailed in hello preceding section):</span></span>

* <span data-ttu-id="f7eaa-178">Zorg ervoor dat uw VM-installatiekopie Hallo hetzelfde opslagaccount die als host fungeert voor uw VM VHD.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-178">Ensure that your VM image is in hello same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="f7eaa-179">Hallo sjabloon JSON-bestand kopiëren en geef een unieke naam voor de besturingssysteemschijf Hallo Hallo nieuwe VM VHD (of VHD's).</span><span class="sxs-lookup"><span data-stu-id="f7eaa-179">Copy hello template JSON file and specify a unique name for hello OS disk of hello new VM's VHD (or VHDs).</span></span> <span data-ttu-id="f7eaa-180">Bijvoorbeeld in Hallo **storageProfile**onder **vhd**in **uri**, Geef een unieke naam voor Hallo **osDisk** VHD vergelijkbaar te`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="f7eaa-180">For example, in hello **storageProfile**, under **vhd**, in **uri**, specify a unique name for hello **osDisk** VHD, similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="f7eaa-181">Maak een NIC in beide Hallo dezelfde of een ander virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-181">Create a NIC in either hello same or a different virtual network.</span></span>
* <span data-ttu-id="f7eaa-182">Hallo gewijzigd sjabloon JSON-bestand gebruikt, maakt u een implementatie in de resourcegroep Hallo in waarmee u een virtueel netwerk Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-182">Using hello modified template JSON file, create a deployment in hello resource group in which you set up hello virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="f7eaa-183">Een Quick Start-sjabloon gebruiken</span><span class="sxs-lookup"><span data-stu-id="f7eaa-183">Use a quickstart template</span></span>
<span data-ttu-id="f7eaa-184">Als u instellen automatisch wanneer u een virtuele machine van de installatiekopie van het Hallo maakt Hallo-netwerk wilt, kunt u deze resources in een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-184">If you want hello network set up automatically when you create a VM from hello image, you can specify those resources in a template.</span></span> <span data-ttu-id="f7eaa-185">Zie bijvoorbeeld Hallo [101-vm-van-gebruiker-image sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-185">For example, see hello [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="f7eaa-186">Deze sjabloon maakt een virtuele machine van uw aangepaste installatiekopie en Hallo nodig virtueel netwerk, openbare IP-adres en NIC-resources.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-186">This template creates a VM from your custom image and hello necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="f7eaa-187">Zie voor een overzicht van het gebruik van de sjabloon Hallo in hello Azure-portal [hoe een virtuele machine van een aangepaste installatiekopie met Resource Manager-sjabloon toocreate](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span><span class="sxs-lookup"><span data-stu-id="f7eaa-187">For a walkthrough of using hello template in hello Azure portal, see [How toocreate a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-hello-azure-vm-create-command"></a><span data-ttu-id="f7eaa-188">Gebruik hello azure vm-opdracht maken</span><span class="sxs-lookup"><span data-stu-id="f7eaa-188">Use hello azure vm create command</span></span>
<span data-ttu-id="f7eaa-189">Meestal is het eenvoudigste toouse een Resource Manager-sjabloon toocreate een virtuele machine uit Hallo-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-189">Usually it's easiest toouse a Resource Manager template toocreate a VM from hello image.</span></span> <span data-ttu-id="f7eaa-190">U kunt echter Hallo VM maken *imperatively* met behulp van Hallo **azure vm maken** opdracht Hello **-Q** (**--installatiekopie urn**) parameter .</span><span class="sxs-lookup"><span data-stu-id="f7eaa-190">However, you can create hello VM *imperatively* by using hello **azure vm create** command with hello **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="f7eaa-191">Als u deze methode gebruikt, u ook Hallo doorgeven **-d** (**--os-schijf-vhd**) parameter toospecify Hallo locatie van de VHD-bestand voor Hallo OS Hallo nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-191">If you use this method, you also pass hello **-d** (**--os-disk-vhd**) parameter toospecify hello location of hello OS .vhd file for hello new VM.</span></span> <span data-ttu-id="f7eaa-192">Dit bestand moet zich in Hallo VHD's container van Hallo opslagaccount waar Hallo installatiekopie VHD-bestand wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-192">This file must be in hello vhds container of hello storage account where hello image VHD file is stored.</span></span> <span data-ttu-id="f7eaa-193">opdracht kopieën hello VHD voor Hallo Hallo nieuwe virtuele machine automatisch toohello **VHD's** container.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-193">hello command copies hello VHD for hello new VM automatically toohello **vhds** container.</span></span>

<span data-ttu-id="f7eaa-194">Voordat u **azure vm maken** voltooien met installatiekopie van het Hallo Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f7eaa-194">Before running **azure vm create** with hello image, complete hello following steps:</span></span>

1. <span data-ttu-id="f7eaa-195">Een resourcegroep maken of een bestaande resourcegroep voor Hallo implementatie identificeren.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-195">Create a resource group, or identify an existing resource group for hello deployment.</span></span>
2. <span data-ttu-id="f7eaa-196">Maken van een openbare IP-adres resource en een NIC-resource voor Hallo nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-196">Create a public IP address resource and a NIC resource for hello new VM.</span></span> <span data-ttu-id="f7eaa-197">Zie eerder in dit artikel voor stappen toocreate de een virtueel netwerk, openbare IP-adres en NIC met behulp van Hallo CLI.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-197">For steps toocreate a virtual network, public IP address, and NIC by using hello CLI, see earlier in this article.</span></span> <span data-ttu-id="f7eaa-198">(**azure vm maken** kunt ook een NIC maken, maar moet u extra parameters toopass voor een virtueel netwerk en subnet.)</span><span class="sxs-lookup"><span data-stu-id="f7eaa-198">(**azure vm create** can also create a NIC, but you need toopass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="f7eaa-199">Voer vervolgens een opdracht die wordt doorgegeven URI's tooboth Hallo nieuwe OS-VHD-bestand en Hallo bestaande installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-199">Then run a command that passes URIs tooboth hello new OS VHD file and hello existing image.</span></span> <span data-ttu-id="f7eaa-200">In dit voorbeeld wordt een grootte Standard_A1 VM wordt gemaakt in de regio VS-Oost Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-200">In this example, a size Standard_A1 VM is created in hello East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="f7eaa-201">Voor extra opdrachtopties, voert u `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="f7eaa-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7eaa-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f7eaa-202">Next steps</span></span>
<span data-ttu-id="f7eaa-203">toomanage uw virtuele machines met Hallo CLI, Zie Hallo taken in [implementeren en beheren van virtuele machines met behulp van Azure Resource Manager-sjablonen en Azure CLI Hallo](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="f7eaa-203">toomanage your VMs with hello CLI, see hello tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

