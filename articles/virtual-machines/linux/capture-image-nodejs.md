---
title: Vastleggen van een Azure Linux VM te gebruiken als sjabloon | Microsoft Docs
description: Informatie over het vastleggen en een installatiekopie van een Linux-gebaseerde Azure virtuele machine (VM) gemaakt met het Azure Resource Manager-implementatiemodel generalize.
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
ms.openlocfilehash: b1164fbd816eea5189786850f096438e32f8f802
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="7fd46-103">Vastleggen van een virtuele Linux-machine uitgevoerd op Azure</span><span class="sxs-lookup"><span data-stu-id="7fd46-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="7fd46-104">Volg de stappen in dit artikel generaliseren en vastleggen van uw Azure Linux virtuele machine (VM) in het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="7fd46-104">Follow the steps in this article to generalize and capture your Azure Linux virtual machine (VM) in the Resource Manager deployment model.</span></span> <span data-ttu-id="7fd46-105">Wanneer u de virtuele machine generalize, kunt u persoonlijke gegevens te verwijderen en voorbereiden van de virtuele machine moet worden gebruikt als een afbeelding.</span><span class="sxs-lookup"><span data-stu-id="7fd46-105">When you generalize the VM, you remove personal account information and prepare the VM to be used as an image.</span></span> <span data-ttu-id="7fd46-106">U vervolgens een installatiekopie van een gegeneraliseerde virtuele harde schijf (VHD) voor het besturingssysteem, virtuele harde schijven voor bijgesloten gegevensschijven, vastleggen en een [Resource Manager-sjabloon](../../azure-resource-manager/resource-group-overview.md) voor nieuwe VM-implementaties.</span><span class="sxs-lookup"><span data-stu-id="7fd46-106">You then capture a generalized virtual hard disk (VHD) image for the OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="7fd46-107">Dit artikel wordt uitgelegd hoe u een VM-installatiekopie met de Azure CLI 1.0 vastleggen voor een virtuele machine met niet-beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="7fd46-107">This article details how to capture a VM image with the Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="7fd46-108">U kunt ook [vastleggen van een VM die gebruikmaakt van Azure beheerd schijven met de Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7fd46-108">You can also [capture a VM using Azure Managed Disks with the Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7fd46-109">Beheerde schijven worden verwerkt door de Azure-platform en hoeven niet de voorbereidings- of locatie om op te slaan.</span><span class="sxs-lookup"><span data-stu-id="7fd46-109">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="7fd46-110">Zie [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Overzicht van Azure Managed Disks) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7fd46-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="7fd46-111">Netwerkbronnen voor elke nieuwe virtuele machine instellen voor het maken van virtuele machines met behulp van de installatiekopie en de sjabloon (een JavaScript Object Notation of JSON,-bestand) gebruiken voor het implementeren van de vastgelegde VHD-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="7fd46-111">To create VMs using the image, set up network resources for each new VM, and use the template (a JavaScript Object Notation, or JSON, file) to deploy it from the captured VHD images.</span></span> <span data-ttu-id="7fd46-112">Op deze manier kunt u een virtuele machine met de huidige softwareconfiguratie, worden dezelfde manier als die u installatiekopieën in Azure Marketplace gebruiken repliceren.</span><span class="sxs-lookup"><span data-stu-id="7fd46-112">In this way, you can replicate a VM with its current software configuration, similar to the way you use images in the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="7fd46-113">Als u wilt maken van een kopie van uw bestaande Linux-VM met de speciale staat voor de back-up of foutopsporing, Zie [een kopie maken van een virtuele Linux-machine uitgevoerd op Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7fd46-113">If you want to create a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7fd46-114">En als u een Linux VHD uploaden van een lokale virtuele machine wilt, Zie [uploaden en Linux-VM te maken van aangepaste schijfimage](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7fd46-114">And if you want to upload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="7fd46-115">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="7fd46-115">CLI versions to complete the task</span></span>
<span data-ttu-id="7fd46-116">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="7fd46-116">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="7fd46-117">[Azure CLI 1.0](#before-you-begin) – onze CLI voor het klassieke en resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="7fd46-117">[Azure CLI 1.0](#before-you-begin) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="7fd46-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="7fd46-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7fd46-119">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="7fd46-119">Before you begin</span></span>
<span data-ttu-id="7fd46-120">Zorg ervoor dat u voldoet aan de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="7fd46-120">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="7fd46-121">**Azure virtuele machine gemaakt in het Resource Manager-implementatiemodel** -als u een Linux-VM nog niet hebt gemaakt, kunt u de [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), wordt de [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), of [Resource Manager-sjablonen](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="7fd46-121">**Azure VM created in the Resource Manager deployment model** - If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), the [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="7fd46-122">De virtuele machine naar wens configureren.</span><span class="sxs-lookup"><span data-stu-id="7fd46-122">Configure the VM as needed.</span></span> <span data-ttu-id="7fd46-123">Bijvoorbeeld: [gegevensschijven toevoegen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), toepassen van updates en toepassingen te installeren.</span><span class="sxs-lookup"><span data-stu-id="7fd46-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="7fd46-124">**Azure CLI** -installeren van de [Azure CLI](../../cli-install-nodejs.md) op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="7fd46-124">**Azure CLI** - Install the [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-the-azure-linux-agent"></a><span data-ttu-id="7fd46-125">Stap 1: De Azure Linux-agent verwijderen</span><span class="sxs-lookup"><span data-stu-id="7fd46-125">Step 1: Remove the Azure Linux agent</span></span>
<span data-ttu-id="7fd46-126">Voer eerst de **waagent** opdracht met de **deprovision** parameter voor de Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="7fd46-126">First, run the **waagent** command with the **deprovision** parameter on the Linux VM.</span></span> <span data-ttu-id="7fd46-127">Deze opdracht verwijdert u bestanden en gegevens om de virtuele machine gereed is voor het generaliseren.</span><span class="sxs-lookup"><span data-stu-id="7fd46-127">This command deletes files and data to make the VM ready for generalizing.</span></span> <span data-ttu-id="7fd46-128">Zie voor meer informatie de [gebruikershandleiding voor Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7fd46-128">For details, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="7fd46-129">Verbinding maken met uw Linux-VM met behulp van een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="7fd46-129">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="7fd46-130">Typ de volgende opdracht in het venster SSH:</span><span class="sxs-lookup"><span data-stu-id="7fd46-130">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="7fd46-131">Deze opdracht alleen uitvoeren op een virtuele machine die u van plan bent om vast te leggen als afbeelding.</span><span class="sxs-lookup"><span data-stu-id="7fd46-131">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="7fd46-132">Er is geen garantie dat de installatiekopie wordt gewist van alle gevoelige informatie of geschikt is voor de herdistributie.</span><span class="sxs-lookup"><span data-stu-id="7fd46-132">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="7fd46-133">Type **y** om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="7fd46-133">Type **y** to continue.</span></span> <span data-ttu-id="7fd46-134">U kunt toevoegen de **-force** parameter om te voorkomen dat deze bevestigingsstap.</span><span class="sxs-lookup"><span data-stu-id="7fd46-134">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="7fd46-135">Nadat u de opdracht is voltooid, typt u **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="7fd46-135">After the command completes, type **exit**.</span></span> <span data-ttu-id="7fd46-136">Deze stap wordt gesloten voor de SSH-client.</span><span class="sxs-lookup"><span data-stu-id="7fd46-136">This step closes the SSH client.</span></span>

## <a name="step-2-capture-the-vm"></a><span data-ttu-id="7fd46-137">Stap 2: De virtuele machine vastleggen</span><span class="sxs-lookup"><span data-stu-id="7fd46-137">Step 2: Capture the VM</span></span>
<span data-ttu-id="7fd46-138">Gebruik de Azure CLI generaliseren en vastleggen van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7fd46-138">Use the Azure CLI to generalize and capture the VM.</span></span> <span data-ttu-id="7fd46-139">In de volgende voorbeelden kunt u de parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="7fd46-139">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="7fd46-140">De namen van de voorbeeld-parameter **myResourceGroup**, **myVnet**, en **myVM**.</span><span class="sxs-lookup"><span data-stu-id="7fd46-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="7fd46-141">Open in uw lokale computer, de Azure CLI en [Meld u aan bij uw Azure-abonnement](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="7fd46-141">From your local computer, open the Azure CLI and [login to your Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="7fd46-142">Zorg ervoor dat u in de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7fd46-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="7fd46-143">Sluit de virtuele machine die u al gemaakt met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7fd46-143">Shut down the VM that you already deprovisioned by using the following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="7fd46-144">Generaliseer de virtuele machine met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7fd46-144">Generalize the VM with the following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="7fd46-145">Voer nu de **azure vm vastleggen** opdracht, waarmee de virtuele machine worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="7fd46-145">Now run the **azure vm capture** command, which captures the VM.</span></span> <span data-ttu-id="7fd46-146">In het volgende voorbeeld wordt de installatiekopie van het vastleggen van VHD's met namen die begint met **MyVHDNamePrefix**, en de **-t** optie geeft u een pad naar de sjabloon **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="7fd46-146">In the following example, the image VHDs are captured with names beginning with **MyVHDNamePrefix**, and the **-t** option specifies a path to the template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="7fd46-147">De VHD-bestanden van de installatiekopie gemaakt in hetzelfde opslagaccount die de oorspronkelijke VM gebruikt standaard.</span><span class="sxs-lookup"><span data-stu-id="7fd46-147">The image VHD files get created by default in the same storage account that the original VM used.</span></span> <span data-ttu-id="7fd46-148">Gebruik de *hetzelfde opslagaccount* voor het opslaan van de VHD's voor nieuwe VM's u van de installatiekopie maken.</span><span class="sxs-lookup"><span data-stu-id="7fd46-148">Use the *same storage account* to store the VHDs for any new VMs you create from the image.</span></span> 

6. <span data-ttu-id="7fd46-149">Als u wilt zoeken naar de locatie van een vastgelegde installatiekopie, opent u het JSON-sjabloon in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="7fd46-149">To find the location of a captured image, open the JSON template in a text editor.</span></span> <span data-ttu-id="7fd46-150">In de **storageProfile**, vinden de **uri** van de **installatiekopie** zich in de **system** container.</span><span class="sxs-lookup"><span data-stu-id="7fd46-150">In the **storageProfile**, find the **uri** of the **image** located in the **system** container.</span></span> <span data-ttu-id="7fd46-151">Bijvoorbeeld: de URI van de installatiekopie van de OS-schijf is vergelijkbaar met`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="7fd46-151">For example, the URI of the OS disk image is similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="7fd46-152">Stap 3: Een virtuele machine van de vastgelegde installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="7fd46-152">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="7fd46-153">De afbeelding met een sjabloon nu gebruiken voor het maken van een Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="7fd46-153">Now use the image with a template to create a Linux VM.</span></span> <span data-ttu-id="7fd46-154">Deze stappen ziet u hoe u de Azure CLI en het JSON-bestand-sjabloon die u hebt vastgelegd voor het maken van de virtuele machine in een nieuw virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="7fd46-154">These steps show you how to use the Azure CLI and the JSON file template you captured to create the VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="7fd46-155">Maken van netwerkbronnen</span><span class="sxs-lookup"><span data-stu-id="7fd46-155">Create network resources</span></span>
<span data-ttu-id="7fd46-156">De sjabloon wilt gebruiken, moet u eerst een virtueel netwerk en NIC instellen voor uw nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7fd46-156">To use the template, you first need to set up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="7fd46-157">Het is raadzaam om dat het maken van een resourcegroep voor deze bronnen op de locatie waar uw VM-installatiekopie is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7fd46-157">We recommend you create a resource group for these resources in the location where your VM image is stored.</span></span> <span data-ttu-id="7fd46-158">De opdrachten uitvoeren is vergelijkbaar met de volgende, waarbij namen voor uw resources en juiste Azure locatie ('centralus' in deze opdrachten):</span><span class="sxs-lookup"><span data-stu-id="7fd46-158">Run commands similar to the following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-the-id-of-the-nic"></a><span data-ttu-id="7fd46-159">De Id van de NIC verkrijgen</span><span class="sxs-lookup"><span data-stu-id="7fd46-159">Get the Id of the NIC</span></span>
<span data-ttu-id="7fd46-160">Voor het implementeren van een virtuele machine van de installatiekopie met behulp van de JSON die u hebt opgeslagen tijdens het vastleggen, moet u de Id van de NIC.</span><span class="sxs-lookup"><span data-stu-id="7fd46-160">To deploy a VM from the image by using the JSON you saved during capture, you need the Id of the NIC.</span></span> <span data-ttu-id="7fd46-161">U ontvangt deze met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7fd46-161">Obtain it by running the following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="7fd46-162">De **Id** in de uitvoer is vergelijkbaar met`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="7fd46-162">The **Id** in the output is similar to `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="7fd46-163">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="7fd46-163">Create a VM</span></span>
<span data-ttu-id="7fd46-164">Voer nu de volgende opdracht voor het maken van uw virtuele machine van de vastgelegde installatiekopie van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7fd46-164">Now run the following command to create your VM from the captured VM image.</span></span> <span data-ttu-id="7fd46-165">Gebruik de **-f** parameter om het pad naar het sjabloon JSON-bestand die u hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7fd46-165">Use the **-f** parameter to specify the path to the template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="7fd46-166">In de opdrachtuitvoer wordt u gevraagd om op te geven van een nieuwe VM-naam, de admin-gebruikersnaam en wachtwoord en de Id van de NIC die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7fd46-166">In the command output, you are prompted to supply a new VM name, the admin user name and password, and the Id of the NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="7fd46-167">Het volgende voorbeeld ziet u wat u voor een geslaagde implementatie zien:</span><span class="sxs-lookup"><span data-stu-id="7fd46-167">The following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment to complete
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

### <a name="verify-the-deployment"></a><span data-ttu-id="7fd46-168">De implementatie controleren</span><span class="sxs-lookup"><span data-stu-id="7fd46-168">Verify the deployment</span></span>
<span data-ttu-id="7fd46-169">Nu SSH aan de virtuele machine die u hebt gemaakt om te controleren of de implementatie en begin met behulp van de nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7fd46-169">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="7fd46-170">Als u wilt verbinding maken via SSH, vinden de IP-adres van de virtuele machine die u hebt gemaakt met de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="7fd46-170">To connect via SSH, find the IP address of the VM you created by running the following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="7fd46-171">Het openbare IP-adres wordt vermeld in de opdrachtuitvoer.</span><span class="sxs-lookup"><span data-stu-id="7fd46-171">The public IP address is listed in the command output.</span></span> <span data-ttu-id="7fd46-172">Standaard verbinding u met de Linux-VM met SSH op poort 22.</span><span class="sxs-lookup"><span data-stu-id="7fd46-172">By default you connect to the Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="7fd46-173">Aanvullende virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="7fd46-173">Create additional VMs</span></span>
<span data-ttu-id="7fd46-174">Gebruik de vastgelegde installatiekopie en de sjabloon voor het implementeren van extra virtuele machines met de stappen in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="7fd46-174">Use the captured image and template to deploy additional VMs using the steps in the preceding section.</span></span> <span data-ttu-id="7fd46-175">Andere opties voor het maken van virtuele machines van de installatiekopie met behulp van een sjabloon Quick Start of uitgevoerd zijn de **azure vm maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="7fd46-175">Other options to create VMs from the image include using a quickstart template or running the **azure vm create** command.</span></span>

### <a name="use-the-captured-template"></a><span data-ttu-id="7fd46-176">De vastgelegde sjabloon gebruiken</span><span class="sxs-lookup"><span data-stu-id="7fd46-176">Use the captured template</span></span>
<span data-ttu-id="7fd46-177">Als u de vastgelegde installatiekopie en de sjabloon, volgt (gespecificeerd in de vorige sectie):</span><span class="sxs-lookup"><span data-stu-id="7fd46-177">To use the captured image and template, follow these steps (detailed in the preceding section):</span></span>

* <span data-ttu-id="7fd46-178">Zorg ervoor dat uw VM-installatiekopie in hetzelfde opslagaccount die als host fungeert voor uw VM VHD.</span><span class="sxs-lookup"><span data-stu-id="7fd46-178">Ensure that your VM image is in the same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="7fd46-179">Kopieer het JSON-bestand van het sjabloon en geef een unieke naam voor de besturingssysteemschijf van de nieuwe VM VHD (of VHD's).</span><span class="sxs-lookup"><span data-stu-id="7fd46-179">Copy the template JSON file and specify a unique name for the OS disk of the new VM's VHD (or VHDs).</span></span> <span data-ttu-id="7fd46-180">Bijvoorbeeld, in de **storageProfile**onder **vhd**in **uri**, Geef een unieke naam voor de **osDisk** VHD, vergelijkbaar met`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="7fd46-180">For example, in the **storageProfile**, under **vhd**, in **uri**, specify a unique name for the **osDisk** VHD, similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="7fd46-181">Maak een NIC in dezelfde of een ander virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="7fd46-181">Create a NIC in either the same or a different virtual network.</span></span>
* <span data-ttu-id="7fd46-182">Maak een implementatie met de gewijzigde sjabloon JSON-bestand in de resourcegroep waarin u het virtuele netwerk hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7fd46-182">Using the modified template JSON file, create a deployment in the resource group in which you set up the virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="7fd46-183">Een Quick Start-sjabloon gebruiken</span><span class="sxs-lookup"><span data-stu-id="7fd46-183">Use a quickstart template</span></span>
<span data-ttu-id="7fd46-184">Als u het instellen van het automatisch wanneer u een virtuele machine van de installatiekopie van het maakt netwerk wilt, kunt u deze resources in een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7fd46-184">If you want the network set up automatically when you create a VM from the image, you can specify those resources in a template.</span></span> <span data-ttu-id="7fd46-185">Zie bijvoorbeeld de [101-vm-van-gebruiker-image sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="7fd46-185">For example, see the [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="7fd46-186">Deze sjabloon maakt een virtuele machine van uw aangepaste installatiekopie en de benodigde virtueel netwerk, openbare IP-adres en NIC-bronnen.</span><span class="sxs-lookup"><span data-stu-id="7fd46-186">This template creates a VM from your custom image and the necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="7fd46-187">Zie voor een overzicht van het gebruik van de sjabloon in de Azure portal [maken van een virtuele machine uit een aangepaste installatiekopie met Resource Manager-sjabloon](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span><span class="sxs-lookup"><span data-stu-id="7fd46-187">For a walkthrough of using the template in the Azure portal, see [How to create a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-the-azure-vm-create-command"></a><span data-ttu-id="7fd46-188">Gebruik de azure vm-opdracht maken</span><span class="sxs-lookup"><span data-stu-id="7fd46-188">Use the azure vm create command</span></span>
<span data-ttu-id="7fd46-189">Meestal is het eenvoudigste Resource Manager-sjabloon gebruiken om te maken van een virtuele machine uit de afbeelding.</span><span class="sxs-lookup"><span data-stu-id="7fd46-189">Usually it's easiest to use a Resource Manager template to create a VM from the image.</span></span> <span data-ttu-id="7fd46-190">U kunt echter de virtuele machine maken *imperatively* met behulp van de **azure vm maken** opdracht met de **-Q** (**--installatiekopie urn**) parameter.</span><span class="sxs-lookup"><span data-stu-id="7fd46-190">However, you can create the VM *imperatively* by using the **azure vm create** command with the **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="7fd46-191">Als u deze methode gebruikt, geeft u ook de **-d** (**--os-schijf-vhd**) parameter om de locatie van het besturingssysteem-VHD-bestand voor de nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7fd46-191">If you use this method, you also pass the **-d** (**--os-disk-vhd**) parameter to specify the location of the OS .vhd file for the new VM.</span></span> <span data-ttu-id="7fd46-192">Dit bestand moet zich in de container VHD's van het opslagaccount waar het VHD-bestand wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7fd46-192">This file must be in the vhds container of the storage account where the image VHD file is stored.</span></span> <span data-ttu-id="7fd46-193">De opdracht kopieert u de VHD voor de nieuwe virtuele machine automatisch omgeleid naar de **VHD's** container.</span><span class="sxs-lookup"><span data-stu-id="7fd46-193">The command copies the VHD for the new VM automatically to the **vhds** container.</span></span>

<span data-ttu-id="7fd46-194">Voordat u **azure vm maken** met de installatiekopie, de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7fd46-194">Before running **azure vm create** with the image, complete the following steps:</span></span>

1. <span data-ttu-id="7fd46-195">Een resourcegroep maken of een bestaande resourcegroep voor de implementatie identificeren.</span><span class="sxs-lookup"><span data-stu-id="7fd46-195">Create a resource group, or identify an existing resource group for the deployment.</span></span>
2. <span data-ttu-id="7fd46-196">De bron van een openbare IP-adres en een NIC-resource maken voor de nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7fd46-196">Create a public IP address resource and a NIC resource for the new VM.</span></span> <span data-ttu-id="7fd46-197">Zie voor stappen voor het maken van een virtueel netwerk, het openbare IP-adres en de NIC met behulp van de CLI, eerder in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="7fd46-197">For steps to create a virtual network, public IP address, and NIC by using the CLI, see earlier in this article.</span></span> <span data-ttu-id="7fd46-198">(**azure vm maken** ook een NIC kunt maken, maar u moet extra parameters voor een virtueel netwerk en subnet doorgeven.)</span><span class="sxs-lookup"><span data-stu-id="7fd46-198">(**azure vm create** can also create a NIC, but you need to pass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="7fd46-199">Voer vervolgens een opdracht die wordt doorgegeven URI's op het nieuwe besturingssysteem-VHD-bestand en de bestaande installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="7fd46-199">Then run a command that passes URIs to both the new OS VHD file and the existing image.</span></span> <span data-ttu-id="7fd46-200">In dit voorbeeld wordt een grootte Standard_A1 VM wordt gemaakt in de regio VS-Oost.</span><span class="sxs-lookup"><span data-stu-id="7fd46-200">In this example, a size Standard_A1 VM is created in the East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="7fd46-201">Voor extra opdrachtopties, voert u `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="7fd46-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fd46-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7fd46-202">Next steps</span></span>
<span data-ttu-id="7fd46-203">Zie de taken in voor het beheren van uw virtuele machines met de CLI [implementeren en beheren van virtuele machines met behulp van Azure Resource Manager-sjablonen en de Azure CLI](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="7fd46-203">To manage your VMs with the CLI, see the tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

