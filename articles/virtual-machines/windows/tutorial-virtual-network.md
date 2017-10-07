---
title: aaaAzure virtuele netwerken en virtuele Machines van Windows | Microsoft Docs
description: Zelfstudie - virtuele Azure-netwerken en virtuele Machines van Windows met Azure PowerShell beheren
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a>Virtuele Azure-netwerken en virtuele Machines van Windows met Azure PowerShell beheren

Azure netwerken virtuele Azure-machines gebruiken voor interne en externe communicatie. In deze zelfstudie maakt u meerdere virtuele machines (VM's) in een virtueel netwerk maken en netwerkconnectiviteit tussen deze twee configureren. Procedures voor:

> [!div class="checklist"]
> * Een virtueel netwerk maken
> * Subnetten virtueel netwerk maken
> * Het netwerkverkeer met Netwerkbeveiligingsgroepen
> * Regels voor het netwerkverkeer in actie weergeven

Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger. Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie. Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).

## <a name="create-vnet"></a>VNet maken

Een VNet is een weergave van uw eigen netwerk in Hallo cloud. Een VNet is een logische isolatie van hello Azure cloud toegewezen tooyour-abonnement. Binnen een VNet vindt u subnetten, regels voor connectiviteit toothose subnetten en verbindingen van Hallo VMs toohello subnetten.

Voordat u een andere Azure-resources maken kunt, moet u toocreate een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myRGNetwork* in Hallo *EastUS* locatie:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

Een subnet is een onderliggende resource van een VNet en helpt bij het segmenten van adresruimten binnen een CIDR-blok met behulp van IP-adresvoorvoegsels definiëren. NIC's kunnen worden toegevoegd, toosubnets en verbonden tooVMs, tegelijk connectiviteit biedt voor verschillende werkbelastingen.

Maak een subnet met [nieuw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

Maak een VNET met de naam *myVNet* met *myFrontendSubnet* met [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a>Front-virtuele machine maken

Voor een VM-toocommunicate in een VNet moet de virtuele netwerkinterface (NIC). Hallo *myFrontendVM* is toegankelijk vanuit Hallo internet, dus u moet ook een openbaar IP-adres. 

Maken van een openbaar IP-adres met [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

Maak een NIC met [nieuwe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

Stel Hallo-gebruikersnaam en wachtwoord nodig voor Hallo-beheerdersaccount op Hallo VM met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Maken van Hallo virtuele machines met [nieuw AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), en [nieuwe-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a>Webserver installeren

U kunt IIS installeren op *myFrontendVM* met behulp van een extern bureaublad-sessiehost. U moet tooget Hallo openbare IP-adres van VM tooaccess Hallo deze.

U krijgt Hallo openbare IP-adres van *myFrontendVM* met [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hallo volgende voorbeeld Hallo IP-adres krijgt voor *myPublicIPAddress* eerder hebt gemaakt:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

Noteer dit IP-adres zodat u deze in toekomstige stappen gebruiken kunt.

Gebruik Hallo volgende opdracht toocreate een extern-bureaubladsessie met *myFrontendVM*. Vervang  *<publicIPAddress>*  met Hallo-adres dat u eerder hebt genoteerd. Voer desgevraagd Hallo referenties gebruikt wanneer u Hallo VM gemaakt.

```
mstsc /v:<publicIpAddress>
``` 

Nu dat u hebt geregistreerd te*myFrontendVM*, kunt u één regel PowerShell tooinstall IIS gebruiken en Hallo lokale firewall regel tooallow-webverkeer inschakelen. Open een PowerShell-prompt en Hallo volgende opdracht uitvoeren:

Gebruik [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun Hallo extensie voor aangepaste scripts die Hallo IIS-webserver installeert:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

U kunt nu Hallo openbare IP-adres toobrowse toohello VM toosee Hallo ISS-site gebruiken.

![Standaardsite van IIS](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a>Interne verkeer beheren

Een netwerkbeveiligingsgroep (NSG) bevat een lijst met regels voor toestaan of weigeren netwerkverkeer tooresources verbonden tooa VNet. Nsg's kunnen worden gekoppeld toosubnets of afzonderlijke NIC's gekoppeld tooVMs. Openen en sluiten tooVMs toegang via poorten wordt gedaan met behulp van NSG-regels. Tijdens het maken van *myFrontendVM*, binnenkomende poort 3389 automatisch voor RDP-verbinding is geopend.

Interne communicatie van virtuele machines kan worden geconfigureerd met een NSG. In deze sectie leest u hoe een ander subnet in Hallo toocreate netwerk en een verbinding van een NSG tooit tooallow toewijzen *myFrontendVM* te*myBackendVM* op poort 1433. Hallo-subnet wordt vervolgens toohello VM toegewezen wanneer deze wordt gemaakt.

U kunt interne verkeer te beperken*myBackendVM* alleen *myFrontendVM* door het maken van een NSG voor subnet van Hallo back-end. Hallo volgende voorbeeld maakt u een NSG regel voor licentiecontrole *myBackendNSGRule* met [nieuw AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

Toevoegen van een netwerkbeveiligingsgroep met de naam *myBackendNSG* met [nieuw AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a>Back-end subnet toevoegen

Add *myBackEndSubnet* te*myVNet* met [toevoegen AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a>Back-end virtuele machine maken

Hallo gemakkelijkste manier toocreate hello die back-end virtuele machine wordt met behulp van een installatiekopie van SQL Server. Deze zelfstudie alleen Hallo VM maakt met de databaseserver hello, maar niet bevatten informatie over het Hallo-database te openen.

Maak *myBackendNic*:

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

Hallo-gebruikersnaam en wachtwoord nodig voor Hallo-beheerdersaccount op Hallo VM met Get-Credential instellen:

```powershell
$cred = Get-Credential
```

Maak *myBackendVM*:

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

Hallo-afbeelding die wordt gebruikt SQL Server is geïnstalleerd, maar niet in deze zelfstudie wordt gebruikt. Het is opgenomen tooshow u hoe u een VM toohandle-webverkeer en het beheer van een VM toohandle databases kunt configureren.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt gemaakt en Azure-netwerken als verwante toovirtual machines beveiligd. 

> [!div class="checklist"]
> * Een virtueel netwerk maken
> * Subnetten virtueel netwerk maken
> * Het netwerkverkeer met Netwerkbeveiligingsgroepen
> * Regels voor het netwerkverkeer in actie weergeven

Ga toohello volgende zelfstudie toolearn over het controleren van het beveiligen van gegevens op virtuele machines met behulp van Azure backup. .

> [!div class="nextstepaction"]
> [Back-up van Windows virtuele machines in Azure](./tutorial-backup-vms.md)
