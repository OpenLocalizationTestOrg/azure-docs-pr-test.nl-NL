---
title: Een interne load balancer in Azure maken met PowerShell | Microsoft Docs
description: Informatie over hoe u met de Azure PowerShell-module een interne load balancer maakt in Azure Resource Manager
services: load-balancer
documentationcenter: na
author: KumudD
manager: jennoc
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/25/2017
ms.author: kumud
ms.openlocfilehash: 6eea6c9bc7f686096c3cf0c97bfbe65a5507de2a
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/18/2017
---
# <a name="create-an-internal-load-balancer-by-using-the-azure-powershell-module"></a>Een interne load balancer maken met behulp van de Azure PowerShell-module

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Sjabloon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-basic-sku-include.md](../../includes/load-balancer-basic-sku-include.md)]

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="get-started-with-the-configuration"></a>Aan de slag met de configuratie

In dit artikel wordt uitgelegd hoe u met de Azure PowerShell-module een interne load balancer maakt in Azure Resource Manager. In het Resource Manager-implementatiemodel worden de objecten die nodig zijn voor het maken van een interne load balancer afzonderlijk geconfigureerd. Nadat de objecten zijn gemaakt en geconfigureerd, worden ze gecombineerd voor het maken van een load balancer.

De volgende objecten moeten worden gemaakt om een load balancer te implementeren:

* Front-end-IP-pool: het particuliere IP-adres voor inkomend netwerkverkeer.
* Back-end-adresgroep: de netwerkinterfaces voor het ontvangen van het verkeer met gelijke taakverdeling van het front-end-IP-adres.
* Taakverdelingsregels: configuratie van bron- en lokale poort voor de load balancer.
* Testconfiguratie: de status van de tests voor virtuele machines.
* Binnenkomende NAT-regels: de poortregels voor directe toegang tot virtuele machines.

Zie [Azure Resource Manager-ondersteuning voor load balancers](load-balancer-arm.md) voor meer informatie over de onderdelen van load balancers.

In de volgende stappen wordt uitgelegd hoe u een load balancer tussen twee virtuele machines configureert.

## <a name="set-up-powershell-to-use-resource-manager"></a>PowerShell instellen voor het gebruik van Resource Manager

Zorg ervoor dat u de nieuwste productieversie van de Azure PowerShell-module hebt. PowerShell moet correct zijn geconfigureerd voor toegang tot uw Azure-abonnement.

### <a name="step-1-start-powershell"></a>Stap 1: PowerShell starten

Start de PowerShell-module voor Azure Resource Manager.

```powershell
Login-AzureRmAccount
```

### <a name="step-2-view-your-subscriptions"></a>Stap 2: Uw abonnementen bekijken

Controleer uw beschikbare Azure-abonnementen.

```powershell
Get-AzureRmSubscription
```

Geef uw referenties wanneer u wordt gevraagd om verificatie.

### <a name="step-3-select-the-subscription-to-use"></a>Stap 3: Het abonnement dat u wilt gebruiken selecteren

Kies welk Azure-abonnement moet worden gebruikt voor het implementeren van de load balancer.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4-choose-the-resource-group-for-the-load-balancer"></a>Stap 4: De resourcegroep voor de load balancer kiezen

Maak een nieuwe resourcegroep voor de load balancer. Sla deze stap over als u een bestaande resourcegroep gebruikt.

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. De locatie wordt gebruikt als de standaardlocatie voor alle resources in de resourcegroep. Gebruik altijd dezelfde resourcegroep voor alle opdrachten die betrekking hebben op het maken van de load balancer.

In het bovenstaande voorbeeld is er een resourcegroep gemaakt met de naam **NRP-RG** en de locatie VS - west.

## <a name="create-the-virtual-network-and-ip-address-for-the-front-end-ip-pool"></a>Het virtuele netwerk en een IP-adres voor de front-end-IP-pool maken

Hiermee maakt u een subnet voor het virtuele netwerk en wijst u deze toe aan de variabele **$backendSubnet**.

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

Maak een virtueel netwerk.

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

Het virtuele netwerk is gemaakt. Het subnet **LB-Subnet-BE** wordt toegevoegd aan het virtuele netwerk **NRPVNet**. Deze waarden worden toegewezen aan de variabele **$vnet**.

## <a name="create-the-front-end-ip-pool-and-back-end-address-pool"></a>De front-end-IP-pool en back-end-adresgroep maken

Hiermee maakt u een front-end-IP-pool voor het binnenkomende verkeer en een back-end-adresgroep om het verkeer met gelijke taakverdeling te ontvangen.

### <a name="step-1-create-a-front-end-ip-pool"></a>Stap 1: Een front-end-IP-pool maken

Maak een front-end-IP-pool maken met het privé-IP-adres 10.0.2.5 voor het subnet 10.0.2.0/24. Dit adres is het eindpunt van het binnenkomende verkeer.

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2-create-a-back-end-address-pool"></a>Stap 2: Een back-end-adresgroep maken

Maak een back-end-adresgroep om binnenkomend verkeer van de front-end-IP-pool te ontvangen:

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-the-configuration-rules-probe-and-load-balancer"></a>Maak de configuratieregels, de test en de load balancer

Nadat de front-end-IP-pool en de back-end-adresgroep zijn gemaakt, kunt u regels voor de load balancer-resource opgeven.

### <a name="step-1-create-the-configuration-rules"></a>Stap 1: De configuratieregels maken

In het voorbeeld maakt u de volgende vier regelobjecten:

* Een binnenkomende NAT-regel voor het Remote Desktop Protocol (RDP): leidt al het binnenkomende verkeer bij poort 3441 naar poort 3389.
* Een tweede binnenkomende NAT-regel voor RDP: leidt al het binnenkomende verkeer bij poort 3442 leidt tot poort 3389.
* Een statustestregel: controleert de status test voor het pad HealthProbe.aspx.
* Een load balancer-regel: zorgt ervoor dat al het verkeer dat binnenkomt bij openbare poort 80, met gelijke taakverdeling wordt omgeleid naar de lokale poort 80 in de back-end-adresgroep.

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

### <a name="step-2-create-the-load-balancer"></a>Stap 2: De load balancer maken

Maak de load balancer en combineer de regelobjecten (inkomende NAT voor RDP, load balancer en statustest):

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-the-network-interfaces"></a>De netwerkinterfaces maken

Nadat de interne load balancer is gemaakt, moet u de netwerkinterfaces (NIC's) definiëren die het binnenkomende netwerkverkeer met gelijke taakverdeling, de NAT-regels en de test kunnen ontvangen. Elke netwerkinterface wordt afzonderlijk geconfigureerd. Deze worden later toegewezen aan een virtuele machine.

### <a name="step-1-create-the-first-network-interface"></a>Stap 1: De eerste netwerkinterface maken

Haal het virtueel netwerk en subnet van de resource op. Deze waarden worden gebruikt om de netwerkinterfaces te maken:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

Maak de eerste netwerkinterface met de naam **lb-nic1-be**. Wijs de interface toe aan de back-end-pool van de load balancer. Koppel de eerste NAT-regel voor RDP aan deze NIC:

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2-create-the-second-network-interface"></a>Stap 2: De tweede netwerkinterface maken

Maak de tweede netwerkinterface met de naam **lb-nic2-be**. Wijs de tweede interface toe aan dezelfde back-end-pool van de load balancer als de eerste interface. Koppel de tweede NIC aan de tweede NAT-regel voor RDP:

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

Controleer de configuratie:

    $backendnic1

De instellingen moeten er als volgt uitzien:

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
                           "PublicIpAddress": {
                             "Id": null
                           },
                           "LoadBalancerBackendAddressPools": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                             }
                           ],
                           "LoadBalancerInboundNatRules": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                             }
                           ],
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3-assign-the-nic-to-a-vm"></a>Stap 3: De NIC toewijzen aan een virtuele machine

Wijs de NIC toe aan een virtuele machine met behulp van de opdracht `Add-AzureRmVMNetworkInterface`.

U vindt de stapsgewijze instructies voor het maken van een virtuele machine en de toewijzing ervan aan een NIC in [Een virtuele machine in Azure maken met behulp van PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-the-network-interface"></a>Netwerkinterface toevoegen

Nadat de virtuele machine is gemaakt, voegt u de netwerkinterface toe.

### <a name="step-1-store-the-load-balancer-resource"></a>Stap 1: De load balancer-resource opslaan

Sla de load balancer-resource op in een variabele (als u dat nog niet hebt gedaan). We maken gebruik van de variabelenaam **$lb**. Gebruik de namen voor de load balancer-resources die zijn gemaakt in de vorige stappen voor de kenmerkwaarden in het script.

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2-store-the-back-end-configuration"></a>Stap 2: De back-end-configuratie opslaan

Sla de configuratie van de back-end op in de variabele **$backend**.

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
```

### <a name="step-3-store-the-network-interface"></a>Stap 3: De netwerkinterface opslaan

Sla de netwerkinterface op in een andere variabele. Deze interface is gemaakt in 'De netwerkinterfaces maken, stap 1'. We maken gebruik van de variabelenaam **$nic1**. Gebruik dezelfde netwerkinterfacenaam als in het vorige voorbeeld.

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4-change-the-back-end-configuration"></a>Stap 4: De back-end-configuratie wijzigen

Wijzig de back-endconfiguratie op de netwerkinterface.

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5-save-the-network-interface-object"></a>Stap 5: Het netwerkinterfaceobject opslaan

Sla het netwerkinterfaceobject op.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Nadat de interface is toegevoegd aan de back-end-pool, wordt het netwerkverkeer gelijk verdeeld volgens de regels. Deze regels zijn geconfigureerd in 'Maak de configuratieregels, de test en de load balancer.'

## <a name="update-an-existing-load-balancer"></a>Een bestaande load balancer bijwerken

### <a name="step-1-assign-the-load-balancer-object-to-a-variable"></a>Stap 1: Het load balancer-object toewijzen aan een variabele

Wijs het load balancer-object (uit het vorige voorbeeld) toe aan de variabele **$slb** met behulp van de opdracht `Get-AzureRmLoadBalancer`:

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2-add-a-nat-rule"></a>Stap 2: Een NAT-regel toevoegen

Voeg een nieuwe binnenkomende NAT-regel toe aan een bestaande load balancer. Gebruik poort 81 voor de front-end-pool en poort 8181 voor de back-end-pool:

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3-save-the-configuration"></a>Stap 3: De configuratie opslaan

Sla de nieuwe configuratie op met behulp van de opdracht `Set-AzureLoadBalancer`:

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-an-existing-load-balancer"></a>Een bestaande load balancer verwijderen

Verwijder de load balancer **NRP-LB** in de resource **NRP-RG** met behulp van de opdracht `Remove-AzureRmLoadBalancer`:

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Gebruik de optionele schakeloptie **-Force** om te voorkomen dat de bevestigingsprompt voor de verwijdering wordt weergegeven.

## <a name="next-steps"></a>Volgende stappen

* [Distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)
* [TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)
