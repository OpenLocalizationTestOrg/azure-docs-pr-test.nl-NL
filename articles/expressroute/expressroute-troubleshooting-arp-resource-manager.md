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
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a>Het ophalen van de ARP tabellen in Hallo Resource Manager-implementatiemodel
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - Klassiek](expressroute-troubleshooting-arp-classic.md)
> 
> 

Dit artikel begeleidt u bij Hallo stappen toolearn Hallo die ARP voor uw ExpressRoute-circuit tabellen. 

> [!IMPORTANT]
> Dit document is bedoeld toohelp u opsporen en oplossen van eenvoudige problemen. Het is niet bedoeld toobe vervanging voor ondersteuning van Microsoft. U moet een ondersteuningsticket met openen [Microsoft ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) bent u toosolve Hallo probleem op door middel van Hallo richtlijnen die hieronder worden beschreven.
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>Adres van de tabellen ARP (Resolution Protocol) en ARP
Protocol ARP (Address Resolution) is een layer 2-protocol gedefinieerd in [RFC 826](https://tools.ietf.org/html/rfc826). ARP is gebruikte toomap Hallo Ethernet-adres (MAC-adres) met een IP-adres.

Hallo ARP-tabel bevat een toewijzing van Hallo ipv4-adres en MAC-adres voor een bepaalde peering. Hallo ARP-tabel voor een ExpressRoute-circuitpeering biedt Hallo volgende informatie voor elke interface (primair en secundair)

1. Toewijzing van de lokale router interface IP-adres toohello MAC-adres
2. Toewijzing van ExpressRoute-router interface IP-adres toohello MAC-adres
3. Leeftijd van Hallo-toewijzing

ARP-tabellen kunnen laag 2-configuratie valideren en het oplossen van eenvoudige laag-2 verbindingsproblemen. 

Voorbeeld van de ARP-tabel: 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


Hallo volgende sectie bevat informatie over hoe u kunt bekijken Hallo gezien door Hallo ExpressRoute-randrouters ARP-tabellen. 

## <a name="prerequisites-for-learning-arp-tables"></a>Vereisten voor het leren van ARP-tabellen
Zorg ervoor dat er Hallo voordat u verder de voortgang volgen

* Een geldig ExpressRoute-circuit dat is geconfigureerd met ten minste één peering. Hallo circuit moet volledig worden geconfigureerd door de connectiviteitsprovider Hallo. U (of uw connectiviteitsprovider) moet hebben geconfigureerd ten minste één Hallo peerings (Azure privé, Azure openbaar en Microsoft) op dit circuit.
* IP-adresbereiken gebruikt voor het configureren van Hallo peerings (Azure privé, Azure openbaar en Microsoft). Hallo IP-adres toewijzing voorbeelden in Hallo bekijkt [pagina voor ExpressRoute routing requirements](expressroute-routing.md) tooget een goed begrip van hoe IP-adressen zijn toegewezen toointerfaces aan uw kant- en op Hallo ExpressRoute aan clientzijde. Krijgt u informatie over het Hallo-peeringconfiguratie aan de hand van Hallo [configuratiepagina van de ExpressRoute-peering](expressroute-howto-routing-arm.md).
* Gegevens uit uw netwerken team / connectiviteitsprovider op Hallo MAC-adressen van de interfaces met deze IP-adressen gebruikt.
* U moet Hallo nieuwste PowerShell-module voor Azure (1,50 of een nieuwere versie) hebben.

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a>Hallo ARP ophalen tabellen voor uw ExpressRoute-circuit
Deze sectie bevat instructies over hoe u kunt bekijken Hallo ARP-tabellen per peering met behulp van PowerShell. U of uw connectiviteitsprovider moet hebben geconfigureerd Hallo peering voordat u zich verder ontwikkelen. Elk circuit heeft twee paden (primair en secundair). U kunt onafhankelijk Hallo ARP-tabel voor elk pad controleren.

### <a name="arp-tables-for-azure-private-peering"></a>ARP-tabellen voor persoonlijke Azure-peering
Hallo volgende cmdlet biedt Hallo ARP tabellen voor persoonlijke Azure-peering

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

Voorbeeld van uitvoer wordt hieronder weergegeven voor een Hallo paden

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>ARP-tabellen voor openbare Azure-peering
Hallo volgende cmdlet biedt Hallo ARP tabellen voor openbare Azure-peering

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


Voorbeeld van uitvoer wordt hieronder weergegeven voor een Hallo paden

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>ARP-tabellen voor Microsoft-peering
Hallo volgende cmdlet biedt Hallo ARP tabellen voor Microsoft-peering

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


Voorbeeld van uitvoer wordt hieronder weergegeven voor een Hallo paden

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Hoe toouse deze informatie
Hallo ARP-tabel van een peering kan worden gebruikt toodetermine valideren laag 2-configuratie en de verbinding. Deze sectie bevat een overzicht van hoe ARP-tabellen onder verschillende scenario's eruit.

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a>ARP-tabel wanneer een circuit bevindt zich in de operationele status (verwachte status)
* Hallo ARP-tabel heeft een vermelding voor Hallo lokale zijde met een geldig IP-adres en MAC-adres en een vergelijkbare vermelding voor Hallo Microsoft aan clientzijde. 
* laatste octet Hallo van Hallo lokale IP-adres wordt altijd een oneven getal zijn.
* de laatste octet Hallo Hallo Microsoft IP-adres wordt altijd een even getal zijn.
* Hallo hetzelfde MAC-adres wordt weergegeven op Hallo Microsoft aan clientzijde voor alle 3 peerings (primaire / secundaire). 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a>ARP-tabel wanneer lokale / verbinding-provider heeft problemen
Als er problemen met Hallo on-premises zijn of connectiviteitsprovider mogelijk ziet u beide slechts één vermelding wordt weergegeven in Hallo ARP tabel of Hallo on-premises MAC-adres wordt niet volledig weergeven. Hallo-toewijzing tussen Hallo MAC-adres en IP-adres in Hallo Microsoft side laat zien. 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

of
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> Een ondersteuningsaanvraag openen met uw provider connectiviteit toodebug dergelijke problemen. Als Hallo ARP-tabel geen heeft toegewezen IP-adressen van de interfaces Hallo tooMAC adressen, bekijk Hallo volgende informatie:
> 
> 1. Als het eerste IP-adres Hallo van Hallo /30 subnet voor Hallo koppeling tussen toegewezen Hallo MSEE PR en MSEE wordt gebruikt op Hallo-interface van MSEE PR. Azure gebruikt altijd Hallo tweede IP-adres voor de msee's.
> 2. Controleer of als Hallo klant (C-code) en VLAN-servicetags (S-Tag) overeenkomt met beide op een combinatie van MSEE PR en MSEE.
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a>ARP-tabel bij Microsoft problemen heeft
* U ziet een ARP-tabel wordt weergegeven voor een peering als er problemen op Hallo Microsoft aan clientzijde zijn. 
* Open een ondersteuningsticket met [Microsoft ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Geef op of er een probleem met laag 2-connectiviteit. 

## <a name="next-steps"></a>Volgende stappen
* Layer 3-configuraties voor uw ExpressRoute-circuit valideren
  * Ophalen van de route samenvatting toodetermine Hallo status van de BGP-sessies 
  * Route tabel toodetermine welke voorvoegsels worden geadverteerd via ExpressRoute ophalen
* Overdracht van gegevens aan de hand van de bytes in / out-valideren
* Open een ondersteuningsticket met [Microsoft ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) als u nog steeds problemen ondervindt.

