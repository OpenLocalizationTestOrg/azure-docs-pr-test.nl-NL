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
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a><span data-ttu-id="92a11-103">Configuratie van de router tooset up voorbeelden en beheren van NAT</span><span class="sxs-lookup"><span data-stu-id="92a11-103">Router configuration samples tooset up and manage NAT</span></span>
<span data-ttu-id="92a11-104">Deze pagina vindt u voorbeelden van de NAT-configuratie voor Cisco ASA en Juniper SRX reeks routers.</span><span class="sxs-lookup"><span data-stu-id="92a11-104">This page provides NAT configuration samples for Cisco ASA and Juniper SRX series routers.</span></span> <span data-ttu-id="92a11-105">Deze voorbeelden van de beoogde toobe voor alleen richtlijnen zijn en mogen niet worden gebruikt omdat de.</span><span class="sxs-lookup"><span data-stu-id="92a11-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="92a11-106">U kunt werken met uw leverancier toocome up met relevante configuraties voor uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="92a11-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="92a11-107">Voorbeelden in deze pagina zijn beoogde toobe puur voor hulp.</span><span class="sxs-lookup"><span data-stu-id="92a11-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="92a11-108">Bespreek met de leverancier van uw verkoop / technisch team en uw netwerken team toocome up met relevante configuraties toomeet uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="92a11-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="92a11-109">Microsoft ondersteunt geen problemen die worden vermeld in deze pagina tooconfigurations gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="92a11-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="92a11-110">Neem contact op met de leverancier van uw apparaat voor ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="92a11-110">You must contact your device vendor for support issues.</span></span>
> 
> 

* <span data-ttu-id="92a11-111">Router configuratie voorbeelden hieronder toepassing tooAzure openbaar en Microsoft-peerings.</span><span class="sxs-lookup"><span data-stu-id="92a11-111">Router configuration samples below apply tooAzure Public and Microsoft peerings.</span></span> <span data-ttu-id="92a11-112">U moet de NAT niet configureren voor persoonlijke Azure-peering.</span><span class="sxs-lookup"><span data-stu-id="92a11-112">You must not configure NAT for Azure private peering.</span></span> <span data-ttu-id="92a11-113">Bekijk [ExpressRoute peerings](expressroute-circuit-peerings.md) en [ExpressRoute NAT-vereisten](expressroute-nat.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="92a11-113">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute NAT requirements](expressroute-nat.md) for more details.</span></span>

* <span data-ttu-id="92a11-114">U moet afzonderlijke NAT IP-groepen gebruiken voor connectiviteit toohello internet- en ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="92a11-114">You MUST use separate NAT IP pools for connectivity toohello internet and ExpressRoute.</span></span> <span data-ttu-id="92a11-115">Hallo dezelfde NAT IP-groep op Hallo van internet en ExpressRoute leidt ertoe dat asymmetrische Routering en verlies van verbinding.</span><span class="sxs-lookup"><span data-stu-id="92a11-115">Using hello same NAT IP pool across hello internet and ExpressRoute will result in asymmetric routing and loss of connectivity.</span></span>


## <a name="cisco-asa-firewalls"></a><span data-ttu-id="92a11-116">Cisco ASA firewalls</span><span class="sxs-lookup"><span data-stu-id="92a11-116">Cisco ASA firewalls</span></span>
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a><span data-ttu-id="92a11-117">PAT configuratie voor verkeer van de klant netwerk tooMicrosoft</span><span class="sxs-lookup"><span data-stu-id="92a11-117">PAT configuration for traffic from customer network tooMicrosoft</span></span>
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

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a><span data-ttu-id="92a11-118">PAT configuratie voor verkeer vanuit Microsoft toocustomer netwerk</span><span class="sxs-lookup"><span data-stu-id="92a11-118">PAT configuration for traffic from Microsoft toocustomer network</span></span>

<span data-ttu-id="92a11-119">**Interfaces en de richting:**</span><span class="sxs-lookup"><span data-stu-id="92a11-119">**Interfaces and Direction:**</span></span>

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

<span data-ttu-id="92a11-120">**Configuratie:**</span><span class="sxs-lookup"><span data-stu-id="92a11-120">**Configuration:**</span></span>

<span data-ttu-id="92a11-121">NAT-adresgroep:</span><span class="sxs-lookup"><span data-stu-id="92a11-121">NAT Pool:</span></span>

    object network outbound-PAT
        host <NAT-IP>

<span data-ttu-id="92a11-122">Doelserver:</span><span class="sxs-lookup"><span data-stu-id="92a11-122">Target Server:</span></span>

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

<span data-ttu-id="92a11-123">Object-groep voor IP-adressen van klanten</span><span class="sxs-lookup"><span data-stu-id="92a11-123">Object Group for Customer IP Addresses</span></span>

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

<span data-ttu-id="92a11-124">NAT-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="92a11-124">NAT Commands:</span></span>

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a><span data-ttu-id="92a11-125">Juniper SRX reeks routers</span><span class="sxs-lookup"><span data-stu-id="92a11-125">Juniper SRX series routers</span></span>
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a><span data-ttu-id="92a11-126">1. Redundante Ethernet-interfaces voor Hallo cluster maken</span><span class="sxs-lookup"><span data-stu-id="92a11-126">1. Create redundant Ethernet interfaces for hello cluster</span></span>
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


### <a name="2-create-two-security-zones"></a><span data-ttu-id="92a11-127">2. Twee beveiligingszones maken</span><span class="sxs-lookup"><span data-stu-id="92a11-127">2. Create two security zones</span></span>
* <span data-ttu-id="92a11-128">Zone voor het interne netwerk en Untrust Zone vertrouwen voor extern gerichte Randrouters-netwerk</span><span class="sxs-lookup"><span data-stu-id="92a11-128">Trust Zone for internal network and Untrust Zone for external network facing Edge Routers</span></span>
* <span data-ttu-id="92a11-129">Juiste interfaces toohello zones toewijzen</span><span class="sxs-lookup"><span data-stu-id="92a11-129">Assign appropriate interfaces toohello zones</span></span>
* <span data-ttu-id="92a11-130">Hallo-interfaces-services toestaan</span><span class="sxs-lookup"><span data-stu-id="92a11-130">Allow services on hello interfaces</span></span>

    <span data-ttu-id="92a11-131">beveiliging {zones {beveiligingszone vertrouwensrelatie {-inkomende-hostverkeer {-systeemservices {ping;                   } protocollen {bgp;                   interfaces}} {reth0.100;               }} beveiligingszone Untrust {-inkomende-hostverkeer {-systeemservices {ping;                   } protocollen {bgp;                   interfaces}} {reth1.100;               }           }       }   }</span><span class="sxs-lookup"><span data-stu-id="92a11-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span></span>


### <a name="3-create-security-policies-between-zones"></a><span data-ttu-id="92a11-132">3. Beveiligingsbeleid tussen de zones maken</span><span class="sxs-lookup"><span data-stu-id="92a11-132">3. Create security policies between zones</span></span>
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


### <a name="4-configure-nat-policies"></a><span data-ttu-id="92a11-133">4. NAT-beleid configureren</span><span class="sxs-lookup"><span data-stu-id="92a11-133">4. Configure NAT policies</span></span>
* <span data-ttu-id="92a11-134">Maak twee NAT-adresgroepen.</span><span class="sxs-lookup"><span data-stu-id="92a11-134">Create two NAT pools.</span></span> <span data-ttu-id="92a11-135">Een zijn van Microsoft toohello klant gebruikte tooNAT verkeer uitgaand tooMicrosoft en andere.</span><span class="sxs-lookup"><span data-stu-id="92a11-135">One will be used tooNAT traffic outbound tooMicrosoft and other from Microsoft toohello customer.</span></span>
* <span data-ttu-id="92a11-136">Regels maken tooNAT Hallo respectieve verkeer</span><span class="sxs-lookup"><span data-stu-id="92a11-136">Create rules tooNAT hello respective traffic</span></span>
  
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

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a><span data-ttu-id="92a11-137">5. BGP tooadvertise selectief voorvoegsels in elke richting configureren</span><span class="sxs-lookup"><span data-stu-id="92a11-137">5. Configure BGP tooadvertise selective prefixes in each direction</span></span>
<span data-ttu-id="92a11-138">Raadpleeg toosamples in [routering configuratie voorbeelden ](expressroute-config-samples-routing.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="92a11-138">Refer toosamples in [Routing configuration samples ](expressroute-config-samples-routing.md) page.</span></span>

### <a name="6-create-policies"></a><span data-ttu-id="92a11-139">6. Beleid maken</span><span class="sxs-lookup"><span data-stu-id="92a11-139">6. Create policies</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="92a11-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="92a11-140">Next steps</span></span>
<span data-ttu-id="92a11-141">Zie Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="92a11-141">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

