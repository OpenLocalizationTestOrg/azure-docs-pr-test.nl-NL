---
title: Azure beheerde toepassing VirtualNetworkCombo UI-element | Microsoft Docs
description: Beschrijft het Microsoft.Network.VirtualNetworkCombo UI-element voor beheerde Azure-toepassingen
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 8bb255b76ac5c3de570fa569a1cfb3ee953f9687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="a4b4e-103">Microsoft.Network.VirtualNetworkCombo UI-element</span><span class="sxs-lookup"><span data-stu-id="a4b4e-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="a4b4e-104">Een groep besturingselementen voor het selecteren van een nieuw of bestaand virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="a4b4e-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a4b4e-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="a4b4e-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="a4b4e-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="a4b4e-108">In de bovenste draadmodel heeft de gebruiker een nieuw virtueel netwerk verzameld, zodat de gebruiker de naam en adres voorvoegsel elk subnet kan aanpassen.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-108">In the top wireframe, the user has picked a new virtual network, so the user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="a4b4e-109">Subnetten configureren is in dit geval optioneel.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="a4b4e-110">In de draadmodel onder een bestaand virtueel netwerk op de gebruiker heeft gekozen zodat de gebruiker elk subnet dat is vereist voor de implementatiesjabloon moet worden toegewezen aan een bestaand subnet.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-110">In the bottom wireframe, the user has picked an existing virtual network, so the user must map each subnet the deployment template requires to an existing subnet.</span></span> <span data-ttu-id="a4b4e-111">Subnetten configureren is in dit geval vereist.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="a4b4e-112">Schema</span><span class="sxs-lookup"><span data-stu-id="a4b4e-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="a4b4e-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a4b4e-113">Remarks</span></span>
- <span data-ttu-id="a4b4e-114">Als opgegeven, voorvoegsel van de grootte van de eerste niet-overlappende adres `defaultValue.addressPrefixSize` automatisch op basis van de bestaande virtuele netwerken in het abonnement van de gebruiker wordt bepaald.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-114">If specified, the first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in the user's subscription.</span></span>
- <span data-ttu-id="a4b4e-115">De standaardwaarde voor `defaultValue.name` en `defaultValue.addressPrefixSize` is **null**.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-115">The default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="a4b4e-116">`constraints.minAddressPrefixSize`moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="a4b4e-117">Een bestaande virtuele netwerken met een adresruimte die kleiner is dan de opgegeven waarde zijn niet beschikbaar voor selectie.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-117">Any existing virtual networks with an address space smaller than the specified value are unavailable for selection.</span></span>
- <span data-ttu-id="a4b4e-118">`subnets`Er moet worden opgegeven en `constraints.minAddressPrefixSize` voor elk subnet moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="a4b4e-119">Wanneer u een nieuw virtueel netwerk maakt, adresvoorvoegsel voor elk subnet wordt automatisch berekend op het virtuele netwerk adresvoorvoegsel en de respectieve `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on the virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="a4b4e-120">Wanneer u een bestaande virtuele netwerk, kleiner is dan de respectieve subnetten `constraints.minAddressPrefixSize` zijn niet beschikbaar voor selectie.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="a4b4e-121">Bovendien, indien opgegeven, subnetten die bevatten geen ten minste `minAddressCount` beschikbare adressen zijn niet beschikbaar voor selectie.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="a4b4e-122">De standaardwaarde is **0**.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-122">The default value is **0**.</span></span> <span data-ttu-id="a4b4e-123">Om ervoor te zorgen dat de beschikbare adressen aaneengesloten zijn, geef **true** voor `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-123">To ensure that the available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="a4b4e-124">De standaardwaarde is **true**.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-124">The default value is **true**.</span></span>
- <span data-ttu-id="a4b4e-125">Maken van subnetten in een bestaand virtueel netwerk wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="a4b4e-126">Als `options.hideExisting` is **true**, de gebruiker een bestaand virtueel netwerk niet kiezen.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-126">If `options.hideExisting` is **true**, the user can't choose an existing virtual network.</span></span> <span data-ttu-id="a4b4e-127">De standaardwaarde is **false**.</span><span class="sxs-lookup"><span data-stu-id="a4b4e-127">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="a4b4e-128">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="a4b4e-128">Sample output</span></span>
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="a4b4e-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4b4e-129">Next steps</span></span>
* <span data-ttu-id="a4b4e-130">Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4b4e-130">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="a4b4e-131">Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4b4e-131">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="a4b4e-132">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="a4b4e-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
