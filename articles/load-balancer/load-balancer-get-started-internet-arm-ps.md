---
title: een Azure internetgerichte aaaCreate de load balancer - PowerShell | Microsoft Docs
description: Meer informatie over hoe een internetgerichte toocreate netwerktaakverdeler in Resource Manager met behulp van PowerShell
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started"></a>Een internetgerichte load balancer maken in Resource Manager met behulp van PowerShell

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Sjabloon](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel. U kunt ook [meer informatie over hoe een internetgerichte toocreate netwerktaakverdeler met het klassieke implementatiemodel Hallo](load-balancer-get-started-internet-classic-cli.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a>Hallo-oplossing implementeren met behulp van Azure PowerShell

Hallo volgen procedures wordt uitgelegd hoe toocreate een internetgerichte netwerktaakverdeler met behulp van Azure Resource Manager met PowerShell. Met Azure Resource Manager elke bron wordt gemaakt en afzonderlijk geconfigureerd en vervolgens samengesteld toocreate een load balancer.

U moet maken en configureren van Hallo objecten toodeploy een load balancer te volgen:

* Front-end-IP-configuratie: bevat openbare IP-adressen (PIP) voor inkomend netwerkverkeer.
* Back-end-adresgroep: netwerkinterfaces (NIC's) voor virtuele machines tooreceive-netwerkverkeer Hallo van Hallo load balancer bevat.
* Regels voor taakverdeling: bevat regels die een openbare poort op Hallo load balancer tooa poort in Hallo back-end-adresgroep toewijzen.
* Binnenkomende NAT-regels: bevat regels die een openbare poort op Hallo load balancer tooa poort voor een specifieke virtuele machine in Hallo back-end-adresgroep toewijzen.
* Tests: bevat de beschikbaarheid van health-tests gebruikt toocheck exemplaren van virtuele machines in Hallo back-end-adresgroep.

Zie [Azure Resource Manager-ondersteuning voor load balancer](load-balancer-arm.md) voor meer informatie.

## <a name="set-up-powershell-toouse-resource-manager"></a>PowerShell toouse Resource Manager instellen

Controleer of er Hallo nieuwste productieversie van hello Azure Resource Manager-module voor PowerShell:

1. Meld u aan tooAzure.

    ```powershell
    Login-AzureRmAccount
    ```

    Voer uw referenties in wanneer dit wordt gevraagd.

2. Controleer de abonnementen Hallo voor Hallo-account.

    ```powershell
    Get-AzureRmSubscription
    ```

3. Kies welke van uw Azure-abonnementen toouse.

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. Maak een resourcegroep. (Sla deze stap over als u een bestaande resourcegroep gebruikt.)

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Een virtueel netwerk en een openbare IP-adres voor Hallo front-end-IP-adresgroep maken

1. Maak een subnet en een virtueel netwerk.

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. Een Azure openbare IP-adres-resource maken, met de naam **PublicIP**, die wordt gebruikt door een front-end-IP-adresgroep met Hallo DNS-naam toobe **loadbalancernrp.westus.cloudapp.azure.com**. Hallo volgende opdracht maakt gebruik van Hallo statische toewijzingstype.

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > Hallo load balancer gebruikmaakt Hallo domeinlabel van Hallo openbare IP-adres als een voorvoegsel voor de FQDN-naam. Dit wijkt af van Hallo klassieke implementatiemodel, dit maakt gebruik van cloudservice Hallo Hallo load balancer FQDN-naam.
   > In dit voorbeeld Hallo FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a>Een front-end-IP-adresgroep en back-endadresgroep maken

1. Maak een front-end-IP-adresgroep met de naam **LB-Frontend** die gebruikmaakt van Hallo **PublicIp** resource.

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. Maak een back-endadresgroep met de naam **LB-backend**.

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a>NAT-regels, een load balancer-regel, een test en een load balancer maken

In dit voorbeeld maakt Hallo volgende items:

* Een NAT-regel tootranslate alle binnenkomend verkeer op poort 3441 tooport 3389
* Een NAT-regel tootranslate alle binnenkomend verkeer op poort 3442 tooport 3389
* Een test regel toocheck Hallo gezondheidsstatus op een pagina met de naam **HealthProbe.aspx**
* Een load balancer-regel toobalance alle binnenkomend verkeer op poort 80 tooport 80 op Hallo adressen in Hallo back-end-pool
* Een load balancer die gebruikmaakt van al deze objecten

Volg deze stappen:

1. Hallo NAT-regels maken.

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. Maak een statustest. Er zijn twee manieren tooconfigure een test:

    HTTP-test

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    TPC-test

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. Maak een load balancer-regel.

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. Hallo load balancer maken met behulp van de objecten Hallo eerder hebt gemaakt.

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a>NIC's maken

Netwerkinterfaces te maken (of bestaande wijzigen) en vervolgens koppelen tooNAT regels, load balancer-regels en -tests:

1. Haal Hallo virtueel netwerk en een virtueel netwerksubnet waar Hallo NIC's moeten toobe gemaakt.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. Maak een NIC met de naam **lb nic1 worden**, en deze koppelen aan de eerste NAT-regel Hallo en Hallo eerste (en alleen) back-end-adresgroep.

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. Maak een NIC met de naam **lb nic2 worden**, en deze koppelen aan de tweede NAT-regel Hallo en Hallo eerste (en alleen) back-end-adresgroep.

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. Controleer Hallo NIC's.

        $backendnic1

    Verwachte uitvoer:

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
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
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. Gebruik Hallo `Add-AzureRmVMNetworkInterface` cmdlet tooassign Hallo NIC's toodifferent virtuele machines.

## <a name="create-a-virtual-machine"></a>Een virtuele machine maken

Zie voor instructies voor het maken van een virtuele machine en het toewijzen van een NIC [Een Azure-VM maken met behulp van PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface-toohello-load-balancer"></a>Hallo network interface toohello load balancer toevoegen

1. Hallo load balancer ophalen uit Azure.

    Hallo load balancerresource in een variabele laden (als u die nog niet hebt gedaan). Hallo variabele heet **$lb**. Gebruik hello dezelfde namen van Hallo load balancerresource die u eerder hebt gemaakt.

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. Hallo-back-end configuratie tooa variabele worden geladen.

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. Netwerkinterface Hallo al gemaakt in een variabele laden. Hallo variabelenaam is **$nic**. Hallo naam voor de netwerkinterface is Hallo dezelfde is als die van Hallo eerdere voorbeeld.

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. Hallo back-end-configuratie wijzigen op Hallo-netwerkinterface.

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. Sla Hallo netwerkinterface-object.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    Na een netwerkinterface is toohello load balancer back-end-adresgroep hebt toegevoegd, start het netwerkverkeer op basis van Hallo-taakverdeling regels voor de load balancerresource ontvangen.

## <a name="update-an-existing-load-balancer"></a>Een bestaande load balancer bijwerken

1. Met behulp van Hallo netwerktaakverdeler uit eerdere voorbeeld Hallo, een load balancer-toohello objectvariabele toewijzen **$slb** met behulp van `Get-AzureLoadBalancer`.

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. In de Hallo voorbeeld te volgen, voegt u een binnenkomende NAT-regel--met behulp van poort 81 in Hallo front-toepassingen en -poort 8181 voor Hallo back-end-pool--tooan bestaande load balancer.

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. Hallo nieuwe configuratie op te slaan met behulp van `Set-AzureLoadBalancer`.

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a>Een load balancer verwijderen

Gebruik de opdracht Hallo `Remove-AzureLoadBalancer` toodelete een eerder gemaakte load balancer met de naam **NRP LB** aangeroepen in een resourcegroep **NRP-RG**.

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> U kunt een optionele schakeloptie Hallo **-Force** tooavoid Hallo prompt voor verwijdering.

## <a name="next-steps"></a>Volgende stappen

[Aan de slag met het configureren van een interne load balancer](load-balancer-get-started-ilb-arm-ps.md)

[Een distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)
