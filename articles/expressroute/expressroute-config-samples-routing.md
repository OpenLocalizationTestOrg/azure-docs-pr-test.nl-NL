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
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a><span data-ttu-id="0c98e-103">Configuratie van de router tooset voorbeelden van en beheren van Routering</span><span class="sxs-lookup"><span data-stu-id="0c98e-103">Router configuration samples tooset up and manage routing</span></span>
<span data-ttu-id="0c98e-104">Deze pagina bevat de interface en routering configuratie voorbeelden voor IOS-XE van Cisco en Juniper MX reeks routers.</span><span class="sxs-lookup"><span data-stu-id="0c98e-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="0c98e-105">Deze voorbeelden van de beoogde toobe voor alleen richtlijnen zijn en mogen niet worden gebruikt omdat de.</span><span class="sxs-lookup"><span data-stu-id="0c98e-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="0c98e-106">U kunt werken met uw leverancier toocome up met relevante configuraties voor uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="0c98e-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0c98e-107">Voorbeelden in deze pagina zijn beoogde toobe puur voor hulp.</span><span class="sxs-lookup"><span data-stu-id="0c98e-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="0c98e-108">Bespreek met de leverancier van uw verkoop / technisch team en uw netwerken team toocome up met relevante configuraties toomeet uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="0c98e-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="0c98e-109">Microsoft ondersteunt geen problemen die worden vermeld in deze pagina tooconfigurations gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="0c98e-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="0c98e-110">Neem contact op met de leverancier van uw apparaat voor ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="0c98e-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="0c98e-111">MTU en TCP MSS-instellingen op de interfaces van router</span><span class="sxs-lookup"><span data-stu-id="0c98e-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="0c98e-112">Hallo MTU voor Hallo ExpressRoute-interface is 1500, Hallo typische standaard MTU voor een Ethernet-interface op een router.</span><span class="sxs-lookup"><span data-stu-id="0c98e-112">hello MTU for hello ExpressRoute interface is 1500, which is hello typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="0c98e-113">Tenzij uw router een andere MTU standaard heeft, is er geen toospecify moet een waarde op Hallo-routerinterface.</span><span class="sxs-lookup"><span data-stu-id="0c98e-113">Unless your router has a different MTU by default, there is no need toospecify a value on hello router interface.</span></span>
* <span data-ttu-id="0c98e-114">In tegenstelling tot een Azure VPN-Gateway hoeft Hallo TCP MSS voor een ExpressRoute-circuit niet toobe opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0c98e-114">Unlike an Azure VPN Gateway, hello TCP MSS for an ExpressRoute circuit does not need toobe specified.</span></span>

<span data-ttu-id="0c98e-115">Router configuratie voorbeelden hieronder tooall peerings van toepassing.</span><span class="sxs-lookup"><span data-stu-id="0c98e-115">Router configuration samples below apply tooall peerings.</span></span> <span data-ttu-id="0c98e-116">Bekijk [ExpressRoute peerings](expressroute-circuit-peerings.md) en [routeringsvereisten voor ExpressRoute](expressroute-routing.md) voor meer informatie over routering.</span><span class="sxs-lookup"><span data-stu-id="0c98e-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="0c98e-117">Cisco IOS-XE gebaseerd routers</span><span class="sxs-lookup"><span data-stu-id="0c98e-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="0c98e-118">Hallo-voorbeelden in deze sectie zijn van toepassing voor een IOS-XE-OS-familie van Hallo-router.</span><span class="sxs-lookup"><span data-stu-id="0c98e-118">hello samples in this section apply for any router running hello IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="0c98e-119">1. Interfaces en onderliggende interfaces configureren</span><span class="sxs-lookup"><span data-stu-id="0c98e-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="0c98e-120">U moet een sub-interface per peering in elke router verbinding tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="0c98e-120">You will require a sub interface per peering in every router you connect tooMicrosoft.</span></span> <span data-ttu-id="0c98e-121">Een sub-interface kan worden geïdentificeerd met een VLAN-ID of een gestapelde paar VLAN-id's en een IP-adres.</span><span class="sxs-lookup"><span data-stu-id="0c98e-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="0c98e-122">**Dot1Q interfacedefinitie**</span><span class="sxs-lookup"><span data-stu-id="0c98e-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="0c98e-123">Dit voorbeeld bevat Hallo onderliggende interfacedefinitie voor een onderliggende interface met een enkel VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="0c98e-123">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="0c98e-124">Hallo VLAN-ID is uniek per peering.</span><span class="sxs-lookup"><span data-stu-id="0c98e-124">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="0c98e-125">laatste octet Hallo van uw IPv4-adres wordt altijd een oneven getal zijn.</span><span class="sxs-lookup"><span data-stu-id="0c98e-125">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="0c98e-126">**QinQ interfacedefinitie**</span><span class="sxs-lookup"><span data-stu-id="0c98e-126">**QinQ interface definition**</span></span>

<span data-ttu-id="0c98e-127">Dit voorbeeld bevat Hallo onderliggende interfacedefinitie voor een onderliggende interface met twee VLAN-id.</span><span class="sxs-lookup"><span data-stu-id="0c98e-127">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="0c98e-128">Hallo buitenste VLAN-ID (s-code), als gebruikt blijft Hallo dezelfde over alle Hallo-peerings.</span><span class="sxs-lookup"><span data-stu-id="0c98e-128">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="0c98e-129">Hallo interne (c-code) van de VLAN-ID is uniek per peering.</span><span class="sxs-lookup"><span data-stu-id="0c98e-129">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="0c98e-130">laatste octet Hallo van uw IPv4-adres wordt altijd een oneven getal zijn.</span><span class="sxs-lookup"><span data-stu-id="0c98e-130">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="0c98e-131">2. Instellen van eBGP-sessies</span><span class="sxs-lookup"><span data-stu-id="0c98e-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="0c98e-132">U moet een BGP-sessie met Microsoft voor elke peering instellen.</span><span class="sxs-lookup"><span data-stu-id="0c98e-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="0c98e-133">Hallo onderstaand voorbeeld kunt u toosetup een BGP-sessie met Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0c98e-133">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="0c98e-134">Als Hallo IPv4-adres die u hebt gebruikt voor de sub-interface a.b.c.d, zich Hallo IP-adres van Hallo BGP neighbor (Microsoft) a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="0c98e-134">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="0c98e-135">de laatste octet Hallo van Hallo BGP neighbor IPv4-adres wordt altijd een even getal zijn.</span><span class="sxs-lookup"><span data-stu-id="0c98e-135">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="0c98e-136">3. Instellen van voorvoegsels toobe geadverteerd via Hallo BGP-sessie</span><span class="sxs-lookup"><span data-stu-id="0c98e-136">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="0c98e-137">U kunt uw router tooadvertise Selecteer voorvoegsels tooMicrosoft configureren.</span><span class="sxs-lookup"><span data-stu-id="0c98e-137">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="0c98e-138">U kunt doen met behulp van Hallo onderstaand voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0c98e-138">You can do so using hello sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="0c98e-139">4. Route maps</span><span class="sxs-lookup"><span data-stu-id="0c98e-139">4. Route maps</span></span>
<span data-ttu-id="0c98e-140">Kunt u route-kaarten en voorvoegsel vermeldt toofilter voorvoegsels doorgegeven in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="0c98e-140">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="0c98e-141">U kunt Hallo voorbeeld hieronder tooaccomplish Hallo taak gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0c98e-141">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="0c98e-142">Zorg ervoor dat er bijbehorende voorvoegsel een lijst met setup.</span><span class="sxs-lookup"><span data-stu-id="0c98e-142">Ensure that you have appropriate prefix lists setup.</span></span>

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


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="0c98e-143">Juniper MX reeks routers</span><span class="sxs-lookup"><span data-stu-id="0c98e-143">Juniper MX series routers</span></span>
<span data-ttu-id="0c98e-144">Hallo-voorbeelden in deze sectie gelden voor alle reeksen Juniper MX routers.</span><span class="sxs-lookup"><span data-stu-id="0c98e-144">hello samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="0c98e-145">1. Interfaces en onderliggende interfaces configureren</span><span class="sxs-lookup"><span data-stu-id="0c98e-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="0c98e-146">**Dot1Q interfacedefinitie**</span><span class="sxs-lookup"><span data-stu-id="0c98e-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="0c98e-147">Dit voorbeeld bevat Hallo onderliggende interfacedefinitie voor een onderliggende interface met een enkel VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="0c98e-147">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="0c98e-148">Hallo VLAN-ID is uniek per peering.</span><span class="sxs-lookup"><span data-stu-id="0c98e-148">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="0c98e-149">laatste octet Hallo van uw IPv4-adres wordt altijd een oneven getal zijn.</span><span class="sxs-lookup"><span data-stu-id="0c98e-149">hello last octet of your IPv4 address will always be an odd number.</span></span>

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


<span data-ttu-id="0c98e-150">**QinQ interfacedefinitie**</span><span class="sxs-lookup"><span data-stu-id="0c98e-150">**QinQ interface definition**</span></span>

<span data-ttu-id="0c98e-151">Dit voorbeeld bevat Hallo onderliggende interfacedefinitie voor een onderliggende interface met twee VLAN-id.</span><span class="sxs-lookup"><span data-stu-id="0c98e-151">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="0c98e-152">Hallo buitenste VLAN-ID (s-code), als gebruikt blijft Hallo dezelfde over alle Hallo-peerings.</span><span class="sxs-lookup"><span data-stu-id="0c98e-152">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="0c98e-153">Hallo interne (c-code) van de VLAN-ID is uniek per peering.</span><span class="sxs-lookup"><span data-stu-id="0c98e-153">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="0c98e-154">laatste octet Hallo van uw IPv4-adres wordt altijd een oneven getal zijn.</span><span class="sxs-lookup"><span data-stu-id="0c98e-154">hello last octet of your IPv4 address will always be an odd number.</span></span>

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

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="0c98e-155">2. Instellen van eBGP-sessies</span><span class="sxs-lookup"><span data-stu-id="0c98e-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="0c98e-156">U moet een BGP-sessie met Microsoft voor elke peering instellen.</span><span class="sxs-lookup"><span data-stu-id="0c98e-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="0c98e-157">Hallo onderstaand voorbeeld kunt u toosetup een BGP-sessie met Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0c98e-157">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="0c98e-158">Als Hallo IPv4-adres die u hebt gebruikt voor de sub-interface a.b.c.d, zich Hallo IP-adres van Hallo BGP neighbor (Microsoft) a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="0c98e-158">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="0c98e-159">de laatste octet Hallo van Hallo BGP neighbor IPv4-adres wordt altijd een even getal zijn.</span><span class="sxs-lookup"><span data-stu-id="0c98e-159">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

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

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="0c98e-160">3. Instellen van voorvoegsels toobe geadverteerd via Hallo BGP-sessie</span><span class="sxs-lookup"><span data-stu-id="0c98e-160">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="0c98e-161">U kunt uw router tooadvertise Selecteer voorvoegsels tooMicrosoft configureren.</span><span class="sxs-lookup"><span data-stu-id="0c98e-161">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="0c98e-162">U kunt doen met behulp van Hallo onderstaand voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0c98e-162">You can do so using hello sample below.</span></span>

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


### <a name="4-route-maps"></a><span data-ttu-id="0c98e-163">4. Route maps</span><span class="sxs-lookup"><span data-stu-id="0c98e-163">4. Route maps</span></span>
<span data-ttu-id="0c98e-164">Kunt u route-kaarten en voorvoegsel vermeldt toofilter voorvoegsels doorgegeven in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="0c98e-164">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="0c98e-165">U kunt Hallo voorbeeld hieronder tooaccomplish Hallo taak gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0c98e-165">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="0c98e-166">Zorg ervoor dat er bijbehorende voorvoegsel een lijst met setup.</span><span class="sxs-lookup"><span data-stu-id="0c98e-166">Ensure that you have appropriate prefix lists setup.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0c98e-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0c98e-167">Next Steps</span></span>
<span data-ttu-id="0c98e-168">Zie Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0c98e-168">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

