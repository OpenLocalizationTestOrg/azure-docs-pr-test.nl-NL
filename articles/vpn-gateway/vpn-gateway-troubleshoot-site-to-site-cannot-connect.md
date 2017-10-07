---
title: een Azure VPN-verbinding voor site-naar-site die geen verbinding kan maken aaaTroubleshoot | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot een site-naar-site VPN-verbinding die plotseling werkt niet en kan niet worden hersteld.
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
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a>Voor probleemoplossing: Een Azure site-naar-site VPN-verbinding kan geen verbinding maken en werkt niet

Nadat u een site-naar-site VPN-verbinding tussen een on-premises netwerk en een Azure-netwerk configureert, wordt Hallo VPN-verbinding plotseling werkt niet en kan niet worden hersteld. In dit artikel voor probleemoplossing stappen toohelp vindt u dit probleem oplossen. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Stappen voor probleemoplossing

tooresolve hello probleem, probeer dan eerst te[reset hello Azure VPN-gateway](vpn-gateway-resetgw-classic.md) en Hallo tunnel van Hallo on-premises VPN-apparaat opnieuw instellen. Als het Hallo-probleem zich blijft voordoen, volgt u deze stappen tooidentify Hallo Hallo probleem veroorzaakt.

### <a name="prerequisite-step"></a>Vereiste stap

Controleer Hallo type hello Azure VPN-gateway.

1. Ga toohello [Azure-portal](https://portal.azure.com).

2. Controleer Hallo **overzicht** pagina Hallo VPN-gateway voor Hallo type informatie.
    
    ![Overzicht van Hallo-gateway](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Step 1. Controleer of de Hallo on-premises VPN-apparaat wordt gevalideerd

1. Controleer of u een [gevalideerde VPN-apparaat en de versie van besturingssysteem](vpn-gateway-about-vpn-devices.md#devicetable). Als het Hallo-apparaat is niet gevalideerde VPN-apparaat, kunt u toocontact Hallo apparaat fabrikant toosee wellicht als er een compatibiliteitsprobleem.

2. Zorg ervoor dat het Hallo-VPN-apparaat correct is geconfigureerd. Zie voor meer informatie [bewerken van apparaatconfiguraties](/vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-verify-hello-shared-key"></a>Stap 2. Controleer of de gedeelde sleutel Hallo

Hallo gedeelde sleutel voor Hallo lokale VPN-apparaat toohello Azure Virtual Network VPN toomake Hallo sleutels overeenkomen met vergelijken. 

tooview hello gedeelde sleutel voor hello Azure VPN-verbinding, een van de volgende methoden hello gebruiken:

**Azure Portal**

1. Ga toohello VPN-gateway site-naar-site-verbinding die u hebt gemaakt.

2. In Hallo **instellingen** sectie, klikt u op **gedeelde sleutel**.
    
    ![Gedeelde sleutel](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

**Azure PowerShell**

Hello Azure Resource Manager-implementatiemodel:

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

Voor het klassieke implementatiemodel Hallo:

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a>Stap 3. Controleer of Hallo VPN-peer IP-adressen

-   IP-definitie in Hallo Hallo **Local Network Gateway** -object in Azure moet overeenkomen met de Hallo lokale apparaat IP.
-   Hello Azure-gateway IP-definitie die is ingesteld op Hallo lokale apparaat moet overeenkomen met hello Azure-gateway IP.

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a>Stap 4. Controleer UDR en nsg's op Hallo gatewaysubnet

Controleren op en verwijderen van de gebruiker gedefinieerde Routering of Netwerkbeveiligingsgroepen (nsg's) op Hallo gatewaysubnet en test u Hallo resultaat. Als het Hallo-probleem is opgelost, controleert u Hallo-instellingen die UDR of NSG toegepast.

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a>Stap 5. Hallo lokale VPN-apparaat externe Interfaceadres controleren

- Als Hallo internetgerichte IP-adres van Hallo VPN-apparaat is opgenomen in Hallo **lokale netwerk** definitie in Azure, kunt u tegenkomen sporadisch worden verbroken.
- Hallo moet externe interface van het apparaat rechtstreeks op Hallo Internet. Er zijn geen netwerkadresomzetting of de firewall tussen Hallo Internet en het Hallo-apparaat.
- tooconfigure firewall clustering toohave een virtueel IP-adres, moet u Hallo cluster opsplitsen en Hallo-VPN-apparaat beschikbaar rechtstreeks tooa openbare interface die Hallo-gateway kan verbinding maken met.

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a>Stap 6. Controleren of subnetten Hallo exact overeenkomen (Azure op beleid gebaseerde gateways)

-   Controleer of dat Hallo subnetten exact hello virtuele Azure-netwerk- en lokale definities voor Hallo virtuele Azure-netwerk overeen.
-   Controleer of dat Hallo subnetten tussen Hallo exact overeenkomen met **Local Network Gateway** en on-premises definities voor Hallo on-premises netwerk.

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a>Stap 7. Controleer of de statuscontrole van hello Azure-gateway

1. Ga toohello [health test](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).

2. Klik in het Hallo-certificaatwaarschuwing.
3. Als u een antwoord ontvangt, Hallo VPN-gateway wordt beschouwd als in orde. Als u niet een antwoord ontvangt, Hallo gateway mogelijk niet in orde of Hallo probleem wordt veroorzaakt door een NSG op Hallo gatewaysubnet. na de tekst Hello is een voorbeeldantwoord:

    &lt;? XML-versie = "1.0"? > <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">primaire exemplaar: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6 < / tekenreeks&gt;

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a>Stap 8. Controleer of Hallo lokale VPN-apparaat heeft Hallo perfect forward secrecy functie is ingeschakeld

Hallo perfect forward secrecy functie veroorzaken verbreken problemen. Als Hallo VPN-apparaat perfect forward secrecy is ingeschakeld heeft, Hallo functie uitschakelen. Werk vervolgens Hallo VPN-gateway IPSec-beleid.

## <a name="next-steps"></a>Volgende stappen

-   [Een site-naar-site-verbinding tooa virtueel netwerk configureren](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [Beleid voor IPsec/IKE voor site-naar-site VPN-verbindingen configureren](vpn-gateway-ipsecikepolicy-rm-powershell.md)
