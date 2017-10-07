---
title: aaaDiagnose On-Premises connectiviteit via VPN-gateway met Azure-netwerk-Watcher | Microsoft Docs
description: Dit artikel wordt beschreven hoe toodiagnose lokale connectiviteit via VPN-gateway met Azure-netwerk-Watcher resource probleemoplossing.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: aeffbf3d-fd19-4d61-831d-a7114f7534f9
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9941c5d1b49bec29062210684dae8653cbdb84b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-on-premises-connectivity-via-vpn-gateways"></a>Diagnose van lokale connectiviteit via VPN-gateways

Azure VPN-Gateway kunt u toocreate hybride oplossing die Hallo behoefte voor een beveiligde verbinding tussen uw on-premises netwerk en uw virtuele Azure-netwerk. Als uw vereisten uniek zijn, dus u Hallo keuze van on-premises VPN-apparaat. Azure ondersteunt momenteel [meerdere VPN-apparaten](../vpn-gateway/vpn-gateway-about-vpn-devices.md#devicetable) die voortdurend samen met Apparaatleveranciers Hallo worden gevalideerd. Bekijk Hallo apparaat-specifieke configuratie-instellingen voordat u uw on-premises VPN-apparaat configureert. Op deze manier Azure VPN-Gateway is geconfigureerd met een reeks [IPSec-parameters ondersteund](../vpn-gateway/vpn-gateway-about-vpn-devices.md#ipsec) die worden gebruikt voor het tot stand brengen van verbindingen. Er is momenteel geen manier voor u toospecify of Selecteer een specifieke combinatie van IPSec-parameters van hello Azure VPN-Gateway. Voor een geslaagde verbinding tussen on-premises en Azure Hallo on-premises instellingen voor VPN-apparaten moet in overeenstemming met IPsec-parameters Hallo voorgeschreven Azure VPN-Gateway. Als hello instellingen correct zijn, er is een verlies van verbinding en tot op heden deze problemen met het niet was trivial en meestal tooidentify en fix Hallo probleem duurde uren.

Hello Azure-netwerk-Watcher oplossen functie, u kunt toodiagnose problemen zijn met uw Gateway en verbindingen en binnen enkele minuten voldoende informatie toomake een gefundeerde beslissing nemen toorectify Hallo probleem.

## <a name="scenario"></a>Scenario

U wilt dat tooconfigure een site-naar-site-verbinding tussen Azure en on-premises met FortiGate zoals Hallo lokale VPN-Gateway. tooachieve voor dit scenario, zou u Hallo na de installatie vereist:

1. Virtuele netwerkgateway - Hallo VPN-Gateway in Azure
1. Lokale netwerkgateway - Hallo [lokale (FortiGate) VPN-Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) weergave in Azure-cloud
1. Site-naar-site-verbinding (op basis van beleid) - [verbinding tussen Hallo VPN-Gateway en Hallo lokale router](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#createconnection)
1. [FortiGate configureren](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/Site-to-Site_VPN_using_FortiGate.md)

Gedetailleerde stapsgewijze instructies voor het configureren van een Site-naar-Site-configuratie kunt u vinden op: [maken van een VNet met een Site-naar-Site-verbinding met hello Azure-portal](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

Een Hallo kritieke configuratiestappen is het configureren van Hallo IPsec communicatie-parameters, een onjuiste configuratie leidt tooloss van de verbinding tussen Hallo on-premises netwerk en Azure. Azure VPN-Gateways zijn momenteel geconfigureerde toosupport Hallo IPSec-parameters voor fase 1 te volgen. Houd er rekening mee, zoals eerder gezegd dat deze instellingen kunnen niet worden gewijzigd.  Zoals u in onderstaande tabel voor hello ziet, zijn versleutelingsalgoritmen hello wordt ondersteund door Azure VPN-Gateway AES256 en AES128 3DES.

### <a name="ike-phase-1-setup"></a>Configuratie IKE fase 1 setup

| **Eigenschap** | **PolicyBased** | **RouteBased en Standard of High-Performance VPN-gateway** |
| --- | --- | --- |
| IKE-versie |IKEv1 |IKEv2 |
| Diffie-Hellman-groep |Groep 2 (1024 bits) |Groep 2 (1024 bits) |
| Verificatiemethode |Vooraf gedeelde sleutel |Vooraf gedeelde sleutel |
| Versleutelingsalgoritmen |AES256 AES128 3DES |AES256 3DES |
| Hash-algoritme |SHA1(SHA128) |SHA1(SHA128), SHA2(SHA256) |
| Levensduur (tijd) van beveiligingskoppeling (SA) fase 1 |28.800 seconden |10.800 seconden |

Als een gebruiker zou u vereiste tooconfigure uw FortiGate een voorbeeldconfiguratie kunt u vinden op [GitHub](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/fortigate_show%20full-configuration.txt). U kunt onbewust uw FortiGate toouse SHA-512 geconfigureerd als Hallo hash-algoritme. Als deze algoritme geen ondersteunde algoritme voor verbindingen op basis van beleid is, werkt uw VPN-verbinding.

Deze problemen zijn moeilijk tootroubleshoot en hoofdoorzaken zijn vaak onduidelijke. In dit geval kunt u een ondersteuning ticket tooget Help-informatie over het oplossen van Hallo probleem openen. Maar oplossen met Azure-netwerk-Watcher API, kunt u deze problemen op uw eigen identificeren.

## <a name="troubleshooting-using-azure-network-watcher"></a>Problemen oplossen met behulp van Azure-netwerk-Watcher

toodiagnose uw verbinding verbinding tooAzure PowerShell en initiëren Hallo `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet. U vindt informatie over het gebruik van deze cmdlet op Hallo [virtuele netwerkgateway oplossen en verbindingen - PowerShell](network-watcher-troubleshoot-manage-powershell.md). Deze cmdlet kan toocomplete van toofew minuten duren.

Nadat het Hallo-cmdlet is voltooid, kunt u toohello-opslaglocatie is opgegeven in de cmdlet Hallo gaat tooget gedetailleerde informatie op over Hallo probleem en de logboeken. Azure-netwerk-Watcher maakt een zip-map met de Hallo logboekbestanden te volgen:

![1][1]

Open Hallo bestand met de naam IKEErrors.txt en wordt Hallo volgende fout, die wijzen op een probleem met lokale onjuiste configuratie IKE-instelling.

```
Error: On-premises device rejected Quick Mode settings. Check values.
     based on log : Peer sent NO_PROPOSAL_CHOSEN notify
```

Kunt u gedetailleerde informatie krijgen via Hallo Scrubbed wfpdiag.txt over Hallo fout, zoals in dit geval er vermeld dat er was `ERROR_IPSEC_IKE_POLICY_MATCH` die lead tooconnection niet goed werkt.

Een andere veelvoorkomende is configuratiefout Hallo onjuist gedeelde sleutels opgeven. Als deze in de Hallo voorgaande voorbeeld u verschillende gedeelde sleutels heeft opgegeven, ziet u Hallo IKEErrors.txt Hallo volgende fout: `Error: Authentication failed. Check shared key`.

Azure-netwerk-Watcher oplossen functie kunt u toodiagnose en oplossen van uw VPN-Gateway en de verbinding met Hallo gemak van een eenvoudig PowerShell-cmdlet. Momenteel ondersteuning voor diagnose Hallo volgende voorwaarden en we naar meer voorwaarde toe te voegen.

### <a name="gateway"></a>Gateway

| Fouttype | Reden | Logboek|
|---|---|---|
| NoFault | Wanneer er geen fout wordt gedetecteerd. |Ja|
| GatewayNotFound | Kan de Gateway of Gateway niet is ingericht niet vinden. |Nee|
| PlannedMaintenance |  Gateway-instantie is in onderhoud.  |Nee|
| UserDrivenUpdate | Wanneer een gebruiker wordt bijgewerkt. Dit wordt mogelijk een bewerking formaat wijzigen. | Nee |
| VipUnResponsive | Kan de primaire instantie Hallo Hallo Gateway niet bereiken. Dit gebeurt wanneer Hallo health test is mislukt. | Nee |
| PlatformInActive | Er is een probleem met het Hallo-platform. | Nee|
| ServiceNotRunning | Hallo onderliggende service is niet uitgevoerd. | Nee|
| NoConnectionsFoundForGateway | Er bestaat geen verbindingen op Hallo-gateway. Dit is alleen een waarschuwing.| Nee|
| ConnectionsNotConnected | Geen van Hallo verbindingen zijn verbonden. Dit is alleen een waarschuwing.| Ja|
| GatewayCPUUsageExceeded | huidige netwerkgatewaygebruik Hallo CPU-gebruik is > 95%. | Ja |

### <a name="connection"></a>Verbinding

| Fouttype | Reden | Logboek|
|---|---|---|
| NoFault | Wanneer er geen fout wordt gedetecteerd. |Ja|
| GatewayNotFound | Kan de Gateway of Gateway niet is ingericht niet vinden. |Nee|
| PlannedMaintenance | Gateway-instantie is in onderhoud.  |Nee|
| UserDrivenUpdate | Wanneer een gebruiker wordt bijgewerkt. Dit wordt mogelijk een bewerking formaat wijzigen.  | Nee |
| VipUnResponsive | Kan de primaire instantie Hallo Hallo Gateway niet bereiken. Dit gebeurt als Hallo health test is mislukt. | Nee |
| ConnectionEntityNotFound | Verbindingsconfiguratie ontbreekt. | Nee |
| ConnectionIsMarkedDisconnected | Hallo verbinding is gemarkeerd als "verbinding verbroken." |Nee|
| ConnectionNotConfiguredOnGateway | onderliggende Hallo-service heeft geen Hallo-verbinding geconfigureerd. | Ja |
| ConnectionMarkedStandy | Hallo onderliggende service is gemarkeerd als stand-by.| Ja|
| Authentication | Vooraf gedeelde sleutel komt niet overeen. | Ja|
| PeerReachability | Hallo peer gateway is niet bereikbaar. | Ja|
| IkePolicyMismatch | Hallo peer gateway heeft IKE-beleidsregels die worden niet ondersteund door Azure. | Ja|
| WfpParse fout | Er is een fout opgetreden bij het parseren Hallo WFP-logboek. |Ja|

## <a name="next-steps"></a>Volgende stappen

Meer informatie over toocheck VPN-Gateway-verbinding met PowerShell en Azure Automation in via [Monitor VPN-gateways bij het oplossen van Azure-netwerk-Watcher](network-watcher-monitor-with-azure-automation.md)

[1]: ./media/network-watcher-diagnose-on-premises-connectivity/figure1.png
