---
title: aaaCreate een interne load balancer - Azure CLI | Microsoft Docs
description: Meer informatie over hoe toocreate een interne load balancer met behulp van Azure CLI in Resource Manager Hallo
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a>Een interne load balancer maken met behulp van hello Azure CLI

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Sjabloon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).  In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](load-balancer-get-started-ilb-classic-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a>Hallo-oplossing implementeren met behulp van hello Azure CLI

Hallo stappen laten zien hoe toocreate een internetgerichte netwerktaakverdeler met behulp van Azure Resource Manager met CLI. Met Azure Resource Manager elke bron wordt gemaakt en afzonderlijk geconfigureerd en vervolgens samengesteld toocreate een resource.

U moet toocreate en configureer Hallo objecten toodeploy een load balancer te volgen:

* **Front-end-IP-configuratie**: bevat openbare IP-adressen voor inkomend netwerkverkeer
* **Back-end-adresgroep**: netwerkinterfaces (NIC's) waarmee Hallo virtuele machines tooreceive netwerkverkeer van Hallo load balancer bevat
* **Regels voor taakverdeling**: bevat regels die een openbare poort op Hallo load balancer tooport in Hallo back-end-adresgroep toewijzen
* **NAT-regels voor binnenkomende verbindingen**: bevat regels die een openbare poort op Hallo load balancer tooa poort voor een specifieke virtuele machine in Hallo back-end-adresgroep toewijzen
* **Tests**: statuscontroles die gebruikt toocheck Hallo beschikbaarheid van exemplaren van virtuele machines in het back-end-adresgroep Hallo zijn bevat

Zie [Azure Resource Manager-ondersteuning voor load balancer](load-balancer-arm.md) voor meer informatie.

## <a name="set-up-cli-toouse-resource-manager"></a>CLI-toouse Resource Manager instellen

1. Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md). Volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.
2. Voer Hallo **azure config mode** opdracht tooswitch tooResource Manager-modus als volgt:

    ```azurecli
    azure config mode arm
    ```

    Verwachte uitvoer:

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a>Stapsgewijs een interne load balancer maken

1. Meld u aan tooAzure.

    ```azurecli
    azure login
    ```

    Voer uw Azure-referenties in wanneer dit wordt gevraagd.

2. Hallo opdracht Extra tooAzure Resource Manager-modus wijzigen.

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Alle resources in Azure Resource Manager zijn gekoppeld aan een resourcegroep. Maak een resourcegroep als u dit nog niet hebt gedaan.

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a>Een interne load balancer-set maken

1. Een interne load balancer maken

    In Hallo scenario te volgen, wordt een resourcegroep met de naam nrprg gemaakt in de regio VS-Oost.

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > Alle resources voor een interne load balancers, zoals virtuele netwerken en virtuele subnetten, moeten zich in dezelfde resourcegroep Hallo en Hallo in dezelfde regio.

2. Maak een front-end-IP-adres voor Hallo interne load balancer.

    Hallo IP-adres dat u gebruikt moet binnen het bereik van de Hallo subnet van het virtuele netwerk.

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. Hallo back-end-adresgroep maken.

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    Nadat u een front-end-IP-adres en een back-endadresgroep hebt gedefinieerd, kunt u load balancer-regels, inkomende NAT-regels en aangepaste statuscontroles maken.

4. Maak een load balancer-regel voor Hallo interne load balancer.

    Bij het uitvoeren van de vorige stappen Hallo Hallo opdracht maakt u een load balancer-regel voor luisteren tooport 1433 in Hallo front-endpool en verzenden taakverdeling netwerkverkeer toohello back-end-adresgroep, ook met behulp van poort 1433.

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. Maak inkomende NAT-regels.

    Binnenkomende NAT-regels zijn gebruikte toocreate-eindpunten in een load balancer die tooa specifieke virtuele machine exemplaar gaat. de vorige stappen Hallo gemaakt twee NAT-regels voor extern bureaublad.

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. Statuscontroles voor Hallo load balancer maken.

    Een health test controleert alle virtuele machine-exemplaren toomake zeker van te zijn dat ze netwerkverkeer kunnen verzenden. exemplaar van de virtuele machine Hallo met mislukte test controles wordt verwijderd van Hallo load balancer totdat deze weer online komt en een test-controle wordt bepaald of dit in orde is.

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > Hallo Microsoft Azure-platform gebruikt een statisch, openbaar routeerbare IPv4-adres voor een verscheidenheid aan scenario's voor beheer. Hallo IP-adres is 168.63.129.16. Dit IP-adres mag niet door firewalls worden geblokkeerd. Dit kan onverwacht gedrag veroorzaken.
    > Met opzicht tooAzure interne load balancing, wordt dit IP-adres gebruikt door de bewaking van de tests uit Hallo load balancer toodetermine Hallo-status voor virtuele machines in een set met gelijke taakverdeling. Als een netwerkbeveiligingsgroep gebruikte toorestrict verkeer tooAzure virtuele machines in een set met gelijke taakverdeling intern is of toegepaste tooa virtueel netwerksubnet, zorg ervoor dat een netwerkbeveiligingsregel tooallow verkeer vanuit 168.63.129.16 wordt toegevoegd.

## <a name="create-nics"></a>NIC's maken

U moet toocreate NIC's (of bestaande wijzigen) en deze koppelt tooNAT regels, load balancer-regels en -tests.

1. Maken van een NIC met de naam *lb nic1 worden*, en vervolgens te koppelen aan Hallo *rdp1* NAT regel en Hallo *beilb* back-end-adresgroep.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
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

2. Maken van een NIC met de naam *lb nic2 worden*, en vervolgens te koppelen aan Hallo *rdp2* NAT regel en Hallo *beilb* back-end-adresgroep.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. Maak een virtuele machine met de naam *DB1*, en vervolgens te koppelen aan Hallo NIC met de naam *lb nic1 worden*. Een opslagaccount aangeroepen *web1nrp* is gemaakt voordat Hallo na de opdracht is uitgevoerd:

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > Virtuele machines in een load balancer moet toobe in Hallo dezelfde beschikbaarheidsset. Gebruik `azure availset create` toocreate een beschikbaarheidsset.

4. Maak een virtuele machine (VM) met de naam *DB2*, en vervolgens te koppelen aan Hallo NIC met de naam *lb nic2 worden*. Een opslagaccount aangeroepen *web1nrp* is gemaakt voordat Hallo volgende opdracht wordt uitgevoerd.

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a>Een load balancer verwijderen

tooremove een load balancer, Hallo volgende opdracht gebruiken:

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a>Volgende stappen

[Een distributiemodus voor load balancer configureren met bron-IP-affiniteit](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)

