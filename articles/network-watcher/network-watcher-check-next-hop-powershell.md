---
title: de volgende hop aaaFind met Azure-netwerk-Watcher volgende Hop - PowerShell | Microsoft Docs
description: In dit artikel wordt beschreven hoe u kunt zoeken welke Hallo type voor het volgende hop is en gebruik van IP-adres van volgende Hop met behulp van PowerShell.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="d8bf2-103">Ontdek welke Hallo volgend hoptype Hallo volgende Hop mogelijkheid gebruikt in Azure met behulp van PowerShell netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="d8bf2-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d8bf2-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d8bf2-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="d8bf2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8bf2-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="d8bf2-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d8bf2-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="d8bf2-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d8bf2-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="d8bf2-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="d8bf2-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="d8bf2-109">De volgende hop is een functie van netwerk-Watcher die de mogelijkheid Hallo biedt Hallo volgend hoptype en IP-adres op basis van een opgegeven virtuele machine ophalen.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="d8bf2-110">Deze functie is handig bij het bepalen of een virtuele machine uitgaand verkeer van een gateway, internet of virtuele netwerken tooget tooits bestemming passeert.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d8bf2-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="d8bf2-111">Before you begin</span></span>

<span data-ttu-id="d8bf2-112">In dit scenario gebruikt u Azure portal toofind Hallo volgend hoptype hello en IP-adres.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-112">In this scenario, you will use hello Azure portal toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="d8bf2-113">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="d8bf2-114">Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="d8bf2-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="d8bf2-115">Scenario</span></span>

<span data-ttu-id="d8bf2-116">Hallo scenario beschreven in dit artikel maakt gebruik van volgende Hop, een functie van netwerk-Watcher waarmee wordt gezocht naar het volgende hoptype hello en IP-adres voor een resource.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="d8bf2-117">toolearn meer informatie over het volgende Hop, gaat u naar [volgende Hop overzicht](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8bf2-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="d8bf2-118">Ophalen van netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="d8bf2-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="d8bf2-119">de eerste stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-119">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="d8bf2-120">Hallo `$networkWatcher` variabele is doorgegeven toohello volgende hop cmdlet controleren.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-120">hello `$networkWatcher` variable is passed toohello next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="d8bf2-121">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="d8bf2-121">Get a virtual machine</span></span>

<span data-ttu-id="d8bf2-122">Volgende hop retourneert de volgende hop Hallo en Hallo IP-adres van de volgende hop Hallo van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-122">Next hop returns hello next hop and hello IP address of hello next hop from a virtual machine.</span></span> <span data-ttu-id="d8bf2-123">Een Id van een virtuele machine is vereist voor het Hallo-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="d8bf2-124">Als u al Hallo-ID van virtuele machine-toouse hello weet, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="d8bf2-125">Volgende hop is vereist dat de VM-resource Hallo toorun wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-125">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="get-hello-network-interfaces"></a><span data-ttu-id="d8bf2-126">Hallo-netwerkinterfaces ophalen</span><span class="sxs-lookup"><span data-stu-id="d8bf2-126">Get hello network interfaces</span></span>

<span data-ttu-id="d8bf2-127">Hallo IP-adres van een NIC op Hallo virtuele machine is vereist, in dit voorbeeld Hallo NIC's op een virtuele machine worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="d8bf2-128">Als u weet al Hallo IP adres die u wilt dat tootest op Hallo virtuele machine, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="d8bf2-129">Ophalen van de volgende Hop</span><span class="sxs-lookup"><span data-stu-id="d8bf2-129">Get Next Hop</span></span>

<span data-ttu-id="d8bf2-130">Nu we Hallo noemen `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-130">Now we call hello `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="d8bf2-131">Wij Hallo cmdlet Hallo netwerk-Watcher virtuele machine Id doorgeven, bron-IP-adres en IP-doeladres.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-131">We pass hello cmdlet hello Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="d8bf2-132">In dit voorbeeld is de IP-doeladres Hallo tooa VM in een ander virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-132">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="d8bf2-133">Er is een virtuele netwerkgateway tussen Hallo twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-133">There is a virtual network gateway between hello two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="d8bf2-134">Resultaten bekijken</span><span class="sxs-lookup"><span data-stu-id="d8bf2-134">Review results</span></span>

<span data-ttu-id="d8bf2-135">Als u klaar worden Hallo resultaten geleverd.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-135">When complete, hello results are provided.</span></span> <span data-ttu-id="d8bf2-136">Hallo volgende hop IP-adres wordt geretourneerd en Hallo type resource is.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-136">hello next hop IP address is returned as well as hello type of resource it is.</span></span> <span data-ttu-id="d8bf2-137">In dit scenario is het openbare IP-adres van de virtuele netwerkgateway Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d8bf2-137">In this scenario, it is hello public IP address of hello virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="d8bf2-138">Hallo bevat volgende lijst de momenteel beschikbare NextHopType waarden Hallo:</span><span class="sxs-lookup"><span data-stu-id="d8bf2-138">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="d8bf2-139">**Volgend Hoptype**</span><span class="sxs-lookup"><span data-stu-id="d8bf2-139">**Next Hop Type**</span></span>

* <span data-ttu-id="d8bf2-140">Internet</span><span class="sxs-lookup"><span data-stu-id="d8bf2-140">Internet</span></span>
* <span data-ttu-id="d8bf2-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="d8bf2-141">VirtualAppliance</span></span>
* <span data-ttu-id="d8bf2-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="d8bf2-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="d8bf2-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="d8bf2-143">VnetLocal</span></span>
* <span data-ttu-id="d8bf2-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="d8bf2-144">HyperNetGateway</span></span>
* <span data-ttu-id="d8bf2-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="d8bf2-145">VnetPeering</span></span>
* <span data-ttu-id="d8bf2-146">Geen</span><span class="sxs-lookup"><span data-stu-id="d8bf2-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8bf2-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d8bf2-147">Next steps</span></span>

<span data-ttu-id="d8bf2-148">Meer informatie over hoe tooreview uw netwerk groep beveiligingsinstellingen programmatisch in via [NSG controleren met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="d8bf2-148">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















