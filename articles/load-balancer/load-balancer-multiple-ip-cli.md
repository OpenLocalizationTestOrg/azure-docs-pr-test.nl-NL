---
title: De Load Balancer op meerdere IP-configuraties met Azure CLI | Microsoft Docs
description: Meer informatie over meerdere IP-adressen toewijzen aan een virtuele machine met Azure CLI | Resource Manager.
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
ms.openlocfilehash: bd15713752ea01ad403d8e3dcfed0c9a7adcc7fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="b00ea-103">De Load Balancer op meerdere IP-configuraties</span><span class="sxs-lookup"><span data-stu-id="b00ea-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b00ea-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b00ea-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="b00ea-105">CLI</span><span class="sxs-lookup"><span data-stu-id="b00ea-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="b00ea-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b00ea-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="b00ea-107">Dit artikel wordt beschreven hoe u Azure Load Balancer met meerdere IP-adressen op een secundaire netwerkinterface (NIC).</span><span class="sxs-lookup"><span data-stu-id="b00ea-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="b00ea-108">In dit scenario hebben we twee virtuele machines met Windows, elk met een primaire en een secundaire NIC.</span><span class="sxs-lookup"><span data-stu-id="b00ea-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="b00ea-109">Elk van de secundaire NIC's twee IP-configuraties hebben.</span><span class="sxs-lookup"><span data-stu-id="b00ea-109">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="b00ea-110">Elke virtuele machine fungeert als host van websites contoso.com en fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="b00ea-110">Each VM hosts both websites contoso.com and fabrikam.com.</span></span> <span data-ttu-id="b00ea-111">Elke website is gebonden aan een van de IP-configuraties voor de secundaire NIC.</span><span class="sxs-lookup"><span data-stu-id="b00ea-111">Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="b00ea-112">We Azure Load Balancer gebruiken om twee IP-adressen voor frontend, één voor elke website, voor het distribueren van het verkeer naar de respectieve IP-configuratie voor de website weer te geven.</span><span class="sxs-lookup"><span data-stu-id="b00ea-112">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="b00ea-113">Dit scenario gebruikt hetzelfde poortnummer op zowel frontends, evenals het IP-adressen van zowel back-end-groep.</span><span class="sxs-lookup"><span data-stu-id="b00ea-113">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![De installatiekopie van de Load Balancer-scenario](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="b00ea-115">Stappen om taken te verdelen over meerdere IP-configuraties</span><span class="sxs-lookup"><span data-stu-id="b00ea-115">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="b00ea-116">Volg onderstaande stappen voor het bereiken van het scenario in dit artikel wordt beschreven:</span><span class="sxs-lookup"><span data-stu-id="b00ea-116">Follow the steps below to achieve the scenario outlined in this article:</span></span>

1. <span data-ttu-id="b00ea-117">[Installeren en configureren van de Azure CLI](../cli-install-nodejs.md) de Azure CLI volgens de stappen in het gekoppelde artikel en het logboek in uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="b00ea-117">[Install and Configure the Azure CLI](../cli-install-nodejs.md) the Azure CLI by following the steps in the linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="b00ea-118">[Een resourcegroep maken](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) aangeroepen *contosofabrikam* zoals hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="b00ea-118">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="b00ea-119">[Maken van een beschikbaarheidsset](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) aan voor de twee virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b00ea-119">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) to for the two VMs.</span></span> <span data-ttu-id="b00ea-120">In dit scenario moet u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b00ea-120">For this scenario, use the following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="b00ea-121">[Een virtueel netwerk maken](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) aangeroepen *myVNet* en een subnet met de naam *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="b00ea-121">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="b00ea-122">[Maken van de load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) aangeroepen *mylb*:</span><span class="sxs-lookup"><span data-stu-id="b00ea-122">[Create the load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="b00ea-123">Maak twee dynamische openbare IP-adressen voor de frontend-IP-configuraties van de load balancer:</span><span class="sxs-lookup"><span data-stu-id="b00ea-123">Create two dynamic public IP addresses for the frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="b00ea-124">Maken van de twee frontend-IP-configuraties *contosofe* en *fabrikamfe* respectievelijk:</span><span class="sxs-lookup"><span data-stu-id="b00ea-124">Create the two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="b00ea-125">Maken van uw back-end-adresgroepen - *contosopool* en *fabrikampool*, een [test](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, en de belasting balancingregels - *HTTPc* en *HTTPf*:</span><span class="sxs-lookup"><span data-stu-id="b00ea-125">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="b00ea-126">Voer de volgende opdracht hieronder en controleer vervolgens de uitvoer naar [Controleer of de load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) correct is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="b00ea-126">Run the following command below and then check the output to [verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="b00ea-127">[Maken van een openbaar IP-adres](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, en [opslagaccount](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* voor uw eerste virtuele machine VM1 zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="b00ea-127">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="b00ea-128">[Maken van de netwerkinterfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) voor VM1 en voeg een tweede IP-configuratie, *VM1 ipconfig2*, en [de virtuele machine maken](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="b00ea-128">[Create the network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create the VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="b00ea-129">Herhaal stap 10 11 voor uw tweede VM:</span><span class="sxs-lookup"><span data-stu-id="b00ea-129">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="b00ea-130">Tot slot moet u DNS-bronrecords om te verwijzen naar de respectieve frontend-IP-adres van de Load Balancer configureren.</span><span class="sxs-lookup"><span data-stu-id="b00ea-130">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span></span> <span data-ttu-id="b00ea-131">U kunt uw domeinen in Azure DNS hosten.</span><span class="sxs-lookup"><span data-stu-id="b00ea-131">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="b00ea-132">Zie voor meer informatie over het gebruik van Azure DNS met Load Balancer [met behulp van Azure DNS met andere Azure-services](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="b00ea-132">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b00ea-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b00ea-133">Next steps</span></span>
- <span data-ttu-id="b00ea-134">Meer informatie over het combineren van de load balancer-services in Azure in [met gelijke taakverdeling van services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="b00ea-134">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="b00ea-135">Meer informatie over hoe u verschillende typen logboeken kunt gebruiken in Azure te beheren en oplossen van de load balancer in [analytics aanmelden voor Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="b00ea-135">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
