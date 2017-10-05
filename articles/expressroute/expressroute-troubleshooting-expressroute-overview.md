---
title: 'Controleren of verbinding: Azure ExpressRoute Troubleshooting Guide | Microsoft Docs'
description: Deze pagina vindt u instructies voor het oplossen van problemen en valideren van de connectiviteit van de end-to-end van een ExpressRoute-circuit.
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
ms.openlocfilehash: 5a6360b56963d219ab576fb3e2636b6c51dd72ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="ccca4-103">ExpressRoute-verbinding controleren</span><span class="sxs-lookup"><span data-stu-id="ccca4-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="ccca4-104">ExpressRoute, die een uitbreiding is een on-premises netwerk via een persoonlijke verbinding die wordt gefaciliteerd door een connectiviteitsprovider in de Microsoft cloud, omvat de volgende drie afzonderlijke netwerkzones:</span><span class="sxs-lookup"><span data-stu-id="ccca4-104">ExpressRoute, which extends an on-premises network into the Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves the following three distinct network zones:</span></span>

-   <span data-ttu-id="ccca4-105">Klantnetwerk</span><span class="sxs-lookup"><span data-stu-id="ccca4-105">Customer Network</span></span>
-   <span data-ttu-id="ccca4-106">Serviceprovider-netwerk</span><span class="sxs-lookup"><span data-stu-id="ccca4-106">Provider Network</span></span>
-   <span data-ttu-id="ccca4-107">Microsoft-datacentrum</span><span class="sxs-lookup"><span data-stu-id="ccca4-107">Microsoft Datacenter</span></span>

<span data-ttu-id="ccca4-108">Het doel van dit document is zodat de gebruiker om te bepalen waar u (of zelfs als) een verbindingsprobleem bestaat en in welke zone, waardoor te zoeken naar Help-informatie van het juiste team om het probleem te verhelpen.</span><span class="sxs-lookup"><span data-stu-id="ccca4-108">The purpose of this document is to help user to identify where (or even if) a connectivity issue exists and within which zone, thereby to seek help from appropriate team to resolve the issue.</span></span> <span data-ttu-id="ccca4-109">Als Microsoft ondersteuning nodig is een probleem op te lossen, opent u een ondersteuningsticket met [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="ccca4-109">If Microsoft support is needed to resolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccca4-110">Dit document is bedoeld om u te helpen opsporen en oplossen van eenvoudige problemen.</span><span class="sxs-lookup"><span data-stu-id="ccca4-110">This document is intended to help diagnosing and fixing simple issues.</span></span> <span data-ttu-id="ccca4-111">Het is niet bedoeld als vervanging voor ondersteuning van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ccca4-111">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="ccca4-112">Open een ondersteuningsticket met [Microsoft Support] [ Support] als u niet voor het oplossen van het probleem op door middel van de richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="ccca4-112">Open a support ticket with [Microsoft Support][Support] if you are unable to solve the problem using the guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="ccca4-113">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ccca4-113">Overview</span></span>
<span data-ttu-id="ccca4-114">Het volgende diagram toont de logische verbindingen van een klantnetwerk met Microsoft-netwerk met behulp van ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ccca4-114">The following diagram shows the logical connectivity of a customer network to Microsoft network using ExpressRoute.</span></span>
<span data-ttu-id="ccca4-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="ccca4-115">[![1]][1]</span></span>

<span data-ttu-id="ccca4-116">De getallen geven in het voorgaande diagram netwerk belangrijke punten.</span><span class="sxs-lookup"><span data-stu-id="ccca4-116">In the preceding diagram, the numbers indicate key network points.</span></span> <span data-ttu-id="ccca4-117">De netwerk-punten zijn vaak in dit artikel verwezen door hun bijbehorende nummers.</span><span class="sxs-lookup"><span data-stu-id="ccca4-117">The network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="ccca4-118">Afhankelijk van het ExpressRoute-connectiviteit model (Cloud Exchange CO-locatie, Point-to-Point Ethernet-verbinding of Any-to-any (IPVPN)) mogelijk de netwerk-punten 3 en 4 switches (Layer 2-apparaten).</span><span class="sxs-lookup"><span data-stu-id="ccca4-118">Depending on the ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) the network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="ccca4-119">De belangrijkste netwerk punten geïllustreerd zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="ccca4-119">The key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="ccca4-120">Klant compute-apparaat (bijvoorbeeld een server of een PC)</span><span class="sxs-lookup"><span data-stu-id="ccca4-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="ccca4-121">CEs: Klant-randrouters</span><span class="sxs-lookup"><span data-stu-id="ccca4-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="ccca4-122">PEs (CE facing): Provider rand routers/schakelaars waarmee worden geconfronteerd randrouters klant.</span><span class="sxs-lookup"><span data-stu-id="ccca4-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="ccca4-123">Genoemd PE CEs in dit document.</span><span class="sxs-lookup"><span data-stu-id="ccca4-123">Referred to as PE-CEs in this document.</span></span>
4.  <span data-ttu-id="ccca4-124">PEs (MSEE facing): Provider rand routers/schakelaars waarmee worden geconfronteerd msee's.</span><span class="sxs-lookup"><span data-stu-id="ccca4-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="ccca4-125">Genoemd PE-msee's in dit document.</span><span class="sxs-lookup"><span data-stu-id="ccca4-125">Referred to as PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="ccca4-126">Msee's: Microsoft Enterprise Edge (MSEE) ExpressRoute-routers</span><span class="sxs-lookup"><span data-stu-id="ccca4-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="ccca4-127">De Gateway virtuele netwerk (VNet)</span><span class="sxs-lookup"><span data-stu-id="ccca4-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="ccca4-128">COMPUTE-apparaat op het Azure VNet</span><span class="sxs-lookup"><span data-stu-id="ccca4-128">Compute device on the Azure VNet</span></span>

<span data-ttu-id="ccca4-129">Als u de connectiviteitsmodellen Cloud Exchange CO-locatie of Point-to-Point Ethernet-verbinding gebruikt, zou de router van de klant rand (2) tot stand brengen BGP-peer met msee's (5).</span><span class="sxs-lookup"><span data-stu-id="ccca4-129">If the Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, the customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="ccca4-130">Netwerk punten 3 en 4 wordt nog steeds aanwezig zijn, maar enigszins transparant als Layer 2-apparaten.</span><span class="sxs-lookup"><span data-stu-id="ccca4-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="ccca4-131">Als het model van de connectiviteit Any-to-any (IPVPN) wordt gebruikt, de PEs (MSEE facing) (4) zou tot stand brengen BGP-peer met msee's (5).</span><span class="sxs-lookup"><span data-stu-id="ccca4-131">If the Any-to-any (IPVPN) connectivity model is used, the PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="ccca4-132">Routes wilt vervolgens terug naar de klantnetwerk via de IPVPN serviceprovider-netwerk doorgeven.</span><span class="sxs-lookup"><span data-stu-id="ccca4-132">Routes would then propagate back to the customer network via the IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="ccca4-133">Microsoft vereist voor ExpressRoute hoge beschikbaarheid, een paar redundante BGP-sessies tussen de msee's (5) en PE-msee's (4).</span><span class="sxs-lookup"><span data-stu-id="ccca4-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="ccca4-134">Een paar redundante netwerkpaden wordt ook aangemoedigd tussen klantnetwerk en PE CEs.</span><span class="sxs-lookup"><span data-stu-id="ccca4-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="ccca4-135">In Any-to-any (IPVPN) verbinding model mogen echter een enkel CE-apparaat (2) worden verbonden met een of meer PEs (3).</span><span class="sxs-lookup"><span data-stu-id="ccca4-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected to one or more PEs (3).</span></span>
>
>

<span data-ttu-id="ccca4-136">Voor het valideren van een ExpressRoute-circuit, worden de volgende stappen uit (met het netwerkpunt aangegeven door het bijbehorende nummer) behandeld:</span><span class="sxs-lookup"><span data-stu-id="ccca4-136">To validate an ExpressRoute circuit, the following steps are covered (with the network point indicated by the associated number):</span></span>
1. [<span data-ttu-id="ccca4-137">Valideren van circuitinrichting en status (5)</span><span class="sxs-lookup"><span data-stu-id="ccca4-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="ccca4-138">Valideren van ten minste één ExpressRoute-peering is geconfigureerd (5)</span><span class="sxs-lookup"><span data-stu-id="ccca4-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="ccca4-139">Valideren van ARP tussen Microsoft en de service provider (koppeling tussen 4 en 5)</span><span class="sxs-lookup"><span data-stu-id="ccca4-139">Validate ARP between Microsoft and the service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="ccca4-140">Valideren van BGP en routes op de MSEE (BGP tussen 4 en 5 en 5 tot en met 6 als een VNet is verbonden)</span><span class="sxs-lookup"><span data-stu-id="ccca4-140">Validate BGP and routes on the MSEE (BGP between 4 to 5, and 5 to 6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="ccca4-141">Controleer de statistieken verkeer (verkeer doorlopen 5)</span><span class="sxs-lookup"><span data-stu-id="ccca4-141">Check the Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="ccca4-142">Meer validaties en controles worden toegevoegd in de toekomst, controle terug maandelijks!</span><span class="sxs-lookup"><span data-stu-id="ccca4-142">More validations and checks will be added in the future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="ccca4-143">Valideren van circuitinrichting en status</span><span class="sxs-lookup"><span data-stu-id="ccca4-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="ccca4-144">Ongeacht het model connectiviteit een ExpressRoute-circuit moet worden gemaakt en dus een servicesleutel gegenereerd voor het inrichten van het circuit.</span><span class="sxs-lookup"><span data-stu-id="ccca4-144">Regardless of the connectivity model, an ExpressRoute circuit has to be created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="ccca4-145">Een ExpressRoute-circuit inrichten, stelt u een redundante laag-2-verbindingen tussen PE-msee's (4) en de msee's (5).</span><span class="sxs-lookup"><span data-stu-id="ccca4-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="ccca4-146">Zie het artikel voor meer informatie over het maken, wijzigen, inrichten en een ExpressRoute-circuit controleren [maken en een ExpressRoute-circuit wijzigen][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="ccca4-146">For more information on how to create, modify, provision, and verify an ExpressRoute circuit, see the article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="ccca4-147">Een servicesleutel is een unieke identificatie voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="ccca4-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="ccca4-148">Deze sleutel is vereist voor het merendeel van de powershell-opdrachten die in dit document worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="ccca4-148">This key is required for most of the powershell commands mentioned in this document.</span></span> <span data-ttu-id="ccca4-149">Ook nodig u hulp hebt van Microsoft of van een ExpressRoute-partner voor een ExpressRoute-probleem kunt oplossen, geeft u de sleutel voor het circuit gemakkelijk te identificeren.</span><span class="sxs-lookup"><span data-stu-id="ccca4-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner to troubleshoot an ExpressRoute issue, provide the service key to readily identify the circuit.</span></span>
>
>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="ccca4-150">Verificatie via de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="ccca4-150">Verification via the Azure portal</span></span>
<span data-ttu-id="ccca4-151">In de Azure portal, de status van een ExpressRoute-circuit kan worden gecontroleerd door het selecteren van ![2][2] in het menu links zijmarge en vervolgens te klikken op het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="ccca4-151">In the Azure portal, the status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="ccca4-152">Selecteren van een ExpressRoute circuit vermeld onder 'Alle resources' de ExpressRoute-circuit blade geopend.</span><span class="sxs-lookup"><span data-stu-id="ccca4-152">Selecting an ExpressRoute circuit listed under "All resources" opens the ExpressRoute circuit blade.</span></span> <span data-ttu-id="ccca4-153">In de ![3][3] sectie van de blade de ExpressRoute essentials worden vermeld, zoals wordt weergegeven in de volgende schermopname:</span><span class="sxs-lookup"><span data-stu-id="ccca4-153">In the ![3][3] section of the blade, the ExpressRoute essentials are listed as shown in the following screen shot:</span></span>

<span data-ttu-id="ccca4-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="ccca4-154">![4][4]</span></span>    

<span data-ttu-id="ccca4-155">In de Essentials ExpressRoute *Circuit status* geeft de status van het circuit aan de kant van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ccca4-155">In the ExpressRoute Essentials, *Circuit status* indicates the status of the circuit on the Microsoft side.</span></span> <span data-ttu-id="ccca4-156">*Providerstatus* geeft aan of het circuit is *ingericht/niet ingericht* aan de kant van de serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="ccca4-156">*Provider status* indicates if the circuit has been *Provisioned/Not provisioned* on the service-provider side.</span></span> 

<span data-ttu-id="ccca4-157">Voor een ExpressRoute-circuit operationeel, de *Circuit status* moet *ingeschakeld* en de *providerstatus* moet *ingericht*.</span><span class="sxs-lookup"><span data-stu-id="ccca4-157">For an ExpressRoute circuit to be operational, the *Circuit status* must be *Enabled* and the *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="ccca4-158">Als de *Circuit status* is niet ingeschakeld, neem contact op met [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="ccca4-158">If the *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="ccca4-159">Als de *providerstatus* is niet ingericht, neem contact op met uw serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="ccca4-159">If the *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="ccca4-160">Verificatie via PowerShell</span><span class="sxs-lookup"><span data-stu-id="ccca4-160">Verification via PowerShell</span></span>
<span data-ttu-id="ccca4-161">Als de ExpressRoute-circuits in een resourcegroep weergeven, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ccca4-161">To list all the ExpressRoute circuits in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="ccca4-162">U kunt de naam van uw resourcegroep ophalen via de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ccca4-162">You can get your resource group name through the Azure portal.</span></span> <span data-ttu-id="ccca4-163">Zie de vorige subsectie van dit document en controleer of de naam van de resourcegroep wordt vermeld in de schermopname voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ccca4-163">See the previous subsection of this document and note that the resource group name is listed in the example screen shot.</span></span>
>
>

<span data-ttu-id="ccca4-164">Als u wilt een bepaalde ExpressRoute-circuit in een resourcegroep selecteren, moet u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ccca4-164">To select a particular ExpressRoute circuit in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="ccca4-165">Er is een voorbeeldantwoord:</span><span class="sxs-lookup"><span data-stu-id="ccca4-165">A sample response is:</span></span>

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

<span data-ttu-id="ccca4-166">Om te bevestigen of een ExpressRoute-circuit operationele speciale aandacht besteden aan de volgende velden:</span><span class="sxs-lookup"><span data-stu-id="ccca4-166">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="ccca4-167">Als de *CircuitProvisioningState* is niet ingeschakeld, neem contact op met [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="ccca4-167">If the *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="ccca4-168">Als de *ServiceProviderProvisioningState* is niet ingericht, neem contact op met uw serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="ccca4-168">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="ccca4-169">Verificatie via PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="ccca4-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="ccca4-170">Als de ExpressRoute-circuits voor een abonnement weergeven, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ccca4-170">To list all the ExpressRoute circuits under a subscription, use the following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="ccca4-171">Selecteer een bepaalde ExpressRoute-circuit, gebruik de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ccca4-171">To select a particular ExpressRoute circuit, use the following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="ccca4-172">Er is een voorbeeldantwoord:</span><span class="sxs-lookup"><span data-stu-id="ccca4-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="ccca4-173">Om te bevestigen of een ExpressRoute-circuit operationele speciale aandacht besteden aan de volgende velden: ServiceProviderProvisioningState: Status ingericht: ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="ccca4-173">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="ccca4-174">Als de *Status* is niet ingeschakeld, neem contact op met [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="ccca4-174">If the *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="ccca4-175">Als de *ServiceProviderProvisioningState* is niet ingericht, neem contact op met uw serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="ccca4-175">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="ccca4-176">Peeringconfiguratie valideren</span><span class="sxs-lookup"><span data-stu-id="ccca4-176">Validate Peering Configuration</span></span>
<span data-ttu-id="ccca4-177">Nadat de serviceprovider is voltooid de inrichting van het ExpressRoute-circuit, kan een routeringsconfiguratie worden gemaakt via de ExpressRoute-circuit tussen de MSEE-PRs (4) en de msee's (5).</span><span class="sxs-lookup"><span data-stu-id="ccca4-177">After the service provider has completed the provisioning the ExpressRoute circuit, a routing configuration can be created over the ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="ccca4-178">Elk ExpressRoute-circuit kan hebben een, twee of drie routing-contexten ingeschakeld: Azure persoonlijke peering (verkeer naar persoonlijke virtuele netwerken in Azure), Azure openbare peering (verkeer naar openbare IP-adressen in Azure) en Microsoft peering (verkeer met Office 365 en Dynamics 365).</span><span class="sxs-lookup"><span data-stu-id="ccca4-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic to private virtual networks in Azure), Azure public peering (traffic to public IP addresses in Azure), and Microsoft peering (traffic to Office 365 and Dynamics 365).</span></span> <span data-ttu-id="ccca4-179">Raadpleeg het artikel voor meer informatie over het maken en beheren van routeringsconfiguratie [maken en wijzigen van routering voor een ExpressRoute-circuit][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="ccca4-179">For more information on how to create and modify routing configuration, see the article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="ccca4-180">Verificatie via de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="ccca4-180">Verification via the Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="ccca4-181">Er is een bekend probleem in de Azure portal ExpressRoute peerings zijn, waarbij de *niet* weergegeven in de portal als geconfigureerd door de serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="ccca4-181">There is a known bug in the Azure portal wherein ExpressRoute peerings are *NOT* shown in the portal if configured by the service provider.</span></span> <span data-ttu-id="ccca4-182">Toevoegen van ExpressRoute-peerings via de portal of PowerShell *overschrijft de instellingen van de serviceprovider*.</span><span class="sxs-lookup"><span data-stu-id="ccca4-182">Adding ExpressRoute peerings via the portal or PowerShell *overwrites the service provider settings*.</span></span> <span data-ttu-id="ccca4-183">Deze actie wordt verbroken de routering op het ExpressRoute-circuit en de ondersteuning van de serviceprovider bij het herstel van de instellingen en herstellen normale routering vereist.</span><span class="sxs-lookup"><span data-stu-id="ccca4-183">This action breaks the routing on the ExpressRoute circuit and requires the support of the service provider to restore the settings and reestablish normal routing.</span></span> <span data-ttu-id="ccca4-184">De ExpressRoute-peerings alleen wijzigen als u zeker dat de serviceprovider alleen layer 2-services levert!</span><span class="sxs-lookup"><span data-stu-id="ccca4-184">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="ccca4-185">Als laag 3 wordt geleverd door de provider en de peerings leeg in de portal zijn, worden PowerShell gebruikt om te zien van de instellingen van de serviceprovider geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ccca4-185">If layer 3 is provided by the service provider and the peerings are blank in the portal, PowerShell can be used to see the service provider configured settings.</span></span>
>
>

<span data-ttu-id="ccca4-186">In de Azure portal, status van een ExpressRoute-circuit kan worden gecontroleerd door het selecteren van ![2][2] in het menu links zijmarge en vervolgens te klikken op het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="ccca4-186">In the Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="ccca4-187">Selecteren van een ExpressRoute opent circuit vermeld onder 'Alle resources' de ExpressRoute-circuit-blade.</span><span class="sxs-lookup"><span data-stu-id="ccca4-187">Selecting an ExpressRoute circuit listed under "All resources" would open the ExpressRoute circuit blade.</span></span> <span data-ttu-id="ccca4-188">In de ![3][3] sectie van de blade de ExpressRoute essentials zou worden weergegeven, zoals wordt weergegeven in de volgende schermopname:</span><span class="sxs-lookup"><span data-stu-id="ccca4-188">In the ![3][3] section of the blade, the ExpressRoute essentials would be listed as shown in the following screen shot:</span></span>

<span data-ttu-id="ccca4-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="ccca4-189">![5][5]</span></span>

<span data-ttu-id="ccca4-190">In het voorgaande voorbeeld als vermelde Azure is persoonlijke peering routering context ingeschakeld, terwijl Azure openbare en Microsoft peering routing-contexten zijn niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ccca4-190">In the preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="ccca4-191">Een context die peering is ingeschakeld, moet ook de primaire en secundaire point-to-point (vereist voor BGP)-subnetten die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="ccca4-191">A successfully enabled peering context would also have the primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="ccca4-192">Het/30-subnetten worden gebruikt voor de interface-IP-adres van de msee's en PE-msee's.</span><span class="sxs-lookup"><span data-stu-id="ccca4-192">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="ccca4-193">Als een peering niet is ingeschakeld, controleert u of de primaire en secundaire subnetten toegewezen overeenkomen met de configuratie voor PE-msee's.</span><span class="sxs-lookup"><span data-stu-id="ccca4-193">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on PE-MSEEs.</span></span> <span data-ttu-id="ccca4-194">Als dit niet het geval is, als u de configuratie op de MSEE-routers, Raadpleeg [maken en wijzigen van routering voor een ExpressRoute-circuit][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="ccca4-194">If not, to change the configuration on MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="ccca4-195">Verificatie via PowerShell</span><span class="sxs-lookup"><span data-stu-id="ccca4-195">Verification via PowerShell</span></span>
<span data-ttu-id="ccca4-196">Als u het Azure configuratiedetails van persoonlijke peering, gebruikt u de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="ccca4-196">To get the Azure private peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="ccca4-197">Een antwoord voorbeeld voor een correct geconfigureerde persoonlijke peering, is:</span><span class="sxs-lookup"><span data-stu-id="ccca4-197">A sample response, for a successfully configured private peering, is:</span></span>

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

 <span data-ttu-id="ccca4-198">Een context die peering is ingeschakeld, moet de primaire en secundaire adresvoorvoegsels vermeld.</span><span class="sxs-lookup"><span data-stu-id="ccca4-198">A successfully enabled peering context would have the primary and secondary address prefixes listed.</span></span> <span data-ttu-id="ccca4-199">Het/30-subnetten worden gebruikt voor de interface-IP-adres van de msee's en PE-msee's.</span><span class="sxs-lookup"><span data-stu-id="ccca4-199">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="ccca4-200">Als u Azure openbare peering configuratiedetails, gebruikt u de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="ccca4-200">To get the Azure public peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="ccca4-201">Als u de configuratiegegevens van de Microsoft-peering, gebruikt u de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="ccca4-201">To get the Microsoft peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="ccca4-202">Als een peering niet is geconfigureerd, zou er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ccca4-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="ccca4-203">Een voorbeeld-antwoord, wanneer de vermelde peering (Azure openbare peering in dit voorbeeld) niet is geconfigureerd in het circuit:</span><span class="sxs-lookup"><span data-stu-id="ccca4-203">A sample response, when the stated peering (Azure Public peering in this example) is not configured within the circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="ccca4-204">Als een peering niet is ingeschakeld, controleert u of de primaire en secundaire subnetten toegewezen overeenkomen met de configuratie op de gekoppelde PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="ccca4-204">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="ccca4-205">Controleer ook of de juiste *VlanId*, *AzureASN*, en *PeerASN* op msee's worden gebruikt en als deze waarden worden toegewezen aan de namen die op de gekoppelde PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="ccca4-205">Also check if the correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="ccca4-206">Als MD5-hash is gekozen, is de gedeelde sleutel moet hetzelfde zijn op de combinatie van MSEE en PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="ccca4-206">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="ccca4-207">Als u de configuratie op de MSEE-routers, verwijzen naar [maken en wijzigen van routering voor een ExpressRoute-circuit] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="ccca4-207">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="ccca4-208">Verificatie via PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="ccca4-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="ccca4-209">Als u het Azure configuratiedetails van persoonlijke peering, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ccca4-209">To get the Azure private peering configuration details, use the following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="ccca4-210">Is een reactie voorbeeld voor een persoonlijke peering Prestatietesten zijn geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="ccca4-210">A sample response, for a successfully configured private peering is:</span></span>

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

<span data-ttu-id="ccca4-211">Een ingeschakeld is, moet peering context dan de primaire en secundaire peer-subnetten die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="ccca4-211">A successfully, enabled peering context would have the primary and secondary peer subnets listed.</span></span> <span data-ttu-id="ccca4-212">Het/30-subnetten worden gebruikt voor de interface-IP-adres van de msee's en PE-msee's.</span><span class="sxs-lookup"><span data-stu-id="ccca4-212">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="ccca4-213">Als u Azure openbare peering configuratiedetails, gebruikt u de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="ccca4-213">To get the Azure public peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="ccca4-214">Als u de configuratiegegevens van de Microsoft-peering, gebruikt u de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="ccca4-214">To get the Microsoft peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="ccca4-215">Als laag 3-peerings zijn ingesteld door de serviceprovider, overschrijft instellen van de ExpressRoute-peerings via de portal of PowerShell de instellingen van de serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="ccca4-215">If layer 3 peerings were set by the service provider, setting the ExpressRoute peerings via the portal or PowerShell overwrites the service provider settings.</span></span> <span data-ttu-id="ccca4-216">Opnieuw instellen van de instellingen van de peering naast vereist de ondersteuning van de serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="ccca4-216">Resetting the provider side peering settings requires the support of the service provider.</span></span> <span data-ttu-id="ccca4-217">De ExpressRoute-peerings alleen wijzigen als u zeker dat de serviceprovider alleen layer 2-services levert!</span><span class="sxs-lookup"><span data-stu-id="ccca4-217">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="ccca4-218">Als een peering niet is ingeschakeld, controleert u of de primaire en secundaire peer subnetten toegewezen overeenkomen met de configuratie op de gekoppelde PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="ccca4-218">If a peering is not enabled, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="ccca4-219">Controleer ook of de juiste *VlanId*, *AzureAsn*, en *PeerAsn* op msee's worden gebruikt en als deze waarden worden toegewezen aan de namen die op de gekoppelde PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="ccca4-219">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="ccca4-220">Als u de configuratie op de MSEE-routers, verwijzen naar [maken en wijzigen van routering voor een ExpressRoute-circuit] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="ccca4-220">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-the-service-provider"></a><span data-ttu-id="ccca4-221">ARP tussen Microsoft en de serviceprovider valideren</span><span class="sxs-lookup"><span data-stu-id="ccca4-221">Validate ARP between Microsoft and the service provider</span></span>
<span data-ttu-id="ccca4-222">Deze sectie wordt gebruikt (klassiek) PowerShell-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="ccca4-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="ccca4-223">Als u PowerShell Azure Resource Manager-opdrachten gebruikt hebt, zorg ervoor dat u beheerder/co-beheerder toegang tot het abonnement via hebben [klassieke Azure-portal][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="ccca4-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="ccca4-224">Voor het oplossen van problemen met Azure Resource Manager opdrachten raadpleegt u de [ophalen ARP-tabellen in het Resource Manager-implementatiemodel] [ ARP] document.</span><span class="sxs-lookup"><span data-stu-id="ccca4-224">For troubleshooting using Azure Resource Manager commands please refer to the [Getting ARP tables in the Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="ccca4-225">Als u ARP, kunnen de Azure portal en de Azure Resource Manager PowerShell-opdrachten worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ccca4-225">To get ARP, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="ccca4-226">Als er fouten optreden met de Azure Resource Manager PowerShell-opdrachten, klassieke PowerShell-opdrachten gebruiken als klassieke PowerShell opdrachten ook worden gebruikt met Azure Resource Manager ExpressRoute-circuits.</span><span class="sxs-lookup"><span data-stu-id="ccca4-226">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="ccca4-227">Als u de ARP-tabel van de primaire MSEE-router voor persoonlijke peering, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ccca4-227">To get the ARP table from the primary MSEE router for the private peering, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="ccca4-228">Een voorbeeld van antwoord voor de opdracht in het scenario voor geslaagd:</span><span class="sxs-lookup"><span data-stu-id="ccca4-228">An example response for the command, in the successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="ccca4-229">Op deze manier kunt u de ARP-tabel van de MSEE in controleren de *primaire*/*secundaire* pad voor *persoonlijke*/*openbare*/*Microsoft* peerings.</span><span class="sxs-lookup"><span data-stu-id="ccca4-229">Similarly, you can check the ARP table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="ccca4-230">Het volgende voorbeeld ziet dat het antwoord van de opdracht voor een peering bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="ccca4-230">The following example shows the response of the command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="ccca4-231">Als de ARP-tabel geen IP-adressen van de interfaces die zijn toegewezen aan de MAC-adressen heeft, moet u de volgende informatie bekijken:</span><span class="sxs-lookup"><span data-stu-id="ccca4-231">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
>1. <span data-ttu-id="ccca4-232">Als het eerste IP-adres van het/30 subnet voor de koppeling tussen de MSEE-PR en MSEE wordt gebruikt op de interface van MSEE PR. toegewezen</span><span class="sxs-lookup"><span data-stu-id="ccca4-232">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="ccca4-233">Azure gebruikt altijd het tweede IP-adres voor de msee's.</span><span class="sxs-lookup"><span data-stu-id="ccca4-233">Azure always uses the second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="ccca4-234">Controleer of als de klant (C-code) en VLAN-servicetags (S-Tag) overeenkomt met beide op een combinatie van MSEE PR en MSEE.</span><span class="sxs-lookup"><span data-stu-id="ccca4-234">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-the-msee"></a><span data-ttu-id="ccca4-235">BGP-routes op de MSEE en valideren</span><span class="sxs-lookup"><span data-stu-id="ccca4-235">Validate BGP and routes on the MSEE</span></span>
<span data-ttu-id="ccca4-236">Deze sectie wordt gebruikt (klassiek) PowerShell-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="ccca4-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="ccca4-237">Als u PowerShell Azure Resource Manager-opdrachten gebruikt hebt, zorg ervoor dat u beheerder/co-beheerder toegang tot het abonnement via hebben [klassieke Azure-portal][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="ccca4-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="ccca4-238">Als u BGP-informatie, kunnen de Azure portal en de Azure Resource Manager PowerShell-opdrachten worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ccca4-238">To get BGP information, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="ccca4-239">Als er fouten optreden met de Azure Resource Manager PowerShell-opdrachten, klassieke PowerShell-opdrachten gebruiken als klassieke PowerShell opdrachten ook worden gebruikt met Azure Resource Manager ExpressRoute-circuits.</span><span class="sxs-lookup"><span data-stu-id="ccca4-239">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="ccca4-240">Als u de routeringstabel (neighbor BGP) samenvatting voor een bepaalde routering context, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ccca4-240">To get the routing table (BGP neighbor) summary for a particular routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="ccca4-241">Er is een voorbeeld van antwoord:</span><span class="sxs-lookup"><span data-stu-id="ccca4-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="ccca4-242">Zoals u in het voorgaande voorbeeld, wordt de opdracht is handig om te bepalen hoe lang de routering context is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ccca4-242">As shown in the preceding example, the command is useful to determine for how long the routing context has been established.</span></span> <span data-ttu-id="ccca4-243">Het aantal route voorvoegsels die worden geadverteerd door de router peering wordt tevens aangegeven.</span><span class="sxs-lookup"><span data-stu-id="ccca4-243">It also indicates number of route prefixes advertised by the peering router.</span></span>

>[!NOTE]
><span data-ttu-id="ccca4-244">Als de status in actief of inactief is, moet u controleren als de primaire en secundaire peer subnetten toegewezen overeenkomen met de configuratie voor de gekoppelde PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="ccca4-244">If the state is in Active or Idle, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="ccca4-245">Controleer ook of de juiste *VlanId*, *AzureAsn*, en *PeerAsn* op msee's worden gebruikt en als deze waarden worden toegewezen aan de namen die op de gekoppelde PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="ccca4-245">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="ccca4-246">Als MD5-hash is gekozen, is de gedeelde sleutel moet hetzelfde zijn op de combinatie van MSEE en PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="ccca4-246">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="ccca4-247">Als u de configuratie op de MSEE-routers, verwijzen naar [maken en wijzigen van routering voor een ExpressRoute-circuit][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="ccca4-247">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="ccca4-248">Als bepaalde bestemmingen niet bereikbaar via een bepaalde peering zijn, controleert u de routetabel van de msee's die horen bij de specifieke context van de peering.</span><span class="sxs-lookup"><span data-stu-id="ccca4-248">If certain destinations are not reachable over a particular peering, check the route table of the MSEEs belonging to the particular peering context.</span></span> <span data-ttu-id="ccca4-249">Als een overeenkomende voorvoegsel (kan worden NATed IP) in de routeringstabel aanwezig is, moet u controleren als er firewalls/NSG/ACL's op het pad en als het verkeer is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="ccca4-249">If a matching prefix (could be NATed IP) is present in the routing table, then check if there are firewalls/NSG/ACLs on the path and if they permit the traffic.</span></span>
>
>

<span data-ttu-id="ccca4-250">De volledige-routeringstabel van de MSEE ophalen op de *primaire* pad voor de betreffende *persoonlijke* routering context, gebruik de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ccca4-250">To get the full routing table from MSEE on the *Primary* path for the particular *Private* routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="ccca4-251">Er is een voorbeeld van de goede afloop voor de opdracht:</span><span class="sxs-lookup"><span data-stu-id="ccca4-251">An example successful outcome for the command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="ccca4-252">Op deze manier kunt u de routeringstabel van de MSEE in controleren de *primaire*/*secundaire* pad voor *persoonlijke*/*openbare*/*Microsoft* een peering context.</span><span class="sxs-lookup"><span data-stu-id="ccca4-252">Similarly, you can check the routing table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="ccca4-253">Het volgende voorbeeld ziet u dat het antwoord van de opdracht voor een peering bestaat niet:</span><span class="sxs-lookup"><span data-stu-id="ccca4-253">The following example shows the response of the command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-the-traffic-statistics"></a><span data-ttu-id="ccca4-254">De statistieken voor het verkeer controleren</span><span class="sxs-lookup"><span data-stu-id="ccca4-254">Check the Traffic Statistics</span></span>
<span data-ttu-id="ccca4-255">Als u de statistieken van de gecombineerde primaire en secundaire pad verkeer--bytes in en uit--van een peering context gebruikt de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ccca4-255">To get the combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use the following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="ccca4-256">Er is een voorbeeld van uitvoer van de opdracht:</span><span class="sxs-lookup"><span data-stu-id="ccca4-256">A sample output of the command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="ccca4-257">Er is een voorbeeld van uitvoer van de opdracht voor een niet-bestaande peering:</span><span class="sxs-lookup"><span data-stu-id="ccca4-257">A sample output of the command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="ccca4-258">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ccca4-258">Next Steps</span></span>
<span data-ttu-id="ccca4-259">Bekijk de volgende koppelingen voor meer informatie en hulp:</span><span class="sxs-lookup"><span data-stu-id="ccca4-259">For more information or help, check out the following links:</span></span>

- <span data-ttu-id="ccca4-260">[Microsoft-ondersteuning][Support]</span><span class="sxs-lookup"><span data-stu-id="ccca4-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="ccca4-261">[Maken en een ExpressRoute-circuit wijzigen][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="ccca4-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="ccca4-262">[Maken en aanpassen van routering voor een ExpressRoute-circuit][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="ccca4-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
<span data-ttu-id="ccca4-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logische Express Route-verbinding"</span><span class="sxs-lookup"><span data-stu-id="ccca4-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logical Express Route Connectivity"</span></span>
<span data-ttu-id="ccca4-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Pictogram voor alle resources"</span><span class="sxs-lookup"><span data-stu-id="ccca4-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "All resources icon"</span></span>
<span data-ttu-id="ccca4-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Overzicht-pictogram"</span><span class="sxs-lookup"><span data-stu-id="ccca4-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Overview icon"</span></span>
<span data-ttu-id="ccca4-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Schermopname van ExpressRoute Essentials-voorbeeld"</span><span class="sxs-lookup"><span data-stu-id="ccca4-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials sample screenshot"</span></span>
<span data-ttu-id="ccca4-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Schermopname van ExpressRoute Essentials-voorbeeld"</span><span class="sxs-lookup"><span data-stu-id="ccca4-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials sample screenshot"</span></span>

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






