---
title: aaaView Azure-netwerk-Watcher-topologie - REST-API | Microsoft Docs
description: In dit artikel wordt beschreven hoe toouse REST-API tooquery topologie van uw netwerk.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="af40e-103">Netwerk-Watcher-topologie met REST-API weergeven</span><span class="sxs-lookup"><span data-stu-id="af40e-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="af40e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="af40e-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="af40e-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="af40e-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="af40e-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="af40e-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="af40e-107">REST API</span><span class="sxs-lookup"><span data-stu-id="af40e-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="af40e-108">Hallo-topologie-functie van netwerk-Watcher biedt een visuele representatie van Hallo netwerkbronnen in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="af40e-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="af40e-109">In de portal Hallo is deze visualisatie opgenomen tooyou automatisch.</span><span class="sxs-lookup"><span data-stu-id="af40e-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="af40e-110">Hallo gegevens achter Hallo Topologieweergave in de portal Hallo kan worden opgehaald via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af40e-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="af40e-111">Hierdoor kunt u meer mogelijkheden zoals Hallo gegevens kunnen worden gebruikt door andere hulpprogramma's voor toobuild uit Hallo visualisatie Hallo topologische informatie.</span><span class="sxs-lookup"><span data-stu-id="af40e-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="af40e-112">Hallo-koppeling is gemodelleerd onder twee-relaties.</span><span class="sxs-lookup"><span data-stu-id="af40e-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="af40e-113">**Containment** -voorbeeld: VNet bevat een Subnet bevat een NIC</span><span class="sxs-lookup"><span data-stu-id="af40e-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="af40e-114">**Gekoppeld** -voorbeeld: NIC is gekoppeld aan een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="af40e-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="af40e-115">Hallo bevat volgende lijst eigenschappen die worden geretourneerd bij het opvragen van Hallo topologie REST-API.</span><span class="sxs-lookup"><span data-stu-id="af40e-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="af40e-116">**naam** - hello naam van het Hallo-resource</span><span class="sxs-lookup"><span data-stu-id="af40e-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="af40e-117">**id** -uri van de resource Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="af40e-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="af40e-118">**locatie** -Hallo locatie waar Hallo resource is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="af40e-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="af40e-119">**koppelingen** -een lijst met koppelingen toohello verwijst naar object.</span><span class="sxs-lookup"><span data-stu-id="af40e-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="af40e-120">**naam** -naam Hallo Hallo waarnaar wordt verwezen resource.</span><span class="sxs-lookup"><span data-stu-id="af40e-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="af40e-121">**resourceId** -Hallo resourceId Hallo-uri van Hallo resource waarnaar wordt verwezen in Hallo-koppeling is.</span><span class="sxs-lookup"><span data-stu-id="af40e-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="af40e-122">**associationType** -Hallo relatie tussen Hallo onderliggend object en de bovenliggende Hallo wordt verwezen naar deze waarde.</span><span class="sxs-lookup"><span data-stu-id="af40e-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="af40e-123">Geldige waarden zijn **bevat** of **gekoppelde**.</span><span class="sxs-lookup"><span data-stu-id="af40e-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="af40e-124">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="af40e-124">Before you begin</span></span>

<span data-ttu-id="af40e-125">In dit scenario moet u Hallo topologische informatie ophalen.</span><span class="sxs-lookup"><span data-stu-id="af40e-125">In this scenario, you retrieve hello topology information.</span></span> <span data-ttu-id="af40e-126">ARMclient is gebruikte toocall Hallo REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af40e-126">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="af40e-127">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="af40e-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="af40e-128">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="af40e-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="af40e-129">Scenario</span><span class="sxs-lookup"><span data-stu-id="af40e-129">Scenario</span></span>

<span data-ttu-id="af40e-130">Hallo scenario beschreven in dit artikel wordt antwoord van de Hallo-topologie voor een opgegeven resourcegroep opgehaald.</span><span class="sxs-lookup"><span data-stu-id="af40e-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="af40e-131">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="af40e-131">Log in with ARMClient</span></span>

<span data-ttu-id="af40e-132">Meld u bij tooarmclient met uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="af40e-132">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="af40e-133">Topologie ophalen</span><span class="sxs-lookup"><span data-stu-id="af40e-133">Retrieve topology</span></span>

<span data-ttu-id="af40e-134">Hallo volgende voorbeeldtopologie aanvragen Hallo uit Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="af40e-134">hello following example requests hello topology from hello REST API.</span></span>  <span data-ttu-id="af40e-135">Hallo-voorbeeld is geparameteriseerd tooallow voor flexibiliteit bij het maken van een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="af40e-135">hello example is parameterized tooallow for flexibility in creating an example.</span></span>  <span data-ttu-id="af40e-136">Vervang alle waarden met \< \> omsluiten.</span><span class="sxs-lookup"><span data-stu-id="af40e-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="af40e-137">Hallo na antwoord is een voorbeeld van een kortere reactie die wordt geretourneerd wanneer de topologie voor een resourcegroup ophalen:</span><span class="sxs-lookup"><span data-stu-id="af40e-137">hello following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="af40e-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="af40e-138">Next steps</span></span>

<span data-ttu-id="af40e-139">Meer informatie over hoe toovisualize uw NSG-flow registreert met Power BI in via [visualiseren NSG loopt logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="af40e-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

