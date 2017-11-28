---
title: Azure CLI-voorbeeldscript - taakverdeling toe te passen meerdere websites met de Azure CLI | Microsoft Docs
description: Azure CLI-voorbeeldscript - taakverdeling toe te passen meerdere websites op de virtuele machine
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
ms.openlocfilehash: c5a584b33025122033b930822ae0a0864a7ec1cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="e33e9-103">Taakverdeling maken voor meerdere websites</span><span class="sxs-lookup"><span data-stu-id="e33e9-103">Load balance multiple websites</span></span>

<span data-ttu-id="e33e9-104">Dit voorbeeldscript wordt een virtueel netwerk maakt met twee virtuele machines (VM) die lid van een beschikbaarheidsset zijn.</span><span class="sxs-lookup"><span data-stu-id="e33e9-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="e33e9-105">Een load balancer wordt doorgestuurd verkeer voor twee afzonderlijke IP-adressen naar de twee virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e33e9-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span></span> <span data-ttu-id="e33e9-106">Nadat het script is uitgevoerd, kan u implementeren web server-software aan de virtuele machines en de host meerdere websites, elk met een eigen IP-adres.</span><span class="sxs-lookup"><span data-stu-id="e33e9-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e33e9-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="e33e9-107">Sample script</span></span>


<span data-ttu-id="e33e9-108">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "taakverdelingen voor meerdere sites")]</span><span class="sxs-lookup"><span data-stu-id="e33e9-108">[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e33e9-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="e33e9-109">Clean up deployment</span></span> 

<span data-ttu-id="e33e9-110">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e33e9-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e33e9-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="e33e9-111">Script explanation</span></span>

<span data-ttu-id="e33e9-112">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, virtueel netwerk, load balancer en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="e33e9-112">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="e33e9-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="e33e9-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e33e9-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="e33e9-114">Command</span></span> | <span data-ttu-id="e33e9-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e33e9-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e33e9-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="e33e9-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e33e9-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e33e9-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e33e9-118">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="e33e9-118">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="e33e9-119">Maakt een virtueel Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="e33e9-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="e33e9-120">AZ netwerk openbare ip-maken</span><span class="sxs-lookup"><span data-stu-id="e33e9-120">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="e33e9-121">Hiermee maakt een openbaar IP-adres met een statisch IP-adres en een bijbehorende DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="e33e9-121">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="e33e9-122">AZ network Load Balancer maken</span><span class="sxs-lookup"><span data-stu-id="e33e9-122">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="e33e9-123">Hiermee maakt u een Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e33e9-123">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="e33e9-124">AZ network Load Balancer-test maken</span><span class="sxs-lookup"><span data-stu-id="e33e9-124">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="e33e9-125">Hiermee maakt u een load balancer-test.</span><span class="sxs-lookup"><span data-stu-id="e33e9-125">Creates a load balancer probe.</span></span> <span data-ttu-id="e33e9-126">Een load balancer-test wordt gebruikt voor het bewaken van elke virtuele machine in de load balancer-set.</span><span class="sxs-lookup"><span data-stu-id="e33e9-126">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="e33e9-127">Als een virtuele machine niet meer toegankelijk is, wordt verkeer niet doorgestuurd naar de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e33e9-127">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="e33e9-128">AZ network Load Balancer-regel maken</span><span class="sxs-lookup"><span data-stu-id="e33e9-128">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="e33e9-129">Maakt een regel voor load balancer.</span><span class="sxs-lookup"><span data-stu-id="e33e9-129">Creates a load balancer rule.</span></span> <span data-ttu-id="e33e9-130">In dit voorbeeld wordt een regel gemaakt voor poort 80.</span><span class="sxs-lookup"><span data-stu-id="e33e9-130">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="e33e9-131">HTTP-verkeer ontvangt bij de load balancer wordt doorgestuurd naar poort 80 een van de virtuele machines in de load balancer-set.</span><span class="sxs-lookup"><span data-stu-id="e33e9-131">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the load balancer set.</span></span> |
| [<span data-ttu-id="e33e9-132">AZ netwerk lb frontend-IP-maken</span><span class="sxs-lookup"><span data-stu-id="e33e9-132">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="e33e9-133">Maak een frontend-IP-adres voor de Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e33e9-133">Create a frontend IP address for the Load Balancer.</span></span> |
| [<span data-ttu-id="e33e9-134">AZ netwerk lb-adresgroep maken</span><span class="sxs-lookup"><span data-stu-id="e33e9-134">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="e33e9-135">Maakt een back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="e33e9-135">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="e33e9-136">AZ netwerk nic maken</span><span class="sxs-lookup"><span data-stu-id="e33e9-136">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="e33e9-137">Hiermee maakt u een virtueel netwerkkaart en gekoppeld aan het virtuele netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="e33e9-137">Creates a virtual network card and attaches it to the virtual network, and subnet.</span></span> |
| [<span data-ttu-id="e33e9-138">AZ vm beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="e33e9-138">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="e33e9-139">Hiermee maakt een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="e33e9-139">Creates an availability set.</span></span> <span data-ttu-id="e33e9-140">Beschikbaarheidssets waarborgen uptime van toepassingen via de virtuele machines verspreid over fysieke resources zo dat als fout optreedt, wordt de hele set niet gedaan.</span><span class="sxs-lookup"><span data-stu-id="e33e9-140">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="e33e9-141">AZ netwerk nic ip-configuratie maken</span><span class="sxs-lookup"><span data-stu-id="e33e9-141">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="e33e9-142">Hiermee maakt u een IP-confiuration.</span><span class="sxs-lookup"><span data-stu-id="e33e9-142">Creates an IP confiuration.</span></span> <span data-ttu-id="e33e9-143">U moet de functie Microsoft.Network/AllowMultipleIpConfigurationsPerNic is ingeschakeld voor uw abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="e33e9-143">You must have the Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="e33e9-144">De primaire IP-configuratie per NIC, kan slechts één configuratie worden aangeduid met de--vlag primair maken.</span><span class="sxs-lookup"><span data-stu-id="e33e9-144">Only one configuration may be designated as the primary IP configuration per NIC, using the --make-primary flag.</span></span> |
| [<span data-ttu-id="e33e9-145">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="e33e9-145">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="e33e9-146">De virtuele machine maakt en met de netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="e33e9-146">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="e33e9-147">Deze opdracht geeft ook aan de installatiekopie van de virtuele machine om te worden gebruikt en administratieve referenties.</span><span class="sxs-lookup"><span data-stu-id="e33e9-147">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="e33e9-148">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="e33e9-148">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e33e9-149">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="e33e9-149">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e33e9-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e33e9-150">Next steps</span></span>

<span data-ttu-id="e33e9-151">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e33e9-151">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e33e9-152">Aanvullende netwerken CLI scriptvoorbeelden vindt u in de [overzicht van Azure-netwerken documentatie](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e33e9-152">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
