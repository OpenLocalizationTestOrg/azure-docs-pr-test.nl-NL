---
title: 'ARP-tabellen ophalen: klassieke: Azure ExpressRoute probleemoplossing | Microsoft Docs'
description: Deze pagina bevat instructies voor het ophalen van Hallo ARP tabellen voor een ExpressRoute-circuit.
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: b5856acf-03c2-4933-8111-6ce12998d92a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: 2b01304a38fa0e0def27dbd7c391d7ad8bbdabff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a><span data-ttu-id="87aa7-103">ARP ophalen tabellen in het klassieke implementatiemodel Hallo</span><span class="sxs-lookup"><span data-stu-id="87aa7-103">Getting ARP tables in hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="87aa7-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="87aa7-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="87aa7-105">PowerShell - Klassiek</span><span class="sxs-lookup"><span data-stu-id="87aa7-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="87aa7-106">Dit artikel begeleidt u bij Hallo stappen voor het ophalen van Hallo Protocol ARP (Address Resolution) tabellen voor uw Azure ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="87aa7-106">This article walks you through hello steps for getting hello Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87aa7-107">Dit document is bedoeld toohelp u opsporen en oplossen van eenvoudige problemen.</span><span class="sxs-lookup"><span data-stu-id="87aa7-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="87aa7-108">Het is niet bedoeld toobe vervanging voor ondersteuning van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="87aa7-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="87aa7-109">Als u op Hallo probleem oplossen kunt met behulp van Hallo richtlijnen te volgen, opent u een ondersteuningsaanvraag met [Microsoft Azure Help + ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="87aa7-109">If you can't solve hello problem by using hello following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="87aa7-110">Adres van de tabellen ARP (Resolution Protocol) en ARP</span><span class="sxs-lookup"><span data-stu-id="87aa7-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="87aa7-111">ARP is een Layer 2-protocol die gedefinieerd in [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="87aa7-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="87aa7-112">ARP is gebruikte toomap een Ethernet-adres (MAC-adres) tooan IP-adres.</span><span class="sxs-lookup"><span data-stu-id="87aa7-112">ARP is used toomap an Ethernet address (MAC address) tooan IP address.</span></span>

<span data-ttu-id="87aa7-113">Een ARP-tabel bevat een toewijzing van Hallo IPv4-adres en MAC-adres voor een bepaalde peering.</span><span class="sxs-lookup"><span data-stu-id="87aa7-113">An ARP table provides a mapping of hello IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="87aa7-114">Hallo ARP-tabel voor een ExpressRoute-circuitpeering biedt Hallo volgende informatie voor elke interface (primair en secundair):</span><span class="sxs-lookup"><span data-stu-id="87aa7-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="87aa7-115">Toewijzing van een lokale router interface IP-adres tooa MAC-adres</span><span class="sxs-lookup"><span data-stu-id="87aa7-115">Mapping of an on-premises router interface IP address tooa MAC address</span></span>
2. <span data-ttu-id="87aa7-116">Toewijzing van een ExpressRoute-router interface IP-adres tooa MAC-adres</span><span class="sxs-lookup"><span data-stu-id="87aa7-116">Mapping of an ExpressRoute router interface IP address tooa MAC address</span></span>
3. <span data-ttu-id="87aa7-117">Hallo leeftijd van Hallo-toewijzing</span><span class="sxs-lookup"><span data-stu-id="87aa7-117">hello age of hello mapping</span></span>

<span data-ttu-id="87aa7-118">ARP-tabellen kunnen u met Layer 2-configuratie wordt gevalideerd en basic Layer 2-verbindingsproblemen op te lossen.</span><span class="sxs-lookup"><span data-stu-id="87aa7-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="87aa7-119">Hieronder volgt een voorbeeld van een ARP-tabel:</span><span class="sxs-lookup"><span data-stu-id="87aa7-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="87aa7-120">Hallo volgende sectie bevat informatie over hoe tooview ARP-tabellen die zijn zichtbaar voor de ExpressRoute-randrouters Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="87aa7-120">hello following section provides information about how tooview hello ARP tables that are seen by hello ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="87aa7-121">Vereisten voor het gebruik van ARP-tabellen</span><span class="sxs-lookup"><span data-stu-id="87aa7-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="87aa7-122">Zorg ervoor dat u Hallo volgende hebt voordat u verdergaat:</span><span class="sxs-lookup"><span data-stu-id="87aa7-122">Ensure that you have hello following before you continue:</span></span>

* <span data-ttu-id="87aa7-123">Een geldig ExpressRoute-circuit dat geconfigureerd met ten minste één peering.</span><span class="sxs-lookup"><span data-stu-id="87aa7-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="87aa7-124">Hallo circuit moet volledig worden geconfigureerd door de connectiviteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="87aa7-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="87aa7-125">U (of uw connectiviteitsprovider) moet configureren ten minste één Hallo peerings (Azure privé, Azure openbaar of Microsoft) op dit circuit.</span><span class="sxs-lookup"><span data-stu-id="87aa7-125">You (or your connectivity provider) must configure at least one of hello peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="87aa7-126">IP-adresbereiken die worden gebruikt voor het configureren van Hallo peerings (Azure privé, Azure openbaar en Microsoft).</span><span class="sxs-lookup"><span data-stu-id="87aa7-126">IP address ranges that are used for configuring hello peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="87aa7-127">Hallo IP-adres toewijzing voorbeelden in Hallo bekijkt [pagina voor ExpressRoute routing requirements](expressroute-routing.md) tooget een goed begrip van hoe IP-adressen zijn toegewezen toointerfaces op uw aise en Hallo ExpressRoute-zijde.</span><span class="sxs-lookup"><span data-stu-id="87aa7-127">Review hello IP address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how IP addresses are mapped toointerfaces on your aise and on hello ExpressRoute side.</span></span> <span data-ttu-id="87aa7-128">U kunt informatie ophalen over Hallo peeringconfiguratie aan de hand van Hallo [configuratiepagina van de ExpressRoute-peering](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="87aa7-128">You can get information about hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="87aa7-129">Gegevens van uw netwerk team of connectiviteit provider over Hallo MAC-adressen van Hallo-interfaces die worden gebruikt met deze IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="87aa7-129">Information from your networking team or connectivity provider about hello MAC addresses of hello interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="87aa7-130">Hallo nieuwste Windows PowerShell-module voor Azure (versie 1,50 of hoger).</span><span class="sxs-lookup"><span data-stu-id="87aa7-130">hello latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="87aa7-131">ARP-tabellen voor uw ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="87aa7-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="87aa7-132">Deze sectie bevat instructies over hoe tooview Hallo ARP voor elk type peering tabellen met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87aa7-132">This section provides instructions about how tooview hello ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="87aa7-133">Voordat u doorgaat, moet u of uw connectiviteitsprovider tooconfigure hello peering.</span><span class="sxs-lookup"><span data-stu-id="87aa7-133">Before you continue, either you or your connectivity provider needs tooconfigure hello peering.</span></span> <span data-ttu-id="87aa7-134">Elk circuit heeft twee paden (primair en secundair).</span><span class="sxs-lookup"><span data-stu-id="87aa7-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="87aa7-135">U kunt onafhankelijk Hallo ARP-tabel voor elk pad controleren.</span><span class="sxs-lookup"><span data-stu-id="87aa7-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="87aa7-136">ARP-tabellen voor persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="87aa7-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="87aa7-137">Hallo volgende cmdlet biedt Hallo ARP tabellen voor persoonlijke Azure-peering:</span><span class="sxs-lookup"><span data-stu-id="87aa7-137">hello following cmdlet provides hello ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="87aa7-138">Hieronder volgt een voorbeeld van uitvoer voor een van de paden Hallo:</span><span class="sxs-lookup"><span data-stu-id="87aa7-138">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="87aa7-139">ARP-tabellen voor openbare Azure-peering:</span><span class="sxs-lookup"><span data-stu-id="87aa7-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="87aa7-140">Hallo volgende cmdlet biedt Hallo ARP tabellen voor openbare Azure-peering:</span><span class="sxs-lookup"><span data-stu-id="87aa7-140">hello following cmdlet provides hello ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="87aa7-141">Hieronder volgt een voorbeeld van uitvoer voor een van de paden Hallo:</span><span class="sxs-lookup"><span data-stu-id="87aa7-141">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="87aa7-142">Hieronder volgt een voorbeeld van uitvoer voor een van de paden Hallo:</span><span class="sxs-lookup"><span data-stu-id="87aa7-142">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="87aa7-143">ARP-tabellen voor Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="87aa7-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="87aa7-144">Hallo volgende cmdlet biedt Hallo ARP tabellen voor Microsoft-peering:</span><span class="sxs-lookup"><span data-stu-id="87aa7-144">hello following cmdlet provides hello ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="87aa7-145">Voorbeeld van uitvoer wordt hieronder weergegeven voor een Hallo paden:</span><span class="sxs-lookup"><span data-stu-id="87aa7-145">Sample output is shown below for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="87aa7-146">Hoe toouse deze informatie</span><span class="sxs-lookup"><span data-stu-id="87aa7-146">How toouse this information</span></span>
<span data-ttu-id="87aa7-147">Hallo ARP-tabel van een peering mag gebruikte toovalidate Layer 2-configuratie en de verbinding.</span><span class="sxs-lookup"><span data-stu-id="87aa7-147">hello ARP table of a peering can be used toovalidate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="87aa7-148">Deze sectie biedt een overzicht van hoe de ARP-tabellen in verschillende scenario's eruit zien.</span><span class="sxs-lookup"><span data-stu-id="87aa7-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="87aa7-149">ARP-tabel wanneer een circuit bevindt zich in een operationele status (verwachte)</span><span class="sxs-lookup"><span data-stu-id="87aa7-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="87aa7-150">Hallo ARP-tabel heeft een vermelding voor Hallo lokale zijde met een geldig IP- en MAC-adres en een vergelijkbare vermelding voor Hallo Microsoft aan clientzijde.</span><span class="sxs-lookup"><span data-stu-id="87aa7-150">hello ARP table has an entry for hello on-premises side with a valid IP and MAC address, and a similar entry for hello Microsoft side.</span></span>
* <span data-ttu-id="87aa7-151">de laatste octet Hallo van Hallo lokale IP-adres is altijd een oneven getal.</span><span class="sxs-lookup"><span data-stu-id="87aa7-151">hello last octet of hello on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="87aa7-152">de laatste octet Hallo Hallo Microsoft IP-adres is altijd een even getal zijn.</span><span class="sxs-lookup"><span data-stu-id="87aa7-152">hello last octet of hello Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="87aa7-153">Hallo hetzelfde MAC-adres wordt weergegeven op Hallo Microsoft aan clientzijde voor alle drie de peerings (primaire en secundaire).</span><span class="sxs-lookup"><span data-stu-id="87aa7-153">hello same MAC address appears on hello Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a><span data-ttu-id="87aa7-154">ARP-tabel wanneer deze on-premises of wanneer Hallo-connectiviteitsprovider heeft problemen</span><span class="sxs-lookup"><span data-stu-id="87aa7-154">ARP table when it's on-premises or when hello connectivity-provider side has problems</span></span>
 <span data-ttu-id="87aa7-155">Slechts één vermelding verschijnt in Hallo ARP-tabel.</span><span class="sxs-lookup"><span data-stu-id="87aa7-155">Only one entry appears in hello ARP table.</span></span> <span data-ttu-id="87aa7-156">Hallo-toewijzing tussen Hallo MAC-adres en Hallo IP-adres dat wordt gebruikt op Hallo Microsoft aan clientzijde worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="87aa7-156">It shows hello mapping between hello MAC address and hello IP address that's used on hello Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="87aa7-157">Als er een probleem als volgt, opent u een ondersteuning vragen met uw provider connectiviteit tooresolve.</span><span class="sxs-lookup"><span data-stu-id="87aa7-157">If you experience an issue like this, open a support request with your connectivity provider tooresolve it.</span></span>
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a><span data-ttu-id="87aa7-158">ARP-tabel wanneer Hallo Microsoft side problemen heeft</span><span class="sxs-lookup"><span data-stu-id="87aa7-158">ARP table when hello Microsoft side has problems</span></span>
* <span data-ttu-id="87aa7-159">U ziet een ARP-tabel wordt weergegeven voor een peering als er problemen op Hallo Microsoft aan clientzijde zijn.</span><span class="sxs-lookup"><span data-stu-id="87aa7-159">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span>
* <span data-ttu-id="87aa7-160">Open een ondersteuningsverzoek met [Microsoft Azure Help + ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="87aa7-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="87aa7-161">Geef op of er een probleem met Layer 2-connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="87aa7-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87aa7-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="87aa7-162">Next steps</span></span>
* <span data-ttu-id="87aa7-163">Layer 3-configuraties voor uw ExpressRoute-circuit valideren:</span><span class="sxs-lookup"><span data-stu-id="87aa7-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="87aa7-164">Een route samenvatting toodetermine Hallo status van de BGP-sessies worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="87aa7-164">Get a route summary toodetermine hello state of BGP sessions.</span></span>
  * <span data-ttu-id="87aa7-165">Ophalen van een route tabel toodetermine welke voorvoegsels worden geadverteerd via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="87aa7-165">Get a route table toodetermine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="87aa7-166">Valideer de overdracht van gegevens aan de hand van bytes in en uit.</span><span class="sxs-lookup"><span data-stu-id="87aa7-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="87aa7-167">Open een ondersteuningsverzoek met [Microsoft Azure Help + ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) als u nog steeds problemen ondervindt.</span><span class="sxs-lookup"><span data-stu-id="87aa7-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

