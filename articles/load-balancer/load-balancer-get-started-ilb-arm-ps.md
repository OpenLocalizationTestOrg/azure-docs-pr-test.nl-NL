---
title: een Azure-interne aaaCreate de load balancer - PowerShell | Microsoft Docs
description: Meer informatie over hoe toocreate een interne load balancer met behulp van PowerShell in Resource Manager
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a>Een interne load balancer maken met behulp van PowerShell

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Sjabloon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).  In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

Hallo stappen wordt uitgelegd hoe toocreate een interne load balancer met Azure Resource Manager met PowerShell. Met Azure Resource Manager Hallo items toocreate een interne load balancer worden afzonderlijk geconfigureerd en vervolgens gecombineerd toocreate een load balancer.

U moet toocreate en configureer Hallo objecten toodeploy een load balancer te volgen:

* Front-end-IP-configuratie - Hallo privé IP-adres voor binnenkomend netwerkverkeer wilt configureren
* Back-endadresgroep - wilt Hallo netwerkinterfaces die ontvangt Hallo taakverdelingsverkeer afkomstig is van de front-end-IP-adresgroep configureren
* Taakverdelingsregels - bron- en configuratie van de lokale poort voor Hallo de load balancer.
* Tests - Hallo health statustest voor de virtuele Machine-exemplaren Hallo configureert.
* NAT-regels voor binnenkomende verbindingen-configureert u de Hallo poort regels toodirectly toegang een Hallo exemplaren van virtuele machines.

Meer informatie over de load balancer-onderdelen in Azure Resource Manager vindt u op [Ondersteuning van Azure Resource Manager voor Azure Load Balancer](load-balancer-arm.md).

Hallo volgende stappen wordt uitgelegd hoe tooconfigure een load balancer tussen twee virtuele machines.

## <a name="setup-powershell-toouse-resource-manager"></a>Setup PowerShell toouse Resource Manager

Zorg ervoor dat u Hallo nieuwste productieversie van hello Azure-module voor PowerShell en PowerShell instellen correct tooaccess uw Azure-abonnement.

### <a name="step-1"></a>Stap 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Stap 2

Controleer de abonnementen Hallo voor Hallo-account

```powershell
Get-AzureRmSubscription
```

U zult na vragen aan gebruiker tooAuthenticate met uw referenties.

### <a name="step-3"></a>Stap 3

Kies welke van uw Azure-abonnementen toouse.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a>Resourcegroep voor load balancer maken

Een nieuwe resourcegroep maken (sla deze stap over als u een bestaande resourcegroep gebruikt)

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Dit wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep. Zorg ervoor dat alle opdrachten toocreate een load balancer gebruiken Hallo dezelfde resourcegroep.

In Hallo voorbeeld hierboven wordt gemaakt met een resourcegroep 'NRP-RG' en de locatie ' West ' genoemd.

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a>Virtueel netwerk en een particulier IP-adres voor front-end-IP-adresgroep maken

Maakt een subnet voor het virtuele netwerk Hallo en wijst toovariable $backendSubnet

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

Een virtueel netwerk maken:

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

Hallo virtueel netwerk maakt en voegt Hallo subnet toohello lb-subnet niet virtueel netwerk NRPVNet toe en wijst toovariable $vnet

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a>Front-end-IP-adresgroep en back-endadresgroep maken

Instellen van een front-end-IP-adresgroep voor inkomende hello load balancer-netwerkverkeer en de back-end adresgroep tooreceive hello taakverdelingsverkeer.

### <a name="step-1"></a>Stap 1

Maak een front-end-IP-adresgroep met Hallo privé IP-adres 10.0.2.5 voor Hallo subnet 10.0.2.0/24 Hallo binnenkomende verkeer netwerkeindpunt worden.

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a>Stap 2

Instellen van een back-end-adresgroep gebruikt tooreceive inkomend verkeer van de front-end-IP-adresgroep:

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a>LB-regels, NAT-regels, test en load balancer maken

Na het Hallo-front-end-IP-adresgroep en Hallo back-end-adresgroep maken, moet u toocreate Hallo regels die deel van toohello load balancerresource uitmaakt:

### <a name="step-1"></a>Stap 1

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

Hallo in bovenstaand voorbeeld met het maken van de volgende items Hallo:

* NAT-regel waarmee alle binnenkomende verkeer tooport 3441 gaat tooport 3389.
* een tweede NAT-regel waarmee alle binnenkomende verkeer tooport 3442 gaat tooport 3389.
* alle binnenkomend verkeer op poort 80 van de openbare poort 80 in Hallo back-end-adresgroep toolocal het saldo van een regel voor load balancer die wordt geladen.
* een test-regel die de gezondheidsstatus Hallo voor pad 'HealthProbe.aspx' wordt gecontroleerd

### <a name="step-2"></a>Stap 2

Hallo load balancer samen met het toevoegen van alle objecten (NAT-regels, Load balancerregels, test-configuraties) maken:

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a>Netwerkinterfaces maken

Na het maken van Hallo interne load balancer, moet u definiëren welke netwerkinterfaces ontvangt Hallo binnenkomende taakverdeling netwerkverkeer, NAT-regels en test. Hallo-netwerkinterface in dit geval afzonderlijk geconfigureerd en kan worden toegewezen tooa virtuele machine later op.

### <a name="step-1"></a>Stap 1

Hallo resource virtuele netwerk en subnet toocreate netwerkinterfaces ophalen:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

Deze stap maakt u een netwerkinterface die wordt behoren toohello load balancer back-end-pool en Hallo eerste NAT-regel voor RDP voor deze netwerkinterface koppelen:

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a>Stap 2

Maak als volgt een tweede netwerkinterface met de naam LB-Nic2-BE:

Deze stap maakt u een tweede netwerkinterface, toohello toewijzen dezelfde load balancer terug pool beëindigen en koppelen van Hallo tweede NAT-regel gemaakt voor RDP:

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

het eindresultaat Hello wordt Hallo volgende weergeven:

    $backendnic1

Verwachte uitvoer:

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



### <a name="step-3"></a>Stap 3

Hallo opdracht toevoegen AzureRmVMNetworkInterface tooassign Hallo NIC tooa virtuele Machine gebruiken.

Vindt u stapsgewijze instructies toocreate een virtuele machine Hallo en tooa NIC toewijzen Hallo documentatie te volgen: [maken van een virtuele machine in Azure met behulp van PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface"></a>Hallo-netwerkinterface toevoegen

Als er al een virtuele machine gemaakt, kunt u Hallo netwerkinterface toevoegen Hello stappen te volgen:

### <a name="step-1"></a>Stap 1

Hallo load balancerresource in een variabele laden (als u die nog niet hebt gedaan). Hallo-variabele die wordt gebruikt is aangeroepen $lb en gebruik Hallo Hallo load balancerresource dezelfde namen die eerder is gemaakt.

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a>Stap 2

Hallo back-end configuratie tooa variabele worden geladen.

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a>Stap 3

Netwerkinterface Hallo al gemaakt in een variabele laden. Hallo variabelenaam gebruikt is $nic. Hallo naam voor de netwerkinterface gebruikt Hallo dezelfde van Hallo in bovenstaand voorbeeld.

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a>Stap 4

Hallo back-end-configuratie wijzigen op Hallo-netwerkinterface.

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a>Stap 5

Sla Hallo netwerkinterface-object.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Nadat een netwerkinterface kan back-endpool van toohello load balancer is toegevoegd, wordt gestart op basis van regels voor de load balancerresource voor taakverdeling Hallo netwerkverkeer ontvangen.

## <a name="update-an-existing-load-balancer"></a>Een bestaande load balancer bijwerken

### <a name="step-1"></a>Stap 1
Load balancer-object toovariable $slb met Get-AzureRmLoadBalancer met Hallo load balancer van Hallo in bovenstaand voorbeeld, toewijzen

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a>Stap 2

In Hallo voorbeeld te volgen, wordt u een nieuwe inkomende NAT-regel met behulp van poort 81 in de front-end Hallo toevoegen en poort 8181 Hallo terug eindigen groep tooan bestaande load balancer

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a>Stap 3

Sla de nieuwe configuratie Hallo met Set-AzureLoadBalancer

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a>Een load balancer verwijderen

Hallo opdracht Remove-AzureRmLoadBalancer toodelete een eerder gemaakte taakverdeler met de naam 'NRP-LB' in een resourcegroep genaamd 'NRP-RG' gebruiken

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> U kunt optioneel Hallo switch - Force tooavoid Hallo prompt voor verwijdering.

## <a name="next-steps"></a>Volgende stappen

[Een distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)
