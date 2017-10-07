---
title: 'Routefilters voor Azure ExpressRoute Microsoft-peering configureren: Portal | Microsoft Docs'
description: Dit artikel wordt beschreven hoe tooconfigure routefilters voor het gebruik van Microsoft-Peering hello Azure-portal
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
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="32d62-103">Routefilters voor Microsoft-peering configureren</span><span class="sxs-lookup"><span data-stu-id="32d62-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="32d62-104">Routefilters zijn een manier tooconsume een subset van de ondersteunde services via Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="32d62-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="32d62-105">Hallo stappen in dit artikel helpen u te configureren en beheren van routefilters voor ExpressRoute-circuits.</span><span class="sxs-lookup"><span data-stu-id="32d62-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="32d62-106">Dynamics 365-services en Office 365-services zoals Exchange Online, SharePoint Online en Skype voor bedrijven, zijn toegankelijk via Hallo Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="32d62-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="32d62-107">Wanneer Microsoft-peering in een ExpressRoute-circuit is geconfigureerd, worden alle voorvoegsels gerelateerde toothese-services worden geadverteerd via Hallo BGP-sessies die zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="32d62-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="32d62-108">Een BGP-communitywaarde is aangesloten tooevery voorvoegsel tooidentify Hallo service die wordt aangeboden via Hallo voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="32d62-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="32d62-109">Zie voor een lijst met Hallo BGP-Communitywaarden en deze worden toegewezen aan Hallo-services, [BGP-community's](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="32d62-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="32d62-110">Als u connectiviteit tooall services vereist, wordt een groot aantal voorvoegsels worden geadverteerd via BGP.</span><span class="sxs-lookup"><span data-stu-id="32d62-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="32d62-111">Dit aanzienlijk groter Hallo Hallo routetabellen onderhouden door routers in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="32d62-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="32d62-112">Als u van plan tooconsume slechts een subset van services die worden aangeboden bent via Microsoft-peering, kunt u de grootte van uw routetabellen op twee manieren Hallo reduceren.</span><span class="sxs-lookup"><span data-stu-id="32d62-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="32d62-113">U kunt:</span><span class="sxs-lookup"><span data-stu-id="32d62-113">You can:</span></span>

- <span data-ttu-id="32d62-114">Filter ongewenste voorvoegsels door routefilters zijn toegepast op de BGP-community's.</span><span class="sxs-lookup"><span data-stu-id="32d62-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="32d62-115">Dit is een standaardprocedure voor netwerken en meestal wordt gebruikt binnen meerdere netwerken.</span><span class="sxs-lookup"><span data-stu-id="32d62-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="32d62-116">Routefilters definiëren en ze tooyour ExpressRoute-circuit toepassen.</span><span class="sxs-lookup"><span data-stu-id="32d62-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="32d62-117">Een routefilter is een nieuwe resource dat u kunt aangeven Hallo lijst met services die u van plan bent tooconsume via Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="32d62-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="32d62-118">ExpressRoute-routers verzenden alleen Hallo lijst met voorvoegsels die deel uitmaken van toohello services in Hallo routefilter geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="32d62-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="32d62-119"><a name="about"></a>Over routefilters</span><span class="sxs-lookup"><span data-stu-id="32d62-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="32d62-120">Wanneer Microsoft-peering is geconfigureerd op uw ExpressRoute-circuit, opzetten Hallo Microsoft randrouters een combinatie van BGP-sessies met Hallo-randrouters (jouw e-mailadres of uw connectiviteitsprovider).</span><span class="sxs-lookup"><span data-stu-id="32d62-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="32d62-121">Er is geen routes worden aangekondigd tooyour netwerk.</span><span class="sxs-lookup"><span data-stu-id="32d62-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="32d62-122">tooenable route-advertisements tooyour netwerk, moet u een routefilter koppelen.</span><span class="sxs-lookup"><span data-stu-id="32d62-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="32d62-123">Een routefilter kunt u identificeren van de services die u wilt dat tooconsume via Microsoft-peering voor uw ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="32d62-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="32d62-124">Het is in wezen een witte lijst van alle Hallo BGP-Communitywaarden.</span><span class="sxs-lookup"><span data-stu-id="32d62-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="32d62-125">Wanneer een bron routeren filter wordt gedefinieerd en tooan ExpressRoute-circuit gekoppeld, zijn alle voorvoegsels die zijn toegewezen toohello BGP-Communitywaarden aangekondigd tooyour netwerk.</span><span class="sxs-lookup"><span data-stu-id="32d62-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="32d62-126">toobe kunnen tooattach routefilters met Office 365-services zich bevinden, moet u autorisatie tooconsume Office 365-services via ExpressRoute hebben.</span><span class="sxs-lookup"><span data-stu-id="32d62-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="32d62-127">Als u geen geautoriseerde tooconsume Office 365-services via ExpressRoute bent, mislukt de Hallo bewerking tooattach routefilters.</span><span class="sxs-lookup"><span data-stu-id="32d62-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="32d62-128">Zie voor meer informatie over het autorisatieproces Hallo [Azure ExpressRoute voor Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="32d62-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="32d62-129">Connectiviteit tooDynamics 365 services is niet vereist voor alle toestemming.</span><span class="sxs-lookup"><span data-stu-id="32d62-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32d62-130">Eerdere tooAugust 1 Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, 2017 hebben alle service voorvoegsels die worden geadverteerd via Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="32d62-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="32d62-131">Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter wordt aangesloten toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="32d62-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="32d62-132"><a name="workflow"></a>Werkstroom</span><span class="sxs-lookup"><span data-stu-id="32d62-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="32d62-133">toobe kunnen toosuccessfully tooservices verbinding via Microsoft-peering, moet u de volgende configuratiestappen Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="32d62-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="32d62-134">U moet een actief ExpressRoute-circuit met Microsoft-peering ingerichte hebben.</span><span class="sxs-lookup"><span data-stu-id="32d62-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="32d62-135">U kunt deze taken Hallo tooaccomplish instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="32d62-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="32d62-136">[Maken van een ExpressRoute-circuit](expressroute-howto-circuit-portal-resource-manager.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="32d62-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="32d62-137">Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="32d62-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="32d62-138">[Microsoft-peering maken](expressroute-howto-routing-portal-resource-manager.md) als u rechtstreeks Hallo BGP-sessie beheren.</span><span class="sxs-lookup"><span data-stu-id="32d62-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="32d62-139">Of vraag uw connectiviteitsprovider Microsoft-peering voor uw circuit inrichten.</span><span class="sxs-lookup"><span data-stu-id="32d62-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="32d62-140">U moet maken en configureren van een routefilter.</span><span class="sxs-lookup"><span data-stu-id="32d62-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="32d62-141">Identificeren Hallo services die u met tooconsume via Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="32d62-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="32d62-142">Lijst van BGP-Communitywaarden die zijn gekoppeld aan services Hallo Hallo identificeren</span><span class="sxs-lookup"><span data-stu-id="32d62-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="32d62-143">Maak een regel tooallow Hallo voorvoegsel lijst overeenkomende Hallo BGP-Communitywaarden</span><span class="sxs-lookup"><span data-stu-id="32d62-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="32d62-144">Hallo route filter toohello ExpressRoute-circuit, moet u koppelen.</span><span class="sxs-lookup"><span data-stu-id="32d62-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="32d62-145">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="32d62-145">Before you begin</span></span>

<span data-ttu-id="32d62-146">Voordat u begint met de configuratie, zorg er dan voor dat u voldoet aan Hallo volgende criteria:</span><span class="sxs-lookup"><span data-stu-id="32d62-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="32d62-147">Bekijk Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="32d62-147">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="32d62-148">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="32d62-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="32d62-149">Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-portal-resource-manager.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="32d62-149">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="32d62-150">Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="32d62-150">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="32d62-151">U hebt een actieve Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="32d62-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="32d62-152">Volg de instructies op [maken en wijzigen van peeringconfiguratie](expressroute-howto-routing-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="32d62-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="32d62-153"><a name="prefixes"></a>Stap 1.</span><span class="sxs-lookup"><span data-stu-id="32d62-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="32d62-154">Een lijst met voorvoegsels en BGP-Communitywaarden ophalen</span><span class="sxs-lookup"><span data-stu-id="32d62-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="32d62-155">1. Een lijst met waarden van BGP-community</span><span class="sxs-lookup"><span data-stu-id="32d62-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="32d62-156">BGP-Communitywaarden die zijn gekoppeld aan services toegankelijk zijn via Microsoft-peering is beschikbaar in Hallo [routeringsvereisten voor ExpressRoute](expressroute-routing.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="32d62-156">BGP community values associated with services accessible through Microsoft peering is available in hello [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="32d62-157">2. Maak een lijst van Hallo waarden die u toouse wilt</span><span class="sxs-lookup"><span data-stu-id="32d62-157">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="32d62-158">Maak een lijst van BGP-Communitywaarden die u wilt dat toouse in Hallo routefilter.</span><span class="sxs-lookup"><span data-stu-id="32d62-158">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="32d62-159">Hallo BGP-communitywaarde voor Dynamics 365 services is een voorbeeld: 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="32d62-159">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="32d62-160"><a name="filter"></a>Stap 2.</span><span class="sxs-lookup"><span data-stu-id="32d62-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="32d62-161">Maak een routefilter en een filterregel</span><span class="sxs-lookup"><span data-stu-id="32d62-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="32d62-162">Een routefilter kan slechts één regel, en Hallo regel moet van het type 'Toestaan'.</span><span class="sxs-lookup"><span data-stu-id="32d62-162">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="32d62-163">Deze regel kan een lijst met BGP-Communitywaarden die zijn gekoppeld hebben.</span><span class="sxs-lookup"><span data-stu-id="32d62-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="32d62-164">1. Maken van een routefilter</span><span class="sxs-lookup"><span data-stu-id="32d62-164">1. Create a route filter</span></span>
<span data-ttu-id="32d62-165">U kunt een routefilter maken door het selecteren van Hallo optie toocreate een nieuwe resource.</span><span class="sxs-lookup"><span data-stu-id="32d62-165">You can create a route filter by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="32d62-166">Klik op **nieuw** > **Networking** > **RouteFilter**, zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="32d62-166">Click **New** > **Networking** > **RouteFilter**, as shown in hello following image:</span></span>

![Maken van een routefilter](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="32d62-168">U moet Hallo routefilter plaatsen in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="32d62-168">You must place hello route filter in a resource group.</span></span> 

![Maken van een routefilter](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="32d62-170">2. Een filterregel maken</span><span class="sxs-lookup"><span data-stu-id="32d62-170">2. Create a filter rule</span></span>

<span data-ttu-id="32d62-171">U kunt toevoegen en updateregels door het selecteren van Hallo regel tabblad voor de routefilter beheren.</span><span class="sxs-lookup"><span data-stu-id="32d62-171">You can add and update rules by selecting hello manage rule tab for your route filter.</span></span>

![Maken van een routefilter](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="32d62-173">Hallo services gewenste tooconnect toofrom Hallo vervolgkeuzelijst en opslaan van de regel Hallo wanneer u klaar bent, kunt u selecteren.</span><span class="sxs-lookup"><span data-stu-id="32d62-173">You can select hello services you want tooconnect toofrom hello drop down list and save hello rule when done.</span></span>

![Maken van een routefilter](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="32d62-175"><a name="attach"></a>Stap 3.</span><span class="sxs-lookup"><span data-stu-id="32d62-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="32d62-176">Hallo route filter tooan ExpressRoute-circuit koppelen</span><span class="sxs-lookup"><span data-stu-id="32d62-176">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="32d62-177">Hallo 'Circuit toevoegen' knop selecteren en ExpressRoute-circuit Hallo selecteren in de vervolgkeuzelijst Hallo kunt Hallo route filter tooa circuit koppelen.</span><span class="sxs-lookup"><span data-stu-id="32d62-177">You can attach hello route filter tooa circuit by selecting hello "add Circuit" button and selecting hello ExpressRoute circuit from hello drop down list.</span></span>

![Maken van een routefilter](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="32d62-179"><a name="getproperties"></a>tooget hello eigenschappen van een routefilter</span><span class="sxs-lookup"><span data-stu-id="32d62-179"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="32d62-180">U kunt de eigenschappen van een routefilter weergeven wanneer u Hallo resource in Hallo portal opent.</span><span class="sxs-lookup"><span data-stu-id="32d62-180">You can view properties of a route filter when you open hello resource in hello portal.</span></span>

![Maken van een routefilter](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="32d62-182"><a name="updateproperties"></a>tooupdate hello eigenschappen van een routefilter</span><span class="sxs-lookup"><span data-stu-id="32d62-182"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="32d62-183">U kunt Hallo-lijst van BGP-community waarden gekoppelde tooa circuit bijwerken door Hallo 'beheren regel' knop te selecteren.</span><span class="sxs-lookup"><span data-stu-id="32d62-183">You can update hello list of BGP community values attached tooa circuit by selecting hello "Manage rule" button.</span></span>


![Maken van een routefilter](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Maken van een routefilter](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="32d62-186"><a name="detach"></a>een routefilter van een ExpressRoute-circuit toodetach</span><span class="sxs-lookup"><span data-stu-id="32d62-186"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="32d62-187">toodetach een circuit van Hallo route-filter, klik met de rechtermuisknop op Hallo circuit en klik op 'losgekoppeld'.</span><span class="sxs-lookup"><span data-stu-id="32d62-187">toodetach a circuit from hello route filter, right click on hello circuit and click on "disassociate".</span></span>

![Maken van een routefilter](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="32d62-189"><a name="delete"></a>een routefilter toodelete</span><span class="sxs-lookup"><span data-stu-id="32d62-189"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="32d62-190">Als u de knop verwijderen Hallo selecteert, kunt u een routefilter verwijderen.</span><span class="sxs-lookup"><span data-stu-id="32d62-190">You can delete a route filter by selecting hello delete button.</span></span> 

![Maken van een routefilter](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="32d62-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="32d62-192">Next steps</span></span>

<span data-ttu-id="32d62-193">Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="32d62-193">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
