---
title: 'Hoe tooconfigure routering (peering) voor een ExpressRoute-circuit: Resource Manager: Azure | Microsoft Docs'
description: Dit artikel begeleidt u bij Hallo stappen voor het maken en inrichten Hallo persoonlijke, openbare en Microsoft-peering van een ExpressRoute-circuit. Dit artikel leest u hoe de status van toocheck hello, bijwerken of verwijderen van peerings voor uw circuit.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="fa68b-104">Maken en wijzigen van de peering voor een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="fa68b-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="fa68b-105">In dit artikel helpt u bij het maken en beheren van routeringsconfiguratie voor een ExpressRoute-circuit in Hallo Resource Manager-implementatiemodel met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fa68b-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using hello Azure portal.</span></span> <span data-ttu-id="fa68b-106">U kunt ook controleren Hallo status, update of delete en inrichting ervan ongedaan peerings voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="fa68b-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="fa68b-107">Als u wilt dat een andere methode toowork toouse met uw circuit, selecteert u een artikel in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="fa68b-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="fa68b-108">Configuratievereisten</span><span class="sxs-lookup"><span data-stu-id="fa68b-108">Configuration prerequisites</span></span>

* <span data-ttu-id="fa68b-109">Zorg ervoor dat u Hallo hebt bekeken [vereisten](expressroute-prerequisites.md) pagina hello [routeringsvereisten](expressroute-routing.md) pagina en Hallo [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="fa68b-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="fa68b-110">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="fa68b-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="fa68b-111">Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-portal-resource-manager.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="fa68b-111">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="fa68b-112">Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld voor u toobe kunnen toorun Hallo cmdlets in de volgende secties Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa68b-112">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in hello next sections.</span></span>
* <span data-ttu-id="fa68b-113">Als u van plan toouse een gedeelde sleutel/MD5-hash bent, worden toouse ervoor dat dit aan beide zijden van Hallo tunnel- en limit Hallo aantal tekens tooa maximaal 25.</span><span class="sxs-lookup"><span data-stu-id="fa68b-113">If you plan toouse a shared key/MD5 hash, be sure toouse this on both sides of hello tunnel and limit hello number of characters tooa maximum of 25.</span></span>

<span data-ttu-id="fa68b-114">Deze instructies zijn alleen van toepassing toocircuits gemaakt met serviceproviders die services voor Layer 2-connectiviteit aanbieden.</span><span class="sxs-lookup"><span data-stu-id="fa68b-114">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="fa68b-115">Als u gebruikmaakt van een serviceprovider die beheerde laag-3-services (meestal een IPVPN, zoals MPLS), uw connectiviteitsprovider configureert en beheert routering voor u.</span><span class="sxs-lookup"><span data-stu-id="fa68b-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="fa68b-116">We momenteel doen nog geen peerings geconfigureerd door serviceproviders via Hallo service management portal.</span><span class="sxs-lookup"><span data-stu-id="fa68b-116">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="fa68b-117">Deze mogelijkheid zal binnenkort worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="fa68b-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="fa68b-118">Neem contact op met uw serviceprovider voordat u BGP-peerings configureert.</span><span class="sxs-lookup"><span data-stu-id="fa68b-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="fa68b-119">U kunt een, twee of alle drie de peerings (Azure privé, Azure openbaar en Microsoft) voor een ExpressRoute-circuit configureren.</span><span class="sxs-lookup"><span data-stu-id="fa68b-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="fa68b-120">U kunt peerings configureren in elke gewenste volgorde.</span><span class="sxs-lookup"><span data-stu-id="fa68b-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="fa68b-121">Echter, moet u ervoor zorgen dat Hallo configuratie van elke peering een tegelijk te voltooien.</span><span class="sxs-lookup"><span data-stu-id="fa68b-121">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="fa68b-122">Persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="fa68b-122">Azure private peering</span></span>

<span data-ttu-id="fa68b-123">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van persoonlijke peering voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="fa68b-123">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="fa68b-124">toocreate persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="fa68b-124">toocreate Azure private peering</span></span>

1. <span data-ttu-id="fa68b-125">Hallo ExpressRoute-circuit configureren.</span><span class="sxs-lookup"><span data-stu-id="fa68b-125">Configure hello ExpressRoute circuit.</span></span> <span data-ttu-id="fa68b-126">Zorg ervoor dat Hallo circuit volledig is ingericht door de connectiviteitsprovider Hallo voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="fa68b-126">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing.</span></span>

  ![lijst](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="fa68b-128">Configureer persoonlijke Azure-peering voor Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="fa68b-128">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="fa68b-129">Zorg ervoor dat u de volgende items voordat u met de volgende stappen Hallo verdergaat Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="fa68b-129">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="fa68b-130">Een/30 subnet voor de primaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa68b-130">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="fa68b-131">Hallo-subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.</span><span class="sxs-lookup"><span data-stu-id="fa68b-131">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="fa68b-132">Een/30 subnet voor de secundaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa68b-132">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="fa68b-133">Hallo-subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.</span><span class="sxs-lookup"><span data-stu-id="fa68b-133">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="fa68b-134">Een geldige VLAN-ID tooestablish deze peering.</span><span class="sxs-lookup"><span data-stu-id="fa68b-134">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="fa68b-135">Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="fa68b-135">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="fa68b-136">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="fa68b-136">AS number for peering.</span></span> <span data-ttu-id="fa68b-137">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa68b-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="fa68b-138">U kunt een persoonlijk AS-nummer voor deze peering gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa68b-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="fa68b-139">Zorg dat u niet 65515 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fa68b-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="fa68b-140">**Optionele -** een MD5-hash, als u ervoor toouse een kiest.</span><span class="sxs-lookup"><span data-stu-id="fa68b-140">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="fa68b-141">Selecteer Hallo persoonlijke Azure rij voor peering, zoals weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="fa68b-141">Select hello Azure Private peering row, as shown in hello following example:</span></span>

  ![Persoonlijke](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="fa68b-143">Configureer persoonlijke Azure-peering.</span><span class="sxs-lookup"><span data-stu-id="fa68b-143">Configure private peering.</span></span> <span data-ttu-id="fa68b-144">Hallo volgende afbeelding toont een configuratievoorbeeld van een:</span><span class="sxs-lookup"><span data-stu-id="fa68b-144">hello following image shows a configuration example:</span></span>

  ![Configureer persoonlijke peering](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="fa68b-146">Hallo-configuratie op te slaan wanneer u alle parameters hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="fa68b-146">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="fa68b-147">Nadat het Hallo-configuratie is geaccepteerd, ziet u iets dergelijks toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa68b-147">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![persoonlijke peering opslaan](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="fa68b-149">tooview Azure persoonlijke peering details</span><span class="sxs-lookup"><span data-stu-id="fa68b-149">tooview Azure private peering details</span></span>

<span data-ttu-id="fa68b-150">U kunt weergeven Hallo eigenschappen van persoonlijke Azure-peering door Hallo peering te selecteren.</span><span class="sxs-lookup"><span data-stu-id="fa68b-150">You can view hello properties of Azure private peering by selecting hello peering.</span></span>

![persoonlijke peering weergeven](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="fa68b-152">tooupdate Azure configuratie van persoonlijke peering</span><span class="sxs-lookup"><span data-stu-id="fa68b-152">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="fa68b-153">U kunt Hallo rij voor peering selecteren en aanpassen van eigenschappen Hallo-peering.</span><span class="sxs-lookup"><span data-stu-id="fa68b-153">You can select hello row for peering and modify hello peering properties.</span></span>

![persoonlijke peering bijwerken](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="fa68b-155">toodelete persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="fa68b-155">toodelete Azure private peering</span></span>

<span data-ttu-id="fa68b-156">U kunt een peeringconfiguratie verwijderen door het verwijderingspictogram Hallo, zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa68b-156">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![persoonlijke peering verwijderen](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="fa68b-158">Openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="fa68b-158">Azure public peering</span></span>

<span data-ttu-id="fa68b-159">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van openbare peering voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="fa68b-159">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="fa68b-160">toocreate openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="fa68b-160">toocreate Azure public peering</span></span>

1. <span data-ttu-id="fa68b-161">Configureer het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="fa68b-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="fa68b-162">Zorg ervoor dat Hallo circuit volledig is ingericht door de connectiviteitsprovider Hallo voordat u verder.</span><span class="sxs-lookup"><span data-stu-id="fa68b-162">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![openbare peering weergeven](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="fa68b-164">Configureer openbare Azure-peering voor Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="fa68b-164">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="fa68b-165">Zorg ervoor dat u de volgende items voordat u met de volgende stappen Hallo verdergaat Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="fa68b-165">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="fa68b-166">Een/30 subnet voor de primaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa68b-166">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="fa68b-167">Dit moet een geldig openbaar IPv4-voorvoegsel zijn.</span><span class="sxs-lookup"><span data-stu-id="fa68b-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="fa68b-168">Een/30 subnet voor de secundaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa68b-168">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="fa68b-169">Dit moet een geldig openbaar IPv4-voorvoegsel zijn.</span><span class="sxs-lookup"><span data-stu-id="fa68b-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="fa68b-170">Een geldige VLAN-ID tooestablish deze peering.</span><span class="sxs-lookup"><span data-stu-id="fa68b-170">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="fa68b-171">Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="fa68b-171">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="fa68b-172">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="fa68b-172">AS number for peering.</span></span> <span data-ttu-id="fa68b-173">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa68b-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="fa68b-174">**Optionele -** een MD5-hash, als u ervoor toouse een kiest.</span><span class="sxs-lookup"><span data-stu-id="fa68b-174">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="fa68b-175">Selecteer hello Azure rij voor openbare peering, zoals wordt weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa68b-175">Select hello Azure public peering row, as shown in hello following image:</span></span>

  ![Selecteer de rij voor openbare peering](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="fa68b-177">Configureer openbare Azure-peering.</span><span class="sxs-lookup"><span data-stu-id="fa68b-177">Configure public peering.</span></span> <span data-ttu-id="fa68b-178">Hallo volgende afbeelding toont een configuratievoorbeeld van een:</span><span class="sxs-lookup"><span data-stu-id="fa68b-178">hello following image shows a configuration example:</span></span>

  ![Configureer openbare peering](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="fa68b-180">Hallo-configuratie op te slaan wanneer u alle parameters hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="fa68b-180">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="fa68b-181">Nadat het Hallo-configuratie is geaccepteerd, ziet u iets dergelijks toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa68b-181">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![Configuratie van openbare peering opslaan](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="fa68b-183">tooview Azure openbare peering details</span><span class="sxs-lookup"><span data-stu-id="fa68b-183">tooview Azure public peering details</span></span>

<span data-ttu-id="fa68b-184">U kunt weergeven Hallo eigenschappen van openbare Azure-peering door Hallo peering te selecteren.</span><span class="sxs-lookup"><span data-stu-id="fa68b-184">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![de eigenschappen van openbare peering weergeven](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="fa68b-186">configuratie van openbare peering Azure tooupdate</span><span class="sxs-lookup"><span data-stu-id="fa68b-186">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="fa68b-187">U kunt Hallo rij voor peering selecteren en aanpassen van eigenschappen Hallo-peering.</span><span class="sxs-lookup"><span data-stu-id="fa68b-187">You can select hello row for peering and modify hello peering properties.</span></span>

![Selecteer de rij voor openbare peering](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="fa68b-189">toodelete openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="fa68b-189">toodelete Azure public peering</span></span>

<span data-ttu-id="fa68b-190">U kunt de peeringconfiguratie verwijderen door het verwijderingspictogram hello, zoals wordt weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="fa68b-190">You can remove your peering configuration by selecting hello delete icon, as shown in hello following example:</span></span>

![openbare peering verwijderen](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="fa68b-192">Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="fa68b-192">Microsoft peering</span></span>

<span data-ttu-id="fa68b-193">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen configuratie Hallo Microsoft-peering gebruiken voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="fa68b-193">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa68b-194">Eerdere tooAugust 1 Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, 2017 hebben alle service voorvoegsels die worden geadverteerd via Hallo Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="fa68b-194">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="fa68b-195">Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter wordt aangesloten toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="fa68b-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="fa68b-196">Zie voor meer informatie [configureren van een routefilter voor Microsoft-peering](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fa68b-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="fa68b-197">toocreate Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="fa68b-197">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="fa68b-198">Configureer het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="fa68b-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="fa68b-199">Zorg ervoor dat Hallo circuit volledig is ingericht door de connectiviteitsprovider Hallo voordat u verder.</span><span class="sxs-lookup"><span data-stu-id="fa68b-199">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![Microsoft-peering weergeven](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="fa68b-201">Configureer Microsoft-peering voor Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="fa68b-201">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="fa68b-202">Zorg ervoor dat er Hallo volgende informatie voordat u verder.</span><span class="sxs-lookup"><span data-stu-id="fa68b-202">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="fa68b-203">Een/30 subnet voor de primaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa68b-203">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="fa68b-204">Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="fa68b-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="fa68b-205">Een/30 subnet voor de secundaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa68b-205">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="fa68b-206">Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="fa68b-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="fa68b-207">Een geldige VLAN-ID tooestablish deze peering.</span><span class="sxs-lookup"><span data-stu-id="fa68b-207">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="fa68b-208">Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="fa68b-208">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="fa68b-209">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="fa68b-209">AS number for peering.</span></span> <span data-ttu-id="fa68b-210">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa68b-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="fa68b-211">Geadverteerde voorvoegsels: U moet een lijst verstrekken van alle voorvoegsels die u van plan bent tooadvertise via Hallo BGP-sessie.</span><span class="sxs-lookup"><span data-stu-id="fa68b-211">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="fa68b-212">Alleen openbare IP-adresvoorvoegsels worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="fa68b-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="fa68b-213">Als u een reeks voorvoegsels toosend plant, kunt u een door komma's gescheiden lijst verzenden.</span><span class="sxs-lookup"><span data-stu-id="fa68b-213">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="fa68b-214">Deze voorvoegsels moeten geregistreerde tooyou in een RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="fa68b-214">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="fa68b-215">**Optionele -** klant-ASN: als u voorvoegsels adverteert die niet zijn ingeschreven toohello peering als getal, kunt u Hallo opgeven als getal toowhich ze zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="fa68b-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="fa68b-216">Naam van Routeringsregister: Kunt u Hallo RIR / IRR met betrekking tot welke Hallo als number en prefixes zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="fa68b-216">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="fa68b-217">**Optionele -** een MD5-hash, als u ervoor toouse een kiest.</span><span class="sxs-lookup"><span data-stu-id="fa68b-217">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="fa68b-218">U kunt selecteren Hallo peering tooconfigure gewenst, zoals wordt weergegeven in de volgende Hallo voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="fa68b-218">You can select hello peering you wish tooconfigure, as shown in hello following example.</span></span> <span data-ttu-id="fa68b-219">Selecteer Hallo rij voor Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="fa68b-219">Select hello Microsoft peering row.</span></span>

  ![Selecteer de rij voor Microsoft-peering](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="fa68b-221">Configureer Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="fa68b-221">Configure Microsoft peering.</span></span> <span data-ttu-id="fa68b-222">Hallo volgende afbeelding toont een configuratievoorbeeld van een:</span><span class="sxs-lookup"><span data-stu-id="fa68b-222">hello following image shows a configuration example:</span></span>

  ![Configureer Microsoft-peering](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="fa68b-224">Hallo-configuratie op te slaan wanneer u alle parameters hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="fa68b-224">Save hello configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="fa68b-225">Als het circuit tooa 'Validatie nodig' status (zoals in afbeelding Hallo), moet u een bewijs van eigendom van Hallo voorvoegsels tooour ondersteuningsteam ondersteuning ticket tooshow openen.</span><span class="sxs-lookup"><span data-stu-id="fa68b-225">If your circuit gets tooa 'Validation needed' state (as shown in hello image), you must open a support ticket tooshow proof of ownership of hello prefixes tooour support team.</span></span>

  ![Microsoft-peeringconfiguratie opslaan](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="fa68b-227">U kunt een ondersteuningsticket openen rechtstreeks vanuit de portal hello, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa68b-227">You can open a support ticket directly from hello portal, as shown in hello following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="fa68b-228">Nadat het Hallo-configuratie is geaccepteerd, ziet u iets dergelijks toohello installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa68b-228">After hello configuration has been accepted successfully, you see something similar toohello following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="fa68b-229">details van tooview Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="fa68b-229">tooview Microsoft peering details</span></span>

<span data-ttu-id="fa68b-230">U kunt weergeven Hallo eigenschappen van openbare Azure-peering door Hallo peering te selecteren.</span><span class="sxs-lookup"><span data-stu-id="fa68b-230">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="fa68b-231">configuratie van tooupdate Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="fa68b-231">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="fa68b-232">U kunt Hallo rij voor peering selecteren en aanpassen van eigenschappen Hallo-peering.</span><span class="sxs-lookup"><span data-stu-id="fa68b-232">You can select hello row for peering and modify hello peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="fa68b-233">toodelete Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="fa68b-233">toodelete Microsoft peering</span></span>

<span data-ttu-id="fa68b-234">U kunt een peeringconfiguratie verwijderen door het verwijderingspictogram Hallo, zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa68b-234">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="fa68b-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fa68b-235">Next steps</span></span>

<span data-ttu-id="fa68b-236">Volgende stap, [koppelen van een VNet tooan ExpressRoute-circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="fa68b-236">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="fa68b-237">Voor meer informatie over ExpressRoute-werkstromen raadpleegt u [ExpressRoute workflows](expressroute-workflows.md) (ExpressRoute-werkstromen).</span><span class="sxs-lookup"><span data-stu-id="fa68b-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="fa68b-238">Voor meer informatie over circuitpeering raadpleegt u [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (ExpressRoute-circuits en -routeringsdomeinen).</span><span class="sxs-lookup"><span data-stu-id="fa68b-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="fa68b-239">Bekijk het [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Virtual Network-overzicht) voor meer informatie over het gebruik van virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="fa68b-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
