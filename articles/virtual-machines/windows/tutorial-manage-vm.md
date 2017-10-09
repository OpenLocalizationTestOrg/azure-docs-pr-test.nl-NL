---
title: aaaCreate en Windows virtuele machines beheren met Azure PowerShell-module Hallo | Microsoft Docs
description: Zelfstudie - maken en beheren van Windows virtuele machines met hello Azure PowerShell-module
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a>Maken en beheren van Windows virtuele machines met hello Azure PowerShell-module

Virtuele machines van Azure bieden een volledig worden geconfigureerd en flexibele computeromgeving. Deze zelfstudie bevat informatie over basic virtuele machine van Azure-implementatie items zoals het selecteren van een VM-grootte, een VM-installatiekopie te selecteren en implementeren van een virtuele machine. Procedures voor:

> [!div class="checklist"]
> * Maken en koppelen tooa VM
> * Selecteer en gebruik van VM-installatiekopieën
> * Weergeven en gebruiken van specifieke VM-grootten
> * De grootte van een virtuele machine wijzigen
> * Bekijken en te begrijpen status virtuele machine

Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger. Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie. Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).

## <a name="create-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) opdracht. 

Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. Een resourcegroep moet worden gemaakt voordat een virtuele machine. In dit voorbeeld wordt een resourcegroep met de naam *myResourceGroupVM* wordt gemaakt in Hallo *EastUS* regio. 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

Hallo-resourcegroep is opgegeven bij het maken of wijzigen van een virtuele machine die in deze zelfstudie kan worden gezien.

## <a name="create-virtual-machine"></a>Virtuele machine maken

Een virtuele machine moet worden verbonden tooa virtueel netwerk. U communiceren met de Hallo virtuele machine via een openbaar IP-adres via een netwerkinterfacekaart.

### <a name="create-virtual-network"></a>Virtueel netwerk maken

Maak een subnet met [nieuw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

Maak een virtueel netwerk met [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a>Openbare IP-adres maken

Maken van een openbaar IP-adres met [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a>Maken van netwerkinterfacekaart

Maken van een netwerkkaart met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a>Netwerkbeveiligingsgroep maken

Een Azure [netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md) (NSG) Hiermee wordt bepaald binnenkomend en uitgaand verkeer voor een of meer virtuele machines. Netwerkbeveiligingsgroepen toestaan of weigeren van netwerkverkeer op een specifieke poort of een poortbereik. Deze regels kunnen ook een voorvoegsel voor bronadres bevatten, zodat alleen verkeer dat afkomstig is op een vooraf gedefinieerde bron met een virtuele machine communiceren kan. tooaccess hello IIS webserver die u installeert, moet u een inkomende NSG-regel toevoegen.

gebruik van een inkomende regel voor het NSG toocreate [toevoegen AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig). Hallo volgende voorbeeld maakt u een NSG regel voor licentiecontrole *myNSGRule* opent die poort *3389* voor Hallo virtuele machine:

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

Maak Hallo NSG met *myNSGRule* met [nieuw AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

Hallo NSG toohello subnet toevoegen in virtueel netwerk met Hallo [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

Update Hallo virtueel netwerk met [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a>Virtuele machine maken

Wanneer u een virtuele machine maakt, er zijn diverse opties beschikbaar zoals besturingssysteemkopie schijf sizing en administratieve referenties. In dit voorbeeld wordt een virtuele machine gemaakt met de naam *myVM* Hallo meest recente versie van Windows Server 2016 Datacenter.

Stel Hallo-gebruikersnaam en wachtwoord nodig voor Hallo-beheerdersaccount op Hallo virtuele machine met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Hallo initiële configuratie maken voor Hallo virtuele machine met [nieuw AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

Toevoegen van Hallo besturingssysteem informatie toohello Virtuele-machineconfiguratie met [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Toevoegen van Hallo installatiekopie informatie toohello Virtuele-machineconfiguratie met [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

Toevoegen van Hallo besturingssysteem schijf instellingen toohello Virtuele-machineconfiguratie met [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

Add Hallo-netwerkinterfacekaart die u eerder hebt gemaakt toohello Virtuele-machineconfiguratie met [toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Maak Hallo virtuele machine met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a>Verbinding maken met tooVM

Nadat het Hallo-implementatie is voltooid, maakt u een verbinding met extern bureaublad met Hallo virtuele machine.

Hallo volgende opdrachten tooreturn Hallo openbare IP-adres van Hallo virtuele machine worden uitgevoerd. Noteer dit IP-adres zodat tooit verbinding met uw browser tootest webverbindingen mogelijk in een toekomstige stap maken kunnen.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

Gebruik Hallo volgende opdracht toocreate een extern-bureaubladsessie met Hallo virtuele machine. Hallo IP-adres vervangen door Hallo *publicIPAddress* van uw virtuele machine. Wanneer u wordt gevraagd, voert u Hallo-referenties gebruikt bij het maken van Hallo virtuele machine.

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a>VM-installatiekopieën begrijpen

Hello Azure marketplace bevat veel installatiekopieën van virtuele machines die gebruikt toocreate een nieuwe virtuele machine worden kunnen. In de vorige stappen hello, is een virtuele machine gemaakt met installatiekopie van Windows Server 2016-Datacenter Hallo. In deze stap is Hallo PowerShell-module gebruikte toosearch Hallo marketplace voor andere Windows-installatiekopieën ook als basis voor de nieuwe virtuele machines kunnen. Dit proces bestaat uit het Hallo-uitgever, aanbieding en Hallo installatiekopie met de naam (Sku) te zoeken. 

Gebruik Hallo [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) opdracht tooreturn een lijst van uitgevers van de installatiekopie.  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

Gebruik Hallo [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn een lijst met aanbiedingen van de installatiekopie. Met deze opdracht Hallo geretourneerd lijst wordt gefilterd op Hallo opgegeven uitgever. 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

Hallo [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) opdracht wordt vervolgens filteren op Hallo publisher en de aanbieding naam tooreturn een lijst met namen van afbeeldingen.

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

Deze informatie kan worden gebruikt toodeploy een virtuele machine met een specifieke installatiekopie. In het volgende voorbeeld wordt de naam van de installatiekopie Hallo op Hallo VM-object. Raadpleeg de eerdere voorbeelden toohello in deze zelfstudie voor volledige implementatiestappen.

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a>VM-grootten begrijpen

De grootte van een virtuele machine bepaalt Hallo hoeveelheid rekenresources zoals CPU en GPU geheugen die beschikbaar toohello virtuele machine zijn aangebracht. Toobe gemaakt met een grootte geschikt voor Hallo werkbelasting verwacht, moeten virtuele machines. Als de werkbelasting toeneemt, kan een bestaande virtuele machine kan worden gewijzigd.

### <a name="vm-sizes"></a>VM-grootten

Hallo tabel categoriseert grootten in gebruiksvoorbeelden.  

| Type                     | Grootten           |    Beschrijving       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Algemeen doel         |DSv2, Dv2, DS, D, Av2, A0 7| Taakverdeling CPU-naar-geheugen. Ideaal voor dev / test- en kleine toomedium toepassingen en gegevens oplossingen.  |
| Geoptimaliseerde rekenkracht      | FS, F             | Hoog CPU-naar-geheugen. Goede voor gemiddeld verkeer toepassingen, netwerkapparatuur en batchprocessen.        |
| Geoptimaliseerd geheugen       | GS, G, DSv2, DS, Dv2, D   | Hoge geheugen-naar-core. Ideaal voor relationele databases, gemiddeld toolarge caches en in het geheugen analytics.                 |
| Geoptimaliseerde opslag       | Ls                | Snelle doorvoer van schijfgegevens en IO. Ideaal voor big data-, SQL- en NoSQL-databases.                                                         |
| GPU           | NV, NC            | Gespecialiseerde VMs gericht voor zware grafische weergave en het bewerken van video's.       |
| Hoge prestaties | H, A8 11          | De krachtigste CPU VMs met optionele hoge gegevensdoorvoer netwerkinterfaces (RDMA). 


### <a name="find-available-vm-sizes"></a>Zoeken naar beschikbare VM-grootten

een lijst met VM toosee groottes beschikbaar in een bepaalde regio, gebruikt u Hallo [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) opdracht.

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a>De grootte van een virtuele machine wijzigen

Nadat een virtuele machine is geïmplementeerd, kan het formaat is gewijzigd tooincrease of resourcetoewijzing verlagen.

Voordat het formaat van een virtuele machine, controleren als hello gewenste grootte beschikbaar op Hallo huidige VM-cluster is. Hallo [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) opdracht retourneert een lijst met grootten. 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

Desgewenst Hallo grootte is beschikbaar kan hello VM worden gewijzigd vanuit een status ingeschakeld op maar deze opnieuw wordt opgestart tijdens het Hallo-bewerking.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

Desgewenst Hallo grootte is niet op Hallo huidig cluster Hallo VM behoeften toobe ongedaan voordat Hallo vergroten of verkleinen van de bewerking kan zich voordoen. Houd er rekening mee wanneer Hallo VM weer is ingeschakeld, worden alle gegevens op de tijdelijke schijf Hallo verwijderd en Hallo openbaar IP-adres wijzigen tenzij u een statisch IP-adres wordt gebruikt. 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a>VM-energiestatus

Een Azure VM kan een van de vele energiestatussen hebben. Deze status vertegenwoordigt de huidige status Hallo Hallo VM Hallo verwerkt Hallo hypervisor. 

### <a name="power-states"></a>Energiestatus

| Energieniveau | Beschrijving
|----|----|
| Starting | Hiermee wordt aangegeven op Hallo virtuele machine wordt gestart. |
| Running | Hiermee wordt aangegeven dat de Hallo virtuele machine wordt uitgevoerd. |
| Stopping | Hiermee wordt aangegeven dat de virtuele machine hello wordt gestopt. | 
| Stopped | Geeft aan dat de virtuele machine Hallo is gestopt. Houd er rekening mee dat virtuele machines in de status gestopt Hallo nog steeds compute worden kosten in rekening.  |
| Toewijzing | Hiermee wordt aangegeven dat de virtuele machine hello wordt opgeheven. |
| De toewijzing ongedaan gemaakt | Hiermee wordt aangegeven dat de virtuele machine hello wordt volledig verwijderd uit Hallo hypervisor maar nog steeds beschikbaar in vlak voor Hallo-besturingselement. Virtuele machines in Hallo Deallocated status kan niet worden compute-kosten in rekening. |
| - | Geeft aan dat de energiestatus Hallo van Hallo virtuele machine onbekend. |

### <a name="find-power-state"></a>Energieniveau vinden

tooretrieve hello status van een bepaalde virtuele machine, gebruik Hallo [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) opdracht. Niet zeker toospecify een geldige naam voor een virtuele machine en de resourcegroep. 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

Uitvoer:

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a>Beheertaken

Tijdens het Hallo-levensduur van een virtuele machine kunt u beheertaken toorun zoals starten, stoppen of een virtuele machine wordt verwijderd. U kunt bovendien toocreate scripts tooautomate herhalende of complexe taken. Met Azure PowerShell, kunnen veel algemene beheertaken worden uitgevoerd vanaf de opdrachtregel hello, hetzij in scripts.

### <a name="stop-virtual-machine"></a>Virtuele machine stoppen

Stop en toewijzing van een virtuele machine met [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

Als u tookeep Hallo virtuele machine in een ingerichte staat wilt, gebruikt u Hallo StayProvisioned - parameter.

### <a name="start-virtual-machine"></a>Virtuele machine starten

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a>Verwijderen van resourcegroep

Verwijderen van een resourcegroep, worden ook alle resources binnen verwijderd.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd over basic VM maken en beheren zoals het:

> [!div class="checklist"]
> * Maken en koppelen tooa VM
> * Selecteer en gebruik van VM-installatiekopieën
> * Weergeven en gebruiken van specifieke VM-grootten
> * De grootte van een virtuele machine wijzigen
> * Bekijken en te begrijpen status virtuele machine

Ga toohello volgende zelfstudie toolearn over VM-schijven.  

> [!div class="nextstepaction"]
> [Maken en beheren van VM-schijven](./tutorial-manage-data-disk.md)
