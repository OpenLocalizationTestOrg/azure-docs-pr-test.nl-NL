---
title: 'Het configureren van routering (peering) voor een ExpressRoute-circuit: Resource Manager: Azure | Microsoft Docs'
description: Dit artikel begeleidt u stapsgewijs door de procedure voor het maken en inrichten van de persoonlijke, openbare en Microsoft-peering van een ExpressRoute-circuit. In dit artikel leest u hoe u de status controleert en peerings voor uw circuit bijwerkt of verwijdert.
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
ms.openlocfilehash: 55ccadfea55b8098ee58dcaef942f6ba54093665
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="9d195-104">Maken en wijzigen van de peering voor een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="9d195-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="9d195-105">In dit artikel helpt u bij het maken en beheren van routeringsconfiguratie voor een ExpressRoute-circuit in het Resource Manager-implementatiemodel met de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9d195-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using the Azure portal.</span></span> <span data-ttu-id="9d195-106">U kunt ook controleren van de status, update of delete en inrichting ervan ongedaan peerings voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="9d195-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="9d195-107">Als u een andere methode gebruiken om te werken met uw circuit wilt, selecteert u een artikel uit de volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="9d195-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="9d195-108">Configuratievereisten</span><span class="sxs-lookup"><span data-stu-id="9d195-108">Configuration prerequisites</span></span>

* <span data-ttu-id="9d195-109">Zorg dat u de pagina met [vereisten](expressroute-prerequisites.md), de pagina over [routeringsvereisten](expressroute-routing.md) en de pagina over [werkstromen](expressroute-workflows.md) hebt gelezen voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="9d195-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="9d195-110">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="9d195-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="9d195-111">Volg de instructies voor het [maken van een ExpressRoute-circuit](expressroute-howto-circuit-portal-resource-manager.md) en laat het circuit inschakelen door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="9d195-111">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="9d195-112">Het ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld om te kunnen uitvoeren van de cmdlets in de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="9d195-112">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in the next sections.</span></span>
* <span data-ttu-id="9d195-113">Als u van plan bent te gebruiken van een gedeelde sleutel/MD5-hash, moet u dit gebruikt op beide zijden van de tunnel en beperkt het aantal tekens tot maximaal 25.</span><span class="sxs-lookup"><span data-stu-id="9d195-113">If you plan to use a shared key/MD5 hash, be sure to use this on both sides of the tunnel and limit the number of characters to a maximum of 25.</span></span>

<span data-ttu-id="9d195-114">Deze instructies zijn alleen van toepassing op circuits die zijn gemaakt met serviceproviders die services met Laag-2-connectiviteit aanbieden.</span><span class="sxs-lookup"><span data-stu-id="9d195-114">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="9d195-115">Als u gebruikmaakt van een serviceprovider die beheerde laag-3-services (meestal een IPVPN, zoals MPLS), uw connectiviteitsprovider configureert en beheert routering voor u.</span><span class="sxs-lookup"><span data-stu-id="9d195-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9d195-116">Op dit moment bieden we nog geen peerings aan die door serviceproviders worden geconfigureerd via de beheerportal van de service.</span><span class="sxs-lookup"><span data-stu-id="9d195-116">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="9d195-117">Deze mogelijkheid zal binnenkort worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9d195-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="9d195-118">Neem contact op met uw serviceprovider voordat u BGP-peerings configureert.</span><span class="sxs-lookup"><span data-stu-id="9d195-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="9d195-119">U kunt een, twee of alle drie de peerings (Azure privé, Azure openbaar en Microsoft) voor een ExpressRoute-circuit configureren.</span><span class="sxs-lookup"><span data-stu-id="9d195-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="9d195-120">U kunt peerings configureren in elke gewenste volgorde.</span><span class="sxs-lookup"><span data-stu-id="9d195-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="9d195-121">U moet er echter wel voor zorgen dat u de configuratie van elke peering een voor een voltooit.</span><span class="sxs-lookup"><span data-stu-id="9d195-121">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="9d195-122">Persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="9d195-122">Azure private peering</span></span>

<span data-ttu-id="9d195-123">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van de Azure persoonlijke peering configuratie voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="9d195-123">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="9d195-124">Persoonlijke Azure-peering maken</span><span class="sxs-lookup"><span data-stu-id="9d195-124">To create Azure private peering</span></span>

1. <span data-ttu-id="9d195-125">Configureer het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="9d195-125">Configure the ExpressRoute circuit.</span></span> <span data-ttu-id="9d195-126">Zorg dat het circuit volledig is ingericht door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="9d195-126">Ensure that the circuit is fully provisioned by the connectivity provider before continuing.</span></span>

  ![lijst](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="9d195-128">Configureer persoonlijke Azure-peering voor het circuit.</span><span class="sxs-lookup"><span data-stu-id="9d195-128">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="9d195-129">Zorg ervoor dat u de volgende items hebt voordat u verdergaat met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="9d195-129">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="9d195-130">Een /30-subnet voor de primaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="9d195-130">A /30 subnet for the primary link.</span></span> <span data-ttu-id="9d195-131">Het subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.</span><span class="sxs-lookup"><span data-stu-id="9d195-131">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="9d195-132">Een /30-subnet voor de secundaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="9d195-132">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="9d195-133">Het subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.</span><span class="sxs-lookup"><span data-stu-id="9d195-133">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="9d195-134">Een geldige VLAN-id waarop u deze peering wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="9d195-134">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="9d195-135">Controleer of er geen andere peering in het circuit is die dezelfde VLAN-id gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9d195-135">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="9d195-136">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="9d195-136">AS number for peering.</span></span> <span data-ttu-id="9d195-137">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d195-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="9d195-138">U kunt een persoonlijk AS-nummer voor deze peering gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d195-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="9d195-139">Zorg dat u niet 65515 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9d195-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="9d195-140">**Optionele -** een MD5-hash, als u ervoor kiest een te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d195-140">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="9d195-141">Selecteer de rij van het Azure persoonlijke peering, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9d195-141">Select the Azure Private peering row, as shown in the following example:</span></span>

  ![Persoonlijke](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="9d195-143">Configureer persoonlijke Azure-peering.</span><span class="sxs-lookup"><span data-stu-id="9d195-143">Configure private peering.</span></span> <span data-ttu-id="9d195-144">De volgende afbeelding toont een configuratievoorbeeld van een:</span><span class="sxs-lookup"><span data-stu-id="9d195-144">The following image shows a configuration example:</span></span>

  ![Configureer persoonlijke peering](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="9d195-146">Sla de configuratie op wanneer u alle parameters hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9d195-146">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="9d195-147">Nadat de configuratie is geaccepteerd, ziet u iets soortgelijks als in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9d195-147">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![persoonlijke peering opslaan](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="9d195-149">De details van persoonlijke Azure-peering weergeven</span><span class="sxs-lookup"><span data-stu-id="9d195-149">To view Azure private peering details</span></span>

<span data-ttu-id="9d195-150">U kunt de eigenschappen van persoonlijke Azure-peering weergeven door de peering te selecteren.</span><span class="sxs-lookup"><span data-stu-id="9d195-150">You can view the properties of Azure private peering by selecting the peering.</span></span>

![persoonlijke peering weergeven](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="9d195-152">De configuratie van persoonlijke Azure-peering bijwerken</span><span class="sxs-lookup"><span data-stu-id="9d195-152">To update Azure private peering configuration</span></span>

<span data-ttu-id="9d195-153">U kunt de rij voor peering selecteren en de eigenschappen van de peering wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9d195-153">You can select the row for peering and modify the peering properties.</span></span>

![persoonlijke peering bijwerken](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="9d195-155">Persoonlijke Azure-peering verwijderen</span><span class="sxs-lookup"><span data-stu-id="9d195-155">To delete Azure private peering</span></span>

<span data-ttu-id="9d195-156">U kunt de peeringconfiguratie verwijderen door het verwijderingspictogram, zoals wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="9d195-156">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![persoonlijke peering verwijderen](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="9d195-158">Openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="9d195-158">Azure public peering</span></span>

<span data-ttu-id="9d195-159">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van de Azure openbare peering configuratie voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="9d195-159">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="9d195-160">Openbare Azure-peering maken</span><span class="sxs-lookup"><span data-stu-id="9d195-160">To create Azure public peering</span></span>

1. <span data-ttu-id="9d195-161">Configureer het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="9d195-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="9d195-162">Zorg dat het circuit volledig is ingericht door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="9d195-162">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![openbare peering weergeven](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="9d195-164">Configureer openbare Azure-peering voor het circuit.</span><span class="sxs-lookup"><span data-stu-id="9d195-164">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="9d195-165">Zorg ervoor dat u de volgende items hebt voordat u verdergaat met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="9d195-165">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="9d195-166">Een /30-subnet voor de primaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="9d195-166">A /30 subnet for the primary link.</span></span> <span data-ttu-id="9d195-167">Dit moet een geldig openbaar IPv4-voorvoegsel zijn.</span><span class="sxs-lookup"><span data-stu-id="9d195-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="9d195-168">Een /30-subnet voor de secundaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="9d195-168">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="9d195-169">Dit moet een geldig openbaar IPv4-voorvoegsel zijn.</span><span class="sxs-lookup"><span data-stu-id="9d195-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="9d195-170">Een geldige VLAN-id waarop u deze peering wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="9d195-170">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="9d195-171">Controleer of er geen andere peering in het circuit is die dezelfde VLAN-id gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9d195-171">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="9d195-172">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="9d195-172">AS number for peering.</span></span> <span data-ttu-id="9d195-173">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d195-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="9d195-174">**Optionele -** een MD5-hash, als u ervoor kiest een te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d195-174">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="9d195-175">Selecteer de Azure rij openbare peering, zoals weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="9d195-175">Select the Azure public peering row, as shown in the following image:</span></span>

  ![Selecteer de rij voor openbare peering](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="9d195-177">Configureer openbare Azure-peering.</span><span class="sxs-lookup"><span data-stu-id="9d195-177">Configure public peering.</span></span> <span data-ttu-id="9d195-178">De volgende afbeelding toont een configuratievoorbeeld van een:</span><span class="sxs-lookup"><span data-stu-id="9d195-178">The following image shows a configuration example:</span></span>

  ![Configureer openbare peering](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="9d195-180">Sla de configuratie op wanneer u alle parameters hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9d195-180">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="9d195-181">Nadat de configuratie is geaccepteerd, ziet u iets soortgelijks als in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9d195-181">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![Configuratie van openbare peering opslaan](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="9d195-183">De details van openbare Azure-peering weergeven</span><span class="sxs-lookup"><span data-stu-id="9d195-183">To view Azure public peering details</span></span>

<span data-ttu-id="9d195-184">U kunt de eigenschappen van openbare Azure-peering weergeven door de peering te selecteren.</span><span class="sxs-lookup"><span data-stu-id="9d195-184">You can view the properties of Azure public peering by selecting the peering.</span></span>

![de eigenschappen van openbare peering weergeven](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="9d195-186">De configuratie van openbare Azure-peering bijwerken</span><span class="sxs-lookup"><span data-stu-id="9d195-186">To update Azure public peering configuration</span></span>

<span data-ttu-id="9d195-187">U kunt de rij voor peering selecteren en de eigenschappen van de peering wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9d195-187">You can select the row for peering and modify the peering properties.</span></span>

![Selecteer de rij voor openbare peering](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="9d195-189">Openbare Azure-peering verwijderen</span><span class="sxs-lookup"><span data-stu-id="9d195-189">To delete Azure public peering</span></span>

<span data-ttu-id="9d195-190">U kunt de peeringconfiguratie verwijderen door het verwijderingspictogram, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9d195-190">You can remove your peering configuration by selecting the delete icon, as shown in the following example:</span></span>

![openbare peering verwijderen](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="9d195-192">Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="9d195-192">Microsoft peering</span></span>

<span data-ttu-id="9d195-193">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van de configuratie voor de Microsoft-peering voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="9d195-193">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d195-194">Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, voordat u 1 augustus 2017 hebben alle service voorvoegsels die worden geadverteerd via de Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="9d195-194">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="9d195-195">Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter is gekoppeld aan het circuit.</span><span class="sxs-lookup"><span data-stu-id="9d195-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="9d195-196">Zie voor meer informatie [configureren van een routefilter voor Microsoft-peering](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9d195-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="9d195-197">Microsoft-peering maken</span><span class="sxs-lookup"><span data-stu-id="9d195-197">To create Microsoft peering</span></span>

1. <span data-ttu-id="9d195-198">Configureer het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="9d195-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="9d195-199">Zorg dat het circuit volledig is ingericht door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="9d195-199">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![Microsoft-peering weergeven](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="9d195-201">Configureer Microsoft-peering voor het circuit.</span><span class="sxs-lookup"><span data-stu-id="9d195-201">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="9d195-202">Zorg ervoor dat u over de volgende informatie beschikt voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="9d195-202">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="9d195-203">Een /30-subnet voor de primaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="9d195-203">A /30 subnet for the primary link.</span></span> <span data-ttu-id="9d195-204">Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="9d195-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="9d195-205">Een /30-subnet voor de secundaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="9d195-205">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="9d195-206">Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="9d195-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="9d195-207">Een geldige VLAN-id waarop u deze peering wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="9d195-207">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="9d195-208">Controleer of er geen andere peering in het circuit is die dezelfde VLAN-id gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9d195-208">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="9d195-209">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="9d195-209">AS number for peering.</span></span> <span data-ttu-id="9d195-210">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d195-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="9d195-211">Geadverteerde voorvoegsels: u moet een lijst verstrekken van alle voorvoegsels die u via de BGP-sessie wilt adverteren.</span><span class="sxs-lookup"><span data-stu-id="9d195-211">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="9d195-212">Alleen openbare IP-adresvoorvoegsels worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="9d195-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="9d195-213">Als u van plan bent een reeks voorvoegsels verzenden, kunt u een door komma's gescheiden lijst verzenden.</span><span class="sxs-lookup"><span data-stu-id="9d195-213">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="9d195-214">Deze voorvoegsels moeten voor u zijn geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="9d195-214">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="9d195-215">**Optionele -** klant-ASN: als u voorvoegsels adverteert die niet zijn geregistreerd op de AS-nummer peering, kunt u het AS-nummer waaraan ze zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="9d195-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="9d195-216">Naam van routeringsregister: u kunt het RIR/IRR opgeven waarbij het AS-nummer en de voorvoegsels zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="9d195-216">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="9d195-217">**Optionele -** een MD5-hash, als u ervoor kiest een te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d195-217">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="9d195-218">U kunt de peering die u configureren, wilt zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="9d195-218">You can select the peering you wish to configure, as shown in the following example.</span></span> <span data-ttu-id="9d195-219">Selecteer de rij voor Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="9d195-219">Select the Microsoft peering row.</span></span>

  ![Selecteer de rij voor Microsoft-peering](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="9d195-221">Configureer Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="9d195-221">Configure Microsoft peering.</span></span> <span data-ttu-id="9d195-222">De volgende afbeelding toont een configuratievoorbeeld van een:</span><span class="sxs-lookup"><span data-stu-id="9d195-222">The following image shows a configuration example:</span></span>

  ![Configureer Microsoft-peering](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="9d195-224">Sla de configuratie op wanneer u alle parameters hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9d195-224">Save the configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="9d195-225">Als het circuit moet worden van een 'validatie nodig' status (zoals weergegeven in de afbeelding), moet u een ondersteuningsticket om aan te tonen dat u eigenaar bent van de voorvoegsels aan ons ondersteuningsteam aan openen.</span><span class="sxs-lookup"><span data-stu-id="9d195-225">If your circuit gets to a 'Validation needed' state (as shown in the image), you must open a support ticket to show proof of ownership of the prefixes to our support team.</span></span>

  ![Microsoft-peeringconfiguratie opslaan](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="9d195-227">U kunt een ondersteuningsticket rechtstreeks vanuit de portal openen, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9d195-227">You can open a support ticket directly from the portal, as shown in the following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="9d195-228">Nadat de configuratie is geaccepteerd, ziet u iets soortgelijks als in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="9d195-228">After the configuration has been accepted successfully, you see something similar to the following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="9d195-229">De details van Microsoft-peering weergeven</span><span class="sxs-lookup"><span data-stu-id="9d195-229">To view Microsoft peering details</span></span>

<span data-ttu-id="9d195-230">U kunt de eigenschappen van openbare Azure-peering weergeven door de peering te selecteren.</span><span class="sxs-lookup"><span data-stu-id="9d195-230">You can view the properties of Azure public peering by selecting the peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="9d195-231">Configuratie van Microsoft-peering bijwerken</span><span class="sxs-lookup"><span data-stu-id="9d195-231">To update Microsoft peering configuration</span></span>

<span data-ttu-id="9d195-232">U kunt de rij voor peering selecteren en de eigenschappen van de peering wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9d195-232">You can select the row for peering and modify the peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="9d195-233">Microsoft-peering verwijderen</span><span class="sxs-lookup"><span data-stu-id="9d195-233">To delete Microsoft peering</span></span>

<span data-ttu-id="9d195-234">U kunt de peeringconfiguratie verwijderen door het verwijderingspictogram, zoals wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="9d195-234">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="9d195-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d195-235">Next steps</span></span>

<span data-ttu-id="9d195-236">Volgende stap, [een VNet koppelen aan een ExpressRoute-circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="9d195-236">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="9d195-237">Voor meer informatie over ExpressRoute-werkstromen raadpleegt u [ExpressRoute workflows](expressroute-workflows.md) (ExpressRoute-werkstromen).</span><span class="sxs-lookup"><span data-stu-id="9d195-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="9d195-238">Voor meer informatie over circuitpeering raadpleegt u [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (ExpressRoute-circuits en -routeringsdomeinen).</span><span class="sxs-lookup"><span data-stu-id="9d195-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="9d195-239">Bekijk het [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Virtual Network-overzicht) voor meer informatie over het gebruik van virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="9d195-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
