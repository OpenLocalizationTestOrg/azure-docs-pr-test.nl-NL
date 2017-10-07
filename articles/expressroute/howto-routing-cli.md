---
title: 'Hoe tooconfigure routering voor een Azure ExpressRoute-circuit: CLI | Microsoft Docs'
description: In dit artikel helpt u bij het maken en inrichten Hallo persoonlijke, openbare en Microsoft-peering van een ExpressRoute-circuit. Dit artikel leest u hoe de status van toocheck hello, bijwerken of verwijderen van peerings voor uw circuit.
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
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="78834-104">Maken en aanpassen van routering voor een ExpressRoute-circuit met CLI</span><span class="sxs-lookup"><span data-stu-id="78834-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="78834-105">In dit artikel helpt u bij het maken en beheren van routeringsconfiguratie voor een ExpressRoute-circuit in Hallo Resource Manager-implementatiemodel met CLI.</span><span class="sxs-lookup"><span data-stu-id="78834-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="78834-106">U kunt ook controleren Hallo status, update of delete en inrichting ervan ongedaan peerings voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="78834-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="78834-107">Als u wilt dat een andere methode toowork toouse met uw circuit, selecteert u een artikel in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="78834-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="78834-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="78834-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="78834-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="78834-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="78834-110">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="78834-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="78834-111">Video - persoonlijke peering</span><span class="sxs-lookup"><span data-stu-id="78834-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="78834-112">Video - openbare peering</span><span class="sxs-lookup"><span data-stu-id="78834-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="78834-113">Video - Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="78834-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="78834-114">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="78834-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="78834-115">Configuratievereisten</span><span class="sxs-lookup"><span data-stu-id="78834-115">Configuration prerequisites</span></span>

* <span data-ttu-id="78834-116">Installeer de nieuwste versie van de Hallo van Hallo CLI-opdrachten (2.0 of hoger) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="78834-116">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="78834-117">Zie voor meer informatie over het installeren van de CLI-opdrachten Hallo [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="78834-117">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="78834-118">Zorg ervoor dat u Hallo hebt bekeken [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstroom](expressroute-workflows.md) voordat u begint met de configuratie-pagina's.</span><span class="sxs-lookup"><span data-stu-id="78834-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="78834-119">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="78834-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="78834-120">Hallo-instructies te volgen[maken van een ExpressRoute-circuit](howto-circuit-cli.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="78834-120">Follow hello instructions too[Create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="78834-121">Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld voor u toobe kunnen toorun Hallo opdrachten in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="78834-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello commands in this article.</span></span>

<span data-ttu-id="78834-122">Deze instructies zijn alleen van toepassing toocircuits gemaakt met serviceproviders die services voor Layer 2-connectiviteit aanbieden.</span><span class="sxs-lookup"><span data-stu-id="78834-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="78834-123">Als u gebruikmaakt van een serviceprovider die beheerde laag-3-services (meestal een IPVPN, zoals MPLS), uw connectiviteitsprovider configureren en beheren van routering voor u.</span><span class="sxs-lookup"><span data-stu-id="78834-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="78834-124">U kunt een, twee of alle drie de peerings (Azure privé, Azure openbaar en Microsoft) voor een ExpressRoute-circuit configureren.</span><span class="sxs-lookup"><span data-stu-id="78834-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="78834-125">U kunt peerings configureren in elke gewenste volgorde.</span><span class="sxs-lookup"><span data-stu-id="78834-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="78834-126">Echter, moet u ervoor zorgen dat Hallo configuratie van elke peering een tegelijk te voltooien.</span><span class="sxs-lookup"><span data-stu-id="78834-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="78834-127">Persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="78834-127">Azure private peering</span></span>

<span data-ttu-id="78834-128">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van persoonlijke peering voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="78834-128">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="78834-129">toocreate persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="78834-129">toocreate Azure private peering</span></span>

1. <span data-ttu-id="78834-130">Hallo meest recente versie van Azure CLI installeren.</span><span class="sxs-lookup"><span data-stu-id="78834-130">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="78834-131">Moet u de meest recente versie Hallo van hello Azure-opdrachtregelinterface (CLI). * revisie Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="78834-131">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="78834-132">Hallo-abonnement u wilt dat de ExpressRoute-circuit toocreate selecteren</span><span class="sxs-lookup"><span data-stu-id="78834-132">Select hello subscription you want toocreate ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="78834-133">Maak een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="78834-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="78834-134">Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](howto-circuit-cli.md) en laat het inrichten door de connectiviteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="78834-134">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="78834-135">Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen.</span><span class="sxs-lookup"><span data-stu-id="78834-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="78834-136">In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo.</span><span class="sxs-lookup"><span data-stu-id="78834-136">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="78834-137">Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert, maar de configuratie met behulp van de volgende stappen Hallo blijven.</span><span class="sxs-lookup"><span data-stu-id="78834-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="78834-138">Controleer de ExpressRoute-circuit toomake Hallo is ingericht en ook ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="78834-138">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="78834-139">Gebruik Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-139">Use hello following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="78834-140">Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-140">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="78834-141">Configureer persoonlijke Azure-peering voor Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="78834-141">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="78834-142">Zorg ervoor dat u de volgende items voordat u met de volgende stappen Hallo verdergaat Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="78834-142">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="78834-143">Een/30 subnet voor de primaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="78834-143">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="78834-144">Hallo-subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.</span><span class="sxs-lookup"><span data-stu-id="78834-144">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="78834-145">Een/30 subnet voor de secundaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="78834-145">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="78834-146">Hallo-subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.</span><span class="sxs-lookup"><span data-stu-id="78834-146">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="78834-147">Een geldige VLAN-ID tooestablish deze peering.</span><span class="sxs-lookup"><span data-stu-id="78834-147">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="78834-148">Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="78834-148">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="78834-149">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="78834-149">AS number for peering.</span></span> <span data-ttu-id="78834-150">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="78834-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="78834-151">U kunt een persoonlijk AS-nummer voor deze peering gebruiken.</span><span class="sxs-lookup"><span data-stu-id="78834-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="78834-152">Zorg dat u niet 65515 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="78834-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="78834-153">**Optionele -** een MD5-hash, als u ervoor toouse een kiest.</span><span class="sxs-lookup"><span data-stu-id="78834-153">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="78834-154">Gebruik Hallo voorbeeld tooconfigure Azure persoonlijke peering voor uw circuit te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-154">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="78834-155">Als u een MD5-hash toouse kiest, gebruikt u Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-155">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="78834-156">Zorg dat u uw AS-nummer als peering-ASN opgeeft, niet als klant-ASN.</span><span class="sxs-lookup"><span data-stu-id="78834-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="78834-157">tooview Azure persoonlijke peering details</span><span class="sxs-lookup"><span data-stu-id="78834-157">tooview Azure private peering details</span></span>

<span data-ttu-id="78834-158">U kunt configuratie-informatie krijgen met behulp van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-158">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="78834-159">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="78834-159">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="78834-160">tooupdate Azure configuratie van persoonlijke peering</span><span class="sxs-lookup"><span data-stu-id="78834-160">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="78834-161">U kunt elk deel van Hallo-configuratie met behulp van de volgende voorbeeld Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="78834-161">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="78834-162">In dit voorbeeld wordt Hallo VLAN-ID van het circuit Hallo van 100 too500 bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="78834-162">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="78834-163">toodelete persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="78834-163">toodelete Azure private peering</span></span>

<span data-ttu-id="78834-164">U kunt de peeringconfiguratie verwijderen door het uitvoeren van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-164">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="78834-165">U moet ervoor zorgen dat alle virtuele netwerken losgekoppeld van Hallo ExpressRoute-circuit zijn voordat u dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="78834-165">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="78834-166">Openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="78834-166">Azure public peering</span></span>

<span data-ttu-id="78834-167">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van openbare peering voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="78834-167">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="78834-168">toocreate openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="78834-168">toocreate Azure public peering</span></span>

1. <span data-ttu-id="78834-169">Hallo meest recente versie van Azure CLI installeren.</span><span class="sxs-lookup"><span data-stu-id="78834-169">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="78834-170">Moet u de meest recente versie Hallo van hello Azure-opdrachtregelinterface (CLI). * revisie Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="78834-170">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="78834-171">Hallo-abonnement waarvoor u toocreate ExpressRoute-circuit wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="78834-171">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="78834-172">Maak een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="78834-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="78834-173">Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](howto-circuit-cli.md) en laat het inrichten door de connectiviteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="78834-173">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="78834-174">Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u aanvragen dat uw connectiviteitsprovider mogelijk persoonlijke Azure-peering voor u maakt.</span><span class="sxs-lookup"><span data-stu-id="78834-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="78834-175">In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo.</span><span class="sxs-lookup"><span data-stu-id="78834-175">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="78834-176">Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert, maar de configuratie met behulp van de volgende stappen Hallo blijven.</span><span class="sxs-lookup"><span data-stu-id="78834-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="78834-177">Controleer Hallo ExpressRoute-circuit tooensure is ingericht en ook ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="78834-177">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="78834-178">Gebruik Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-178">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="78834-179">Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-179">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="78834-180">Configureer openbare Azure-peering voor Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="78834-180">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="78834-181">Zorg ervoor dat u de volgende informatie voordat u verder Hallo hebt.</span><span class="sxs-lookup"><span data-stu-id="78834-181">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="78834-182">Een/30 subnet voor de primaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="78834-182">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="78834-183">Dit moet een geldig openbaar IPv4-voorvoegsel zijn.</span><span class="sxs-lookup"><span data-stu-id="78834-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="78834-184">Een/30 subnet voor de secundaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="78834-184">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="78834-185">Dit moet een geldig openbaar IPv4-voorvoegsel zijn.</span><span class="sxs-lookup"><span data-stu-id="78834-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="78834-186">Een geldige VLAN-ID tooestablish deze peering.</span><span class="sxs-lookup"><span data-stu-id="78834-186">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="78834-187">Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="78834-187">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="78834-188">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="78834-188">AS number for peering.</span></span> <span data-ttu-id="78834-189">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="78834-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="78834-190">**Optionele -** een MD5-hash, als u ervoor toouse een kiest.</span><span class="sxs-lookup"><span data-stu-id="78834-190">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="78834-191">Voer Hallo voorbeeld tooconfigure Azure openbare peering voor uw circuit te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-191">Run hello following example tooconfigure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="78834-192">Als u een MD5-hash toouse kiest, gebruikt u Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-192">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="78834-193">Zorg dat u uw AS-nummer als peering-ASN opgeeft, niet als klant-ASN.</span><span class="sxs-lookup"><span data-stu-id="78834-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="78834-194">tooview Azure openbare peering details</span><span class="sxs-lookup"><span data-stu-id="78834-194">tooview Azure public peering details</span></span>

<span data-ttu-id="78834-195">U kunt krijgen configuratiegegevens wilt weergeven Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-195">You can get configuration details using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="78834-196">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="78834-196">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="78834-197">configuratie van openbare peering Azure tooupdate</span><span class="sxs-lookup"><span data-stu-id="78834-197">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="78834-198">U kunt elk deel van Hallo-configuratie met behulp van de volgende voorbeeld Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="78834-198">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="78834-199">In dit voorbeeld wordt Hallo VLAN-ID van het circuit Hallo van 200 too600 bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="78834-199">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="78834-200">toodelete openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="78834-200">toodelete Azure public peering</span></span>

<span data-ttu-id="78834-201">U kunt de peeringconfiguratie verwijderen door het uitvoeren van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-201">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="78834-202">Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="78834-202">Microsoft peering</span></span>

<span data-ttu-id="78834-203">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen configuratie Hallo Microsoft-peering gebruiken voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="78834-203">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78834-204">Eerdere tooAugust 1 Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, 2017 hebben alle service voorvoegsels die worden geadverteerd via Hallo Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="78834-204">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="78834-205">Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter wordt aangesloten toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="78834-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="78834-206">Zie voor meer informatie [configureren van een routefilter voor Microsoft-peering](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="78834-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="78834-207">toocreate Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="78834-207">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="78834-208">Hallo meest recente versie van Azure CLI installeren.</span><span class="sxs-lookup"><span data-stu-id="78834-208">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="78834-209">Gebruik Hallo meest recente versie van Azure-opdrachtregelinterface (CLI) Hallo. * revisie Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="78834-209">Use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="78834-210">Hallo-abonnement waarvoor u toocreate ExpressRoute-circuit wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="78834-210">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="78834-211">Maak een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="78834-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="78834-212">Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](howto-circuit-cli.md) en laat het inrichten door de connectiviteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="78834-212">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="78834-213">Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen.</span><span class="sxs-lookup"><span data-stu-id="78834-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="78834-214">In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo.</span><span class="sxs-lookup"><span data-stu-id="78834-214">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="78834-215">Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert, maar de configuratie met behulp van de volgende stappen Hallo blijven.</span><span class="sxs-lookup"><span data-stu-id="78834-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>

3. <span data-ttu-id="78834-216">Controleer de ExpressRoute-circuit toomake Hallo is ingericht en ook ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="78834-216">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="78834-217">Gebruik Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-217">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="78834-218">Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-218">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="78834-219">Configureer Microsoft-peering voor Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="78834-219">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="78834-220">Zorg ervoor dat er Hallo volgende informatie voordat u verder.</span><span class="sxs-lookup"><span data-stu-id="78834-220">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="78834-221">Een/30 subnet voor de primaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="78834-221">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="78834-222">Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="78834-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="78834-223">Een/30 subnet voor de secundaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="78834-223">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="78834-224">Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="78834-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="78834-225">Een geldige VLAN-ID tooestablish deze peering.</span><span class="sxs-lookup"><span data-stu-id="78834-225">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="78834-226">Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="78834-226">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="78834-227">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="78834-227">AS number for peering.</span></span> <span data-ttu-id="78834-228">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="78834-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="78834-229">Geadverteerde voorvoegsels: U moet een lijst verstrekken van alle voorvoegsels die u van plan bent tooadvertise via Hallo BGP-sessie.</span><span class="sxs-lookup"><span data-stu-id="78834-229">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="78834-230">Alleen openbare IP-adresvoorvoegsels worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="78834-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="78834-231">Als u een reeks voorvoegsels toosend plant, kunt u een door komma's gescheiden lijst verzenden.</span><span class="sxs-lookup"><span data-stu-id="78834-231">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="78834-232">Deze voorvoegsels moeten geregistreerde tooyou in een RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="78834-232">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="78834-233">**Optionele -** klant-ASN: als u voorvoegsels adverteert die niet zijn ingeschreven toohello peering als getal, kunt u Hallo opgeven als getal toowhich ze zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="78834-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="78834-234">Naam van Routeringsregister: Kunt u Hallo RIR / IRR met betrekking tot welke Hallo als number en prefixes zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="78834-234">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="78834-235">**Optionele -** een MD5-hash, als u ervoor toouse een kiest.</span><span class="sxs-lookup"><span data-stu-id="78834-235">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="78834-236">Voer Hallo voorbeeld tooconfigure Microsoft-peering voor uw circuit te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-236">Run hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="78834-237">details van tooget Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="78834-237">tooget Microsoft peering details</span></span>

<span data-ttu-id="78834-238">U kunt configuratie-informatie krijgen met behulp van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-238">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="78834-239">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="78834-239">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="78834-240">configuratie van tooupdate Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="78834-240">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="78834-241">U kunt elk deel van Hallo configuratie bijwerken.</span><span class="sxs-lookup"><span data-stu-id="78834-241">You can update any part of hello configuration.</span></span> <span data-ttu-id="78834-242">Hallo geadverteerde voorvoegsels van Hallo circuit vanuit 123.1.0.0/24 too124.1.0.0/24 in het volgende voorbeeld Hallo worden bijgewerkt:</span><span class="sxs-lookup"><span data-stu-id="78834-242">hello advertised prefixes of hello circuit are being updated from 123.1.0.0/24 too124.1.0.0/24 in hello following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="78834-243">toodelete Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="78834-243">toodelete Microsoft peering</span></span>

<span data-ttu-id="78834-244">U kunt de peeringconfiguratie verwijderen door het uitvoeren van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="78834-244">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="78834-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="78834-245">Next steps</span></span>

<span data-ttu-id="78834-246">Volgende stap, [koppelen van een VNet tooan ExpressRoute-circuit](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="78834-246">Next step, [Link a VNet tooan ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="78834-247">Voor meer informatie over ExpressRoute-werkstromen raadpleegt u [ExpressRoute workflows](expressroute-workflows.md) (ExpressRoute-werkstromen).</span><span class="sxs-lookup"><span data-stu-id="78834-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="78834-248">Voor meer informatie over circuitpeering raadpleegt u [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (ExpressRoute-circuits en -routeringsdomeinen).</span><span class="sxs-lookup"><span data-stu-id="78834-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="78834-249">Bekijk het [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Virtual Network-overzicht) voor meer informatie over het gebruik van virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="78834-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>