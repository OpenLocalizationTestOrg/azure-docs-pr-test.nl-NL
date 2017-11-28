---
title: Volgende Hop met Azure-netwerk-Watcher volgende Hop - REST aaaFind | Microsoft Docs
description: In dit artikel wordt beschreven hoe u kunt zoeken welke Hallo type voor het volgende hop is en het IP-adres met behulp van volgende Hop hello Azure REST-API
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
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="91201-103">Ontdek welke Hallo volgend hoptype Hallo volgende Hop mogelijkheid gebruikt in Azure met Azure REST API netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="91201-103">Find out what hello next hop type is using hello Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="91201-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="91201-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="91201-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="91201-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="91201-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="91201-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="91201-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="91201-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="91201-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="91201-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="91201-109">De volgende hop is een functie van netwerk-Watcher die de mogelijkheid Hallo biedt Hallo volgend hoptype en IP-adres op basis van een opgegeven virtuele machine ophalen.</span><span class="sxs-lookup"><span data-stu-id="91201-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="91201-110">Deze functie is handig bij het bepalen of een virtuele machine uitgaand verkeer van een gateway, internet of virtuele netwerken tooget tooits bestemming passeert.</span><span class="sxs-lookup"><span data-stu-id="91201-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="91201-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="91201-111">Before you begin</span></span>

<span data-ttu-id="91201-112">ARMclient is gebruikte toocall Hallo REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91201-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="91201-113">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="91201-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="91201-114">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="91201-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="91201-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="91201-115">Scenario</span></span>

<span data-ttu-id="91201-116">Hallo scenario beschreven in dit artikel maakt gebruik van volgende Hop, een functie van netwerk-Watcher waarmee wordt gezocht naar het volgende hoptype hello en IP-adres voor een resource.</span><span class="sxs-lookup"><span data-stu-id="91201-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="91201-117">toolearn meer informatie over het volgende Hop, gaat u naar [volgende Hop overzicht](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91201-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="91201-118">U wordt in dit scenario:</span><span class="sxs-lookup"><span data-stu-id="91201-118">In this scenario, you will:</span></span>

* <span data-ttu-id="91201-119">De volgende hop Hallo voor een virtuele machine worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="91201-119">Retrieve hello next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="91201-120">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="91201-120">Log in with ARMClient</span></span>

<span data-ttu-id="91201-121">Meld u bij tooarmclient met uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="91201-121">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="91201-122">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="91201-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="91201-123">Hallo script tooreturn na een virtuele machine uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="91201-123">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="91201-124">Deze informatie is nodig voor het uitvoeren van volgende hop.</span><span class="sxs-lookup"><span data-stu-id="91201-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="91201-125">Hallo na code moet waarden voor Hallo variabelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="91201-125">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="91201-126">**subscriptionId** -Hallo toouse voor abonnement-Id.</span><span class="sxs-lookup"><span data-stu-id="91201-126">**subscriptionId** - hello subscription Id toouse.</span></span>
- <span data-ttu-id="91201-127">**resourceGroupName** - hello naam van een resourcegroep die virtuele machines bevatten.</span><span class="sxs-lookup"><span data-stu-id="91201-127">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="91201-128">Hallo-id van Hallo virtuele machine wordt van de volgende Hallo uitvoer, gebruikt in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="91201-128">From hello following output, hello id of hello virtual machine is used in hello following example:</span></span>

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

## <a name="get-next-hop"></a><span data-ttu-id="91201-129">Ophalen van de volgende Hop</span><span class="sxs-lookup"><span data-stu-id="91201-129">Get Next Hop</span></span>

<span data-ttu-id="91201-130">Zodra Hallo autorisatie-header is gemaakt, kan de volgende hop Hallo van een virtuele machine worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="91201-130">Once hello authorization header is created, hello next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="91201-131">Hallo moeten volgende waarden worden vervangen voor Hallo code voorbeeld toowork.</span><span class="sxs-lookup"><span data-stu-id="91201-131">hello following values must be replaced for hello code example toowork.</span></span>

> [!Important]
> <span data-ttu-id="91201-132">Voor de REST-API voor netwerk-Watcher Hallo aanroepen Resourcegroepnaam in Hallo aanvraag-URI is Hallo-resourcegroep met Hallo netwerk-Watcher niet Hallo-bronnen zoals u Hallo diagnostische acties uitvoert op.</span><span class="sxs-lookup"><span data-stu-id="91201-132">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

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
> <span data-ttu-id="91201-133">Volgende hop is vereist dat de VM-resource Hallo toorun wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="91201-133">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="results"></a><span data-ttu-id="91201-134">Resultaten</span><span class="sxs-lookup"><span data-stu-id="91201-134">Results</span></span>

<span data-ttu-id="91201-135">Hallo bevat volgende fragment een voorbeeld van uitvoer van Hallo ontvangen.</span><span class="sxs-lookup"><span data-stu-id="91201-135">hello following snippet is an example of hello output received.</span></span> <span data-ttu-id="91201-136">Hallo resultaten bevatten Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="91201-136">hello results contain hello following values:</span></span>

* <span data-ttu-id="91201-137">**nextHopType** -deze waarde is een van de volgende waarden Hallo: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway of None.</span><span class="sxs-lookup"><span data-stu-id="91201-137">**nextHopType** - This value is one of hello following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="91201-138">**nextHopIpAddress** -IP-adres van de volgende hop Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="91201-138">**nextHopIpAddress** - hello IP address of hello next hop.</span></span>
* <span data-ttu-id="91201-139">**routeTableId** - Hallo-waarde is ofwel een uri voor de routetabel Hallo Hallo route gekoppeld of als geen gebruiker gedefinieerde route is gedefinieerd Hallo-waarde van *Systeemroute* wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="91201-139">**routeTableId** - hello value is either a uri for hello route table associated with hello route, or if no user-defined route is defined hello value of *System Route* is returned.</span></span>

<span data-ttu-id="91201-140">Hallo volgen Hallo resulteert in een json-indeling.</span><span class="sxs-lookup"><span data-stu-id="91201-140">hello following are hello results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="91201-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="91201-141">Next steps</span></span>

<span data-ttu-id="91201-142">Als u kunnen toofind uit de volgende hop Hallo voor een virtuele machine zijn, kunt u Hallo beveiliging van uw netwerkresources bekijken in via [overzicht van de beveiliging](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="91201-142">Once you have been able toofind out hello next hop for a virtual machine, you can view hello security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














