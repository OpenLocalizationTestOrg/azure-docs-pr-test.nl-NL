---
title: Beschikbaarheidssets zelfstudie voor Windows-machines in Azure | Microsoft Docs
description: Meer informatie over de Beschikbaarheidssets voor Windows-machines in Azure.
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
ms.openlocfilehash: d918362106ef93cf47620e0018d363cd510884b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-availability-sets"></a>Het gebruik van beschikbaarheidssets

In deze zelfstudie leert u hoe u verhoogt de beschikbaarheid en betrouwbaarheid van uw virtuele Machine-oplossingen in Azure met een mogelijkheid Beschikbaarheidssets aangeroepen. Beschikbaarheidssets Zorg ervoor dat de virtuele machines die u implementeert in Azure worden gedistribueerd over meerdere geïsoleerde hardware-clusters. Dit zorgt ervoor dat als een storing hardware of software in Azure gebeurt, van invloed op een onderliggende reeks uw virtuele machines en die uw algehele oplossing blijft beschikbaar en operationele vanuit het perspectief van uw gebruik van klanten. 

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Een beschikbaarheidsset maken
> * Een virtuele machine in een beschikbaarheidsset maken
> * Controleer de beschikbare grootten voor virtuele machine

Voor deze zelfstudie is moduleversie 3,6 of hoger van Azure PowerShell vereist. Voer ` Get-Module -ListAvailable AzureRM` uit om de versie te bekijken. Als u upgraden wilt, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).

## <a name="availability-set-overview"></a>Overzicht van de beschikbaarheidsset

Een Beschikbaarheidsset is een logische groepering-functie die u in Azure gebruiken kunt om ervoor te zorgen dat de VM-resources die u in het plaatsen van elkaar geïsoleerd zijn wanneer ze zijn geïmplementeerd in een Azure-datacenter. Azure zorgt ervoor dat de virtuele machines die u binnen een Beschikbaarheidsset uitvoeren op meerdere fysieke servers plaatst, compute rekken eenheden voor opslag en netwerkswitches. Dit zorgt ervoor dat in het geval van een hardware- of Azure software fout slechts een subset van uw virtuele machines worden beïnvloed en uw algehele toepassing blijft en blijven beschikbaar voor uw klanten. Met behulp van Beschikbaarheidssets is een essentiële functie gebruiken als u wilt om betrouwbare cloudoplossingen te bouwen.

Laten we eens een typische VM-oplossing op basis van waar u mogelijk 4 front-end-webservers en 2 back-end virtuele machines die een database te hosten. Met Azure twee beschikbaarheidssets definiëren voordat u uw virtuele machines implementeert u zou willen: één beschikbaarheidsset voor de laag 'web' en een beschikbaarheidsset voor de laag 'database'. Bij het maken van een nieuwe virtuele machine vervolgens u kunt de beschikbaarheidsset als een parameter voor de vm az opdracht maken en Azure automatisch zorgt u dat de virtuele machines die u in de set beschikbaar maakt zijn geïsoleerd over meerdere fysieke hardware-resources. Dit betekent dat als de fysieke hardware die een van uw webserver of VM's Database-Server wordt uitgevoerd op een probleem is, u kent dat de andere exemplaren van uw webserver en de Database virtuele machines actief probleemloos blijven wordt omdat ze op andere hardware.

U moet altijd Beschikbaarheidssets gebruiken wanneer u wilt implementeren, betrouwbare op basis van VM-oplossingen in Azure.

## <a name="create-an-availability-set"></a>Een beschikbaarheidsset maken

Kunt u een beschikbaarheidsset met [nieuw AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). In dit voorbeeld wordt zowel het aantal update en fouttolerantie domeinen op ingesteld *2* voor de beschikbaarheid van de set met de naam *myAvailabilitySet* in de *myResourceGroupAvailability* resourcegroep.

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

Virtuele machines moeten worden gemaakt binnen de beschikbaarheidsset om ervoor te zorgen dat ze correct zijn verdeeld over de hardware. U kunt een bestaande virtuele machine toevoegen aan een beschikbaarheidsset nadat deze is gemaakt. 

De hardware op een locatie is onderverdeeld meerdere domeinen van de update en domeinen met fouten. Een **updatedomein** is een groep VM's en de onderliggende fysieke hardware die op hetzelfde moment kan worden opgestart. Virtuele machines in dezelfde **foutdomein** algemene storage, evenals een gemeenschappelijk power-bron- en switch delen. 

Wanneer u een virtuele machine met behulp van de configuratie maakt [nieuw AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) opgeven van de beschikbaarheidsset met behulp van de `-AvailabilitySetId` parameter om de ID van de beschikbaarheidsset.

Maken van 2 virtuele machines met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in de beschikbaarheid instellen.

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

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

   # Here is where we specify the availability set
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

Het duurt enkele minuten maken en configureren van beide virtuele machines. Wanneer u klaar bent, hebt u 2 virtuele machines die zijn verdeeld over de onderliggende hardware. 

## <a name="check-for-available-vm-sizes"></a>Controleren op beschikbare VM-grootten 

U kunt meer virtuele machines toevoegen aan de beschikbaarheid later instellen, maar u moet weten welke VM-grootten zijn beschikbaar op de hardware. Gebruik [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) voor een lijst met alle van de beschikbare grootten van de hardware-cluster gebruikt voor de beschikbaarheidsset.

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

Ga naar de volgende zelfstudie voor meer informatie over virtuele-machineschaalsets.

> [!div class="nextstepaction"]
> [Een VM-schaalset maken](tutorial-create-vmss.md)


