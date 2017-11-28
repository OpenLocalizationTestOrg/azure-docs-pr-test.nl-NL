---
title: Beheerde toepassing VirtualNetworkCombo UI-element aaaAzure | Microsoft Docs
description: Beschrijft Hallo Microsoft.Network.VirtualNetworkCombo UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="77eed-103">Microsoft.Network.VirtualNetworkCombo UI-element</span><span class="sxs-lookup"><span data-stu-id="77eed-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="77eed-104">Een groep besturingselementen voor het selecteren van een nieuw of bestaand virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="77eed-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="77eed-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="77eed-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="77eed-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="77eed-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="77eed-108">In de bovenste draadmodel hello, heeft Hallo gebruiker een nieuw virtueel netwerk verzameld zodat Hallo gebruiker elk subnet naam en adres voorvoegsel kan aanpassen.</span><span class="sxs-lookup"><span data-stu-id="77eed-108">In hello top wireframe, hello user has picked a new virtual network, so hello user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="77eed-109">Subnetten configureren is in dit geval optioneel.</span><span class="sxs-lookup"><span data-stu-id="77eed-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="77eed-110">In Hallo onderaan draadmodel, Hallo gebruiker heeft gekozen een bestaand virtueel netwerk, zodat Hallo gebruiker moet worden toegewezen elk subnet Hallo-implementatiesjabloon bestaand subnet tooan vereist.</span><span class="sxs-lookup"><span data-stu-id="77eed-110">In hello bottom wireframe, hello user has picked an existing virtual network, so hello user must map each subnet hello deployment template requires tooan existing subnet.</span></span> <span data-ttu-id="77eed-111">Subnetten configureren is in dit geval vereist.</span><span class="sxs-lookup"><span data-stu-id="77eed-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="77eed-112">Schema</span><span class="sxs-lookup"><span data-stu-id="77eed-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="77eed-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="77eed-113">Remarks</span></span>
- <span data-ttu-id="77eed-114">Indien opgegeven, de eerste niet-overlappende adresvoorvoegsel met een grootte van Hallo `defaultValue.addressPrefixSize` automatisch op basis van de bestaande virtuele netwerken in het abonnement van de gebruiker hello wordt bepaald.</span><span class="sxs-lookup"><span data-stu-id="77eed-114">If specified, hello first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in hello user's subscription.</span></span>
- <span data-ttu-id="77eed-115">de standaardwaarde voor Hallo `defaultValue.name` en `defaultValue.addressPrefixSize` is **null**.</span><span class="sxs-lookup"><span data-stu-id="77eed-115">hello default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="77eed-116">`constraints.minAddressPrefixSize`moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="77eed-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="77eed-117">Een bestaande virtuele netwerken met een adresruimte die kleiner is dan hello opgegeven waarde zijn niet beschikbaar voor selectie.</span><span class="sxs-lookup"><span data-stu-id="77eed-117">Any existing virtual networks with an address space smaller than hello specified value are unavailable for selection.</span></span>
- <span data-ttu-id="77eed-118">`subnets`Er moet worden opgegeven en `constraints.minAddressPrefixSize` voor elk subnet moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="77eed-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="77eed-119">Wanneer u een nieuw virtueel netwerk maakt, adresvoorvoegsel voor elk subnet wordt automatisch berekend op Hallo van het virtuele netwerk adresvoorvoegsel en de respectieve `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="77eed-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on hello virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="77eed-120">Wanneer u een bestaande virtuele netwerk, kleiner is dan de respectieve subnetten `constraints.minAddressPrefixSize` zijn niet beschikbaar voor selectie.</span><span class="sxs-lookup"><span data-stu-id="77eed-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="77eed-121">Bovendien, indien opgegeven, subnetten die bevatten geen ten minste `minAddressCount` beschikbare adressen zijn niet beschikbaar voor selectie.</span><span class="sxs-lookup"><span data-stu-id="77eed-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="77eed-122">de standaardwaarde Hallo is **0**.</span><span class="sxs-lookup"><span data-stu-id="77eed-122">hello default value is **0**.</span></span> <span data-ttu-id="77eed-123">tooensure die Hallo beschikbare adressen zijn aaneengesloten, geeft u **true** voor `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="77eed-123">tooensure that hello available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="77eed-124">de standaardwaarde Hallo is **true**.</span><span class="sxs-lookup"><span data-stu-id="77eed-124">hello default value is **true**.</span></span>
- <span data-ttu-id="77eed-125">Maken van subnetten in een bestaand virtueel netwerk wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="77eed-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="77eed-126">Als `options.hideExisting` is **true**, Hallo gebruiker een bestaand virtueel netwerk niet kiezen.</span><span class="sxs-lookup"><span data-stu-id="77eed-126">If `options.hideExisting` is **true**, hello user can't choose an existing virtual network.</span></span> <span data-ttu-id="77eed-127">de standaardwaarde Hallo is **false**.</span><span class="sxs-lookup"><span data-stu-id="77eed-127">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="77eed-128">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="77eed-128">Sample output</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="77eed-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="77eed-129">Next steps</span></span>
* <span data-ttu-id="77eed-130">Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77eed-130">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="77eed-131">Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77eed-131">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="77eed-132">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="77eed-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
