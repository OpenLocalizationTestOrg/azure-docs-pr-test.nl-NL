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
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a>Azure hybride gebruik voordeel voor WindowsServer en Windows-Client
Voor klanten met Software Assurance Azure hybride gebruik Benefit kunt u toouse uw lokale Windows Server en Windows-Client licenties en voer Windows virtuele machines in Azure tegen lagere kosten. Azure hybride gebruik voordeel voor Windows Server omvat Windows Server 2008 R2, Windows Server 2012, Windows Server 2012R2 en Windows Server 2016. Azure hybride gebruik voordeel voor Windows-Client omvat Windows 10. Zie voor meer informatie Hallo [Azure hybride gebruik voordeel licentieverlening pagina](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

>[!IMPORTANT]
>Azure hybride gebruik voordelen voor Windows-Client is momenteel in Preview met Windows 10 Hallo installatiekopie in hello Azure Marketplace. Alleen zakelijke klanten met Windows 10 Enterprise E3/E5 per gebruiker of Windows VDA per gebruiker (abonnement gebruikerslicenties of abonnement voor extra gebruikerslicenties) ('in aanmerking komende licenties') in aanmerking komen.
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a>Manieren toouse Azure hybride gebruik Benefit
Er zijn een aantal verschillende manieren toodeploy VM's van Windows Hello Azure hybride gebruik voordeel:

1. U kunt virtuele machines van [specifieke Marketplace-installatiekopieën](#deploy-a-vm-using-the-azure-marketplace) die vooraf is geconfigureerd met Azure hybride gebruik voordeel - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 en Windows Server 2008SP1 zijn.
2. U kunt [uploaden van een aangepaste VM](#upload-a-windows-vhd) en [implementeren met behulp van een Resource Manager-sjabloon](#deploy-a-vm-via-resource-manager) of [Azure PowerShell](#detailed-powershell-deployment-walkthrough).

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a>Een virtuele machine geïmplementeerd met hello Azure Marketplace
Volgende installatiekopieën zijn beschikbaar in Hallo Marketplace vooraf geconfigureerd met Azure hybride gebruik voordeel: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 en Windows Server 2008SP1. Deze installatiekopieën kunnen rechtstreeks vanuit hello Azure-portal, Resource Manager-sjablonen of Azure PowerShell worden geïmplementeerd.

U kunt deze installatiekopieën rechtstreeks vanuit hello Azure-portal kunt implementeren. Voor gebruik in het Resource Manager-sjablonen en met Azure PowerShell, Hallo lijst weergeven met afbeeldingen als volgt:

Voor WindowsServer:
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- 2016 Datacenter versie 2016.127.20170406 of hoger

- 2012-R2-Datacenter versie 4.127.20170406 of hoger

- 2012 Datacenter versie 3.127.20170406 of hoger

- 2008 R2 SP1-versie 2.127.20170406 of hoger

Voor Windows-Client:
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a>Een WindowsServer-VHD uploaden
toodeploy een Windows Server-VM in Azure, moet u eerst een VHD met uw Windows-build base toocreate. Deze VHD moet op de juiste wijze worden voorbereid met Sysprep voordat u deze tooAzure uploaden. U kunt [voor meer informatie over Hallo VHD vereisten en Sysprep-proces](upload-generalized-managed.md) en [Sysprep-ondersteuning voor serverrollen](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles). Back-up Hallo VM voordat Sysprep wordt uitgevoerd. 

Zorg ervoor dat u hebt [geïnstalleerd en geconfigureerd hello nieuwste Azure PowerShell](/powershell/azure/overview). Nadat u uw VHD hebt voorbereid, uploaden Hallo VHD tooyour Azure Storage-account met behulp van Hallo `Add-AzureRmVhd` cmdlet als volgt:

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> Microsoft SQL Server, SharePoint Server en Dynamics kan ook gebruikmaken van uw Software Assurance-licentieverlening. U moet nog steeds tooprepare Hallo de installatiekopie van Windows Server door onderdelen van uw toepassing installeren en dienovereenkomstig licentiesleutels bieden, en vervolgens Hallo schijf installatiekopie tooAzure uploaden. Hallo geschikte documentatie voor het uitvoeren van Sysprep met uw toepassing, zoals lezen [overwegingen voor SQL Server installeren met behulp van Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) of [bouwen van een SharePoint-Server 2016 referentie-installatiekopie (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).
>
>

U kunt ook meer informatie over [Hallo VHD tooAzure proces uploaden](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)


## <a name="deploy-a-vm-via-resource-manager-template"></a>Een virtuele machine via Resource Manager-sjabloon implementeren
In de Resource Manager-sjablonen, een extra parameter voor `licenseType` kan worden opgegeven. U kunt meer lezen over [Azure Resource Manager-sjablonen ontwerpen](../../resource-group-authoring-templates.md). Zodra u uw tooAzure VHD geüpload hebt, bewerk u Resource Manager tooinclude Hallo licentie voor het sjabloontype als onderdeel van Hallo provider berekenen en implementeren van uw sjabloon als normale:

Voor WindowsServer:
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

Voor alleen Windows-Client-toouse met Azure Marketplace-installatiekopie:
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a>Een virtuele machine via PowerShell Quick Start implementeren
Wanneer u uw Windows Server-VM via PowerShell implementeert, hebt u een extra parameter voor `-LicenseType`. Zodra u uw tooAzure VHD geüpload hebt, maakt u een VM met `New-AzureRmVM` en geef een Hallo licentieverlening als volgt:

Voor WindowsServer:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

Voor alleen Windows-Client-toouse met Azure Marketplace-installatiekopie:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

U kunt [lezen van een meer gedetailleerde uitleg over het implementeren van een virtuele machine in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) onderstaande of lezen een meer beschrijvende gids op verschillende stappen te Hallo[maken van een Windows-VM met Resource Manager en PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a>Controleer of uw virtuele machine wordt gebruikt door de licentiegegevens voordeel Hallo
Nadat u uw virtuele machine via Hallo PowerShell of Resource Manager-implementatiemethode hebt geïmplementeerd, controleren of de Hallo licentietype met `Get-AzureRmVM` als volgt:

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

Hallo uitvoer is vergelijkbaar toohello volgt voor Windows Server:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

Deze uitvoer in tegenstelling tot Hallo die volgende VM geïmplementeerd zonder Azure hybride gebruik voordeel-licentieverlening, zoals een virtuele machine rechtstreeks vanuit de galerie van Azure Hallo geïmplementeerd:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a>Gedetailleerd overzicht van de PowerShell-implementatie
Hallo volgende gedetailleerde PowerShell stappen weergeven met een volledige implementatie van een virtuele machine. U kunt meer context lezen als toohello Werkelijke cmdlets en andere onderdelen wordt gemaakt in [maken van een Windows-VM met Resource Manager en PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). U stapsgewijs door het maken van de resourcegroep, storage-account en virtuele netwerken, en vervolgens uw virtuele machine definiëren en ten slotte uw virtuele machine maken.

Eerst veilig referenties verkrijgen, stelt u een locatie en de naam van resourcegroep:

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

Maak een openbare IP-adres:

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

Uw subnet, NIC en VNET definiëren:

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

Naam van uw virtuele machine en maak een VM-configuratie:

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

Definieer uw besturingssysteem:

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Voeg uw NIC toohello VM:

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Hallo storage account toouse definiëren:

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

Upload uw VHD, voldoende voorbereid, en koppel tooyour VM voor gebruik:

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

Ten slotte uw virtuele machine maken en definiëren van Hallo type tooutilize Azure hybride gebruik voordeel licentieverlening:

Voor WindowsServer:
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a>Een virtuele-machineschaalset ingesteld via Resource Manager-sjabloon implementeren
Binnen de VMSS Resource Manager-sjablonen, een extra parameter voor `licenseType` moet worden opgegeven. U kunt meer lezen over [Azure Resource Manager-sjablonen ontwerpen](../../resource-group-authoring-templates.md). De eigenschap Resource Manager template tooinclude hello licenseType bewerken als onderdeel van Hallo scale set virtualMachineProfile en implementeren van uw sjabloon als normale - Zie het voorbeeld hieronder met installatiekopie van Windows Server 2016:


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
> Ondersteuning voor het implementeren van een virtuele-machineschaalset AHUB voordelen via PowerShell en andere SDK-hulpprogramma's in te stellen is binnenkort beschikbaar.
>

## <a name="next-steps"></a>Volgende stappen
Lees meer over [Azure hybride gebruik voordeel licentieverlening](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

Meer informatie over [met Resource Manager-sjablonen](../../azure-resource-manager/resource-group-overview.md).

Meer informatie over [Azure hybride gebruik voordeel en Azure Site Recovery kunt migreren toepassingen tooAzure nog meer rendabele](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).
