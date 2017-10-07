---
title: aaaAzure Quick Start - VM PowerShell maken | Microsoft Docs
description: Snel een virtuele Linux-machines met PowerShell meer toocreate
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a>Een virtuele Linux-machine maken met PowerShell

Hello Azure PowerShell-module is gebruikte toocreate en Azure-resources te beheren vanaf Hallo PowerShell-opdrachtregel of in scripts. Deze handleiding details hello Azure PowerShell-module toodeploy met een virtuele machine met Ubuntu server. Zodra Hallo-server is geïmplementeerd, een SSH-verbinding wordt gemaakt en een NGINX-webserver is geïnstalleerd.

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

Deze snel starten vereist hello Azure PowerShell-moduleversie 3,6 of hoger. Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).

Ten slotte een openbare SSH sleutel met de naam van de Hallo *id_rsa.pub* toobe opgeslagen in Hallo moet *SSH* map van uw Windows-gebruikersprofiel. Zie voor gedetailleerde informatie over het maken van SSH-sleutels voor Azure [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (SSH-sleutels maken voor Azure).

## <a name="log-in-tooazure"></a>Meld u bij tooAzure

Meld u bij de Azure-abonnement met Hallo tooyour `Login-AzureRmAccount` opdracht in en volg Hallo op het scherm instructies.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Een resourcegroep maken

Maak een Azure-resourcegroep met de opdracht [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a>Netwerkresources maken

Maak een virtueel netwerk, subnet en een openbaar IP-adres. Deze resources zijn gebruikte tooprovide network connectivity toohello virtuele machine en verbindt u deze toohello internet.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

Maak een netwerkbeveiligingsgroep en een regel voor de netwerkbeveiligingsgroep. netwerkbeveiligingsgroep Hallo beveiligt Hallo virtuele machine met behulp van regels voor binnenkomende en uitgaande. In dit geval is er een binnenkomende regel gemaakt voor poort 22, waarmee binnenkomende SSH-verbindingen worden toegestaan. Tevens willen we toocreate een inkomende regel voor poort 80, waardoor inkomend webverkeer.

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

Maken van een netwerkkaart met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) voor Hallo virtuele machine. Hallo netwerkkaart verbindt Hallo tooa subnet met virtuele machines, netwerkbeveiligingsgroep en openbare IP-adres.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Virtuele machine maken

Maak een virtuele-machineconfiguratie. Deze configuratie omvat Hallo-instellingen die worden gebruikt bij het implementeren van Hallo virtuele machine, zoals de configuratie van een virtuele machine-installatiekopie, grootte en verificatie.

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

Maak Hallo virtuele machine met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Verbinding maken met toovirtual machine

Nadat het Hallo-implementatie is voltooid, moet u een SSH-verbinding maken met Hallo virtuele machine.

Gebruik Hallo [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) opdracht tooreturn Hallo openbaar IP-adres van Hallo virtuele machine.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

Gebruikte Hallo volgende opdracht uit een systeem met SSH geïnstalleerd, tooconnect toohello virtuele machine. Als op Windows, werkt [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) gebruikte toocreate Hallo verbinding kan worden. 

```bash 
ssh <Public IP Address>
```

Wanneer u wordt gevraagd, Hallo aanmeldingsnaam is *azureuser*. Als u een wachtwoordzin is ingevoerd bij het maken van SSH-sleutels, moet u dit ook tooenter.


## <a name="install-nginx"></a>NGINX installeren

Gebruik Hallo volgende scriptbronnen tooupdate pakket bash en installeer de meest recente NGINX-pakket Hallo. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a>Hallo-NGIX welkomstpagina weergeven

U kunt een webbrowser van uw keuze tooview hello NGINX standaardwelkomstpagina gebruiken van NGINX geïnstalleerd en de poort 80 is nu open op de virtuele machine van de Internet - Hallo. Worden ervoor toouse Hallo openbaar IP-adres die u hiervoor toovisit Hallo standaardpagina beschreven. 

![Standaardsite van NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>Resources opschonen

Wanneer deze niet langer nodig is, kunt u Hallo [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

In deze Snel starten hebt u een eenvoudige virtuele machine geïmplementeerd, een netwerkbeveiligingsgroepregel gemaakt en een webserver geïnstalleerd. toolearn meer informatie over virtuele machines in Azure, blijven toohello zelfstudie voor virtuele Linux-machines.

> [!div class="nextstepaction"]
> [Zelfstudies over virtuele Linux-machines](./tutorial-manage-vm.md)
