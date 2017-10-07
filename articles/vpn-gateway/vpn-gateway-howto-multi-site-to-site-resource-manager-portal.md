---
title: 'Toevoegen van meerdere VPN-gateway Site-naar-Site-verbindingen tooa VNet: Azure-Portal: Resource Manager | Microsoft Docs'
description: Toevoegen van meerdere sites S2S-verbindingen tooa VPN-gateway met een bestaande verbinding
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a>Toevoegen van een Site-naar-Site-verbinding tooa VNet met een bestaande VPN-gateway-verbinding

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (klassiek)](vpn-gateway-multi-site.md)
>
> 

Dit artikel begeleidt u bij hello Azure portal tooadd Site-naar-Site (S2S)-verbindingen tooa VPN-gateway met een bestaande verbinding gebruiken. Dit type verbinding is vaak waarnaar wordt verwezen tooas een 'multi-site'-configuratie. U kunt een S2S-verbinding tooa VNet waarop al een S2S-verbinding, een punt-naar-Site-verbinding of een VNet-naar-VNet-verbinding toevoegen. Er zijn enkele beperkingen bij het toevoegen van verbindingen. Controleer de Hallo [voordat u begint met](#before) sectie in dit artikel tooverify voordat u uw configuratie. 

In dit artikel van toepassing is gemaakt met Resource Manager-implementatiemodel Hallo tooVNets waarvoor een RouteBased VPN-gateway. Deze stappen zijn niet van toepassing tooExpressRoute/Site-naar-Site naast elkaar bestaande verbinding configuraties. Zie [ExpressRoute/S2S naast elkaar bestaande verbindingen](../expressroute/expressroute-howto-coexist-resource-manager.md) voor informatie over naast elkaar bestaande verbindingen.

### <a name="deployment-models-and-methods"></a>Implementatiemodellen en -methoden
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Deze tabel wordt bijgewerkt als er nieuwe artikelen en aanvullende hulpprogramma's beschikbaar zijn voor deze configuratie. Wanneer een artikel beschikbaar is, koppelen we rechtstreeks tooit uit deze tabel.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a>Voordat u begint
Controleer of de volgende items Hallo:

* Geen maakt u een ExpressRoute/S2S naast elkaar bestaande verbinding.
* U hebt een virtueel netwerk dat is gemaakt met de Hallo Resource Manager-implementatiemodel met een bestaande verbinding.
* de virtuele netwerkgateway Hallo voor uw VNet is RouteBased. Als u een PolicyBased VPN-gateway hebt, moet u Hallo virtuele netwerkgateway verwijderen en maak een nieuwe VPN-gateway als RouteBased.
* Geen Hallo-adresbereiken voor een van de VNets die dit VNet verbinding met maakt Hallo niet overlappen.
* U hebt compatibel VPN-apparaat en iemand die dit kunnen tooconfigure deze. Zie [About VPN Devices](vpn-gateway-about-vpn-devices.md) (Over VPN-apparaten). Als u niet bekend bent met het configureren van uw VPN-apparaat of niet bekend met de Hallo IP-adresbereiken zich in uw on-premises netwerkconfiguratie bent, moet u toocoordinate met iemand die deze details voor u verstrekken kan.
* U hebt een extern gericht openbaar IP-adres voor uw VPN-apparaat. Dit IP-adres kan zich niet achter een NAT bevinden.

## <a name="part1"></a>Deel 1: een verbinding configureren
1. Navigeer via een browser toohello [Azure-portal](http://portal.azure.com) en, indien nodig, meld u aan met uw Azure-account.
2. Klik op **alle resources** en zoek uw **virtuele netwerkgateway** uit Hallo lijst met resources en klik erop.
3. Op Hallo **virtuele netwerkgateway** blade, klikt u op **verbindingen**.
   
    ![Blade Verbindingen](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Blade Verbindingen")<br>
4. Op Hallo **verbindingen** blade, klikt u op **+ toevoegen**.
   
    ![De knop verbinding toevoegen](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "de knop verbinding toevoegen")<br>
5. Op Hallo **verbinding toevoegen** blade Vul Hallo velden te volgen:
   
   * **Naam:** gewenste toogive toohello site die u verbinding met Hallo maakt Hallo-naam.
   * **Verbindingstype:** Selecteer **Site-naar-site (IPsec)**.
     
     ![Tabblad van de verbinding toevoegen](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "verbinding-tabblad toevoegen")<br>

## <a name="part2"></a>Deel 2: een lokale netwerkgateway toevoegen
1. Klik op **lokale netwerkgateway** ***een lokale netwerkgateway kiezen***. Hiermee opent u Hallo **de lokale netwerkgateway kiezen** blade.
   
    ![De lokale netwerkgateway kiezen](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "de lokale netwerkgateway kiezen")<br>
2. Klik op **nieuw** tooopen hello **de lokale netwerkgateway maken** blade.
   
    ![Blade lokale netwerkgateway maken](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "de lokale netwerkgateway maken")<br>
3. Op Hallo **de lokale netwerkgateway maken** blade Vul Hallo velden te volgen:
   
   * **Naam:** gewenste toogive toohello lokale gateway netwerkbron Hallo-naam.
   * **IP-adres:** Hallo openbaar IP-adres van VPN-apparaat Hallo op Hallo-site die u wilt dat tooconnect naar.
   * **Adresruimte:** Hallo-adresruimte die u wilt dat toobe toohello nieuwe lokale netwerksite gerouteerd.
4. Klik op **OK** op Hallo **de lokale netwerkgateway maken** blade toosave Hallo wijzigingen.

## <a name="part3"></a>Deel 3: Hallo gedeelde sleutel toevoegen en Hallo verbinding maken
1. Op Hallo **verbinding toevoegen** blade Hallo gedeelde sleutel die u wilt dat toouse toocreate uw verbinding toevoegen. U kunt gedeelde sleutel Hallo ophalen van uw VPN-apparaat, of een hier en configureer vervolgens uw VPN-apparaat toouse Hallo dezelfde gedeelde sleutel. Hallo belangrijk ding wordt Hallo sleutels zijn exact Hallo dezelfde.
   
    ![Gedeelde sleutel](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Gedeelde sleutel")<br>
2. Hallo onderaan de blade hello, klikt u op **OK** toocreate Hallo verbinding.

## <a name="part4"></a>Deel 4 – Hallo VPN-verbinding controleren


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a>Volgende stappen

Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie Hallo virtuele machines [leertraject](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) voor meer informatie.
