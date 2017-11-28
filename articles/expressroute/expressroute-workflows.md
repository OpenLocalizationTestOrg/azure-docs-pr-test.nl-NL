---
title: aaaWorkflows voor het configureren van een ExpressRoute-circuit | Microsoft Docs
description: Deze pagina wordt u begeleid bij Hallo werkstromen voor het configureren van ExpressRoute-circuit en -peerings
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="e3217-103">ExpressRoute-werkstromen voor circuitinrichting en -statussen</span><span class="sxs-lookup"><span data-stu-id="e3217-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="e3217-104">Deze pagina wordt u begeleid Hallo service-inrichting en routering configuration werkstroom op hoog niveau.</span><span class="sxs-lookup"><span data-stu-id="e3217-104">This page walks you through hello service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="e3217-105">Hallo volgende afbeelding en de bijbehorende stappen Hallo taken weergeven dat moet u een ExpressRoute-circuit ingerichte end-to-end in de volgorde toohave volgen.</span><span class="sxs-lookup"><span data-stu-id="e3217-105">hello following figure and corresponding steps show hello tasks you must follow in order toohave an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="e3217-106">Gebruik PowerShell tooconfigure een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="e3217-106">Use PowerShell tooconfigure an ExpressRoute circuit.</span></span> <span data-ttu-id="e3217-107">Volg de instructies Hallo in Hallo [maken ExpressRoute-circuits](expressroute-howto-circuit-classic.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e3217-107">Follow hello instructions in hello [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="e3217-108">De verbinding van de volgorde van Hallo-provider.</span><span class="sxs-lookup"><span data-stu-id="e3217-108">Order connectivity from hello service provider.</span></span> <span data-ttu-id="e3217-109">Dit proces is.</span><span class="sxs-lookup"><span data-stu-id="e3217-109">This process varies.</span></span> <span data-ttu-id="e3217-110">Neem contact op met uw connectiviteitsprovider voor meer informatie over het tooorder connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="e3217-110">Contact your connectivity provider for more details about how tooorder connectivity.</span></span>
3. <span data-ttu-id="e3217-111">Zorg ervoor dat Hallo circuit is ingericht met succes gecontroleerd of ExpressRoute-circuit Hallo Inrichtingsstatus via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3217-111">Ensure that hello circuit has been provisioned successfully by verifying hello ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="e3217-112">Configureer Routeringsdomeinen.</span><span class="sxs-lookup"><span data-stu-id="e3217-112">Configure routing domains.</span></span> <span data-ttu-id="e3217-113">Als uw connectiviteitsprovider beheert de Layer 3 voor u, zal ze configureren voor uw circuit routering.</span><span class="sxs-lookup"><span data-stu-id="e3217-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="e3217-114">Als uw connectiviteitsprovider alleen Layer 2-services biedt, moet u routering per richtlijnen die worden beschreven in Hallo [routeringsvereisten](expressroute-routing.md) en [routeringsconfiguratie](expressroute-howto-routing-classic.md) pagina's.</span><span class="sxs-lookup"><span data-stu-id="e3217-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in hello [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="e3217-115">Inschakelen van persoonlijke Azure-peering - u moet deze peering tooconnect tooVMs inschakelen / cloudservices geïmplementeerd in virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="e3217-115">Enable Azure private peering - You must enable this peering tooconnect tooVMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="e3217-116">Inschakelen van openbare Azure-peering - u openbare Azure-peering moet inschakelen indien u wenst dat tooconnect tooAzure services die worden gehost op openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="e3217-116">Enable Azure public peering - You must enable Azure public peering if you wish tooconnect tooAzure services hosted on public IP addresses.</span></span> <span data-ttu-id="e3217-117">Dit is een vereiste tooaccess Azure-resources als u ervoor tooenable standaardroutering gekozen hebt voor persoonlijke Azure-peering.</span><span class="sxs-lookup"><span data-stu-id="e3217-117">This is a requirement tooaccess Azure resources if you have chosen tooenable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="e3217-118">Schakel Microsoft-peering - u moet deze tooaccess Office 365 en Dynamics 365 inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e3217-118">Enable Microsoft peering - You must enable this tooaccess Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="e3217-119">U moet ervoor zorgen dat u een afzonderlijke proxy gebruiken / edge tooconnect tooMicrosoft dan het account dat u gebruikt voor Hallo Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="e3217-119">You must ensure that you use a separate proxy / edge tooconnect tooMicrosoft than hello one you use for hello Internet.</span></span> <span data-ttu-id="e3217-120">Hallo dezelfde rand voor ExpressRoute- en Hallo Internet wordt veroorzaken asymmetrische Routering en connectiviteit uitval voor uw netwerk worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e3217-120">Using hello same edge for both ExpressRoute and hello Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="e3217-121">Koppelen van virtuele netwerken tooExpressRoute circuits - kunt u virtuele netwerken tooyour ExpressRoute-circuit koppelen.</span><span class="sxs-lookup"><span data-stu-id="e3217-121">Linking virtual networks tooExpressRoute circuits - You can link virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="e3217-122">Volg de instructies [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuit.</span><span class="sxs-lookup"><span data-stu-id="e3217-122">Follow instructions [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuit.</span></span> <span data-ttu-id="e3217-123">Deze VNets kan zijn in dezelfde Azure-abonnement als Hallo ExpressRoute-circuit Hallo of kunnen zich in een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="e3217-123">These VNets can either be in hello same Azure subscription as hello ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="e3217-124">ExpressRoute-circuit inrichtingstatuswaarden</span><span class="sxs-lookup"><span data-stu-id="e3217-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="e3217-125">Elk ExpressRoute-circuit heeft twee statussen:</span><span class="sxs-lookup"><span data-stu-id="e3217-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="e3217-126">Serviceprovider Inrichtingsstatus</span><span class="sxs-lookup"><span data-stu-id="e3217-126">Service provider provisioning state</span></span>
* <span data-ttu-id="e3217-127">Status</span><span class="sxs-lookup"><span data-stu-id="e3217-127">Status</span></span>

<span data-ttu-id="e3217-128">Status vertegenwoordigt van Microsoft-Inrichtingsstatus.</span><span class="sxs-lookup"><span data-stu-id="e3217-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="e3217-129">Deze eigenschap wordt tooEnabled ingesteld wanneer u een Expressroute-circuit maken</span><span class="sxs-lookup"><span data-stu-id="e3217-129">This property is set tooEnabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="e3217-130">Hallo connectiviteit provider Inrichtingsstatus vertegenwoordigt de status Hallo Hallo connectiviteit van de provider-zijde.</span><span class="sxs-lookup"><span data-stu-id="e3217-130">hello connectivity provider provisioning state represents hello state on hello connectivity provider's side.</span></span> <span data-ttu-id="e3217-131">Het kan zijn *NotProvisioned*, *inrichten*, of *ingericht*.</span><span class="sxs-lookup"><span data-stu-id="e3217-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="e3217-132">Hallo ExpressRoute-circuit moet worden ingericht voor u toobe kunnen toouse deze.</span><span class="sxs-lookup"><span data-stu-id="e3217-132">hello ExpressRoute circuit must be in Provisioned state for you toobe able toouse it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="e3217-133">Mogelijke statussen van een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="e3217-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="e3217-134">Deze sectie vindt u uit Hallo mogelijke statussen voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="e3217-134">This section lists out hello possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="e3217-135">**Tijdens het maken**</span><span class="sxs-lookup"><span data-stu-id="e3217-135">**At creation time**</span></span>

<span data-ttu-id="e3217-136">Hier ziet u Hallo ExpressRoute-circuit in Hallo zodra u de status na Hallo PowerShell cmdlet toocreate hello ExpressRoute-circuit worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e3217-136">You will see hello ExpressRoute circuit in hello following state as soon as you run hello PowerShell cmdlet toocreate hello ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="e3217-137">**Wanneer de connectiviteitsprovider in Hallo-proces voor het leveren van Hallo circuit is**</span><span class="sxs-lookup"><span data-stu-id="e3217-137">**When connectivity provider is in hello process of provisioning hello circuit**</span></span>

<span data-ttu-id="e3217-138">U ziet Hallo ExpressRoute-circuit in Hallo zodra u de status na sleutel toohello Hallo-connectiviteit serviceprovider doorgeven en ze Hallo inrichtingsproces hebt gestart.</span><span class="sxs-lookup"><span data-stu-id="e3217-138">You will see hello ExpressRoute circuit in hello following state as soon as you pass hello service key toohello connectivity provider and they have started hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="e3217-139">**Wanneer de connectiviteitsprovider Hallo inrichtingsproces is voltooid**</span><span class="sxs-lookup"><span data-stu-id="e3217-139">**When connectivity provider has completed hello provisioning process**</span></span>

<span data-ttu-id="e3217-140">U ziet Hallo ExpressRoute-circuit in Hallo status volgen als u de connectiviteitsprovider Hallo Hallo inrichtingsproces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e3217-140">You will see hello ExpressRoute circuit in hello following state as soon as hello connectivity provider has completed hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="e3217-141">Ingericht en ingeschakeld is Hallo status Hallo circuit kan slechts voor u toobe kunnen toouse deze worden.</span><span class="sxs-lookup"><span data-stu-id="e3217-141">Provisioned and Enabled is hello only state hello circuit can be in for you toobe able toouse it.</span></span> <span data-ttu-id="e3217-142">Als u een Layer 2-provider gebruikt, kunt u configureren routering voor uw circuit alleen wanneer deze status heeft.</span><span class="sxs-lookup"><span data-stu-id="e3217-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="e3217-143">**Wanneer de connectiviteitsprovider Hallo circuit is laagsjabloon**</span><span class="sxs-lookup"><span data-stu-id="e3217-143">**When connectivity provider is deprovisioning hello circuit**</span></span>

<span data-ttu-id="e3217-144">Als u Hallo serviceprovider toodeprovision hello ExpressRoute-circuit is aangevraagd, ziet u Hallo circuit ingesteld toohello status te volgen nadat het Hallo-serviceprovider Hallo opheffen van inrichting proces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e3217-144">If you requested hello service provider toodeprovision hello ExpressRoute circuit, you will see hello circuit set toohello following state after hello service provider has completed hello deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="e3217-145">U kunt toore inschakelen als, of de PowerShell-cmdlets uitvoeren toodelete Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="e3217-145">You can choose toore-enable it if needed, or run PowerShell cmdlets toodelete hello circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="e3217-146">Als u mislukt Hallo PowerShell cmdlet toodelete Hallo circuit wanneer Hallo ServiceProviderProvisioningState Provisioning of ingericht Hallo-bewerking is.</span><span class="sxs-lookup"><span data-stu-id="e3217-146">If you run hello PowerShell cmdlet toodelete hello circuit when hello ServiceProviderProvisioningState is Provisioning or Provisioned hello operation will fail.</span></span> <span data-ttu-id="e3217-147">Neem contact op met uw netwerkverbinding provider toodeprovision hello ExpressRoute-circuit eerst en verwijder vervolgens Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="e3217-147">Please work with your connectivity provider toodeprovision hello ExpressRoute circuit first and then delete hello circuit.</span></span> <span data-ttu-id="e3217-148">Microsoft blijft toobill Hallo circuit totdat u Hallo PowerShell cmdlet toodelete Hallo circuit uitvoert.</span><span class="sxs-lookup"><span data-stu-id="e3217-148">Microsoft will continue toobill hello circuit until you run hello PowerShell cmdlet toodelete hello circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="e3217-149">Configuratie van routering sessiestatus</span><span class="sxs-lookup"><span data-stu-id="e3217-149">Routing session configuration state</span></span>
<span data-ttu-id="e3217-150">Hallo BGP Inrichtingsstatus laat u weten als Hallo BGP-sessie op de Microsoft edge Hallo is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e3217-150">hello BGP provisioning state lets you know if hello BGP session has been enabled on hello Microsoft edge.</span></span> <span data-ttu-id="e3217-151">Hallo staat moet zijn ingeschakeld voor u toobe kunnen toouse hello peering.</span><span class="sxs-lookup"><span data-stu-id="e3217-151">hello state must be enabled for you toobe able toouse hello peering.</span></span>

<span data-ttu-id="e3217-152">Het is belangrijk toocheck Hallo BGP-sessiestatus met name voor Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="e3217-152">It is important toocheck hello BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="e3217-153">Toevoeging toohello BGP inrichting status heeft, wordt een andere status aangeroepen *aangekondigde openbare voorvoegsels status*.</span><span class="sxs-lookup"><span data-stu-id="e3217-153">In addition toohello BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="e3217-154">Hallo aangekondigde openbare voorvoegsels status moet *geconfigureerd* state, zowel voor Hallo BGP-sessie toobe omhoog als voor de routering toowork end-to-end.</span><span class="sxs-lookup"><span data-stu-id="e3217-154">hello advertised public prefixes state must be in *configured* state, both for hello BGP session toobe up and for your routing toowork end-to-end.</span></span> 

<span data-ttu-id="e3217-155">Als Hallo aangekondigd openbaar voorvoegsel status ingesteld op tooa *validatie nodig* staat, Hallo BGP-sessie niet is ingeschakeld, Hallo geadverteerde voorvoegsels komt niet overeen met de Hallo AS-nummer in een Hallo routeringsregisters.</span><span class="sxs-lookup"><span data-stu-id="e3217-155">If hello advertised public prefix state is set tooa *validation needed* state, hello BGP session is not enabled, as hello advertised prefixes did not match hello AS number in any of hello routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e3217-156">Als Hallo openbare voorvoegsels status aangekondigde is in *handmatige validatie* staat, moet u een ondersteuningsticket met openen [Microsoft ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) en bewijzen dat u Hallo IP-adressen bezit langs aangekondigd Hello autonoom systeemnummer die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="e3217-156">If hello advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own hello IP addresses advertised along with hello associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e3217-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e3217-157">Next steps</span></span>
* <span data-ttu-id="e3217-158">Configureer uw ExpressRoute-verbinding.</span><span class="sxs-lookup"><span data-stu-id="e3217-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="e3217-159">Een ExpressRoute-circuit maken</span><span class="sxs-lookup"><span data-stu-id="e3217-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="e3217-160">Routering configureren</span><span class="sxs-lookup"><span data-stu-id="e3217-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="e3217-161">Koppelen van een VNet tooan ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="e3217-161">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

