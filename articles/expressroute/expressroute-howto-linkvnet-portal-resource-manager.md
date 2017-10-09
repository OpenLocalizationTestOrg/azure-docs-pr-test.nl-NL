---
title: 'Koppelen van een virtueel netwerk tooan ExpressRoute-circuit: Azure portal | Microsoft Docs'
description: Dit document bevat een overzicht van hoe toolink virtuele (vnet's) tooExpressRoute circuits netwerken.
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Verbinding maken met een virtueel netwerk tooan ExpressRoute-circuit
> [!div class="op_single_selector"]
> * [Azure Portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure-CLI](howto-linkvnet-cli.md)
> * [Video - Azure-portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (klassiek)](expressroute-howto-linkvnet-classic.md)
> 

In dit artikel helpt u bij virtuele netwerken (vnet's) tooAzure ExpressRoute-circuits koppelen met Hallo Resource Manager-implementatiemodel en hello Azure-portal. Virtuele netwerken kunnen zijn in Hallo hetzelfde abonnement, of dat ze deel kunnen uitmaken van een ander abonnement.

## <a name="before-you-begin"></a>Voordat u begint
* Bekijk Hallo [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.
* U moet een actief ExpressRoute-circuit hebben.
  
  * Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-portal-resource-manager.md) en laat Hallo-circuit inschakelen door de connectiviteitsprovider.
  * Zorg ervoor dat u persoonlijke Azure-peering voor uw circuit is geconfigureerd. Zie Hallo [Configure routing](expressroute-howto-routing-portal-resource-manager.md) artikel voor routering instructies.
  * Zorg ervoor dat persoonlijke Azure-peering is geconfigureerd en actief Hallo BGP-peering tussen uw netwerk en Microsoft is, zodat u kunt end-to-end-connectiviteit inschakelen.
  * Zorg ervoor dat u hebt een virtueel netwerk en een virtuele netwerkgateway gemaakt en volledig is ingericht. Hallo-instructies te volgen[maken van een virtuele netwerkgateway voor ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Hallo GatewayType 'ExpressRoute' niet VPN maakt gebruik van een virtuele netwerkgateway voor ExpressRoute.

* U kunt een koppeling van too10 virtuele netwerken tooa standaard ExpressRoute-circuit. Alle virtuele netwerken moet Hallo dezelfde geopolitieke regio bij gebruik van een standaard ExpressRoute-circuit. 
* U kunt een virtueel netwerk buiten de geopolitieke regio Hallo Hallo ExpressRoute-circuit koppelen of verbinding maken met een groter aantal virtuele netwerken tooyour ExpressRoute-circuit als u premium-invoegtoepassing voor ExpressRoute Hallo ingeschakeld. Controleer de Hallo [Veelgestelde vragen over](expressroute-faqs.md) voor meer informatie over Hallo premium-invoegtoepassing.
* U kunt [Bekijk een video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) voordat begin toobetter begrijpen Hallo stappen.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Verbinding maken met een virtueel netwerk in Hallo hetzelfde abonnement tooa circuit

### <a name="toocreate-a-connection"></a>toocreate een verbinding

> [!NOTE]
> BGP-configuratie-informatie wordt niet weergegeven als Hallo laag 3-provider uw peerings geconfigureerd. Als uw circuit ingericht status heeft is, moet u kunnen toocreate verbindingen.
>

1. Zorg ervoor dat uw ExpressRoute-circuit en de persoonlijke Azure-peering correct is geconfigureerd. Volg de instructies in Hallo [maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en [Configure routing](expressroute-howto-routing-arm.md). Uw ExpressRoute-circuit moet eruitzien als Hallo installatiekopie te volgen:

    ![ExpressRoute-circuit-schermafbeelding](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. U kunt nu starten inrichten van een verbinding toolink uw virtuele netwerk gateway tooyour ExpressRoute-circuit. Klik op **verbinding** > **toevoegen** tooopen hello **verbinding toevoegen** blade en configureer vervolgens Hallo waarden.

    ![Schermafbeelding van de verbinding toevoegen](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. Nadat de verbinding is geconfigureerd, ziet uw verbindingsobject Hallo-informatie voor Hallo-verbinding.

     ![Schermafbeelding van de verbinding-object](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a>toodelete een verbinding
U kunt een verbinding verwijderen door het selecteren van Hallo **verwijderen** pictogram op de blade Hallo voor de verbinding.

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Verbinding maken met een virtueel netwerk in een ander abonnement tooa circuit
U kunt een ExpressRoute-circuit delen tussen meerdere abonnementen. Hallo afbeelding hieronder ziet een eenvoudige schematische van hoe delen werkt voor ExpressRoute-circuits voor meerdere abonnementen.

![Abonnementoverschrijdende connectiviteit](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- Elk van de kleinere clouds binnen grote cloud Hallo Hallo is gebruikte toorepresent abonnementen die deel uitmaken van toodifferent afdelingen binnen een organisatie.
- Elk van de afdelingen binnen de organisatie Hallo Hallo hun eigen abonnement kunt gebruiken voor het implementeren van hun services, maar ze kunnen een enkel ExpressRoute-circuit tooconnect back tooyour on-premises netwerk delen.
- Één afdeling (in dit voorbeeld: IT) eigenaar kunnen Hallo ExpressRoute-circuit. Andere abonnementen binnen de organisatie Hallo kunnen Hallo ExpressRoute-circuit gebruiken.

    > [!NOTE]
    > Verbindingen en bandbreedte kosten voor speciale Hallo circuit zijn toegepaste toohello ExpressRoute-circuiteigenaar. Alle virtuele netwerken Hallo delen dezelfde bandbreedte.
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a>Beheer - circuit eigenaars en circuit gebruikers

Hallo 'circuiteigenaar' is een geautoriseerde gebruiker Power Hallo ExpressRoute-circuit resource. Hallo circuiteigenaar kunt autorisaties die kunnen worden ingewisseld door 'circuit gebruikers' maken. Circuit gebruikers kunnen eigenaren van het virtuele netwerk gateways die niet binnen hetzelfde abonnement Hallo zoals Hallo ExpressRoute-circuit. Circuit gebruikers kunnen inwisselen autorisaties (één autorisatie per virtueel netwerk).

Hallo circuiteigenaar heeft Hallo power toomodify en trek autorisaties op elk gewenst moment. Intrekken van een vergunning resulteert in alle koppeling verbindingen wordt verwijderd uit het Hallo-abonnement waarvoor de toegang is ingetrokken.

### <a name="circuit-owner-operations"></a>Circuit eigenaar bewerkingen

**een verbindingsverificatie toocreate**

Hallo circuiteigenaar maakt een autorisatie. Dit resulteert in Hallo maken van een autorisatiesleutel die kan worden gebruikt door een gebruiker circuit tooconnect hun virtuele netwerk gateways toohello ExpressRoute-circuit. Een vergunning is geldig voor slechts één verbinding.

1. Klik op Hallo ExpressRoute blade **autorisaties** en typ vervolgens een **naam** voor Hallo autorisatie en klik op **opslaan**.

    ![autorisaties](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. Zodra het Hallo-configuratie is opgeslagen, kopiëren Hallo **Resource-ID** en Hallo **Autorisatiesleutel**.

    ![Autorisatiesleutel](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

**een verbindingsverificatie toodelete**

U kunt een verbinding verwijderen door het selecteren van Hallo **verwijderen** pictogram op de blade Hallo voor de verbinding.

### <a name="circuit-user-operations"></a>Bewerkingen voor circuit-gebruikers

Hallo circuit gebruiker moet Hallo resource-ID en een autorisatiesleutel van Hallo circuiteigenaar. 

**een verbindingsverificatie tooredeem**

1.  Klik op Hallo **+ nieuw** knop.

    ![Klik op nieuwe](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  Zoeken naar **'Verbinding'** in Hallo Marketplace, te selecteren en op **maken**.

    ![Zoekactie voor verbinding](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  Zorg ervoor dat Hallo **verbindingstype** te is ingesteld 'ExpressRoute'.


4.  Vul Hallo details en klik vervolgens op **OK** in de blade grondbeginselen Hallo.

    ![Blade Grondbeginselen](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  In Hallo **instellingen** blade, selecteer Hallo **virtuele netwerkgateway** en controleer Hallo **inwisselen autorisatie** selectievakje.

6.  Voer Hallo **autorisatiesleutel** en Hallo **circuit URI Peer** en geef een naam op Hallo-verbinding. Klik op **OK**.

    ![Blade Instellingen](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. Lees de informatie Hallo in Hallo **samenvatting** blade en klik op **OK**.


**een verbindingsverificatie toorelease**

U kunt een vergunning vrijgeven door Hallo-verbinding die is gekoppeld aan Hallo ExpressRoute-circuit toohello virtueel netwerk te verwijderen.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).
