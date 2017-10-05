---
title: Vinden van de volgende Hop met Azure-netwerk-Watcher volgende Hop - REST | Microsoft Docs
description: In dit artikel wordt beschreven hoe u kunt vinden wat het volgende hoptype is en IP-adres met de volgende Hop met de REST-API van Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 644713d365191bf5e51517d0cc565efbc2abc144
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="31f88-103">Uitzoeken wat het volgende hoptype gebruikt de mogelijkheid van de volgende Hop in Azure met Azure REST API netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="31f88-103">Find out what the next hop type is using the Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="31f88-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="31f88-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="31f88-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31f88-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="31f88-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="31f88-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="31f88-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="31f88-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="31f88-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="31f88-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="31f88-109">De volgende hop is een functie van netwerk-Watcher die de mogelijkheid get biedt de volgende hoptype en IP-adres op basis van een opgegeven virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="31f88-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="31f88-110">Deze functie is handig bij het bepalen of een virtuele machine uitgaand verkeer van een gateway, internet of virtuele netwerken om te gaan naar de bestemming passeert.</span><span class="sxs-lookup"><span data-stu-id="31f88-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="31f88-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="31f88-111">Before you begin</span></span>

<span data-ttu-id="31f88-112">ARMclient wordt gebruikt voor het aanroepen van de REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31f88-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="31f88-113">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="31f88-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="31f88-114">Dit scenario wordt ervan uitgegaan dat u de stappen in al hebt gevolgd [maken van een netwerk-Watcher](network-watcher-create.md) voor het maken van een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="31f88-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="31f88-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="31f88-115">Scenario</span></span>

<span data-ttu-id="31f88-116">Het scenario beschreven in dit artikel maakt gebruik van volgende Hop, een functie van netwerk-Watcher waarmee wordt gezocht naar de volgende hoptype en IP-adres voor een resource.</span><span class="sxs-lookup"><span data-stu-id="31f88-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="31f88-117">Voor meer informatie over de volgende Hop, gaat u naar [volgende Hop overzicht](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="31f88-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="31f88-118">U wordt in dit scenario:</span><span class="sxs-lookup"><span data-stu-id="31f88-118">In this scenario, you will:</span></span>

* <span data-ttu-id="31f88-119">De volgende hop voor een virtuele machine worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="31f88-119">Retrieve the next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="31f88-120">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="31f88-120">Log in with ARMClient</span></span>

<span data-ttu-id="31f88-121">Aanmelden bij armclient met uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="31f88-121">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="31f88-122">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="31f88-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="31f88-123">Voer het volgende script om te retourneren van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="31f88-123">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="31f88-124">Deze informatie is nodig voor het uitvoeren van volgende hop.</span><span class="sxs-lookup"><span data-stu-id="31f88-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="31f88-125">De volgende code moet waarden voor de volgende variabelen:</span><span class="sxs-lookup"><span data-stu-id="31f88-125">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="31f88-126">**subscriptionId** -de abonnements-Id te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="31f88-126">**subscriptionId** - The subscription Id to use.</span></span>
- <span data-ttu-id="31f88-127">**resourceGroupName** -de naam van een resourcegroep die virtuele machines bevatten.</span><span class="sxs-lookup"><span data-stu-id="31f88-127">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="31f88-128">De id van de virtuele machine wordt gebruikt van de volgende uitvoer in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="31f88-128">From the following output, the id of the virtual machine is used in the following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a><span data-ttu-id="31f88-129">Ophalen van de volgende Hop</span><span class="sxs-lookup"><span data-stu-id="31f88-129">Get Next Hop</span></span>

<span data-ttu-id="31f88-130">Zodra de autorisatie-header is gemaakt, kan de volgende hop van een virtuele machine worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="31f88-130">Once the authorization header is created, the next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="31f88-131">De volgende waarden moeten worden vervangen voor het voorbeeld om te werken.</span><span class="sxs-lookup"><span data-stu-id="31f88-131">The following values must be replaced for the code example to work.</span></span>

> [!Important]
> <span data-ttu-id="31f88-132">Voor netwerk-Watcher REST API-aanroepen dat de naam van de resourcegroep in de aanvraag-URI is de resourcegroep met de netwerk-Watcher, niet de resources u diagnostische acties op uitvoert.</span><span class="sxs-lookup"><span data-stu-id="31f88-132">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> <span data-ttu-id="31f88-133">Volgende hop is vereist dat de VM-resource wordt toegewezen om te worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="31f88-133">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="results"></a><span data-ttu-id="31f88-134">Resultaten</span><span class="sxs-lookup"><span data-stu-id="31f88-134">Results</span></span>

<span data-ttu-id="31f88-135">Het volgende codefragment is een voorbeeld van de uitvoer ontvangen.</span><span class="sxs-lookup"><span data-stu-id="31f88-135">The following snippet is an example of the output received.</span></span> <span data-ttu-id="31f88-136">De resultaten bevatten de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="31f88-136">The results contain the following values:</span></span>

* <span data-ttu-id="31f88-137">**nextHopType** -deze waarde is een van de volgende waarden: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway of None.</span><span class="sxs-lookup"><span data-stu-id="31f88-137">**nextHopType** - This value is one of the following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="31f88-138">**nextHopIpAddress** -het IP-adres van de volgende hop.</span><span class="sxs-lookup"><span data-stu-id="31f88-138">**nextHopIpAddress** - The IP address of the next hop.</span></span>
* <span data-ttu-id="31f88-139">**routeTableId** : de waarde van een uri voor de routetabel die zijn gekoppeld aan de route is of als geen gebruiker gedefinieerde route is gedefinieerd de waarde van *Systeemroute* wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="31f88-139">**routeTableId** - The value is either a uri for the route table associated with the route, or if no user-defined route is defined the value of *System Route* is returned.</span></span>

<span data-ttu-id="31f88-140">Hieronder vindt u de resultaten in json-indeling.</span><span class="sxs-lookup"><span data-stu-id="31f88-140">The following are the results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="31f88-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="31f88-141">Next steps</span></span>

<span data-ttu-id="31f88-142">Als u gelukt om erachter te komen de volgende hop voor een virtuele machine, kunt u de beveiliging van uw netwerkbronnen bekijken in via [overzicht van de beveiliging](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="31f88-142">Once you have been able to find out the next hop for a virtual machine, you can view the security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














