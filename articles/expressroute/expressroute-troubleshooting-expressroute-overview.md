---
title: 'Controleren of verbinding: Azure ExpressRoute Troubleshooting Guide | Microsoft Docs'
description: Deze pagina vindt u instructies voor het oplossen van problemen en end tooend verbinding van een ExpressRoute-circuit valideren.
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="5a314-103">ExpressRoute-verbinding controleren</span><span class="sxs-lookup"><span data-stu-id="5a314-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="5a314-104">ExpressRoute, die een uitbreiding is een on-premises netwerk via een persoonlijke verbinding die wordt gefaciliteerd door een connectiviteitsprovider in Hallo Microsoft cloud, omvat Hallo drie afzonderlijke netwerkzones te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a314-104">ExpressRoute, which extends an on-premises network into hello Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves hello following three distinct network zones:</span></span>

-   <span data-ttu-id="5a314-105">Klantnetwerk</span><span class="sxs-lookup"><span data-stu-id="5a314-105">Customer Network</span></span>
-   <span data-ttu-id="5a314-106">Serviceprovider-netwerk</span><span class="sxs-lookup"><span data-stu-id="5a314-106">Provider Network</span></span>
-   <span data-ttu-id="5a314-107">Microsoft-datacentrum</span><span class="sxs-lookup"><span data-stu-id="5a314-107">Microsoft Datacenter</span></span>

<span data-ttu-id="5a314-108">Hallo-doel van dit document is toohelp gebruiker tooidentify waar (of zelfs als) een verbindingsprobleem bestaat en in welke zone, waardoor tooseek hulp van de juiste team tooresolve Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="5a314-108">hello purpose of this document is toohelp user tooidentify where (or even if) a connectivity issue exists and within which zone, thereby tooseek help from appropriate team tooresolve hello issue.</span></span> <span data-ttu-id="5a314-109">Als de ondersteuning van Microsoft nodig tooresolve een probleem is, opent u een ondersteuningsticket met [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="5a314-109">If Microsoft support is needed tooresolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a314-110">Dit document is bedoeld toohelp opsporen en oplossen van eenvoudige problemen.</span><span class="sxs-lookup"><span data-stu-id="5a314-110">This document is intended toohelp diagnosing and fixing simple issues.</span></span> <span data-ttu-id="5a314-111">Het is niet bedoeld toobe vervanging voor ondersteuning van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5a314-111">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="5a314-112">Open een ondersteuningsticket met [Microsoft Support] [ Support] bent u toosolve Hallo probleem op door middel van Hallo richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="5a314-112">Open a support ticket with [Microsoft Support][Support] if you are unable toosolve hello problem using hello guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="5a314-113">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5a314-113">Overview</span></span>
<span data-ttu-id="5a314-114">Hallo toont volgende diagram Hallo logische verbinding van een klant tooMicrosoft netwerk van het netwerk met behulp van ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5a314-114">hello following diagram shows hello logical connectivity of a customer network tooMicrosoft network using ExpressRoute.</span></span>
<span data-ttu-id="5a314-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="5a314-115">[![1]][1]</span></span>

<span data-ttu-id="5a314-116">In Hallo voorgaande diagram, aangeven Hallo cijfers netwerk belangrijke punten.</span><span class="sxs-lookup"><span data-stu-id="5a314-116">In hello preceding diagram, hello numbers indicate key network points.</span></span> <span data-ttu-id="5a314-117">Hallo netwerk punten zijn vaak in dit artikel verwezen door hun bijbehorende nummers.</span><span class="sxs-lookup"><span data-stu-id="5a314-117">hello network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="5a314-118">Afhankelijk van Hallo ExpressRoute connectiviteit mogelijk model (Cloud Exchange CO-locatie, Point-to-Point Ethernet-verbinding of Any-to-any (IPVPN)) Hallo netwerk punten 3 en 4 switches (Layer 2-apparaten).</span><span class="sxs-lookup"><span data-stu-id="5a314-118">Depending on hello ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) hello network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="5a314-119">Hallo netwerk belangrijke punten geïllustreerd zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="5a314-119">hello key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="5a314-120">Klant compute-apparaat (bijvoorbeeld een server of een PC)</span><span class="sxs-lookup"><span data-stu-id="5a314-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="5a314-121">CEs: Klant-randrouters</span><span class="sxs-lookup"><span data-stu-id="5a314-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="5a314-122">PEs (CE facing): Provider rand routers/schakelaars waarmee worden geconfronteerd randrouters klant.</span><span class="sxs-lookup"><span data-stu-id="5a314-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="5a314-123">Tooas PE CEs in dit document wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="5a314-123">Referred tooas PE-CEs in this document.</span></span>
4.  <span data-ttu-id="5a314-124">PEs (MSEE facing): Provider rand routers/schakelaars waarmee worden geconfronteerd msee's.</span><span class="sxs-lookup"><span data-stu-id="5a314-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="5a314-125">Tooas PE-msee's in dit document wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="5a314-125">Referred tooas PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="5a314-126">Msee's: Microsoft Enterprise Edge (MSEE) ExpressRoute-routers</span><span class="sxs-lookup"><span data-stu-id="5a314-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="5a314-127">De Gateway virtuele netwerk (VNet)</span><span class="sxs-lookup"><span data-stu-id="5a314-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="5a314-128">COMPUTE-apparaat op Hallo Azure VNet</span><span class="sxs-lookup"><span data-stu-id="5a314-128">Compute device on hello Azure VNet</span></span>

<span data-ttu-id="5a314-129">Als u connectiviteitsmodellen Hallo Cloud Exchange CO-locatie of Point-to-Point Ethernet-verbinding gebruikt, zou Hallo klant edge router (2) tot stand brengen BGP-peer met msee's (5).</span><span class="sxs-lookup"><span data-stu-id="5a314-129">If hello Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, hello customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="5a314-130">Netwerk punten 3 en 4 wordt nog steeds aanwezig zijn, maar enigszins transparant als Layer 2-apparaten.</span><span class="sxs-lookup"><span data-stu-id="5a314-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="5a314-131">Als Hallo Any-to-any (IPVPN) connectiviteit model wordt gebruikt, Hallo PEs (MSEE facing) (4) zou tot stand brengen BGP-peer met msee's (5).</span><span class="sxs-lookup"><span data-stu-id="5a314-131">If hello Any-to-any (IPVPN) connectivity model is used, hello PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="5a314-132">Routes zou worden doorgegeven aan een netwerk van de klant back toohello via Hallo IPVPN serviceprovider-netwerk.</span><span class="sxs-lookup"><span data-stu-id="5a314-132">Routes would then propagate back toohello customer network via hello IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="5a314-133">Microsoft vereist voor ExpressRoute hoge beschikbaarheid, een paar redundante BGP-sessies tussen de msee's (5) en PE-msee's (4).</span><span class="sxs-lookup"><span data-stu-id="5a314-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="5a314-134">Een paar redundante netwerkpaden wordt ook aangemoedigd tussen klantnetwerk en PE CEs.</span><span class="sxs-lookup"><span data-stu-id="5a314-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="5a314-135">Echter, in Any-to-any (IPVPN) verbinding model één CE-apparaat (2) mogelijk verbonden tooone of meer PEs (3).</span><span class="sxs-lookup"><span data-stu-id="5a314-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected tooone or more PEs (3).</span></span>
>
>

<span data-ttu-id="5a314-136">toovalidate een ExpressRoute-circuit Hallo stappen te volgen (met Hallo netwerk beheerpunt door Hallo gekoppeld getal aangegeven) worden behandeld:</span><span class="sxs-lookup"><span data-stu-id="5a314-136">toovalidate an ExpressRoute circuit, hello following steps are covered (with hello network point indicated by hello associated number):</span></span>
1. [<span data-ttu-id="5a314-137">Valideren van circuitinrichting en status (5)</span><span class="sxs-lookup"><span data-stu-id="5a314-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="5a314-138">Valideren van ten minste één ExpressRoute-peering is geconfigureerd (5)</span><span class="sxs-lookup"><span data-stu-id="5a314-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="5a314-139">Valideren van ARP tussen Microsoft en Hallo serviceprovider (koppeling tussen 4 en 5)</span><span class="sxs-lookup"><span data-stu-id="5a314-139">Validate ARP between Microsoft and hello service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="5a314-140">Valideren van BGP en routes op Hallo MSEE (BGP tussen too5 4 en 5 too6 als een VNet is verbonden)</span><span class="sxs-lookup"><span data-stu-id="5a314-140">Validate BGP and routes on hello MSEE (BGP between 4 too5, and 5 too6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="5a314-141">Selectievakje Hallo verkeer-statistieken (verkeer doorlopen 5)</span><span class="sxs-lookup"><span data-stu-id="5a314-141">Check hello Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="5a314-142">Meer validaties en controles worden toegevoegd in Hallo toekomstige, controle terug maandelijks!</span><span class="sxs-lookup"><span data-stu-id="5a314-142">More validations and checks will be added in hello future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="5a314-143">Valideren van circuitinrichting en status</span><span class="sxs-lookup"><span data-stu-id="5a314-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="5a314-144">Ongeacht Hallo connectivity-model, heeft een ExpressRoute-circuit toobe gemaakt, en daarom een service sleutel gegenereerd voor het inrichten van het circuit.</span><span class="sxs-lookup"><span data-stu-id="5a314-144">Regardless of hello connectivity model, an ExpressRoute circuit has toobe created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="5a314-145">Een ExpressRoute-circuit inrichten, stelt u een redundante laag-2-verbindingen tussen PE-msee's (4) en de msee's (5).</span><span class="sxs-lookup"><span data-stu-id="5a314-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="5a314-146">Zie voor meer informatie over hoe toocreate, wijzigen, inrichten en een ExpressRoute-circuit controleren Hallo artikel [maken en een ExpressRoute-circuit wijzigen][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="5a314-146">For more information on how toocreate, modify, provision, and verify an ExpressRoute circuit, see hello article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="5a314-147">Een servicesleutel is een unieke identificatie voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="5a314-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="5a314-148">Deze sleutel is vereist voor de meeste Hallo powershell-opdrachten die in dit document worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="5a314-148">This key is required for most of hello powershell commands mentioned in this document.</span></span> <span data-ttu-id="5a314-149">Bovendien moet u hulp nodig hebt van Microsoft of van een ExpressRoute-partner tootroubleshoot een probleem met ExpressRoute, Hallo service leveren sleutel tooreadily Hallo circuit identificeren.</span><span class="sxs-lookup"><span data-stu-id="5a314-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner tootroubleshoot an ExpressRoute issue, provide hello service key tooreadily identify hello circuit.</span></span>
>
>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="5a314-150">Verificatie via hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="5a314-150">Verification via hello Azure portal</span></span>
<span data-ttu-id="5a314-151">In hello Azure-portal, Hallo status van een ExpressRoute-circuit kan worden gecontroleerd door het selecteren van ![2][2] Hallo ExpressRoute-circuit op Hallo links zijmarge menu en vervolgens te selecteren.</span><span class="sxs-lookup"><span data-stu-id="5a314-151">In hello Azure portal, hello status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="5a314-152">Selecteren van een ExpressRoute circuit vermeld onder 'Alle resources' hello ExpressRoute-circuit blade geopend.</span><span class="sxs-lookup"><span data-stu-id="5a314-152">Selecting an ExpressRoute circuit listed under "All resources" opens hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="5a314-153">In Hallo ![3][3] sectie van Hallo blade Hallo ExpressRoute essentials worden vermeld, zoals wordt weergegeven in de volgende schermopname Hallo:</span><span class="sxs-lookup"><span data-stu-id="5a314-153">In hello ![3][3] section of hello blade, hello ExpressRoute essentials are listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="5a314-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="5a314-154">![4][4]</span></span>    

<span data-ttu-id="5a314-155">In Hallo ExpressRoute Essentials *Circuit status* Hallo status van de Hallo circuit op Hallo Microsoft side aangeeft.</span><span class="sxs-lookup"><span data-stu-id="5a314-155">In hello ExpressRoute Essentials, *Circuit status* indicates hello status of hello circuit on hello Microsoft side.</span></span> <span data-ttu-id="5a314-156">*Providerstatus* geeft aan of Hallo circuit is *ingericht/niet ingericht* Hallo serviceprovider zijde.</span><span class="sxs-lookup"><span data-stu-id="5a314-156">*Provider status* indicates if hello circuit has been *Provisioned/Not provisioned* on hello service-provider side.</span></span> 

<span data-ttu-id="5a314-157">Voor een ExpressRoute-circuit toobe operationele, Hallo *Circuit status* moet *ingeschakeld* en Hallo *providerstatus* moet *ingericht*.</span><span class="sxs-lookup"><span data-stu-id="5a314-157">For an ExpressRoute circuit toobe operational, hello *Circuit status* must be *Enabled* and hello *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="5a314-158">Als hello *Circuit status* is niet ingeschakeld, neem contact op met [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="5a314-158">If hello *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="5a314-159">Als hello *providerstatus* is niet ingericht, neem contact op met uw serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="5a314-159">If hello *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="5a314-160">Verificatie via PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a314-160">Verification via PowerShell</span></span>
<span data-ttu-id="5a314-161">toolist alle Hallo ExpressRoute-circuits in een resourcegroep, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5a314-161">toolist all hello ExpressRoute circuits in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="5a314-162">U kunt de naam van uw resourcegroep ophalen via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5a314-162">You can get your resource group name through hello Azure portal.</span></span> <span data-ttu-id="5a314-163">Zie de vorige subsectie Hallo van dit document en houd er rekening mee dat naam resourcegroep Hallo Hallo voorbeeld schermopname wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="5a314-163">See hello previous subsection of this document and note that hello resource group name is listed in hello example screen shot.</span></span>
>
>

<span data-ttu-id="5a314-164">tooselect een bepaalde ExpressRoute-circuit in een resourcegroep of gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5a314-164">tooselect a particular ExpressRoute circuit in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="5a314-165">Er is een voorbeeldantwoord:</span><span class="sxs-lookup"><span data-stu-id="5a314-165">A sample response is:</span></span>

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

<span data-ttu-id="5a314-166">tooconfirm als een ExpressRoute-circuit functioneert, betalen bijzondere aandacht toohello velden te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a314-166">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="5a314-167">Als hello *CircuitProvisioningState* is niet ingeschakeld, neem contact op met [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="5a314-167">If hello *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="5a314-168">Als hello *ServiceProviderProvisioningState* is niet ingericht, neem contact op met uw serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="5a314-168">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="5a314-169">Verificatie via PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="5a314-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="5a314-170">toolist alle Hallo ExpressRoute-circuits voor een abonnement, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5a314-170">toolist all hello ExpressRoute circuits under a subscription, use hello following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="5a314-171">tooselect een bepaalde ExpressRoute-circuit Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5a314-171">tooselect a particular ExpressRoute circuit, use hello following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="5a314-172">Er is een voorbeeldantwoord:</span><span class="sxs-lookup"><span data-stu-id="5a314-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="5a314-173">tooconfirm als een ExpressRoute-circuit functioneert, betaalt u speciale aandacht toohello velden te volgen: ServiceProviderProvisioningState: Status ingericht: ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="5a314-173">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="5a314-174">Als hello *Status* is niet ingeschakeld, neem contact op met [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="5a314-174">If hello *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="5a314-175">Als hello *ServiceProviderProvisioningState* is niet ingericht, neem contact op met uw serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="5a314-175">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="5a314-176">Peeringconfiguratie valideren</span><span class="sxs-lookup"><span data-stu-id="5a314-176">Validate Peering Configuration</span></span>
<span data-ttu-id="5a314-177">Nadat het Hallo-aanbieder heeft voltooide Hallo Hallo ExpressRoute-circuit inrichten, kan een routeringsconfiguratie worden gemaakt via Hallo ExpressRoute-circuit tussen de MSEE-PRs (4) en de msee's (5).</span><span class="sxs-lookup"><span data-stu-id="5a314-177">After hello service provider has completed hello provisioning hello ExpressRoute circuit, a routing configuration can be created over hello ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="5a314-178">Elk ExpressRoute-circuit kan hebben een, twee of drie routing-contexten ingeschakeld: persoonlijke Azure-peering (verkeer tooprivate virtuele netwerken in Azure) en Microsoft-peering (verkeer tooOffice 365 openbare Azure-peering (verkeer toopublic IP-adressen in Azure) (en Dynamics 365).</span><span class="sxs-lookup"><span data-stu-id="5a314-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic tooprivate virtual networks in Azure), Azure public peering (traffic toopublic IP addresses in Azure), and Microsoft peering (traffic tooOffice 365 and Dynamics 365).</span></span> <span data-ttu-id="5a314-179">Voor meer informatie over het toocreate en routeringsconfiguratie wijzigen, Zie het artikel Hallo [maken en wijzigen van routering voor een ExpressRoute-circuit][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="5a314-179">For more information on how toocreate and modify routing configuration, see hello article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="5a314-180">Verificatie via hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="5a314-180">Verification via hello Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="5a314-181">Er is een bekend probleem in hello Azure-portal ExpressRoute peerings zijn, waarbij de *niet* wordt weergegeven in het Hallo-portal als geconfigureerd door Hallo-provider.</span><span class="sxs-lookup"><span data-stu-id="5a314-181">There is a known bug in hello Azure portal wherein ExpressRoute peerings are *NOT* shown in hello portal if configured by hello service provider.</span></span> <span data-ttu-id="5a314-182">Toevoegen van ExpressRoute-peerings via Hallo portal of PowerShell *overschrijft Hallo service Providerinstellingen*.</span><span class="sxs-lookup"><span data-stu-id="5a314-182">Adding ExpressRoute peerings via hello portal or PowerShell *overwrites hello service provider settings*.</span></span> <span data-ttu-id="5a314-183">Deze actie wordt verbroken Hallo routering op Hallo ExpressRoute-circuit en vereist ondersteuning van Hallo service toorestore Hallo Providerinstellingen Hallo en herstellen van de normale routering.</span><span class="sxs-lookup"><span data-stu-id="5a314-183">This action breaks hello routing on hello ExpressRoute circuit and requires hello support of hello service provider toorestore hello settings and reestablish normal routing.</span></span> <span data-ttu-id="5a314-184">Hallo ExpressRoute peerings alleen wijzigen als deze bepaalde dat die Hallo serviceprovider biedt alleen een layer 2-services!</span><span class="sxs-lookup"><span data-stu-id="5a314-184">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="5a314-185">Als laag 3 is opgegeven door Hallo service provider en Hallo peerings leeg in Hallo-portal zijn, zijn PowerShell gebruikte toosee Hallo service-instellingen voor provider geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="5a314-185">If layer 3 is provided by hello service provider and hello peerings are blank in hello portal, PowerShell can be used toosee hello service provider configured settings.</span></span>
>
>

<span data-ttu-id="5a314-186">In hello Azure-portal, de status van een ExpressRoute-circuit kan worden gecontroleerd door te selecteren ![2][2] Hallo ExpressRoute-circuit op Hallo links zijmarge menu en vervolgens te selecteren.</span><span class="sxs-lookup"><span data-stu-id="5a314-186">In hello Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="5a314-187">Selecteren van een ExpressRoute zou circuit vermeld onder 'Alle resources' Hallo ExpressRoute-circuit blade geopend.</span><span class="sxs-lookup"><span data-stu-id="5a314-187">Selecting an ExpressRoute circuit listed under "All resources" would open hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="5a314-188">In Hallo ![3][3] sectie van Hallo blade Hallo ExpressRoute essentials zou worden weergegeven, zoals wordt weergegeven in de volgende schermopname Hallo:</span><span class="sxs-lookup"><span data-stu-id="5a314-188">In hello ![3][3] section of hello blade, hello ExpressRoute essentials would be listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="5a314-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="5a314-189">![5][5]</span></span>

<span data-ttu-id="5a314-190">In de Hallo voorgaande voorbeeld, als vermelde Azure is persoonlijke peering routering context ingeschakeld, terwijl Azure openbare en Microsoft peering routing-contexten zijn niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5a314-190">In hello preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="5a314-191">Een context die peering is ingeschakeld, moet ook Hallo primaire en secundaire point-to-point (vereist voor BGP)-subnetten die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="5a314-191">A successfully enabled peering context would also have hello primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="5a314-192">Hallo /30 subnetten worden gebruikt voor het Hallo-interface IP-adres Hallo msee's en PE-msee's.</span><span class="sxs-lookup"><span data-stu-id="5a314-192">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="5a314-193">Als een peering niet is ingeschakeld, controleert u als Hallo primaire en secundaire subnetten toegewezen overeenkomen Hallo-configuratie op PE-msee's.</span><span class="sxs-lookup"><span data-stu-id="5a314-193">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on PE-MSEEs.</span></span> <span data-ttu-id="5a314-194">Als geen toochange Hallo configuratie op MSEE-routers, raadpleeg dan te[maken en wijzigen van routering voor een ExpressRoute-circuit][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="5a314-194">If not, toochange hello configuration on MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="5a314-195">Verificatie via PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a314-195">Verification via PowerShell</span></span>
<span data-ttu-id="5a314-196">tooget hello Azure persoonlijke peering configuratiedetails Hallo volgende opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5a314-196">tooget hello Azure private peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="5a314-197">Een antwoord voorbeeld voor een correct geconfigureerde persoonlijke peering, is:</span><span class="sxs-lookup"><span data-stu-id="5a314-197">A sample response, for a successfully configured private peering, is:</span></span>

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 <span data-ttu-id="5a314-198">Een context die is ingeschakeld peering moet Hallo primaire en secundaire adresvoorvoegsels vermeld.</span><span class="sxs-lookup"><span data-stu-id="5a314-198">A successfully enabled peering context would have hello primary and secondary address prefixes listed.</span></span> <span data-ttu-id="5a314-199">Hallo /30 subnetten worden gebruikt voor het Hallo-interface IP-adres Hallo msee's en PE-msee's.</span><span class="sxs-lookup"><span data-stu-id="5a314-199">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="5a314-200">tooget hello Azure openbare peering configuratiedetails Hallo opdrachten na gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5a314-200">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="5a314-201">tooget hello Microsoft peering configuratiedetails Hallo volgende opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5a314-201">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="5a314-202">Als een peering niet is geconfigureerd, zou er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5a314-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="5a314-203">Een voorbeeldantwoord wanneer Hallo vermeld peering (Azure openbare peering in dit voorbeeld) niet is geconfigureerd binnen Hallo circuit:</span><span class="sxs-lookup"><span data-stu-id="5a314-203">A sample response, when hello stated peering (Azure Public peering in this example) is not configured within hello circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="5a314-204">Als een peering niet is ingeschakeld, controleert u of de primaire en secundaire subnetten toegewezen overeen Hallo-configuratie op Hallo Hallo PE MSEE gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="5a314-204">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="5a314-205">Ook controleren of hello corrigeren *VlanId*, *AzureASN*, en *PeerASN* op msee's worden gebruikt en als deze waarden worden toegewezen toohello zijn gebruikt op Hallo gekoppeld PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a314-205">Also check if hello correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="5a314-206">Als MD5-hash is gekozen, is Hallo gedeelde sleutel moet hetzelfde zijn op de combinatie van MSEE en PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a314-206">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="5a314-207">toochange Hallo-configuratie op Hallo MSEE-routers te verwijzen [maken en wijzigen van routering voor een ExpressRoute-circuit] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="5a314-207">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="5a314-208">Verificatie via PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="5a314-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="5a314-209">tooget hello Azure persoonlijke peering configuratiedetails Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5a314-209">tooget hello Azure private peering configuration details, use hello following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="5a314-210">Is een reactie voorbeeld voor een persoonlijke peering Prestatietesten zijn geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="5a314-210">A sample response, for a successfully configured private peering is:</span></span>

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

<span data-ttu-id="5a314-211">Een ingeschakeld is, peering context Hallo primaire en secundaire peer subnetten vermeld zou hebben.</span><span class="sxs-lookup"><span data-stu-id="5a314-211">A successfully, enabled peering context would have hello primary and secondary peer subnets listed.</span></span> <span data-ttu-id="5a314-212">Hallo /30 subnetten worden gebruikt voor het Hallo-interface IP-adres Hallo msee's en PE-msee's.</span><span class="sxs-lookup"><span data-stu-id="5a314-212">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="5a314-213">tooget hello Azure openbare peering configuratiedetails Hallo opdrachten na gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5a314-213">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="5a314-214">tooget hello Microsoft peering configuratiedetails Hallo volgende opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5a314-214">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="5a314-215">Als laag 3-peerings zijn ingesteld door de serviceprovider hello, overschreven Hallo ExpressRoute peerings via Hallo portal of PowerShell instellen Hallo serviceprovider instellingen.</span><span class="sxs-lookup"><span data-stu-id="5a314-215">If layer 3 peerings were set by hello service provider, setting hello ExpressRoute peerings via hello portal or PowerShell overwrites hello service provider settings.</span></span> <span data-ttu-id="5a314-216">Opnieuw instellen van Hallo side peering Providerinstellingen vereist Hallo-ondersteuning van Hallo-provider.</span><span class="sxs-lookup"><span data-stu-id="5a314-216">Resetting hello provider side peering settings requires hello support of hello service provider.</span></span> <span data-ttu-id="5a314-217">Hallo ExpressRoute peerings alleen wijzigen als deze bepaalde dat die Hallo serviceprovider biedt alleen een layer 2-services!</span><span class="sxs-lookup"><span data-stu-id="5a314-217">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="5a314-218">Als een peering niet is ingeschakeld, controleert u of Hallo primaire en secundaire peer subnetten toegewezen overeen Hallo-configuratie op Hallo PE MSEE gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="5a314-218">If a peering is not enabled, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="5a314-219">Ook controleren of hello corrigeren *VlanId*, *AzureAsn*, en *PeerAsn* op msee's worden gebruikt en als deze waarden worden toegewezen toohello zijn gebruikt op Hallo gekoppeld PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a314-219">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="5a314-220">toochange Hallo-configuratie op Hallo MSEE-routers te verwijzen [maken en wijzigen van routering voor een ExpressRoute-circuit] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="5a314-220">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a><span data-ttu-id="5a314-221">ARP tussen Microsoft en Hallo serviceprovider valideren</span><span class="sxs-lookup"><span data-stu-id="5a314-221">Validate ARP between Microsoft and hello service provider</span></span>
<span data-ttu-id="5a314-222">Deze sectie wordt gebruikt (klassiek) PowerShell-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="5a314-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="5a314-223">Als u PowerShell Azure Resource Manager-opdrachten gebruikt hebt, zorg ervoor dat er beheerder/co-beheerder toegang toohello abonnement via de [klassieke Azure-portal][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="5a314-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="5a314-224">Voor het oplossen van problemen met Azure Resource Manager opdrachten raadpleegt u toohello [ARP ophalen van tabellen in de Resource Manager-implementatiemodel Hallo] [ ARP] document.</span><span class="sxs-lookup"><span data-stu-id="5a314-224">For troubleshooting using Azure Resource Manager commands please refer toohello [Getting ARP tables in hello Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="5a314-225">tooget ARP, zowel hello Azure-portal en Azure Resource Manager PowerShell-opdrachten kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5a314-225">tooget ARP, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="5a314-226">Als er fouten optreden met hello Azure Resource Manager PowerShell-opdrachten, klassieke PowerShell-opdrachten gebruiken als klassieke PowerShell opdrachten ook worden gebruikt met Azure Resource Manager ExpressRoute-circuits.</span><span class="sxs-lookup"><span data-stu-id="5a314-226">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="5a314-227">tooget ARP-tabel uit de primaire MSEE router voor persoonlijke peering Hallo Hallo Hallo, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5a314-227">tooget hello ARP table from hello primary MSEE router for hello private peering, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="5a314-228">Een voorbeeld van antwoord voor Hallo-opdracht in Hallo geslaagde scenario:</span><span class="sxs-lookup"><span data-stu-id="5a314-228">An example response for hello command, in hello successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="5a314-229">Op deze manier kunt u controleren Hallo ARP-tabel uit Hallo MSEE in Hallo *primaire*/*secundaire* pad voor *persoonlijke* /  *Openbare*/*Microsoft* peerings.</span><span class="sxs-lookup"><span data-stu-id="5a314-229">Similarly, you can check hello ARP table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="5a314-230">Hallo bestaat volgende voorbeeld toont Hallo respons van Hallo-opdracht voor een peering niet.</span><span class="sxs-lookup"><span data-stu-id="5a314-230">hello following example shows hello response of hello command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="5a314-231">Als Hallo ARP-tabel geen heeft toegewezen IP-adressen van de interfaces Hallo tooMAC adressen, bekijk Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="5a314-231">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
>1. <span data-ttu-id="5a314-232">Als het eerste IP-adres Hallo van Hallo /30 subnet voor Hallo koppeling tussen toegewezen Hallo MSEE PR en MSEE wordt gebruikt op Hallo-interface van MSEE PR.</span><span class="sxs-lookup"><span data-stu-id="5a314-232">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="5a314-233">Azure gebruikt altijd Hallo tweede IP-adres voor de msee's.</span><span class="sxs-lookup"><span data-stu-id="5a314-233">Azure always uses hello second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="5a314-234">Controleer of als Hallo klant (C-code) en VLAN-servicetags (S-Tag) overeenkomt met beide op een combinatie van MSEE PR en MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a314-234">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a><span data-ttu-id="5a314-235">BGP-routes op Hallo MSEE en valideren</span><span class="sxs-lookup"><span data-stu-id="5a314-235">Validate BGP and routes on hello MSEE</span></span>
<span data-ttu-id="5a314-236">Deze sectie wordt gebruikt (klassiek) PowerShell-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="5a314-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="5a314-237">Als u PowerShell Azure Resource Manager-opdrachten gebruikt hebt, zorg ervoor dat er beheerder/co-beheerder toegang toohello abonnement via de [klassieke Azure-portal][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="5a314-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="5a314-238">tooget BGP gegevens, zowel hello Azure-portal en Azure Resource Manager PowerShell-opdrachten kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5a314-238">tooget BGP information, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="5a314-239">Als er fouten optreden met hello Azure Resource Manager PowerShell-opdrachten, klassieke PowerShell-opdrachten gebruiken als klassieke PowerShell opdrachten ook worden gebruikt met Azure Resource Manager ExpressRoute-circuits.</span><span class="sxs-lookup"><span data-stu-id="5a314-239">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="5a314-240">tooget Hallo routeringstabel (neighbor BGP) voor een bepaalde routering context samenvatting, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5a314-240">tooget hello routing table (BGP neighbor) summary for a particular routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="5a314-241">Er is een voorbeeld van antwoord:</span><span class="sxs-lookup"><span data-stu-id="5a314-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="5a314-242">Zoals u in het voorgaande voorbeeld Hallo, is Hallo opdracht nuttig toodetermine voor hoe lang Hallo routering context is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5a314-242">As shown in hello preceding example, hello command is useful toodetermine for how long hello routing context has been established.</span></span> <span data-ttu-id="5a314-243">Het aantal route voorvoegsels die worden geadverteerd door de peering router hello wordt tevens aangegeven.</span><span class="sxs-lookup"><span data-stu-id="5a314-243">It also indicates number of route prefixes advertised by hello peering router.</span></span>

>[!NOTE]
><span data-ttu-id="5a314-244">Als Hallo status in actief of inactief, controleert u of Hallo primaire en secundaire peer subnetten toegewezen overeen Hallo-configuratie op Hallo PE MSEE gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="5a314-244">If hello state is in Active or Idle, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="5a314-245">Ook controleren of hello corrigeren *VlanId*, *AzureAsn*, en *PeerAsn* op msee's worden gebruikt en als deze waarden worden toegewezen toohello zijn gebruikt op Hallo gekoppeld PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a314-245">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="5a314-246">Als MD5-hash is gekozen, is Hallo gedeelde sleutel moet hetzelfde zijn op de combinatie van MSEE en PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a314-246">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="5a314-247">toochange Hallo-configuratie op Hallo MSEE-routers te verwijzen[maken en wijzigen van routering voor een ExpressRoute-circuit][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="5a314-247">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="5a314-248">Als bepaalde bestemmingen niet bereikbaar via een bepaalde peering zijn, controleert u de routetabel Hallo van Hallo msee's die horen toohello bepaalde peering context.</span><span class="sxs-lookup"><span data-stu-id="5a314-248">If certain destinations are not reachable over a particular peering, check hello route table of hello MSEEs belonging toohello particular peering context.</span></span> <span data-ttu-id="5a314-249">Als een overeenkomende voorvoegsel (kan worden NATed IP) in de routeringstabel Hallo aanwezig is, moet u controleren als er firewalls / / ACL's voor NSG op Hallo pad, en als ze Hallo verkeer is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="5a314-249">If a matching prefix (could be NATed IP) is present in hello routing table, then check if there are firewalls/NSG/ACLs on hello path and if they permit hello traffic.</span></span>
>
>

<span data-ttu-id="5a314-250">tooget hello volledige routeringstabel van de MSEE op Hallo *primaire* pad voor bepaalde Hallo *persoonlijke* routering context, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5a314-250">tooget hello full routing table from MSEE on hello *Primary* path for hello particular *Private* routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="5a314-251">Een geslaagde uitkomst voorbeeld voor Hallo-opdracht is:</span><span class="sxs-lookup"><span data-stu-id="5a314-251">An example successful outcome for hello command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="5a314-252">Op deze manier kunt u de routeringstabel Hallo van Hallo MSEE in Hallo controleren *primaire*/*secundaire* pad voor *persoonlijke* / *Openbare*/*Microsoft* een peering context.</span><span class="sxs-lookup"><span data-stu-id="5a314-252">Similarly, you can check hello routing table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="5a314-253">Hallo bestaat volgende voorbeeld toont Hallo respons van Hallo-opdracht voor een peering niet:</span><span class="sxs-lookup"><span data-stu-id="5a314-253">hello following example shows hello response of hello command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a><span data-ttu-id="5a314-254">Hallo verkeer statistieken controleren</span><span class="sxs-lookup"><span data-stu-id="5a314-254">Check hello Traffic Statistics</span></span>
<span data-ttu-id="5a314-255">Hallo tooget gecombineerd primaire en secundaire pad verkeer statistieken--bytes in en uit--van een peering context, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5a314-255">tooget hello combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="5a314-256">Er is een voorbeeld van uitvoer van Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="5a314-256">A sample output of hello command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="5a314-257">Er is een voorbeeld van uitvoer van de opdracht Hallo voor een niet-bestaande peering:</span><span class="sxs-lookup"><span data-stu-id="5a314-257">A sample output of hello command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="5a314-258">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a314-258">Next Steps</span></span>
<span data-ttu-id="5a314-259">Bekijk voor meer informatie en hulp Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a314-259">For more information or help, check out hello following links:</span></span>

- <span data-ttu-id="5a314-260">[Microsoft-ondersteuning][Support]</span><span class="sxs-lookup"><span data-stu-id="5a314-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="5a314-261">[Maken en een ExpressRoute-circuit wijzigen][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="5a314-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="5a314-262">[Maken en aanpassen van routering voor een ExpressRoute-circuit][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="5a314-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logische Express Route-verbinding"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Pictogram voor alle resources"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Overzicht-pictogram"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Schermopname van ExpressRoute Essentials-voorbeeld"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Schermopname van ExpressRoute Essentials-voorbeeld"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






