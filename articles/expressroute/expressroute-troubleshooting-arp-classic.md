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
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a>ARP ophalen tabellen in het klassieke implementatiemodel Hallo
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - Klassiek](expressroute-troubleshooting-arp-classic.md)
> 
> 

Dit artikel begeleidt u bij Hallo stappen voor het ophalen van Hallo Protocol ARP (Address Resolution) tabellen voor uw Azure ExpressRoute-circuit.

> [!IMPORTANT]
> Dit document is bedoeld toohelp u opsporen en oplossen van eenvoudige problemen. Het is niet bedoeld toobe vervanging voor ondersteuning van Microsoft. Als u op Hallo probleem oplossen kunt met behulp van Hallo richtlijnen te volgen, opent u een ondersteuningsaanvraag met [Microsoft Azure Help + ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>Adres van de tabellen ARP (Resolution Protocol) en ARP
ARP is een Layer 2-protocol die gedefinieerd in [RFC 826](https://tools.ietf.org/html/rfc826). ARP is gebruikte toomap een Ethernet-adres (MAC-adres) tooan IP-adres.

Een ARP-tabel bevat een toewijzing van Hallo IPv4-adres en MAC-adres voor een bepaalde peering. Hallo ARP-tabel voor een ExpressRoute-circuitpeering biedt Hallo volgende informatie voor elke interface (primair en secundair):

1. Toewijzing van een lokale router interface IP-adres tooa MAC-adres
2. Toewijzing van een ExpressRoute-router interface IP-adres tooa MAC-adres
3. Hallo leeftijd van Hallo-toewijzing

ARP-tabellen kunnen u met Layer 2-configuratie wordt gevalideerd en basic Layer 2-verbindingsproblemen op te lossen.

Hieronder volgt een voorbeeld van een ARP-tabel:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


Hallo volgende sectie bevat informatie over hoe tooview ARP-tabellen die zijn zichtbaar voor de ExpressRoute-randrouters Hallo Hallo.

## <a name="prerequisites-for-using-arp-tables"></a>Vereisten voor het gebruik van ARP-tabellen
Zorg ervoor dat u Hallo volgende hebt voordat u verdergaat:

* Een geldig ExpressRoute-circuit dat geconfigureerd met ten minste één peering. Hallo circuit moet volledig worden geconfigureerd door de connectiviteitsprovider Hallo. U (of uw connectiviteitsprovider) moet configureren ten minste één Hallo peerings (Azure privé, Azure openbaar of Microsoft) op dit circuit.
* IP-adresbereiken die worden gebruikt voor het configureren van Hallo peerings (Azure privé, Azure openbaar en Microsoft). Hallo IP-adres toewijzing voorbeelden in Hallo bekijkt [pagina voor ExpressRoute routing requirements](expressroute-routing.md) tooget een goed begrip van hoe IP-adressen zijn toegewezen toointerfaces op uw aise en Hallo ExpressRoute-zijde. U kunt informatie ophalen over Hallo peeringconfiguratie aan de hand van Hallo [configuratiepagina van de ExpressRoute-peering](expressroute-howto-routing-classic.md).
* Gegevens van uw netwerk team of connectiviteit provider over Hallo MAC-adressen van Hallo-interfaces die worden gebruikt met deze IP-adressen.
* Hallo nieuwste Windows PowerShell-module voor Azure (versie 1,50 of hoger).

## <a name="arp-tables-for-your-expressroute-circuit"></a>ARP-tabellen voor uw ExpressRoute-circuit
Deze sectie bevat instructies over hoe tooview Hallo ARP voor elk type peering tabellen met behulp van PowerShell. Voordat u doorgaat, moet u of uw connectiviteitsprovider tooconfigure hello peering. Elk circuit heeft twee paden (primair en secundair). U kunt onafhankelijk Hallo ARP-tabel voor elk pad controleren.

### <a name="arp-tables-for-azure-private-peering"></a>ARP-tabellen voor persoonlijke Azure-peering
Hallo volgende cmdlet biedt Hallo ARP tabellen voor persoonlijke Azure-peering:

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

Hieronder volgt een voorbeeld van uitvoer voor een van de paden Hallo:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>ARP-tabellen voor openbare Azure-peering:
Hallo volgende cmdlet biedt Hallo ARP tabellen voor openbare Azure-peering:

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

Hieronder volgt een voorbeeld van uitvoer voor een van de paden Hallo:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


Hieronder volgt een voorbeeld van uitvoer voor een van de paden Hallo:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>ARP-tabellen voor Microsoft-peering
Hallo volgende cmdlet biedt Hallo ARP tabellen voor Microsoft-peering:

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


Voorbeeld van uitvoer wordt hieronder weergegeven voor een Hallo paden:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Hoe toouse deze informatie
Hallo ARP-tabel van een peering mag gebruikte toovalidate Layer 2-configuratie en de verbinding. Deze sectie biedt een overzicht van hoe de ARP-tabellen in verschillende scenario's eruit zien.

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a>ARP-tabel wanneer een circuit bevindt zich in een operationele status (verwachte)
* Hallo ARP-tabel heeft een vermelding voor Hallo lokale zijde met een geldig IP- en MAC-adres en een vergelijkbare vermelding voor Hallo Microsoft aan clientzijde.
* de laatste octet Hallo van Hallo lokale IP-adres is altijd een oneven getal.
* de laatste octet Hallo Hallo Microsoft IP-adres is altijd een even getal zijn.
* Hallo hetzelfde MAC-adres wordt weergegeven op Hallo Microsoft aan clientzijde voor alle drie de peerings (primaire en secundaire).

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a>ARP-tabel wanneer deze on-premises of wanneer Hallo-connectiviteitsprovider heeft problemen
 Slechts één vermelding verschijnt in Hallo ARP-tabel. Hallo-toewijzing tussen Hallo MAC-adres en Hallo IP-adres dat wordt gebruikt op Hallo Microsoft aan clientzijde worden weergegeven.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> Als er een probleem als volgt, opent u een ondersteuning vragen met uw provider connectiviteit tooresolve.
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a>ARP-tabel wanneer Hallo Microsoft side problemen heeft
* U ziet een ARP-tabel wordt weergegeven voor een peering als er problemen op Hallo Microsoft aan clientzijde zijn.
* Open een ondersteuningsverzoek met [Microsoft Azure Help + ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Geef op of er een probleem met Layer 2-connectiviteit.

## <a name="next-steps"></a>Volgende stappen
* Layer 3-configuraties voor uw ExpressRoute-circuit valideren:
  * Een route samenvatting toodetermine Hallo status van de BGP-sessies worden opgehaald.
  * Ophalen van een route tabel toodetermine welke voorvoegsels worden geadverteerd via ExpressRoute.
* Valideer de overdracht van gegevens aan de hand van bytes in en uit.
* Open een ondersteuningsverzoek met [Microsoft Azure Help + ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) als u nog steeds problemen ondervindt.

