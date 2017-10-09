---
title: aaaHow tooload saldo Windows virtuele machines in Azure | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure balancer toocreate een maximaal beschikbare en beveiligde toepassing geladen over drie Windows VM 's
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Hoe tooload balans vinden tussen Windows virtuele machines in Azure toocreate een maximaal beschikbare toepassing
Taakverdeling biedt een hoger niveau van de beschikbaarheid van binnenkomende aanvragen verspreid over meerdere virtuele machines. In deze zelfstudie leert u Hallo verschillende onderdelen van hello Azure load balancer die verkeer distribueren en bieden hoge beschikbaarheid. Procedures voor:

> [!div class="checklist"]
> * Een Azure load balancer maken
> * Een load balancer health test maken
> * Regels voor netwerkverkeer voor de load balancer maken
> * Hallo aangepaste Scriptextensie toocreate een normale IIS-website gebruiken
> * Virtuele machines maken en koppelen tooa load balancer
> * Een load balancer in actie weergeven
> * Toevoegen of virtuele machines van een load balancer verwijderen

Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger. Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie. Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).


## <a name="azure-load-balancer-overview"></a>Overzicht van Azure load balancer
Een Azure load balancer is een Layer-4 (TCP, UDP) load balancer die zorgt voor hoge beschikbaarheid door het distribueren van inkomend verkeer tussen orde virtuele machines. Een load balancer health test een bepaalde poort op elke virtuele machine bewaakt en distribueert u alleen verkeer tooan operationele VM.

U definieert een front-end-IP-configuratie met een of meer openbare IP-adressen. Deze front-end-IP-configuratie kan de load balancer en toepassingen toobe toegankelijk via Hallo Internet. 

Virtuele machines verbinding tooa load balancer met behulp van de virtuele netwerkinterfacekaart (NIC). toodistribute verkeer toohello VM's, een back-end-adresgroep bevat Hallo IP-adressen van Hallo virtuele (NIC's) verbonden toohello load balancer.

toocontrol hello stroom van verkeer, kunt u definiëren load balancerregels voor specifieke poorten en protocollen die zijn toegewezen tooyour virtuele machines.


## <a name="create-azure-load-balancer"></a>Azure load balancer maken
In deze sectie beschrijft hoe u kunt maken en configureren van elk onderdeel Hallo load balancer. Voordat u de load balancer maken kunt, maakt u een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupLoadBalancer* in Hallo *EastUS* locatie:

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a>Een openbaar IP-adres maken
tooaccess uw app op Hallo Internet, moet u een openbaar IP-adres voor Hallo load balancer. Maken van een openbaar IP-adres met [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam *myPublicIP* in Hallo *myResourceGroupLoadBalancer* resourcegroep:

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a>Een load balancer maken
Maken van een frontend-IP-adres met [nieuw AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Hallo volgende voorbeeld wordt een frontend-IP-adres met de naam *myFrontEndPool*: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

Maak een back-end-adresgroep met [nieuw AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Hallo volgende voorbeeld wordt een back-end-adresgroep met de naam *myBackEndPool*:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Maak nu Hallo load balancer met [nieuw AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer). Hallo volgende voorbeeld maakt u een load balancer met de naam *myLoadBalancer* met Hallo *myPublicIP* adres:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a>Een health test maken
tooallow hello load balancer toomonitor Hallo status van uw app, dat u een health test gebruiken. Hallo health test wordt dynamisch toegevoegd of verwijderd van virtuele machines van Hallo load balancer wisselen op basis van hun antwoord toohealth controles. Standaard wordt een virtuele machine verwijderd uit Hallo load balancer-distributie na twee opeenvolgende fouten met intervallen van 15 seconden. U maakt een health test op basis van een protocol of de pagina voor de controle van een specifieke status voor uw app. 

Hallo volgende voorbeeld wordt een TCP-test. U kunt ook aangepaste HTTP-tests voor meer fijnmazige statuscontroles maken. Wanneer u een aangepaste HTTP-test, moet u Hallo selectievakje statuspagina, zoals *healthcheck.aspx*. Hallo test moet retourneren een **HTTP 200 OK** antwoord voor Hallo load balancer tookeep Hallo host in de draaihoek.

toocreate een TCP health test, die u gebruikt [toevoegen AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Hallo volgende voorbeeld wordt een health test met de naam *myHealthProbe* die elke VM bewaakt:

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

Hallo load balancer is met bijwerken [Set AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a>Een load balancer-regel maken
Een load balancer-regel is gebruikte toodefine hoe verkeer wordt gedistribueerde toohello virtuele machines. U definieert Hallo front-end-IP-configuratie voor Hallo binnenkomende verkeer en Hallo backend-IP-adresgroep tooreceive Hallo, samen met de vereiste bron Hallo en doelpoort. toomake zorgen dat alleen orde virtuele machines verkeer ontvangt, u Hallo health test toouse ook definiëren.

Maken van een regel voor load balancer met [toevoegen AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Hallo volgende voorbeeld maakt u een regel voor load balancer met de naam *myLoadBalancerRule* en verkeer op poort sluitend *80*:

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

Hallo load balancer is met bijwerken [Set AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a>Virtueel netwerk configureren
Voordat u een aantal virtuele machines implementeren en uw balancer kunt testen, maak Hallo ondersteunende resources van een virtueel netwerk. Zie voor meer informatie over virtuele netwerken Hallo [Azure Virtual Networks beheren](tutorial-virtual-network.md) zelfstudie.

### <a name="create-network-resources"></a>Maken van netwerkbronnen
Maak een virtueel netwerk met [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* met *mySubnet*:

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

Maken van een groep van de netwerkbeveiligingsregel met [nieuw AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), maakt u een netwerkbeveiligingsgroep met [nieuw AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Toevoegen van Hallo beveiliging groep toohello netwerksubnet met [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) en werk vervolgens Hallo virtueel netwerk met [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork). 

Hallo volgende voorbeeld wordt een groep netwerkbeveiligingsregel met de naam *myNetworkSecurityGroup* en past u deze te*mySubnet*:

```powershell
# Create security rule config
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

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

Virtuele NIC's zijn gemaakt met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Hallo maakt volgende voorbeeld drie virtuele NIC's. (Een virtuele NIC voor elke VM die u maakt voor uw app in hello te volgen stappen.) U kunt extra virtuele NIC's en virtuele machines maken op elk gewenst moment en ze toohello load balancer toevoegen:

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a>Virtuele machines maken
tooimprove hello hoge beschikbaarheid van uw app, uw virtuele machines in een beschikbaarheidsset plaatst.

Maken van een beschikbaarheidsset met [nieuw AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Hallo volgende voorbeeld maakt u een beschikbaarheidsset benoemde *myAvailabilitySet*:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

Stel dat een beheerder gebruikersnaam en wachtwoord voor Hallo VM's met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Nu kunt u virtuele machines Hallo met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Hallo volgende voorbeeld maakt drie virtuele machines:

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
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
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

Het duurt enkele minuten toocreate en configureer alle drie virtuele machines.

### <a name="install-iis-with-custom-script-extension"></a>IIS installeren met de extensie voor aangepaste scripts
In een vorige zelfstudie over [hoe toocustomize virtuele Windows-machine](tutorial-automate-vm-deployment.md), hebt u geleerd hoe tooautomate VM aanpassing met aangepaste Script uitbreiding voor Windows hello. U kunt Hallo dezelfde tooinstall benadering en IIS configureren op uw virtuele machines.

Gebruik [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Hallo extensie voor aangepaste scripts. Hallo-extensie wordt uitgevoerd `powershell Add-WindowsFeature Web-Server` tooinstall Hallo IIS-webserver en klik vervolgens op updates Hallo *Default.htm* pagina tooshow Hallo hostnaam Hallo VM:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a>Test load balancer
Hallo openbare IP-adres van de load balancer met verkrijgen [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hallo volgende voorbeeld Hallo IP-adres krijgt voor *myPublicIP* eerder hebt gemaakt:

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

Vervolgens kunt u in de webbrowser tooa Hallo openbaar IP-adres invoeren. Hallo-website wordt weergegeven, inclusief Hallo hostnaam Hallo VM die Hallo load balancer gedistribueerde tooas verkeer in het volgende voorbeeld Hallo:

![Actieve IIS-website](./media/tutorial-load-balancer/running-iis-website.png)

toosee hello load balancer verkeer verdelen over alle drie virtuele machines waarop uw app wordt uitgevoerd, u kunt force vernieuwen van uw webbrowser.


## <a name="add-and-remove-vms"></a>Toevoegen en verwijderen van virtuele machines
Mogelijk moet u tooperform onderhoud op Hallo van virtuele machines waarop uw app, zoals het installeren van updates voor het besturingssysteem wordt uitgevoerd. toodeal met tooyour-app voor verkeer, moet u mogelijk tooadd extra virtuele machines. Deze sectie leest u hoe tooremove of een virtuele machine van Hallo load balancer toe te voegen.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Een virtuele machine van Hallo load balancer verwijderen
Hallo-netwerkinterfacekaart met ophalen [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), vervolgens set Hallo *loadbalancerbackendaddresspools gebruikt* eigenschap van Hallo virtuele NIC te*$null*. Tot slot werkt Hallo virtuele NIC:

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

toosee hello load balancer verkeer verdelen over Hallo overige twee virtuele machines met uw app u kunt force vernieuwen van uw webbrowser. U kunt nu onderhoud uitvoeren op Hallo VM, zoals het installeren van updates voor het besturingssysteem of het uitvoeren van een VM opnieuw wordt opgestart.

### <a name="add-a-vm-toohello-load-balancer"></a>Een VM toohello load balancer toevoegen
Na onderhoud aan de virtuele machine uitvoeren of als u tooexpand capaciteit nodig hebt, stelt u Hallo *loadbalancerbackendaddresspools gebruikt* eigenschap van de virtuele NIC toohello hello *BackendAddressPool* van [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):

Hallo load balancer ophalen:

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt gemaakt van een load balancer en virtuele machines tooit gekoppeld. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Een Azure load balancer maken
> * Een load balancer health test maken
> * Regels voor netwerkverkeer voor de load balancer maken
> * Hallo aangepaste Scriptextensie toocreate een normale IIS-website gebruiken
> * Virtuele machines maken en koppelen tooa load balancer
> * Een load balancer in actie weergeven
> * Toevoegen of virtuele machines van een load balancer verwijderen

Hoe gaan van de volgende zelfstudie toolearn toohello toomanage VM-netwerken.

> [!div class="nextstepaction"]
> [Virtuele machines en virtuele netwerken beheren](./tutorial-virtual-network.md)
