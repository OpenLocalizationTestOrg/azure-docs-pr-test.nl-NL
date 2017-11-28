---
title: Een interne load balancer maken - Azure CLI | Microsoft Docs
description: Informatie over hoe u met Azure CLI een interne load balancer maakt in Resource Manager
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
ms.openlocfilehash: 128b91c685b5f7e494a69ca5b04165a0ee7cbb78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-by-using-the-azure-cli"></a><span data-ttu-id="7a5d7-103">Een interne load balancer maken met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7a5d7-103">Create an internal load balancer by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a5d7-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7a5d7-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="7a5d7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a5d7-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="7a5d7-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7a5d7-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="7a5d7-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="7a5d7-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="7a5d7-108">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7a5d7-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="7a5d7-109">Dit artikel bevat informatie over het Resource Manager-implementatiemodel, dat door Microsoft wordt aanbevolen voor de meeste nieuwe implementaties in plaats van het [klassieke implementatiemodel](load-balancer-get-started-ilb-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7a5d7-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-solution-by-using-the-azure-cli"></a><span data-ttu-id="7a5d7-110">De oplossing implementeren met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7a5d7-110">Deploy the solution by using the Azure CLI</span></span>

<span data-ttu-id="7a5d7-111">De volgende stappen laten zien hoe u Azure Resource Manager gebruikt om een internetgerichte load balancer te maken met behulp van CLI.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-111">The following steps show how to create an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="7a5d7-112">Met Azure Resource Manager wordt elke resource afzonderlijk gemaakt en geconfigureerd, en vervolgens samengevoegd om een resource te maken.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="7a5d7-113">U moet de volgende objecten maken en configureren om een load balancer te implementeren:</span><span class="sxs-lookup"><span data-stu-id="7a5d7-113">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="7a5d7-114">**Front-end-IP-configuratie**: bevat openbare IP-adressen voor inkomend netwerkverkeer</span><span class="sxs-lookup"><span data-stu-id="7a5d7-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="7a5d7-115">**Back-endadresgroep**: bevat netwerkinterfaces (NIC's) waardoor de virtuele machines netwerkverkeer kunnen ontvangen van de load balancer</span><span class="sxs-lookup"><span data-stu-id="7a5d7-115">**Back-end address pool**: contains network interfaces (NICs) that enable the virtual machines to receive network traffic from the load balancer</span></span>
* <span data-ttu-id="7a5d7-116">**Regels voor taakverdeling**: bevat regels die een openbare poort op de load balancer toewijst aan een poort in de back-endadresgroep</span><span class="sxs-lookup"><span data-stu-id="7a5d7-116">**Load-balancing rules**: contains rules that map a public port on the load balancer to port in the back-end address pool</span></span>
* <span data-ttu-id="7a5d7-117">**Inkomende NAT-regels**: bevat regels die een openbare poort op de load balancer toewijst aan een poort voor een specifieke virtuele machine in de back-endadresgroep</span><span class="sxs-lookup"><span data-stu-id="7a5d7-117">**Inbound NAT rules**: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool</span></span>
* <span data-ttu-id="7a5d7-118">**Tests**: bevat statuscontroles die worden gebruikt om de beschikbaarheid van exemplaren van virtuele machines in de back-endadresgroep te controleren</span><span class="sxs-lookup"><span data-stu-id="7a5d7-118">**Probes**: contains health probes that are used to check the availability of virtual machines instances in the back-end address pool</span></span>

<span data-ttu-id="7a5d7-119">Zie [Azure Resource Manager-ondersteuning voor load balancer](load-balancer-arm.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-to-use-resource-manager"></a><span data-ttu-id="7a5d7-120">CLI instellen voor het gebruik van Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7a5d7-120">Set up CLI to use Resource Manager</span></span>

1. <span data-ttu-id="7a5d7-121">Zie [Install and configure the Azure CLI](../cli-install-nodejs.md) (Azure CLI installeren en configureren) als u Azure CLI nog nooit hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-121">If you have never used Azure CLI, see [Install and configure the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="7a5d7-122">Volg de instructies tot het punt waar u uw Azure-account en -abonnement selecteert.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-122">Follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="7a5d7-123">Voer de opdracht **azure config mode** als volgt uit om over te schakelen naar de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-123">Run the **azure config mode** command to switch to Resource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="7a5d7-124">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="7a5d7-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="7a5d7-125">Stapsgewijs een interne load balancer maken</span><span class="sxs-lookup"><span data-stu-id="7a5d7-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="7a5d7-126">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-126">Sign in to Azure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="7a5d7-127">Voer uw Azure-referenties in wanneer dit wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="7a5d7-128">Wijzig de opdrachthulpprogramma's in de modus Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-128">Change the command tools to Azure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="7a5d7-129">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="7a5d7-129">Create a resource group</span></span>

<span data-ttu-id="7a5d7-130">Alle resources in Azure Resource Manager zijn gekoppeld aan een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="7a5d7-131">Maak een resourcegroep als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="7a5d7-132">Een interne load balancer-set maken</span><span class="sxs-lookup"><span data-stu-id="7a5d7-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="7a5d7-133">Een interne load balancer maken</span><span class="sxs-lookup"><span data-stu-id="7a5d7-133">Create an internal load balancer</span></span>

    <span data-ttu-id="7a5d7-134">In het volgende scenario wordt een resourcegroep met de naam nrprg gemaakt in de regio VS - oost.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-134">In the following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="7a5d7-135">Alle resources voor een interne load balancer, zoals virtuele netwerken en virtuele subnetten van netwerken, moeten zich in dezelfde resourcegroep en in dezelfde regio bevinden.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in the same resource group and in the same region.</span></span>

2. <span data-ttu-id="7a5d7-136">Maak een front-end-IP-adres voor de interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-136">Create a front-end IP address for the internal load balancer.</span></span>

    <span data-ttu-id="7a5d7-137">Het IP-adres dat u gebruikt, moet zich binnen het subnetbereik van het virtuele netwerk bevinden.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-137">The IP address that you use must be within the subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="7a5d7-138">Maak de back-endadresgroep.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-138">Create the back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="7a5d7-139">Nadat u een front-end-IP-adres en een back-endadresgroep hebt gedefinieerd, kunt u load balancer-regels, inkomende NAT-regels en aangepaste statuscontroles maken.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="7a5d7-140">Maak een load balancer-regel voor de interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-140">Create a load balancer rule for the internal load balancer.</span></span>

    <span data-ttu-id="7a5d7-141">Wanneer u de vorige stappen hebt gevolgd, maakt de opdracht een load balancer-regel voor het luisteren naar poort 1433 in de front-endpool en verzendt deze netwerkverkeer met taakverdeling naar de back-endadresgroep, waarbij ook gebruik wordt gemaakt van poort 1433.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-141">When you follow the previous steps, the command creates a load-balancer rule for listening to port 1433 in the front-end pool and sending load-balanced network traffic to the back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="7a5d7-142">Maak inkomende NAT-regels.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="7a5d7-143">Inkomende NAT-regels worden gebruikt om eindpunten in een load balancer te maken die naar een specifiek exemplaar van een virtuele machine gaan.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-143">Inbound NAT rules are used to create endpoints in a load balancer that go to a specific virtual machine instance.</span></span> <span data-ttu-id="7a5d7-144">Met de vorige stappen zijn twee NAT-regels voor een extern bureaublad gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-144">The previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="7a5d7-145">Maak statuscontroles voor de load balancer.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-145">Create health probes for the load balancer.</span></span>

    <span data-ttu-id="7a5d7-146">Een statuscontrole controleert alle exemplaren van de virtuele machines om ervoor te zorgen dat deze netwerkverkeer kunnen verzenden.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-146">A health probe checks all virtual machine instances to make sure they can send network traffic.</span></span> <span data-ttu-id="7a5d7-147">Het exemplaar van een virtuele machine met mislukte testcontroles wordt uit de load balancer verwijderd totdat deze weer online komt en een testcontrole bepaalt of deze in orde is.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-147">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="7a5d7-148">Het Microsoft Azure-platform gebruikt een statisch, openbaar routeerbaar IPv4-adres voor diverse beheerscenario's.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-148">The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="7a5d7-149">Het IP-adres is 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-149">The IP address is 168.63.129.16.</span></span> <span data-ttu-id="7a5d7-150">Dit IP-adres mag niet door firewalls worden geblokkeerd. Dit kan onverwacht gedrag veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="7a5d7-151">Wat Azure interne taakverdeling betreft, wordt dit IP-adres gebruikt door bewakingstests van de load balancer om de status van virtuele machines in een set met gelijke taakverdeling te bepalen.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-151">With respect to Azure internal load balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="7a5d7-152">Als er een netwerkbeveiligingsgroep wordt gebruikt om het verkeer naar virtuele Azure-machines in een set met intern gelijke taakverdeling te beperken of wordt toegepast op een subnet in een virtueel netwerk, zorg er dan voor dat er een netwerkbeveiligingsregel wordt toegevoegd om verkeer van 168.63.129.16 toe te staan.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-152">If a network security group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a virtual network subnet, ensure that a network security rule is added to allow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="7a5d7-153">NIC's maken</span><span class="sxs-lookup"><span data-stu-id="7a5d7-153">Create NICs</span></span>

<span data-ttu-id="7a5d7-154">U moet NIC's maken (of bestaande wijzigen) en deze koppelen aan NAT-regels, load balancer-regels en tests.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="7a5d7-155">Maak een NIC met de naam *lb-nic1-be*, en koppel deze vervolgens aan de NAT-regel *rdp1* en de back-endadresgroep *beilb*.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-155">Create an NIC named *lb-nic1-be*, and then associate it with the *rdp1* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="7a5d7-156">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="7a5d7-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up the network interface "lb-nic1-be"
        + Looking up the subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up the network interface "lb-nic1-be"
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

2. <span data-ttu-id="7a5d7-157">Maak een NIC met de naam *lb-nic2-be*, en koppel deze vervolgens aan de NAT-regel *rdp2* en de back-endadresgroep *beilb*.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-157">Create an NIC named *lb-nic2-be*, and then associate it with the *rdp2* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="7a5d7-158">Maak een virtuele machine met de naam *DB1* en koppel deze vervolgens aan de NIC met de naam *lb-nic1-be*.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-158">Create a virtual machine named *DB1*, and then associate it with the NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="7a5d7-159">Voordat onderstaande opdracht wordt uitgevoerd, wordt er een opslagaccount met de naam *web1nrp* gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-159">A storage account called *web1nrp* is created before the following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="7a5d7-160">Virtuele machines in een load balancer moeten zich in dezelfde beschikbaarheidsset bevinden.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-160">VMs in a load balancer need to be in the same availability set.</span></span> <span data-ttu-id="7a5d7-161">Gebruik `azure availset create` om een beschikbaarheidsset te maken.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-161">Use `azure availset create` to create an availability set.</span></span>

4. <span data-ttu-id="7a5d7-162">Maak een virtuele machine (VM) met de naam *DB2* en koppel deze vervolgens aan de NIC met de naam *lb-nic2-be*.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-162">Create a virtual machine (VM) named *DB2*, and then associate it with the NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="7a5d7-163">Voordat onderstaande opdracht wordt uitgevoerd, wordt er een opslagaccount met de naam *web1nrp* gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7a5d7-163">A storage account called *web1nrp* was created before running the following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="7a5d7-164">Een load balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="7a5d7-164">Delete a load balancer</span></span>

<span data-ttu-id="7a5d7-165">Gebruik de volgende opdracht om een load balancer te verwijderen:</span><span class="sxs-lookup"><span data-stu-id="7a5d7-165">To remove a load balancer, use the following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="7a5d7-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7a5d7-166">Next steps</span></span>

[<span data-ttu-id="7a5d7-167">Een distributiemodus voor load balancer configureren met bron-IP-affiniteit</span><span class="sxs-lookup"><span data-stu-id="7a5d7-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="7a5d7-168">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="7a5d7-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

