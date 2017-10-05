---
title: Voorbeeldconfiguratie - Cisco ASA apparaat verbinding te maken met Azure VPN-gateways | Microsoft Docs
description: Dit artikel bevat een voorbeeldconfiguratie voor Cisco ASA apparaat verbinding te maken met Azure VPN-gateways.
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
ms.openlocfilehash: 10466b8928e2cd687f7961a2956b6d60823b82be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a>Voorbeeldconfiguratie: Cisco ASA apparaat (BGP IKEv2/Nee)
Dit artikel vindt voorbeelden van configuraties voor Cisco ASA-apparaten die verbinding maken met Azure VPN-gateways.

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
> 1. De onderstaande configuratie een Cisco ASA-apparaat verbindt met een Azure **op route gebaseerde** VPN-gateway met behulp van aangepaste IPsec/IKE-beleid met de optie 'UserPolicyBasedTrafficSelectors', zoals beschreven in [in dit artikel](vpn-gateway-connect-multiple-policybased-rm-ps.md).
> 2. Hiervoor ASA-apparaten **IKEv2** met configuraties toegang lijst is gebaseerd op VTI basis niet.
> 3. Neem contact op met de VPN-leverancier apparaatspecificaties om te controleren of dat het beleid wordt ondersteund op uw on-premises VPN-apparaten.

## <a name="vpn-device-requirements"></a>Vereisten voor VPN-apparaten
Azure VPN-gateways gebruiken standaard IPsec/IKE-protocol suites voor S2S-VPN-tunnels tot stand brengen. Raadpleeg [over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor de parameters van gedetailleerde IPsec/IKE-protocol en de standaard cryptografische algoritmen voor Azure VPN-gateways. U kunt optioneel de exacte combinatie van cryptografische algoritmen en de belangrijkste sterkte voor een specifieke verbinding opgeven zoals beschreven in [over de vereisten voor cryptografische](vpn-gateway-about-compliance-crypto.md). Als u een specifieke combinatie van cryptografische algoritmen en de belangrijkste sterkte selecteert, Controleer of dat u de overeenkomstige specificaties gebruiken op uw VPN-apparaten.

## <a name="single-vpn-tunnel"></a>Één VPN-tunnel
Deze topologie bestaat uit één S2S-VPN-tunnel tussen een Azure VPN-gateway en uw on-premises VPN-apparaat. U kunt desgewenst BGP configureren via de VPN-tunnel.

![één tunnel](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

Raadpleeg [één tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) voor gedetailleerde, stapsgewijze instructies voor het bouwen van de Azure-configuraties.

### <a name="network-and-vpn-gateway-information"></a>Gegevens voor netwerk- en VPN-gateway
Deze sectie lijst met de parameters voor dit voorbeeld.

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

De volgende tabel bevat de IPsec/IKE-algoritmen en parameters die worden gebruikt in het voorbeeld. Neem contact op met uw VPN-apparaatspecificaties om ervoor te zorgen dat alle hierboven vermelde-algoritmen worden ondersteund door uw VPN-apparaatmodellen en firmware-versies.

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
> 3. IPSec-codering met AES-GCM en IPSec-integriteit met SHA-256, SHA-384 en SHA-512 ondersteuning vereist ASA versie 9.x op nieuwere ASA hardware; 5505 ASA, 5510, 5520, 5540, 5550, 5580 zijn **niet** ondersteund. (Controleer of de Leverancierspecificaties om te bevestigen.)
>


### <a name="sample-device-configurations"></a>Voorbeeld apparaatconfiguraties
Het onderstaande script geeft een voorbeeldconfiguratie op basis van de topologie en de hierboven vermelde parameters. De configuratie van de S2S VPN-tunnel bestaat uit de volgende onderdelen:

1. Interfaces & routes
2. Een lijst met toegang
3. IKE-beleid en de parameters (fase 1 of hoofdmodus)
4. IPSec-beleid en de parameters (fase 2 of snelle modus)
5. Andere parameters (TCP MSS clamping, enz.)

>[!IMPORTANT] 
>Controleer of u de aanvullende configuratie hieronder vermelde voltooien en vervang de tijdelijke aanduidingen door de werkelijke waarden:
> 
> - Configuratie voor zowel binnen als buiten interfaces interface
> - Routes voor uw binnen en persoonlijke en buiten/openbare netwerken
> - Zorg ervoor dat alle namen en getallen beleid zijn uniek op het apparaat
> - Zorg ervoor dat de cryptografische algoritmen worden ondersteund op uw apparaat
> - De volgende plaats houders vervangen door de werkelijke waarden
>   - Buiten Interfacenaam: 'externe'
>   - Azure_Gateway_Public_IP
>   - OnPrem_Device_Public_IP
>   - IKE-Pre_Shared_Key
>   - VNet en lokale gateway netwerknamen (VNetName, LNGName)
>   - VNet- en on-premises netwerk adresvoorvoegsels
>   - Juiste netmaskers

#### <a name="sample-configuration"></a>Voorbeeldconfiguratie

```
! Sample ASA configuration for connecting to Azure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace the following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - the Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with the actual nexthop IP address
!
! (*) Must be unique names in the device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on the outside interface or vlan
!     > <PrivateIPAddress> on the inside interface or vlan; e.g., 10.51.0.1/24
!     > Route to connect to <Azure_Gateway_Public_IP> address
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
!       (1) Allow S2S VPN tunnels between the ASA and the Azure gateway public IP address
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
!     > Object group that corresponding to the <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines the on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify the access-list between the Azure VNet and your on-premises network.
!       This access list defines the IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between the on-premises network and Azure VNet
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
!       - Make sure the policy number is not used
!       - integrity and prf must be the same
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
!       - This sample uses "Azure-<VNetName>-map" as the crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned to your outside interface, you must use
!         the same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses the access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses the proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS to 1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a>Eenvoudige foutopsporing opdrachten

Hier volgen enkele ASA-opdrachten voor foutopsporing:

1. IPsec en IKE-SA weergeven
    - ' weergeven crypto ipsec sa '
    - ' weergeven crypto ikev2 sa '
2. Invoeren foutopsporingsmodus - dit zeer veel ruis veroorzaken kunt krijgen op de console
    - ' debug crypto ikev2 platform <level>'
    - ' debug crypto ikev2 protocol <level>'
3. Lijst met huidige configuraties
    - 'show uitvoeren' - ziet u de huidige configuraties op het apparaat. u kunt de verschillende onderliggende opdrachten voor het specifieke onderdelen van de lijst van de configuratie. Bijvoorbeeld 'crypto-presentatie', 'weergeven die worden uitgevoerd toegang-list', 'uitvoeren tunnel-groep weergeven', enzovoort.


## <a name="next-steps"></a>Volgende stappen
Zie [Actief/actief VPN-gateways configureren voor cross-premises en VNet-naar-VNet-verbindingen](vpn-gateway-activeactive-rm-powershell.md) voor de stappen om actief/actief on-premises en VNet-naar-VNet-verbindingen te configureren.

