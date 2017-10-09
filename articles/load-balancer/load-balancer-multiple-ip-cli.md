---
title: aaaLoad balancing op meerdere IP-configuraties met Azure CLI | Microsoft Docs
description: Meer informatie over hoe tooassign meerdere IP-adressen tooa virtuele machine met Azure CLI | Resource Manager.
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: annahar
ms.openlocfilehash: df81e1b8193f274bad435d6b506c7be824117416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="c3cd0-103">De Load Balancer op meerdere IP-configuraties</span><span class="sxs-lookup"><span data-stu-id="c3cd0-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3cd0-104">Portal</span><span class="sxs-lookup"><span data-stu-id="c3cd0-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="c3cd0-105">CLI</span><span class="sxs-lookup"><span data-stu-id="c3cd0-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="c3cd0-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3cd0-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="c3cd0-107">Dit artikel wordt beschreven hoe toouse Azure Load Balancer met meerdere IP-adressen op een secundaire netwerkinterface (NIC).</span><span class="sxs-lookup"><span data-stu-id="c3cd0-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="c3cd0-108">In dit scenario hebben we twee virtuele machines met Windows, elk met een primaire en een secundaire NIC.</span><span class="sxs-lookup"><span data-stu-id="c3cd0-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="c3cd0-109">Elk van de secundaire Hallo NIC's, hebben twee IP-configuraties.</span><span class="sxs-lookup"><span data-stu-id="c3cd0-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="c3cd0-110">Elke virtuele machine fungeert als host van websites contoso.com en fabrikam.com. Elke website is gebonden tooone Hallo IP-configuraties op Hallo secundaire NIC.</span><span class="sxs-lookup"><span data-stu-id="c3cd0-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="c3cd0-111">We gebruiken Azure Load Balancer tooexpose twee frontend IP-adressen, één voor elke website, toodistribute verkeer toohello respectieve IP-configuratie voor Hallo-website.</span><span class="sxs-lookup"><span data-stu-id="c3cd0-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="c3cd0-112">Dit scenario maakt gebruik van hetzelfde poortnummer Hallo over zowel frontends, evenals het IP-adressen van zowel back-end-groep.</span><span class="sxs-lookup"><span data-stu-id="c3cd0-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![De installatiekopie van de Load Balancer-scenario](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="c3cd0-114">Stappen tooload verdelen over meerdere IP-configuraties</span><span class="sxs-lookup"><span data-stu-id="c3cd0-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="c3cd0-115">Hallo stappen hieronder tooachieve Hallo scenario in dit artikel wordt beschreven:</span><span class="sxs-lookup"><span data-stu-id="c3cd0-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="c3cd0-116">[Installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) hello Azure CLI aan de hand van Hallo stappen in de gekoppelde artikel Hallo en het logboek in uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c3cd0-116">[Install and Configure hello Azure CLI](../cli-install-nodejs.md) hello Azure CLI by following hello steps in hello linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="c3cd0-117">[Een resourcegroep maken](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) aangeroepen *contosofabrikam* zoals hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="c3cd0-117">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="c3cd0-118">[Maken van een beschikbaarheidsset](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor Hallo twee virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c3cd0-118">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello two VMs.</span></span> <span data-ttu-id="c3cd0-119">Gebruik voor dit scenario Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c3cd0-119">For this scenario, use hello following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="c3cd0-120">[Een virtueel netwerk maken](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) aangeroepen *myVNet* en een subnet met de naam *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="c3cd0-120">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="c3cd0-121">[Hallo load balancer maken](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) aangeroepen *mylb*:</span><span class="sxs-lookup"><span data-stu-id="c3cd0-121">[Create hello load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="c3cd0-122">Maak twee dynamische openbare IP-adressen voor Hallo frontend-IP-configuraties van de load balancer:</span><span class="sxs-lookup"><span data-stu-id="c3cd0-122">Create two dynamic public IP addresses for hello frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="c3cd0-123">Hallo twee frontend-IP-configuraties maken *contosofe* en *fabrikamfe* respectievelijk:</span><span class="sxs-lookup"><span data-stu-id="c3cd0-123">Create hello two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="c3cd0-124">Maken van uw back-end-adresgroepen - *contosopool* en *fabrikampool*, een [test](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, en de belasting balancingregels - *HTTPc* en *HTTPf*:</span><span class="sxs-lookup"><span data-stu-id="c3cd0-124">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="c3cd0-125">Voer Hallo volgende opdracht hieronder en vervolgens te controleren Hallo uitvoer[Controleer of de load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) correct is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="c3cd0-125">Run hello following command below and then check hello output too[verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="c3cd0-126">[Maken van een openbaar IP-adres](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, en [opslagaccount](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* voor uw eerste virtuele machine VM1 zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="c3cd0-126">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="c3cd0-127">[Hallo netwerkinterfaces te maken](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) voor VM1 en voeg een tweede IP-configuratie, *VM1 ipconfig2*, en [Hallo VM maken](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="c3cd0-127">[Create hello network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create hello VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="c3cd0-128">Herhaal stap 10 11 voor uw tweede VM:</span><span class="sxs-lookup"><span data-stu-id="c3cd0-128">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="c3cd0-129">Tot slot moet u DNS-resource records toopoint toohello respectieve frontend IP-adres van de Load Balancer Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="c3cd0-129">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="c3cd0-130">U kunt uw domeinen in Azure DNS hosten.</span><span class="sxs-lookup"><span data-stu-id="c3cd0-130">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="c3cd0-131">Zie voor meer informatie over het gebruik van Azure DNS met Load Balancer [met behulp van Azure DNS met andere Azure-services](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="c3cd0-131">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3cd0-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c3cd0-132">Next steps</span></span>
- <span data-ttu-id="c3cd0-133">Meer informatie over hoe toocombine load balancing-services in Azure in [met gelijke taakverdeling van services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="c3cd0-133">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="c3cd0-134">Meer informatie over hoe u verschillende typen Logboeken gebruiken in Azure toomanage en oplossen van de load balancer in [analytics aanmelden voor Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="c3cd0-134">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
