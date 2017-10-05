---
title: Een begeleide afbeelding maken in Azure | Microsoft Docs
description: Maak een begeleide afbeelding van een gegeneraliseerde virtuele machine of VHD in Azure. Afbeeldingen kunnen worden gebruikt voor het maken van meerdere virtuele machines die gebruikmaken van beheerde schijven.
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
ms.openlocfilehash: f64b81489ab426b50ec89af369e1581ac71848be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="463c7-104">Maken van een begeleide afbeelding van een gegeneraliseerde virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="463c7-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="463c7-105">Een beheerde Afbeeldingsbron kan worden gemaakt vanuit een gegeneraliseerde virtuele machine die wordt opgeslagen als een beheerde schijf of een niet-beheerde schijf in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="463c7-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="463c7-106">De installatiekopie kan vervolgens worden gebruikt voor het maken van meerdere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="463c7-106">The image can then be used to create multiple VMs.</span></span> 


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="463c7-107">De virtuele machine van Windows met behulp van Sysprep generalize</span><span class="sxs-lookup"><span data-stu-id="463c7-107">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="463c7-108">Sysprep verwijdert alle persoonlijke gegevens over uw account, onder andere en voorbereiden van de machine moet worden gebruikt als een afbeelding.</span><span class="sxs-lookup"><span data-stu-id="463c7-108">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="463c7-109">Zie voor meer informatie over Sysprep [hoe gebruik Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="463c7-109">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="463c7-110">Zorg ervoor dat de serverfuncties die op de computer uitgevoerd worden ondersteund door Sysprep.</span><span class="sxs-lookup"><span data-stu-id="463c7-110">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="463c7-111">Zie voor meer informatie [Sysprep-ondersteuning voor serverfuncties](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="463c7-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="463c7-112">Als u Sysprep voordat u uw VHD uploadt naar Azure voor het eerst uitvoert, controleert u of u hebt [uw virtuele machine voorbereid](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voordat Sysprep wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="463c7-112">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="463c7-113">Meld u aan de virtuele machine van Windows.</span><span class="sxs-lookup"><span data-stu-id="463c7-113">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="463c7-114">Open het venster opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="463c7-114">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="463c7-115">Wijzig de map in **%windir%\system32\sysprep**, en voer vervolgens `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="463c7-115">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="463c7-116">In de **hulpprogramma voor systeemvoorbereiding** dialoogvenster, **System Voer Out-of-Box Experience (OOBE)**, en zorg ervoor dat de **Generalize** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="463c7-116">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="463c7-117">In **afsluitopties**, selecteer **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="463c7-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="463c7-118">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="463c7-118">Click **OK**.</span></span>
   
    ![Sysprep starten](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="463c7-120">Wanneer Sysprep is voltooid, afgesloten de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="463c7-120">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="463c7-121">Start de virtuele machine niet opnieuw.</span><span class="sxs-lookup"><span data-stu-id="463c7-121">Do not restart the VM.</span></span>


## <a name="create-a-managed-image-in-the-portal"></a><span data-ttu-id="463c7-122">Een begeleide afbeelding maken in de portal</span><span class="sxs-lookup"><span data-stu-id="463c7-122">Create a managed image in the portal</span></span> 

1. <span data-ttu-id="463c7-123">Open de [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="463c7-123">Open the [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="463c7-124">Klik op het plusteken om een nieuwe resource te maken.</span><span class="sxs-lookup"><span data-stu-id="463c7-124">Click the plus sign to create a new resource.</span></span>
3. <span data-ttu-id="463c7-125">Typ in het zoeken filter **installatiekopie**.</span><span class="sxs-lookup"><span data-stu-id="463c7-125">In the filter search, type **Image**.</span></span>
4. <span data-ttu-id="463c7-126">Selecteer **installatiekopie** uit de resultaten.</span><span class="sxs-lookup"><span data-stu-id="463c7-126">Select **Image** from the results.</span></span>
5. <span data-ttu-id="463c7-127">In de **installatiekopie** blade, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="463c7-127">In the **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="463c7-128">In **naam**, typ een naam voor de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="463c7-128">In **Name**, type a name for the image.</span></span>
7. <span data-ttu-id="463c7-129">Als u meer dan één abonnement hebt, selecteert u de juiste versie van de **abonnement** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="463c7-129">If you have more than one subscription, select the correct one from the **Subscription** drop-down.</span></span>
7. <span data-ttu-id="463c7-130">In **resourcegroep** select **nieuw** en typ een naam in of selecteer **uit bestaande** en selecteer een resourcegroep te gebruiken uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="463c7-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group to use from the drop-down list.</span></span>
8. <span data-ttu-id="463c7-131">In **locatie**, kies de locatie van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="463c7-131">In **Location**, choose the location of your resource group.</span></span>
9. <span data-ttu-id="463c7-132">In **type besturingssysteem** Selecteer het type van Windows of Linux-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="463c7-132">In **OS type** select the type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="463c7-133">In **Storage-blob**, klikt u op **Bladeren** om te zoeken voor de VHD in uw Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="463c7-133">In **Storage blob**, click **Browse** to look for the VHD in your Azure storage.</span></span>
12. <span data-ttu-id="463c7-134">In **accounttype** Standard_LRS of Premium_LRS kiezen.</span><span class="sxs-lookup"><span data-stu-id="463c7-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="463c7-135">Standaard harde schijven en Premium SSD-schijven gebruikt.</span><span class="sxs-lookup"><span data-stu-id="463c7-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="463c7-136">Beide lokaal redundante opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="463c7-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="463c7-137">In **schijfcache** selecteert u de juiste optie voor de schijfcache.</span><span class="sxs-lookup"><span data-stu-id="463c7-137">In **Disk caching** select the appropriate disk caching option.</span></span> <span data-ttu-id="463c7-138">De opties zijn **geen**, **alleen-lezen** en **alleen-lezen**.</span><span class="sxs-lookup"><span data-stu-id="463c7-138">The options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="463c7-139">Optioneel: U kunt ook een bestaande gegevensschijf toevoegen op de installatiekopie door te klikken op **+ gegevensschijf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="463c7-139">Optional: You can also add an existing data disk to the image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="463c7-140">Wanneer u klaar bent u deze hebt geselecteerd, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="463c7-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="463c7-141">Nadat de installatiekopie is gemaakt, ziet u dit als een **installatiekopie** resource in de lijst met resources in de resourcegroep die u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="463c7-141">After the image is created, you will see it as an **Image** resource in the list of resources in the resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="463c7-142">Maken van een begeleide afbeelding van een virtuele machine met behulp van Powershell</span><span class="sxs-lookup"><span data-stu-id="463c7-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="463c7-143">Het maken van een installatiekopie van een rechtstreeks vanuit de virtuele machine, zorgt u ervoor dat de installatiekopie alle schijven die zijn gekoppeld aan de virtuele machine bevat, inclusief de Besturingssysteemschijf en alle gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="463c7-143">Creating an image directly from the VM ensures that the image includes all of the disks associated with the VM, including the OS Disk and any data disks.</span></span>


<span data-ttu-id="463c7-144">Voordat u begint, zorg ervoor dat u de nieuwste versie van de AzureRM.Compute PowerShell-module hebt.</span><span class="sxs-lookup"><span data-stu-id="463c7-144">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="463c7-145">Voer de volgende opdracht om deze te installeren.</span><span class="sxs-lookup"><span data-stu-id="463c7-145">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="463c7-146">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="463c7-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="463c7-147">Sommige variabelen maken.</span><span class="sxs-lookup"><span data-stu-id="463c7-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="463c7-148">Zorg ervoor dat de virtuele machine is opgeheven.</span><span class="sxs-lookup"><span data-stu-id="463c7-148">Make sure the VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="463c7-149">Zet de status van de virtuele machine **gegeneraliseerd**.</span><span class="sxs-lookup"><span data-stu-id="463c7-149">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="463c7-150">Zorg dat de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="463c7-150">Get the virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="463c7-151">Maak de configuratie van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="463c7-151">Create the image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="463c7-152">Maken van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="463c7-152">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="463c7-153">Maken van een begeleide afbeelding van een VHD in PowerShell</span><span class="sxs-lookup"><span data-stu-id="463c7-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="463c7-154">Maak een begeleide afbeelding met behulp van uw algemene besturingssysteem-VHD.</span><span class="sxs-lookup"><span data-stu-id="463c7-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="463c7-155">Stel eerst de algemene parameters:</span><span class="sxs-lookup"><span data-stu-id="463c7-155">First, set the common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="463c7-156">Step\deallocate de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="463c7-156">Step\deallocate the VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="463c7-157">De virtuele machine niet markeren als gegeneraliseerd.</span><span class="sxs-lookup"><span data-stu-id="463c7-157">Mark the VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="463c7-158">De installatiekopie via uw algemene besturingssysteem-VHD maken.</span><span class="sxs-lookup"><span data-stu-id="463c7-158">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="463c7-159">Een begeleide afbeelding maken vanuit een momentopname met behulp van Powershell</span><span class="sxs-lookup"><span data-stu-id="463c7-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="463c7-160">U kunt ook een begeleide afbeelding maken vanuit een momentopname van de VHD van een gegeneraliseerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="463c7-160">You can also create a managed image from a snapshot of the VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="463c7-161">Sommige variabelen maken.</span><span class="sxs-lookup"><span data-stu-id="463c7-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="463c7-162">Ophalen van de momentopname.</span><span class="sxs-lookup"><span data-stu-id="463c7-162">Get the snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="463c7-163">Maak de configuratie van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="463c7-163">Create the image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="463c7-164">Maken van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="463c7-164">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="463c7-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="463c7-165">Next steps</span></span>
- <span data-ttu-id="463c7-166">Nu u kunt [een virtuele machine maken van de installatiekopie van het algemene beheerde](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="463c7-166">Now you can [create a VM from the generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>  

