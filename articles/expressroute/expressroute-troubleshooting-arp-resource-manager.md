---
title: 'ARP-tabellen ophalen: Resource Manager: Azure ExpressRoute probleemoplossing | Microsoft Docs'
description: Deze pagina vindt u instructies voor het ophalen van Hallo ARP tabellen voor een ExpressRoute-circuit
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: 0a6bf1d5-6baf-44dd-87d3-1ebd2fd08bdc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: c386b031814d40ef6ea3ce5e0eaaab9634470e8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a><span data-ttu-id="b098c-103">Het ophalen van de ARP tabellen in Hallo Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="b098c-103">Getting ARP tables in hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b098c-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b098c-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="b098c-105">PowerShell - Klassiek</span><span class="sxs-lookup"><span data-stu-id="b098c-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="b098c-106">Dit artikel begeleidt u bij Hallo stappen toolearn Hallo die ARP voor uw ExpressRoute-circuit tabellen.</span><span class="sxs-lookup"><span data-stu-id="b098c-106">This article walks you through hello steps toolearn hello ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b098c-107">Dit document is bedoeld toohelp u opsporen en oplossen van eenvoudige problemen.</span><span class="sxs-lookup"><span data-stu-id="b098c-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="b098c-108">Het is niet bedoeld toobe vervanging voor ondersteuning van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b098c-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="b098c-109">U moet een ondersteuningsticket met openen [Microsoft ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) bent u toosolve Hallo probleem op door middel van Hallo richtlijnen die hieronder worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="b098c-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable toosolve hello problem using hello guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="b098c-110">Adres van de tabellen ARP (Resolution Protocol) en ARP</span><span class="sxs-lookup"><span data-stu-id="b098c-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="b098c-111">Protocol ARP (Address Resolution) is een layer 2-protocol gedefinieerd in [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="b098c-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="b098c-112">ARP is gebruikte toomap Hallo Ethernet-adres (MAC-adres) met een IP-adres.</span><span class="sxs-lookup"><span data-stu-id="b098c-112">ARP is used toomap hello Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="b098c-113">Hallo ARP-tabel bevat een toewijzing van Hallo ipv4-adres en MAC-adres voor een bepaalde peering.</span><span class="sxs-lookup"><span data-stu-id="b098c-113">hello ARP table provides a mapping of hello ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="b098c-114">Hallo ARP-tabel voor een ExpressRoute-circuitpeering biedt Hallo volgende informatie voor elke interface (primair en secundair)</span><span class="sxs-lookup"><span data-stu-id="b098c-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="b098c-115">Toewijzing van de lokale router interface IP-adres toohello MAC-adres</span><span class="sxs-lookup"><span data-stu-id="b098c-115">Mapping of on-premises router interface ip address toohello MAC address</span></span>
2. <span data-ttu-id="b098c-116">Toewijzing van ExpressRoute-router interface IP-adres toohello MAC-adres</span><span class="sxs-lookup"><span data-stu-id="b098c-116">Mapping of ExpressRoute router interface ip address toohello MAC address</span></span>
3. <span data-ttu-id="b098c-117">Leeftijd van Hallo-toewijzing</span><span class="sxs-lookup"><span data-stu-id="b098c-117">Age of hello mapping</span></span>

<span data-ttu-id="b098c-118">ARP-tabellen kunnen laag 2-configuratie valideren en het oplossen van eenvoudige laag-2 verbindingsproblemen.</span><span class="sxs-lookup"><span data-stu-id="b098c-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="b098c-119">Voorbeeld van de ARP-tabel:</span><span class="sxs-lookup"><span data-stu-id="b098c-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="b098c-120">Hallo volgende sectie bevat informatie over hoe u kunt bekijken Hallo gezien door Hallo ExpressRoute-randrouters ARP-tabellen.</span><span class="sxs-lookup"><span data-stu-id="b098c-120">hello following section provides information on how you can view hello ARP tables seen by hello ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="b098c-121">Vereisten voor het leren van ARP-tabellen</span><span class="sxs-lookup"><span data-stu-id="b098c-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="b098c-122">Zorg ervoor dat er Hallo voordat u verder de voortgang volgen</span><span class="sxs-lookup"><span data-stu-id="b098c-122">Ensure that you have hello following before you progress further</span></span>

* <span data-ttu-id="b098c-123">Een geldig ExpressRoute-circuit dat is geconfigureerd met ten minste één peering.</span><span class="sxs-lookup"><span data-stu-id="b098c-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="b098c-124">Hallo circuit moet volledig worden geconfigureerd door de connectiviteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="b098c-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="b098c-125">U (of uw connectiviteitsprovider) moet hebben geconfigureerd ten minste één Hallo peerings (Azure privé, Azure openbaar en Microsoft) op dit circuit.</span><span class="sxs-lookup"><span data-stu-id="b098c-125">You (or your connectivity provider) must have configured at least one of hello peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="b098c-126">IP-adresbereiken gebruikt voor het configureren van Hallo peerings (Azure privé, Azure openbaar en Microsoft).</span><span class="sxs-lookup"><span data-stu-id="b098c-126">IP address ranges used for configuring hello peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="b098c-127">Hallo IP-adres toewijzing voorbeelden in Hallo bekijkt [pagina voor ExpressRoute routing requirements](expressroute-routing.md) tooget een goed begrip van hoe IP-adressen zijn toegewezen toointerfaces aan uw kant- en op Hallo ExpressRoute aan clientzijde.</span><span class="sxs-lookup"><span data-stu-id="b098c-127">Review hello ip address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how ip addresses are mapped toointerfaces on your side and on hello ExpressRoute side.</span></span> <span data-ttu-id="b098c-128">Krijgt u informatie over het Hallo-peeringconfiguratie aan de hand van Hallo [configuratiepagina van de ExpressRoute-peering](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b098c-128">You can get information on hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="b098c-129">Gegevens uit uw netwerken team / connectiviteitsprovider op Hallo MAC-adressen van de interfaces met deze IP-adressen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b098c-129">Information from your networking team / connectivity provider on hello MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="b098c-130">U moet Hallo nieuwste PowerShell-module voor Azure (1,50 of een nieuwere versie) hebben.</span><span class="sxs-lookup"><span data-stu-id="b098c-130">You must have hello latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="b098c-131">Hallo ARP ophalen tabellen voor uw ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="b098c-131">Getting hello ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="b098c-132">Deze sectie bevat instructies over hoe u kunt bekijken Hallo ARP-tabellen per peering met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b098c-132">This section provides instructions on how you can view hello ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="b098c-133">U of uw connectiviteitsprovider moet hebben geconfigureerd Hallo peering voordat u zich verder ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="b098c-133">You or your connectivity provider must have configured hello peering before progressing further.</span></span> <span data-ttu-id="b098c-134">Elk circuit heeft twee paden (primair en secundair).</span><span class="sxs-lookup"><span data-stu-id="b098c-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="b098c-135">U kunt onafhankelijk Hallo ARP-tabel voor elk pad controleren.</span><span class="sxs-lookup"><span data-stu-id="b098c-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="b098c-136">ARP-tabellen voor persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="b098c-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="b098c-137">Hallo volgende cmdlet biedt Hallo ARP tabellen voor persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="b098c-137">hello following cmdlet provides hello ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="b098c-138">Voorbeeld van uitvoer wordt hieronder weergegeven voor een Hallo paden</span><span class="sxs-lookup"><span data-stu-id="b098c-138">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="b098c-139">ARP-tabellen voor openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="b098c-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="b098c-140">Hallo volgende cmdlet biedt Hallo ARP tabellen voor openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="b098c-140">hello following cmdlet provides hello ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="b098c-141">Voorbeeld van uitvoer wordt hieronder weergegeven voor een Hallo paden</span><span class="sxs-lookup"><span data-stu-id="b098c-141">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="b098c-142">ARP-tabellen voor Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="b098c-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="b098c-143">Hallo volgende cmdlet biedt Hallo ARP tabellen voor Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="b098c-143">hello following cmdlet provides hello ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="b098c-144">Voorbeeld van uitvoer wordt hieronder weergegeven voor een Hallo paden</span><span class="sxs-lookup"><span data-stu-id="b098c-144">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="b098c-145">Hoe toouse deze informatie</span><span class="sxs-lookup"><span data-stu-id="b098c-145">How toouse this information</span></span>
<span data-ttu-id="b098c-146">Hallo ARP-tabel van een peering kan worden gebruikt toodetermine valideren laag 2-configuratie en de verbinding.</span><span class="sxs-lookup"><span data-stu-id="b098c-146">hello ARP table of a peering can be used toodetermine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="b098c-147">Deze sectie bevat een overzicht van hoe ARP-tabellen onder verschillende scenario's eruit.</span><span class="sxs-lookup"><span data-stu-id="b098c-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="b098c-148">ARP-tabel wanneer een circuit bevindt zich in de operationele status (verwachte status)</span><span class="sxs-lookup"><span data-stu-id="b098c-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="b098c-149">Hallo ARP-tabel heeft een vermelding voor Hallo lokale zijde met een geldig IP-adres en MAC-adres en een vergelijkbare vermelding voor Hallo Microsoft aan clientzijde.</span><span class="sxs-lookup"><span data-stu-id="b098c-149">hello ARP table will have an entry for hello on-premises side with a valid IP address and MAC address and a similar entry for hello Microsoft side.</span></span> 
* <span data-ttu-id="b098c-150">laatste octet Hallo van Hallo lokale IP-adres wordt altijd een oneven getal zijn.</span><span class="sxs-lookup"><span data-stu-id="b098c-150">hello last octet of hello on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="b098c-151">de laatste octet Hallo Hallo Microsoft IP-adres wordt altijd een even getal zijn.</span><span class="sxs-lookup"><span data-stu-id="b098c-151">hello last octet of hello Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="b098c-152">Hallo hetzelfde MAC-adres wordt weergegeven op Hallo Microsoft aan clientzijde voor alle 3 peerings (primaire / secundaire).</span><span class="sxs-lookup"><span data-stu-id="b098c-152">hello same MAC address will appear on hello Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="b098c-153">ARP-tabel wanneer lokale / verbinding-provider heeft problemen</span><span class="sxs-lookup"><span data-stu-id="b098c-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="b098c-154">Als er problemen met Hallo on-premises zijn of connectiviteitsprovider mogelijk ziet u beide slechts één vermelding wordt weergegeven in Hallo ARP tabel of Hallo on-premises MAC-adres wordt niet volledig weergeven.</span><span class="sxs-lookup"><span data-stu-id="b098c-154">If there are issues with hello on-premises or connectivity provider you may see that either only one entry will appear in hello ARP table or hello on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="b098c-155">Hallo-toewijzing tussen Hallo MAC-adres en IP-adres in Hallo Microsoft side laat zien.</span><span class="sxs-lookup"><span data-stu-id="b098c-155">This will show hello mapping between hello MAC address and IP address used in hello Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="b098c-156">of</span><span class="sxs-lookup"><span data-stu-id="b098c-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="b098c-157">Een ondersteuningsaanvraag openen met uw provider connectiviteit toodebug dergelijke problemen.</span><span class="sxs-lookup"><span data-stu-id="b098c-157">Open a support request with your connectivity provider toodebug such issues.</span></span> <span data-ttu-id="b098c-158">Als Hallo ARP-tabel geen heeft toegewezen IP-adressen van de interfaces Hallo tooMAC adressen, bekijk Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="b098c-158">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
> 
> 1. <span data-ttu-id="b098c-159">Als het eerste IP-adres Hallo van Hallo /30 subnet voor Hallo koppeling tussen toegewezen Hallo MSEE PR en MSEE wordt gebruikt op Hallo-interface van MSEE PR.</span><span class="sxs-lookup"><span data-stu-id="b098c-159">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="b098c-160">Azure gebruikt altijd Hallo tweede IP-adres voor de msee's.</span><span class="sxs-lookup"><span data-stu-id="b098c-160">Azure always uses hello second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="b098c-161">Controleer of als Hallo klant (C-code) en VLAN-servicetags (S-Tag) overeenkomt met beide op een combinatie van MSEE PR en MSEE.</span><span class="sxs-lookup"><span data-stu-id="b098c-161">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="b098c-162">ARP-tabel bij Microsoft problemen heeft</span><span class="sxs-lookup"><span data-stu-id="b098c-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="b098c-163">U ziet een ARP-tabel wordt weergegeven voor een peering als er problemen op Hallo Microsoft aan clientzijde zijn.</span><span class="sxs-lookup"><span data-stu-id="b098c-163">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span> 
* <span data-ttu-id="b098c-164">Open een ondersteuningsticket met [Microsoft ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="b098c-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="b098c-165">Geef op of er een probleem met laag 2-connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="b098c-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b098c-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b098c-166">Next Steps</span></span>
* <span data-ttu-id="b098c-167">Layer 3-configuraties voor uw ExpressRoute-circuit valideren</span><span class="sxs-lookup"><span data-stu-id="b098c-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="b098c-168">Ophalen van de route samenvatting toodetermine Hallo status van de BGP-sessies</span><span class="sxs-lookup"><span data-stu-id="b098c-168">Get route summary toodetermine hello state of BGP sessions</span></span> 
  * <span data-ttu-id="b098c-169">Route tabel toodetermine welke voorvoegsels worden geadverteerd via ExpressRoute ophalen</span><span class="sxs-lookup"><span data-stu-id="b098c-169">Get route table toodetermine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="b098c-170">Overdracht van gegevens aan de hand van de bytes in / out-valideren</span><span class="sxs-lookup"><span data-stu-id="b098c-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="b098c-171">Open een ondersteuningsticket met [Microsoft ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) als u nog steeds problemen ondervindt.</span><span class="sxs-lookup"><span data-stu-id="b098c-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

