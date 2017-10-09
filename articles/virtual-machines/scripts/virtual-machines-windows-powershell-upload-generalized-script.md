---
title: een gegeneraliseerde VHD tooAzure PowerShell-voorbeeldscript aaaUpload | Microsoft Docs
description: PowerShell script tooupload een gegeneraliseerde VHD tooAzure steekproef en een nieuwe virtuele machine maken met Hallo resource manager-implementatiemodel en schijven beheerd.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/18/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 72b4ff09eb7a6ba1604b9d5cbac51e60eded7545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-script-tooupload-a-vhd-tooazure-and-create-a-new-vm"></a><span data-ttu-id="2f0f0-103">Voorbeeld tooupload script een VHD-tooAzure en een nieuwe virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="2f0f0-103">Sample script tooupload a VHD tooAzure and create a new VM</span></span>

<span data-ttu-id="2f0f0-104">Dit script krijgt een lokale VHD-bestand met een gegeneraliseerde virtuele machine en tooAzure geüpload, maakt u een beheerd schijfkopie en Hallo toocreate een nieuwe virtuele machine gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-104">This script takes a local .vhd file from a generalized VM and uploads it tooAzure, creates a Managed Disk image and uses hello toocreate a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2f0f0-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="2f0f0-105">Sample script</span></span>

```powershell
# Provide values for hello variables
$resourceGroup = 'myResourceGroup'
$location = 'EastUS'
$storageaccount = 'mystorageaccount'
$storageType = 'Standard_LRS'
$containername = 'mycontainer'
$localPath = 'C:\Users\Public\Documents\Hyper-V\VHDs\generalized.vhd'
$vmName = 'myVM'
$imageName = 'myImage'
$vhdName = 'myUploadedVhd.vhd'
$diskSizeGB = '128'
$subnetName = 'mySubnet'
$vnetName = 'myVnet'
$ipName = 'myPip'
$nicName = 'myNic'
$nsgName = 'myNsg'
$ruleName = 'myRdpRule'
$vmName = 'myVM'
$computerName = 'myComputerName'
$vmSize = 'Standard_DS1_v2'

# Get hello username and password toobe used for hello administrators account on hello VM. 
# This is used when connecting toohello VM using RDP.

$cred = Get-Credential

# Upload hello VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading hello VHD may take awhile!

# Create a managed image from hello uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create hello networking resources
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $resourceGroup -Location $location `
    -AllocationMethod Dynamic
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroup -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description 'Allow RDP' -Access Allow `
    -Protocol Tcp -Direction Inbound -Priority 110 -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $resourceGroup -Name $vnetName

# Start building hello VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set hello VM image as source image for hello new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish hello VM configuration and add hello NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create hello VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that hello VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="2f0f0-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="2f0f0-106">Clean up deployment</span></span> 

<span data-ttu-id="2f0f0-107">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2f0f0-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="2f0f0-108">Script explanation</span></span>

<span data-ttu-id="2f0f0-109">Dit script maakt gebruik van Hallo opdrachten toocreate Hallo implementatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="2f0f0-110">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2f0f0-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="2f0f0-111">Command</span></span>                                                                                                             | <span data-ttu-id="2f0f0-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="2f0f0-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="2f0f0-113">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2f0f0-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="2f0f0-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="2f0f0-115">Nieuwe AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="2f0f0-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="2f0f0-116">Hiermee maakt u een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="2f0f0-117">Voeg AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="2f0f0-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="2f0f0-118">Een virtuele harde schijf van een lokale virtuele machine tooa blob in een cloud-opslagaccount in Azure uploadt.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-118">Uploads a virtual hard disk from an on-premises virtual machine tooa blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="2f0f0-119">Nieuwe AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="2f0f0-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="2f0f0-120">Maakt een configureerbare installatiekopie-object.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="2f0f0-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="2f0f0-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="2f0f0-122">Hiermee stelt u Hallo besturingssysteem schijfeigenschappen op een installatiekopie-object.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-122">Sets hello operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="2f0f0-123">Nieuwe AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="2f0f0-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="2f0f0-124">Maakt een nieuwe installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="2f0f0-125">Nieuwe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="2f0f0-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="2f0f0-126">Hiermee maakt u de subnetconfiguratie van een.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-126">Creates a subnet configuration.</span></span> <span data-ttu-id="2f0f0-127">Deze configuratie wordt gebruikt met Hallo-proces voor het maken van virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-127">This configuration is used with hello virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="2f0f0-128">Nieuwe-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="2f0f0-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="2f0f0-129">Hiermee maakt u een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="2f0f0-130">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="2f0f0-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="2f0f0-131">Hiermee maakt u een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="2f0f0-132">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="2f0f0-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="2f0f0-133">Maakt een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="2f0f0-134">Nieuwe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="2f0f0-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="2f0f0-135">Maakt een groep regel de netwerkbeveiligingsconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="2f0f0-136">Deze configuratie is gebruikte toocreate een regel voor het NSG wanneer Hallo NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-136">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span>                                                       |
| [<span data-ttu-id="2f0f0-137">Nieuwe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="2f0f0-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="2f0f0-138">Een netwerkbeveiligingsgroep maakt.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="2f0f0-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="2f0f0-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="2f0f0-140">Hiermee haalt een virtueel netwerk in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="2f0f0-141">Nieuwe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="2f0f0-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="2f0f0-142">Maakt een VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-142">Creates a VM configuration.</span></span> <span data-ttu-id="2f0f0-143">Deze configuratie bevat informatie zoals de naam, het besturingssysteem en de beheerdersreferenties VM.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="2f0f0-144">Hallo-configuratie wordt gebruikt tijdens het maken van VM.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="2f0f0-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="2f0f0-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="2f0f0-146">Hiermee geeft u een installatiekopie voor een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="2f0f0-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="2f0f0-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="2f0f0-148">Hiermee stelt u Hallo besturingssysteem schijfeigenschappen op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-148">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="2f0f0-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="2f0f0-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="2f0f0-150">Hiermee stelt u Hallo besturingssysteem schijfeigenschappen op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-150">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="2f0f0-151">Voeg AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="2f0f0-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="2f0f0-152">Voegt een network interface tooa virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-152">Adds a network interface tooa virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="2f0f0-153">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="2f0f0-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="2f0f0-154">Maak een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="2f0f0-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2f0f0-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="2f0f0-156">Hiermee verwijdert u een resourcegroep en alle resources binnen.</span><span class="sxs-lookup"><span data-stu-id="2f0f0-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="2f0f0-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f0f0-157">Next steps</span></span>

<span data-ttu-id="2f0f0-158">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2f0f0-158">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2f0f0-159">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f0f0-159">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
