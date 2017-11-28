---
title: "aangepaste VM-installatiekopieën aaaCreate Hello Azure PowerShell | Microsoft Docs"
description: Zelfstudie - een aangepaste VM-installatiekopie met behulp van Azure PowerShell Hallo maken.
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
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="f0114-103">Maken van een aangepaste installatiekopie van een virtuele machine in Azure met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0114-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="f0114-104">Aangepaste installatiekopieën zijn zoals marketplace-installatiekopieën, maar u deze zelf maken.</span><span class="sxs-lookup"><span data-stu-id="f0114-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="f0114-105">Aangepaste installatiekopieën kunnen worden gebruikt toobootstrap configuraties zoals vooraf laden van toepassingen, toepassingsconfiguraties en andere configuraties OS.</span><span class="sxs-lookup"><span data-stu-id="f0114-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="f0114-106">In deze zelfstudie maakt u uw eigen aangepaste installatiekopie van een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="f0114-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="f0114-107">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="f0114-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f0114-108">Sysprep en generalize van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="f0114-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="f0114-109">Een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f0114-109">Create a custom image</span></span>
> * <span data-ttu-id="f0114-110">Een virtuele machine van een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f0114-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="f0114-111">Lijst van alle Hallo-installatiekopieën in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="f0114-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="f0114-112">Een afbeelding verwijderen</span><span class="sxs-lookup"><span data-stu-id="f0114-112">Delete an image</span></span>

<span data-ttu-id="f0114-113">Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="f0114-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="f0114-114">Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="f0114-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="f0114-115">Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f0114-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f0114-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f0114-116">Before you begin</span></span>

<span data-ttu-id="f0114-117">Hallo stappen hieronder wordt beschreven hoe tootake een bestaande virtuele machine en schakel dit in een herbruikbare aangepaste installatiekopie die u hebt de nieuwe VM-instanties toocreate kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f0114-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="f0114-118">toocomplete hello voorbeeld in deze zelfstudie, moet u een bestaande virtuele machine hebben.</span><span class="sxs-lookup"><span data-stu-id="f0114-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="f0114-119">Indien nodig, dit [voorbeeldscript](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) kunt maken voor u.</span><span class="sxs-lookup"><span data-stu-id="f0114-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="f0114-120">Wanneer werkende Hallo-zelfstudie vervangt benoemt Hallo resourcegroep en de VM waar nodig.</span><span class="sxs-lookup"><span data-stu-id="f0114-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="f0114-121">Virtuele machine voorbereiden</span><span class="sxs-lookup"><span data-stu-id="f0114-121">Prepare VM</span></span>

<span data-ttu-id="f0114-122">toocreate een installatiekopie van een virtuele machine, moet u tooprepare Hallo VM door het generaliseren Hallo VM, toewijzing en het vervolgens markeren Hallo bron-VM als gegeneraliseerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="f0114-122">toocreate an image of a virtual machine, you need tooprepare hello VM by generalizing hello VM, deallocating, and then marking hello source VM as generalized in Azure.</span></span>

### <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="f0114-123">Generalize Hallo van virtuele machine van Windows met behulp van Sysprep</span><span class="sxs-lookup"><span data-stu-id="f0114-123">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="f0114-124">Sysprep verwijdert alle persoonlijke gegevens over uw account, onder andere en bereidt Hallo machine toobe gebruikt als een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="f0114-124">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="f0114-125">Zie voor meer informatie over Sysprep [hoe tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0114-125">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="f0114-126">Verbinding maken met toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f0114-126">Connect toohello virtual machine.</span></span>
2. <span data-ttu-id="f0114-127">Hallo-opdrachtpromptvenster open als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f0114-127">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="f0114-128">Hallo directory ook wijzigen*%windir%\system32\sysprep*, en voer vervolgens *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="f0114-128">Change hello directory too*%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="f0114-129">In Hallo **hulpprogramma voor systeemvoorbereiding** dialoogvenster, *System Voer Out-of-Box Experience (OOBE)*, en zorg ervoor dat Hallo *Generalize* selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f0114-129">In hello **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that hello *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="f0114-130">In **afsluitopties**, selecteer *afsluiten* en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0114-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="f0114-131">Wanneer Sysprep is voltooid, afgesloten Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f0114-131">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="f0114-132">**Hallo VM niet opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="f0114-132">**Do not restart hello VM**.</span></span>

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="f0114-133">Toewijzing ongedaan maken en Hallo VM zoals gegeneraliseerd markeren</span><span class="sxs-lookup"><span data-stu-id="f0114-133">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="f0114-134">een installatiekopie van een toocreate, Hallo VM moet toobe toewijzing ongedaan gemaakt en is gemarkeerd als gegeneraliseerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="f0114-134">toocreate an image, hello VM needs toobe deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="f0114-135">Hallo toewijzing ongedaan is gemaakt met behulp van VM [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f0114-135">Deallocated hello VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="f0114-136">Hallo-status van Hallo virtuele machine te instellen`-Generalized` met [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f0114-136">Set hello status of hello virtual machine too`-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a><span data-ttu-id="f0114-137">Hallo installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f0114-137">Create hello image</span></span>

<span data-ttu-id="f0114-138">Nu u een installatiekopie van Hallo VM maken met behulp van kunt [nieuw AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) en [nieuw AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="f0114-138">Now you can create an image of hello VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="f0114-139">Hallo volgende voorbeeld wordt een installatiekopie met de naam *myImage* van een virtuele machine met de naam *myVM*.</span><span class="sxs-lookup"><span data-stu-id="f0114-139">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="f0114-140">Hallo virtuele machine worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="f0114-140">Get hello virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="f0114-141">Hallo imageconfiguratie maken.</span><span class="sxs-lookup"><span data-stu-id="f0114-141">Create hello image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="f0114-142">Hallo-installatiekopie kan maken.</span><span class="sxs-lookup"><span data-stu-id="f0114-142">Create hello image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="f0114-143">Virtuele machines uit Hallo installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f0114-143">Create VMs from hello image</span></span>

<span data-ttu-id="f0114-144">Nu dat u een installatiekopie hebt, kunt u een of meer nieuwe virtuele machines kunt maken van Hallo image.</span><span class="sxs-lookup"><span data-stu-id="f0114-144">Now that you have an image, you can create one or more new VMs from hello image.</span></span> <span data-ttu-id="f0114-145">Maken van een virtuele machine van een aangepaste installatiekopie is heel vergelijkbaar toocreating een VM die gebruikmaakt van een Marketplace-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="f0114-145">Creating a VM from a custom image is very similar toocreating a VM using a Marketplace image.</span></span> <span data-ttu-id="f0114-146">Wanneer u een Marketplace-installatiekopie gebruikt, hebt u tooinformation over Hallo-installatiekopie, afbeeldingenprovider, aanbieding, SKU en versie.</span><span class="sxs-lookup"><span data-stu-id="f0114-146">When you use a Marketplace image, you have tooinformation about hello image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="f0114-147">Met een aangepaste installatiekopie hoeft u alleen tooprovide Hallo-ID van de aangepaste Afbeeldingsbron Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0114-147">With a custom image, you just need tooprovide hello ID of hello custom image resource.</span></span> 

<span data-ttu-id="f0114-148">Hallo script volgen, maken we een variabele *$image* toostore informatie over het gebruik van de aangepaste installatiekopie Hallo [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) en vervolgens gebruiken we [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)en met behulp van Hallo Hallo-ID opgeven *$image* variabele we zojuist hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f0114-148">In hello following script, we create a variable *$image* toostore information about hello custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify hello ID using hello *$image* variable we just created.</span></span> 

<span data-ttu-id="f0114-149">Hallo script maakt een virtuele machine met de naam *myVMfromImage* van onze aangepaste installatiekopie in een nieuwe resourcegroep met de naam *myResourceGroupFromImage* in Hallo *VS-West* locatie.</span><span class="sxs-lookup"><span data-stu-id="f0114-149">hello script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in hello *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

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

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="f0114-150">Beheer van installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="f0114-150">Image management</span></span> 

<span data-ttu-id="f0114-151">Hier volgen enkele voorbeelden van algemene beheertaken voor de installatiekopie en hoe toocomplete ze met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0114-151">Here are some examples of common management image tasks and how toocomplete them using PowerShell.</span></span>

<span data-ttu-id="f0114-152">Lijst van alle installatiekopieën op naam.</span><span class="sxs-lookup"><span data-stu-id="f0114-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="f0114-153">Een afbeelding verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f0114-153">Delete an image.</span></span> <span data-ttu-id="f0114-154">In dit voorbeeld verwijderingen Hallo installatiekopie met de naam *myOldImage* van Hallo *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="f0114-154">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f0114-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f0114-155">Next steps</span></span>

<span data-ttu-id="f0114-156">In deze zelfstudie maakt u een aangepaste installatiekopie van de virtuele machine gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f0114-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="f0114-157">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="f0114-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f0114-158">Sysprep en generalize van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="f0114-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="f0114-159">Een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f0114-159">Create a custom image</span></span>
> * <span data-ttu-id="f0114-160">Een virtuele machine van een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f0114-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="f0114-161">Lijst van alle Hallo-installatiekopieën in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="f0114-161">List all hello images in your subscription</span></span>
> * <span data-ttu-id="f0114-162">Een afbeelding verwijderen</span><span class="sxs-lookup"><span data-stu-id="f0114-162">Delete an image</span></span>

<span data-ttu-id="f0114-163">Ga toohello volgende zelfstudie toolearn over hoe maximaal beschikbare virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f0114-163">Advance toohello next tutorial toolearn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f0114-164">Virtuele machines met hoge beschikbaarheid maken</span><span class="sxs-lookup"><span data-stu-id="f0114-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



