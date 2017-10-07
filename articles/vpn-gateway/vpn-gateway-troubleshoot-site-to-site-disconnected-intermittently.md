---
title: Azure Site-naar-Site VPN-verbinding wordt verbroken afwisselend aaaTroubleshoot | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot Hallo probleem in welke Hallo Site-naar-Site VPN-verbinding regelmatig wordt verbroken.
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a>Voor probleemoplossing: Azure Site-naar-Site VPN-verbinding verbreekt met tussenpozen

U kunt problemen Hallo dat een nieuwe of bestaande Microsoft Azure punt-naar-Site VPN-verbinding niet stabiel is of regelmatig wordt verbroken. Dit artikel vindt u stappen toohelp u identificeren en oplossen van Hallo oorzaak van Hallo probleem oplossen. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Stappen voor probleemoplossing

### <a name="prerequisite-step"></a>Vereiste stap

Controleer Hallo type gateway voor virtuele Azure-netwerk:

1. Ga te[Azure-portal](https://portal.azure.com).
2. Controleer de Hallo **overzicht** pagina van de virtuele netwerkgateway Hallo voor Hallo type informatie.
    
    ![Hallo-overzicht van Hallo-gateway](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Stap 1 Controleer of Hallo lokale VPN-apparaat wordt gevalideerd

1. Controleer of u een [gevalideerde VPN-apparaat en de versie van besturingssysteem](vpn-gateway-about-vpn-devices.md#devicetable). Als Hallo VPN-apparaat is niet gevalideerd, kunt u toocontact Hallo apparaat fabrikant toosee mogelijk als er een compatibiliteitsprobleem.
2. Zorg ervoor dat het Hallo-VPN-apparaat correct is geconfigureerd. Zie voor meer informatie [bewerken van apparaatconfiguraties](vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a>Stap 2 selectievakje Hallo beveiligingskoppeling instellingen (voor gateways voor virtuele Azure-netwerk op basis van beleid)

1. Zorg ervoor dat dit Hallo virtuele netwerk, subnetten en bereiken in Hallo **lokale netwerkgateway** definitie in Microsoft Azure zijn hetzelfde als het Hallo-configuratie op Hallo on-premises VPN-apparaat.
2. Controleer of overeenkomen met de instellingen van die Hallo beveiligingskoppeling.

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a>Stap 3-controle voor de gebruiker gedefinieerde Routes of Netwerkbeveiligingsgroepen van Gatewaysubnet

Een gebruiker gedefinieerde route op Hallo gatewaysubnet kan beperken sommige verkeer en andere verkeer toestaat. Op deze manier worden weergegeven dat Hallo VPN-verbinding voor verkeer onbetrouwbaar en geschikt is voor anderen. 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a>Stap 4 selectievakje 'een VPN-Tunnel per Subnet paar' Hallo instellen (voor gateways voor virtueel netwerk op basis van beleid)

Zorg ervoor dat Hallo lokale VPN-apparaat is ingesteld toohave **een VPN-tunnel per subnet paar** voor virtuele netwerkgateways op basis van beleid.

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a>Stap 5-controle voor beveiliging koppeling beperking (voor gateways voor virtueel netwerk op basis van beleid)

Hallo op beleid gebaseerde virtuele netwerkgateway heeft de limiet van 200 subnet beveiligingskoppeling paren. Als het aantal virtuele Azure-netwerksubnetten Hallo keren vermenigvuldigd door Hallo lokale subnetten aantal is groter dan 200, er sporadisch subnetten verbinding wordt verbroken.

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a>Stap 6 Controleer on-premises VPN-apparaat externe Interfaceadres

- Als hello Internetgericht IP-adres van Hallo VPN-apparaat is opgenomen in Hallo **lokale netwerkgateway** definitie in Azure, treden sporadisch worden verbroken.
- Hallo moet externe interface van het apparaat rechtstreeks op Hallo Internet. Er zijn geen NAT (Network Address Translation) of firewall tussen Hallo Internet en het Hallo-apparaat.
-  Als u op een virtueel IP-adres toohave Clustering Firewall configureert, moet u opsplitsen Hallo cluster en het Hallo-VPN-apparaat beschikbaar rechtstreeks tooa openbare interface die Hallo gateway kan verbinding maken met.

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a>Stap 7 controle of Hallo lokale VPN-apparaat is Perfect Forward Secrecy ingeschakeld

Hallo **Perfect Forward Secrecy** functie Hallo verbreken problemen kan veroorzaken. Als Hallo VPN-apparaat heeft **Perfect forward Secrecy** Hallo-functie ingeschakeld, uitschakelen. Vervolgens [Hallo virtueel netwerk gateway IPSec-beleid bijwerken](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).

## <a name="next-steps"></a>Volgende stappen

- [Een virtueel netwerk voor Site-naar-Site-verbinding tooa configureren](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [Beleid voor IPsec/IKE voor Site-naar-Site VPN-verbindingen configureren](vpn-gateway-ipsecikepolicy-rm-powershell.md)

