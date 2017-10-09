---
title: aaaAzure voorbeeldscript CLI - taakverdeling toe te passen meerdere websites Hello Azure CLI | Microsoft Docs
description: Azure CLI-voorbeeldscript - taakverdeling toe te passen meerdere websites toohello dezelfde virtuele machine
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="65e44-103">Taakverdeling maken voor meerdere websites</span><span class="sxs-lookup"><span data-stu-id="65e44-103">Load balance multiple websites</span></span>

<span data-ttu-id="65e44-104">Dit voorbeeldscript wordt een virtueel netwerk maakt met twee virtuele machines (VM) die lid van een beschikbaarheidsset zijn.</span><span class="sxs-lookup"><span data-stu-id="65e44-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="65e44-105">Een load balancer stuurt verkeer voor twee afzonderlijke IP-adressen toohello twee virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="65e44-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="65e44-106">Na het Hallo-script wordt uitgevoerd, kan u web server software toohello virtuele machines implementeren en hosten van meerdere websites, elk met een eigen IP-adres.</span><span class="sxs-lookup"><span data-stu-id="65e44-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="65e44-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="65e44-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="65e44-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="65e44-108">Clean up deployment</span></span> 

<span data-ttu-id="65e44-109">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="65e44-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="65e44-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="65e44-110">Script explanation</span></span>

<span data-ttu-id="65e44-111">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep of virtueel netwerk, load balancer en alle gerelateerde resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="65e44-111">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="65e44-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="65e44-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="65e44-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="65e44-113">Command</span></span> | <span data-ttu-id="65e44-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="65e44-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="65e44-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="65e44-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="65e44-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="65e44-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="65e44-117">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="65e44-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="65e44-118">Maakt een virtueel Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="65e44-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="65e44-119">AZ netwerk openbare ip-maken</span><span class="sxs-lookup"><span data-stu-id="65e44-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="65e44-120">Hiermee maakt een openbaar IP-adres met een statisch IP-adres en een bijbehorende DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="65e44-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="65e44-121">AZ network Load Balancer maken</span><span class="sxs-lookup"><span data-stu-id="65e44-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="65e44-122">Hiermee maakt u een Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="65e44-122">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="65e44-123">AZ network Load Balancer-test maken</span><span class="sxs-lookup"><span data-stu-id="65e44-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="65e44-124">Hiermee maakt u een load balancer-test.</span><span class="sxs-lookup"><span data-stu-id="65e44-124">Creates a load balancer probe.</span></span> <span data-ttu-id="65e44-125">Een load balancer-test gebruikte toomonitor elke virtuele machine in Hallo load balancer-set is.</span><span class="sxs-lookup"><span data-stu-id="65e44-125">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="65e44-126">Als een virtuele machine niet meer toegankelijk is, wordt verkeer is geen gerouteerde toohello VM.</span><span class="sxs-lookup"><span data-stu-id="65e44-126">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="65e44-127">AZ network Load Balancer-regel maken</span><span class="sxs-lookup"><span data-stu-id="65e44-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="65e44-128">Maakt een regel voor load balancer.</span><span class="sxs-lookup"><span data-stu-id="65e44-128">Creates a load balancer rule.</span></span> <span data-ttu-id="65e44-129">In dit voorbeeld wordt een regel gemaakt voor poort 80.</span><span class="sxs-lookup"><span data-stu-id="65e44-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="65e44-130">HTTP-verkeer ontvangt bij Hallo load balancer is gerouteerde tooport 80 een Hallo VM's in Hallo load balancer-set.</span><span class="sxs-lookup"><span data-stu-id="65e44-130">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello load balancer set.</span></span> |
| [<span data-ttu-id="65e44-131">AZ netwerk lb frontend-IP-maken</span><span class="sxs-lookup"><span data-stu-id="65e44-131">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="65e44-132">Maak een frontend-IP-adres voor Hallo Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="65e44-132">Create a frontend IP address for hello Load Balancer.</span></span> |
| [<span data-ttu-id="65e44-133">AZ netwerk lb-adresgroep maken</span><span class="sxs-lookup"><span data-stu-id="65e44-133">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="65e44-134">Maakt een back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="65e44-134">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="65e44-135">AZ netwerk nic maken</span><span class="sxs-lookup"><span data-stu-id="65e44-135">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="65e44-136">Maakt een virtueel netwerkkaart en toohello virtueel netwerk en subnet gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="65e44-136">Creates a virtual network card and attaches it toohello virtual network, and subnet.</span></span> |
| [<span data-ttu-id="65e44-137">AZ vm beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="65e44-137">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="65e44-138">Hiermee maakt een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="65e44-138">Creates an availability set.</span></span> <span data-ttu-id="65e44-139">Beschikbaarheidssets waarborgen uptime van toepassingen via Hallo virtuele machines verspreid over fysieke resources zo dat als fout optreedt, wordt de hele set Hallo niet gedaan.</span><span class="sxs-lookup"><span data-stu-id="65e44-139">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="65e44-140">AZ netwerk nic ip-configuratie maken</span><span class="sxs-lookup"><span data-stu-id="65e44-140">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="65e44-141">Hiermee maakt u een IP-confiuration.</span><span class="sxs-lookup"><span data-stu-id="65e44-141">Creates an IP confiuration.</span></span> <span data-ttu-id="65e44-142">U moet Hallo Microsoft.Network/AllowMultipleIpConfigurationsPerNic functie is ingeschakeld voor uw abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="65e44-142">You must have hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="65e44-143">Hallo primaire IP-configuratie per NIC, met behulp van Hallo--primair maken vlag kan slechts één configuratie worden aangeduid.</span><span class="sxs-lookup"><span data-stu-id="65e44-143">Only one configuration may be designated as hello primary IP configuration per NIC, using hello --make-primary flag.</span></span> |
| [<span data-ttu-id="65e44-144">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="65e44-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="65e44-145">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="65e44-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="65e44-146">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="65e44-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="65e44-147">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="65e44-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="65e44-148">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="65e44-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="65e44-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65e44-149">Next steps</span></span>

<span data-ttu-id="65e44-150">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65e44-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="65e44-151">Aanvullende netwerken CLI scriptvoorbeelden kunnen u vinden in Hallo [overzicht van Azure-netwerken documentatie](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65e44-151">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
