---
title: Windows virtuele Machines en virtuele netwerken in Azure | Microsoft Docs
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
ms.openlocfilehash: c71c07f8ecd123a7e27848ba5043d46e315fcf03
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a>Virtuele Azure-netwerken en virtuele Machines van Windows met Azure PowerShell beheren

Azure netwerken virtuele Azure-machines gebruiken voor interne en externe communicatie. In deze zelfstudie maakt u meerdere virtuele machines (VM's) in een virtueel netwerk maken en netwerkconnectiviteit tussen deze twee configureren. Procedures voor:

> [!div class="checklist"]
> * Een virtueel netwerk maken
> * Subnetten virtueel netwerk maken
> * Het netwerkverkeer met Netwerkbeveiligingsgroepen
> * Regels voor het netwerkverkeer in actie weergeven

Voor deze zelfstudie is moduleversie 3,6 of hoger van Azure PowerShell vereist. Voer ` Get-Module -ListAvailable AzureRM` uit om de versie te bekijken. Als u upgraden wilt, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).

## <a name="create-vnet"></a>VNet maken

Een VNet is een weergave van uw eigen netwerk in de cloud. Een VNet is een logische isolatie van de Azure-cloud toegewezen aan uw abonnement. U vindt subnetten, regels voor verbinding met deze subnetten en verbindingen van de virtuele machines naar de subnetten binnen een VNet.

Voordat u alle andere Azure-resources maken kunt, moet u een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Het volgende voorbeeld wordt een resourcegroep met de naam *myRGNetwork* in de *EastUS* locatie:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

Een subnet is een onderliggende resource van een VNet en helpt bij het segmenten van adresruimten binnen een CIDR-blok met behulp van IP-adresvoorvoegsels definiëren. NIC's worden toegevoegd aan subnetten en verbonden met virtuele machines, tegelijk connectiviteit biedt voor verschillende werkbelastingen.

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

Voor een virtuele machine om te communiceren in een VNet, moet de virtuele netwerkinterface (NIC). De *myFrontendVM* is toegankelijk vanuit het internet, dus u moet ook een openbaar IP-adres. 

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

Stel de gebruikersnaam en wachtwoord nodig voor de administrator-account op de virtuele machine met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Maken van het VMs met een [nieuwe AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), en [nieuwe-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). 

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

U kunt IIS installeren op *myFrontendVM* met behulp van een extern bureaublad-sessiehost. U moet het openbare IP-adres van de virtuele machine om deze te openen.

U kunt het openbare IP-adres ophalen *myFrontendVM* met [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Het volgende voorbeeld verkrijgt het IP-adres voor *myPublicIPAddress* eerder hebt gemaakt:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

Noteer dit IP-adres zodat u deze in toekomstige stappen gebruiken kunt.

Gebruik de volgende opdracht voor het maken van een extern-bureaubladsessie met *myFrontendVM*. Vervang  *<publicIPAddress>*  met het adres dat u eerder hebt genoteerd. Voer desgevraagd de referenties die worden gebruikt bij het maken van de virtuele machine.

```
mstsc /v:<publicIpAddress>
``` 

Nu dat u zich hebt aangemeld bij *myFrontendVM*, kunt u één regel PowerShell IIS installeren en activeren van de lokale firewallregel webverkeer toestaan. Open een PowerShell-prompt en voer de volgende opdracht uit:

Gebruik [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) om uit te voeren van de extensie voor aangepaste scripts die de IIS-webserver installeert:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

U kunt nu het openbare IP-adres gebruiken om te bladeren naar de virtuele machine om te zien van de IIS-site.

![Standaardsite van IIS](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a>Interne verkeer beheren

Een netwerkbeveiligingsgroep (NSG) bevat een lijst met regels voor toestaan of weigeren van netwerkverkeer naar bronnen die zijn verbonden met een VNet. Nsg's kunnen worden gekoppeld aan subnetten of afzonderlijke NIC's die zijn gekoppeld aan virtuele machines. Openen of sluiten van toegang tot virtuele machines via poorten wordt gedaan met behulp van NSG-regels. Tijdens het maken van *myFrontendVM*, binnenkomende poort 3389 automatisch voor RDP-verbinding is geopend.

Interne communicatie van virtuele machines kan worden geconfigureerd met een NSG. In dit gedeelte vindt u informatie over het maken van een ander subnet in het netwerk en een NSG toewijzen aan toe te staan een verbinding van *myFrontendVM* naar *myBackendVM* op poort 1433. Het subnet wordt vervolgens toegewezen aan de virtuele machine wanneer deze wordt gemaakt.

U kunt interne verkeer beperkt tot *myBackendVM* alleen *myFrontendVM* door het maken van een NSG voor het subnet voor back-end. Het volgende voorbeeld wordt een NSG regel voor licentiecontrole *myBackendNSGRule* met [nieuw AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):

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

Add *myBackEndSubnet* naar *myVNet* met [toevoegen AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):

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

Er is de eenvoudigste manier om de back-end virtuele machine maken met behulp van een installatiekopie van SQL Server. Deze zelfstudie alleen de virtuele machine maakt met de database-server, maar geen biedt informatie over het openen van de database.

Maak *myBackendNic*:

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

De gebruikersnaam en wachtwoord nodig voor het beheerdersaccount op de virtuele machine met Get-Credential instellen:

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

De afbeelding die wordt gebruikt SQL Server is geïnstalleerd, maar niet in deze zelfstudie wordt gebruikt. Het is opgenomen om weer te geven hoe u een virtuele machine voor het afhandelen van webverkeer en een virtuele machine voor het afhandelen van database-beheer kunt configureren.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt gemaakt en beveiligd Azure-netwerken met betrekking tot virtuele machines. 

> [!div class="checklist"]
> * Een virtueel netwerk maken
> * Subnetten virtueel netwerk maken
> * Het netwerkverkeer met Netwerkbeveiligingsgroepen
> * Regels voor het netwerkverkeer in actie weergeven

Ga naar de volgende zelfstudie voor meer informatie over het controleren van het beveiligen van gegevens op virtuele machines met behulp van Azure backup. .

> [!div class="nextstepaction"]
> [Back-up van Windows virtuele machines in Azure](./tutorial-backup-vms.md)
