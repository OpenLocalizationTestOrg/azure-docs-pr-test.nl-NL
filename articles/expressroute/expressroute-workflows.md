---
title: Werkstromen voor het configureren van een ExpressRoute-circuit | Microsoft Docs
description: Deze pagina wordt u begeleid bij de werkstromen voor het configureren van ExpressRoute-circuit en -peerings
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
ms.openlocfilehash: cba1b2cfee379e7d2b079bcb3089981ef1044d66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="4b80e-103">ExpressRoute-werkstromen voor circuitinrichting en -statussen</span><span class="sxs-lookup"><span data-stu-id="4b80e-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="4b80e-104">Deze pagina doorloopt u de service-inrichting en configuratie werkstromen routeren op hoog niveau.</span><span class="sxs-lookup"><span data-stu-id="4b80e-104">This page walks you through the service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="4b80e-105">De volgende afbeelding en de bijbehorende stappen wordt de taken die u volgen moet om een ExpressRoute-circuit ingericht end-to-end weergeven.</span><span class="sxs-lookup"><span data-stu-id="4b80e-105">The following figure and corresponding steps show the tasks you must follow in order to have an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="4b80e-106">PowerShell gebruiken voor het configureren van een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="4b80e-106">Use PowerShell to configure an ExpressRoute circuit.</span></span> <span data-ttu-id="4b80e-107">Volg de instructies in de [maken ExpressRoute-circuits](expressroute-howto-circuit-classic.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4b80e-107">Follow the instructions in the [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="4b80e-108">De verbinding van de volgorde van de serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="4b80e-108">Order connectivity from the service provider.</span></span> <span data-ttu-id="4b80e-109">Dit proces is.</span><span class="sxs-lookup"><span data-stu-id="4b80e-109">This process varies.</span></span> <span data-ttu-id="4b80e-110">Neem contact op met uw connectiviteitsprovider voor meer informatie over het rangschikken van connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="4b80e-110">Contact your connectivity provider for more details about how to order connectivity.</span></span>
3. <span data-ttu-id="4b80e-111">Zorg ervoor dat het circuit is ingericht met succes gecontroleerd of het ExpressRoute-circuit Inrichtingsstatus via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b80e-111">Ensure that the circuit has been provisioned successfully by verifying the ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="4b80e-112">Configureer Routeringsdomeinen.</span><span class="sxs-lookup"><span data-stu-id="4b80e-112">Configure routing domains.</span></span> <span data-ttu-id="4b80e-113">Als uw connectiviteitsprovider beheert de Layer 3 voor u, zal ze configureren voor uw circuit routering.</span><span class="sxs-lookup"><span data-stu-id="4b80e-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="4b80e-114">Als uw connectiviteitsprovider alleen Layer 2-services biedt, moet u routering per richtlijnen die worden beschreven in de [routeringsvereisten](expressroute-routing.md) en [routeringsconfiguratie](expressroute-howto-routing-classic.md) pagina's.</span><span class="sxs-lookup"><span data-stu-id="4b80e-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in the [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="4b80e-115">Inschakelen van persoonlijke Azure-peering - moet u deze peering als u wilt verbinding maken met virtuele machines / cloudservices geïmplementeerd in virtuele netwerken inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4b80e-115">Enable Azure private peering - You must enable this peering to connect to VMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="4b80e-116">Inschakelen van openbare Azure-peering - moet u de openbare Azure-peering als u wilt verbinding maken met Azure-services die worden gehost op openbare IP-adressen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4b80e-116">Enable Azure public peering - You must enable Azure public peering if you wish to connect to Azure services hosted on public IP addresses.</span></span> <span data-ttu-id="4b80e-117">Dit is een vereiste voor toegang tot Azure-resources als u hebt gekozen om in te schakelen standaardroutering voor persoonlijke Azure-peering.</span><span class="sxs-lookup"><span data-stu-id="4b80e-117">This is a requirement to access Azure resources if you have chosen to enable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="4b80e-118">Schakel Microsoft-peering - u moet dit inschakelt voor toegang tot Office 365 en Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="4b80e-118">Enable Microsoft peering - You must enable this to access Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="4b80e-119">U moet ervoor zorgen dat u een afzonderlijke proxy gebruiken / edge verbinding maken met Microsoft dan de versie die u gebruikt voor het Internet.</span><span class="sxs-lookup"><span data-stu-id="4b80e-119">You must ensure that you use a separate proxy / edge to connect to Microsoft than the one you use for the Internet.</span></span> <span data-ttu-id="4b80e-120">Met behulp van de rand voor ExpressRoute- en Internet veroorzaken asymmetrische Routering en leiden tot uitval connectiviteit voor uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="4b80e-120">Using the same edge for both ExpressRoute and the Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="4b80e-121">Virtuele netwerken koppelen aan ExpressRoute-circuits - kunt u virtuele netwerken koppelen aan uw ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="4b80e-121">Linking virtual networks to ExpressRoute circuits - You can link virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="4b80e-122">Volg de instructies [VNets koppelen](expressroute-howto-linkvnet-arm.md) aan uw circuit.</span><span class="sxs-lookup"><span data-stu-id="4b80e-122">Follow instructions [to link VNets](expressroute-howto-linkvnet-arm.md) to your circuit.</span></span> <span data-ttu-id="4b80e-123">Deze VNets in dezelfde Azure-abonnement als het ExpressRoute-circuit kan zijn of kunnen zich in een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="4b80e-123">These VNets can either be in the same Azure subscription as the ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="4b80e-124">ExpressRoute-circuit inrichtingstatuswaarden</span><span class="sxs-lookup"><span data-stu-id="4b80e-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="4b80e-125">Elk ExpressRoute-circuit heeft twee statussen:</span><span class="sxs-lookup"><span data-stu-id="4b80e-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="4b80e-126">Serviceprovider Inrichtingsstatus</span><span class="sxs-lookup"><span data-stu-id="4b80e-126">Service provider provisioning state</span></span>
* <span data-ttu-id="4b80e-127">Status</span><span class="sxs-lookup"><span data-stu-id="4b80e-127">Status</span></span>

<span data-ttu-id="4b80e-128">Status vertegenwoordigt van Microsoft-Inrichtingsstatus.</span><span class="sxs-lookup"><span data-stu-id="4b80e-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="4b80e-129">Deze eigenschap is ingesteld op ingeschakeld wanneer u een Expressroute-circuit maken</span><span class="sxs-lookup"><span data-stu-id="4b80e-129">This property is set to Enabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="4b80e-130">De provider-Inrichtingsstatus connectiviteit vertegenwoordigt de status van de connectiviteitsprovider zijde.</span><span class="sxs-lookup"><span data-stu-id="4b80e-130">The connectivity provider provisioning state represents the state on the connectivity provider's side.</span></span> <span data-ttu-id="4b80e-131">Het kan zijn *NotProvisioned*, *inrichten*, of *ingericht*.</span><span class="sxs-lookup"><span data-stu-id="4b80e-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="4b80e-132">Het ExpressRoute-circuit moet zijn ingericht voor u te kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4b80e-132">The ExpressRoute circuit must be in Provisioned state for you to be able to use it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="4b80e-133">Mogelijke statussen van een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="4b80e-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="4b80e-134">Deze sectie vindt u uit de mogelijke statussen voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="4b80e-134">This section lists out the possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="4b80e-135">**Tijdens het maken**</span><span class="sxs-lookup"><span data-stu-id="4b80e-135">**At creation time**</span></span>

<span data-ttu-id="4b80e-136">U ziet het ExpressRoute-circuit in de volgende status zodra u de PowerShell-cmdlet voor het maken van het ExpressRoute-circuit worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4b80e-136">You will see the ExpressRoute circuit in the following state as soon as you run the PowerShell cmdlet to create the ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="4b80e-137">**Wanneer de connectiviteitsprovider is bezig het inrichten van het circuit**</span><span class="sxs-lookup"><span data-stu-id="4b80e-137">**When connectivity provider is in the process of provisioning the circuit**</span></span>

<span data-ttu-id="4b80e-138">U ziet het ExpressRoute-circuit in de volgende status zodra u de servicesleutel aan de connectiviteitsprovider doorgeven en ze tijdens het inrichtingsproces hebt gestart.</span><span class="sxs-lookup"><span data-stu-id="4b80e-138">You will see the ExpressRoute circuit in the following state as soon as you pass the service key to the connectivity provider and they have started the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="4b80e-139">**Wanneer de connectiviteitsprovider tijdens het inrichtingsproces is voltooid**</span><span class="sxs-lookup"><span data-stu-id="4b80e-139">**When connectivity provider has completed the provisioning process**</span></span>

<span data-ttu-id="4b80e-140">U ziet het ExpressRoute-circuit in de volgende status zodra de connectiviteitsprovider tijdens het inrichtingsproces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4b80e-140">You will see the ExpressRoute circuit in the following state as soon as the connectivity provider has completed the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="4b80e-141">Ingericht en ingeschakeld is dat de enige staat het circuit kan zich in te kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4b80e-141">Provisioned and Enabled is the only state the circuit can be in for you to be able to use it.</span></span> <span data-ttu-id="4b80e-142">Als u een Layer 2-provider gebruikt, kunt u configureren routering voor uw circuit alleen wanneer deze status heeft.</span><span class="sxs-lookup"><span data-stu-id="4b80e-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="4b80e-143">**Wanneer de connectiviteitsprovider het circuit is laagsjabloon**</span><span class="sxs-lookup"><span data-stu-id="4b80e-143">**When connectivity provider is deprovisioning the circuit**</span></span>

<span data-ttu-id="4b80e-144">Als u de serviceprovider voor het ExpressRoute-circuit inrichting ervan ongedaan hebt aangevraagd, ziet u het circuit is ingesteld op de volgende status nadat de serviceprovider de inrichting proces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4b80e-144">If you requested the service provider to deprovision the ExpressRoute circuit, you will see the circuit set to the following state after the service provider has completed the deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="4b80e-145">U kunt deze opnieuw inschakelen als nodig is of PowerShell-cmdlets voor het verwijderen van het circuit worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4b80e-145">You can choose to re-enable it if needed, or run PowerShell cmdlets to delete the circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="4b80e-146">Als u de PowerShell-cmdlet voor het verwijderen van het circuit bij het inrichten van de ServiceProviderProvisioningState of ingericht, de bewerking mislukt uitvoert.</span><span class="sxs-lookup"><span data-stu-id="4b80e-146">If you run the PowerShell cmdlet to delete the circuit when the ServiceProviderProvisioningState is Provisioning or Provisioned the operation will fail.</span></span> <span data-ttu-id="4b80e-147">Neem contact op met uw connectiviteitsprovider om na te inrichting ervan ongedaan maakt het ExpressRoute-circuit eerst en verwijder vervolgens het circuit.</span><span class="sxs-lookup"><span data-stu-id="4b80e-147">Please work with your connectivity provider to deprovision the ExpressRoute circuit first and then delete the circuit.</span></span> <span data-ttu-id="4b80e-148">Microsoft blijft het circuit factureren totdat u de PowerShell-cmdlet voor het verwijderen van het circuit uitvoert.</span><span class="sxs-lookup"><span data-stu-id="4b80e-148">Microsoft will continue to bill the circuit until you run the PowerShell cmdlet to delete the circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="4b80e-149">Configuratie van routering sessiestatus</span><span class="sxs-lookup"><span data-stu-id="4b80e-149">Routing session configuration state</span></span>
<span data-ttu-id="4b80e-150">De Inrichtingsstatus BGP laat u weten als de BGP-sessie op de Microsoft edge is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4b80e-150">The BGP provisioning state lets you know if the BGP session has been enabled on the Microsoft edge.</span></span> <span data-ttu-id="4b80e-151">De status moet zijn ingeschakeld om te kunnen gebruiken de peering.</span><span class="sxs-lookup"><span data-stu-id="4b80e-151">The state must be enabled for you to be able to use the peering.</span></span>

<span data-ttu-id="4b80e-152">Het is belangrijk om te controleren van de status van de BGP-sessie met name voor Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="4b80e-152">It is important to check the BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="4b80e-153">Naast het BGP Inrichtingsstatus, is een andere status aangeroepen *aangekondigde openbare voorvoegsels status*.</span><span class="sxs-lookup"><span data-stu-id="4b80e-153">In addition to the BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="4b80e-154">De status van de aangekondigde openbare voorvoegsels moet *geconfigureerd* state, zowel voor de BGP-sessie worden omhoog als voor uw rondsturen werkt end-to-end.</span><span class="sxs-lookup"><span data-stu-id="4b80e-154">The advertised public prefixes state must be in *configured* state, both for the BGP session to be up and for your routing to work end-to-end.</span></span> 

<span data-ttu-id="4b80e-155">Als de status van de aangekondigde openbare voorvoegsel is ingesteld op een *validatie nodig* staat, de BGP-sessie niet is ingeschakeld, zoals de geadverteerde voorvoegsels komt niet overeen met het AS-nummer in een van de routeringsregisters.</span><span class="sxs-lookup"><span data-stu-id="4b80e-155">If the advertised public prefix state is set to a *validation needed* state, the BGP session is not enabled, as the advertised prefixes did not match the AS number in any of the routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4b80e-156">Als de status aangekondigde openbare voorvoegsels *handmatige validatie* staat, moet u een ondersteuningsticket met openen [Microsoft ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) en bewijzen dat u eigenaar van de IP-adressen die zijn aangekondigd samen met de gekoppelde autonoom systeemnummer.</span><span class="sxs-lookup"><span data-stu-id="4b80e-156">If the advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own the IP addresses advertised along with the associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4b80e-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b80e-157">Next steps</span></span>
* <span data-ttu-id="4b80e-158">Configureer uw ExpressRoute-verbinding.</span><span class="sxs-lookup"><span data-stu-id="4b80e-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="4b80e-159">Een ExpressRoute-circuit maken</span><span class="sxs-lookup"><span data-stu-id="4b80e-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="4b80e-160">Routering configureren</span><span class="sxs-lookup"><span data-stu-id="4b80e-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="4b80e-161">Een VNet koppelen aan een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="4b80e-161">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

