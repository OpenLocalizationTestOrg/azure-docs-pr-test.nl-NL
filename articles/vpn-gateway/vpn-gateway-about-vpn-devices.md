---
title: Over VPN-apparaten voor cross-premises Azure-verbindingen | Microsoft Docs
description: Dit artikel gaat over VPN-apparaten en IPSec-parameters voor cross-premises site-naar-site-VPN-gateway-verbindingen. Het artikel bevat koppelingen naar configuratie-instructies en voorbeelden.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: ba449333-2716-4b7f-9889-ecc521e4d616
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: yushwang;cherylmc
ms.openlocfilehash: 7b7e5f0f089cc87c9e63eee1fd3d29b7a2c0d49f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/11/2017
---
# <a name="about-vpn-devices-and-ipsecike-parameters-for-site-to-site-vpn-gateway-connections"></a>VPN-apparaten en IPSec-/IKE-parameters voor site-naar-site-VPN-gateway-verbindingen

U hebt een VPN-apparaat nodig om een cross-premises site-naar-site-VPN-verbinding te configureren. Site-naar-site-verbindingen kunnen worden gebruikt om een hybride oplossing te maken of wanneer u beveiligde verbindingen wilt maken tussen uw on-premises netwerken en virtuele netwerken. Dit artikel bevat een lijst met gevalideerde VPN-apparaten en een lijst met IPSec-/IKE-parameters voor VPN-gateways.

> [!IMPORTANT]
> Raadpleeg [Bekende compatibiliteitsproblemen](#known) als u problemen ondervindt met de connectiviteit tussen uw lokale VPN-apparaten en VPN-gateways.
>

### <a name="items-to-note-when-viewing-the-tables"></a>Waar u op moet letten wanneer u de tabellen bekijkt:

* Er is een terminologiewijziging voor Azure VPN-gateways. Alleen de namen zijn gewijzigd. Er is geen wijziging in de functionaliteit.
  * Statische routering = PolicyBased
  * Dynamische routering = RouteBased
* De specificaties voor een HighPerformance-VPN-gateway en een RouteBased VPN-gateway zijn hetzelfde, tenzij anders wordt vermeld. Zo zijn de gevalideerde VPN-apparaten die compatibel zijn met RouteBased VPN-gateways, ook compatibel met de HighPerformance VPN-gateway.

## <a name="devicetable"></a>Gevalideerde VPN-apparaten en apparaatconfiguratiehandleidingen

> [!NOTE]
> Wanneer u een S2S-verbinding configureert, hebt u een openbaar IPv4-adres voor het VPN-apparaat nodig.
>

We hebben samen met apparaatleveranciers een reeks standaard VPN-apparaten gevalideerd. Alle apparaten in de apparaatfamilies in de volgende lijst kunnen met VPN-gateways worden gebruikt. Zie [Over VPN-gatewayinstellingen](vpn-gateway-about-vpn-gateway-settings.md#vpntype) voor informatie over welk VPN-type u moet gebruiken (PolicyBased of RouteBased) voor de VPN-gatewayoplossing die u wilt configureren.

Voor hulp bij de configuratie van uw VPN-apparaat, raadpleegt u de koppelingen die overeenkomen met de betreffende apparaatstuurprogrammafamilie. De koppelingen naar configuratie-instructies worden naar beste vermogen geleverd. Voor ondersteuning van VPN-apparaten neemt u contact op met de fabrikant van uw apparaat.

|**Leverancier**          |**Apparaatfamilie**     |**Minimale versie van het besturingssysteem** |**PolicyBased configuratie-instructies** |**RouteBased configuratie-instructies** |
| ---                | ---                  | ---                   | ---            | ---           |
| A10 Networks, Inc. |Thunder CFW           |ACOS 4.1.1             |Niet compatibel  |[Configuratiehandleiding](https://www.a10networks.com/resources/deployment-guides/a10-thunder-cfw-ipsec-vpn-interoperability-azure-vpn-gateways)|
| Allied Telesis     |VPN-routers uit AR-serie |2.9.2                  |Binnenkort beschikbaar     |Niet compatibel  |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall F-serie |PolicyBased: 5.4.3<br>RouteBased: 6.2.0 |[Configuratiehandleiding](https://techlib.barracuda.com/NGF/AzurePolicyBasedVPNGW) |[Configuratiehandleiding](https://techlib.barracuda.com/NGF/AzureRouteBasedVPNGW) |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall X-serie |Barracuda Firewall 6.5 |[Configuratiehandleiding](https://techlib.barracuda.com/BFW/ConfigAzureVPNGateway) |Niet compatibel |
| Brocade            |Vyatta 5400 vRouter   |Virtual Router 6.6R3 GA|[Configuratiehandleiding](http://www1.brocade.com/downloads/documents/html_product_manuals/vyatta/vyatta_5400_manual/wwhelp/wwhimpl/js/html/wwhelp.htm#href=VPN_Site-to-Site%20IPsec%20VPN/Preface.1.1.html) |Niet compatibel |
| Check Point |Security Gateway |R77.30 |[Configuratiehandleiding](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |[Configuratiehandleiding](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |
| Cisco              |ASA       |8.3<br>8.4+ (IKEv2*) |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA) |[Configuratiehandleiding*](vpn-gateway-3rdparty-device-config-cisco-asa.md) |
| Cisco |ASR |PolicyBased: IOS 15.1<br>RouteBased: IOS 15.2 |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |
| Cisco |ISR |PolicyBased: IOS 15.0<br>RouteBased*: IOS 15.1 |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |[Voorbeelden van configuraties**](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |
| Citrix |NetScaler MPX, SDX, VPX |10.1 en hoger |[Configuratiehandleiding](https://docs.citrix.com/en-us/netscaler/11-1/system/cloudbridge-connector-introduction/cloudbridge-connector-azure.html) |Niet compatibel |
| F5 |BIG-IP-serie |12.0 |[Configuratiehandleiding](https://devcentral.f5.com/articles/connecting-to-windows-azure-with-the-big-ip) |[Configuratiehandleiding](https://devcentral.f5.com/articles/big-ip-to-azure-dynamic-ipsec-tunneling) |
| Fortinet |FortiGate |FortiOS 5.4.2 |  |[Configuratiehandleiding](http://cookbook.fortinet.com/ipsec-vpn-microsoft-azure-54) |
| Internet Initiative Japan (IIJ) |SEIL-serie |SEIL/X 4.60<br>SEIL/B1 4.60<br>SEIL/x86 3.20 |[Configuratiehandleiding](http://www.iij.ad.jp/biz/seil/ConfigAzureSEILVPN.pdf) |Niet compatibel |
| Juniper |SRX |PolicyBased: JunOS 10.2<br>Routebased: JunOS 11.4 |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |
| Juniper |J-serie |PolicyBased: JunOS 10.4r9<br>RouteBased: JunOS 11.4 |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |
| Juniper |ISG |ScreenOS 6.3 |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |
| Juniper |SSG |ScreenOS 6.2 |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |
| Microsoft |Routering en Remote Access-Service |Windows Server 2012 |Niet compatibel |[Voorbeelden van configuraties](http://go.microsoft.com/fwlink/p/?LinkId=717761) |
| Open Systems AG |Mission Control Security Gateway |N.v.t. |[Configuratiehandleiding](https://www.open.ch/_pdf/Azure/AzureVPNSetup_Installation_Guide.pdf) |Niet compatibel |
| Palo Alto Networks |Alle apparaten waarop PAN-OS wordt uitgevoerd |PAN-OS<br>PolicyBased: 6.1.5 of hoger<br>RouteBased: 7.1.4 |[Configuratiehandleiding](https://live.paloaltonetworks.com/t5/Configuration-Articles/How-to-Configure-VPN-Tunnel-Between-a-Palo-Alto-Networks/ta-p/59065) |[Configuratiehandleiding](https://live.paloaltonetworks.com/t5/Integration-Articles/Configuring-IKEv2-VPN-for-Microsoft-Azure-Environment/ta-p/60340) |
| SonicWall |TZ-serie, NSA-serie<br>SuperMassive-serie<br>E-Class NSA-serie |SonicOS 5.8.x<br>SonicOS 5.9.x<br>SonicOS 6.x |Niet ondersteund|[Configuratiehandleiding](https://www.sonicwall.com/en-us/support/knowledge-base/170505320011694) |
| WatchGuard |Alle |Fireware XTM<br> PolicyBased: v11.11.x<br>RouteBased: v11.12.x |[Configuratiehandleiding](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA2F00000000LI7KAM&lang=en_US) |[Configuratiehandleiding](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA22A000000XZogSAG&lang=en_US)|

> [!NOTE]
>
> (*) Met Cisco ASA versie 8.4 en hoger wordt IKEv2-ondersteuning toegevoegd en kan verbinding worden gemaakt met Azure VPN-gateways met behulp van een aangepast IPsec/IKE-beleid met de optie UsePolicyBasedTrafficSelectors. Raadpleeg dit [artikel met instructies](vpn-gateway-connect-multiple-policybased-rm-ps.md).
>
> (**) Routers uit de ISR 7200-serie bieden alleen ondersteuning voor PolicyBased VPN's.

## <a name="additionaldevices"></a>Niet-gevalideerde VPN-apparaten

Als uw apparaat niet in de tabel met gevalideerde VPN-apparaten wordt vermeld, werkt het misschien toch met een site-naar-site-verbinding. Neem contact op met de fabrikant van uw apparaat voor aanvullende ondersteuning en configuratie-instructies.

## <a name="editing"></a>Voorbeelden van het bewerken van apparaatconfiguraties

Nadat u het bij het VPN-apparaat meegeleverde configuratievoorbeeld hebt gedownload, moet u enkele waarden veranderen zodat ze overeenkomen met de instellingen voor uw omgeving.

### <a name="to-edit-a-sample"></a>U bewerkt een voorbeeld als volgt:

1. Open het voorbeeld met Kladblok.
2. Zoek alle <*tekst*>-tekenreeksen en vervang ze door de waarden die betrekking hebben op uw omgeving. Zorg dat u < en > opneemt. Als u een naam opgeeft, moet deze uniek zijn. Als een opdracht niet werkt, raadpleeg dan de documentatie van de fabrikant van uw apparaat.

| **Voorbeeldtekst** | **Wijzig in** |
| --- | --- |
| &lt;RP_OnPremisesNetwork&gt; |De naam die u voor dit object hebt gekozen. Voorbeeld: myOnPremisesNetwork |
| &lt;RP_AzureNetwork&gt; |De naam die u voor dit object hebt gekozen. Voorbeeld: myAzureNetwork |
| &lt;RP_AccessList&gt; |De naam die u voor dit object hebt gekozen. Voorbeeld: myAzureAccessList |
| &lt;RP_IPSecTransformSet&gt; |De naam die u voor dit object hebt gekozen. Voorbeeld: myIPSecTransformSet |
| &lt;RP_IPSecCryptoMap&gt; |De naam die u voor dit object hebt gekozen. Voorbeeld: myIPSecCryptoMap |
| &lt;SP_AzureNetworkIpRange&gt; |Geef het bereik op. Voorbeeld: 192.168.0.0 |
| &lt;SP_AzureNetworkSubnetMask&gt; |Geef het subnetmasker op. Voorbeeld: 255.255.0.0 |
| &lt;SP_OnPremisesNetworkIpRange&gt; |Geef het on-premises bereik op. Voorbeeld: 10.2.1.0 |
| &lt;SP_OnPremisesNetworkSubnetMask&gt; |Geef het on-premises subnetmasker op. Voorbeeld: 255.255.255.0 |
| &lt;SP_AzureGatewayIpAddress&gt; |Deze informatie is specifiek voor uw virtuele netwerk en u vindt deze in de beheerportal als **IP-adres van gateway**. |
| &lt;SP_PresharedKey&gt; |Deze informatie is specifiek voor uw virtuele netwerk en u vindt deze in de beheerportal onder Sleutel beheren. |

## <a name="ipsec"></a>IPSec-/IKE-parameters

> [!IMPORTANT]
> 1. De onderstaande tabellen bevatten de combinaties van algoritmen en parameters die in de standaardconfiguratie voor Azure VPN-gateways worden gebruikt. Voor op routes gebaseerde VPN-gateways die zijn gemaakt met het Azure Resource Management-implementatiemodel, kunt u voor elke afzonderlijke verbinding een aangepast beleid opgeven. Raadpleeg [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) (IPsec/IKE-beleid configureren) voor gedetailleerde instructies.
>
> 2. Bovendien moet u TCP **MSS** vastzetten op **1350**. Als uw VPN-apparaten het vastzetten van MSS niet ondersteunen, kunt u in plaats daarvan ook de **MTU** op de tunnelinterface **1400** instellen op bytes.
>

In de volgende tabellen:

* SA = Security Association
* IKE Phase 1 wordt ook 'Main Mode' genoemd
* IKE Phase 2 wordt ook 'Quick Mode' genoemd

### <a name="ike-phase-1-main-mode-parameters"></a>Parameters voor IKE Phase 1 (Main Mode)

| **Eigenschap**          |**PolicyBased**    | **RouteBased**    |
| ---                   | ---               | ---               |
| IKE-versie           |IKEv1              |IKEv2              |
| Diffie-Hellman-groep  |Groep 2 (1024 bits) |Groep 2 (1024 bits) |
| Verificatiemethode |Vooraf gedeelde sleutel     |Vooraf gedeelde sleutel     |
| Versleutelings- en hash-algoritmen |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |1. AES256, SHA1<br>2. AES256, SHA256<br>3. AES128, SHA1<br>4. AES128, SHA256<br>5. 3DES, SHA1<br>6. 3DES, SHA256 |
| SA-levensduur           |28.800 seconden     |28.800 seconden     |

### <a name="ike-phase-2-quick-mode-parameters"></a>Parameters voor IKE Phase 2 (Quick Mode)

| **Eigenschap**                  |**PolicyBased**| **RouteBased**                              |
| ---                           | ---           | ---                                         |
| IKE-versie                   |IKEv1          |IKEv2                                        |
| Versleutelings- en hash-algoritmen |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |[RouteBased QM SA-aanbiedingen](#RouteBasedOffers) |
| SA-levensduur (tijd)            |3.600 seconden  |27.000 seconden                                |
| SA-levensduur (bytes)           |102.400.000 kB | -                                           |
| Perfect Forward Secrecy (PFS) |Nee             |[RouteBased QM SA-aanbiedingen](#RouteBasedOffers) |
| Dead Peer Detection (DPD)     |Niet ondersteund  |Ondersteund                                    |


### <a name ="RouteBasedOffers"></a>Aanbiedingen RouteBased VPN IPsec Security Association (IKE Quick Mode SA)

De volgende tabel bevat aanbiedingen van IPSec-SA (IKE Quick Mode). De aanbiedingen staan in volgorde van voorkeur waarin de aanbieding is gepresenteerd of geaccepteerd.

#### <a name="azure-gateway-as-initiator"></a>Azure-gateway als initiator

|-  |**Versleuteling**|**Verificatie**|**PFS-groep**|
|---| ---          |---               |---          |
| 1 |GCM AES256    |GCM (AES256)      |Geen         |
| 2 |AES256        |SHA1              |Geen         |
| 3 |3DES          |SHA1              |Geen         |
| 4 |AES256        |SHA256            |Geen         |
| 5 |AES128        |SHA1              |Geen         |
| 6 |3DES          |SHA256            |Geen         |

#### <a name="azure-gateway-as-responder"></a>Azure-Gateway als antwoorder

|-  |**Versleuteling**|**Verificatie**|**PFS-groep**|
|---| ---          | ---              |---          |
| 1 |GCM AES256    |GCM (AES256)      |Geen         |
| 2 |AES256        |SHA1              |Geen         |
| 3 |3DES          |SHA1              |Geen         |
| 4 |AES256        |SHA256            |Geen         |
| 5 |AES128        |SHA1              |Geen         |
| 6 |3DES          |SHA256            |Geen         |
| 7 |DES           |SHA1              |Geen         |
| 8 |AES256        |SHA1              |1            |
| 9 |AES256        |SHA1              |2            |
| 10|AES256        |SHA1              |14           |
| 11|AES128        |SHA1              |1            |
| 12|AES128        |SHA1              |2            |
| 13|AES128        |SHA1              |14           |
| 14|3DES          |SHA1              |1            |
| 15|3DES          |SHA1              |2            |
| 16|3DES          |SHA256            |2            |
| 17|AES256        |SHA256            |1            |
| 18|AES256        |SHA256            |2            |
| 19|AES256        |SHA256            |14           |
| 20|AES256        |SHA1              |24           |
| 21|AES256        |SHA256            |24           |
| 22|AES128        |SHA256            |Geen         |
| 23|AES128        |SHA256            |1            |
| 24|AES128        |SHA256            |2            |
| 25|AES128        |SHA256            |14           |
| 26|3DES          |SHA1              |14           |

* U kunt IPsec ESP NULL-versleuteling opgeven met RouteBased VPN-gateways en HighPerformance VPN-gateways. Op null gebaseerde versleuteling biedt geen beveiliging voor gegevens tijdens de overdracht. Dit mag alleen worden gebruikt wanneer maximale doorvoer en minimale latentie zijn vereist. Clients kunnen ervoor kiezen dit te gebruiken voor communicatie tussen VNET's of wanneer elders in de oplossing versleuteling wordt toegepast.
* Gebruik voor cross-premises connectiviteit via internet de standaardinstellingen voor Azure VPN-gateways met versleuteling en hash-algoritmen die in de tabel hierboven worden vermeld, om beveiliging van uw kritieke communicatie te waarborgen.

## <a name="known"></a>Bekende compatibiliteitsproblemen

> [!IMPORTANT]
> Dit zijn de bekende compatibiliteitsproblemen tussen VPN-apparaten van derden en Azure VPN-gateways. Het team van Azure werkt samen met de leveranciers aan een oplossing voor de hier vermelde problemen. Zodra de problemen zijn opgelost, wordt deze pagina bijgewerkt met de meest actuele informatie. Bekijk deze pagina daarom regelmatig.
>
>

### <a name="feb-16-2017"></a>16 februari 2017

**Palo Alto Networks-apparaten met een oudere versie dan 7.1.4** voor op route gebaseerde Azure VPN: als u VPN-apparaten van Palo Alto Networks gebruikt met een PAN-OS-versie die ouder is dan 7.1.4 en u connectiviteitsproblemen hebt met op route gebaseerde Azure VPN-gateways, voert u de volgende stappen uit:

1. Controleer de firmwareversie van uw Palo Alto Networks-apparaat. Als de PAN-OS-versie ouder is dan 7.1.4, voert u een upgrade uit naar 7.1.4.
2. Op het Palo Alto Networks-apparaat wijzigt u de levensduur van de beveiligingskoppeling fase 2 (of de beveiligingskoppeling in snelle modus) in 28.800 seconden (8 uur) wanneer er verbinding met de Azure VPN-gateway wordt gemaakt.
3. Als het connectiviteitsprobleem zich nog steeds voordoet, opent u een ondersteuningsaanvraag via de Azure-portal.