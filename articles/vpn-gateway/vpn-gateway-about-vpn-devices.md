---
title: aaaAbout VPN-apparaten voor cross-premises Azure-verbindingen | Microsoft Docs
description: Dit artikel gaat over VPN-apparaten en IPSec-parameters voor cross-premises site-naar-site-VPN-gateway-verbindingen. Koppelingen vindt u tooconfiguration-instructies en voorbeelden.
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
ms.openlocfilehash: 8b84afbf93d807342ecd56ab369d5909a13343e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-devices-and-ipsecike-parameters-for-site-to-site-vpn-gateway-connections"></a>VPN-apparaten en IPSec-/IKE-parameters voor site-naar-site-VPN-gateway-verbindingen

Een VPN-apparaat is vereist tooconfigure een Site-naar-Site (S2S) cross-premises VPN-verbinding via een VPN-gateway. Site-naar-Site-verbindingen kunnen gebruikte toocreate een hybride oplossing of gewenst beveiligde verbindingen tussen uw on-premises netwerken en uw virtuele netwerken. Dit artikel bevat een lijst met gevalideerde VPN-apparaten en een lijst met IPSec-/IKE-parameters voor VPN-gateways.

> [!IMPORTANT]
> Als u problemen met de netwerkverbinding tussen uw on-premises VPN-apparaten en VPN-gateways ondervindt, raadpleeg dan te[bekende compatibiliteitsproblemen apparaat](#known).
>
>

### <a name="items-toonote-when-viewing-hello-tables"></a>Items toonote wanneer u bekijkt hello tabellen:

* Er is een terminologiewijziging voor Azure VPN-gateways. Alleen Hallo namen zijn gewijzigd. Er is geen wijziging in de functionaliteit.
  * Statische routering = PolicyBased
  * Dynamische routering = RouteBased
* Specificaties voor HighPerformance VPN-gateway en RouteBased VPN-gateway zijn Hallo hetzelfde, tenzij anders vermeld. Hallo gevalideerde VPN-apparaten die compatibel met RouteBased VPN-gateways zijn zijn bijvoorbeeld ook compatibel met Hallo HighPerformance VPN-gateway.

## <a name="devicetable"></a>Gevalideerde VPN-apparaten en apparaatconfiguratiehandleidingen

> [!NOTE]
> Wanneer u een S2S-verbinding configureert, hebt u een openbaar IPv4-adres voor het VPN-apparaat nodig.
>

We hebben samen met apparaatleveranciers een reeks standaard VPN-apparaten gevalideerd. Alle apparaten in de apparaatfamilies Hallo in lijst na Hallo Hallo moet samenwerken met VPN-gateways. Zie [over VPN-Gateway-instellingen](vpn-gateway-about-vpn-gateway-settings.md#vpntype) toounderstand Hallo VPN-gebruik (PolicyBased of RouteBased) voor VPN-Gateway-oplossing die u wilt dat tooconfigure Hallo typt.

toohelp uw VPN-apparaat configureren, raadpleegt u toohello-koppelingen die overeenkomen met tooappropriate apparaatfamilie. Hallo koppelingen tooconfiguration instructies vindt u op basis van best-effort. Voor ondersteuning van VPN-apparaten neemt u contact op met de fabrikant van uw apparaat.

|**Leverancier**          |**Apparaatfamilie**     |**Minimale versie van het besturingssysteem** |**PolicyBased configuratie-instructies** |**RouteBased configuratie-instructies** |
| ---                | ---                  | ---                   | ---            | ---           |
| A10 Networks, Inc. |Thunder CFW           |ACOS 4.1.1             |Niet compatibel  |[Configuratiehandleiding](https://www.a10networks.com/resources/deployment-guides/a10-thunder-cfw-ipsec-vpn-interoperability-azure-vpn-gateways)|
| Allied Telesis     |VPN-routers uit AR-serie |2.9.2                  |Binnenkort beschikbaar     |Niet compatibel  |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall F-serie |PolicyBased: 5.4.3<br>RouteBased: 6.2.0 |[Configuratiehandleiding](https://techlib.barracuda.com/NGF/AzurePolicyBasedVPNGW) |[Configuratiehandleiding](https://techlib.barracuda.com/NGF/AzureRouteBasedVPNGW) |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall X-serie |Barracuda Firewall 6.5 |[Configuratiehandleiding](https://techlib.barracuda.com/BFW/ConfigAzureVPNGateway) |Niet compatibel |
| Brocade            |Vyatta 5400 vRouter   |Virtual Router 6.6R3 GA|[Configuratiehandleiding](http://www1.brocade.com/downloads/documents/html_product_manuals/vyatta/vyatta_5400_manual/wwhelp/wwhimpl/js/html/wwhelp.htm#href=VPN_Site-to-Site%20IPsec%20VPN/Preface.1.1.html) |Niet compatibel |
| Check Point |Security Gateway |R77.30 |[Configuratiehandleiding](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |[Configuratiehandleiding](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |
| Cisco              |ASA       |8.3 |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA) |Niet compatibel |
| Cisco |ASR |PolicyBased: IOS 15.1<br>RouteBased: IOS 15.2 |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |
| Cisco |ISR |PolicyBased: IOS 15.0<br>RouteBased*: IOS 15.1 |[Voorbeelden van configuraties](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |[Voorbeelden van configuraties*](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |
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
| Openswan |Openswan |2.6.32 |(binnenkort beschikbaar) |Niet compatibel |
| Palo Alto Networks |Alle apparaten waarop PAN-OS wordt uitgevoerd |PAN-OS<br>PolicyBased: 6.1.5 of hoger<br>RouteBased: 7.1.4 |[Configuratiehandleiding](https://live.paloaltonetworks.com/t5/Configuration-Articles/How-to-Configure-VPN-Tunnel-Between-a-Palo-Alto-Networks/ta-p/59065) |[Configuratiehandleiding](https://live.paloaltonetworks.com/t5/Integration-Articles/Configuring-IKEv2-VPN-for-Microsoft-Azure-Environment/ta-p/60340) |
| SonicWall |TZ-serie, NSA-serie<br>SuperMassive-serie<br>E-Class NSA-serie |SonicOS 5.8.x<br>SonicOS 5.9.x<br>SonicOS 6.x |[Configuratiehandleiding voor SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Configuratiehandleiding voor SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |[Configuratiehandleiding voor SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Configuratiehandleiding voor SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |
| WatchGuard |Alle |Fireware XTM<br> PolicyBased: v11.11.x<br>RouteBased: v11.12.x |[Configuratiehandleiding](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA2F00000000LI7KAM&lang=en_US) |[Configuratiehandleiding](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA22A000000XZogSAG&lang=en_US)|

(*) Routers uit de ISR 7200-serie bieden alleen ondersteuning voor PolicyBased VPN-verbindingen.

## <a name="additionaldevices"></a>Niet-gevalideerde VPN-apparaten

Als u uw apparaat weergegeven in de tabel van Hallo gevalideerde VPN-apparaten niet ziet, is het apparaat nog steeds mogelijk werken met een Site-naar-Site-verbinding. Neem contact op met de fabrikant van uw apparaat voor aanvullende ondersteuning en configuratie-instructies.

## <a name="editing"></a>Voorbeelden van het bewerken van apparaatconfiguraties

Nadat u Hallo opgegeven VPN-apparaat configuratievoorbeeld hebt gedownload, moet u tooreplace aantal Hallo waarden tooreflect Hallo-instellingen voor uw omgeving.

### <a name="tooedit-a-sample"></a>een voorbeeld van een tooedit:

1. Open Hallo voorbeeld met Kladblok.
2. Zoeken en vervangen van alle <*tekst*> tekenreeksen met Hallo-waarden die betrekking tooyour omgeving hebben. Worden ervoor tooinclude < en >. Als u een naam opgeeft, moet Hallo-naam die u selecteert uniek zijn. Als een opdracht niet werkt, raadpleeg dan de documentatie van de fabrikant van uw apparaat.

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
| &lt;SP_AzureGatewayIpAddress&gt; |Deze informatie specifieke tooyour virtueel netwerk en bevindt zich in het Hallo-beheerportal als **IP-adres Gateway**. |
| &lt;SP_PresharedKey&gt; |Deze informatie is specifiek tooyour virtueel netwerk en bevindt zich in het Hallo-beheerportal onder sleutel beheren. |

## <a name="ipsec"></a>IPSec-/IKE-parameters

> [!NOTE]
> Hoewel het Hallo-waarden die worden vermeld in de volgende tabel Hallo worden ondersteund door Hallo VPN-gateway, momenteel er is geen methode voor u toospecify of Selecteer een specifieke combinatie van algoritmen of parameters van Hallo VPN-gateway. U moet eventuele beperkingen vanuit Hallo on-premises VPN-apparaat opgeven. Bovendien moet u **MSS** vastzetten op **1350**.
> 
>

In de Hallo tabellen te volgen:

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

Hallo bevat volgende tabel aanbiedingen voor IPSec-SA (IKE snelle modus). Aanbiedingen zijn vermelde Hallo volgorde van voorkeur die Hallo aanbieding is gepresenteerd of geaccepteerd.

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

* U kunt IPsec ESP NULL-versleuteling opgeven met RouteBased VPN-gateways en HighPerformance VPN-gateways. Op null gebaseerde versleuteling biedt geen bescherming toodata onderweg en mag alleen worden gebruikt wanneer maximale doorvoer en minimale latentie is vereist. Clients kunnen Kies toouse deze in scenario's voor VNet-naar-VNet-communicatie, of als versleuteling wordt toegepast elders in Hallo-oplossing.
* Gebruik voor cross-premises connectiviteit via Internet hello, Hallo standaard Azure VPN-gateway-instellingen met versleuteling en hash-algoritmen opgenomen in de tabellen Hallo hierboven tooensure beveiliging van uw kritieke communicatie.

## <a name="known"></a>Bekende compatibiliteitsproblemen

> [!IMPORTANT]
> Deze zijn Hallo bekende compatibiliteitsproblemen tussen Azure VPN-gateways en VPN-apparaten van derden. Hallo team van Azure werkt actief met Hallo leveranciers tooaddress Hallo problemen hier vermeld. Zodra het Hallo-problemen zijn opgelost, wordt deze pagina worden bijgewerkt met de meest actuele informatie Hallo. Bekijk deze pagina daarom regelmatig.
>
>

### <a name="feb-16-2017"></a>16 februari 2017

**Apparaten met versie voorafgaande too7.1.4 Palo Alto Networks** voor Azure op route gebaseerde VPN: als u van VPN-apparaten van Palo Alto-netwerken met eerdere too7.1.4 voor PAN-OS-versie gebruikmaakt en connectiviteit ondervinden problemen tooAzure op route gebaseerde VPN-gateways Voer Hallo stappen te volgen:

1. De firmwareversie Hallo van uw apparaat Palo Alto Networks controleren. Als uw PAN-OS-versie ouder dan 7.1.4 is, voer een upgrade too7.1.4.
2. Op Hallo Palo Alto Networks apparaat wijzigen Hallo SA voor fase 2 (of SA in de snelle modus) levensduur too28, 800 seconden (8 uur) wanneer toohello Azure VPN-gateway verbinding te maken.
3. Als u steeds problemen ondervindt nog, moet u een ondersteuningsaanvraag openen vanuit hello Azure-portal.
