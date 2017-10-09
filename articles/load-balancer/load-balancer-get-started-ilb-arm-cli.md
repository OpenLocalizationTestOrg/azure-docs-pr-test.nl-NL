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
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a><span data-ttu-id="64f05-103">Een interne load balancer maken met behulp van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="64f05-103">Create an internal load balancer by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="64f05-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="64f05-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="64f05-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="64f05-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="64f05-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="64f05-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="64f05-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="64f05-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="64f05-108">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="64f05-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="64f05-109">In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](load-balancer-get-started-ilb-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="64f05-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a><span data-ttu-id="64f05-110">Hallo-oplossing implementeren met behulp van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="64f05-110">Deploy hello solution by using hello Azure CLI</span></span>

<span data-ttu-id="64f05-111">Hallo stappen laten zien hoe toocreate een internetgerichte netwerktaakverdeler met behulp van Azure Resource Manager met CLI.</span><span class="sxs-lookup"><span data-stu-id="64f05-111">hello following steps show how toocreate an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="64f05-112">Met Azure Resource Manager elke bron wordt gemaakt en afzonderlijk geconfigureerd en vervolgens samengesteld toocreate een resource.</span><span class="sxs-lookup"><span data-stu-id="64f05-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="64f05-113">U moet toocreate en configureer Hallo objecten toodeploy een load balancer te volgen:</span><span class="sxs-lookup"><span data-stu-id="64f05-113">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="64f05-114">**Front-end-IP-configuratie**: bevat openbare IP-adressen voor inkomend netwerkverkeer</span><span class="sxs-lookup"><span data-stu-id="64f05-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="64f05-115">**Back-end-adresgroep**: netwerkinterfaces (NIC's) waarmee Hallo virtuele machines tooreceive netwerkverkeer van Hallo load balancer bevat</span><span class="sxs-lookup"><span data-stu-id="64f05-115">**Back-end address pool**: contains network interfaces (NICs) that enable hello virtual machines tooreceive network traffic from hello load balancer</span></span>
* <span data-ttu-id="64f05-116">**Regels voor taakverdeling**: bevat regels die een openbare poort op Hallo load balancer tooport in Hallo back-end-adresgroep toewijzen</span><span class="sxs-lookup"><span data-stu-id="64f05-116">**Load-balancing rules**: contains rules that map a public port on hello load balancer tooport in hello back-end address pool</span></span>
* <span data-ttu-id="64f05-117">**NAT-regels voor binnenkomende verbindingen**: bevat regels die een openbare poort op Hallo load balancer tooa poort voor een specifieke virtuele machine in Hallo back-end-adresgroep toewijzen</span><span class="sxs-lookup"><span data-stu-id="64f05-117">**Inbound NAT rules**: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool</span></span>
* <span data-ttu-id="64f05-118">**Tests**: statuscontroles die gebruikt toocheck Hallo beschikbaarheid van exemplaren van virtuele machines in het back-end-adresgroep Hallo zijn bevat</span><span class="sxs-lookup"><span data-stu-id="64f05-118">**Probes**: contains health probes that are used toocheck hello availability of virtual machines instances in hello back-end address pool</span></span>

<span data-ttu-id="64f05-119">Zie [Azure Resource Manager-ondersteuning voor load balancer](load-balancer-arm.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="64f05-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="64f05-120">CLI-toouse Resource Manager instellen</span><span class="sxs-lookup"><span data-stu-id="64f05-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="64f05-121">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="64f05-121">If you have never used Azure CLI, see [Install and configure hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="64f05-122">Volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="64f05-122">Follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="64f05-123">Voer Hallo **azure config mode** opdracht tooswitch tooResource Manager-modus als volgt:</span><span class="sxs-lookup"><span data-stu-id="64f05-123">Run hello **azure config mode** command tooswitch tooResource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="64f05-124">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="64f05-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="64f05-125">Stapsgewijs een interne load balancer maken</span><span class="sxs-lookup"><span data-stu-id="64f05-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="64f05-126">Meld u aan tooAzure.</span><span class="sxs-lookup"><span data-stu-id="64f05-126">Sign in tooAzure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="64f05-127">Voer uw Azure-referenties in wanneer dit wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="64f05-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="64f05-128">Hallo opdracht Extra tooAzure Resource Manager-modus wijzigen.</span><span class="sxs-lookup"><span data-stu-id="64f05-128">Change hello command tools tooAzure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="64f05-129">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="64f05-129">Create a resource group</span></span>

<span data-ttu-id="64f05-130">Alle resources in Azure Resource Manager zijn gekoppeld aan een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="64f05-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="64f05-131">Maak een resourcegroep als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="64f05-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="64f05-132">Een interne load balancer-set maken</span><span class="sxs-lookup"><span data-stu-id="64f05-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="64f05-133">Een interne load balancer maken</span><span class="sxs-lookup"><span data-stu-id="64f05-133">Create an internal load balancer</span></span>

    <span data-ttu-id="64f05-134">In Hallo scenario te volgen, wordt een resourcegroep met de naam nrprg gemaakt in de regio VS-Oost.</span><span class="sxs-lookup"><span data-stu-id="64f05-134">In hello following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="64f05-135">Alle resources voor een interne load balancers, zoals virtuele netwerken en virtuele subnetten, moeten zich in dezelfde resourcegroep Hallo en Hallo in dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="64f05-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in hello same resource group and in hello same region.</span></span>

2. <span data-ttu-id="64f05-136">Maak een front-end-IP-adres voor Hallo interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="64f05-136">Create a front-end IP address for hello internal load balancer.</span></span>

    <span data-ttu-id="64f05-137">Hallo IP-adres dat u gebruikt moet binnen het bereik van de Hallo subnet van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="64f05-137">hello IP address that you use must be within hello subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="64f05-138">Hallo back-end-adresgroep maken.</span><span class="sxs-lookup"><span data-stu-id="64f05-138">Create hello back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="64f05-139">Nadat u een front-end-IP-adres en een back-endadresgroep hebt gedefinieerd, kunt u load balancer-regels, inkomende NAT-regels en aangepaste statuscontroles maken.</span><span class="sxs-lookup"><span data-stu-id="64f05-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="64f05-140">Maak een load balancer-regel voor Hallo interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="64f05-140">Create a load balancer rule for hello internal load balancer.</span></span>

    <span data-ttu-id="64f05-141">Bij het uitvoeren van de vorige stappen Hallo Hallo opdracht maakt u een load balancer-regel voor luisteren tooport 1433 in Hallo front-endpool en verzenden taakverdeling netwerkverkeer toohello back-end-adresgroep, ook met behulp van poort 1433.</span><span class="sxs-lookup"><span data-stu-id="64f05-141">When you follow hello previous steps, hello command creates a load-balancer rule for listening tooport 1433 in hello front-end pool and sending load-balanced network traffic toohello back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="64f05-142">Maak inkomende NAT-regels.</span><span class="sxs-lookup"><span data-stu-id="64f05-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="64f05-143">Binnenkomende NAT-regels zijn gebruikte toocreate-eindpunten in een load balancer die tooa specifieke virtuele machine exemplaar gaat.</span><span class="sxs-lookup"><span data-stu-id="64f05-143">Inbound NAT rules are used toocreate endpoints in a load balancer that go tooa specific virtual machine instance.</span></span> <span data-ttu-id="64f05-144">de vorige stappen Hallo gemaakt twee NAT-regels voor extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="64f05-144">hello previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="64f05-145">Statuscontroles voor Hallo load balancer maken.</span><span class="sxs-lookup"><span data-stu-id="64f05-145">Create health probes for hello load balancer.</span></span>

    <span data-ttu-id="64f05-146">Een health test controleert alle virtuele machine-exemplaren toomake zeker van te zijn dat ze netwerkverkeer kunnen verzenden.</span><span class="sxs-lookup"><span data-stu-id="64f05-146">A health probe checks all virtual machine instances toomake sure they can send network traffic.</span></span> <span data-ttu-id="64f05-147">exemplaar van de virtuele machine Hallo met mislukte test controles wordt verwijderd van Hallo load balancer totdat deze weer online komt en een test-controle wordt bepaald of dit in orde is.</span><span class="sxs-lookup"><span data-stu-id="64f05-147">hello virtual machine instance with failed probe checks is removed from hello load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="64f05-148">Hallo Microsoft Azure-platform gebruikt een statisch, openbaar routeerbare IPv4-adres voor een verscheidenheid aan scenario's voor beheer.</span><span class="sxs-lookup"><span data-stu-id="64f05-148">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="64f05-149">Hallo IP-adres is 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="64f05-149">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="64f05-150">Dit IP-adres mag niet door firewalls worden geblokkeerd. Dit kan onverwacht gedrag veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="64f05-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="64f05-151">Met opzicht tooAzure interne load balancing, wordt dit IP-adres gebruikt door de bewaking van de tests uit Hallo load balancer toodetermine Hallo-status voor virtuele machines in een set met gelijke taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="64f05-151">With respect tooAzure internal load balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="64f05-152">Als een netwerkbeveiligingsgroep gebruikte toorestrict verkeer tooAzure virtuele machines in een set met gelijke taakverdeling intern is of toegepaste tooa virtueel netwerksubnet, zorg ervoor dat een netwerkbeveiligingsregel tooallow verkeer vanuit 168.63.129.16 wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="64f05-152">If a network security group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa virtual network subnet, ensure that a network security rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="64f05-153">NIC's maken</span><span class="sxs-lookup"><span data-stu-id="64f05-153">Create NICs</span></span>

<span data-ttu-id="64f05-154">U moet toocreate NIC's (of bestaande wijzigen) en deze koppelt tooNAT regels, load balancer-regels en -tests.</span><span class="sxs-lookup"><span data-stu-id="64f05-154">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="64f05-155">Maken van een NIC met de naam *lb nic1 worden*, en vervolgens te koppelen aan Hallo *rdp1* NAT regel en Hallo *beilb* back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="64f05-155">Create an NIC named *lb-nic1-be*, and then associate it with hello *rdp1* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="64f05-156">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="64f05-156">Expected output:</span></span>

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

2. <span data-ttu-id="64f05-157">Maken van een NIC met de naam *lb nic2 worden*, en vervolgens te koppelen aan Hallo *rdp2* NAT regel en Hallo *beilb* back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="64f05-157">Create an NIC named *lb-nic2-be*, and then associate it with hello *rdp2* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="64f05-158">Maak een virtuele machine met de naam *DB1*, en vervolgens te koppelen aan Hallo NIC met de naam *lb nic1 worden*.</span><span class="sxs-lookup"><span data-stu-id="64f05-158">Create a virtual machine named *DB1*, and then associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="64f05-159">Een opslagaccount aangeroepen *web1nrp* is gemaakt voordat Hallo na de opdracht is uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="64f05-159">A storage account called *web1nrp* is created before hello following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="64f05-160">Virtuele machines in een load balancer moet toobe in Hallo dezelfde beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="64f05-160">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="64f05-161">Gebruik `azure availset create` toocreate een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="64f05-161">Use `azure availset create` toocreate an availability set.</span></span>

4. <span data-ttu-id="64f05-162">Maak een virtuele machine (VM) met de naam *DB2*, en vervolgens te koppelen aan Hallo NIC met de naam *lb nic2 worden*.</span><span class="sxs-lookup"><span data-stu-id="64f05-162">Create a virtual machine (VM) named *DB2*, and then associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="64f05-163">Een opslagaccount aangeroepen *web1nrp* is gemaakt voordat Hallo volgende opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="64f05-163">A storage account called *web1nrp* was created before running hello following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="64f05-164">Een load balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="64f05-164">Delete a load balancer</span></span>

<span data-ttu-id="64f05-165">tooremove een load balancer, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="64f05-165">tooremove a load balancer, use hello following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="64f05-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64f05-166">Next steps</span></span>

[<span data-ttu-id="64f05-167">Een distributiemodus voor load balancer configureren met bron-IP-affiniteit</span><span class="sxs-lookup"><span data-stu-id="64f05-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="64f05-168">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="64f05-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

