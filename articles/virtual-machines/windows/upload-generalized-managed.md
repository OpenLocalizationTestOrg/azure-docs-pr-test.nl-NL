---
title: een beheerde Azure-virtuele machine vanaf een VHD gegeneraliseerde lokale aaaCreate | Microsoft Docs
description: Uploaden van een gegeneraliseerde VHD tooAzure en gebruik deze toocreate nieuwe virtuele machines in Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a><span data-ttu-id="50bc4-103">Een gegeneraliseerde VHD uploaden en gebruik deze toocreate nieuwe virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="50bc4-103">Upload a generalized VHD and use it toocreate new VMs in Azure</span></span>

<span data-ttu-id="50bc4-104">In dit onderwerp leert u met behulp van PowerShell tooupload een VHD van een gegeneraliseerde VM tooAzure, een installatiekopie van Hallo VHD maken en een nieuwe virtuele machine maken vanuit die installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="50bc4-104">This topic walks you through using PowerShell tooupload a VHD of a generalized VM tooAzure, create an image from hello VHD and create a new VM from that image.</span></span> <span data-ttu-id="50bc4-105">U kunt een VHD die is geëxporteerd vanuit een hulpprogramma voor het virtualisatie lokale of vanuit een andere cloud uploaden.</span><span class="sxs-lookup"><span data-stu-id="50bc4-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="50bc4-106">Met behulp van [schijven beheerd](managed-disks-overview.md) voor Hallo nieuwe virtuele machine vereenvoudigt het beheer van Hallo-VM en zorgt voor betere beschikbaarheid als Hallo VM wordt geplaatst in een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="50bc4-106">Using [Managed Disks](managed-disks-overview.md) for hello new VM simplifies hello VM managment and provides better availability when hello VM is placed in an availability set.</span></span> 

<span data-ttu-id="50bc4-107">Als u een voorbeeldscript toouse wilt, Zie [Sample script tooupload een VHD-tooAzure en maak een nieuwe virtuele machine](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="50bc4-107">If you want toouse a sample script, see [Sample script tooupload a VHD tooAzure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="50bc4-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="50bc4-108">Before you begin</span></span>

- <span data-ttu-id="50bc4-109">Voordat u een VHD-tooAzure uploadt, u moet volgen [voorbereiden van een Windows-VHD of VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="50bc4-109">Before uploading any VHD tooAzure, you should follow [Prepare a Windows VHD or VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="50bc4-110">Bekijk [Hallo-migratie plannen tooManaged schijven](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) voordat u uw migratie te[schijven beheerd](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="50bc4-110">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration too[Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="50bc4-111">Zorg ervoor dat u beschikt over de nieuwste versie van de Hallo Hallo AzureRM.Compute PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="50bc4-111">Make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="50bc4-112">Voer Hallo na de opdracht tooinstall deze.</span><span class="sxs-lookup"><span data-stu-id="50bc4-112">Run hello following command tooinstall it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="50bc4-113">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="50bc4-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="50bc4-114">Generalize Hallo van virtuele machine van Windows met behulp van Sysprep</span><span class="sxs-lookup"><span data-stu-id="50bc4-114">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="50bc4-115">Sysprep verwijdert alle persoonlijke gegevens over uw account, onder andere en bereidt Hallo machine toobe gebruikt als een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="50bc4-115">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="50bc4-116">Zie voor meer informatie over Sysprep [hoe tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="50bc4-116">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="50bc4-117">Zorg ervoor dat het Hallo-serverfuncties op Hallo machine worden ondersteund door Sysprep.</span><span class="sxs-lookup"><span data-stu-id="50bc4-117">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="50bc4-118">Zie voor meer informatie [Sysprep-ondersteuning voor serverfuncties](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="50bc4-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50bc4-119">Als u Sysprep voordat u uploadt uw VHD tooAzure voor Hallo eerst uitvoert, controleert u of u hebt [uw virtuele machine voorbereid](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat Sysprep wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="50bc4-119">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="50bc4-120">Meld u aan toohello virtuele Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="50bc4-120">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="50bc4-121">Hallo-opdrachtpromptvenster open als beheerder.</span><span class="sxs-lookup"><span data-stu-id="50bc4-121">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="50bc4-122">Hallo directory ook wijzigen**%windir%\system32\sysprep**, en voer vervolgens `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="50bc4-122">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="50bc4-123">In Hallo **hulpprogramma voor systeemvoorbereiding** dialoogvenster, **System Voer Out-of-Box Experience (OOBE)**, en zorg ervoor dat Hallo **Generalize** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="50bc4-123">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="50bc4-124">In **afsluitopties**, selecteer **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="50bc4-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="50bc4-125">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="50bc4-125">Click **OK**.</span></span>
   
    ![Sysprep starten](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="50bc4-127">Wanneer Sysprep is voltooid, afgesloten Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="50bc4-127">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="50bc4-128">Hallo VM niet opnieuw.</span><span class="sxs-lookup"><span data-stu-id="50bc4-128">Do not restart hello VM.</span></span>



## <a name="log-in-tooazure"></a><span data-ttu-id="50bc4-129">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="50bc4-129">Log in tooAzure</span></span>
<span data-ttu-id="50bc4-130">Als er geen PowerShell-versie 1.4 al of hoger is geïnstalleerd, lezen [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="50bc4-130">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="50bc4-131">Open Azure PowerShell en meld tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="50bc4-131">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="50bc4-132">Een pop-upvenster wordt geopend voor tooenter u de referenties van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="50bc4-132">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="50bc4-133">Hallo abonnement-id's voor uw beschikbare abonnementen ophalen.</span><span class="sxs-lookup"><span data-stu-id="50bc4-133">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="50bc4-134">Set Hallo juiste abonnement Hallo abonnement-id.</span><span class="sxs-lookup"><span data-stu-id="50bc4-134">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="50bc4-135">Vervang  *<subscriptionID>*  corrigeren abonnement met de Hallo Hallo-ID.</span><span class="sxs-lookup"><span data-stu-id="50bc4-135">Replace *<subscriptionID>* with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a><span data-ttu-id="50bc4-136">Hallo storage-account ophalen</span><span class="sxs-lookup"><span data-stu-id="50bc4-136">Get hello storage account</span></span>
<span data-ttu-id="50bc4-137">U moet een opslagaccount in Azure toostore Hallo geüpload VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="50bc4-137">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="50bc4-138">U kunt een bestaand opslagaccount gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="50bc4-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="50bc4-139">Als u Hallo VHD toocreate een beheerde schijf voor een virtuele machine gebruikt, moet Hallo opslagaccountlocatie dezelfde Hallo locatie waar u Hallo VM maakt.</span><span class="sxs-lookup"><span data-stu-id="50bc4-139">If you will be using hello VHD toocreate a managed disk for a VM, hello storage account location must be same hello location where you will be creating hello VM.</span></span>

<span data-ttu-id="50bc4-140">tooshow hello beschikbaar storage-accounts, typt u:</span><span class="sxs-lookup"><span data-stu-id="50bc4-140">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="50bc4-141">Als u een bestaand opslagaccount toouse wilt, gaat u verder toohello [Hallo VM-installatiekopie uploaden](#upload-the-vm-vhd-to-your-storage-account) sectie.</span><span class="sxs-lookup"><span data-stu-id="50bc4-141">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="50bc4-142">Als u een opslagaccount toocreate moet, volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="50bc4-142">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="50bc4-143">U moet Hallo-naam van resourcegroep Hallo waar Hallo storage-account moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50bc4-143">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="50bc4-144">toofind uit alle Hallo resourcegroepen in uw abonnement, type:</span><span class="sxs-lookup"><span data-stu-id="50bc4-144">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="50bc4-145">een resourcegroep met de naam toocreate **myResourceGroup** in Hallo **VS-Oost** regio, type:</span><span class="sxs-lookup"><span data-stu-id="50bc4-145">toocreate a resource group named **myResourceGroup** in hello **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="50bc4-146">Maken van een opslagaccount met de naam **mystorageaccount** in deze resourcegroep via Hallo [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="50bc4-146">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="50bc4-147">Geldige waarden voor - SkuName zijn:</span><span class="sxs-lookup"><span data-stu-id="50bc4-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="50bc4-148">**Standard_LRS** -lokaal redundante opslag.</span><span class="sxs-lookup"><span data-stu-id="50bc4-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="50bc4-149">**Standard_ZRS** -Zone-redundante opslag.</span><span class="sxs-lookup"><span data-stu-id="50bc4-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="50bc4-150">**Standard_GRS** -geografisch redundante opslag.</span><span class="sxs-lookup"><span data-stu-id="50bc4-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="50bc4-151">**Standard_RAGRS** -geografisch redundante opslag met leestoegang.</span><span class="sxs-lookup"><span data-stu-id="50bc4-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="50bc4-152">**Premium_LRS** -Premium lokaal redundante opslag.</span><span class="sxs-lookup"><span data-stu-id="50bc4-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="50bc4-153">Hallo VHD tooyour storage-account uploaden</span><span class="sxs-lookup"><span data-stu-id="50bc4-153">Upload hello VHD tooyour storage account</span></span>

<span data-ttu-id="50bc4-154">Gebruik Hallo [toevoegen AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet tooupload Hallo VHD tooa container in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="50bc4-154">Use hello [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="50bc4-155">In dit voorbeeld uploads Hallo bestand *myVHD.vhd* van *' C:\Users\Public\Documents\Virtual harde schijven\"*  tooa opslagaccount met de naam *mystorageaccount*in Hallo *myResourceGroup* resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="50bc4-155">This example uploads hello file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="50bc4-156">Hallo-bestand worden opgenomen in het Hallo-container met de naam *mycontainer* en worden nieuwe bestandsnaam Hallo *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="50bc4-156">hello file will be placed into hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="50bc4-157">Als dit lukt, kunt u een antwoord dat vergelijkbare toothis lijkt krijgen:</span><span class="sxs-lookup"><span data-stu-id="50bc4-157">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="50bc4-158">Afhankelijk van uw netwerkverbinding en het Hallo-grootte van het VHD-bestand met deze opdracht kan een tijdje duren toocomplete</span><span class="sxs-lookup"><span data-stu-id="50bc4-158">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

<span data-ttu-id="50bc4-159">Hallo opslaan **bestemmings-URI** pad toouse later als u een beheerde schijf toocreate gaat of een nieuwe virtuele machine met behulp van Hallo VHD geüpload.</span><span class="sxs-lookup"><span data-stu-id="50bc4-159">Save hello **Destination URI** path toouse later if you are going toocreate a managed disk or a new VM using hello uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="50bc4-160">Andere opties voor het uploaden van een VHD</span><span class="sxs-lookup"><span data-stu-id="50bc4-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="50bc4-161">U kunt ook een VHD tooyour storage-account met behulp van een van de volgende Hallo uploaden:</span><span class="sxs-lookup"><span data-stu-id="50bc4-161">You can also upload a VHD tooyour storage account using one of hello following:</span></span>

- [<span data-ttu-id="50bc4-162">AzCopy</span><span class="sxs-lookup"><span data-stu-id="50bc4-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="50bc4-163">API voor Azure Storage kopiëren-Blob</span><span class="sxs-lookup"><span data-stu-id="50bc4-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="50bc4-164">Azure Storage Explorer uploaden van BLOB 's</span><span class="sxs-lookup"><span data-stu-id="50bc4-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="50bc4-165">Opslag voor importeren/exporteren Service REST API-verwijzing</span><span class="sxs-lookup"><span data-stu-id="50bc4-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="50bc4-166">U kunt het beste Import/Export-Service gebruikt als de geschatte tijd uploaden is langer dan zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="50bc4-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="50bc4-167">U kunt [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate Hallo tijd van de grootte en de overdracht van gegevenseenheid.</span><span class="sxs-lookup"><span data-stu-id="50bc4-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span> 
    <span data-ttu-id="50bc4-168">Import/Export kan worden gebruikt toocopy tooa standard-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="50bc4-168">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="50bc4-169">U moet toocopy van standaardopslag toopremium storage-account met behulp van een hulpprogramma zoals AzCopy.</span><span class="sxs-lookup"><span data-stu-id="50bc4-169">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a><span data-ttu-id="50bc4-170">Maak een beheerde afbeelding van Hallo VHD geüpload</span><span class="sxs-lookup"><span data-stu-id="50bc4-170">Create a managed image from hello uploaded VHD</span></span> 

<span data-ttu-id="50bc4-171">Maak een begeleide afbeelding met behulp van uw algemene besturingssysteem-VHD.</span><span class="sxs-lookup"><span data-stu-id="50bc4-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="50bc4-172">Hallo waarden vervangt door uw eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="50bc4-172">Replace hello values with your own information.</span></span>


1.  <span data-ttu-id="50bc4-173">Stel eerst Hallo algemene parameters:</span><span class="sxs-lookup"><span data-stu-id="50bc4-173">First, set hello common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="50bc4-174">Hallo-installatiekopie met behulp van uw algemene besturingssysteem-VHD maken.</span><span class="sxs-lookup"><span data-stu-id="50bc4-174">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="50bc4-175">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="50bc4-175">Create a virtual network</span></span>
<span data-ttu-id="50bc4-176">Hallo vNet en subnet Hallo maken [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="50bc4-176">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="50bc4-177">Hallo subnet maken.</span><span class="sxs-lookup"><span data-stu-id="50bc4-177">Create hello subnet.</span></span> <span data-ttu-id="50bc4-178">In dit voorbeeld wordt een subnet met de naam *mySubnet* met het Hallo-adresvoorvoegsel van *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="50bc4-178">This example creates a subnet named *mySubnet* with hello address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="50bc4-179">Hallo virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="50bc4-179">Create hello virtual network.</span></span> <span data-ttu-id="50bc4-180">In dit voorbeeld wordt een virtueel netwerk met de naam *myVnet* met het Hallo-adresvoorvoegsel van *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="50bc4-180">This example creates a virtual network named *myVnet* with hello address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="50bc4-181">Een openbaar IP-adres en een netwerkinterface maken</span><span class="sxs-lookup"><span data-stu-id="50bc4-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="50bc4-182">tooenable communicatie met Hallo virtuele machine in het virtuele netwerk hello, moet u een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) en een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="50bc4-182">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="50bc4-183">Een openbaar IP-adres maken.</span><span class="sxs-lookup"><span data-stu-id="50bc4-183">Create a public IP address.</span></span> <span data-ttu-id="50bc4-184">In dit voorbeeld wordt een openbaar IP-adres met de naam *myPip*.</span><span class="sxs-lookup"><span data-stu-id="50bc4-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="50bc4-185">Hallo NIC. maken</span><span class="sxs-lookup"><span data-stu-id="50bc4-185">Create hello NIC.</span></span> <span data-ttu-id="50bc4-186">In dit voorbeeld wordt een NIC met de naam **myNic**.</span><span class="sxs-lookup"><span data-stu-id="50bc4-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="50bc4-187">Netwerkbeveiligingsgroep hello en een RDP-regel maken</span><span class="sxs-lookup"><span data-stu-id="50bc4-187">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="50bc4-188">toobe kunnen toolog in tooyour VM met RDP, moet u toohave een netwerkbeveiligingsregel (NSG) waarmee op poort 3389 van RDP-toegang.</span><span class="sxs-lookup"><span data-stu-id="50bc4-188">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="50bc4-189">In dit voorbeeld maakt u een NSG met de naam *myNsg* die een regel aangeroepen bevat *myRdpRule* waarmee RDP-verkeer via poort 3389.</span><span class="sxs-lookup"><span data-stu-id="50bc4-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="50bc4-190">Zie voor meer informatie over Nsg [openen van poorten tooa VM in Azure met behulp van PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="50bc4-190">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="50bc4-191">Een variabele voor Hallo virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="50bc4-191">Create a variable for hello virtual network</span></span>

<span data-ttu-id="50bc4-192">Maak een variabele voor het virtuele netwerk Hallo voltooid.</span><span class="sxs-lookup"><span data-stu-id="50bc4-192">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="50bc4-193">Hallo-referenties voor Hallo VM ophalen</span><span class="sxs-lookup"><span data-stu-id="50bc4-193">Get hello credentials for hello VM</span></span>

<span data-ttu-id="50bc4-194">Hallo wordt volgende cmdlet een venster geopend waarin u een nieuwe gebruiker-naam en het wachtwoord toouse Hallo lokale administrator-account wordt invoeren voor toegang op afstand tot Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="50bc4-194">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a><span data-ttu-id="50bc4-195">Hallo VM-naam en de grootte van toohello VM-configuratie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="50bc4-195">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="50bc4-196">Set Hallo VM-installatiekopie als bronafbeelding voor Hallo nieuwe virtuele machine</span><span class="sxs-lookup"><span data-stu-id="50bc4-196">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="50bc4-197">Stel broninstallatiekopie Hallo Hallo-id van VM-installatiekopie Hallo beheerd.</span><span class="sxs-lookup"><span data-stu-id="50bc4-197">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="50bc4-198">Configuratie van het besturingssysteem Hallo en toevoegen van Hallo NIC.</span><span class="sxs-lookup"><span data-stu-id="50bc4-198">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="50bc4-199">Hallo opslagtype (PremiumLRS of StandardLRS) en het Hallo-grootte van de besturingssysteemschijf Hallo invoeren.</span><span class="sxs-lookup"><span data-stu-id="50bc4-199">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="50bc4-200">In dit voorbeeld wordt het accounttype hello te*PremiumLRS*, schijfgrootte te Hallo*128 GB* en schijfcache te*ReadWrite*.</span><span class="sxs-lookup"><span data-stu-id="50bc4-200">This example sets hello account type too*PremiumLRS*, hello disk size too*128 GB* and disk caching too*ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="50bc4-201">Hallo VM maken</span><span class="sxs-lookup"><span data-stu-id="50bc4-201">Create hello VM</span></span>

<span data-ttu-id="50bc4-202">Maken van nieuwe virtuele machine met behulp van Hallo-configuratie is opgeslagen in Hallo Hallo **$vm** variabele.</span><span class="sxs-lookup"><span data-stu-id="50bc4-202">Create hello new VM using hello configuration stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="50bc4-203">Controleer of deze Hallo die VM is gemaakt</span><span class="sxs-lookup"><span data-stu-id="50bc4-203">Verify that hello VM was created</span></span>
<span data-ttu-id="50bc4-204">Wanneer voltooid, ziet u VM nieuw wordt gemaakt in Hallo Hallo [Azure-portal](https://portal.azure.com) onder **Bladeren** > **virtuele machines**, of met behulp van de volgende Hallo PowerShell-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="50bc4-204">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="50bc4-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="50bc4-205">Next steps</span></span>

<span data-ttu-id="50bc4-206">toosign in tooyour nieuwe virtuele machine, bladeren toohello VM in Hallo [portal](https://portal.azure.com), klikt u op **Connect**, en open Hallo Remote Desktop RDP-bestand.</span><span class="sxs-lookup"><span data-stu-id="50bc4-206">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="50bc4-207">Gebruik de accountreferenties op Hallo van uw oorspronkelijke toosign van de virtuele machine in tooyour nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="50bc4-207">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="50bc4-208">Zie voor meer informatie [hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="50bc4-208">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

