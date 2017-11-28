---
title: een installatiekopie van een niet-beheerde van een gegeneraliseerde virtuele machine in Azure aaaCreate | Microsoft Docs
description: Een unmanged installatiekopie maken van een gegeneraliseerde virtuele Windows-machine toouse toocreate meerdere exemplaren van een virtuele machine in Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="d28b0-103">Hoe toocreate een niet-beheerde virtuele machine een installatiekopie van een Azure VM</span><span class="sxs-lookup"><span data-stu-id="d28b0-103">How toocreate an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="d28b0-104">In dit artikel bevat informatie over met behulp van storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="d28b0-104">This article covers using storage accounts.</span></span> <span data-ttu-id="d28b0-105">Het is raadzaam dat u beheerde schijven en beheerde installatiekopieën in plaats van een opslagaccount gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d28b0-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="d28b0-106">Zie voor meer informatie [beheerde-installatiekopie van een gegeneraliseerde virtuele machine in Azure](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d28b0-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="d28b0-107">Dit artikel ziet u hoe toouse Azure PowerShell toocreate een installatiekopie van een gegeneraliseerde virtuele machine van Azure met behulp van een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="d28b0-107">This article shows you how toouse Azure PowerShell toocreate an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="d28b0-108">U kunt een andere virtuele machine vervolgens Hallo installatiekopie toocreate.</span><span class="sxs-lookup"><span data-stu-id="d28b0-108">You can then use hello image toocreate another VM.</span></span> <span data-ttu-id="d28b0-109">Hallo installatiekopie bevat Hallo besturingssysteemschijf en gegevensschijven Hallo die aangesloten toohello virtuele machine zijn.</span><span class="sxs-lookup"><span data-stu-id="d28b0-109">hello image includes hello OS disk and hello data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="d28b0-110">Hallo installatiekopie bevat geen virtuele Hallo-netwerkbronnen, dus moet u tooset van deze bronnen bij het maken van nieuwe virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="d28b0-110">hello image doesn't include hello virtual network resources, so you need tooset up those resources when you create hello new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d28b0-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d28b0-111">Prerequisites</span></span>
<span data-ttu-id="d28b0-112">U moet Azure PowerShell-versie toohave 1.0.x of hoger zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d28b0-112">You need toohave Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="d28b0-113">Als u nog niet PowerShell hebt geïnstalleerd, leest u [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor de installatiestappen.</span><span class="sxs-lookup"><span data-stu-id="d28b0-113">If you haven't already installed PowerShell, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-hello-vm"></a><span data-ttu-id="d28b0-114">Hallo VM generalize</span><span class="sxs-lookup"><span data-stu-id="d28b0-114">Generalize hello VM</span></span> 
<span data-ttu-id="d28b0-115">Deze sectie leest u hoe toogeneralize uw Windows-machine voor gebruik als een afbeelding.</span><span class="sxs-lookup"><span data-stu-id="d28b0-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="d28b0-116">Het generaliseren van een virtuele machine verwijdert alle persoonlijke gegevens over uw account, onder andere en bereidt Hallo machine toobe gebruikt als een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="d28b0-116">Generalizing a VM removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="d28b0-117">Zie voor meer informatie over Sysprep [hoe tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="d28b0-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="d28b0-118">Zorg ervoor dat het Hallo-serverfuncties op Hallo machine worden ondersteund door Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d28b0-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="d28b0-119">Zie voor meer informatie [Sysprep-ondersteuning voor serverfuncties](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="d28b0-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d28b0-120">Als u uw VHD tooAzure voor Hallo eerst uploadt, controleert u of u hebt [uw virtuele machine voorbereid](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat Sysprep wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d28b0-120">If you are uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="d28b0-121">U kunt ook een Linux-VM met generalize `sudo waagent -deprovision+user` en gebruik vervolgens PowerShell toocapture Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="d28b0-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell toocapture hello VM.</span></span> <span data-ttu-id="d28b0-122">Zie voor meer informatie over het gebruik van Hallo CLI toocapture een virtuele machine [hoe toogeneralize en vastleggen een Linux-virtuele machine met Azure CLI Hallo ](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="d28b0-122">For information about using hello CLI toocapture a VM, see [How toogeneralize and capture a Linux virtual machine using hello Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="d28b0-123">Meld u aan toohello virtuele Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="d28b0-123">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="d28b0-124">Hallo-opdrachtpromptvenster open als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d28b0-124">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="d28b0-125">Hallo directory ook wijzigen**%windir%\system32\sysprep**, en voer vervolgens `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="d28b0-125">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="d28b0-126">In Hallo **hulpprogramma voor systeemvoorbereiding** dialoogvenster, **System Voer Out-of-Box Experience (OOBE)**, en zorg ervoor dat Hallo **Generalize** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d28b0-126">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="d28b0-127">In **afsluitopties**, selecteer **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="d28b0-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="d28b0-128">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d28b0-128">Click **OK**.</span></span>
   
    ![Sysprep starten](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="d28b0-130">Wanneer Sysprep is voltooid, afgesloten Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d28b0-130">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d28b0-131">Hallo VM niet opnieuw opstarten nadat u bent gereed uploaden Hallo VHD tooAzure of maken van een afbeelding van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="d28b0-131">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="d28b0-132">Als Hallo VM per ongeluk opnieuw opgestart wordt, voert u Sysprep toogeneralize deze opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d28b0-132">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 

## <a name="log-in-tooazure-powershell"></a><span data-ttu-id="d28b0-133">Meld u bij tooAzure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d28b0-133">Log in tooAzure PowerShell</span></span>
1. <span data-ttu-id="d28b0-134">Open Azure PowerShell en meld tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="d28b0-134">Open Azure PowerShell and sign in tooyour Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="d28b0-135">Een pop-upvenster wordt geopend voor tooenter u de referenties van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="d28b0-135">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
2. <span data-ttu-id="d28b0-136">Hallo abonnement-id's voor uw beschikbare abonnementen ophalen.</span><span class="sxs-lookup"><span data-stu-id="d28b0-136">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="d28b0-137">Set Hallo juiste abonnement Hallo abonnement-id.</span><span class="sxs-lookup"><span data-stu-id="d28b0-137">Set hello correct subscription using hello subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a><span data-ttu-id="d28b0-138">Hallo VM ongedaan en Hallo status toogeneralized instellen</span><span class="sxs-lookup"><span data-stu-id="d28b0-138">Deallocate hello VM and set hello state toogeneralized</span></span>
1. <span data-ttu-id="d28b0-139">Hallo VM netwerkbronnen ongedaan.</span><span class="sxs-lookup"><span data-stu-id="d28b0-139">Deallocate hello VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="d28b0-140">Hallo *Status* voor Hallo VM in hello Azure portal wordt gewijzigd van **gestopt** te**gestopt (toewijzing opgeheven)**.</span><span class="sxs-lookup"><span data-stu-id="d28b0-140">hello *Status* for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="d28b0-141">Hallo-status van Hallo virtuele machine te instellen**gegeneraliseerd**.</span><span class="sxs-lookup"><span data-stu-id="d28b0-141">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="d28b0-142">Controleer de status van de Hallo Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="d28b0-142">Check hello status of hello VM.</span></span> <span data-ttu-id="d28b0-143">Hallo **OSState/gegeneraliseerd** sectie voor Hallo VM Hallo hebt **DisplayStatus** instellen te**VM is gegeneraliseerd**.</span><span class="sxs-lookup"><span data-stu-id="d28b0-143">hello **OSState/generalized** section for hello VM should have hello **DisplayStatus** set too**VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a><span data-ttu-id="d28b0-144">Hallo installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="d28b0-144">Create hello image</span></span>

<span data-ttu-id="d28b0-145">Maak een installatiekopie van een niet-beheerde virtuele machine in Hallo bestemming storage-container die u met deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="d28b0-145">Create an unmanaged virtual machine image in hello destination storage container using this command.</span></span> <span data-ttu-id="d28b0-146">Hallo installatiekopie wordt gemaakt in Hallo hetzelfde opslagaccount als Hallo oorspronkelijke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d28b0-146">hello image is created in hello same storage account as hello original virtual machine.</span></span> <span data-ttu-id="d28b0-147">Hallo `-Path` parameter slaat een kopie van Hallo JSON-sjabloon voor Hallo bron VM tooyour lokale computer.</span><span class="sxs-lookup"><span data-stu-id="d28b0-147">hello `-Path` parameter saves a copy of hello JSON template for hello source VM tooyour local computer.</span></span> <span data-ttu-id="d28b0-148">Hallo `-DestinationContainerName` parameter heet Hallo Hallo-container die u toohold uw afbeeldingen wilt.</span><span class="sxs-lookup"><span data-stu-id="d28b0-148">hello `-DestinationContainerName` parameter is hello name of hello container that you want toohold your images.</span></span> <span data-ttu-id="d28b0-149">Als het Hallo-container bestaat niet, is het voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d28b0-149">If hello container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="d28b0-150">Hallo-URL van uw installatiekopie kunt u krijgen via Hallo JSON-bestandssjabloon.</span><span class="sxs-lookup"><span data-stu-id="d28b0-150">You can get hello URL of your image from hello JSON file template.</span></span> <span data-ttu-id="d28b0-151">Ga toohello **resources** > **storageProfile** > **osDisk** > **installatiekopie**  >  **uri** sectie voor het volledige pad Hallo van uw installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="d28b0-151">Go toohello **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for hello complete path of your image.</span></span> <span data-ttu-id="d28b0-152">Hallo-URL van de afbeelding Hallo eruitziet: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="d28b0-152">hello URL of hello image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="d28b0-153">U kunt ook controleren Hallo URI in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="d28b0-153">You can also verify hello URI in hello portal.</span></span> <span data-ttu-id="d28b0-154">Hallo-installatiekopie is gekopieerde tooa container met de naam **system** in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="d28b0-154">hello image is copied tooa container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-hello-image"></a><span data-ttu-id="d28b0-155">Een virtuele machine uit Hallo installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="d28b0-155">Create a VM from hello image</span></span>

<span data-ttu-id="d28b0-156">Nu kunt u een of meer VM's van niet-beheerde Hallo-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="d28b0-156">Now you can create one or more VMs from hello unmanaged image.</span></span>

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="d28b0-157">Hallo-URI van Hallo VHD instellen</span><span class="sxs-lookup"><span data-stu-id="d28b0-157">Set hello URI of hello VHD</span></span>

<span data-ttu-id="d28b0-158">Hallo URI voor Hallo VHD toouse heeft Hallo indeling: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**VHD.</span><span class="sxs-lookup"><span data-stu-id="d28b0-158">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="d28b0-159">In dit voorbeeld Hallo VHD met de naam **myVHD** is in het opslagaccount hello **mystorageaccount** in Hallo container **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="d28b0-159">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="d28b0-160">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="d28b0-160">Create a virtual network</span></span>
<span data-ttu-id="d28b0-161">Hallo vNet en subnet Hallo maken [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d28b0-161">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="d28b0-162">Hallo subnet maken.</span><span class="sxs-lookup"><span data-stu-id="d28b0-162">Create hello subnet.</span></span> <span data-ttu-id="d28b0-163">Hallo volgende voorbeeld maakt u een subnet met de naam **mySubnet** in de resourcegroep Hallo **myResourceGroup** met het Hallo-adresvoorvoegsel van **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="d28b0-163">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="d28b0-164">Hallo virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="d28b0-164">Create hello virtual network.</span></span> <span data-ttu-id="d28b0-165">Hallo volgende voorbeeld maakt u een virtueel netwerk met de naam **myVnet** in Hallo **VS-West** locatie met het Hallo-adresvoorvoegsel van **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="d28b0-165">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="d28b0-166">Een openbaar IP-adres en een netwerkinterface maken</span><span class="sxs-lookup"><span data-stu-id="d28b0-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="d28b0-167">tooenable communicatie met Hallo virtuele machine in het virtuele netwerk hello, moet u een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) en een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="d28b0-167">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="d28b0-168">Een openbaar IP-adres maken.</span><span class="sxs-lookup"><span data-stu-id="d28b0-168">Create a public IP address.</span></span> <span data-ttu-id="d28b0-169">In dit voorbeeld wordt een openbaar IP-adres met de naam **myPip**.</span><span class="sxs-lookup"><span data-stu-id="d28b0-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="d28b0-170">Hallo NIC. maken</span><span class="sxs-lookup"><span data-stu-id="d28b0-170">Create hello NIC.</span></span> <span data-ttu-id="d28b0-171">In dit voorbeeld wordt een NIC met de naam **myNic**.</span><span class="sxs-lookup"><span data-stu-id="d28b0-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="d28b0-172">Netwerkbeveiligingsgroep hello en een RDP-regel maken</span><span class="sxs-lookup"><span data-stu-id="d28b0-172">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="d28b0-173">toobe kunnen toolog in tooyour VM met RDP, moet u een regel waarmee RDP-toegang op poort 3389 toohave.</span><span class="sxs-lookup"><span data-stu-id="d28b0-173">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="d28b0-174">In dit voorbeeld maakt u een NSG met de naam **myNsg** die een regel aangeroepen bevat **myRdpRule** waarmee RDP-verkeer via poort 3389.</span><span class="sxs-lookup"><span data-stu-id="d28b0-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="d28b0-175">Zie voor meer informatie over Nsg [openen van poorten tooa VM in Azure met behulp van PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d28b0-175">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="d28b0-176">Een variabele voor Hallo virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="d28b0-176">Create a variable for hello virtual network</span></span>
<span data-ttu-id="d28b0-177">Maak een variabele voor het virtuele netwerk Hallo voltooid.</span><span class="sxs-lookup"><span data-stu-id="d28b0-177">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="d28b0-178">Hallo VM maken</span><span class="sxs-lookup"><span data-stu-id="d28b0-178">Create hello VM</span></span>
<span data-ttu-id="d28b0-179">Hallo volgende PowerShell wordt voltooid Hallo virtuele-machineconfiguraties en niet-beheerde installatiekopie als Hallo bron voor de nieuwe installatie Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d28b0-179">hello following PowerShell completes hello virtual machine configurations and uses unmanaged image as hello source for hello new installation.</span></span>

</br>

```powershell
    # Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="d28b0-180">Controleer of deze Hallo die VM is gemaakt</span><span class="sxs-lookup"><span data-stu-id="d28b0-180">Verify that hello VM was created</span></span>
<span data-ttu-id="d28b0-181">Wanneer voltooid, ziet u VM nieuw wordt gemaakt in Hallo Hallo [Azure-portal](https://portal.azure.com) onder **Bladeren** > **virtuele machines**, of met behulp van de volgende Hallo PowerShell-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="d28b0-181">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="d28b0-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d28b0-182">Next steps</span></span>
<span data-ttu-id="d28b0-183">toomanage uw nieuwe virtuele machine met Azure PowerShell, Zie [virtuele machines beheren met Azure Resource Manager en PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d28b0-183">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


