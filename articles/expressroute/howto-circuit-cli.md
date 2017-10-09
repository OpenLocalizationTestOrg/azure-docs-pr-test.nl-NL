---
title: 'Maken en wijzigen van een Azure ExpressRoute-circuit: CLI | Microsoft Docs'
description: Dit artikel wordt beschreven hoe toocreate, inrichten, controleren, bijwerken, verwijderen en een ExpressRoute-circuit met CLI inrichting ervan ongedaan maakt.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="cc5d2-103">Maken en een ExpressRoute-circuit met CLI wijzigen</span><span class="sxs-lookup"><span data-stu-id="cc5d2-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="cc5d2-104">Dit artikel wordt beschreven hoe een Azure ExpressRoute-circuit met behulp van toocreate Hallo opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="cc5d2-104">This article describes how toocreate an Azure ExpressRoute circuit by using hello Command Line Interface (CLI).</span></span> <span data-ttu-id="cc5d2-105">Dit artikel ziet u ook hoe toocheck Hallo status, bijwerken, of verwijderen en een circuit inrichting ervan ongedaan maakt.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-105">This article also shows you how toocheck hello status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="cc5d2-106">Als u een andere methode toowork met ExpressRoute-circuits toouse wilt, kunt u Hallo artikel van Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-106">If you want toouse a different method toowork with ExpressRoute circuits, you can select hello article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc5d2-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cc5d2-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="cc5d2-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc5d2-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="cc5d2-109">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="cc5d2-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="cc5d2-110">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="cc5d2-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="cc5d2-111">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="cc5d2-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="cc5d2-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="cc5d2-112">Before you begin</span></span>

* <span data-ttu-id="cc5d2-113">Installeer de nieuwste versie van de Hallo van Hallo CLI-opdrachten (2.0 of hoger) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-113">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="cc5d2-114">Zie voor meer informatie over het installeren van de CLI-opdrachten Hallo [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli) en [aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cc5d2-114">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="cc5d2-115">Bekijk Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-115">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="cc5d2-116">Maken en een ExpressRoute-circuit inrichten</span><span class="sxs-lookup"><span data-stu-id="cc5d2-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="cc5d2-117">1. Meld u aan tooyour Azure-account en uw abonnement te selecteren</span><span class="sxs-lookup"><span data-stu-id="cc5d2-117">1. Sign in tooyour Azure account and select your subscription</span></span>

<span data-ttu-id="cc5d2-118">toobegin uw configuratie, aanmelden tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-118">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="cc5d2-119">Gebruik Hallo volgen voorbeelden toohelp die u verbinding kunt maken:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-119">Use hello following examples toohelp you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="cc5d2-120">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-120">Check hello subscriptions for hello account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="cc5d2-121">Hallo-abonnement waarvoor u een ExpressRoute-circuit toocreate wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-121">Select hello subscription for which you want toocreate an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="cc5d2-122">2. Hallo-lijst met ondersteunde providers, locaties en bandbreedten</span><span class="sxs-lookup"><span data-stu-id="cc5d2-122">2. Get hello list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="cc5d2-123">Voordat u een ExpressRoute-circuit maken, moet u Hallo lijst met ondersteunde connectiviteitsproviders, locaties en bandbreedte-opties.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-123">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="cc5d2-124">CLI-opdracht 'az netwerk express route lijst-service-providers' Hello retourneert deze informatie, die u in latere stappen:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-124">hello CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="cc5d2-125">Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-125">hello response is similar toohello following example:</span></span>

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

<span data-ttu-id="cc5d2-126">Controleer Hallo antwoord toosee als uw connectiviteitsprovider wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-126">Check hello response toosee if your connectivity provider is listed.</span></span> <span data-ttu-id="cc5d2-127">Maak een notitie van Hallo informatie die u bij het maken van een circuit dient te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-127">Make a note of hello following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="cc5d2-128">Naam</span><span class="sxs-lookup"><span data-stu-id="cc5d2-128">Name</span></span>
* <span data-ttu-id="cc5d2-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="cc5d2-129">PeeringLocations</span></span>
* <span data-ttu-id="cc5d2-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="cc5d2-130">BandwidthsOffered</span></span>

<span data-ttu-id="cc5d2-131">U bent nu klaar toocreate een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-131">You're now ready toocreate an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="cc5d2-132">3. Een ExpressRoute-circuit maken</span><span class="sxs-lookup"><span data-stu-id="cc5d2-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc5d2-133">Uw ExpressRoute-circuit wordt gefactureerd vanaf Hallo moment dat die de sleutel van een service wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-133">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="cc5d2-134">Deze bewerking niet uitvoeren wanneer de connectiviteitsprovider Hallo gereed tooprovision Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-134">Perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="cc5d2-135">Als u nog een resourcegroep hebt, moet u een maken voordat u uw ExpressRoute-circuit maken.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="cc5d2-136">U kunt een resourcegroep maken door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-136">You can create a resource group by running hello following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="cc5d2-137">Hallo volgende voorbeeld ziet u hoe toocreate een 200 Mbps-ExpressRoute-circuit via Equinix in Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-137">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="cc5d2-138">Als u een andere provider en andere instellingen gebruikt, vervangt u die informatie door wanneer u uw aanvraag.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="cc5d2-139">Zorg ervoor dat u de juiste SKU-laag Hallo en SKU-serie opgeeft:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-139">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="cc5d2-140">SKU-laag bepaalt of een standaard ExpressRoute of een premium-invoegtoepassing voor ExpressRoute is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="cc5d2-141">U kunt 'Standaard' tooget Hallo standaard SKU- of Premium voor Hallo premium-invoegtoepassing opgeven.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-141">You can specify 'Standard' tooget hello standard SKU or 'Premium' for hello premium add-on.</span></span>
* <span data-ttu-id="cc5d2-142">SKU-serie, bepaalt Hallo facturering.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-142">SKU family determines hello billing type.</span></span> <span data-ttu-id="cc5d2-143">U kunt 'Metereddata' voor een datalimiet plannings- en 'Unlimiteddata' opgeven voor een onbeperkte gegevens-plan.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="cc5d2-144">U kunt facturering type van het 'Metereddata 'too'Unlimiteddata', maar type niet wijzigen Hallo van 'Unlimiteddata' too'Metereddata' Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-144">You can change hello billing type from 'Metereddata' too'Unlimiteddata', but you can't change hello type from 'Unlimiteddata' too'Metereddata'.</span></span>


<span data-ttu-id="cc5d2-145">Uw ExpressRoute-circuit wordt gefactureerd vanaf Hallo moment dat die de sleutel van een service wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-145">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="cc5d2-146">Hallo volgende voorbeeld wordt een aanvraag voor een nieuwe servicesleutel:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-146">hello following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="cc5d2-147">Hallo-antwoord bevat de servicesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-147">hello response contains hello service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="cc5d2-148">4. Lijst van alle ExpressRoute-circuits</span><span class="sxs-lookup"><span data-stu-id="cc5d2-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="cc5d2-149">een lijst met alle Hallo ExpressRoute-circuits die u hebt gemaakt, tooget Hallo 'az express route lijst met netwerken' opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-149">tooget a list of all hello ExpressRoute circuits that you created, run hello 'az network express-route list' command.</span></span> <span data-ttu-id="cc5d2-150">Met deze opdracht kunt u deze informatie op elk gewenst moment ophalen.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="cc5d2-151">toolist alle circuits zorg Hallo aanroepen zonder parameters.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-151">toolist all circuits, make hello call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="cc5d2-152">De sleutel van uw service wordt vermeld in Hallo *ServiceKey* antwoord Hallo veld.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-152">Your service key is listed in hello *ServiceKey* field of hello response.</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

<span data-ttu-id="cc5d2-153">U kunt gedetailleerde beschrijvingen van alle Hallo parameters ophalen door actieve Hallo-opdracht met Hallo '-h' parameter.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-153">You can get detailed descriptions of all hello parameters by running hello command using hello '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="cc5d2-154">5. Sleutel tooyour Hallo-connectiviteit serviceprovider voor het inrichten van verzenden</span><span class="sxs-lookup"><span data-stu-id="cc5d2-154">5. Send hello service key tooyour connectivity provider for provisioning</span></span>

<span data-ttu-id="cc5d2-155">'ServiceProviderProvisioningState' bevat informatie over de huidige status van de Hallo van inrichting Hallo serviceprovider zijde.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-155">'ServiceProviderProvisioningState' provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="cc5d2-156">Hallo status biedt Hallo status op Hallo Microsoft aan clientzijde.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-156">hello status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="cc5d2-157">Zie voor meer informatie, Hallo [werkstromen artikel](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span><span class="sxs-lookup"><span data-stu-id="cc5d2-157">For more information, see hello [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="cc5d2-158">Bij het maken van nieuwe ExpressRoute-circuit heeft Hallo circuit Hallo status te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-158">When you create a new ExpressRoute circuit, hello circuit is in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="cc5d2-159">Hallo circuit wijzigingen toohello status wanneer Hallo connectiviteitsprovider in Hallo-proces voor het inschakelen van deze voor u te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-159">hello circuit changes toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="cc5d2-160">Voor u toobe kunnen toouse een ExpressRoute-circuit, moet het Hallo status volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-160">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="cc5d2-161">6. Hallo-status en Hallo-status van de Hallo circuit sleutel regelmatig te controleren</span><span class="sxs-lookup"><span data-stu-id="cc5d2-161">6. Periodically check hello status and hello state of hello circuit key</span></span>

<span data-ttu-id="cc5d2-162">Controle op Hallo status en status van Hallo circuit sleutel hello, laat u weten wanneer uw provider uw circuit is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-162">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="cc5d2-163">Nadat het Hallo-circuit is geconfigureerd, is 'ServiceProviderProvisioningState' wordt weergegeven als 'Ingericht', zoals wordt weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-163">After hello circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in hello following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="cc5d2-164">Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-164">hello response is similar toohello following example:</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="cc5d2-165">7. Maken van uw configuratie van de routering</span><span class="sxs-lookup"><span data-stu-id="cc5d2-165">7. Create your routing configuration</span></span>

<span data-ttu-id="cc5d2-166">Zie voor stapsgewijze instructies Hallo [ExpressRoute-circuit routeringsconfiguratie](howto-routing-cli.md) toocreate artikel en circuit peerings wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-166">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](howto-routing-cli.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc5d2-167">Deze instructies zijn alleen van toepassing toocircuits die zijn gemaakt met serviceproviders die services op laag 2-connectiviteit aanbieden.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-167">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="cc5d2-168">Als u een serviceprovider die beheerde laag-3-services (meestal een IP VPN, zoals MPLS), uw connectiviteitsprovider configureert en beheert routering voor u.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="cc5d2-169">8. Koppelen van een virtueel netwerk tooan ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="cc5d2-169">8. Link a virtual network tooan ExpressRoute circuit</span></span>

<span data-ttu-id="cc5d2-170">Koppel vervolgens een virtueel netwerk tooyour ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-170">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="cc5d2-171">Gebruik Hallo [tooExpressRoute circuits koppelt virtuele netwerken](howto-linkvnet-cli.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-171">Use hello [Linking virtual networks tooExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="cc5d2-172"><a name="modify"></a>Wijzigen van een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="cc5d2-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="cc5d2-173">U kunt bepaalde eigenschappen van een ExpressRoute-circuit wijzigen zonder enige impact op connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="cc5d2-174">Kunt u de volgende wijzigingen zonder uitvaltijd Hallo maken:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-174">You can make hello following changes with no downtime:</span></span>

* <span data-ttu-id="cc5d2-175">U kunt in- of uitschakelen van een ExpressRoute premium-invoegtoepassing voor ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="cc5d2-176">U kunt de bandbreedte Hallo van uw ExpressRoute-circuit vergroten mits er capaciteit beschikbaar is op Hallo-poort.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-176">You can increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="cc5d2-177">Echter, Hallo bandbreedte van een circuit downgraden wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-177">However, downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="cc5d2-178">U kunt Hallo softwarelicentiecontrole plan wijzigen van gegevens Datalimiet tooUnlimited gegevens.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-178">You can change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="cc5d2-179">Het wijzigen van echter Hallo softwarelicentiecontrole plan van onbeperkt tooMetered die gegevens worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-179">However, changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="cc5d2-180">U kunt inschakelen en uitschakelen *klassieke bewerkingen toestaan*.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="cc5d2-181">Zie voor meer informatie over limieten en beperkingen Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="cc5d2-181">For more information on limits and limitations, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="cc5d2-182">tooenable hello ExpressRoute premium-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="cc5d2-182">tooenable hello ExpressRoute premium add-on</span></span>

<span data-ttu-id="cc5d2-183">U kunt Hallo ExpressRoute premium-invoegtoepassing voor uw bestaande circuit inschakelen met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-183">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="cc5d2-184">Hallo-circuit heeft nu Hallo ExpressRoute premium-invoegtoepassing voor functies die worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-184">hello circuit now has hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="cc5d2-185">We beginnen facturering voor Hallo premium-invoegtoepassing mogelijkheid zodra Hallo-opdracht met succes is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-185">We begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="cc5d2-186">toodisable hello ExpressRoute premium-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="cc5d2-186">toodisable hello ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc5d2-187">Deze bewerking kan mislukken als u resources die groter zijn dan wat voor Hallo standaard circuit is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-187">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="cc5d2-188">Begrijpen voordat Hallo ExpressRoute premium-invoegtoepassing is uitgeschakeld, Hallo volgende criteria:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-188">Before disabling hello ExpressRoute premium add-on, understand hello following criteria:</span></span>

* <span data-ttu-id="cc5d2-189">Voordat u van premium toostandard downgraden, moet u ervoor zorgen dat er minder dan 10 virtuele netwerken gekoppelde toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-189">Before you downgrade from premium toostandard, you must make sure that you have fewer than 10 virtual networks linked toohello circuit.</span></span> <span data-ttu-id="cc5d2-190">Als u meer dan 10 hebt, uw aanvraag bijwerken mislukt en er kosten in rekening brengen volgens de premietarieven voor.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="cc5d2-191">U moet alle virtuele netwerken in andere geopolitieke regio's ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="cc5d2-192">Als u niet alle virtuele netwerken ontkoppelt, mislukt de updateaanvraag en we u volgens de premietarieven voor rekening.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="cc5d2-193">De routetabel moet minder dan 4000 routes voor persoonlijke peering.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="cc5d2-194">Als uw tabel route groter dan 4000 routes is, zakt Hallo BGP-sessie.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-194">If your route table size is greater than 4,000 routes, hello BGP session drops.</span></span> <span data-ttu-id="cc5d2-195">Hallo sessie won't totdat het aantal geadverteerde voorvoegsels Hallo lager dan 4000 is worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-195">hello session won't be reenabled until hello number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="cc5d2-196">U kunt Hallo-invoegtoepassing voor ExpressRoute premium voor een bestaand circuit Hallo uitschakelen met behulp van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-196">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="cc5d2-197">bandbreedte tooupdate hello ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="cc5d2-197">tooupdate hello ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="cc5d2-198">Controleer voor Hallo ondersteund bandbreedte-opties voor uw provider, Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="cc5d2-198">For hello supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="cc5d2-199">U kunt de grootte die groter zijn dan de grootte van uw bestaande circuit Hallo verzamelen.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-199">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc5d2-200">Als er onvoldoende capaciteit op de bestaande poort hello, mogelijk hebt u toorecreate hello ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-200">If there is inadequate capacity on hello existing port, you may have toorecreate hello ExpressRoute circuit.</span></span> <span data-ttu-id="cc5d2-201">U kunt Hallo circuit niet upgraden als er geen extra capaciteit beschikbaar is op die locatie.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-201">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="cc5d2-202">U kunt Hallo bandbreedte van een ExpressRoute-circuit zonder onderbreking niet reduceren.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-202">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="cc5d2-203">Bandbreedte downgraden vereist u toodeprovision hello ExpressRoute-circuit en vervolgens opnieuw inrichten van nieuwe ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-203">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="cc5d2-204">Nadat u hebt besloten Hallo grootte die u nodig hebt, uw circuit Hallo opdracht tooresize volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-204">After you decide hello size you need, use hello following command tooresize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="cc5d2-205">Uw circuit wordt aangepast Hallo Microsoft zijde.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-205">Your circuit is sized up on hello Microsoft side.</span></span> <span data-ttu-id="cc5d2-206">Vervolgens maakt u moet contact opnemen met uw connectiviteit provider tooupdate-configuraties van hun kant toomatch deze wijziging.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-206">Next, you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="cc5d2-207">Nadat u deze melding, beginnen wij u facturering voor Hallo bijgewerkt bandbreedte optie.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-207">After you make this notification, we begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="cc5d2-208">toomove hello SKU van gecontroleerde toounlimited</span><span class="sxs-lookup"><span data-stu-id="cc5d2-208">toomove hello SKU from metered toounlimited</span></span>

<span data-ttu-id="cc5d2-209">U kunt Hallo SKU van een ExpressRoute-circuit wijzigen met behulp van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-209">You can change hello SKU of an ExpressRoute circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="cc5d2-210">toocontrol toegang toohello klassieke en Resource Manager-omgevingen</span><span class="sxs-lookup"><span data-stu-id="cc5d2-210">toocontrol access toohello classic and Resource Manager environments</span></span>

<span data-ttu-id="cc5d2-211">Lees de instructies Hallo in [verplaatsen ExpressRoute-circuits vanuit Hallo klassieke toohello Resource Manager-implementatiemodel](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="cc5d2-211">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="cc5d2-212">Opheffen van inrichting en een ExpressRoute-circuit verwijderen</span><span class="sxs-lookup"><span data-stu-id="cc5d2-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="cc5d2-213">toodeprovision en een ExpressRoute-circuit verwijderen Zorg er dan voor dat u begrijpt Hallo volgende criteria:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-213">toodeprovision and delete an ExpressRoute circuit, make sure you understand hello following criteria:</span></span>

* <span data-ttu-id="cc5d2-214">U moet alle virtuele netwerken vanuit Hallo ExpressRoute-circuit ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-214">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="cc5d2-215">Als deze bewerking is mislukt, controleert u toosee als er geen virtuele netwerken zijn gekoppeld toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-215">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="cc5d2-216">Als Hallo ExpressRoute-circuit serviceprovider Inrichtingsstatus **inrichten** of **ingericht**, moet u werken met uw serviceprovider toodeprovision Hallo circuit op hun kant.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-216">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="cc5d2-217">We gaan tooreserve resources en kosten in rekening brengen totdat Hallo serviceprovider inrichting Hallo circuit is voltooid en een melding van ons.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-217">We continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="cc5d2-218">U kunt Hallo circuit verwijderen als serviceprovider Hallo heeft gemaakt Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-218">You can delete hello circuit if hello service provider has deprovisioned hello circuit.</span></span> <span data-ttu-id="cc5d2-219">Wanneer een circuit is gemaakt, Hallo serviceprovider Inrichtingsstatus te ingesteld**niet ingericht**.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-219">When a circuit is deprovisioned, hello service provider provisioning state is set too**Not provisioned**.</span></span> <span data-ttu-id="cc5d2-220">Hierdoor wordt voorkomen dat facturering voor Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="cc5d2-220">This stops billing for hello circuit.</span></span>

<span data-ttu-id="cc5d2-221">U kunt uw ExpressRoute-circuit verwijderen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-221">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="cc5d2-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cc5d2-222">Next steps</span></span>

<span data-ttu-id="cc5d2-223">Nadat u het circuit hebt gemaakt, zorg dat u Hallo volgende taken:</span><span class="sxs-lookup"><span data-stu-id="cc5d2-223">After you create your circuit, make sure that you do hello following tasks:</span></span>

* [<span data-ttu-id="cc5d2-224">Maken en aanpassen van routering voor ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="cc5d2-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="cc5d2-225">Koppelen van uw virtuele netwerk tooyour ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="cc5d2-225">Link your virtual network tooyour ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)
