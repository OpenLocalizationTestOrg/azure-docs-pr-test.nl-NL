---
title: "Maken van aangepaste installatiekopieën voor virtuele machine met Azure PowerShell | Microsoft Docs"
description: Zelfstudie - maken van een aangepaste VM-installatiekopie met de Azure PowerShell.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 96be2872a902a7d7063bf1dff7b4ca209a5b67c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="345e4-103">Maken van een aangepaste installatiekopie van een virtuele machine in Azure met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="345e4-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="345e4-104">Aangepaste installatiekopieën zijn zoals marketplace-installatiekopieën, maar u deze zelf maken.</span><span class="sxs-lookup"><span data-stu-id="345e4-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="345e4-105">Aangepaste installatiekopieën kunnen worden gebruikt voor de bootstrap configuraties, zoals het vooraf laden van toepassingen, toepassingsconfiguraties en andere configuraties OS.</span><span class="sxs-lookup"><span data-stu-id="345e4-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="345e4-106">In deze zelfstudie maakt u uw eigen aangepaste installatiekopie van een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="345e4-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="345e4-107">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="345e4-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="345e4-108">Sysprep en generalize van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="345e4-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="345e4-109">Een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="345e4-109">Create a custom image</span></span>
> * <span data-ttu-id="345e4-110">Een virtuele machine van een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="345e4-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="345e4-111">Lijst van alle installatiekopieën in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="345e4-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="345e4-112">Een afbeelding verwijderen</span><span class="sxs-lookup"><span data-stu-id="345e4-112">Delete an image</span></span>

<span data-ttu-id="345e4-113">Voor deze zelfstudie is moduleversie 3,6 of hoger van Azure PowerShell vereist.</span><span class="sxs-lookup"><span data-stu-id="345e4-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="345e4-114">Voer ` Get-Module -ListAvailable AzureRM` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="345e4-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="345e4-115">Als u upgraden wilt, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="345e4-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="345e4-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="345e4-116">Before you begin</span></span>

<span data-ttu-id="345e4-117">De onderstaande stappen worden in detail beschreven hoe moet worden overgenomen van een bestaande virtuele machine en schakelt u deze in een herbruikbare aangepaste installatiekopie die u gebruiken kunt om nieuwe VM-exemplaren te maken.</span><span class="sxs-lookup"><span data-stu-id="345e4-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="345e4-118">Als u het voorbeeld in deze zelfstudie, moet u een bestaande virtuele machine hebben.</span><span class="sxs-lookup"><span data-stu-id="345e4-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="345e4-119">Indien nodig, dit [voorbeeldscript](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) kunt maken voor u.</span><span class="sxs-lookup"><span data-stu-id="345e4-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="345e4-120">Wanneer het uitvoeren van de zelfstudie vervangt benoemt de resourcegroep en de virtuele machine waar nodig.</span><span class="sxs-lookup"><span data-stu-id="345e4-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="345e4-121">Virtuele machine voorbereiden</span><span class="sxs-lookup"><span data-stu-id="345e4-121">Prepare VM</span></span>

<span data-ttu-id="345e4-122">Voor het maken van een installatiekopie van een virtuele machine, moet u de virtuele machine voorbereiden door het generaliseren van de virtuele machine, toewijzing en vervolgens de bron-VM als gegeneraliseerd in Azure te markeren.</span><span class="sxs-lookup"><span data-stu-id="345e4-122">To create an image of a virtual machine, you need to prepare the VM by generalizing the VM, deallocating, and then marking the source VM as generalized in Azure.</span></span>

### <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="345e4-123">De virtuele machine van Windows met behulp van Sysprep generalize</span><span class="sxs-lookup"><span data-stu-id="345e4-123">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="345e4-124">Sysprep verwijdert alle persoonlijke gegevens over uw account, onder andere en voorbereiden van de machine moet worden gebruikt als een afbeelding.</span><span class="sxs-lookup"><span data-stu-id="345e4-124">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="345e4-125">Zie voor meer informatie over Sysprep [hoe gebruik Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="345e4-125">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="345e4-126">Verbinding maken met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="345e4-126">Connect to the virtual machine.</span></span>
2. <span data-ttu-id="345e4-127">Open het venster opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="345e4-127">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="345e4-128">Wijzig de map in *%windir%\system32\sysprep*, en voer vervolgens *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="345e4-128">Change the directory to *%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="345e4-129">In de **hulpprogramma voor systeemvoorbereiding** dialoogvenster, *System Voer Out-of-Box Experience (OOBE)*, en zorg ervoor dat de *Generalize* selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="345e4-129">In the **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that the *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="345e4-130">In **afsluitopties**, selecteer *afsluiten* en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="345e4-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="345e4-131">Wanneer Sysprep is voltooid, afgesloten de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="345e4-131">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="345e4-132">**De virtuele machine niet opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="345e4-132">**Do not restart the VM**.</span></span>

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="345e4-133">Toewijzing ongedaan maken en de virtuele machine niet markeren als gegeneraliseerd</span><span class="sxs-lookup"><span data-stu-id="345e4-133">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="345e4-134">Voor het maken van een installatiekopie, moet de virtuele machine worden toewijzing ongedaan gemaakt en is gemarkeerd als gegeneraliseerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="345e4-134">To create an image, the VM needs to be deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="345e4-135">De virtuele machine met behulp van de toewijzing opgeheven [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="345e4-135">Deallocated the VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="345e4-136">Zet de status van de virtuele machine `-Generalized` met [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="345e4-136">Set the status of the virtual machine to `-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-the-image"></a><span data-ttu-id="345e4-137">De installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="345e4-137">Create the image</span></span>

<span data-ttu-id="345e4-138">Nu u een installatiekopie van de virtuele machine maken met behulp van kunt [nieuw AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) en [nieuw AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="345e4-138">Now you can create an image of the VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="345e4-139">Het volgende voorbeeld wordt een installatiekopie met de naam *myImage* van een virtuele machine met de naam *myVM*.</span><span class="sxs-lookup"><span data-stu-id="345e4-139">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="345e4-140">Zorg dat de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="345e4-140">Get the virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="345e4-141">Maak de configuratie van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="345e4-141">Create the image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="345e4-142">Maken van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="345e4-142">Create the image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="345e4-143">Virtuele machines van de installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="345e4-143">Create VMs from the image</span></span>

<span data-ttu-id="345e4-144">Nu dat u een installatiekopie hebt, kunt u een of meer nieuwe virtuele machines kunt maken van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="345e4-144">Now that you have an image, you can create one or more new VMs from the image.</span></span> <span data-ttu-id="345e4-145">Maken van een virtuele machine van een aangepaste installatiekopie is vergelijkbaar met het maken van een virtuele machine met behulp van een Marketplace-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="345e4-145">Creating a VM from a custom image is very similar to creating a VM using a Marketplace image.</span></span> <span data-ttu-id="345e4-146">Wanneer u een Marketplace-installatiekopie gebruikt, moet u informatie over de installatiekopie, afbeeldingenprovider, aanbieding, SKU en versie.</span><span class="sxs-lookup"><span data-stu-id="345e4-146">When you use a Marketplace image, you have to information about the image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="345e4-147">Met een aangepaste installatiekopie moet u alleen de ID van de aangepaste Afbeeldingsbron opgeven.</span><span class="sxs-lookup"><span data-stu-id="345e4-147">With a custom image, you just need to provide the ID of the custom image resource.</span></span> 

<span data-ttu-id="345e4-148">In het volgende script maken we een variabele *$image* voor het opslaan van informatie over het gebruik van de aangepaste installatiekopie [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) en vervolgens gebruiken we [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) en geeft u de ID met de *$image* variabele we zojuist hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="345e4-148">In the following script, we create a variable *$image* to store information about the custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify the ID using the *$image* variable we just created.</span></span> 

<span data-ttu-id="345e4-149">Het script maakt een virtuele machine met de naam *myVMfromImage* van onze aangepaste installatiekopie in een nieuwe resourcegroep met de naam *myResourceGroupFromImage* in de *VS-West* locatie.</span><span class="sxs-lookup"><span data-stu-id="345e4-149">The script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in the *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable to store information about the image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want to create the VM from and image and provide the image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="345e4-150">Beheer van installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="345e4-150">Image management</span></span> 

<span data-ttu-id="345e4-151">Hier volgen enkele voorbeelden van algemene beheertaken voor de installatiekopie en hoe u uit te voeren met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="345e4-151">Here are some examples of common management image tasks and how to complete them using PowerShell.</span></span>

<span data-ttu-id="345e4-152">Lijst van alle installatiekopieën op naam.</span><span class="sxs-lookup"><span data-stu-id="345e4-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="345e4-153">Een afbeelding verwijderen.</span><span class="sxs-lookup"><span data-stu-id="345e4-153">Delete an image.</span></span> <span data-ttu-id="345e4-154">Dit voorbeeld wordt verwijderd van de installatiekopie met de naam *myOldImage* van de *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="345e4-154">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="345e4-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="345e4-155">Next steps</span></span>

<span data-ttu-id="345e4-156">In deze zelfstudie maakt u een aangepaste installatiekopie van de virtuele machine gemaakt.</span><span class="sxs-lookup"><span data-stu-id="345e4-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="345e4-157">U leert hoe naar:</span><span class="sxs-lookup"><span data-stu-id="345e4-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="345e4-158">Sysprep en generalize van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="345e4-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="345e4-159">Een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="345e4-159">Create a custom image</span></span>
> * <span data-ttu-id="345e4-160">Een virtuele machine van een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="345e4-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="345e4-161">Lijst van alle installatiekopieën in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="345e4-161">List all the images in your subscription</span></span>
> * <span data-ttu-id="345e4-162">Een afbeelding verwijderen</span><span class="sxs-lookup"><span data-stu-id="345e4-162">Delete an image</span></span>

<span data-ttu-id="345e4-163">Ga naar de volgende zelfstudie voor meer informatie over hoe maximaal beschikbare virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="345e4-163">Advance to the next tutorial to learn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="345e4-164">Virtuele machines met hoge beschikbaarheid maken</span><span class="sxs-lookup"><span data-stu-id="345e4-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



