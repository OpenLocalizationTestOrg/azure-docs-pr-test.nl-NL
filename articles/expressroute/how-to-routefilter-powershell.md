---
title: 'Routefilters voor Azure ExpressRoute Microsoft-peering configureren: PowerShell | Microsoft Docs'
description: Dit artikel wordt beschreven hoe tooconfigure routefilters voor Microsoft-Peering met behulp van PowerShell
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
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="51f20-103">Routefilters voor Microsoft-peering configureren</span><span class="sxs-lookup"><span data-stu-id="51f20-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="51f20-104">Routefilters zijn een manier tooconsume een subset van de ondersteunde services via Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="51f20-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="51f20-105">Hallo stappen in dit artikel helpen u te configureren en beheren van routefilters voor ExpressRoute-circuits.</span><span class="sxs-lookup"><span data-stu-id="51f20-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="51f20-106">Dynamics 365-services en Office 365-services zoals Exchange Online, SharePoint Online en Skype voor bedrijven, zijn toegankelijk via Hallo Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="51f20-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="51f20-107">Wanneer Microsoft-peering in een ExpressRoute-circuit is geconfigureerd, worden alle voorvoegsels gerelateerde toothese-services worden geadverteerd via Hallo BGP-sessies die zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="51f20-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="51f20-108">Een BGP-communitywaarde is aangesloten tooevery voorvoegsel tooidentify Hallo service die wordt aangeboden via Hallo voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="51f20-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="51f20-109">Zie voor een lijst met Hallo BGP-Communitywaarden en deze worden toegewezen aan Hallo-services, [BGP-community's](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="51f20-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="51f20-110">Als u connectiviteit tooall services vereist, wordt een groot aantal voorvoegsels worden geadverteerd via BGP.</span><span class="sxs-lookup"><span data-stu-id="51f20-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="51f20-111">Dit aanzienlijk groter Hallo Hallo routetabellen onderhouden door routers in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="51f20-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="51f20-112">Als u van plan tooconsume slechts een subset van services die worden aangeboden bent via Microsoft-peering, kunt u de grootte van uw routetabellen op twee manieren Hallo reduceren.</span><span class="sxs-lookup"><span data-stu-id="51f20-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="51f20-113">U kunt:</span><span class="sxs-lookup"><span data-stu-id="51f20-113">You can:</span></span>

- <span data-ttu-id="51f20-114">Filter ongewenste voorvoegsels door routefilters zijn toegepast op de BGP-community's.</span><span class="sxs-lookup"><span data-stu-id="51f20-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="51f20-115">Dit is een standaardprocedure voor netwerken en meestal wordt gebruikt binnen meerdere netwerken.</span><span class="sxs-lookup"><span data-stu-id="51f20-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="51f20-116">Routefilters definiëren en ze tooyour ExpressRoute-circuit toepassen.</span><span class="sxs-lookup"><span data-stu-id="51f20-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="51f20-117">Een routefilter is een nieuwe resource dat u kunt aangeven Hallo lijst met services die u van plan bent tooconsume via Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="51f20-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="51f20-118">ExpressRoute-routers verzenden alleen Hallo lijst met voorvoegsels die deel uitmaken van toohello services in Hallo routefilter geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="51f20-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="51f20-119"><a name="about"></a>Over routefilters</span><span class="sxs-lookup"><span data-stu-id="51f20-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="51f20-120">Wanneer Microsoft-peering is geconfigureerd op uw ExpressRoute-circuit, opzetten Hallo Microsoft randrouters een combinatie van BGP-sessies met Hallo-randrouters (jouw e-mailadres of uw connectiviteitsprovider).</span><span class="sxs-lookup"><span data-stu-id="51f20-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="51f20-121">Er is geen routes worden aangekondigd tooyour netwerk.</span><span class="sxs-lookup"><span data-stu-id="51f20-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="51f20-122">tooenable route-advertisements tooyour netwerk, moet u een routefilter koppelen.</span><span class="sxs-lookup"><span data-stu-id="51f20-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="51f20-123">Een routefilter kunt u identificeren van de services die u wilt dat tooconsume via Microsoft-peering voor uw ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="51f20-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="51f20-124">Het is in wezen een witte lijst van alle Hallo BGP-Communitywaarden.</span><span class="sxs-lookup"><span data-stu-id="51f20-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="51f20-125">Wanneer een bron routeren filter wordt gedefinieerd en tooan ExpressRoute-circuit gekoppeld, zijn alle voorvoegsels die zijn toegewezen toohello BGP-Communitywaarden aangekondigd tooyour netwerk.</span><span class="sxs-lookup"><span data-stu-id="51f20-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="51f20-126">toobe kunnen tooattach routefilters met Office 365-services zich bevinden, moet u autorisatie tooconsume Office 365-services via ExpressRoute hebben.</span><span class="sxs-lookup"><span data-stu-id="51f20-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="51f20-127">Als u geen geautoriseerde tooconsume Office 365-services via ExpressRoute bent, mislukt de Hallo bewerking tooattach routefilters.</span><span class="sxs-lookup"><span data-stu-id="51f20-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="51f20-128">Zie voor meer informatie over het autorisatieproces Hallo [Azure ExpressRoute voor Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="51f20-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="51f20-129">Connectiviteit tooDynamics 365 services is niet vereist voor alle toestemming.</span><span class="sxs-lookup"><span data-stu-id="51f20-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51f20-130">Eerdere tooAugust 1 Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, 2017 hebben alle service voorvoegsels die worden geadverteerd via Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="51f20-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="51f20-131">Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter wordt aangesloten toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="51f20-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="51f20-132"><a name="workflow"></a>Werkstroom</span><span class="sxs-lookup"><span data-stu-id="51f20-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="51f20-133">toobe kunnen toosuccessfully tooservices verbinding via Microsoft-peering, moet u de volgende configuratiestappen Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="51f20-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="51f20-134">U moet een actief ExpressRoute-circuit met Microsoft-peering ingerichte hebben.</span><span class="sxs-lookup"><span data-stu-id="51f20-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="51f20-135">U kunt deze taken Hallo tooaccomplish instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="51f20-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="51f20-136">[Maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="51f20-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="51f20-137">Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="51f20-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="51f20-138">[Microsoft-peering maken](expressroute-circuit-peerings.md) als u rechtstreeks Hallo BGP-sessie beheren.</span><span class="sxs-lookup"><span data-stu-id="51f20-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="51f20-139">Of vraag uw connectiviteitsprovider Microsoft-peering voor uw circuit inrichten.</span><span class="sxs-lookup"><span data-stu-id="51f20-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="51f20-140">U moet maken en configureren van een routefilter.</span><span class="sxs-lookup"><span data-stu-id="51f20-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="51f20-141">Identificeren Hallo services die u met tooconsume via Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="51f20-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="51f20-142">Lijst van BGP-Communitywaarden die zijn gekoppeld aan services Hallo Hallo identificeren</span><span class="sxs-lookup"><span data-stu-id="51f20-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="51f20-143">Maak een regel tooallow Hallo voorvoegsel lijst overeenkomende Hallo BGP-Communitywaarden</span><span class="sxs-lookup"><span data-stu-id="51f20-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="51f20-144">Hallo route filter toohello ExpressRoute-circuit, moet u koppelen.</span><span class="sxs-lookup"><span data-stu-id="51f20-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="51f20-145">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="51f20-145">Before you begin</span></span>

<span data-ttu-id="51f20-146">Voordat u begint met de configuratie, zorg er dan voor dat u voldoet aan Hallo volgende criteria:</span><span class="sxs-lookup"><span data-stu-id="51f20-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="51f20-147">Installeer de nieuwste versie Hallo Hallo Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="51f20-147">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="51f20-148">Zie voor meer informatie [installeren en configureren van Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="51f20-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="51f20-149">Download de nieuwste versie Hallo bij Hallo PowerShell Gallery in plaats van met behulp van Hallo installatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="51f20-149">Download hello latest version from hello PowerShell Gallery, rather than using hello Installer.</span></span> <span data-ttu-id="51f20-150">Hallo installatieprogramma momenteel biedt geen ondersteuning voor cmdlets Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="51f20-150">hello Installer currently does not support hello required cmdlets.</span></span>
  > 

 - <span data-ttu-id="51f20-151">Bekijk Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="51f20-151">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="51f20-152">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="51f20-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="51f20-153">Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="51f20-153">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="51f20-154">Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="51f20-154">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="51f20-155">U hebt een actieve Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="51f20-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="51f20-156">Volg de instructies op [maken en wijzigen van peeringconfiguratie](expressroute-circuit-peerings.md)</span><span class="sxs-lookup"><span data-stu-id="51f20-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="51f20-157">Meld u bij tooyour Azure-account</span><span class="sxs-lookup"><span data-stu-id="51f20-157">Log in tooyour Azure account</span></span>

<span data-ttu-id="51f20-158">Voordat u deze configuratie, moet u zich aanmeldt tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="51f20-158">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="51f20-159">Hallo-cmdlet wordt u gevraagd om de aanmeldingsreferenties Hallo voor uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="51f20-159">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="51f20-160">Na het aanmelden, downloadt het instellingen van uw account, zodat ze beschikbaar tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51f20-160">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="51f20-161">Open de PowerShell-console met verhoogde bevoegdheden en tooyour-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="51f20-161">Open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="51f20-162">Gebruik Hallo voorbeeld toohelp die u verbinding maakt te volgen:</span><span class="sxs-lookup"><span data-stu-id="51f20-162">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="51f20-163">Als u meerdere Azure-abonnementen hebt, controleert u Hallo abonnementen voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="51f20-163">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="51f20-164">Hallo-abonnement dat u wilt dat toouse opgeven.</span><span class="sxs-lookup"><span data-stu-id="51f20-164">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="51f20-165"><a name="prefixes"></a>Stap 1.</span><span class="sxs-lookup"><span data-stu-id="51f20-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="51f20-166">Een lijst met voorvoegsels en BGP-Communitywaarden ophalen</span><span class="sxs-lookup"><span data-stu-id="51f20-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="51f20-167">1. Een lijst met waarden van BGP-community</span><span class="sxs-lookup"><span data-stu-id="51f20-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="51f20-168">Gebruik Hallo cmdlet tooget Hallo lijst met BGP-Communitywaarden die zijn gekoppeld aan services toegankelijk zijn via Microsoft-peering te volgen en Hallo lijst met voorvoegsels die zijn gekoppeld:</span><span class="sxs-lookup"><span data-stu-id="51f20-168">Use hello following cmdlet tooget hello list of BGP community values associated with services accessible through Microsoft peering, and hello list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="51f20-169">2. Maak een lijst van Hallo waarden die u toouse wilt</span><span class="sxs-lookup"><span data-stu-id="51f20-169">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="51f20-170">Maak een lijst van BGP-Communitywaarden die u wilt dat toouse in Hallo routefilter.</span><span class="sxs-lookup"><span data-stu-id="51f20-170">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="51f20-171">Hallo BGP-communitywaarde voor Dynamics 365 services is een voorbeeld: 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="51f20-171">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="51f20-172"><a name="filter"></a>Stap 2.</span><span class="sxs-lookup"><span data-stu-id="51f20-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="51f20-173">Maak een routefilter en een filterregel</span><span class="sxs-lookup"><span data-stu-id="51f20-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="51f20-174">Een routefilter kan slechts één regel, en Hallo regel moet van het type 'Toestaan'.</span><span class="sxs-lookup"><span data-stu-id="51f20-174">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="51f20-175">Deze regel kan een lijst met BGP-Communitywaarden die zijn gekoppeld hebben.</span><span class="sxs-lookup"><span data-stu-id="51f20-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="51f20-176">1. Maken van een routefilter</span><span class="sxs-lookup"><span data-stu-id="51f20-176">1. Create a route filter</span></span>

<span data-ttu-id="51f20-177">Maak eerst Hallo routefilter.</span><span class="sxs-lookup"><span data-stu-id="51f20-177">First, create hello route filter.</span></span> <span data-ttu-id="51f20-178">Hallo-opdracht 'New-AzureRmRouteFilter' wordt alleen een bron routeren filter.</span><span class="sxs-lookup"><span data-stu-id="51f20-178">hello command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="51f20-179">Nadat u Hallo bron maakt, moet u vervolgens maakt u een regel en koppelt u dit object toohello route-filter.</span><span class="sxs-lookup"><span data-stu-id="51f20-179">After you create hello resource, you must then create a rule and attach it toohello route filter object.</span></span> <span data-ttu-id="51f20-180">Voer Hallo opdracht toocreate na een bron routeren filter:</span><span class="sxs-lookup"><span data-stu-id="51f20-180">Run hello following command toocreate a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="51f20-181">2. Een filterregel maken</span><span class="sxs-lookup"><span data-stu-id="51f20-181">2. Create a filter rule</span></span>

<span data-ttu-id="51f20-182">U kunt een set van BGP-community's opgeven als een lijst door komma's gescheiden zoals weergegeven in Hallo voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="51f20-182">You can specify a set of BGP communities as a comma-separated list, as shown in hello example.</span></span> <span data-ttu-id="51f20-183">Voer Hallo opdracht toocreate na een nieuwe regel:</span><span class="sxs-lookup"><span data-stu-id="51f20-183">Run hello following command toocreate a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a><span data-ttu-id="51f20-184">3. Hallo regel toohello route-filter toevoegen</span><span class="sxs-lookup"><span data-stu-id="51f20-184">3. Add hello rule toohello route filter</span></span>

<span data-ttu-id="51f20-185">Voer Hallo opdracht tooadd Hallo regel toohello route datumfilter te volgen:</span><span class="sxs-lookup"><span data-stu-id="51f20-185">Run hello following command tooadd hello filter rule toohello route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="51f20-186"><a name="attach"></a>Stap 3.</span><span class="sxs-lookup"><span data-stu-id="51f20-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="51f20-187">Hallo route filter tooan ExpressRoute-circuit koppelen</span><span class="sxs-lookup"><span data-stu-id="51f20-187">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="51f20-188">Voer Hallo opdracht tooattach Hallo route filter toohello ExpressRoute-circuit, ervan uitgaande dat u hebt alleen Microsoft-peering te volgen:</span><span class="sxs-lookup"><span data-stu-id="51f20-188">Run hello following command tooattach hello route filter toohello ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="51f20-189"><a name="getproperties"></a>tooget hello eigenschappen van een routefilter</span><span class="sxs-lookup"><span data-stu-id="51f20-189"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="51f20-190">tooget hello eigenschappen van een routefilter, gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="51f20-190">tooget hello properties of a route filter, use hello following steps:</span></span>

1. <span data-ttu-id="51f20-191">Voer Hallo opdracht tooget Hallo route filter resource te volgen:</span><span class="sxs-lookup"><span data-stu-id="51f20-191">Run hello following command tooget hello route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="51f20-192">Hallo route filterregels voor Hallo route-filter resource ophalen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="51f20-192">Get hello route filter rules for hello route-filter resource by running hello following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="51f20-193"><a name="updateproperties"></a>tooupdate hello eigenschappen van een routefilter</span><span class="sxs-lookup"><span data-stu-id="51f20-193"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="51f20-194">Als Hallo routefilter is al gekoppeld tooa circuit, lijst met updates toohello BGP-community automatisch doorgegeven wijzigingen van de juiste voorvoegsel aankondiging via de BGP-sessies Hallo tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="51f20-194">If hello route filter is already attached tooa circuit, updates toohello BGP community list automatically propagates appropriate prefix advertisement changes through hello established BGP sessions.</span></span> <span data-ttu-id="51f20-195">U kunt Hallo BGP-community lijst van de routefilter met behulp van de volgende opdracht Hallo bijwerken:</span><span class="sxs-lookup"><span data-stu-id="51f20-195">You can update hello BGP community list of your route filter using hello following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="51f20-196"><a name="detach"></a>een routefilter van een ExpressRoute-circuit toodetach</span><span class="sxs-lookup"><span data-stu-id="51f20-196"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="51f20-197">Zodra een routefilter wordt losgekoppeld van Hallo ExpressRoute-circuit, worden er geen voorvoegsels zijn geadverteerd via Hallo BGP-sessie.</span><span class="sxs-lookup"><span data-stu-id="51f20-197">Once a route filter is detached from hello ExpressRoute circuit, no prefixes are advertised through hello BGP session.</span></span> <span data-ttu-id="51f20-198">U kunt een routefilter van een ExpressRoute-circuit met behulp van de volgende opdracht Hallo loskoppelen:</span><span class="sxs-lookup"><span data-stu-id="51f20-198">You can detach a route filter from an ExpressRoute circuit using hello following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="51f20-199"><a name="delete"></a>een routefilter toodelete</span><span class="sxs-lookup"><span data-stu-id="51f20-199"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="51f20-200">U kunt alleen verwijderen routefilter als het is niet gekoppeld tooany circuit.</span><span class="sxs-lookup"><span data-stu-id="51f20-200">You can only delete a route filter if it is not attached tooany circuit.</span></span> <span data-ttu-id="51f20-201">Zorg ervoor dat Hallo route-filter is niet gekoppeld tooany circuit voordat u probeert toodelete deze.</span><span class="sxs-lookup"><span data-stu-id="51f20-201">Ensure that hello route filter is not attached tooany circuit before attempting toodelete it.</span></span> <span data-ttu-id="51f20-202">U kunt een routefilter met behulp van de volgende opdracht Hallo verwijderen:</span><span class="sxs-lookup"><span data-stu-id="51f20-202">You can delete a route filter using hello following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="51f20-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51f20-203">Next steps</span></span>

<span data-ttu-id="51f20-204">Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="51f20-204">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
