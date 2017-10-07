---
title: configuratie van aaaSample - Cisco ASA apparaat tooAzure VPN-gateways verbinden | Microsoft Docs
description: Dit artikel bevat een voorbeeldconfiguratie voor Cisco ASA apparaat tooAzure VPN-gateways verbinden.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a>Voorbeeldconfiguratie: Cisco ASA apparaat (BGP IKEv2/Nee)
Dit artikel vindt voorbeelden van configuraties voor Cisco ASA apparaten tooAzure VPN-gateways verbinden.

## <a name="device-at-a-glance"></a>Apparaat in een oogopslag

|                        |                                   |
| ---                    | ---                               |
| De leverancier van apparaat          | Cisco                             |
| Apparaatmodel           | ASA (adaptieve beveiliging toestel) |
| Doelversie         | 8.4+                              |
| Geteste model           | 5505 ASA                          |
| Geteste versie         | 9.2                               |
| IKE-versie            | **IKEv2**                         |
| BGP                    | **Nee**                            |
| Azure VPN-gateway-type | **Op route gebaseerde** VPN-gateway       |
|                        |                                   |

> [!NOTE]
> 1. Hallo configuratie hieronder verbindt een Cisco ASA apparaat tooan Azure **op route gebaseerde** VPN-gateway met behulp van aangepaste IPsec/IKE-beleid met de optie 'UserPolicyBasedTrafficSelectors', zoals beschreven in [in dit artikel](vpn-gateway-connect-multiple-policybased-rm-ps.md).
> 2. Hiervoor ASA apparaten toouse **IKEv2** met configuraties toegang lijst is gebaseerd op VTI basis niet.
> 3. Neem contact op met uw VPN-apparaat Leverancierspecificaties tooensure Hallo beleid op uw on-premises VPN-apparaten wordt ondersteund.

## <a name="vpn-device-requirements"></a>Vereisten voor VPN-apparaten
Azure VPN-gateways gebruiken standaard IPsec/IKE-protocol suites tooestablish S2S VPN-tunnels. Raadpleeg te[over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor Hallo gedetailleerde parameters voor IPsec/IKE-protocol en standaard cryptografische algoritmen voor Azure VPN-gateways. U kunt optioneel Hallo exact dezelfde combinatie van cryptografische algoritmen en de belangrijkste sterkte voor een specifieke verbinding opgeven zoals beschreven in [over de vereisten voor cryptografische](vpn-gateway-about-compliance-crypto.md). Als u een specifieke combinatie van cryptografische algoritmen en de belangrijkste sterkte selecteert, Controleer of dat u de overeenkomstige specificaties hello gebruiken op uw VPN-apparaten.

## <a name="single-vpn-tunnel"></a>Één VPN-tunnel
Deze topologie bestaat uit één S2S-VPN-tunnel tussen een Azure VPN-gateway en uw on-premises VPN-apparaat. Desgewenst kunt u BGP configureren op Hallo VPN-tunnel.

![één tunnel](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

Raadpleeg te[één tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) voor gedetailleerde, stapsgewijze instructies toobuild hello Azure configuraties.

### <a name="network-and-vpn-gateway-information"></a>Gegevens voor netwerk- en VPN-gateway
In deze sectie lijst Hallo parameters voor Hallo van dit voorbeeld.

| **Parameter**                | **Waarde**                    |
| ---                          | ---                          |
| VNet-adresvoorvoegsels        | 10.11.0.0/16<br>10.12.0.0/16 |
| Azure VPN-gateway-IP         | Azure_Gateway_Public_IP      |
| Lokale adresvoorvoegsels | 10.51.0.0/16<br>10.52.0.0/16 |
| Lokale VPN-apparaat IP    | OnPrem_Device_Public_IP     |
| * VNet BGP ASN                | 65010                        |
| * Azure BGP-peer-IP           | 10.12.255.30                 |
| * On-premises BGP ASN         | 65050                        |
| * On-premises BGP-peer-IP     | 10.52.255.254                |
|                              |                              |

* (*) Optionele parameters voor BGP alleen.

### <a name="ipsecike-policy--parameters"></a>Beleid voor IPsec/IKE & parameters

Hallo in de volgende tabel geeft een lijst Hallo IPsec/IKE-algoritmen en parameters die in de steekproef hello worden gebruikt. Neem contact op met uw VPN-apparaat specificaties toomake-ervoor dat alle hierboven vermelde-algoritmen worden ondersteund door uw VPN-apparaatmodellen en firmware-versies.

| **IPsec/IKEv2**  | **Waarde**                            |
| ---              | ---                                  |
| IKEv2-versleuteling | AES256                               |
| IKEv2-integriteit  | SHA384                               |
| DH-groep         | DHGroup24                            |
| IPsec-versleuteling | AES256                               |
| IPsec-integriteit  | SHA1                                 |
| PFS-groep        | PFS24                                |
| QM SA-levensduur   | 7200 seconden                         |
| Verkeersselector | UsePolicyBasedTrafficSelectors $True |
| Vooraf gedeelde sleutel   | PreSharedKey                         |
|                  |                                      |

- (*) Op sommige apparaten moet IPSec-integriteit 'null' als GCM-AES wordt gebruikt als de IPsec-versleutelingsalgoritme.

### <a name="device-notes"></a>Opmerkingen bij de apparaten

>[!NOTE]
>
> 1. IKEv2-ondersteuning vereist ASA versie 8.4 en hoger.
> 2. Ondersteuning voor hogere DH en PFS (anders dan de groep 5) is de ASA-versie vereist 9.x.
> 3. IPSec-codering met AES-GCM en IPSec-integriteit met SHA-256, SHA-384 en SHA-512 ondersteuning vereist ASA versie 9.x op nieuwere ASA hardware; 5505 ASA, 5510, 5520, 5540, 5550, 5580 zijn **niet** ondersteund. (Controleer Hallo leverancier specificaties tooconfirm.)
>


### <a name="sample-device-configurations"></a>Voorbeeld apparaatconfiguraties
Hallo script hieronder biedt een voorbeeldconfiguratie op basis van het Hallo-topologie en parameters die hierboven worden genoemd. Hallo S2S VPN-tunnelconfiguratie bestaat uit Hallo volgende onderdelen:

1. Interfaces & routes
2. Een lijst met toegang
3. IKE-beleid en de parameters (fase 1 of hoofdmodus)
4. IPSec-beleid en de parameters (fase 2 of snelle modus)
5. Andere parameters (TCP MSS clamping, enz.)

>[!IMPORTANT] 
>Controleer of u Hallo aanvullende configuratie hieronder vermelde voltooien en vervang Hallo tijdelijke aanduidingen door de werkelijke waarden Hallo:
> 
> - Configuratie voor zowel binnen als buiten interfaces interface
> - Routes voor uw binnen en persoonlijke en buiten/openbare netwerken
> - Zorg ervoor dat alle namen en getallen beleid zijn uniek op Hallo-apparaat
> - Zorg ervoor dat Hallo cryptografische algoritmen worden ondersteund op uw apparaat
> - Na de houders plaats door de werkelijke waarden Hallo Hallo vervangen
>   - Buiten Interfacenaam: 'externe'
>   - Azure_Gateway_Public_IP
>   - OnPrem_Device_Public_IP
>   - IKE-Pre_Shared_Key
>   - VNet en lokale gateway netwerknamen (VNetName, LNGName)
>   - VNet- en on-premises netwerk adresvoorvoegsels
>   - Juiste netmaskers

#### <a name="sample-configuration"></a>Voorbeeldconfiguratie

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a>Eenvoudige foutopsporing opdrachten

Hier volgen enkele ASA-opdrachten voor foutopsporing:

1. Weergeven Hallo IPsec en IKE-SA
    - ' weergeven crypto ipsec sa '
    - ' weergeven crypto ikev2 sa '
2. Invoeren foutopsporingsmodus - dit zeer veel ruis veroorzaken kunt krijgen op Hallo-console
    - ' debug crypto ikev2 platform <level>'
    - ' debug crypto ikev2 protocol <level>'
3. Lijst met huidige configuraties
    - 'Voer show' - toont Hallo huidige configuraties op Hallo apparaat; u kunt verschillende onderliggende opdrachten toolist specifieke onderdelen van de configuratie Hallo Hallo. Bijvoorbeeld 'crypto-presentatie', 'weergeven die worden uitgevoerd toegang-list', 'uitvoeren tunnel-groep weergeven', enzovoort.


## <a name="next-steps"></a>Volgende stappen
Zie [actieve VPN-Gateways voor Cross-Premises en VNet-naar-VNet-verbindingen configureren](vpn-gateway-activeactive-rm-powershell.md) voor stappen tooconfigure actieve cross-premises en VNet-naar-VNet-verbindingen.

