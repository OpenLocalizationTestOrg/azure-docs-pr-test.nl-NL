---
title: 'Maken en een ExpressRoute-circuit aanpassen: Azure portal | Microsoft Docs'
description: Dit artikel wordt beschreven hoe toocreate, inrichten, controleren, bijwerken, verwijderen en een ExpressRoute-circuit inrichting ervan ongedaan maakt.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a>Maken en een ExpressRoute-circuit wijzigen
> [!div class="op_single_selector"]
> * [Azure Portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure-CLI](howto-circuit-cli.md)
> * [Video - Azure-portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (klassiek)](expressroute-howto-circuit-classic.md)
>

Dit artikel wordt beschreven hoe een Azure ExpressRoute-circuit met behulp van toocreate hello Azure portal en hello Azure Resource Manager-implementatiemodel. volgende stappen uit ook Hallo ziet u hoe toocheck Hallo status van het Hallo-circuit, bijwerken of verwijderen en deze inrichting ervan ongedaan.


## <a name="before-you-begin"></a>Voordat u begint
* Bekijk Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.
* Zorg ervoor dat u toegang toohello hebt [Azure-portal](https://portal.azure.com).
* Zorg ervoor dat u machtigingen toocreate nieuwe netwerkresources. Neem contact op met uw accountbeheerder als u niet de juiste machtigingen Hallo hebt.
* U kunt [Bekijk een video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) voordat u begint in volgorde toobetter Hallo stappen begrijpen.

## <a name="create-and-provision-an-expressroute-circuit"></a>Maken en een ExpressRoute-circuit inrichten
### <a name="1-sign-in-toohello-azure-portal"></a>1. Meld u aan toohello Azure-portal
Navigeer via een browser toohello [Azure-portal](http://portal.azure.com) en meld u aan met uw Azure-account.

### <a name="2-create-a-new-expressroute-circuit"></a>2. Een nieuwe ExpressRoute-circuit maken
> [!IMPORTANT]
> Uw ExpressRoute-circuit worden gefactureerd vanaf Hallo moment dat die de sleutel van een service wordt verleend. Zorg ervoor dat u deze bewerking niet uitvoeren wanneer de connectiviteitsprovider Hallo gereed tooprovision Hallo circuit.
> 
> 

1. U kunt een ExpressRoute-circuit maken door het selecteren van Hallo optie toocreate een nieuwe resource. Klik op **nieuw** > **Networking** > **ExpressRoute**, zoals weergegeven in Hallo installatiekopie te volgen:
   
    ![Een ExpressRoute-circuit maken](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. Nadat u op **ExpressRoute**, ziet u Hallo **maken ExpressRoute-circuit** blade. Wanneer u Hallo waarden op deze blade hebt ingevuld, zorg ervoor dat u opgeeft dat de juiste SKU-laag Hallo en gegevensmeters.
   
   * **Laag** bepaalt of een standaard ExpressRoute of een premium-invoegtoepassing voor ExpressRoute is ingeschakeld. U kunt opgeven **standaard** tooget Hallo standaard SKU of **Premium** voor Hallo premium-invoegtoepassing.
   * **Gegevensmeters** bepaalt Hallo facturering type. U kunt opgeven **Metered** voor een plan datalimiet en **onbeperkt** voor een onbeperkte gegevens-plan. Houd er rekening mee dat u kunt facturering type Hallo van wijzigen **Metered** te**onbeperkt**, maar niet Hallo type uit **onbeperkt** te**Metered**.
     
     ![Hallo SKU-laag en gegevensmeters configureren](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> Zorg ervoor dat Hallo Peering locatie geeft Hallo [fysieke locatie](expressroute-locations.md) waar u peering met Microsoft. Dit is **niet** gekoppeld te 'Locatie'-eigenschap die verwijst toohello Geografie waar hello Azure Network-Resource Provider zich bevindt. Hoewel ze niet zijn gerelateerd, is een goede gewoonte toochoose een Netwerkresourceprovider geografisch sluiten toohello Peering-locatie van het Hallo-circuit. 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a>3. Weergave Hallo circuits en -eigenschappen
**Alle Hallo circuits weergeven**

U vindt alle Hallo-circuits die u hebt gemaakt door te selecteren **alle resources** Hallo aan de linkerkant menu.

![Weergave circuits](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

**Hallo-eigenschappen weergeven**

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Eigenschappen weergeven](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>4. Sleutel tooyour Hallo-connectiviteit serviceprovider voor het inrichten van verzenden
Op deze blade **providerstatus** bevat informatie over de huidige status van de Hallo van inrichting Hallo serviceprovider zijde. **Status circuit** Hallo status biedt op Hallo Microsoft aan clientzijde. Zie voor meer informatie over het circuit inrichtingstatuswaarden hello [werkstromen](expressroute-workflows.md#expressroute-circuit-provisioning-states) artikel.

Bij het maken van nieuwe ExpressRoute-circuit liggen Hallo circuit Hallo status te volgen:

Providerstatus: niet ingericht<BR>
Circuit status: ingeschakeld

![Inrichting te initiëren](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

Hallo circuit verandert toohello status wanneer Hallo connectiviteitsprovider in Hallo-proces voor het inschakelen van deze voor u te volgen:

Providerstatus: inrichting<BR>
Circuit status: ingeschakeld

Voor u toobe kunnen toouse een ExpressRoute-circuit, moet het Hallo status volgende zijn:

Providerstatus: ingericht<BR>
Circuit status: ingeschakeld

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>5. Hallo-status en Hallo-status van de Hallo circuit sleutel regelmatig te controleren
U kunt weergeven Hallo-eigenschappen van het Hallo-circuit dat u geïnteresseerd bent in het door deze te selecteren. Controleer Hallo **providerstatus** en zorg ervoor dat deze te verplaatst**ingericht** voordat u doorgaat.

![Status van circuit en -provider](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a>6. Maken van uw configuratie van de routering
Raadpleeg voor stapsgewijze instructies toohello [ExpressRoute-circuit routeringsconfiguratie](expressroute-howto-routing-portal-resource-manager.md) toocreate artikel en circuit peerings wijzigen.

> [!IMPORTANT]
> Deze instructies zijn alleen van toepassing toocircuits die zijn gemaakt met serviceproviders die services op laag 2-connectiviteit aanbieden. Als u een serviceprovider die beheerde laag-3-services (meestal een IP VPN, zoals MPLS), uw connectiviteitsprovider configureren en beheren van routering voor u.
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a>7. Koppelen van een virtueel netwerk tooan ExpressRoute-circuit
Koppel vervolgens een virtueel netwerk tooyour ExpressRoute-circuit. Gebruik Hallo [tooExpressRoute circuits koppelt virtuele netwerken](expressroute-howto-linkvnet-arm.md) artikel als u met Hallo Resource Manager-implementatiemodel werkt.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Hallo-status van een ExpressRoute-circuit ophalen
U kunt de status van een circuit Hallo weergeven door deze te selecteren. 

![Status van een ExpressRoute-circuit](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a>Wijzigen van een ExpressRoute-circuit
U kunt bepaalde eigenschappen van een ExpressRoute-circuit wijzigen zonder enige impact op connectiviteit.

U kunt doen Hallo zonder uitvaltijd te volgen:

* In- of uitschakelen van een ExpressRoute premium-invoegtoepassing voor ExpressRoute-circuit.
* Hallo-bandbreedte verhoging van uw ExpressRoute-circuit mits capaciteit beschikbaar op Hallo-poort. Houd er rekening mee dat Hallo bandbreedte van een circuit downgraden wordt niet ondersteund. 
* Hallo softwarelicentiecontrole plan van gegevens Datalimiet tooUnlimited gegevens wijzigen. Houd er rekening mee dat veranderende Hallo softwarelicentiecontrole plan van onbeperkt tooMetered die gegevens worden niet ondersteund.
* U kunt inschakelen en uitschakelen *klassieke bewerkingen toestaan*.

Raadpleeg voor meer informatie over limieten en beperkingen toohello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).

toomodify een ExpressRoute-circuit, klikt u op Hallo **configuratie** zoals weergegeven in onderstaande afbeelding ziet Hallo.

![Circuit wijzigen](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

U kunt Hallo bandbreedte, SKU, factureringsmodel wijzigen en kunnen klassieke bewerkingen binnen Hallo configuratie blade.

> [!IMPORTANT]
> Mogelijk hebt u toorecreate hello ExpressRoute-circuit als er onvoldoende capaciteit op de bestaande poort Hallo. U kunt Hallo circuit niet upgraden als er geen extra capaciteit beschikbaar is op die locatie.
>
> U kunt Hallo bandbreedte van een ExpressRoute-circuit zonder onderbreking niet reduceren. Downgraden bandbreedte, moet u toodeprovision hello ExpressRoute-circuit en vervolgens opnieuw inrichten van nieuwe ExpressRoute-circuit.
> 
> Premium-invoegtoepassing uit te schakelen kunnen mislukken als u resources die groter zijn dan wat voor Hallo standaard circuit is toegestaan.
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Opheffen van inrichting en een ExpressRoute-circuit verwijderen
U kunt uw ExpressRoute-circuit verwijderen door het selecteren van Hallo **verwijderen** pictogram. Let op Hallo volgende:

* U moet alle virtuele netwerken vanuit Hallo ExpressRoute-circuit ontkoppelen. Als deze bewerking is mislukt, controleert u of er geen virtuele netwerken zijn gekoppeld toohello circuit.
* Als Hallo ExpressRoute-circuit serviceprovider Inrichtingsstatus **inrichten** of **ingericht** moet u werken met uw serviceprovider toodeprovision Hallo circuit op hun kant. We gaan tooreserve resources en kosten in rekening brengen totdat Hallo serviceprovider inrichting Hallo circuit is voltooid en een melding van ons.
* Als serviceprovider Hallo heeft gemaakt Hallo circuit (Hallo serviceprovider Inrichtingsstatus te is ingesteld**niet ingericht**) kunt u Hallo circuit verwijderen. Hiermee stopt u facturering voor Hallo circuit

## <a name="next-steps"></a>Volgende stappen
Nadat u het circuit hebt gemaakt, moet u Hallo te volgen:

* [Maken en aanpassen van routering voor ExpressRoute-circuit](expressroute-howto-routing-portal-resource-manager.md)
* [Koppelen van uw virtuele netwerk tooyour ExpressRoute-circuit](expressroute-howto-linkvnet-arm.md)

