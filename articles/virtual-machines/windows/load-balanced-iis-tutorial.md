---
title: aaaTutorial - Build een maximaal beschikbare toepassing op Azure Virtual machines | Microsoft Docs
description: Meer informatie over hoe toocreate een maximaal beschikbare en beveiligde toepassing in drie Windows virtuele machines met een load balancer in Azure
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
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a>Een taakverdeling, maximaal beschikbare toepassing op Windows virtuele machines in Azure bouwen

In deze zelfstudie maakt maken u een maximaal beschikbare toepassing die is robuuste toomaintenance gebeurtenissen. Hallo app gebruikmaakt van een load balancer, een beschikbaarheidsset en drie Windows virtuele machines (VM's). Deze zelfstudie IIS installeert, maar u kunt deze zelfstudie toodeploy wordt gebruikt door een andere toepassing framework Hallo dezelfde hoge beschikbaarheid onderdelen en richtlijnen. 

## <a name="step-1---azure-prerequisites"></a>Stap 1: vereisten voor Azure

toocomplete in deze zelfstudie maakt voor zorgen Hallo meest recente geïnstalleerd [Azure PowerShell](/powershell/azure/overview) module.

Eerst aanmelden tooyour Azure-abonnement met Hallo Login-AzureRmAccount opdracht en volg Hallo op het scherm aanwijzingen.

```powershell
Login-AzureRmAccount
```

Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. Voordat u een andere Azure-resources maken kunt, moet u toocreate een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westeurope` regio: 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a>Stap 2: beschikbaarheidsset maken

Virtuele machines kunnen worden gemaakt tussen logische fouttolerantie en domeinen bijwerken. Elk domein logische vertegenwoordigt een deel van de hardware in Hallo onderliggende Azure-datacenter. Wanneer u twee of meer virtuele machines maakt, worden uw resources berekenings- en verdeeld over deze domeinen. Deze verdeling onderhoudt Hallo beschikbaarheid van uw app als een hardware-onderdeel onderhoud moet. Beschikbaarheidssets kunnen u deze logische domeinen met fouten en update definiëren.

Maken van een beschikbaarheidsset met [nieuw AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Hallo volgende voorbeeld maakt u een beschikbaarheidsset benoemde `myAvailabilitySet`:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a>Stap 3: het maken van de load balancer

Een Azure load balancer wordt verkeer over een reeks gedefinieerde virtuele machines met regels voor load balancer. Een health test een bepaalde poort op elke virtuele machine bewaakt en distribueert u alleen verkeer tooan operationele VM.

### <a name="create-public-ip-address"></a>Openbare IP-adres maken

tooaccess uw app op Internet, Hallo toewijzen een openbare IP-adres toohello load balancer. Maken van een openbaar IP-adres met [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam `myPublicIP`:

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a>Load balancer maken

Maken van een frontend-IP-adres met [nieuw AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Hallo volgende voorbeeld wordt een frontend-IP-adres met de naam `myFrontEndPool`: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

Maak een back-end-adresgroep met [nieuw AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Hallo volgende voorbeeld wordt een back-end-adresgroep met de naam `myBackEndPool`:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Maak nu Hallo load balancer met [nieuw AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer). Hallo volgende voorbeeld maakt u een load balancer met de naam `myLoadBalancer` met Hallo `myPublicIP` adres:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a>Maken van de health test

tooallow hello load balancer toomonitor Hallo status van uw app, dat u een health test gebruiken. Hallo health test wordt dynamisch toegevoegd of verwijderd van virtuele machines van Hallo load balancer wisselen op basis van hun antwoord toohealth controles. Standaard wordt een virtuele machine verwijderd uit Hallo load balancer-distributie na twee opeenvolgende fouten met intervallen van 15 seconden.

Maken van een health test met [toevoegen AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Hallo volgende voorbeeld wordt een health test met de naam `myHealthProbe` die elke VM bewaakt:

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a>Load balancer-regel maken

Een load balancer-regel is gebruikte toodefine hoe verkeer wordt gedistribueerde toohello virtuele machines.

Maken van een regel voor load balancer met [toevoegen AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Hallo volgende voorbeeld maakt u een regel voor load balancer met de naam `myLoadBalancerRule` en verkeer op poort sluitend `80`:

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

Hallo load balancer is met bijwerken [Set AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a>Stap 4 - netwerken configureren

Elke virtuele machine heeft een of meer virtuele netwerkinterfacekaarten (NIC's) die tooa virtueel netwerk verbinden. Dit virtuele netwerk, toofilter-verkeer op basis van gedefinieerde toegangsregels is beveiligd.

### <a name="create-virtual-network"></a>Virtueel netwerk maken

Configureer eerst een subnet met [nieuw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Hallo volgende voorbeeld wordt een subnet met de naam `mySubnet`:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

tooprovide network connectivity tooyour virtuele machines, maak een virtueel netwerk met [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Hallo volgende voorbeeld wordt een virtueel netwerk met de naam `myVnet` met `mySubnet`:

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a>Netwerkbeveiliging configureren

Een Azure [netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md) (NSG) Hiermee wordt bepaald binnenkomend en uitgaand verkeer voor een of meer virtuele machines. Netwerkbeveiligingsgroepen toestaan of weigeren van netwerkverkeer op een specifieke poort of een poortbereik. Deze regels kunnen ook een voorvoegsel voor bronadres bevatten, zodat alleen verkeer dat afkomstig is op een vooraf gedefinieerde bron met een virtuele machine communiceren kan.

tooallow web-verkeer tooreach uw app, maakt u een groep van de netwerkbeveiligingsregel met [nieuw AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Hallo volgende voorbeeld wordt een groep netwerkbeveiligingsregel met de naam `myNetworkSecurityGroupRule`:

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow
```

Maken van een netwerkbeveiligingsgroep met [nieuw AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Hallo volgende voorbeeld maakt u een NSG met de naam `myNetworkSecurityGroup`:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

Toevoegen van Hallo beveiliging groep toohello netwerksubnet met [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

Update Hallo virtueel netwerk met [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a>Netwerkinterfacekaarten voor virtueel netwerk maken

Load balancers-functie met Hallo virtuele NIC-bron in plaats van Hallo werkelijke VM. Hallo virtuele NIC verbonden toohello load balancer en vervolgens tooa VM gekoppeld.

Maken van een virtuele NIC met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Hallo maakt volgende voorbeeld drie virtuele NIC's. (Een virtuele NIC voor elke VM die u maakt voor uw app in hello te volgen stappen):


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a>Stap 5: virtuele machines maken

Met alle Hallo onderliggende onderdelen geïmplementeerd, kunt u nu maximaal beschikbare virtuele machines toorun uw app maken. 

Hallo-gebruikersnaam en wachtwoord nodig voor Hallo-beheerdersaccount op Hallo virtuele machine met ophalen [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Maken van Hallo virtuele machines met [nieuw AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Toevoegen AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), en [nieuwe-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Hallo volgende voorbeeld maakt drie virtuele machines:

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

Het duurt enkele minuten toocreate en configureer alle drie virtuele machines. Hallo load balancer health test automatisch gedetecteerd wanneer Hallo-app wordt uitgevoerd op elke virtuele machine. Zodra het Hallo-app wordt uitgevoerd, begint Hallo load balancer-regel toodistribute verkeer.

### <a name="install-hello-app"></a>Hallo-app installeren 

Virtuele machine van Azure-extensies zijn gebruikte tooautomate virtuele machine configuratietaken zoals toepassingen installeren en configureren van het besturingssysteem Hallo. Hallo [extensie voor aangepaste scripts voor Windows](./../virtual-machines-windows-extensions-customscript.md) gebruikte toorun is een PowerShell-script op Hallo virtuele machine. Hallo script worden opgeslagen in Azure storage, een willekeurig toegankelijk eindpunt van de HTTP- of worden ingesloten in de configuratie voor de uitbreiding van Hallo aangepast script. Wanneer u de aangepaste scriptextensie hello, beheert hello Azure VM-agent Hallo script worden uitgevoerd.

Gebruik [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Hallo aangepaste scriptextensie. Hallo-extensie wordt uitgevoerd `powershell Add-WindowsFeature Web-Server` tooinstall Hallo IIS-webserver:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a>Uw app testen

Hallo openbare IP-adres van de load balancer met verkrijgen [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hallo volgende voorbeeld Hallo IP-adres krijgt voor `myPublicIP` eerder hebt gemaakt:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

Voer Hallo openbaar IP-adres in de webbrowser tooa. Met Hallo NSG regel aanwezig, wordt Hallo standaard IIS-website weergegeven. 

![Standaardsite van IIS](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a>Stap 6 – beheertaken

Mogelijk moet u tooperform onderhoud op Hallo van virtuele machines waarop uw app, zoals het installeren van updates voor het besturingssysteem wordt uitgevoerd. toodeal met tooyour-app voor verkeer, moet u mogelijk tooadd extra virtuele machines. Deze sectie leest u hoe tooremove of een virtuele machine van Hallo load balancer toe te voegen. 

### <a name="remove-a-vm-from-hello-load-balancer"></a>Een virtuele machine van Hallo load balancer verwijderen

Een virtuele machine verwijderen uit Hallo back-endadresgroep hello loadbalancerbackendaddresspools gebruikt de eigenschap van netwerkinterfacekaart Hallo herstelt.

Hallo-netwerkinterfacekaart met ophalen [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

Hallo loadbalancerbackendaddresspools gebruikt eigenschap van netwerkinterfacekaart hello te instellen $null:

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

Hallo netwerkinterfacekaart bijwerken:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a>Een VM toohello load balancer toevoegen

Na het uitvoeren van onderhoud van de virtuele machine of als u tooexpand capaciteit moet, toe te voegen Hallo NIC van een VM toohello back-end-adresgroep Hallo load balancer.

Hallo load balancer ophalen:

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

Hallo back-endadresgroep van netwerkinterfacekaart van Hallo load balancer toohello toevoegen:

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

Hallo netwerkinterfacekaart bijwerken:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Volgende stappen

Voorbeelden: [Azure virtuele Machine PowerShell-voorbeeldscripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
