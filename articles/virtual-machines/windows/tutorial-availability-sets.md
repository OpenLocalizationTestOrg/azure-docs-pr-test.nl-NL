---
title: aaaAvailability zelfstudie ingesteld voor Windows-machines in Azure | Microsoft Docs
description: Meer informatie over Hallo beschikbaarheid Sets voor Windows-machines in Azure.
documentationcenter: 
services: virtual-machines-windows
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
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Hoe toouse beschikbaarheidssets

In deze zelfstudie leert u hoe tooincrease Hallo beschikbaarheid en betrouwbaarheid van uw virtuele Machine-oplossingen in Azure met een mogelijkheid Beschikbaarheidssets aangeroepen. Beschikbaarheidssets Zorg ervoor dat u implementeert op Azure VM's zijn verdeeld over meerdere geïsoleerde hardware clusters Hallo. Dit zorgt ervoor dat als een storing hardware of software in Azure gebeurt, van invloed op een onderliggende reeks uw virtuele machines die uw algehele oplossing blijft beschikbaar en operationele vanuit het oogpunt van uw klanten die gebruikmaken van het Hallo van. 

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Een beschikbaarheidsset maken
> * Een virtuele machine in een beschikbaarheidsset maken
> * Controleer de beschikbare grootten voor virtuele machine

Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger. Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie. Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).

## <a name="availability-set-overview"></a>Overzicht van de beschikbaarheidsset

Een Beschikbaarheidsset, is een logische groepering-functie die u kunt gebruiken in Azure tooensure dat Hallo VM resources die u in het plaatsen van elkaar geïsoleerd zijn wanneer ze zijn geïmplementeerd in een Azure-datacenter. Azure zorgt ervoor dat Hallo virtuele machines die u binnen een Beschikbaarheidsset uitvoeren op meerdere fysieke servers plaatst, compute rekken eenheden voor opslag en netwerkswitches. Dit zorgt ervoor dat in geval van een softwarestoring van de Azure-of hardware Hallo slechts een subset van uw virtuele machines worden beïnvloed en uw algehele toepassing blijft en doorgaan toobe beschikbaar tooyour klanten. Gebruik Beschikbaarheidssets is een tooleverage essentiële mogelijkheden als u wilt dat toobuild betrouwbare cloudoplossingen.

Laten we eens een typische VM-oplossing op basis van waar u mogelijk 4 front-end-webservers en 2 back-end virtuele machines die een database te hosten. Met Azure, kunt u twee beschikbaarheidssets toodefine voordat u uw virtuele machines implementeren: één beschikbaarheid instellen voor Hallo 'web' laag en een beschikbaarheidsset voor Hallo 'database' laag. Bij het maken van een nieuwe virtuele machine vervolgens u Hallo beschikbaarheid instellen opgeven kunt als een parameter toohello az vm-opdracht maken en Azure zorgt u dat Hallo virtuele machines die u binnen Hallo beschikbaar maken automatisch worden ingesteld op de resources van meerdere fysieke hardware geïsoleerd. Dit betekent dat als Hallo fysieke hardware die een van uw webserver of VM's Database-Server wordt uitgevoerd op een probleem, u dat Hallo weet andere exemplaren van uw webserver en de Database virtuele machines blijven actief probleemloos omdat ze op andere hardware.

Als u wilt dat toodeploy betrouwbare VM op basis van oplossingen in Azure, moet u altijd Beschikbaarheidssets gebruiken.

## <a name="create-an-availability-set"></a>Een beschikbaarheidsset maken

Kunt u een beschikbaarheidsset met [nieuw AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). In dit voorbeeld we beide Hallo aantal update en fouttolerantie domeinen op instellen *2* voor Hallo beschikbaarheidsset benoemde *myAvailabilitySet* in Hallo *myResourceGroupAvailability*resourcegroep.

Maak een resourcegroep.

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a>Virtuele machines in een beschikbaarheidsset maken

Virtuele machines moeten toobe in Hallo beschikbaarheid set toomake zeker van te zijn dat ze correct zijn verdeeld over Hallo hardware hebt gemaakt. U kunt een bestaande VM tooan beschikbaarheidsset nadat deze is gemaakt niet toevoegen. 

Hallo hardware op een locatie is onderverdeeld in toomultiple update domeinen en domeinen met fouten. Een **updatedomein** is een groep VM's en de onderliggende fysieke hardware die kan worden opgestart op Hallo hetzelfde moment. Virtuele machines in dezelfde Hallo **foutdomein** algemene storage, evenals een gemeenschappelijk power-bron- en switch delen. 

Wanneer u een virtuele machine met behulp van de configuratie maakt [nieuw AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) u Hallo beschikbaarheid instellen met behulp van Hallo opgeven `-AvailabilitySetId` toospecify Hallo-ID van weergaveparameter van Hallo beschikbaarheidsset.

Maken van 2 virtuele machines met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in Hallo beschikbaarheid instellen.

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

Het duurt enkele minuten toocreate en beide VM's configureren. Wanneer u klaar bent, hebt u 2 virtuele machines die zijn verdeeld over de onderliggende hardware Hallo. 

## <a name="check-for-available-vm-sizes"></a>Controleren op beschikbare VM-grootten 

U kunt meer virtuele machines toohello beschikbaarheidsset later toevoegen, maar u moet tooknow welke VM-grootten zijn beschikbaar op Hallo hardware. Gebruik [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist alle beschikbare grootten van Hallo op Hallo hardware-cluster voor Hallo beschikbaarheidsset.

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> * Een beschikbaarheidsset maken
> * Een virtuele machine in een beschikbaarheidsset maken
> * Controleer de beschikbare grootten voor virtuele machine

Toohello volgende zelfstudie toolearn over virtuele-machineschaalsets gaan.

> [!div class="nextstepaction"]
> [Een VM-schaalset maken](tutorial-create-vmss.md)


