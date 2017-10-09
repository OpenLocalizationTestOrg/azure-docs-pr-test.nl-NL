---
title: een VHD generalize toocreate aaaUpload meerdere virtuele machines in Azure | Microsoft Docs
description: Upload een gegeneraliseerde VHD tooan Azure storage-account toocreate een virtuele machine van Windows-toouse met Hallo Resource Manager-implementatiemodel.
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
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a><span data-ttu-id="aed1c-103">Uploaden van een gegeneraliseerde VHD tooAzure toocreate een nieuwe virtuele machine</span><span class="sxs-lookup"><span data-stu-id="aed1c-103">Upload a generalized VHD tooAzure toocreate a new VM</span></span>

<span data-ttu-id="aed1c-104">In dit onderwerp bevat informatie over het uploaden van een gegeneraliseerde onbeheerde schijf tooa storage-account en maak vervolgens een nieuwe virtuele machine met Hallo geüpload schijf.</span><span class="sxs-lookup"><span data-stu-id="aed1c-104">This topic covers uploading a generalized unmanaged disk tooa storage account and then creating a new VM using hello uploaded disk.</span></span> <span data-ttu-id="aed1c-105">Een algemene VHD-installatiekopie heeft al uw persoonlijke accountgegevens verwijderd met behulp van Sysprep.</span><span class="sxs-lookup"><span data-stu-id="aed1c-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="aed1c-106">Als u een virtuele machine vanaf een speciale VHD in een opslagaccount toocreate wilt, Zie [een virtuele machine maken vanaf een speciale VHD](sa-create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="aed1c-106">If you want toocreate a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="aed1c-107">In dit onderwerp worden met behulp van storage-accounts, maar we raden klanten toousing beheerd schijven in plaats daarvan verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="aed1c-107">This topic covers using storage accounts, but we recommend customers move toousing Managed Disks instead.</span></span> <span data-ttu-id="aed1c-108">Zie voor een volledig overzicht van hoe tooprepare, uploaden en maak een nieuwe virtuele machine met schijven die worden beheerd, [Maak een nieuwe virtuele machine uit een gegeneraliseerde VHD geüpload tooAzure schijven beheerd](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="aed1c-108">For a complete walk-through of how tooprepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded tooAzure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-hello-vm"></a><span data-ttu-id="aed1c-109">Hallo VM voorbereiden</span><span class="sxs-lookup"><span data-stu-id="aed1c-109">Prepare hello VM</span></span>

<span data-ttu-id="aed1c-110">Een gegeneraliseerde VHD heeft al uw persoonlijke accountgegevens verwijderd met behulp van Sysprep.</span><span class="sxs-lookup"><span data-stu-id="aed1c-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="aed1c-111">Als u van plan toouse Hallo VHD als een installatiekopie toocreate bent nieuwe virtuele machines van moet:</span><span class="sxs-lookup"><span data-stu-id="aed1c-111">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span>
  
  * <span data-ttu-id="aed1c-112">[Voorbereiden van een Windows-VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="aed1c-112">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="aed1c-113">Hallo virtuele machine met behulp van Sysprep generalize</span><span class="sxs-lookup"><span data-stu-id="aed1c-113">Generalize hello virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="aed1c-114">Een virtuele Windows-machine met behulp van Sysprep generalize</span><span class="sxs-lookup"><span data-stu-id="aed1c-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="aed1c-115">Deze sectie leest u hoe toogeneralize uw Windows-machine voor gebruik als een afbeelding.</span><span class="sxs-lookup"><span data-stu-id="aed1c-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="aed1c-116">Sysprep verwijdert alle persoonlijke gegevens over uw account, onder andere en bereidt Hallo machine toobe gebruikt als een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="aed1c-116">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="aed1c-117">Zie voor meer informatie over Sysprep [hoe tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="aed1c-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="aed1c-118">Zorg ervoor dat het Hallo-serverfuncties op Hallo machine worden ondersteund door Sysprep.</span><span class="sxs-lookup"><span data-stu-id="aed1c-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="aed1c-119">Zie voor meer informatie [Sysprep-ondersteuning voor serverfuncties](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="aed1c-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aed1c-120">Als u Sysprep voordat u uploadt uw VHD tooAzure voor Hallo eerst uitvoert, controleert u of u hebt [uw virtuele machine voorbereid](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat Sysprep wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aed1c-120">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="aed1c-121">Meld u aan toohello virtuele Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="aed1c-121">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="aed1c-122">Hallo-opdrachtpromptvenster open als beheerder.</span><span class="sxs-lookup"><span data-stu-id="aed1c-122">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="aed1c-123">Hallo directory ook wijzigen**%windir%\system32\sysprep**, en voer vervolgens `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="aed1c-123">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="aed1c-124">In Hallo **hulpprogramma voor systeemvoorbereiding** dialoogvenster, **System Voer Out-of-Box Experience (OOBE)**, en zorg ervoor dat Hallo **Generalize** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="aed1c-124">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="aed1c-125">In **afsluitopties**, selecteer **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="aed1c-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="aed1c-126">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="aed1c-126">Click **OK**.</span></span>
   
    ![Sysprep starten](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="aed1c-128">Wanneer Sysprep is voltooid, afgesloten Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="aed1c-128">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="aed1c-129">Hallo VM niet opnieuw opstarten nadat u bent gereed uploaden Hallo VHD tooAzure of maken van een afbeelding van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="aed1c-129">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="aed1c-130">Als Hallo VM per ongeluk opnieuw opgestart wordt, voert u Sysprep toogeneralize deze opnieuw.</span><span class="sxs-lookup"><span data-stu-id="aed1c-130">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 


## <a name="upload-hello-vhd"></a><span data-ttu-id="aed1c-131">Hallo VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="aed1c-131">Upload hello VHD</span></span>

<span data-ttu-id="aed1c-132">Hallo VHD tooan Azure storage-account uploaden.</span><span class="sxs-lookup"><span data-stu-id="aed1c-132">Upload hello VHD tooan Azure storage account.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="aed1c-133">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="aed1c-133">Log in tooAzure</span></span>
<span data-ttu-id="aed1c-134">Als er geen PowerShell-versie 1.4 al of hoger is geïnstalleerd, lezen [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aed1c-134">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="aed1c-135">Open Azure PowerShell en meld tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="aed1c-135">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="aed1c-136">Een pop-upvenster wordt geopend voor tooenter u de referenties van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="aed1c-136">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="aed1c-137">Hallo abonnement-id's voor uw beschikbare abonnementen ophalen.</span><span class="sxs-lookup"><span data-stu-id="aed1c-137">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="aed1c-138">Set Hallo juiste abonnement Hallo abonnement-id.</span><span class="sxs-lookup"><span data-stu-id="aed1c-138">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="aed1c-139">Vervang `<subscriptionID>` corrigeren abonnement met de Hallo Hallo-ID.</span><span class="sxs-lookup"><span data-stu-id="aed1c-139">Replace `<subscriptionID>` with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a><span data-ttu-id="aed1c-140">Hallo storage-account ophalen</span><span class="sxs-lookup"><span data-stu-id="aed1c-140">Get hello storage account</span></span>
<span data-ttu-id="aed1c-141">U moet een opslagaccount in Azure toostore Hallo geüpload VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="aed1c-141">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="aed1c-142">U kunt een bestaand opslagaccount gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="aed1c-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="aed1c-143">tooshow hello beschikbaar storage-accounts, typt u:</span><span class="sxs-lookup"><span data-stu-id="aed1c-143">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="aed1c-144">Als u een bestaand opslagaccount toouse wilt, gaat u verder toohello [Hallo VM-installatiekopie uploaden](#upload-the-vm-vhd-to-your-storage-account) sectie.</span><span class="sxs-lookup"><span data-stu-id="aed1c-144">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="aed1c-145">Als u een opslagaccount toocreate moet, volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="aed1c-145">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="aed1c-146">U moet Hallo-naam van resourcegroep Hallo waar Hallo storage-account moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aed1c-146">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="aed1c-147">toofind uit alle Hallo resourcegroepen in uw abonnement, type:</span><span class="sxs-lookup"><span data-stu-id="aed1c-147">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="aed1c-148">een resourcegroep met de naam toocreate **myResourceGroup** in Hallo **VS-West** regio, type:</span><span class="sxs-lookup"><span data-stu-id="aed1c-148">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="aed1c-149">Maken van een opslagaccount met de naam **mystorageaccount** in deze resourcegroep via Hallo [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="aed1c-149">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a><span data-ttu-id="aed1c-150">Hallo uploaden starten</span><span class="sxs-lookup"><span data-stu-id="aed1c-150">Start hello upload</span></span> 

<span data-ttu-id="aed1c-151">Gebruik Hallo [toevoegen AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload Hallo installatiekopie tooa container in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="aed1c-151">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="aed1c-152">In dit voorbeeld uploads Hallo bestand **myVHD.vhd** van `"C:\Users\Public\Documents\Virtual hard disks\"` tooa opslagaccount met de naam **mystorageaccount** in Hallo **myResourceGroup** resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="aed1c-152">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="aed1c-153">Hallo-bestand worden opgenomen in het Hallo-container met de naam **mycontainer** en worden nieuwe bestandsnaam Hallo **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="aed1c-153">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="aed1c-154">Als dit lukt, kunt u een antwoord dat vergelijkbare toothis lijkt krijgen:</span><span class="sxs-lookup"><span data-stu-id="aed1c-154">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="aed1c-155">Afhankelijk van uw netwerkverbinding en het Hallo-grootte van het VHD-bestand met deze opdracht kan een tijdje duren toocomplete.</span><span class="sxs-lookup"><span data-stu-id="aed1c-155">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="aed1c-156">Een nieuwe virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="aed1c-156">Create a new VM</span></span> 

<span data-ttu-id="aed1c-157">U kunt nu gebruik Hallo geüpload VHD toocreate een nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="aed1c-157">You can now use hello uploaded VHD toocreate a new VM.</span></span> 

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="aed1c-158">Hallo-URI van Hallo VHD instellen</span><span class="sxs-lookup"><span data-stu-id="aed1c-158">Set hello URI of hello VHD</span></span>

<span data-ttu-id="aed1c-159">Hallo URI voor Hallo VHD toouse heeft Hallo indeling: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**VHD.</span><span class="sxs-lookup"><span data-stu-id="aed1c-159">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="aed1c-160">In dit voorbeeld Hallo VHD met de naam **myVHD** is in het opslagaccount hello **mystorageaccount** in Hallo container **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="aed1c-160">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="aed1c-161">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="aed1c-161">Create a virtual network</span></span>
<span data-ttu-id="aed1c-162">Hallo vNet en subnet Hallo maken [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aed1c-162">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="aed1c-163">Hallo subnet maken.</span><span class="sxs-lookup"><span data-stu-id="aed1c-163">Create hello subnet.</span></span> <span data-ttu-id="aed1c-164">Hallo volgende voorbeeld maakt u een subnet met de naam **mySubnet** in de resourcegroep Hallo **myResourceGroup** met het Hallo-adresvoorvoegsel van **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="aed1c-164">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="aed1c-165">Hallo virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="aed1c-165">Create hello virtual network.</span></span> <span data-ttu-id="aed1c-166">Hallo volgende voorbeeld maakt u een virtueel netwerk met de naam **myVnet** in Hallo **VS-West** locatie met het Hallo-adresvoorvoegsel van **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="aed1c-166">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="aed1c-167">Een openbaar IP-adres en een netwerkinterface maken</span><span class="sxs-lookup"><span data-stu-id="aed1c-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="aed1c-168">tooenable communicatie met Hallo virtuele machine in het virtuele netwerk hello, moet u een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) en een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="aed1c-168">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="aed1c-169">Een openbaar IP-adres maken.</span><span class="sxs-lookup"><span data-stu-id="aed1c-169">Create a public IP address.</span></span> <span data-ttu-id="aed1c-170">In dit voorbeeld wordt een openbaar IP-adres met de naam **myPip**.</span><span class="sxs-lookup"><span data-stu-id="aed1c-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="aed1c-171">Hallo NIC. maken</span><span class="sxs-lookup"><span data-stu-id="aed1c-171">Create hello NIC.</span></span> <span data-ttu-id="aed1c-172">In dit voorbeeld wordt een NIC met de naam **myNic**.</span><span class="sxs-lookup"><span data-stu-id="aed1c-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="aed1c-173">Netwerkbeveiligingsgroep hello en een RDP-regel maken</span><span class="sxs-lookup"><span data-stu-id="aed1c-173">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="aed1c-174">toobe kunnen toolog in tooyour VM met RDP, moet u een regel waarmee RDP-toegang op poort 3389 toohave.</span><span class="sxs-lookup"><span data-stu-id="aed1c-174">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="aed1c-175">In dit voorbeeld maakt u een NSG met de naam **myNsg** die een regel aangeroepen bevat **myRdpRule** waarmee RDP-verkeer via poort 3389.</span><span class="sxs-lookup"><span data-stu-id="aed1c-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="aed1c-176">Zie voor meer informatie over Nsg [openen van poorten tooa VM in Azure met behulp van PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aed1c-176">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="aed1c-177">Een variabele voor Hallo virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="aed1c-177">Create a variable for hello virtual network</span></span>
<span data-ttu-id="aed1c-178">Maak een variabele voor het virtuele netwerk Hallo voltooid.</span><span class="sxs-lookup"><span data-stu-id="aed1c-178">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="aed1c-179">Hallo VM maken</span><span class="sxs-lookup"><span data-stu-id="aed1c-179">Create hello VM</span></span>
<span data-ttu-id="aed1c-180">Hallo toont volgende PowerShell-script hoe tooset Hallo virtuele-machineconfiguraties en gebruik Hallo VM-installatiekopie als bron voor de nieuwe installatie Hallo Hallo geüpload.</span><span class="sxs-lookup"><span data-stu-id="aed1c-180">hello following PowerShell script shows how tooset up hello virtual machine configurations and use hello uploaded VM image as hello source for hello new installation.</span></span>



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

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="aed1c-181">Controleer of deze Hallo die VM is gemaakt</span><span class="sxs-lookup"><span data-stu-id="aed1c-181">Verify that hello VM was created</span></span>
<span data-ttu-id="aed1c-182">Wanneer voltooid, ziet u VM nieuw wordt gemaakt in Hallo Hallo [Azure-portal](https://portal.azure.com) onder **Bladeren** > **virtuele machines**, of met behulp van de volgende Hallo PowerShell-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="aed1c-182">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="aed1c-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aed1c-183">Next steps</span></span>
<span data-ttu-id="aed1c-184">toomanage uw nieuwe virtuele machine met Azure PowerShell, Zie [virtuele machines beheren met Azure Resource Manager en PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aed1c-184">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


