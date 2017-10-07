---
title: Quick Start - aaaAzure maken Windows VM PowerShell | Microsoft Docs
description: Snel een virtuele Windows-machines met PowerShell meer toocreate
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a>Een virtuele Windows-machine maken met PowerShell

Hello Azure PowerShell-module is gebruikte toocreate en Azure-resources te beheren vanaf Hallo PowerShell-opdrachtregel of in scripts. Deze handleiding gegevens met behulp van PowerShell toocreate en Azure virtuele machine met Windows Server 2016. Zodra de implementatie is voltooid, we toohello server verbinden en IIS installeren.  

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

Deze snel starten vereist hello Azure PowerShell-moduleversie 3,6 of hoger. Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).

## <a name="log-in-tooazure"></a>Meld u bij tooAzure

Meld u bij de Azure-abonnement met Hallo tooyour `Login-AzureRmAccount` opdracht in en volg Hallo op het scherm instructies.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Een resourcegroep maken

Maak een Azure-resourcegroep met de opdracht [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a>Netwerkresources maken

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a>Maak een virtueel netwerk, subnet en een openbaar IP-adres. 
Deze resources zijn gebruikte tooprovide network connectivity toohello virtuele machine en verbindt u deze toohello internet.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Maak een netwerkbeveiligingsgroep en een regel voor de netwerkbeveiligingsgroep. 
netwerkbeveiligingsgroep Hallo beveiligt Hallo virtuele machine met behulp van regels voor binnenkomende en uitgaande. In dit geval is er een binnenkomende regel gemaakt voor poort 3389, waarmee binnenkomende verbindingen met een extern bureaublad worden toegestaan. Tevens willen we toocreate een inkomende regel voor poort 80, waardoor inkomend webverkeer.

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-hello-virtual-machine"></a>Maak een netwerkkaart voor Hallo virtuele machine. 
Maken van een netwerkkaart met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) voor Hallo virtuele machine. Hallo netwerkkaart verbindt Hallo tooa subnet met virtuele machines, netwerkbeveiligingsgroep en openbare IP-adres.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Virtuele machine maken

Maak een virtuele-machineconfiguratie. Deze configuratie omvat Hallo-instellingen die worden gebruikt bij het implementeren van Hallo virtuele machine, zoals de configuratie van een virtuele machine-installatiekopie, grootte en verificatie. Als deze stap wordt uitgevoerd, wordt u gevraagd referenties op te geven. Hallo-waarden die u invoert worden geconfigureerd als Hallo-gebruikersnaam en wachtwoord voor Hallo virtuele machine.

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

Maak Hallo virtuele machine met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Verbinding maken met toovirtual machine

Nadat het Hallo-implementatie is voltooid, maakt u een verbinding met extern bureaublad met Hallo virtuele machine.

Gebruik Hallo [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) opdracht tooreturn Hallo openbaar IP-adres van Hallo virtuele machine. Noteer dit IP-adres zodat tooit verbinding met uw browser tootest webverbindingen mogelijk in een toekomstige stap maken kunnen.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

Gebruik Hallo volgende opdracht toocreate een extern-bureaubladsessie met Hallo virtuele machine. Hallo IP-adres vervangen door Hallo *publicIPAddress* van uw virtuele machine. Wanneer u wordt gevraagd, voert u Hallo-referenties gebruikt bij het maken van Hallo virtuele machine.

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a>IIS installeren met behulp van PowerShell

Nu dat u hebt geregistreerd in Azure VM toohello, kunt u één regel PowerShell tooinstall IIS gebruiken en Hallo lokale firewall regel tooallow-webverkeer inschakelen. Open een PowerShell-prompt en Hallo volgende opdracht uitvoeren:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Weergave Hallo IIS-welkomstpagina

Met IIS is geïnstalleerd en poort 80 is nu open op de virtuele machine uit Hallo Internet, kunt u een webbrowser van uw keuze tooview Hallo IIS standaardwelkomstpagina. Ervoor toouse Hallo worden *publicIpAddress* u hiervoor toovisit Hallo standaardpagina beschreven. 

![Standaardsite van IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Resources opschonen

Wanneer deze niet langer nodig is, kunt u Hallo [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

In deze Snel starten hebt u een eenvoudige virtuele machine geïmplementeerd, een netwerkbeveiligingsgroepregel gemaakt en een webserver geïnstalleerd. toolearn meer informatie over virtuele machines in Azure, blijven toohello zelfstudie voor VM's van Windows.

> [!div class="nextstepaction"]
> [Zelfstudies over virtuele Windows-machines](./tutorial-manage-vm.md)
