---
title: Voorbeelden van aaaExpressRoute klant router configuratie | Microsoft Docs
description: Deze pagina vindt u voorbeelden van de router-configuratie voor Cisco en Juniper routers.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: d6ea716f-d5ee-4a61-92b0-640d6e7d6974
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: b5faca0666bda6173e54abb0b6560d5f8bf8bfc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a>Configuratie van de router tooset up voorbeelden en beheren van NAT
Deze pagina vindt u voorbeelden van de NAT-configuratie voor Cisco ASA en Juniper SRX reeks routers. Deze voorbeelden van de beoogde toobe voor alleen richtlijnen zijn en mogen niet worden gebruikt omdat de. U kunt werken met uw leverancier toocome up met relevante configuraties voor uw netwerk. 

> [!IMPORTANT]
> Voorbeelden in deze pagina zijn beoogde toobe puur voor hulp. Bespreek met de leverancier van uw verkoop / technisch team en uw netwerken team toocome up met relevante configuraties toomeet uw behoeften. Microsoft ondersteunt geen problemen die worden vermeld in deze pagina tooconfigurations gerelateerd. Neem contact op met de leverancier van uw apparaat voor ondersteuning.
> 
> 

* Router configuratie voorbeelden hieronder toepassing tooAzure openbaar en Microsoft-peerings. U moet de NAT niet configureren voor persoonlijke Azure-peering. Bekijk [ExpressRoute peerings](expressroute-circuit-peerings.md) en [ExpressRoute NAT-vereisten](expressroute-nat.md) voor meer informatie.

* U moet afzonderlijke NAT IP-groepen gebruiken voor connectiviteit toohello internet- en ExpressRoute. Hallo dezelfde NAT IP-groep op Hallo van internet en ExpressRoute leidt ertoe dat asymmetrische Routering en verlies van verbinding.


## <a name="cisco-asa-firewalls"></a>Cisco ASA firewalls
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a>PAT configuratie voor verkeer van de klant netwerk tooMicrosoft
    object network MSFT-PAT
      range <SNAT-START-IP> <SNAT-END-IP>


    object-group network MSFT-Range
      network-object <IP> <Subnet_Mask>

    object-group network on-prem-range-1
      network-object <IP> <Subnet-Mask>

    object-group network on-prem-range-2
      network-object <IP> <Subnet-Mask>

    object-group network on-prem
      network-object object on-prem-range-1
      network-object object on-prem-range-2

    nat (outside,inside) source dynamic on-prem pat-pool MSFT-PAT destination static MSFT-Range MSFT-Range

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a>PAT configuratie voor verkeer vanuit Microsoft toocustomer netwerk

**Interfaces en de richting:**

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

**Configuratie:**

NAT-adresgroep:

    object network outbound-PAT
        host <NAT-IP>

Doelserver:

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

Object-groep voor IP-adressen van klanten

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

NAT-opdrachten:

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a>Juniper SRX reeks routers
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a>1. Redundante Ethernet-interfaces voor Hallo cluster maken
    interfaces {
        reth0 {
            description "tooInternal Network";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 1;
            }
            unit 100 {
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
        reth1 {
            description "tooMicrosoft via Edge Router";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 2;
            }
            unit 100 {
                description "tooMicrosoft via Edge Router";
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
    }


### <a name="2-create-two-security-zones"></a>2. Twee beveiligingszones maken
* Zone voor het interne netwerk en Untrust Zone vertrouwen voor extern gerichte Randrouters-netwerk
* Juiste interfaces toohello zones toewijzen
* Hallo-interfaces-services toestaan

    beveiliging {zones {beveiligingszone vertrouwensrelatie {-inkomende-hostverkeer {-systeemservices {ping;                   } protocollen {bgp;                   interfaces}} {reth0.100;               }} beveiligingszone Untrust {-inkomende-hostverkeer {-systeemservices {ping;                   } protocollen {bgp;                   interfaces}} {reth1.100;               }           }       }   }


### <a name="3-create-security-policies-between-zones"></a>3. Beveiligingsbeleid tussen de zones maken
    security {
        policies {
            from-zone Trust to-zone Untrust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
            from-zone Untrust to-zone Trust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
        }
    }


### <a name="4-configure-nat-policies"></a>4. NAT-beleid configureren
* Maak twee NAT-adresgroepen. Een zijn van Microsoft toohello klant gebruikte tooNAT verkeer uitgaand tooMicrosoft en andere.
* Regels maken tooNAT Hallo respectieve verkeer
  
       security {
           nat {
               source {
                   pool SNAT-To-ExpressRoute {
                       routing-instance {
                           External-ExpressRoute;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   pool SNAT-From-ExpressRoute {
                       routing-instance {
                           Internal;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   rule-set Outbound_NAT {
                       from routing-instance Internal;
                       toorouting-instance External-ExpressRoute;
                       rule SNAT-Out {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-To-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
                   rule-set Inbound-NAT {
                       from routing-instance External-ExpressRoute;
                       toorouting-instance Internal;
                       rule SNAT-In {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-From-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
               }
           }
       }

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a>5. BGP tooadvertise selectief voorvoegsels in elke richting configureren
Raadpleeg toosamples in [routering configuratie voorbeelden ](expressroute-config-samples-routing.md) pagina.

### <a name="6-create-policies"></a>6. Beleid maken
    routing-options {
                  autonomous-system <Customer-ASN>;
    }
    policy-options {
        prefix-list Microsoft-Prefixes {
            <IP-Address/Subnet-Mask;
            <IP-Address/Subnet-Mask;
        }
        prefix-list private-ranges {
            10.0.0.0/8;
            172.16.0.0/12;
            192.168.0.0/16;
            100.64.0.0/10;
        }
        policy-statement Advertise-NAT-Pools {
            from {
                protocol static;
                route-filter <NAT-Pool-Address/Subnet-mask> prefix-length-range /32-/32;
            }
            then accept;
        }
        policy-statement Accept-from-Microsoft {
            term 1 {
                from {
                    instance External-ExpressRoute;
                    prefix-list-filter Microsoft-Prefixes orlonger;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
        policy-statement Accept-from-Internal {
            term no-private {
                from {
                    instance Internal;
                    prefix-list-filter private-ranges orlonger;
                }
                then reject;
            }
            term bgp {
                from {
                    instance Internal;
                    protocol bgp;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
    }
    routing-instances {
        Internal {
            instance-type virtual-router;
            interface reth0.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Microsoft;
            }
            protocols {
                bgp {
                    group customer {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-ASN-1>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
        External-ExpressRoute {
            instance-type virtual-router;
            interface reth1.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Internal;
            }
            protocols {
                bgp {
                    group edge-router {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-Public-ASN>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
    }

## <a name="next-steps"></a>Volgende stappen
Zie Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md) voor meer informatie.

