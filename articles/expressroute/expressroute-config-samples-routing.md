---
title: ExpressRoute klant router configuratie voorbeelden | Microsoft Docs
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
ms.openlocfilehash: 032e584dc5abf59e9e3e8d80673b402f1fbf721b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="router-configuration-samples-to-set-up-and-manage-routing"></a><span data-ttu-id="26af4-103">Voorbeelden van de router configuratie instellen en beheren van Routering</span><span class="sxs-lookup"><span data-stu-id="26af4-103">Router configuration samples to set up and manage routing</span></span>
<span data-ttu-id="26af4-104">Deze pagina bevat de interface en routering configuratie voorbeelden voor IOS-XE van Cisco en Juniper MX reeks routers.</span><span class="sxs-lookup"><span data-stu-id="26af4-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="26af4-105">Deze zijn bedoeld als voorbeelden voor richtlijnen alleen en moeten niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="26af4-105">These are intended to be samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="26af4-106">U kunt werken met uw leverancier om te bedenken geschikte configuraties voor uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="26af4-106">You can work with your vendor to come up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="26af4-107">Voorbeelden in deze pagina zijn bedoeld om te worden uitsluitend voor hulp.</span><span class="sxs-lookup"><span data-stu-id="26af4-107">Samples in this page are intended to be purely for guidance.</span></span> <span data-ttu-id="26af4-108">Bespreek met de leverancier van uw verkoop / technisch team en uw netwerken team actief met relevante configuraties om te voldoen aan uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="26af4-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span></span> <span data-ttu-id="26af4-109">Problemen met configuraties die worden vermeld in deze pagina wordt niet door Microsoft ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="26af4-109">Microsoft will not support issues related to configurations listed in this page.</span></span> <span data-ttu-id="26af4-110">Neem contact op met de leverancier van uw apparaat voor ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="26af4-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="26af4-111">MTU en TCP MSS-instellingen op de interfaces van router</span><span class="sxs-lookup"><span data-stu-id="26af4-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="26af4-112">De MTU van de ExpressRoute-interface is 1500, de gangbare standaard MTU voor een Ethernet-interface op een router.</span><span class="sxs-lookup"><span data-stu-id="26af4-112">The MTU for the ExpressRoute interface is 1500, which is the typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="26af4-113">Tenzij uw router een andere MTU standaard heeft, is er niet nodig om op te geven van een waarde op de routerinterface.</span><span class="sxs-lookup"><span data-stu-id="26af4-113">Unless your router has a different MTU by default, there is no need to specify a value on the router interface.</span></span>
* <span data-ttu-id="26af4-114">In tegenstelling tot een Azure VPN-Gateway hoeft de TCP-MSS voor een ExpressRoute-circuit niet te worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="26af4-114">Unlike an Azure VPN Gateway, the TCP MSS for an ExpressRoute circuit does not need to be specified.</span></span>

<span data-ttu-id="26af4-115">Router configuratie voorbeelden van toepassing op alle peerings.</span><span class="sxs-lookup"><span data-stu-id="26af4-115">Router configuration samples below apply to all peerings.</span></span> <span data-ttu-id="26af4-116">Bekijk [ExpressRoute peerings](expressroute-circuit-peerings.md) en [routeringsvereisten voor ExpressRoute](expressroute-routing.md) voor meer informatie over routering.</span><span class="sxs-lookup"><span data-stu-id="26af4-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="26af4-117">Cisco IOS-XE gebaseerd routers</span><span class="sxs-lookup"><span data-stu-id="26af4-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="26af4-118">De voorbeelden in deze sectie voor een router met de IOS-XE-OS-familie van toepassing.</span><span class="sxs-lookup"><span data-stu-id="26af4-118">The samples in this section apply for any router running the IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="26af4-119">1. Interfaces en onderliggende interfaces configureren</span><span class="sxs-lookup"><span data-stu-id="26af4-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="26af4-120">U moet een sub-interface per in elke router die u verbinding met Microsoft maken-peering.</span><span class="sxs-lookup"><span data-stu-id="26af4-120">You will require a sub interface per peering in every router you connect to Microsoft.</span></span> <span data-ttu-id="26af4-121">Een sub-interface kan worden geïdentificeerd met een VLAN-ID of een gestapelde paar VLAN-id's en een IP-adres.</span><span class="sxs-lookup"><span data-stu-id="26af4-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="26af4-122">**Dot1Q interfacedefinitie**</span><span class="sxs-lookup"><span data-stu-id="26af4-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="26af4-123">In dit voorbeeld worden de onderliggende interfacedefinitie voor een onderliggende interface met een enkel VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="26af4-123">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="26af4-124">De VLAN-ID is uniek per peering.</span><span class="sxs-lookup"><span data-stu-id="26af4-124">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="26af4-125">Het laatste octet van uw IPv4-adres wordt altijd een oneven getal zijn.</span><span class="sxs-lookup"><span data-stu-id="26af4-125">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="26af4-126">**QinQ interfacedefinitie**</span><span class="sxs-lookup"><span data-stu-id="26af4-126">**QinQ interface definition**</span></span>

<span data-ttu-id="26af4-127">Dit voorbeeld bevat de submappen interfacedefinitie voor een onderliggende interface met twee VLAN-id.</span><span class="sxs-lookup"><span data-stu-id="26af4-127">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="26af4-128">De buitenste VLAN-ID (s-code), als het gebruikt hetzelfde is gebleven via de peerings.</span><span class="sxs-lookup"><span data-stu-id="26af4-128">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="26af4-129">De interne (c-code) van de VLAN-ID is uniek per peering.</span><span class="sxs-lookup"><span data-stu-id="26af4-129">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="26af4-130">Het laatste octet van uw IPv4-adres wordt altijd een oneven getal zijn.</span><span class="sxs-lookup"><span data-stu-id="26af4-130">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="26af4-131">2. Instellen van eBGP-sessies</span><span class="sxs-lookup"><span data-stu-id="26af4-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="26af4-132">U moet een BGP-sessie met Microsoft voor elke peering instellen.</span><span class="sxs-lookup"><span data-stu-id="26af4-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="26af4-133">Het onderstaande voorbeeld kunt u instellen dat een BGP-sessie met Microsoft.</span><span class="sxs-lookup"><span data-stu-id="26af4-133">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="26af4-134">Als het IPv4-adres dat u voor uw sub-interface gebruikt a.b.c.d is, worden de IP-adres van de BGP-neighbor (Microsoft) a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="26af4-134">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="26af4-135">Het laatste octet van de BGP-neighbor IPv4-adres wordt altijd een even getal zijn.</span><span class="sxs-lookup"><span data-stu-id="26af4-135">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="26af4-136">3. Voorvoegsels instellen om te worden geadverteerd via de BGP-sessie</span><span class="sxs-lookup"><span data-stu-id="26af4-136">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="26af4-137">U kunt uw router voor het adverteren Selecteer voorvoegsels naar Microsoft configureren.</span><span class="sxs-lookup"><span data-stu-id="26af4-137">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="26af4-138">U kunt dit doen met behulp van het voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="26af4-138">You can do so using the sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="26af4-139">4. Route maps</span><span class="sxs-lookup"><span data-stu-id="26af4-139">4. Route maps</span></span>
<span data-ttu-id="26af4-140">U kunt gebruiken route-kaarten en voorvoegsel lijsten moeten filter voorvoegsels doorgegeven in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="26af4-140">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="26af4-141">Het onderstaande voorbeeld kunt u de taak uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="26af4-141">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="26af4-142">Zorg ervoor dat er bijbehorende voorvoegsel een lijst met setup.</span><span class="sxs-lookup"><span data-stu-id="26af4-142">Ensure that you have appropriate prefix lists setup.</span></span>

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


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="26af4-143">Juniper MX reeks routers</span><span class="sxs-lookup"><span data-stu-id="26af4-143">Juniper MX series routers</span></span>
<span data-ttu-id="26af4-144">De voorbeelden in deze sectie gelden voor alle reeksen Juniper MX routers.</span><span class="sxs-lookup"><span data-stu-id="26af4-144">The samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="26af4-145">1. Interfaces en onderliggende interfaces configureren</span><span class="sxs-lookup"><span data-stu-id="26af4-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="26af4-146">**Dot1Q interfacedefinitie**</span><span class="sxs-lookup"><span data-stu-id="26af4-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="26af4-147">In dit voorbeeld worden de onderliggende interfacedefinitie voor een onderliggende interface met een enkel VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="26af4-147">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="26af4-148">De VLAN-ID is uniek per peering.</span><span class="sxs-lookup"><span data-stu-id="26af4-148">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="26af4-149">Het laatste octet van uw IPv4-adres wordt altijd een oneven getal zijn.</span><span class="sxs-lookup"><span data-stu-id="26af4-149">The last octet of your IPv4 address will always be an odd number.</span></span>

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


<span data-ttu-id="26af4-150">**QinQ interfacedefinitie**</span><span class="sxs-lookup"><span data-stu-id="26af4-150">**QinQ interface definition**</span></span>

<span data-ttu-id="26af4-151">Dit voorbeeld bevat de submappen interfacedefinitie voor een onderliggende interface met twee VLAN-id.</span><span class="sxs-lookup"><span data-stu-id="26af4-151">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="26af4-152">De buitenste VLAN-ID (s-code), als het gebruikt hetzelfde is gebleven via de peerings.</span><span class="sxs-lookup"><span data-stu-id="26af4-152">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="26af4-153">De interne (c-code) van de VLAN-ID is uniek per peering.</span><span class="sxs-lookup"><span data-stu-id="26af4-153">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="26af4-154">Het laatste octet van uw IPv4-adres wordt altijd een oneven getal zijn.</span><span class="sxs-lookup"><span data-stu-id="26af4-154">The last octet of your IPv4 address will always be an odd number.</span></span>

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

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="26af4-155">2. Instellen van eBGP-sessies</span><span class="sxs-lookup"><span data-stu-id="26af4-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="26af4-156">U moet een BGP-sessie met Microsoft voor elke peering instellen.</span><span class="sxs-lookup"><span data-stu-id="26af4-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="26af4-157">Het onderstaande voorbeeld kunt u instellen dat een BGP-sessie met Microsoft.</span><span class="sxs-lookup"><span data-stu-id="26af4-157">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="26af4-158">Als het IPv4-adres dat u voor uw sub-interface gebruikt a.b.c.d is, worden de IP-adres van de BGP-neighbor (Microsoft) a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="26af4-158">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="26af4-159">Het laatste octet van de BGP-neighbor IPv4-adres wordt altijd een even getal zijn.</span><span class="sxs-lookup"><span data-stu-id="26af4-159">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

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

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="26af4-160">3. Voorvoegsels instellen om te worden geadverteerd via de BGP-sessie</span><span class="sxs-lookup"><span data-stu-id="26af4-160">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="26af4-161">U kunt uw router voor het adverteren Selecteer voorvoegsels naar Microsoft configureren.</span><span class="sxs-lookup"><span data-stu-id="26af4-161">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="26af4-162">U kunt dit doen met behulp van het voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="26af4-162">You can do so using the sample below.</span></span>

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


### <a name="4-route-maps"></a><span data-ttu-id="26af4-163">4. Route maps</span><span class="sxs-lookup"><span data-stu-id="26af4-163">4. Route maps</span></span>
<span data-ttu-id="26af4-164">U kunt gebruiken route-kaarten en voorvoegsel lijsten moeten filter voorvoegsels doorgegeven in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="26af4-164">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="26af4-165">Het onderstaande voorbeeld kunt u de taak uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="26af4-165">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="26af4-166">Zorg ervoor dat er bijbehorende voorvoegsel een lijst met setup.</span><span class="sxs-lookup"><span data-stu-id="26af4-166">Ensure that you have appropriate prefix lists setup.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="26af4-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="26af4-167">Next Steps</span></span>
<span data-ttu-id="26af4-168">Zie de [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="26af4-168">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

