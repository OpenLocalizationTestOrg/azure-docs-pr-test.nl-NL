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
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a>Maken van een aangepaste installatiekopie van een virtuele machine in Azure met behulp van PowerShell

Aangepaste installatiekopieën zijn zoals marketplace-installatiekopieën, maar u deze zelf maken. Aangepaste installatiekopieën kunnen worden gebruikt toobootstrap configuraties zoals vooraf laden van toepassingen, toepassingsconfiguraties en andere configuraties OS. In deze zelfstudie maakt u uw eigen aangepaste installatiekopie van een virtuele machine van Azure. Procedures voor:

> [!div class="checklist"]
> * Sysprep en generalize van virtuele machines
> * Een aangepaste installatiekopie maken
> * Een virtuele machine van een aangepaste installatiekopie maken
> * Lijst van alle Hallo-installatiekopieën in uw abonnement
> * Een afbeelding verwijderen

Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger. Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie. Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).

## <a name="before-you-begin"></a>Voordat u begint

Hallo stappen hieronder wordt beschreven hoe tootake een bestaande virtuele machine en schakel dit in een herbruikbare aangepaste installatiekopie die u hebt de nieuwe VM-instanties toocreate kunnen gebruiken.

toocomplete hello voorbeeld in deze zelfstudie, moet u een bestaande virtuele machine hebben. Indien nodig, dit [voorbeeldscript](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) kunt maken voor u. Wanneer werkende Hallo-zelfstudie vervangt benoemt Hallo resourcegroep en de VM waar nodig.

## <a name="prepare-vm"></a>Virtuele machine voorbereiden

toocreate een installatiekopie van een virtuele machine, moet u tooprepare Hallo VM door het generaliseren Hallo VM, toewijzing en het vervolgens markeren Hallo bron-VM als gegeneraliseerd in Azure.

### <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalize Hallo van virtuele machine van Windows met behulp van Sysprep

Sysprep verwijdert alle persoonlijke gegevens over uw account, onder andere en bereidt Hallo machine toobe gebruikt als een installatiekopie. Zie voor meer informatie over Sysprep [hoe tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).


1. Verbinding maken met toohello virtuele machine.
2. Hallo-opdrachtpromptvenster open als beheerder. Hallo directory ook wijzigen*%windir%\system32\sysprep*, en voer vervolgens *sysprep.exe*.
3. In Hallo **hulpprogramma voor systeemvoorbereiding** dialoogvenster, *System Voer Out-of-Box Experience (OOBE)*, en zorg ervoor dat Hallo *Generalize* selectievakje is ingeschakeld.
4. In **afsluitopties**, selecteer *afsluiten* en klik vervolgens op **OK**.
5. Wanneer Sysprep is voltooid, afgesloten Hallo virtuele machine. **Hallo VM niet opnieuw**.

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Toewijzing ongedaan maken en Hallo VM zoals gegeneraliseerd markeren

een installatiekopie van een toocreate, Hallo VM moet toobe toewijzing ongedaan gemaakt en is gemarkeerd als gegeneraliseerd in Azure.

Hallo toewijzing ongedaan is gemaakt met behulp van VM [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

Hallo-status van Hallo virtuele machine te instellen`-Generalized` met [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm). 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a>Hallo installatiekopie maken

Nu u een installatiekopie van Hallo VM maken met behulp van kunt [nieuw AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) en [nieuw AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage). Hallo volgende voorbeeld wordt een installatiekopie met de naam *myImage* van een virtuele machine met de naam *myVM*.

Hallo virtuele machine worden opgehaald. 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

Hallo imageconfiguratie maken.

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

Hallo-installatiekopie kan maken.

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a>Virtuele machines uit Hallo installatiekopie maken

Nu dat u een installatiekopie hebt, kunt u een of meer nieuwe virtuele machines kunt maken van Hallo image. Maken van een virtuele machine van een aangepaste installatiekopie is heel vergelijkbaar toocreating een VM die gebruikmaakt van een Marketplace-installatiekopie. Wanneer u een Marketplace-installatiekopie gebruikt, hebt u tooinformation over Hallo-installatiekopie, afbeeldingenprovider, aanbieding, SKU en versie. Met een aangepaste installatiekopie hoeft u alleen tooprovide Hallo-ID van de aangepaste Afbeeldingsbron Hallo. 

Hallo script volgen, maken we een variabele *$image* toostore informatie over het gebruik van de aangepaste installatiekopie Hallo [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) en vervolgens gebruiken we [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)en met behulp van Hallo Hallo-ID opgeven *$image* variabele we zojuist hebben gemaakt. 

Hallo script maakt een virtuele machine met de naam *myVMfromImage* van onze aangepaste installatiekopie in een nieuwe resourcegroep met de naam *myResourceGroupFromImage* in Hallo *VS-West* locatie.


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

## <a name="image-management"></a>Beheer van installatiekopieën 

Hier volgen enkele voorbeelden van algemene beheertaken voor de installatiekopie en hoe toocomplete ze met behulp van PowerShell.

Lijst van alle installatiekopieën op naam.

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

Een afbeelding verwijderen. In dit voorbeeld verwijderingen Hallo installatiekopie met de naam *myOldImage* van Hallo *myResourceGroup*.

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt u een aangepaste installatiekopie van de virtuele machine gemaakt. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Sysprep en generalize van virtuele machines
> * Een aangepaste installatiekopie maken
> * Een virtuele machine van een aangepaste installatiekopie maken
> * Lijst van alle Hallo-installatiekopieën in uw abonnement
> * Een afbeelding verwijderen

Ga toohello volgende zelfstudie toolearn over hoe maximaal beschikbare virtuele machines.

> [!div class="nextstepaction"]
> [Virtuele machines met hoge beschikbaarheid maken](tutorial-availability-sets.md)



