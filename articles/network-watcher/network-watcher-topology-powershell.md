---
title: aaaView Azure-netwerk-Watcher-topologie - PowerShell | Microsoft Docs
description: In dit artikel wordt beschreven hoe toouse PowerShell tooquery topologie van uw netwerk.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="18af5-103">Netwerk-Watcher-topologie met PowerShell weergeven</span><span class="sxs-lookup"><span data-stu-id="18af5-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="18af5-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="18af5-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="18af5-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="18af5-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="18af5-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="18af5-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="18af5-107">REST API</span><span class="sxs-lookup"><span data-stu-id="18af5-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="18af5-108">Hallo-topologie-functie van netwerk-Watcher biedt een visuele representatie van Hallo netwerkbronnen in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="18af5-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="18af5-109">In de portal Hallo is deze visualisatie opgenomen tooyou automatisch.</span><span class="sxs-lookup"><span data-stu-id="18af5-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="18af5-110">Hallo gegevens achter Hallo Topologieweergave in de portal Hallo kan worden opgehaald via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="18af5-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="18af5-111">Hierdoor kunt u meer mogelijkheden zoals Hallo gegevens kunnen worden gebruikt door andere hulpprogramma's voor toobuild uit Hallo visualisatie Hallo topologische informatie.</span><span class="sxs-lookup"><span data-stu-id="18af5-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="18af5-112">Hallo-koppeling is gemodelleerd onder twee-relaties.</span><span class="sxs-lookup"><span data-stu-id="18af5-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="18af5-113">**Containment** -voorbeeld: VNet bevat een Subnet bevat een NIC</span><span class="sxs-lookup"><span data-stu-id="18af5-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="18af5-114">**Gekoppeld** -voorbeeld: NIC is gekoppeld aan een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="18af5-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="18af5-115">Hallo bevat volgende lijst eigenschappen die worden geretourneerd bij het opvragen van Hallo topologie REST-API.</span><span class="sxs-lookup"><span data-stu-id="18af5-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="18af5-116">**naam** - hello naam van het Hallo-resource</span><span class="sxs-lookup"><span data-stu-id="18af5-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="18af5-117">**id** -uri van de resource Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="18af5-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="18af5-118">**locatie** -Hallo locatie waar Hallo resource is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="18af5-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="18af5-119">**koppelingen** -een lijst met koppelingen toohello verwijst naar object.</span><span class="sxs-lookup"><span data-stu-id="18af5-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="18af5-120">**naam** -naam Hallo Hallo waarnaar wordt verwezen resource.</span><span class="sxs-lookup"><span data-stu-id="18af5-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="18af5-121">**resourceId** -Hallo resourceId Hallo-uri van Hallo resource waarnaar wordt verwezen in Hallo-koppeling is.</span><span class="sxs-lookup"><span data-stu-id="18af5-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="18af5-122">**associationType** -Hallo relatie tussen Hallo onderliggend object en de bovenliggende Hallo wordt verwezen naar deze waarde.</span><span class="sxs-lookup"><span data-stu-id="18af5-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="18af5-123">Geldige waarden zijn **bevat** of **gekoppelde**.</span><span class="sxs-lookup"><span data-stu-id="18af5-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="18af5-124">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="18af5-124">Before you begin</span></span>

<span data-ttu-id="18af5-125">In dit scenario gebruikt u Hallo `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve Hallo topologische informatie.</span><span class="sxs-lookup"><span data-stu-id="18af5-125">In this scenario, you use hello `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="18af5-126">Er is ook een artikel over het te[ophalen netwerktopologie met REST-API](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="18af5-126">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="18af5-127">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="18af5-127">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="18af5-128">Scenario</span><span class="sxs-lookup"><span data-stu-id="18af5-128">Scenario</span></span>

<span data-ttu-id="18af5-129">Hallo scenario beschreven in dit artikel wordt antwoord van de Hallo-topologie voor een opgegeven resourcegroep opgehaald.</span><span class="sxs-lookup"><span data-stu-id="18af5-129">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="18af5-130">Ophalen van netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="18af5-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="18af5-131">de eerste stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="18af5-131">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="18af5-132">Hallo `$networkWatcher` variabele is doorgegeven toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="18af5-132">hello `$networkWatcher` variable is passed toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="18af5-133">Topologie ophalen</span><span class="sxs-lookup"><span data-stu-id="18af5-133">Retrieve topology</span></span>

<span data-ttu-id="18af5-134">Hallo `Get-AzureRmNetworkWatcherTopology` cmdlet haalt Hallo-topologie voor een opgegeven resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="18af5-134">hello `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves hello topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="18af5-135">Resultaten</span><span class="sxs-lookup"><span data-stu-id="18af5-135">Results</span></span>

<span data-ttu-id="18af5-136">Hallo resultaten hebben een eigenschap name 'Resources', waarin Hallo json antwoordtekst voor Hallo `Get-AzureRmNetworkWatcherTopology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="18af5-136">hello results returned have a property name "Resources", which contains hello json response body for hello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="18af5-137">Hallo-antwoord bevat Hallo bronnen Hallo Netwerkbeveiligingsgroep en de bijbehorende koppelingen (dat wil zeggen, bevat, gekoppelde).</span><span class="sxs-lookup"><span data-stu-id="18af5-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a><span data-ttu-id="18af5-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="18af5-138">Next steps</span></span>

<span data-ttu-id="18af5-139">Meer informatie over hoe toovisualize uw NSG-flow registreert met Power BI in via [visualiseren NSG loopt logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="18af5-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


