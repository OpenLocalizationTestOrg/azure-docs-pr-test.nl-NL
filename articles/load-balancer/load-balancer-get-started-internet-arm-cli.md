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
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a><span data-ttu-id="0994d-103">Maken van een internet-load balancer hello Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="0994d-103">Creating an internet load balancer using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0994d-104">Portal</span><span class="sxs-lookup"><span data-stu-id="0994d-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="0994d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0994d-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="0994d-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0994d-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="0994d-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="0994d-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="0994d-108">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="0994d-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="0994d-109">U kunt ook [meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler via de klassieke implementatie](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0994d-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="0994d-110">Hallo-oplossing met behulp van Azure CLI Hallo implementeren</span><span class="sxs-lookup"><span data-stu-id="0994d-110">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="0994d-111">Hallo stappen laten zien hoe toocreate een internetverbinding netwerktaakverdeler met Azure Resource Manager met CLI.</span><span class="sxs-lookup"><span data-stu-id="0994d-111">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="0994d-112">Met Azure Resource Manager elke bron wordt gemaakt en afzonderlijk geconfigureerd, klikt u vervolgens samenstellen toocreate een resource.</span><span class="sxs-lookup"><span data-stu-id="0994d-112">With Azure Resource Manager each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="0994d-113">U moet maken en configureren van Hallo objecten toodeploy een load balancer te volgen:</span><span class="sxs-lookup"><span data-stu-id="0994d-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="0994d-114">Front-end-IP-configuratie: bevat openbare IP-adressen voor inkomend netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="0994d-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="0994d-115">Back-end-adresgroep - bevat netwerkinterfaces (NIC's) voor virtuele machines tooreceive-netwerkverkeer Hallo van Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="0994d-115">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="0994d-116">Taakverdeling regels - bevat regels voor toewijzing van een openbare poort op Hallo load balancer tooport in Hallo back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="0994d-116">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="0994d-117">Binnenkomende NAT-regels: regels voor toewijzing van een openbare poort op Hallo load balancer tooa poort voor een specifieke virtuele machine in het back-end-adresgroep Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="0994d-117">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="0994d-118">Tests - beschikbaarheid van health-tests gebruikt toocheck van exemplaren van virtuele machines in het back-end-adresgroep Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="0994d-118">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="0994d-119">Zie [Ondersteuning van Azure Resource Manager voor Azure Load Balancer](load-balancer-arm.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0994d-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="0994d-120">CLI-toouse Resource Manager instellen</span><span class="sxs-lookup"><span data-stu-id="0994d-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="0994d-121">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="0994d-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="0994d-122">Voer Hallo **azure config mode** opdracht tooswitch tooResource modus Manager, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0994d-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="0994d-123">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="0994d-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="0994d-124">Een virtueel netwerk en een openbare IP-adres voor Hallo front-end-IP-adresgroep maken</span><span class="sxs-lookup"><span data-stu-id="0994d-124">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="0994d-125">Maak een virtueel netwerk (VNet) met de naam *NRPVnet* in de locatie VS-Oost Hallo met behulp van een resourcegroep met de naam *NRPRG*.</span><span class="sxs-lookup"><span data-stu-id="0994d-125">Create a virtual network (VNet) named *NRPVnet* in hello East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="0994d-126">Maak een subnet met de naam *NRPVnetSubnet* en een CIDR-blok 10.0.0.0/24 in *NRPVnet*.</span><span class="sxs-lookup"><span data-stu-id="0994d-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="0994d-127">Maken van een openbaar IP-adres met de naam *NRPPublicIP* toobe die wordt gebruikt door een front-end-IP-adresgroep met DNS-naam *loadbalancernrp.eastus.cloudapp.azure.com*. Hallo onderstaande opdracht maakt gebruik van statische Hallo-toewijzingstype en time-out voor inactiviteit van vier minuten.</span><span class="sxs-lookup"><span data-stu-id="0994d-127">Create a public IP address named *NRPPublicIP* toobe used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*. hello command below uses hello static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="0994d-128">Hallo load balancer Hallo domeinlabel van Hallo openbare IP-adres gebruikt als de FQDN.</span><span class="sxs-lookup"><span data-stu-id="0994d-128">hello load balancer will use hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="0994d-129">Deze een wijziging van de klassieke implementatie, die gebruikmaakt van Hallo cloudservice zoals Hallo load balancer Fully Qualified Domain Name (FQDN).</span><span class="sxs-lookup"><span data-stu-id="0994d-129">This a change from classic deployment, which uses hello cloud service as hello load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="0994d-130">In dit voorbeeld Hallo FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="0994d-130">In this example, hello FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="0994d-131">Een load balancer maken</span><span class="sxs-lookup"><span data-stu-id="0994d-131">Create a load balancer</span></span>

<span data-ttu-id="0994d-132">Hallo volgende opdracht maakt u een load balancer met de naam *NRPlb* in Hallo *NRPRG* resourcegroep in Hallo *VS-Oost* Azure-locatie.</span><span class="sxs-lookup"><span data-stu-id="0994d-132">hello following command creates a load balancer named *NRPlb* in hello *NRPRG* resource group in hello *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="0994d-133">Een front-end-IP-adresgroep en back-endadresgroep maken</span><span class="sxs-lookup"><span data-stu-id="0994d-133">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="0994d-134">In dit voorbeeld laat zien hoe toocreate Hallo front-end-IP-adresgroep die binnenkomend netwerkverkeer op Hallo Hallo ontvangt de load balancer en Hallo back-end-IP-adresgroep waar front-pool Hallo Hallo taakverdeling netwerkverkeer verzendt.</span><span class="sxs-lookup"><span data-stu-id="0994d-134">This example demonstrates how toocreate hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello backend IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="0994d-135">Maak een front-end-IP-adresgroep Hallo openbare IP-adres gemaakt in de vorige stap Hallo en Hallo load balancer koppelen.</span><span class="sxs-lookup"><span data-stu-id="0994d-135">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="0994d-136">Instellen van een back-end-adresgroep gebruikt tooreceive binnenkomend verkeer vanuit Hallo front-end-IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="0994d-136">Set up a back-end address pool used tooreceive incoming traffic from hello front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="0994d-137">LB-regels, NAT-regels en test maken</span><span class="sxs-lookup"><span data-stu-id="0994d-137">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="0994d-138">Dit voorbeeld wordt de volgende items Hallo.</span><span class="sxs-lookup"><span data-stu-id="0994d-138">This example creates hello following items.</span></span>

* <span data-ttu-id="0994d-139">een NAT-regel tootranslate alle binnenkomend verkeer op poort 21 tooport 22<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="0994d-139">a NAT rule tootranslate all incoming traffic on port 21 tooport 22<sup>1</sup></span></span>
* <span data-ttu-id="0994d-140">een NAT-regel tootranslate alle binnenkomend verkeer op poort 23 tooport 22</span><span class="sxs-lookup"><span data-stu-id="0994d-140">a NAT rule tootranslate all incoming traffic on port 23 tooport 22</span></span>
* <span data-ttu-id="0994d-141">een load balancer-regel toobalance alle binnenkomend verkeer op poort 80 tooport 80 op Hallo adressen in Hallo back-end-pool.</span><span class="sxs-lookup"><span data-stu-id="0994d-141">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="0994d-142">een test regel toocheck Hallo gezondheidsstatus op een pagina met de naam *HealthProbe.aspx*.</span><span class="sxs-lookup"><span data-stu-id="0994d-142">a probe rule toocheck hello health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="0994d-143"><sup>1</sup> NAT-regels zijn gekoppeld tooa specifieke virtuele machine exemplaar achter Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="0994d-143"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="0994d-144">Hallo-netwerkverkeer dat binnenkomt op poort 21 verzonden tooa specifieke virtuele machine op poort 22 die zijn gekoppeld aan deze NAT-regel.</span><span class="sxs-lookup"><span data-stu-id="0994d-144">hello network traffic arriving on port 21 is sent tooa specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="0994d-145">U moet een protocol (UDP of TCP) voor een NAT-regel opgeven.</span><span class="sxs-lookup"><span data-stu-id="0994d-145">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="0994d-146">Beide protocollen kunnen niet worden toegewezen toohello dezelfde poort.</span><span class="sxs-lookup"><span data-stu-id="0994d-146">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="0994d-147">Hallo NAT-regels maken.</span><span class="sxs-lookup"><span data-stu-id="0994d-147">Create hello NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="0994d-148">Maak een load balancer-regel.</span><span class="sxs-lookup"><span data-stu-id="0994d-148">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="0994d-149">Maak een statustest.</span><span class="sxs-lookup"><span data-stu-id="0994d-149">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="0994d-150">Controleer uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="0994d-150">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="0994d-151">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="0994d-151">Expected output:</span></span>

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

## <a name="create-nics"></a><span data-ttu-id="0994d-152">NIC's maken</span><span class="sxs-lookup"><span data-stu-id="0994d-152">Create NICs</span></span>

<span data-ttu-id="0994d-153">U moet toocreate NIC's (of bestaande wijzigen) en deze koppelt tooNAT regels, load balancer-regels en -tests.</span><span class="sxs-lookup"><span data-stu-id="0994d-153">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="0994d-154">Maak een NIC met de naam *lb nic1 worden*, en deze koppelen aan Hallo *rdp1* NAT-regel en Hallo *NRPbackendpool* back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="0994d-154">Create a NIC named *lb-nic1-be*, and associate it with hello *rdp1* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="0994d-155">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="0994d-155">Expected output:</span></span>

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

2. <span data-ttu-id="0994d-156">Maak een NIC met de naam *lb nic2 worden*, en deze koppelen aan Hallo *rdp2* NAT-regel en Hallo *NRPbackendpool* back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="0994d-156">Create a NIC named *lb-nic2-be*, and associate it with hello *rdp2* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="0994d-157">Maak een virtuele machine (VM) met de naam *web1*, en deze koppelen aan Hallo NIC met de naam *lb nic1 worden*.</span><span class="sxs-lookup"><span data-stu-id="0994d-157">Create a virtual machine (VM) named *web1*, and associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="0994d-158">Een opslagaccount aangeroepen *web1nrp* is gemaakt voordat Hallo onderstaande opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0994d-158">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="0994d-159">Virtuele machines in een load balancer moet toobe in Hallo dezelfde beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="0994d-159">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="0994d-160">Gebruik `azure availset create` toocreate een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="0994d-160">Use `azure availset create` toocreate an availability set.</span></span>

    <span data-ttu-id="0994d-161">Hallo-uitvoer moet vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="0994d-161">hello output should be similar toohello following:</span></span>

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
    > <span data-ttu-id="0994d-162">Hallo informatiebericht **dit is een NIC zonder publicIP geconfigureerd** sinds hello NIC gemaakt voor Hallo load balancer verbinding te maken met Hallo load balancer openbare IP-adres tooInternet wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="0994d-162">hello informational message **This is a NIC without publicIP configured** is expected since hello NIC created for hello load balancer connecting tooInternet using hello load balancer public IP address.</span></span>

    <span data-ttu-id="0994d-163">Sinds Hallo *lb nic1 worden* NIC is gekoppeld aan Hallo *rdp1* NAT-regel, kunt u te*web1* met RDP via poort 3441 op Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="0994d-163">Since hello *lb-nic1-be* NIC is associated with hello *rdp1* NAT rule, you can connect too*web1* using RDP through port 3441 on hello load balancer.</span></span>

4. <span data-ttu-id="0994d-164">Maak een virtuele machine (VM) met de naam *web2*, en deze koppelen aan Hallo NIC met de naam *lb nic2 worden*.</span><span class="sxs-lookup"><span data-stu-id="0994d-164">Create a virtual machine (VM) named *web2*, and associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="0994d-165">Een opslagaccount aangeroepen *web1nrp* is gemaakt voordat Hallo onderstaande opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0994d-165">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="0994d-166">Een bestaande load balancer bijwerken</span><span class="sxs-lookup"><span data-stu-id="0994d-166">Update an existing load balancer</span></span>
<span data-ttu-id="0994d-167">U kunt regels toevoegen die naar een bestaande load balancer verwijzen.</span><span class="sxs-lookup"><span data-stu-id="0994d-167">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="0994d-168">In het volgende voorbeeld hello, een nieuwe regel voor load balancer tooan bestaande load balancer wordt toegevoegd **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="0994d-168">In hello next example, a new load balancer rule is added tooan existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="0994d-169">Een load balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="0994d-169">Delete a load balancer</span></span>
<span data-ttu-id="0994d-170">Gebruik Hallo opdracht tooremove een load balancer te volgen:</span><span class="sxs-lookup"><span data-stu-id="0994d-170">Use hello following command tooremove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="0994d-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0994d-171">Next steps</span></span>
[<span data-ttu-id="0994d-172">Aan de slag met het configureren van een interne load balancer</span><span class="sxs-lookup"><span data-stu-id="0994d-172">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="0994d-173">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="0994d-173">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="0994d-174">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="0994d-174">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
