---
title: 'Maken en wijzigen van een Azure ExpressRoute-circuit: CLI | Microsoft Docs'
description: In dit artikel wordt beschreven hoe maken, richten, controleren, bijwerken, verwijderen en een ExpressRoute-circuit met CLI inrichting ervan ongedaan.
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
ms.openlocfilehash: 1a1c9a96b772868e2c832e9ff57874038c0db2d4
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="11a82-103">Maken en een ExpressRoute-circuit met CLI wijzigen</span><span class="sxs-lookup"><span data-stu-id="11a82-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="11a82-104">In dit artikel wordt beschreven hoe een Azure ExpressRoute-circuit maken via de opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="11a82-104">This article describes how to create an Azure ExpressRoute circuit by using the Command Line Interface (CLI).</span></span> <span data-ttu-id="11a82-105">Dit artikel ziet u ook het controleren van de status, update of delete en inrichting ervan ongedaan maakt een circuit.</span><span class="sxs-lookup"><span data-stu-id="11a82-105">This article also shows you how to check the status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="11a82-106">Als u wilt een andere methode gebruiken om te werken met ExpressRoute-circuits, kunt u het artikel uit de volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="11a82-106">If you want to use a different method to work with ExpressRoute circuits, you can select the article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="11a82-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="11a82-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="11a82-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="11a82-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="11a82-109">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="11a82-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="11a82-110">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="11a82-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="11a82-111">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="11a82-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="11a82-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="11a82-112">Before you begin</span></span>

* <span data-ttu-id="11a82-113">Installeer eerst de meest recente versie van de CLI-opdrachten (2.0 of hoger).</span><span class="sxs-lookup"><span data-stu-id="11a82-113">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="11a82-114">Zie [Azure CLI 2.0 installeren](/cli/azure/install-azure-cli) en [Aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli) voor meer informatie over het installeren van de CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="11a82-114">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="11a82-115">Controleer de [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="11a82-115">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="11a82-116">Maken en een ExpressRoute-circuit inrichten</span><span class="sxs-lookup"><span data-stu-id="11a82-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-to-your-azure-account-and-select-your-subscription"></a><span data-ttu-id="11a82-117">1. Aanmelden bij uw Azure-account en uw abonnement te selecteren</span><span class="sxs-lookup"><span data-stu-id="11a82-117">1. Sign in to your Azure account and select your subscription</span></span>

<span data-ttu-id="11a82-118">Om te beginnen met uw configuratie, moet u zich aanmelden bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="11a82-118">To begin your configuration, sign in to your Azure account.</span></span> <span data-ttu-id="11a82-119">Met de volgende voorbeelden kunt u verbinding kunt maken:</span><span class="sxs-lookup"><span data-stu-id="11a82-119">Use the following examples to help you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="11a82-120">Controleer de abonnementen voor het account.</span><span class="sxs-lookup"><span data-stu-id="11a82-120">Check the subscriptions for the account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="11a82-121">Selecteer het abonnement waarvoor u wilt maken van een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="11a82-121">Select the subscription for which you want to create an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="11a82-122">2. De lijst met ondersteunde providers, locaties en bandbreedten ophalen</span><span class="sxs-lookup"><span data-stu-id="11a82-122">2. Get the list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="11a82-123">Voordat u een ExpressRoute-circuit maken, moet u de lijst met ondersteunde connectiviteitsproviders, locaties en bandbreedte-opties.</span><span class="sxs-lookup"><span data-stu-id="11a82-123">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="11a82-124">De CLI-opdracht 'az netwerk express route lijst-service-providers' retourneert deze informatie, die u in latere stappen:</span><span class="sxs-lookup"><span data-stu-id="11a82-124">The CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="11a82-125">Het antwoord is vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11a82-125">The response is similar to the following example:</span></span>

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

<span data-ttu-id="11a82-126">Controleer het antwoord om te zien als uw connectiviteitsprovider wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="11a82-126">Check the response to see if your connectivity provider is listed.</span></span> <span data-ttu-id="11a82-127">Noteer de volgende informatie, u moet bij het maken van een circuit:</span><span class="sxs-lookup"><span data-stu-id="11a82-127">Make a note of the following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="11a82-128">Naam</span><span class="sxs-lookup"><span data-stu-id="11a82-128">Name</span></span>
* <span data-ttu-id="11a82-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="11a82-129">PeeringLocations</span></span>
* <span data-ttu-id="11a82-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="11a82-130">BandwidthsOffered</span></span>

<span data-ttu-id="11a82-131">U kunt nu gereed voor het maken van een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="11a82-131">You're now ready to create an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="11a82-132">3. Een ExpressRoute-circuit maken</span><span class="sxs-lookup"><span data-stu-id="11a82-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11a82-133">Uw ExpressRoute-circuit wordt gefactureerd vanaf het moment dat de sleutel van een service wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="11a82-133">Your ExpressRoute circuit is billed from the moment a service key is issued.</span></span> <span data-ttu-id="11a82-134">Deze bewerking niet uitvoeren wanneer de connectiviteitsprovider gereed is voor het inrichten van het circuit.</span><span class="sxs-lookup"><span data-stu-id="11a82-134">Perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="11a82-135">Als u nog een resourcegroep hebt, moet u een maken voordat u uw ExpressRoute-circuit maken.</span><span class="sxs-lookup"><span data-stu-id="11a82-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="11a82-136">U kunt een resourcegroep maken met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="11a82-136">You can create a resource group by running the following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="11a82-137">Het volgende voorbeeld ziet hoe u een 200-Mbps ExpressRoute-circuit via Equinix in Silicon Valley maakt.</span><span class="sxs-lookup"><span data-stu-id="11a82-137">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="11a82-138">Als u een andere provider en andere instellingen gebruikt, vervangt u die informatie door wanneer u uw aanvraag.</span><span class="sxs-lookup"><span data-stu-id="11a82-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="11a82-139">Zorg ervoor dat u de juiste SKU-laag en de SKU-serie opgeven:</span><span class="sxs-lookup"><span data-stu-id="11a82-139">Make sure that you specify the correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="11a82-140">SKU-laag bepaalt of een standaard ExpressRoute of een premium-invoegtoepassing voor ExpressRoute is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="11a82-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="11a82-141">U kunt 'Standaard' voor de SKU-standard of Premium voor de premium-invoegtoepassing opgeven.</span><span class="sxs-lookup"><span data-stu-id="11a82-141">You can specify 'Standard' to get the standard SKU or 'Premium' for the premium add-on.</span></span>
* <span data-ttu-id="11a82-142">SKU-serie, bepaalt de facturering.</span><span class="sxs-lookup"><span data-stu-id="11a82-142">SKU family determines the billing type.</span></span> <span data-ttu-id="11a82-143">U kunt 'Metereddata' voor een datalimiet plannings- en 'Unlimiteddata' opgeven voor een onbeperkte gegevens-plan.</span><span class="sxs-lookup"><span data-stu-id="11a82-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="11a82-144">U kunt ook het facturering type 'Metereddata'-'Unlimiteddata' wijzigen, maar u het type 'Unlimiteddata'-'Metereddata' niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="11a82-144">You can change the billing type from 'Metereddata' to 'Unlimiteddata', but you can't change the type from 'Unlimiteddata' to 'Metereddata'.</span></span>


<span data-ttu-id="11a82-145">Uw ExpressRoute-circuit wordt gefactureerd vanaf het moment dat de sleutel van een service wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="11a82-145">Your ExpressRoute circuit is billed from the moment a service key is issued.</span></span> <span data-ttu-id="11a82-146">Het volgende voorbeeld wordt een aanvraag voor een nieuwe servicesleutel:</span><span class="sxs-lookup"><span data-stu-id="11a82-146">The following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="11a82-147">Het antwoord bevat de sleutel van de service.</span><span class="sxs-lookup"><span data-stu-id="11a82-147">The response contains the service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="11a82-148">4. Lijst van alle ExpressRoute-circuits</span><span class="sxs-lookup"><span data-stu-id="11a82-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="11a82-149">Als u een lijst met alle ExpressRoute-circuits die u hebt gemaakt, voert u de opdracht 'az express route lijst met netwerken'.</span><span class="sxs-lookup"><span data-stu-id="11a82-149">To get a list of all the ExpressRoute circuits that you created, run the 'az network express-route list' command.</span></span> <span data-ttu-id="11a82-150">Met deze opdracht kunt u deze informatie op elk gewenst moment ophalen.</span><span class="sxs-lookup"><span data-stu-id="11a82-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="11a82-151">Als alle circuits wilt weergeven, voer de aanroep zonder parameters.</span><span class="sxs-lookup"><span data-stu-id="11a82-151">To list all circuits, make the call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="11a82-152">De sleutel van uw service wordt vermeld in de *ServiceKey* veld van het antwoord.</span><span class="sxs-lookup"><span data-stu-id="11a82-152">Your service key is listed in the *ServiceKey* field of the response.</span></span>

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

<span data-ttu-id="11a82-153">Krijgt u gedetailleerde beschrijvingen van alle parameters door het uitvoeren van de opdracht met behulp van de '-h' parameter.</span><span class="sxs-lookup"><span data-stu-id="11a82-153">You can get detailed descriptions of all the parameters by running the command using the '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="11a82-154">5. De servicesleutel verzenden naar uw connectiviteitsprovider voor inrichting</span><span class="sxs-lookup"><span data-stu-id="11a82-154">5. Send the service key to your connectivity provider for provisioning</span></span>

<span data-ttu-id="11a82-155">'ServiceProviderProvisioningState' bevat informatie over de huidige status van inrichting aan de kant van de serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="11a82-155">'ServiceProviderProvisioningState' provides information about the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="11a82-156">De status van de biedt status van de aan de kant van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="11a82-156">The status provides the state on the Microsoft side.</span></span> <span data-ttu-id="11a82-157">Zie voor meer informatie de [werkstromen artikel](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span><span class="sxs-lookup"><span data-stu-id="11a82-157">For more information, see the [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="11a82-158">Wanneer u een nieuwe ExpressRoute-circuit maakt, wordt het circuit in de volgende status is:</span><span class="sxs-lookup"><span data-stu-id="11a82-158">When you create a new ExpressRoute circuit, the circuit is in the following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="11a82-159">Het circuit wordt gewijzigd in de volgende status wanneer de connectiviteitsprovider wordt deze voor u inschakelen:</span><span class="sxs-lookup"><span data-stu-id="11a82-159">The circuit changes to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="11a82-160">Voordat u kunt een ExpressRoute-circuit gebruiken, moet deze de status van de volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="11a82-160">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="11a82-161">6. Controleer regelmatig de status en de status van de sleutel van het circuit</span><span class="sxs-lookup"><span data-stu-id="11a82-161">6. Periodically check the status and the state of the circuit key</span></span>

<span data-ttu-id="11a82-162">Controleren of de status en de status van de sleutel van het circuit, laat u weten wanneer uw provider uw circuit is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="11a82-162">Checking the status and the state of the circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="11a82-163">Nadat het circuit is geconfigureerd, is 'ServiceProviderProvisioningState' wordt weergegeven als 'Ingericht', zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11a82-163">After the circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in the following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="11a82-164">Het antwoord is vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11a82-164">The response is similar to the following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="11a82-165">7. Maken van uw configuratie van de routering</span><span class="sxs-lookup"><span data-stu-id="11a82-165">7. Create your routing configuration</span></span>

<span data-ttu-id="11a82-166">Zie voor stapsgewijze instructies de [ExpressRoute-circuit routeringsconfiguratie](howto-routing-cli.md) artikel maken en wijzigen van circuit peerings.</span><span class="sxs-lookup"><span data-stu-id="11a82-166">For step-by-step instructions, see the [ExpressRoute circuit routing configuration](howto-routing-cli.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11a82-167">Deze instructies zijn alleen van toepassing op circuits die zijn gemaakt met serviceproviders die services op laag 2-connectiviteit aanbieden.</span><span class="sxs-lookup"><span data-stu-id="11a82-167">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="11a82-168">Als u een serviceprovider die beheerde laag-3-services (meestal een IP VPN, zoals MPLS), uw connectiviteitsprovider configureert en beheert routering voor u.</span><span class="sxs-lookup"><span data-stu-id="11a82-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="11a82-169">8. Een virtueel netwerk koppelen aan een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="11a82-169">8. Link a virtual network to an ExpressRoute circuit</span></span>

<span data-ttu-id="11a82-170">Vervolgens moet u een virtueel netwerk koppelen aan uw ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="11a82-170">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="11a82-171">Gebruik de [virtuele netwerken koppelen aan ExpressRoute-circuits](howto-linkvnet-cli.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="11a82-171">Use the [Linking virtual networks to ExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="11a82-172"><a name="modify"></a>Wijzigen van een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="11a82-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="11a82-173">U kunt bepaalde eigenschappen van een ExpressRoute-circuit wijzigen zonder enige impact op connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="11a82-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="11a82-174">U kunt de volgende wijzigingen zonder uitvaltijd aanbrengen:</span><span class="sxs-lookup"><span data-stu-id="11a82-174">You can make the following changes with no downtime:</span></span>

* <span data-ttu-id="11a82-175">U kunt in- of uitschakelen van een ExpressRoute premium-invoegtoepassing voor ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="11a82-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="11a82-176">U kunt de bandbreedte van uw ExpressRoute-circuit vergroten, mits er capaciteit beschikbaar is op de poort.</span><span class="sxs-lookup"><span data-stu-id="11a82-176">You can increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="11a82-177">Echter, de bandbreedte van een circuit downgraden wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="11a82-177">However, downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="11a82-178">U kunt het plan softwarelicentiecontrole uit Datalimiet gegevens wijzigen in onbeperkte gegevens.</span><span class="sxs-lookup"><span data-stu-id="11a82-178">You can change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="11a82-179">Echter, het softwarelicentiecontrole plan wijzigen van onbeperkt in Datalimiet gegevens wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="11a82-179">However, changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="11a82-180">U kunt inschakelen en uitschakelen *klassieke bewerkingen toestaan*.</span><span class="sxs-lookup"><span data-stu-id="11a82-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="11a82-181">Zie voor meer informatie over limieten en beperkingen de [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="11a82-181">For more information on limits and limitations, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="11a82-182">De invoegtoepassing ExpressRoute premium inschakelen</span><span class="sxs-lookup"><span data-stu-id="11a82-182">To enable the ExpressRoute premium add-on</span></span>

<span data-ttu-id="11a82-183">U kunt de invoegtoepassing ExpressRoute premium inschakelen voor uw bestaande circuit met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="11a82-183">You can enable the ExpressRoute premium add-on for your existing circuit by using the following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="11a82-184">Het circuit heeft nu de ExpressRoute premium-invoegtoepassing voor functies ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="11a82-184">The circuit now has the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="11a82-185">We beginnen facturering voor de premium-invoegtoepassing mogelijkheid zodra de opdracht met succes is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="11a82-185">We begin billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="11a82-186">De invoegtoepassing ExpressRoute premium uitschakelen</span><span class="sxs-lookup"><span data-stu-id="11a82-186">To disable the ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11a82-187">Deze bewerking kan mislukken als u resources die groter zijn dan wat voor het standaard circuit is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="11a82-187">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

<span data-ttu-id="11a82-188">Voordat u de invoegtoepassing ExpressRoute premium uitschakelt, inzicht in de volgende criteria:</span><span class="sxs-lookup"><span data-stu-id="11a82-188">Before disabling the ExpressRoute premium add-on, understand the following criteria:</span></span>

* <span data-ttu-id="11a82-189">Voordat u van premium op standaard downgraden, moet u ervoor zorgen dat er minder dan 10 virtuele netwerken die zijn gekoppeld aan het circuit.</span><span class="sxs-lookup"><span data-stu-id="11a82-189">Before you downgrade from premium to standard, you must make sure that you have fewer than 10 virtual networks linked to the circuit.</span></span> <span data-ttu-id="11a82-190">Als u meer dan 10 hebt, uw aanvraag bijwerken mislukt en er kosten in rekening brengen volgens de premietarieven voor.</span><span class="sxs-lookup"><span data-stu-id="11a82-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="11a82-191">U moet alle virtuele netwerken in andere geopolitieke regio's ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="11a82-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="11a82-192">Als u niet alle virtuele netwerken ontkoppelt, mislukt de updateaanvraag en we u volgens de premietarieven voor rekening.</span><span class="sxs-lookup"><span data-stu-id="11a82-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="11a82-193">De routetabel moet minder dan 4000 routes voor persoonlijke peering.</span><span class="sxs-lookup"><span data-stu-id="11a82-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="11a82-194">Als uw tabel route groter dan 4000 routes is, wordt de BGP-sessie verwijderd.</span><span class="sxs-lookup"><span data-stu-id="11a82-194">If your route table size is greater than 4,000 routes, the BGP session drops.</span></span> <span data-ttu-id="11a82-195">De sessie won't totdat het aantal geadverteerde voorvoegsels lager dan 4000 is worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="11a82-195">The session won't be reenabled until the number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="11a82-196">U kunt de invoegtoepassing ExpressRoute premium voor een bestaand circuit uitschakelen met behulp van het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11a82-196">You can disable the ExpressRoute premium add-on for the existing circuit by using the following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="11a82-197">Bijwerken van de bandbreedte van het ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="11a82-197">To update the ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="11a82-198">Raadpleeg voor de ondersteunde bandbreedte-opties voor uw provider de [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="11a82-198">For the supported bandwidth options for your provider, check the [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="11a82-199">U kunt de grootte die groter zijn dan de grootte van uw bestaande circuit verzamelen.</span><span class="sxs-lookup"><span data-stu-id="11a82-199">You can pick any size greater than the size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11a82-200">Als er onvoldoende capaciteit op de bestaande poort, moet u wellicht opnieuw maken van het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="11a82-200">If there is inadequate capacity on the existing port, you may have to recreate the ExpressRoute circuit.</span></span> <span data-ttu-id="11a82-201">U kunt het circuit niet upgraden als er geen extra capaciteit beschikbaar is op die locatie.</span><span class="sxs-lookup"><span data-stu-id="11a82-201">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="11a82-202">U kunt de bandbreedte van een ExpressRoute-circuit zonder onderbreking niet reduceren.</span><span class="sxs-lookup"><span data-stu-id="11a82-202">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="11a82-203">Downgraden bandbreedte, moet u het ExpressRoute-circuit inrichting ervan ongedaan en vervolgens opnieuw inrichten van nieuwe ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="11a82-203">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="11a82-204">Nadat u de grootte die u nodig hebt, gebruik de volgende opdracht om het formaat van uw circuit te bepalen:</span><span class="sxs-lookup"><span data-stu-id="11a82-204">After you decide the size you need, use the following command to resize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="11a82-205">Uw circuit wordt aangepast om aan de kant van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="11a82-205">Your circuit is sized up on the Microsoft side.</span></span> <span data-ttu-id="11a82-206">U kunt vervolgens moet contact op met uw connectiviteitsprovider om bij te werken-configuraties van hun kant overeenkomen met deze wijziging.</span><span class="sxs-lookup"><span data-stu-id="11a82-206">Next, you must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="11a82-207">Nadat u deze melding, beginnen wij u voor de optie bijgewerkte bandbreedte facturering.</span><span class="sxs-lookup"><span data-stu-id="11a82-207">After you make this notification, we begin billing you for the updated bandwidth option.</span></span>

### <a name="to-move-the-sku-from-metered-to-unlimited"></a><span data-ttu-id="11a82-208">Als u wilt verplaatsen van de SKU van datalimiet op onbeperkt</span><span class="sxs-lookup"><span data-stu-id="11a82-208">To move the SKU from metered to unlimited</span></span>

<span data-ttu-id="11a82-209">U kunt de SKU van een ExpressRoute-circuit wijzigen met behulp van het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11a82-209">You can change the SKU of an ExpressRoute circuit by using the following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="to-control-access-to-the-classic-and-resource-manager-environments"></a><span data-ttu-id="11a82-210">Toegang tot het klassieke en het Resource Manager-omgevingen</span><span class="sxs-lookup"><span data-stu-id="11a82-210">To control access to the classic and Resource Manager environments</span></span>

<span data-ttu-id="11a82-211">Lees de instructies in [verplaatsen ExpressRoute-circuits van het klassieke naar het Resource Manager-implementatiemodel](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="11a82-211">Review the instructions in [Move ExpressRoute circuits from the classic to the Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="11a82-212">Opheffen van inrichting en een ExpressRoute-circuit verwijderen</span><span class="sxs-lookup"><span data-stu-id="11a82-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="11a82-213">Voor inrichting ervan ongedaan maakt en een ExpressRoute-circuit verwijderen, moet dat u weten dat de volgende criteria:</span><span class="sxs-lookup"><span data-stu-id="11a82-213">To deprovision and delete an ExpressRoute circuit, make sure you understand the following criteria:</span></span>

* <span data-ttu-id="11a82-214">U moet alle virtuele netwerken van het ExpressRoute-circuit ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="11a82-214">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="11a82-215">Als deze bewerking is mislukt, controleert u of er geen virtuele netwerken zijn gekoppeld aan het circuit.</span><span class="sxs-lookup"><span data-stu-id="11a82-215">If this operation fails, check to see if any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="11a82-216">Als de ExpressRoute-circuit serviceprovider Inrichtingsstatus **inrichten** of **ingericht**, moet u werken met uw serviceprovider voor inrichting ervan ongedaan maakt het circuit op hun kant.</span><span class="sxs-lookup"><span data-stu-id="11a82-216">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="11a82-217">We blijven resources reserveren en u in rekening brengen totdat de serviceprovider is voltooid opheffen van inrichting het circuit en waarschuwt ons.</span><span class="sxs-lookup"><span data-stu-id="11a82-217">We continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="11a82-218">Als de provider heeft het circuit deprovisioned, kunt u het circuit verwijderen.</span><span class="sxs-lookup"><span data-stu-id="11a82-218">You can delete the circuit if the service provider has deprovisioned the circuit.</span></span> <span data-ttu-id="11a82-219">Wanneer een circuit is gemaakt, de serviceprovider Inrichtingsstatus is ingesteld op **niet ingericht**.</span><span class="sxs-lookup"><span data-stu-id="11a82-219">When a circuit is deprovisioned, the service provider provisioning state is set to **Not provisioned**.</span></span> <span data-ttu-id="11a82-220">Hierdoor wordt voorkomen dat facturering voor het circuit.</span><span class="sxs-lookup"><span data-stu-id="11a82-220">This stops billing for the circuit.</span></span>

<span data-ttu-id="11a82-221">U kunt uw ExpressRoute-circuit verwijderen door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="11a82-221">You can delete your ExpressRoute circuit by running the following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="11a82-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11a82-222">Next steps</span></span>

<span data-ttu-id="11a82-223">Nadat u het circuit hebt gemaakt, zorg er dan voor dat u de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="11a82-223">After you create your circuit, make sure that you do the following tasks:</span></span>

* [<span data-ttu-id="11a82-224">Maken en aanpassen van routering voor ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="11a82-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="11a82-225">Het virtuele netwerk koppelen aan uw ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="11a82-225">Link your virtual network to your ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)