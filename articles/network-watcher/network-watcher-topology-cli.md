---
title: Weergeven van de Azure-netwerk-Watcher-topologie - Azure CLI | Microsoft Docs
description: In dit artikel wordt beschreven hoe Azure CLI gebruiken om op te vragen uw netwerktopologie.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5be8e103f9a1f32117a4ed3be73bff021db1186d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a><span data-ttu-id="a3f17-103">Netwerk-Watcher-topologie met Azure CLI weergeven</span><span class="sxs-lookup"><span data-stu-id="a3f17-103">View Network Watcher topology with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a3f17-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3f17-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="a3f17-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a3f17-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="a3f17-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a3f17-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="a3f17-107">REST API</span><span class="sxs-lookup"><span data-stu-id="a3f17-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="a3f17-108">De functie van de topologie van netwerk-Watcher biedt een visuele representatie van de netwerkbronnen in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="a3f17-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="a3f17-109">In de portal voor is deze visualisatie aan u gepresenteerd automatisch.</span><span class="sxs-lookup"><span data-stu-id="a3f17-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="a3f17-110">De gegevens achter de Topologieweergave in de portal kan worden opgehaald via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3f17-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="a3f17-111">Hierdoor is de topologische informatie flexibeler omdat de gegevens kunnen worden gebruikt door andere hulpprogramma's voor het bouwen van de visualisatie.</span><span class="sxs-lookup"><span data-stu-id="a3f17-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="a3f17-112">Dit artikel wordt platformoverschrijdende Azure CLI 1.0 gebruikt die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="a3f17-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="a3f17-113">Netwerk-Watcher gebruikt momenteel de Azure CLI 1.0 voor CLI-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="a3f17-113">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

<span data-ttu-id="a3f17-114">De koppeling is gemodelleerd onder twee-relaties.</span><span class="sxs-lookup"><span data-stu-id="a3f17-114">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="a3f17-115">**Containment** -voorbeeld: VNet bevat een Subnet bevat een NIC</span><span class="sxs-lookup"><span data-stu-id="a3f17-115">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="a3f17-116">**Gekoppeld** -voorbeeld: NIC is gekoppeld aan een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="a3f17-116">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="a3f17-117">De volgende lijst bevat eigenschappen die worden geretourneerd bij het opvragen van de topologie REST-API.</span><span class="sxs-lookup"><span data-stu-id="a3f17-117">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="a3f17-118">**naam** -de naam van de resource</span><span class="sxs-lookup"><span data-stu-id="a3f17-118">**name** - The name of the resource</span></span>
* <span data-ttu-id="a3f17-119">**id** -de uri van de resource.</span><span class="sxs-lookup"><span data-stu-id="a3f17-119">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="a3f17-120">**locatie** -de locatie waar de resource is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a3f17-120">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="a3f17-121">**koppelingen** -een lijst met koppelingen naar het object waarnaar wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="a3f17-121">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="a3f17-122">**naam** -de naam van de bron waarnaar wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="a3f17-122">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="a3f17-123">**resourceId** -resourceId van de is de uri van de bron waarnaar wordt verwezen in de koppeling.</span><span class="sxs-lookup"><span data-stu-id="a3f17-123">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="a3f17-124">**associationType** -deze waarde verwijst naar de relatie tussen het onderliggende object en het bovenliggende item.</span><span class="sxs-lookup"><span data-stu-id="a3f17-124">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="a3f17-125">Geldige waarden zijn **bevat** of **gekoppelde**.</span><span class="sxs-lookup"><span data-stu-id="a3f17-125">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a3f17-126">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="a3f17-126">Before you begin</span></span>

<span data-ttu-id="a3f17-127">In dit scenario gebruikt u de `network watcher topology` cmdlet voor het ophalen van de topologische informatie.</span><span class="sxs-lookup"><span data-stu-id="a3f17-127">In this scenario, you use the `network watcher topology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="a3f17-128">Er is ook een artikel over het [ophalen netwerktopologie met REST-API](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="a3f17-128">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="a3f17-129">Dit scenario wordt ervan uitgegaan dat u de stappen in al hebt gevolgd [maken van een netwerk-Watcher](network-watcher-create.md) voor het maken van een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="a3f17-129">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="a3f17-130">Scenario</span><span class="sxs-lookup"><span data-stu-id="a3f17-130">Scenario</span></span>

<span data-ttu-id="a3f17-131">Het scenario beschreven in dit artikel wordt het antwoord van de topologie voor een opgegeven resourcegroep opgehaald.</span><span class="sxs-lookup"><span data-stu-id="a3f17-131">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="a3f17-132">Topologie ophalen</span><span class="sxs-lookup"><span data-stu-id="a3f17-132">Retrieve topology</span></span>

<span data-ttu-id="a3f17-133">De `network watcher topology` cmdlet haalt de topologie voor een bepaalde groep.</span><span class="sxs-lookup"><span data-stu-id="a3f17-133">The `network watcher topology` cmdlet retrieves the topology for a given resource group.</span></span> <span data-ttu-id="a3f17-134">Voeg het argument '--json ' de oput weergeven in json-indeling</span><span class="sxs-lookup"><span data-stu-id="a3f17-134">Add the argument "--json" to view the oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="a3f17-135">Resultaten</span><span class="sxs-lookup"><span data-stu-id="a3f17-135">Results</span></span>

<span data-ttu-id="a3f17-136">De resultaten hebben een eigenschap name 'Resources', waarin de json-antwoordtekst voor de `network watcher topology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a3f17-136">The results returned have a property name "Resources", which contains the json response body for the `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="a3f17-137">Het antwoord bevat de resources in de Netwerkbeveiligingsgroep en de bijbehorende koppelingen (dat wil zeggen, bevat, gekoppelde).</span><span class="sxs-lookup"><span data-stu-id="a3f17-137">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="a3f17-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a3f17-138">Next steps</span></span>

<span data-ttu-id="a3f17-139">Meer informatie over de beveiligingsregels voor verbindingen die worden toegepast op uw netwerkbronnen in via [beveiligingsoverzicht groep weergeven](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a3f17-139">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
