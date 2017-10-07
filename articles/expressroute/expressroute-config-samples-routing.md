---
title: Voorbeelden van aaaExpressRoute klant router configuratie | Microsoft Docs
description: Deze pagina vindt u voorbeelden van router config voor Cisco en Juniper routers.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 564826bc-017a-4683-a385-37c9fa814948
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 5c91f24e6082e01c3e8df91b4fcfda46a6c29fa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a>Configuratie van de router tooset voorbeelden van en beheren van Routering
Deze pagina bevat de interface en routering configuratie voorbeelden voor IOS-XE van Cisco en Juniper MX reeks routers. Deze voorbeelden van de beoogde toobe voor alleen richtlijnen zijn en mogen niet worden gebruikt omdat de. U kunt werken met uw leverancier toocome up met relevante configuraties voor uw netwerk. 

> [!IMPORTANT]
> Voorbeelden in deze pagina zijn beoogde toobe puur voor hulp. Bespreek met de leverancier van uw verkoop / technisch team en uw netwerken team toocome up met relevante configuraties toomeet uw behoeften. Microsoft ondersteunt geen problemen die worden vermeld in deze pagina tooconfigurations gerelateerd. Neem contact op met de leverancier van uw apparaat voor ondersteuning.
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a>MTU en TCP MSS-instellingen op de interfaces van router
* Hallo MTU voor Hallo ExpressRoute-interface is 1500, Hallo typische standaard MTU voor een Ethernet-interface op een router. Tenzij uw router een andere MTU standaard heeft, is er geen toospecify moet een waarde op Hallo-routerinterface.
* In tegenstelling tot een Azure VPN-Gateway hoeft Hallo TCP MSS voor een ExpressRoute-circuit niet toobe opgegeven.

Router configuratie voorbeelden hieronder tooall peerings van toepassing. Bekijk [ExpressRoute peerings](expressroute-circuit-peerings.md) en [routeringsvereisten voor ExpressRoute](expressroute-routing.md) voor meer informatie over routering.


## <a name="cisco-ios-xe-based-routers"></a>Cisco IOS-XE gebaseerd routers
Hallo-voorbeelden in deze sectie zijn van toepassing voor een IOS-XE-OS-familie van Hallo-router.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Interfaces en onderliggende interfaces configureren
U moet een sub-interface per peering in elke router verbinding tooMicrosoft. Een sub-interface kan worden geïdentificeerd met een VLAN-ID of een gestapelde paar VLAN-id's en een IP-adres.

**Dot1Q interfacedefinitie**

Dit voorbeeld bevat Hallo onderliggende interfacedefinitie voor een onderliggende interface met een enkel VLAN-ID. Hallo VLAN-ID is uniek per peering. laatste octet Hallo van uw IPv4-adres wordt altijd een oneven getal zijn.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

**QinQ interfacedefinitie**

Dit voorbeeld bevat Hallo onderliggende interfacedefinitie voor een onderliggende interface met twee VLAN-id. Hallo buitenste VLAN-ID (s-code), als gebruikt blijft Hallo dezelfde over alle Hallo-peerings. Hallo interne (c-code) van de VLAN-ID is uniek per peering. laatste octet Hallo van uw IPv4-adres wordt altijd een oneven getal zijn.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a>2. Instellen van eBGP-sessies
U moet een BGP-sessie met Microsoft voor elke peering instellen. Hallo onderstaand voorbeeld kunt u toosetup een BGP-sessie met Microsoft. Als Hallo IPv4-adres die u hebt gebruikt voor de sub-interface a.b.c.d, zich Hallo IP-adres van Hallo BGP neighbor (Microsoft) a.b.c.d+1. de laatste octet Hallo van Hallo BGP neighbor IPv4-adres wordt altijd een even getal zijn.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Instellen van voorvoegsels toobe geadverteerd via Hallo BGP-sessie
U kunt uw router tooadvertise Selecteer voorvoegsels tooMicrosoft configureren. U kunt doen met behulp van Hallo onderstaand voorbeeld.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a>4. Route maps
Kunt u route-kaarten en voorvoegsel vermeldt toofilter voorvoegsels doorgegeven in uw netwerk. U kunt Hallo voorbeeld hieronder tooaccomplish Hallo taak gebruiken. Zorg ervoor dat er bijbehorende voorvoegsel een lijst met setup.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
      neighbor <IP#2_used_by_Azure> route-map <MS_Prefixes_Inbound> in
     exit-address-family
    !
    route-map <MS_Prefixes_Inbound> permit 10
     match ip address prefix-list <MS_Prefixes>
    !


## <a name="juniper-mx-series-routers"></a>Juniper MX reeks routers
Hallo-voorbeelden in deze sectie gelden voor alle reeksen Juniper MX routers.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Interfaces en onderliggende interfaces configureren

**Dot1Q interfacedefinitie**

Dit voorbeeld bevat Hallo onderliggende interfacedefinitie voor een onderliggende interface met een enkel VLAN-ID. Hallo VLAN-ID is uniek per peering. laatste octet Hallo van uw IPv4-adres wordt altijd een oneven getal zijn.

    interfaces {
        vlan-tagging;
        <Interface_Number> {
            unit <Number> {
                vlan-id <VLAN_ID>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }
            }
        }
    }


**QinQ interfacedefinitie**

Dit voorbeeld bevat Hallo onderliggende interfacedefinitie voor een onderliggende interface met twee VLAN-id. Hallo buitenste VLAN-ID (s-code), als gebruikt blijft Hallo dezelfde over alle Hallo-peerings. Hallo interne (c-code) van de VLAN-ID is uniek per peering. laatste octet Hallo van uw IPv4-adres wordt altijd een oneven getal zijn.

    interfaces {
        <Interface_Number> {
            flexible-vlan-tagging;
            unit <Number> {
                vlan-tags outer <S-tag> inner <C-tag>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }                           
            }                               
        }                                   
    }                           

### <a name="2-setting-up-ebgp-sessions"></a>2. Instellen van eBGP-sessies
U moet een BGP-sessie met Microsoft voor elke peering instellen. Hallo onderstaand voorbeeld kunt u toosetup een BGP-sessie met Microsoft. Als Hallo IPv4-adres die u hebt gebruikt voor de sub-interface a.b.c.d, zich Hallo IP-adres van Hallo BGP neighbor (Microsoft) a.b.c.d+1. de laatste octet Hallo van Hallo BGP neighbor IPv4-adres wordt altijd een even getal zijn.

    routing-options {
        autonomous-system <Customer_ASN>;
    }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Instellen van voorvoegsels toobe geadverteerd via Hallo BGP-sessie
U kunt uw router tooadvertise Selecteer voorvoegsels tooMicrosoft configureren. U kunt doen met behulp van Hallo onderstaand voorbeeld.

    policy-options {
        policy-statement <Policy_Name> {
            term 1 {
                from protocol OSPF;
        route-filter <Prefix_to_be_advertised/Subnet_Mask> exact;
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }


### <a name="4-route-maps"></a>4. Route maps
Kunt u route-kaarten en voorvoegsel vermeldt toofilter voorvoegsels doorgegeven in uw netwerk. U kunt Hallo voorbeeld hieronder tooaccomplish Hallo taak gebruiken. Zorg ervoor dat er bijbehorende voorvoegsel een lijst met setup.

    policy-options {
        prefix-list MS_Prefixes {
            <IP_Prefix_1/Subnet_Mask>;
            <IP_Prefix_2/Subnet_Mask>;
        }
        policy-statement <MS_Prefixes_Inbound> {
            term 1 {
                from {
        prefix-list MS_Prefixes;
                }
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                import <MS_Prefixes_Inbound>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

## <a name="next-steps"></a>Volgende stappen
Zie Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md) voor meer informatie.

