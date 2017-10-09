---
title: aaaAzure hybride gebruik voordeel voor Windows Server en Windows-Client | Microsoft Docs
description: Meer informatie over hoe toomaximize uw Windows Software Assurance voordelen toobring lokale tooAzure licenties
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: f24487320a60132aaf766a31f3e6f3726d4a3bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a><span data-ttu-id="9541c-103">Azure hybride gebruik voordeel voor WindowsServer en Windows-Client</span><span class="sxs-lookup"><span data-stu-id="9541c-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span></span>
<span data-ttu-id="9541c-104">Voor klanten met Software Assurance Azure hybride gebruik Benefit kunt u toouse uw lokale Windows Server en Windows-Client licenties en voer Windows virtuele machines in Azure tegen lagere kosten.</span><span class="sxs-lookup"><span data-stu-id="9541c-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you toouse your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span></span> <span data-ttu-id="9541c-105">Azure hybride gebruik voordeel voor Windows Server omvat Windows Server 2008 R2, Windows Server 2012, Windows Server 2012R2 en Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="9541c-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span></span> <span data-ttu-id="9541c-106">Azure hybride gebruik voordeel voor Windows-Client omvat Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9541c-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span></span> <span data-ttu-id="9541c-107">Zie voor meer informatie Hallo [Azure hybride gebruik voordeel licentieverlening pagina](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="9541c-107">For more information, please see hello [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

>[!IMPORTANT]
><span data-ttu-id="9541c-108">Azure hybride gebruik voordelen voor Windows-Client is momenteel in Preview met Windows 10 Hallo installatiekopie in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9541c-108">Azure Hybrid Use Benefits for Windows Client is currently in Preview using hello Windows 10 image in hello Azure Marketplace.</span></span> <span data-ttu-id="9541c-109">Alleen zakelijke klanten met Windows 10 Enterprise E3/E5 per gebruiker of Windows VDA per gebruiker (abonnement gebruikerslicenties of abonnement voor extra gebruikerslicenties) ('in aanmerking komende licenties') in aanmerking komen.</span><span class="sxs-lookup"><span data-stu-id="9541c-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span></span>
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a><span data-ttu-id="9541c-110">Manieren toouse Azure hybride gebruik Benefit</span><span class="sxs-lookup"><span data-stu-id="9541c-110">Ways toouse Azure Hybrid Use Benefit</span></span>
<span data-ttu-id="9541c-111">Er zijn een aantal verschillende manieren toodeploy VM's van Windows Hello Azure hybride gebruik voordeel:</span><span class="sxs-lookup"><span data-stu-id="9541c-111">There are a couple of different ways toodeploy Windows VMs with hello Azure Hybrid Use Benefit:</span></span>

1. <span data-ttu-id="9541c-112">U kunt virtuele machines van [specifieke Marketplace-installatiekopieën](#deploy-a-vm-using-the-azure-marketplace) die vooraf is geconfigureerd met Azure hybride gebruik voordeel - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 en Windows Server 2008SP1 zijn.</span><span class="sxs-lookup"><span data-stu-id="9541c-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span>
2. <span data-ttu-id="9541c-113">U kunt [uploaden van een aangepaste VM](#upload-a-windows-vhd) en [implementeren met behulp van een Resource Manager-sjabloon](#deploy-a-vm-via-resource-manager) of [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="9541c-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span></span>

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a><span data-ttu-id="9541c-114">Een virtuele machine geïmplementeerd met hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="9541c-114">Deploy a VM using hello Azure Marketplace</span></span>
<span data-ttu-id="9541c-115">Volgende installatiekopieën zijn beschikbaar in Hallo Marketplace vooraf geconfigureerd met Azure hybride gebruik voordeel: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 en Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="9541c-115">Following images are available in hello Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span> <span data-ttu-id="9541c-116">Deze installatiekopieën kunnen rechtstreeks vanuit hello Azure-portal, Resource Manager-sjablonen of Azure PowerShell worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="9541c-116">These images can be deployed directly from hello Azure portal, Resource Manager templates, or Azure PowerShell.</span></span>

<span data-ttu-id="9541c-117">U kunt deze installatiekopieën rechtstreeks vanuit hello Azure-portal kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="9541c-117">You can deploy these images directly from hello Azure portal.</span></span> <span data-ttu-id="9541c-118">Voor gebruik in het Resource Manager-sjablonen en met Azure PowerShell, Hallo lijst weergeven met afbeeldingen als volgt:</span><span class="sxs-lookup"><span data-stu-id="9541c-118">For use in Resource Manager templates and with Azure PowerShell, view hello list of images as follows:</span></span>

<span data-ttu-id="9541c-119">Voor WindowsServer:</span><span class="sxs-lookup"><span data-stu-id="9541c-119">For Windows Server:</span></span>
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- <span data-ttu-id="9541c-120">2016 Datacenter versie 2016.127.20170406 of hoger</span><span class="sxs-lookup"><span data-stu-id="9541c-120">2016-Datacenter version 2016.127.20170406 or above</span></span>

- <span data-ttu-id="9541c-121">2012-R2-Datacenter versie 4.127.20170406 of hoger</span><span class="sxs-lookup"><span data-stu-id="9541c-121">2012-R2-Datacenter version 4.127.20170406 or above</span></span>

- <span data-ttu-id="9541c-122">2012 Datacenter versie 3.127.20170406 of hoger</span><span class="sxs-lookup"><span data-stu-id="9541c-122">2012-Datacenter version 3.127.20170406 or above</span></span>

- <span data-ttu-id="9541c-123">2008 R2 SP1-versie 2.127.20170406 of hoger</span><span class="sxs-lookup"><span data-stu-id="9541c-123">2008-R2-SP1 version 2.127.20170406 or above</span></span>

<span data-ttu-id="9541c-124">Voor Windows-Client:</span><span class="sxs-lookup"><span data-stu-id="9541c-124">For Windows Client:</span></span>
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a><span data-ttu-id="9541c-125">Een WindowsServer-VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="9541c-125">Upload a Windows Server VHD</span></span>
<span data-ttu-id="9541c-126">toodeploy een Windows Server-VM in Azure, moet u eerst een VHD met uw Windows-build base toocreate.</span><span class="sxs-lookup"><span data-stu-id="9541c-126">toodeploy a Windows Server VM in Azure, you first need toocreate a VHD that contains your base Windows build.</span></span> <span data-ttu-id="9541c-127">Deze VHD moet op de juiste wijze worden voorbereid met Sysprep voordat u deze tooAzure uploaden.</span><span class="sxs-lookup"><span data-stu-id="9541c-127">This VHD must be appropriately prepared via Sysprep before you upload it tooAzure.</span></span> <span data-ttu-id="9541c-128">U kunt [voor meer informatie over Hallo VHD vereisten en Sysprep-proces](upload-generalized-managed.md) en [Sysprep-ondersteuning voor serverrollen](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="9541c-128">You can [read more about hello VHD requirements and Sysprep process](upload-generalized-managed.md) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span> <span data-ttu-id="9541c-129">Back-up Hallo VM voordat Sysprep wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9541c-129">Back up hello VM before running Sysprep.</span></span> 

<span data-ttu-id="9541c-130">Zorg ervoor dat u hebt [geïnstalleerd en geconfigureerd hello nieuwste Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9541c-130">Make sure you have [installed and configured hello latest Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="9541c-131">Nadat u uw VHD hebt voorbereid, uploaden Hallo VHD tooyour Azure Storage-account met behulp van Hallo `Add-AzureRmVhd` cmdlet als volgt:</span><span class="sxs-lookup"><span data-stu-id="9541c-131">Once you have prepared your VHD, upload hello VHD tooyour Azure Storage account using hello `Add-AzureRmVhd` cmdlet as follows:</span></span>

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> <span data-ttu-id="9541c-132">Microsoft SQL Server, SharePoint Server en Dynamics kan ook gebruikmaken van uw Software Assurance-licentieverlening.</span><span class="sxs-lookup"><span data-stu-id="9541c-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span></span> <span data-ttu-id="9541c-133">U moet nog steeds tooprepare Hallo de installatiekopie van Windows Server door onderdelen van uw toepassing installeren en dienovereenkomstig licentiesleutels bieden, en vervolgens Hallo schijf installatiekopie tooAzure uploaden.</span><span class="sxs-lookup"><span data-stu-id="9541c-133">You still need tooprepare hello Windows Server image by installing your application components and providing license keys accordingly, then uploading hello disk image tooAzure.</span></span> <span data-ttu-id="9541c-134">Hallo geschikte documentatie voor het uitvoeren van Sysprep met uw toepassing, zoals lezen [overwegingen voor SQL Server installeren met behulp van Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) of [bouwen van een SharePoint-Server 2016 referentie-installatiekopie (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span><span class="sxs-lookup"><span data-stu-id="9541c-134">Review hello appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span></span>
>
>

<span data-ttu-id="9541c-135">U kunt ook meer informatie over [Hallo VHD tooAzure proces uploaden](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="9541c-135">You can also read more about [uploading hello VHD tooAzure process](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span></span>


## <a name="deploy-a-vm-via-resource-manager-template"></a><span data-ttu-id="9541c-136">Een virtuele machine via Resource Manager-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="9541c-136">Deploy a VM via Resource Manager Template</span></span>
<span data-ttu-id="9541c-137">In de Resource Manager-sjablonen, een extra parameter voor `licenseType` kan worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9541c-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span></span> <span data-ttu-id="9541c-138">U kunt meer lezen over [Azure Resource Manager-sjablonen ontwerpen](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9541c-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="9541c-139">Zodra u uw tooAzure VHD geüpload hebt, bewerk u Resource Manager tooinclude Hallo licentie voor het sjabloontype als onderdeel van Hallo provider berekenen en implementeren van uw sjabloon als normale:</span><span class="sxs-lookup"><span data-stu-id="9541c-139">Once you have your VHD uploaded tooAzure, edit you Resource Manager template tooinclude hello license type as part of hello compute provider and deploy your template as normal:</span></span>

<span data-ttu-id="9541c-140">Voor WindowsServer:</span><span class="sxs-lookup"><span data-stu-id="9541c-140">For Windows Server:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

<span data-ttu-id="9541c-141">Voor alleen Windows-Client-toouse met Azure Marketplace-installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="9541c-141">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a><span data-ttu-id="9541c-142">Een virtuele machine via PowerShell Quick Start implementeren</span><span class="sxs-lookup"><span data-stu-id="9541c-142">Deploy a VM via PowerShell quickstart</span></span>
<span data-ttu-id="9541c-143">Wanneer u uw Windows Server-VM via PowerShell implementeert, hebt u een extra parameter voor `-LicenseType`.</span><span class="sxs-lookup"><span data-stu-id="9541c-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span></span> <span data-ttu-id="9541c-144">Zodra u uw tooAzure VHD geüpload hebt, maakt u een VM met `New-AzureRmVM` en geef een Hallo licentieverlening als volgt:</span><span class="sxs-lookup"><span data-stu-id="9541c-144">Once you have your VHD uploaded tooAzure, you create a VM using `New-AzureRmVM` and specify hello licensing type as follows:</span></span>

<span data-ttu-id="9541c-145">Voor WindowsServer:</span><span class="sxs-lookup"><span data-stu-id="9541c-145">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="9541c-146">Voor alleen Windows-Client-toouse met Azure Marketplace-installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="9541c-146">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

<span data-ttu-id="9541c-147">U kunt [lezen van een meer gedetailleerde uitleg over het implementeren van een virtuele machine in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) onderstaande of lezen een meer beschrijvende gids op verschillende stappen te Hallo[maken van een Windows-VM met Resource Manager en PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9541c-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on hello different steps too[create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a><span data-ttu-id="9541c-148">Controleer of uw virtuele machine wordt gebruikt door de licentiegegevens voordeel Hallo</span><span class="sxs-lookup"><span data-stu-id="9541c-148">Verify your VM is utilizing hello licensing benefit</span></span>
<span data-ttu-id="9541c-149">Nadat u uw virtuele machine via Hallo PowerShell of Resource Manager-implementatiemethode hebt geïmplementeerd, controleren of de Hallo licentietype met `Get-AzureRmVM` als volgt:</span><span class="sxs-lookup"><span data-stu-id="9541c-149">Once you have deployed your VM through either hello PowerShell or Resource Manager deployment method, verify hello license type with `Get-AzureRmVM` as follows:</span></span>

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="9541c-150">Hallo uitvoer is vergelijkbaar toohello volgt voor Windows Server:</span><span class="sxs-lookup"><span data-stu-id="9541c-150">hello output is similar toohello following example for Windows Server:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

<span data-ttu-id="9541c-151">Deze uitvoer in tegenstelling tot Hallo die volgende VM geïmplementeerd zonder Azure hybride gebruik voordeel-licentieverlening, zoals een virtuele machine rechtstreeks vanuit de galerie van Azure Hallo geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="9541c-151">This output contrasts with hello following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from hello Azure Gallery:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a><span data-ttu-id="9541c-152">Gedetailleerd overzicht van de PowerShell-implementatie</span><span class="sxs-lookup"><span data-stu-id="9541c-152">Detailed PowerShell deployment walkthrough</span></span>
<span data-ttu-id="9541c-153">Hallo volgende gedetailleerde PowerShell stappen weergeven met een volledige implementatie van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9541c-153">hello following detailed PowerShell steps show a full deployment of a VM.</span></span> <span data-ttu-id="9541c-154">U kunt meer context lezen als toohello Werkelijke cmdlets en andere onderdelen wordt gemaakt in [maken van een Windows-VM met Resource Manager en PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9541c-154">You can read more context as toohello actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="9541c-155">U stapsgewijs door het maken van de resourcegroep, storage-account en virtuele netwerken, en vervolgens uw virtuele machine definiëren en ten slotte uw virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="9541c-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span></span>

<span data-ttu-id="9541c-156">Eerst veilig referenties verkrijgen, stelt u een locatie en de naam van resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="9541c-156">First, securely obtain credentials, set a location, and resource group name:</span></span>

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

<span data-ttu-id="9541c-157">Maak een openbare IP-adres:</span><span class="sxs-lookup"><span data-stu-id="9541c-157">Create a public IP:</span></span>

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

<span data-ttu-id="9541c-158">Uw subnet, NIC en VNET definiëren:</span><span class="sxs-lookup"><span data-stu-id="9541c-158">Define your subnet, NIC, and VNET:</span></span>

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

<span data-ttu-id="9541c-159">Naam van uw virtuele machine en maak een VM-configuratie:</span><span class="sxs-lookup"><span data-stu-id="9541c-159">Name your VM and create a VM config:</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

<span data-ttu-id="9541c-160">Definieer uw besturingssysteem:</span><span class="sxs-lookup"><span data-stu-id="9541c-160">Define your OS:</span></span>

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="9541c-161">Voeg uw NIC toohello VM:</span><span class="sxs-lookup"><span data-stu-id="9541c-161">Add your NIC toohello VM:</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="9541c-162">Hallo storage account toouse definiëren:</span><span class="sxs-lookup"><span data-stu-id="9541c-162">Define hello storage account toouse:</span></span>

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

<span data-ttu-id="9541c-163">Upload uw VHD, voldoende voorbereid, en koppel tooyour VM voor gebruik:</span><span class="sxs-lookup"><span data-stu-id="9541c-163">Upload your VHD, suitably prepared, and attach tooyour VM for use:</span></span>

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

<span data-ttu-id="9541c-164">Ten slotte uw virtuele machine maken en definiëren van Hallo type tooutilize Azure hybride gebruik voordeel licentieverlening:</span><span class="sxs-lookup"><span data-stu-id="9541c-164">Finally, create your VM and define hello licensing type tooutilize Azure Hybrid Use Benefit:</span></span>

<span data-ttu-id="9541c-165">Voor WindowsServer:</span><span class="sxs-lookup"><span data-stu-id="9541c-165">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a><span data-ttu-id="9541c-166">Een virtuele-machineschaalset ingesteld via Resource Manager-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="9541c-166">Deploy a virtual machine scale set via Resource Manager template</span></span>
<span data-ttu-id="9541c-167">Binnen de VMSS Resource Manager-sjablonen, een extra parameter voor `licenseType` moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9541c-167">Within your VMSS Resource Manager templates, an additional parameter for `licenseType` must be specified.</span></span> <span data-ttu-id="9541c-168">U kunt meer lezen over [Azure Resource Manager-sjablonen ontwerpen](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9541c-168">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="9541c-169">De eigenschap Resource Manager template tooinclude hello licenseType bewerken als onderdeel van Hallo scale set virtualMachineProfile en implementeren van uw sjabloon als normale - Zie het voorbeeld hieronder met installatiekopie van Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="9541c-169">Edit your Resource Manager template tooinclude hello licenseType property as part of hello scale set’s virtualMachineProfile and deploy your template as normal - see example below using 2016 Windows Server image:</span></span>


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> <span data-ttu-id="9541c-170">Ondersteuning voor het implementeren van een virtuele-machineschaalset AHUB voordelen via PowerShell en andere SDK-hulpprogramma's in te stellen is binnenkort beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="9541c-170">Support for deploying a virtual machine scale set with AHUB benefits through PowerShell and other SDK tools is coming soon.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="9541c-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9541c-171">Next steps</span></span>
<span data-ttu-id="9541c-172">Lees meer over [Azure hybride gebruik voordeel licentieverlening](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="9541c-172">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

<span data-ttu-id="9541c-173">Meer informatie over [met Resource Manager-sjablonen](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9541c-173">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="9541c-174">Meer informatie over [Azure hybride gebruik voordeel en Azure Site Recovery kunt migreren toepassingen tooAzure nog meer rendabele](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span><span class="sxs-lookup"><span data-stu-id="9541c-174">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications tooAzure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span></span>
