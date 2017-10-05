---
title: 'Routefilters voor Azure ExpressRoute Microsoft-peering configureren: Portal | Microsoft Docs'
description: Dit artikel wordt beschreven hoe u routefilters configureren voor Microsoft-Peering met de Azure portal
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
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: f17bf3e475a33cfc617e8a026e9606b3792101f3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="d2462-103">Routefilters voor Microsoft-peering configureren</span><span class="sxs-lookup"><span data-stu-id="d2462-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="d2462-104">Routefilters zijn een manier om te gebruiken een subset van de ondersteunde services via Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="d2462-104">Route filters are a way to consume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="d2462-105">De stappen in dit artikel te configureren en beheren van routefilters voor ExpressRoute-circuits.</span><span class="sxs-lookup"><span data-stu-id="d2462-105">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="d2462-106">Dynamics 365-services en Office 365-services zoals Exchange Online, SharePoint Online en Skype voor bedrijven, zijn toegankelijk via de Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="d2462-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through the Microsoft peering.</span></span> <span data-ttu-id="d2462-107">Wanneer Microsoft-peering in een ExpressRoute-circuit is geconfigureerd, worden alle voorvoegsels die betrekking hebben op deze services worden geadverteerd via de BGP-sessies worden tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="d2462-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span></span> <span data-ttu-id="d2462-108">Een BGP-communitywaarde is gekoppeld aan elke voorvoegsel van de service die wordt aangeboden via het voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="d2462-108">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span></span> <span data-ttu-id="d2462-109">Zie voor een lijst van de BGP-Communitywaarden en deze worden toegewezen aan services [BGP-community's](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="d2462-109">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="d2462-110">Als u de verbinding met alle services vereist, wordt een groot aantal voorvoegsels worden geadverteerd via BGP.</span><span class="sxs-lookup"><span data-stu-id="d2462-110">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="d2462-111">Dit verhoogt de aanzienlijk de grootte van de routetabellen onderhouden door routers in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="d2462-111">This significantly increases the size of the route tables maintained by routers within your network.</span></span> <span data-ttu-id="d2462-112">Als u van plan bent te gebruiken alleen een subset van services die worden aangeboden via Microsoft-peering, kunt u de grootte van uw routetabellen op twee manieren verkleinen.</span><span class="sxs-lookup"><span data-stu-id="d2462-112">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span></span> <span data-ttu-id="d2462-113">U kunt:</span><span class="sxs-lookup"><span data-stu-id="d2462-113">You can:</span></span>

- <span data-ttu-id="d2462-114">Filter ongewenste voorvoegsels door routefilters zijn toegepast op de BGP-community's.</span><span class="sxs-lookup"><span data-stu-id="d2462-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="d2462-115">Dit is een standaardprocedure voor netwerken en meestal wordt gebruikt binnen meerdere netwerken.</span><span class="sxs-lookup"><span data-stu-id="d2462-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="d2462-116">Routefilters definiëren en toegepast op uw ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="d2462-116">Define route filters and apply them to your ExpressRoute circuit.</span></span> <span data-ttu-id="d2462-117">Een routefilter is een nieuwe resource waarmee u de lijst met services die u van plan bent te gebruiken via Microsoft-peering te selecteren.</span><span class="sxs-lookup"><span data-stu-id="d2462-117">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span></span> <span data-ttu-id="d2462-118">ExpressRoute-routers worden alleen de lijst met voorvoegsels die deel uitmaken van de services die zijn geïdentificeerd in het routefilter verzenden.</span><span class="sxs-lookup"><span data-stu-id="d2462-118">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span></span>

### <span data-ttu-id="d2462-119"><a name="about"></a>Over routefilters</span><span class="sxs-lookup"><span data-stu-id="d2462-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="d2462-120">Wanneer Microsoft-peering is geconfigureerd op uw ExpressRoute-circuit, is de Microsoft-randrouters tot stand brengen een combinatie van BGP-sessies met routers van de rand (jouw e-mailadres of uw connectiviteitsprovider).</span><span class="sxs-lookup"><span data-stu-id="d2462-120">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="d2462-121">Er is geen routes worden geadverteerd naar uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="d2462-121">No routes are advertised to your network.</span></span> <span data-ttu-id="d2462-122">U moet een routefilter koppelen zodat route-advertisements met uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="d2462-122">To enable route advertisements to your network, you must associate a route filter.</span></span>

<span data-ttu-id="d2462-123">Een routefilter kunt u identificeren services die u gebruiken wilt via Microsoft-peering voor uw ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="d2462-123">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="d2462-124">Het is in wezen een witte lijst van alle waarden van de BGP-community.</span><span class="sxs-lookup"><span data-stu-id="d2462-124">It is essentially a white list of all the BGP community values.</span></span> <span data-ttu-id="d2462-125">Als een bron routeren filter wordt gedefinieerd en gekoppeld aan een ExpressRoute-circuit, worden alle voorvoegsels die zijn toegewezen aan de BGP-Communitywaarden worden geadverteerd naar uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="d2462-125">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span></span>

<span data-ttu-id="d2462-126">Als u routefilters met Office 365-services op deze te koppelen, moet u de autorisatie voor Office 365-services via ExpressRoute gebruiken hebben.</span><span class="sxs-lookup"><span data-stu-id="d2462-126">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="d2462-127">Als u bent niet gemachtigd om te gebruiken van Office 365-services via ExpressRoute, mislukt de bewerking routefilters koppelen.</span><span class="sxs-lookup"><span data-stu-id="d2462-127">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span></span> <span data-ttu-id="d2462-128">Zie voor meer informatie over het autorisatieproces [Azure ExpressRoute voor Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="d2462-128">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="d2462-129">De verbinding met Dynamics 365 services is niet vereist voor eventuele toestemming.</span><span class="sxs-lookup"><span data-stu-id="d2462-129">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2462-130">Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, voordat u 1 augustus 2017 hebben alle service voorvoegsels die worden geadverteerd via Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="d2462-130">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="d2462-131">Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter is gekoppeld aan het circuit.</span><span class="sxs-lookup"><span data-stu-id="d2462-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span>
> 
> 

### <span data-ttu-id="d2462-132"><a name="workflow"></a>Werkstroom</span><span class="sxs-lookup"><span data-stu-id="d2462-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="d2462-133">Om te kunnen maken met services via Microsoft-peering, moet u de volgende configuratiestappen uit:</span><span class="sxs-lookup"><span data-stu-id="d2462-133">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span></span>

- <span data-ttu-id="d2462-134">U moet een actief ExpressRoute-circuit met Microsoft-peering ingerichte hebben.</span><span class="sxs-lookup"><span data-stu-id="d2462-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="d2462-135">De volgende instructies kunt u deze taken:</span><span class="sxs-lookup"><span data-stu-id="d2462-135">You can use the following instructions to accomplish these tasks:</span></span>
  - <span data-ttu-id="d2462-136">[Maken van een ExpressRoute-circuit](expressroute-howto-circuit-portal-resource-manager.md) en laat het circuit ingeschakeld door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="d2462-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="d2462-137">Het ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d2462-137">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="d2462-138">[Microsoft-peering maken](expressroute-howto-routing-portal-resource-manager.md) als u de BGP-sessie rechtstreeks beheren.</span><span class="sxs-lookup"><span data-stu-id="d2462-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage the BGP session directly.</span></span> <span data-ttu-id="d2462-139">Of vraag uw connectiviteitsprovider Microsoft-peering voor uw circuit inrichten.</span><span class="sxs-lookup"><span data-stu-id="d2462-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="d2462-140">U moet maken en configureren van een routefilter.</span><span class="sxs-lookup"><span data-stu-id="d2462-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="d2462-141">Identificeer de services die u met gebruiken via Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="d2462-141">Identify the services you with to consume through Microsoft peering</span></span>
    - <span data-ttu-id="d2462-142">De lijst met BGP-Communitywaarden die zijn gekoppeld aan de services te identificeren</span><span class="sxs-lookup"><span data-stu-id="d2462-142">Identify the list of BGP community values associated with the services</span></span>
    - <span data-ttu-id="d2462-143">Maak een regel om toe te staan de Voorvoegsellijst die overeenkomen met de waarden van BGP-community</span><span class="sxs-lookup"><span data-stu-id="d2462-143">Create a rule to allow the prefix list matching the BGP community values</span></span>

-  <span data-ttu-id="d2462-144">U moet de routefilter koppelen aan ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="d2462-144">You must attach the route filter to the ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d2462-145">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="d2462-145">Before you begin</span></span>

<span data-ttu-id="d2462-146">Voordat u begint met de configuratie, zorg er dan voor dat u voldoet aan de volgende criteria:</span><span class="sxs-lookup"><span data-stu-id="d2462-146">Before you begin configuration, make sure you meet the following criteria:</span></span>

 - <span data-ttu-id="d2462-147">Controleer de [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="d2462-147">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="d2462-148">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="d2462-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="d2462-149">Volg de instructies voor het [maken van een ExpressRoute-circuit](expressroute-howto-circuit-portal-resource-manager.md) en laat het circuit inschakelen door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="d2462-149">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="d2462-150">Het ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d2462-150">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="d2462-151">U hebt een actieve Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="d2462-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="d2462-152">Volg de instructies op [maken en wijzigen van peeringconfiguratie](expressroute-howto-routing-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="d2462-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="d2462-153"><a name="prefixes"></a>Stap 1.</span><span class="sxs-lookup"><span data-stu-id="d2462-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="d2462-154">Een lijst met voorvoegsels en BGP-Communitywaarden ophalen</span><span class="sxs-lookup"><span data-stu-id="d2462-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="d2462-155">1. Een lijst met waarden van BGP-community</span><span class="sxs-lookup"><span data-stu-id="d2462-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="d2462-156">BGP-Communitywaarden die zijn gekoppeld aan services toegankelijk zijn via Microsoft-peering is beschikbaar in de [routeringsvereisten voor ExpressRoute](expressroute-routing.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="d2462-156">BGP community values associated with services accessible through Microsoft peering is available in the [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-the-values-that-you-want-to-use"></a><span data-ttu-id="d2462-157">2. Maak een lijst van de waarden die u wilt gebruiken</span><span class="sxs-lookup"><span data-stu-id="d2462-157">2. Make a list of the values that you want to use</span></span>

<span data-ttu-id="d2462-158">Maak een lijst van BGP-Communitywaarden die u wilt gebruiken in het routefilter.</span><span class="sxs-lookup"><span data-stu-id="d2462-158">Make a list of BGP community values you want to use in the route filter.</span></span> <span data-ttu-id="d2462-159">De BGP-communitywaarde voor Dynamics 365-services is een voorbeeld: 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="d2462-159">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="d2462-160"><a name="filter"></a>Stap 2.</span><span class="sxs-lookup"><span data-stu-id="d2462-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="d2462-161">Maak een routefilter en een filterregel</span><span class="sxs-lookup"><span data-stu-id="d2462-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="d2462-162">Een routefilter kan slechts één regel, en de regel moet van het type 'Toestaan'.</span><span class="sxs-lookup"><span data-stu-id="d2462-162">A route filter can have only one rule, and the rule must be of type 'Allow'.</span></span> <span data-ttu-id="d2462-163">Deze regel kan een lijst met BGP-Communitywaarden die zijn gekoppeld hebben.</span><span class="sxs-lookup"><span data-stu-id="d2462-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="d2462-164">1. Maken van een routefilter</span><span class="sxs-lookup"><span data-stu-id="d2462-164">1. Create a route filter</span></span>
<span data-ttu-id="d2462-165">U kunt een routefilter maken door de optie voor het maken van een nieuwe resource.</span><span class="sxs-lookup"><span data-stu-id="d2462-165">You can create a route filter by selecting the option to create a new resource.</span></span> <span data-ttu-id="d2462-166">Klik op **nieuw** > **Networking** > **RouteFilter**, zoals wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="d2462-166">Click **New** > **Networking** > **RouteFilter**, as shown in the following image:</span></span>

![Maken van een routefilter](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="d2462-168">U moet het routefilter plaatsen in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d2462-168">You must place the route filter in a resource group.</span></span> 

![Maken van een routefilter](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="d2462-170">2. Een filterregel maken</span><span class="sxs-lookup"><span data-stu-id="d2462-170">2. Create a filter rule</span></span>

<span data-ttu-id="d2462-171">U kunt toevoegen en regels bijwerken door het selecteren van het tabblad van de regel beheren voor uw routefilter.</span><span class="sxs-lookup"><span data-stu-id="d2462-171">You can add and update rules by selecting the manage rule tab for your route filter.</span></span>

![Maken van een routefilter](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="d2462-173">De services die u wilt verbinding maken met in de vervolgkeuzelijst en opslaan van de regel wanneer u klaar bent, kunt u selecteren.</span><span class="sxs-lookup"><span data-stu-id="d2462-173">You can select the services you want to connect to from the drop down list and save the rule when done.</span></span>

![Maken van een routefilter](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="d2462-175"><a name="attach"></a>Stap 3.</span><span class="sxs-lookup"><span data-stu-id="d2462-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="d2462-176">De routefilter koppelen aan een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="d2462-176">Attach the route filter to an ExpressRoute circuit</span></span>

<span data-ttu-id="d2462-177">U kunt de routefilter koppelen aan een circuit door met de knop 'Circuit toevoegen' en het ExpressRoute-circuit in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="d2462-177">You can attach the route filter to a circuit by selecting the "add Circuit" button and selecting the ExpressRoute circuit from the drop down list.</span></span>

![Maken van een routefilter](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="d2462-179"><a name="getproperties"></a>Ophalen van de eigenschappen van een routefilter</span><span class="sxs-lookup"><span data-stu-id="d2462-179"><a name="getproperties"></a>To get the properties of a route filter</span></span>

<span data-ttu-id="d2462-180">U kunt de eigenschappen van een routefilter weergeven bij het openen van de resource in de portal.</span><span class="sxs-lookup"><span data-stu-id="d2462-180">You can view properties of a route filter when you open the resource in the portal.</span></span>

![Maken van een routefilter](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="d2462-182"><a name="updateproperties"></a>De eigenschappen van een routefilter bijwerken</span><span class="sxs-lookup"><span data-stu-id="d2462-182"><a name="updateproperties"></a>To update the properties of a route filter</span></span>

<span data-ttu-id="d2462-183">U kunt de lijst met BGP-Communitywaarden die is gekoppeld aan een circuit door het selecteren van de knop 'Beheren regel' bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d2462-183">You can update the list of BGP community values attached to a circuit by selecting the "Manage rule" button.</span></span>


![Maken van een routefilter](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Maken van een routefilter](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="d2462-186"><a name="detach"></a>Ontkoppelen van een routefilter van een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="d2462-186"><a name="detach"></a>To detach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="d2462-187">Als u wilt loskoppelen van een met het routefilter voor de-circuit, klik met de rechtermuisknop op het circuit en klik op 'losgekoppeld'.</span><span class="sxs-lookup"><span data-stu-id="d2462-187">To detach a circuit from the route filter, right click on the circuit and click on "disassociate".</span></span>

![Maken van een routefilter](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="d2462-189"><a name="delete"></a>Een routefilter verwijderen</span><span class="sxs-lookup"><span data-stu-id="d2462-189"><a name="delete"></a>To delete a route filter</span></span>

<span data-ttu-id="d2462-190">U kunt een routefilter verwijderen door het selecteren van de knop verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d2462-190">You can delete a route filter by selecting the delete button.</span></span> 

![Maken van een routefilter](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="d2462-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d2462-192">Next steps</span></span>

<span data-ttu-id="d2462-193">Voor meer informatie over ExpressRoute raadpleegt u de [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="d2462-193">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>