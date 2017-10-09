---
title: aaaCreate een begeleide afbeelding in Azure | Microsoft Docs
description: "Maak een begeleide afbeelding van een gegeneraliseerde virtuele machine of VHD in Azure. Installatiekopieën van het gebruikte toocreate meerdere virtuele machines die gebruikmaken van beheerde schijven kan worden."
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
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="8e074-104">Maken van een begeleide afbeelding van een gegeneraliseerde virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="8e074-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="8e074-105">Een beheerde Afbeeldingsbron kan worden gemaakt vanuit een gegeneraliseerde virtuele machine die wordt opgeslagen als een beheerde schijf of een niet-beheerde schijf in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8e074-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="8e074-106">Hallo installatiekopie kan vervolgens worden de gebruikte toocreate meerdere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8e074-106">hello image can then be used toocreate multiple VMs.</span></span> 


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="8e074-107">Generalize Hallo van virtuele machine van Windows met behulp van Sysprep</span><span class="sxs-lookup"><span data-stu-id="8e074-107">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="8e074-108">Sysprep verwijdert alle persoonlijke gegevens over uw account, onder andere en bereidt Hallo machine toobe gebruikt als een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="8e074-108">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="8e074-109">Zie voor meer informatie over Sysprep [hoe tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e074-109">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="8e074-110">Zorg ervoor dat het Hallo-serverfuncties op Hallo machine worden ondersteund door Sysprep.</span><span class="sxs-lookup"><span data-stu-id="8e074-110">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="8e074-111">Zie voor meer informatie [Sysprep-ondersteuning voor serverfuncties](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="8e074-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e074-112">Als u Sysprep voordat u uploadt uw VHD tooAzure voor Hallo eerst uitvoert, controleert u of u hebt [uw virtuele machine voorbereid](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat Sysprep wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8e074-112">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="8e074-113">Meld u aan toohello virtuele Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="8e074-113">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="8e074-114">Hallo-opdrachtpromptvenster open als beheerder.</span><span class="sxs-lookup"><span data-stu-id="8e074-114">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="8e074-115">Hallo directory ook wijzigen**%windir%\system32\sysprep**, en voer vervolgens `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="8e074-115">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="8e074-116">In Hallo **hulpprogramma voor systeemvoorbereiding** dialoogvenster, **System Voer Out-of-Box Experience (OOBE)**, en zorg ervoor dat Hallo **Generalize** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8e074-116">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="8e074-117">In **afsluitopties**, selecteer **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="8e074-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="8e074-118">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e074-118">Click **OK**.</span></span>
   
    ![Sysprep starten](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="8e074-120">Wanneer Sysprep is voltooid, afgesloten Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8e074-120">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="8e074-121">Hallo VM niet opnieuw.</span><span class="sxs-lookup"><span data-stu-id="8e074-121">Do not restart hello VM.</span></span>


## <a name="create-a-managed-image-in-hello-portal"></a><span data-ttu-id="8e074-122">Maken van een begeleide afbeelding in Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="8e074-122">Create a managed image in hello portal</span></span> 

1. <span data-ttu-id="8e074-123">Open Hallo [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8e074-123">Open hello [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8e074-124">Klik op Hallo plusteken toocreate een nieuwe resource.</span><span class="sxs-lookup"><span data-stu-id="8e074-124">Click hello plus sign toocreate a new resource.</span></span>
3. <span data-ttu-id="8e074-125">Typ in Hallo filter zoeken **installatiekopie**.</span><span class="sxs-lookup"><span data-stu-id="8e074-125">In hello filter search, type **Image**.</span></span>
4. <span data-ttu-id="8e074-126">Selecteer **installatiekopie** uit Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="8e074-126">Select **Image** from hello results.</span></span>
5. <span data-ttu-id="8e074-127">In Hallo **installatiekopie** blade, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="8e074-127">In hello **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="8e074-128">In **naam**, typ een naam voor het Hallo-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="8e074-128">In **Name**, type a name for hello image.</span></span>
7. <span data-ttu-id="8e074-129">Als u meer dan één abonnement hebt, selecteer juiste paneel van Hallo Hallo **abonnement** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="8e074-129">If you have more than one subscription, select hello correct one from hello **Subscription** drop-down.</span></span>
7. <span data-ttu-id="8e074-130">In **resourcegroep** select **nieuw** en typ een naam in of selecteer **uit bestaande** en selecteert u een groep resource toouse in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e074-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group toouse from hello drop-down list.</span></span>
8. <span data-ttu-id="8e074-131">In **locatie**, kies Hallo-locatie van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8e074-131">In **Location**, choose hello location of your resource group.</span></span>
9. <span data-ttu-id="8e074-132">In **type besturingssysteem** Hallo-type van Windows of Linux-besturingssysteem selecteert.</span><span class="sxs-lookup"><span data-stu-id="8e074-132">In **OS type** select hello type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="8e074-133">In **Storage-blob**, klikt u op **Bladeren** toolook voor Hallo VHD in uw Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="8e074-133">In **Storage blob**, click **Browse** toolook for hello VHD in your Azure storage.</span></span>
12. <span data-ttu-id="8e074-134">In **accounttype** Standard_LRS of Premium_LRS kiezen.</span><span class="sxs-lookup"><span data-stu-id="8e074-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="8e074-135">Standaard harde schijven en Premium SSD-schijven gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e074-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="8e074-136">Beide lokaal redundante opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8e074-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="8e074-137">In **schijfcache** Selecteer Hallo geschikte schijf opslaan in cache optie.</span><span class="sxs-lookup"><span data-stu-id="8e074-137">In **Disk caching** select hello appropriate disk caching option.</span></span> <span data-ttu-id="8e074-138">Hallo-opties zijn **geen**, **alleen-lezen** en **alleen-lezen**.</span><span class="sxs-lookup"><span data-stu-id="8e074-138">hello options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="8e074-139">Optioneel: U kunt ook een bestaande gegevens schijf toohello afbeelding toevoegen door te klikken op **+ gegevensschijf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8e074-139">Optional: You can also add an existing data disk toohello image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="8e074-140">Wanneer u klaar bent u deze hebt geselecteerd, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="8e074-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="8e074-141">Nadat het Hallo-installatiekopie is gemaakt, ziet u dit als een **installatiekopie** resource in Hallo lijst met resources in Hallo-resourcegroep die u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="8e074-141">After hello image is created, you will see it as an **Image** resource in hello list of resources in hello resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="8e074-142">Maken van een begeleide afbeelding van een virtuele machine met behulp van Powershell</span><span class="sxs-lookup"><span data-stu-id="8e074-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="8e074-143">Het maken van een installatiekopie van een rechtstreeks vanuit Hallo die VM zorgt ervoor dat Hallo-installatiekopie bevat alle Hallo schijven die zijn gekoppeld aan virtuele machine, met inbegrip van Hallo Besturingssysteemschijf en alle gegevensschijven Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e074-143">Creating an image directly from hello VM ensures that hello image includes all of hello disks associated with hello VM, including hello OS Disk and any data disks.</span></span>


<span data-ttu-id="8e074-144">Voordat u begint, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt.</span><span class="sxs-lookup"><span data-stu-id="8e074-144">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="8e074-145">Voer Hallo na de opdracht tooinstall deze.</span><span class="sxs-lookup"><span data-stu-id="8e074-145">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="8e074-146">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8e074-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="8e074-147">Sommige variabelen maken.</span><span class="sxs-lookup"><span data-stu-id="8e074-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="8e074-148">Zorg ervoor dat Hallo die VM is opgeheven.</span><span class="sxs-lookup"><span data-stu-id="8e074-148">Make sure hello VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="8e074-149">Hallo-status van Hallo virtuele machine te instellen**gegeneraliseerd**.</span><span class="sxs-lookup"><span data-stu-id="8e074-149">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="8e074-150">Hallo virtuele machine worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="8e074-150">Get hello virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="8e074-151">Hallo imageconfiguratie maken.</span><span class="sxs-lookup"><span data-stu-id="8e074-151">Create hello image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="8e074-152">Hallo-installatiekopie kan maken.</span><span class="sxs-lookup"><span data-stu-id="8e074-152">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="8e074-153">Maken van een begeleide afbeelding van een VHD in PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e074-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="8e074-154">Maak een begeleide afbeelding met behulp van uw algemene besturingssysteem-VHD.</span><span class="sxs-lookup"><span data-stu-id="8e074-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="8e074-155">Stel eerst Hallo algemene parameters:</span><span class="sxs-lookup"><span data-stu-id="8e074-155">First, set hello common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="8e074-156">Step\deallocate hello VM.</span><span class="sxs-lookup"><span data-stu-id="8e074-156">Step\deallocate hello VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="8e074-157">Hallo VM zoals gegeneraliseerd markeren.</span><span class="sxs-lookup"><span data-stu-id="8e074-157">Mark hello VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="8e074-158">Hallo-installatiekopie met behulp van uw algemene besturingssysteem-VHD maken.</span><span class="sxs-lookup"><span data-stu-id="8e074-158">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="8e074-159">Een begeleide afbeelding maken vanuit een momentopname met behulp van Powershell</span><span class="sxs-lookup"><span data-stu-id="8e074-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="8e074-160">U kunt ook een begeleide afbeelding maken vanuit een momentopname van Hallo VHD van een gegeneraliseerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8e074-160">You can also create a managed image from a snapshot of hello VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="8e074-161">Sommige variabelen maken.</span><span class="sxs-lookup"><span data-stu-id="8e074-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="8e074-162">Hallo-momentopname ophalen.</span><span class="sxs-lookup"><span data-stu-id="8e074-162">Get hello snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="8e074-163">Hallo imageconfiguratie maken.</span><span class="sxs-lookup"><span data-stu-id="8e074-163">Create hello image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="8e074-164">Hallo-installatiekopie kan maken.</span><span class="sxs-lookup"><span data-stu-id="8e074-164">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="8e074-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8e074-165">Next steps</span></span>
- <span data-ttu-id="8e074-166">Nu u kunt [een virtuele machine maken van Hallo gegeneraliseerd begeleide afbeelding](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8e074-166">Now you can [create a VM from hello generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>    

