---
title: aaaView Azure-netwerk-Watcher-topologie - Azure CLI | Microsoft Docs
description: In dit artikel wordt beschreven hoe toouse Azure CLI tooquery topologie van uw netwerk.
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
ms.openlocfilehash: afa7e7dd844ecb2ab4c616ba99fa0a433f1e4ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a><span data-ttu-id="17ece-103">Netwerk-Watcher-topologie met Azure CLI weergeven</span><span class="sxs-lookup"><span data-stu-id="17ece-103">View Network Watcher topology with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="17ece-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="17ece-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="17ece-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="17ece-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="17ece-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="17ece-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="17ece-107">REST API</span><span class="sxs-lookup"><span data-stu-id="17ece-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="17ece-108">Hallo-topologie-functie van netwerk-Watcher biedt een visuele representatie van Hallo netwerkbronnen in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="17ece-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="17ece-109">In de portal Hallo is deze visualisatie opgenomen tooyou automatisch.</span><span class="sxs-lookup"><span data-stu-id="17ece-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="17ece-110">Hallo gegevens achter Hallo Topologieweergave in de portal Hallo kan worden opgehaald via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="17ece-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="17ece-111">Hierdoor kunt u meer mogelijkheden zoals Hallo gegevens kunnen worden gebruikt door andere hulpprogramma's voor toobuild uit Hallo visualisatie Hallo topologische informatie.</span><span class="sxs-lookup"><span data-stu-id="17ece-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="17ece-112">Dit artikel wordt platformoverschrijdende Azure CLI 1.0 gebruikt die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="17ece-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="17ece-113">Netwerk-Watcher gebruikt momenteel de Azure CLI 1.0 voor CLI-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="17ece-113">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

<span data-ttu-id="17ece-114">Hallo-koppeling is gemodelleerd onder twee-relaties.</span><span class="sxs-lookup"><span data-stu-id="17ece-114">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="17ece-115">**Containment** -voorbeeld: VNet bevat een Subnet bevat een NIC</span><span class="sxs-lookup"><span data-stu-id="17ece-115">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="17ece-116">**Gekoppeld** -voorbeeld: NIC is gekoppeld aan een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="17ece-116">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="17ece-117">Hallo bevat volgende lijst eigenschappen die worden geretourneerd bij het opvragen van Hallo topologie REST-API.</span><span class="sxs-lookup"><span data-stu-id="17ece-117">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="17ece-118">**naam** - hello naam van het Hallo-resource</span><span class="sxs-lookup"><span data-stu-id="17ece-118">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="17ece-119">**id** -uri van de resource Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="17ece-119">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="17ece-120">**locatie** -Hallo locatie waar Hallo resource is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="17ece-120">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="17ece-121">**koppelingen** -een lijst met koppelingen toohello verwijst naar object.</span><span class="sxs-lookup"><span data-stu-id="17ece-121">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="17ece-122">**naam** -naam Hallo Hallo waarnaar wordt verwezen resource.</span><span class="sxs-lookup"><span data-stu-id="17ece-122">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="17ece-123">**resourceId** -Hallo resourceId Hallo-uri van Hallo resource waarnaar wordt verwezen in Hallo-koppeling is.</span><span class="sxs-lookup"><span data-stu-id="17ece-123">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="17ece-124">**associationType** -Hallo relatie tussen Hallo onderliggend object en de bovenliggende Hallo wordt verwezen naar deze waarde.</span><span class="sxs-lookup"><span data-stu-id="17ece-124">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="17ece-125">Geldige waarden zijn **bevat** of **gekoppelde**.</span><span class="sxs-lookup"><span data-stu-id="17ece-125">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="17ece-126">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="17ece-126">Before you begin</span></span>

<span data-ttu-id="17ece-127">In dit scenario gebruikt u Hallo `network watcher topology` cmdlet tooretrieve Hallo topologische informatie.</span><span class="sxs-lookup"><span data-stu-id="17ece-127">In this scenario, you use hello `network watcher topology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="17ece-128">Er is ook een artikel over het te[ophalen netwerktopologie met REST-API](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="17ece-128">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="17ece-129">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="17ece-129">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="17ece-130">Scenario</span><span class="sxs-lookup"><span data-stu-id="17ece-130">Scenario</span></span>

<span data-ttu-id="17ece-131">Hallo scenario beschreven in dit artikel wordt antwoord van de Hallo-topologie voor een opgegeven resourcegroep opgehaald.</span><span class="sxs-lookup"><span data-stu-id="17ece-131">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="17ece-132">Topologie ophalen</span><span class="sxs-lookup"><span data-stu-id="17ece-132">Retrieve topology</span></span>

<span data-ttu-id="17ece-133">Hallo `network watcher topology` cmdlet haalt Hallo-topologie voor een opgegeven resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="17ece-133">hello `network watcher topology` cmdlet retrieves hello topology for a given resource group.</span></span> <span data-ttu-id="17ece-134">Voeg Hallo argument '--json ' tooview hello oput in json-indeling</span><span class="sxs-lookup"><span data-stu-id="17ece-134">Add hello argument "--json" tooview hello oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="17ece-135">Resultaten</span><span class="sxs-lookup"><span data-stu-id="17ece-135">Results</span></span>

<span data-ttu-id="17ece-136">Hallo resultaten hebben een eigenschap name 'Resources', waarin Hallo json antwoordtekst voor Hallo `network watcher topology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="17ece-136">hello results returned have a property name "Resources", which contains hello json response body for hello `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="17ece-137">Hallo-antwoord bevat Hallo bronnen Hallo Netwerkbeveiligingsgroep en de bijbehorende koppelingen (dat wil zeggen, bevat, gekoppelde).</span><span class="sxs-lookup"><span data-stu-id="17ece-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="17ece-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="17ece-138">Next steps</span></span>

<span data-ttu-id="17ece-139">Meer informatie over Hallo beveiligingsregels voor verbindingen die toegepast tooyour netwerkbronnen in via zijn [beveiligingsoverzicht groep weergeven](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="17ece-139">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
