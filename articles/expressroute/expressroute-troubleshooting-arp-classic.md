---
title: 'ARP-tabellen ophalen: klassieke: Azure ExpressRoute probleemoplossing | Microsoft Docs'
description: Deze pagina bevat instructies voor het ophalen van het ARP tabellen voor een ExpressRoute-circuit.
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
ms.openlocfilehash: fcc847b7e30fd55ca759830e0254ab7542e7663e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-classic-deployment-model"></a><span data-ttu-id="a4de5-103">Het ophalen van de ARP tabellen in het klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="a4de5-103">Getting ARP tables in the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4de5-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a4de5-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="a4de5-105">PowerShell - Klassiek</span><span class="sxs-lookup"><span data-stu-id="a4de5-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="a4de5-106">Dit artikel begeleidt u bij de stappen voor het ophalen van de tabellen Protocol ARP (Address Resolution) voor uw Azure ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a4de5-106">This article walks you through the steps for getting the Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4de5-107">Dit document is bedoeld voor hulp bij het opsporen en oplossen van eenvoudige problemen.</span><span class="sxs-lookup"><span data-stu-id="a4de5-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="a4de5-108">Het is niet bedoeld als vervanging voor ondersteuning van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a4de5-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="a4de5-109">Als u op het probleem oplossen kunt met behulp van de volgende richtlijnen, opent u een ondersteuningsaanvraag met [Microsoft Azure Help + ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="a4de5-109">If you can't solve the problem by using the following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="a4de5-110">Adres van de tabellen ARP (Resolution Protocol) en ARP</span><span class="sxs-lookup"><span data-stu-id="a4de5-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="a4de5-111">ARP is een Layer 2-protocol die gedefinieerd in [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="a4de5-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="a4de5-112">ARP wordt gebruikt om een Ethernet-adres (MAC-adres) worden toegewezen aan een IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a4de5-112">ARP is used to map an Ethernet address (MAC address) to an IP address.</span></span>

<span data-ttu-id="a4de5-113">Een ARP-tabel bevat een toewijzing van de IPv4-adres en MAC-adres voor een bepaalde peering.</span><span class="sxs-lookup"><span data-stu-id="a4de5-113">An ARP table provides a mapping of the IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="a4de5-114">De ARP-tabel voor een ExpressRoute-circuitpeering biedt de volgende informatie voor elke interface (primair en secundair):</span><span class="sxs-lookup"><span data-stu-id="a4de5-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="a4de5-115">Toewijzing van een lokale router interface IP-adres op een MAC-adres</span><span class="sxs-lookup"><span data-stu-id="a4de5-115">Mapping of an on-premises router interface IP address to a MAC address</span></span>
2. <span data-ttu-id="a4de5-116">Toewijzing van een ExpressRoute-router interface IP-adres op een MAC-adres</span><span class="sxs-lookup"><span data-stu-id="a4de5-116">Mapping of an ExpressRoute router interface IP address to a MAC address</span></span>
3. <span data-ttu-id="a4de5-117">De leeftijd van de toewijzing</span><span class="sxs-lookup"><span data-stu-id="a4de5-117">The age of the mapping</span></span>

<span data-ttu-id="a4de5-118">ARP-tabellen kunnen u met Layer 2-configuratie wordt gevalideerd en basic Layer 2-verbindingsproblemen op te lossen.</span><span class="sxs-lookup"><span data-stu-id="a4de5-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="a4de5-119">Hieronder volgt een voorbeeld van een ARP-tabel:</span><span class="sxs-lookup"><span data-stu-id="a4de5-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="a4de5-120">De volgende sectie bevat informatie over het weergeven van de ARP-tabellen die zijn zichtbaar voor de ExpressRoute-randrouters.</span><span class="sxs-lookup"><span data-stu-id="a4de5-120">The following section provides information about how to view the ARP tables that are seen by the ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="a4de5-121">Vereisten voor het gebruik van ARP-tabellen</span><span class="sxs-lookup"><span data-stu-id="a4de5-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="a4de5-122">Zorg ervoor dat u het volgende hebt voordat u verdergaat:</span><span class="sxs-lookup"><span data-stu-id="a4de5-122">Ensure that you have the following before you continue:</span></span>

* <span data-ttu-id="a4de5-123">Een geldig ExpressRoute-circuit dat geconfigureerd met ten minste één peering.</span><span class="sxs-lookup"><span data-stu-id="a4de5-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="a4de5-124">Het circuit moet volledig worden geconfigureerd door de connectiviteitsprovider.</span><span class="sxs-lookup"><span data-stu-id="a4de5-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="a4de5-125">U (of uw connectiviteitsprovider) moet configureren ten minste één van de peerings (Azure privé, Azure openbaar of Microsoft) op dit circuit.</span><span class="sxs-lookup"><span data-stu-id="a4de5-125">You (or your connectivity provider) must configure at least one of the peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="a4de5-126">IP-adresbereiken die worden gebruikt voor het configureren van de peerings (Azure privé, Azure openbaar en Microsoft).</span><span class="sxs-lookup"><span data-stu-id="a4de5-126">IP address ranges that are used for configuring the peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="a4de5-127">Controleer de IP-adres toewijzing voorbeelden in de [pagina voor ExpressRoute routing requirements](expressroute-routing.md) ophalen van een goed begrip van hoe IP-adressen zijn toegewezen aan de interfaces op uw aise en de ExpressRoute-zijde.</span><span class="sxs-lookup"><span data-stu-id="a4de5-127">Review the IP address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how IP addresses are mapped to interfaces on your aise and on the ExpressRoute side.</span></span> <span data-ttu-id="a4de5-128">U kunt informatie ophalen over de configuratie van de peering aan de hand van de [configuratiepagina van de ExpressRoute-peering](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="a4de5-128">You can get information about the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="a4de5-129">Gegevens van uw netwerk team of connectiviteit provider over de MAC-adressen van de interfaces die worden gebruikt met deze IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="a4de5-129">Information from your networking team or connectivity provider about the MAC addresses of the interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="a4de5-130">De meest recente Windows PowerShell-module voor Azure (versie 1,50 of hoger).</span><span class="sxs-lookup"><span data-stu-id="a4de5-130">The latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="a4de5-131">ARP-tabellen voor uw ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="a4de5-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="a4de5-132">Deze sectie bevat instructies over het weergeven van de ARP-tabellen voor elk type peering met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4de5-132">This section provides instructions about how to view the ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="a4de5-133">Voordat u doorgaat, moet u of uw connectiviteitsprovider voor het configureren van de peering.</span><span class="sxs-lookup"><span data-stu-id="a4de5-133">Before you continue, either you or your connectivity provider needs to configure the peering.</span></span> <span data-ttu-id="a4de5-134">Elk circuit heeft twee paden (primair en secundair).</span><span class="sxs-lookup"><span data-stu-id="a4de5-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="a4de5-135">U kunt de ARP-tabel voor elk pad onafhankelijk controleren.</span><span class="sxs-lookup"><span data-stu-id="a4de5-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="a4de5-136">ARP-tabellen voor persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="a4de5-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="a4de5-137">De volgende cmdlet geeft de ARP tabellen voor persoonlijke Azure-peering:</span><span class="sxs-lookup"><span data-stu-id="a4de5-137">The following cmdlet provides the ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="a4de5-138">Hieronder volgt een voorbeeld van uitvoer voor een van de paden:</span><span class="sxs-lookup"><span data-stu-id="a4de5-138">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="a4de5-139">ARP-tabellen voor openbare Azure-peering:</span><span class="sxs-lookup"><span data-stu-id="a4de5-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="a4de5-140">De volgende cmdlet geeft de ARP tabellen voor openbare Azure-peering:</span><span class="sxs-lookup"><span data-stu-id="a4de5-140">The following cmdlet provides the ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="a4de5-141">Hieronder volgt een voorbeeld van uitvoer voor een van de paden:</span><span class="sxs-lookup"><span data-stu-id="a4de5-141">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="a4de5-142">Hieronder volgt een voorbeeld van uitvoer voor een van de paden:</span><span class="sxs-lookup"><span data-stu-id="a4de5-142">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="a4de5-143">ARP-tabellen voor Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="a4de5-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="a4de5-144">De volgende cmdlet geeft de ARP tabellen voor Microsoft-peering:</span><span class="sxs-lookup"><span data-stu-id="a4de5-144">The following cmdlet provides the ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="a4de5-145">Voorbeeld van uitvoer wordt hieronder weergegeven voor een van de paden:</span><span class="sxs-lookup"><span data-stu-id="a4de5-145">Sample output is shown below for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="a4de5-146">Het gebruik van deze informatie</span><span class="sxs-lookup"><span data-stu-id="a4de5-146">How to use this information</span></span>
<span data-ttu-id="a4de5-147">De ARP-tabel van een peering kan worden gebruikt voor het valideren van Layer 2-configuratie en de verbinding.</span><span class="sxs-lookup"><span data-stu-id="a4de5-147">The ARP table of a peering can be used to validate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="a4de5-148">Deze sectie biedt een overzicht van hoe de ARP-tabellen in verschillende scenario's eruit zien.</span><span class="sxs-lookup"><span data-stu-id="a4de5-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="a4de5-149">ARP-tabel wanneer een circuit bevindt zich in een operationele status (verwachte)</span><span class="sxs-lookup"><span data-stu-id="a4de5-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="a4de5-150">De ARP-tabel heeft een vermelding voor de lokale kant met een geldig IP- en MAC-adres en een vergelijkbare vermelding voor de Microsoft-zijde.</span><span class="sxs-lookup"><span data-stu-id="a4de5-150">The ARP table has an entry for the on-premises side with a valid IP and MAC address, and a similar entry for the Microsoft side.</span></span>
* <span data-ttu-id="a4de5-151">Het laatste octet van het lokale IP-adres is altijd een oneven getal.</span><span class="sxs-lookup"><span data-stu-id="a4de5-151">The last octet of the on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="a4de5-152">Het laatste octet van het Microsoft-IP-adres is altijd een even getal zijn.</span><span class="sxs-lookup"><span data-stu-id="a4de5-152">The last octet of the Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="a4de5-153">Hetzelfde MAC-adres wordt weergegeven aan de kant van Microsoft voor alle drie de peerings (primaire en secundaire).</span><span class="sxs-lookup"><span data-stu-id="a4de5-153">The same MAC address appears on the Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-the-connectivity-provider-side-has-problems"></a><span data-ttu-id="a4de5-154">ARP-tabel wanneer deze on-premises of wanneer de kant van de connectiviteitsprovider problemen heeft</span><span class="sxs-lookup"><span data-stu-id="a4de5-154">ARP table when it's on-premises or when the connectivity-provider side has problems</span></span>
 <span data-ttu-id="a4de5-155">Er wordt slechts één vermelding weergegeven in de ARP-tabel.</span><span class="sxs-lookup"><span data-stu-id="a4de5-155">Only one entry appears in the ARP table.</span></span> <span data-ttu-id="a4de5-156">De toewijzing tussen het MAC-adres en het IP-adres dat wordt gebruikt bij Microsoft worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a4de5-156">It shows the mapping between the MAC address and the IP address that's used on the Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="a4de5-157">Als er een probleem als volgt, moet u een ondersteuningsaanvraag openen met uw connectiviteitsprovider te verhelpen.</span><span class="sxs-lookup"><span data-stu-id="a4de5-157">If you experience an issue like this, open a support request with your connectivity provider to resolve it.</span></span>
> 
> 

### <a name="arp-table-when-the-microsoft-side-has-problems"></a><span data-ttu-id="a4de5-158">ARP-tabel wanneer de Microsoft-zijde problemen heeft</span><span class="sxs-lookup"><span data-stu-id="a4de5-158">ARP table when the Microsoft side has problems</span></span>
* <span data-ttu-id="a4de5-159">U ziet een ARP-tabel wordt weergegeven voor een peering als er problemen bij Microsoft zijn.</span><span class="sxs-lookup"><span data-stu-id="a4de5-159">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span>
* <span data-ttu-id="a4de5-160">Open een ondersteuningsverzoek met [Microsoft Azure Help + ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="a4de5-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="a4de5-161">Geef op of er een probleem met Layer 2-connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="a4de5-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4de5-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4de5-162">Next steps</span></span>
* <span data-ttu-id="a4de5-163">Layer 3-configuraties voor uw ExpressRoute-circuit valideren:</span><span class="sxs-lookup"><span data-stu-id="a4de5-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="a4de5-164">Een route samenvatting om te bepalen van de status van de BGP-sessies worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="a4de5-164">Get a route summary to determine the state of BGP sessions.</span></span>
  * <span data-ttu-id="a4de5-165">Een routetabel om te bepalen welke voorvoegsels worden geadverteerd via ExpressRoute worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="a4de5-165">Get a route table to determine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="a4de5-166">Valideer de overdracht van gegevens aan de hand van bytes in en uit.</span><span class="sxs-lookup"><span data-stu-id="a4de5-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="a4de5-167">Open een ondersteuningsverzoek met [Microsoft Azure Help + ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) als u nog steeds problemen ondervindt.</span><span class="sxs-lookup"><span data-stu-id="a4de5-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

