---
title: Azure CLI de load balancer - aaaCreate een internetgerichte | Microsoft Docs
description: Meer informatie over hoe een Internet gerichte load balancer bij het gebruik van Resource Manager toocreate hello Azure CLI
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a>Maken van een internet-load balancer hello Azure CLI gebruiken

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Sjabloon](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel. U kunt ook [meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler via de klassieke implementatie](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Hallo-oplossing met behulp van Azure CLI Hallo implementeren

Hallo stappen laten zien hoe toocreate een internetverbinding netwerktaakverdeler met Azure Resource Manager met CLI. Met Azure Resource Manager elke bron wordt gemaakt en afzonderlijk geconfigureerd, klikt u vervolgens samenstellen toocreate een resource.

U moet maken en configureren van Hallo objecten toodeploy een load balancer te volgen:

* Front-end-IP-configuratie: bevat openbare IP-adressen voor inkomend netwerkverkeer.
* Back-end-adresgroep - bevat netwerkinterfaces (NIC's) voor virtuele machines tooreceive-netwerkverkeer Hallo van Hallo load balancer.
* Taakverdeling regels - bevat regels voor toewijzing van een openbare poort op Hallo load balancer tooport in Hallo back-end-adresgroep.
* Binnenkomende NAT-regels: regels voor toewijzing van een openbare poort op Hallo load balancer tooa poort voor een specifieke virtuele machine in het back-end-adresgroep Hallo bevat.
* Tests - beschikbaarheid van health-tests gebruikt toocheck van exemplaren van virtuele machines in het back-end-adresgroep Hallo bevat.

Zie [Ondersteuning van Azure Resource Manager voor Azure Load Balancer](load-balancer-arm.md) voor meer informatie.

## <a name="set-up-cli-toouse-resource-manager"></a>CLI-toouse Resource Manager instellen

1. Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.
2. Voer Hallo **azure config mode** opdracht tooswitch tooResource modus Manager, zoals hieronder wordt weergegeven.

    ```azurecli
        azure config mode arm
    ```

    Verwachte uitvoer:

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Een virtueel netwerk en een openbare IP-adres voor Hallo front-end-IP-adresgroep maken

1. Maak een virtueel netwerk (VNet) met de naam *NRPVnet* in de locatie VS-Oost Hallo met behulp van een resourcegroep met de naam *NRPRG*.

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    Maak een subnet met de naam *NRPVnetSubnet* en een CIDR-blok 10.0.0.0/24 in *NRPVnet*.

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. Maken van een openbaar IP-adres met de naam *NRPPublicIP* toobe die wordt gebruikt door een front-end-IP-adresgroep met DNS-naam *loadbalancernrp.eastus.cloudapp.azure.com*. Hallo onderstaande opdracht maakt gebruik van statische Hallo-toewijzingstype en time-out voor inactiviteit van vier minuten.

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > Hallo load balancer Hallo domeinlabel van Hallo openbare IP-adres gebruikt als de FQDN. Deze een wijziging van de klassieke implementatie, die gebruikmaakt van Hallo cloudservice zoals Hallo load balancer Fully Qualified Domain Name (FQDN).
   > In dit voorbeeld Hallo FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.

## <a name="create-a-load-balancer"></a>Een load balancer maken

Hallo volgende opdracht maakt u een load balancer met de naam *NRPlb* in Hallo *NRPRG* resourcegroep in Hallo *VS-Oost* Azure-locatie.

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a>Een front-end-IP-adresgroep en back-endadresgroep maken
In dit voorbeeld laat zien hoe toocreate Hallo front-end-IP-adresgroep die binnenkomend netwerkverkeer op Hallo Hallo ontvangt de load balancer en Hallo back-end-IP-adresgroep waar front-pool Hallo Hallo taakverdeling netwerkverkeer verzendt.

1. Maak een front-end-IP-adresgroep Hallo openbare IP-adres gemaakt in de vorige stap Hallo en Hallo load balancer koppelen.

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. Instellen van een back-end-adresgroep gebruikt tooreceive binnenkomend verkeer vanuit Hallo front-end-IP-adresgroep.

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a>LB-regels, NAT-regels en test maken

Dit voorbeeld wordt de volgende items Hallo.

* een NAT-regel tootranslate alle binnenkomend verkeer op poort 21 tooport 22<sup>1</sup>
* een NAT-regel tootranslate alle binnenkomend verkeer op poort 23 tooport 22
* een load balancer-regel toobalance alle binnenkomend verkeer op poort 80 tooport 80 op Hallo adressen in Hallo back-end-pool.
* een test regel toocheck Hallo gezondheidsstatus op een pagina met de naam *HealthProbe.aspx*.

<sup>1</sup> NAT-regels zijn gekoppeld tooa specifieke virtuele machine exemplaar achter Hallo load balancer. Hallo-netwerkverkeer dat binnenkomt op poort 21 verzonden tooa specifieke virtuele machine op poort 22 die zijn gekoppeld aan deze NAT-regel. U moet een protocol (UDP of TCP) voor een NAT-regel opgeven. Beide protocollen kunnen niet worden toegewezen toohello dezelfde poort.

1. Hallo NAT-regels maken.

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. Maak een load balancer-regel.

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. Maak een statustest.

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. Controleer uw instellingen.

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    Verwachte uitvoer:

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a>NIC's maken

U moet toocreate NIC's (of bestaande wijzigen) en deze koppelt tooNAT regels, load balancer-regels en -tests.

1. Maak een NIC met de naam *lb nic1 worden*, en deze koppelen aan Hallo *rdp1* NAT-regel en Hallo *NRPbackendpool* back-end-adresgroep.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    Verwachte uitvoer:

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. Maak een NIC met de naam *lb nic2 worden*, en deze koppelen aan Hallo *rdp2* NAT-regel en Hallo *NRPbackendpool* back-end-adresgroep.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. Maak een virtuele machine (VM) met de naam *web1*, en deze koppelen aan Hallo NIC met de naam *lb nic1 worden*. Een opslagaccount aangeroepen *web1nrp* is gemaakt voordat Hallo onderstaande opdracht wordt uitgevoerd.

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > Virtuele machines in een load balancer moet toobe in Hallo dezelfde beschikbaarheidsset. Gebruik `azure availset create` toocreate een beschikbaarheidsset.

    Hallo-uitvoer moet vergelijkbaar toohello volgende:

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > Hallo informatiebericht **dit is een NIC zonder publicIP geconfigureerd** sinds hello NIC gemaakt voor Hallo load balancer verbinding te maken met Hallo load balancer openbare IP-adres tooInternet wordt verwacht.

    Sinds Hallo *lb nic1 worden* NIC is gekoppeld aan Hallo *rdp1* NAT-regel, kunt u te*web1* met RDP via poort 3441 op Hallo load balancer.

4. Maak een virtuele machine (VM) met de naam *web2*, en deze koppelen aan Hallo NIC met de naam *lb nic2 worden*. Een opslagaccount aangeroepen *web1nrp* is gemaakt voordat Hallo onderstaande opdracht wordt uitgevoerd.

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a>Een bestaande load balancer bijwerken
U kunt regels toevoegen die naar een bestaande load balancer verwijzen. In het volgende voorbeeld hello, een nieuwe regel voor load balancer tooan bestaande load balancer wordt toegevoegd **NRPlb**

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a>Een load balancer verwijderen
Gebruik Hallo opdracht tooremove een load balancer te volgen:

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a>Volgende stappen
[Aan de slag met het configureren van een interne load balancer](load-balancer-get-started-ilb-arm-cli.md)

[Een distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)
