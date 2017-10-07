---
title: een virtueel netwerk aaaConfigure en Gateway voor ExpressRoute in de klassieke portal Hallo | Microsoft Docs
description: Dit artikel begeleidt u bij het instellen van een virtueel netwerk voor ExpressRoute met het klassieke implementatiemodel Hallo en Hallo klassieke portal.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 688817d9-51c8-4372-9af8-33fa098c7c5a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/20/2016
ms.author: cherylmc
ms.openlocfilehash: dd1f6c5e85dbb3ad0a53ecd81c13b4d3f5c06e66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-for-expressroute-in-hello-classic-portal"></a>Een virtueel netwerk maken voor ExpressRoute in de klassieke portal Hallo
Hallo stappen in dit artikel begeleidt u bij het configureren van een virtueel netwerk en een virtuele netwerkgateway voor gebruik met ExpressRoute met het klassieke implementatiemodel Hallo en Hallo klassieke portal.

Als u nog geen instructies voor het Hallo Resource Manager-implementatiemodel, kunt u Hallo artikelen te volgen: [een virtueel netwerk maken met behulp van PowerShell](../virtual-network/virtual-networks-create-vnet-arm-ps.md) en [toevoegen van een VPN-Gateway tooa Resource Manager VNet voor ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Over Azure-implementatiemodellen**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="create-a-classic-vnet-and-gateway"></a>Een klassiek VNet en gateway maken
Hallo volgende stappen maakt u een klassiek VNet en een virtuele netwerkgateway. Als u al een klassiek VNet hebt, raadpleegt u Hallo [configureren van een bestaande klassieke VNet](#config) sectie in dit artikel.

1. Meld u bij toohello [klassieke Azure-portal](http://manage.windowsazure.com).
2. In Hallo linkerbenedenhoek van Hallo scherm, klikt u op **nieuw**. Klik in het navigatiedeelvenster hello, **netwerkservices**, en klik vervolgens op **virtueel netwerk**. Klik op **aangepast maken** toobegin Hallo-configuratiewizard.
3. Op Hallo **Details van virtueel netwerk** pagina, voert u de volgende Hallo:
   
   * **Naam** – naam van het virtuele netwerk. U gebruikt deze virtuele-netwerknaam bij het implementeren van uw virtuele machines en PaaS-instanties, zodat u geen toomake Hallo naam is te ingewikkeld kunt.
   * **Locatie** – Hallo locatie is direct gerelateerd toohello fysieke locatie (regio) waar u uw tooreside resources (VM's). Als u Hallo virtuele machines die u toothis virtueel netwerk toobe fysiek bevinden in VS-Oost wilt implementeert, selecteert u die locatie in. U kunt Hallo regio die is gekoppeld aan het virtuele netwerk nadat u deze hebt gemaakt niet wijzigen.
4. Op Hallo **DNS-Servers en VPN-verbinding** pagina, Voer Hallo volgende informatie en klik op volgende pijl in de rechterbenedenhoek Hallo Hallo. 
   
   * **DNS-Servers** : Geef Hallo DNS-servernaam en IP-adres op of Selecteer een eerder geregistreerde DNS-server in het snelmenu Hallo. Met deze instelling wordt geen DNS-server gemaakt. Hiermee kunt u toospecify Hallo DNS-servers wilt u toouse voor naamomzetting voor dit virtuele netwerk.
   * **Site-naar-Site-connectiviteit** : Selecteer Hallo selectievakje voor **een site-naar-site-VPN configureren**.
   * **ExpressRoute** – Selecteer Hallo selectievakje **gebruik ExpressRoute**. Deze optie wordt alleen weergegeven als u hebt geselecteerd **een Site-naar-Site-VPN configureren**.
   * **Lokale netwerk** -zijn van vereiste toohave een lokale netwerksite voor ExpressRoute. Echter in geval van een ExpressRoute-verbinding Hallo Hallo adresvoorvoegsels opgegeven voor Hallo lokale netwerksite wordt genegeerd. In plaats daarvan geadverteerd Hallo adresvoorvoegsels tooMicrosoft via ExpressRoute-circuit hello worden gebruikt voor de routering.<BR>Als u al een lokaal netwerk gemaakt voor uw ExpressRoute-verbinding hebt, selecteert u deze uit de vervolgkeuzelijst Hallo. Zo niet, selecteer **opgeven van een nieuw lokaal netwerk**.
5. Hallo **Site-naar-Site-connectiviteit** pagina wordt weergegeven als u een nieuw lokaal netwerk toospecify in de vorige stap Hallo geselecteerd. tooconfigure uw lokale netwerk Hallo volgende informatie en klik vervolgens op Hallo pijl op volgende. 
   
   * **Naam** -Hallo gewenste naam toocall uw lokale netwerksite (op locatie).
   * **Adresruimte** - inclusief IP-beginadres en de CIDR (aantal adressen). Als deze niet met Hallo-adresbereik voor het virtuele netwerk overlappen, kunt u eventuele-adresbereik opgeven. Normaal gesproken geeft dit Hallo-adresbereiken voor uw on-premises netwerken, maar in geval van ExpressRoute Hallo deze instellingen niet worden gebruikt. Deze instelling is echter vereist in de volgorde toocreate Hallo lokale netwerk wanneer u de klassieke portal Hallo gebruikt.
   * **Adresruimte toevoegen** -deze instelling is niet relevant voor ExpressRoute.
6. Op Hallo **adresruimten voor virtueel netwerk** pagina, Voer Hallo volgende informatie en klik Hallo vinkje Hallo lagere rechts tooconfigure uw netwerk. 
   
   * **Adresruimte** - zoals begin-IP en los deze telling. Controleer of dat Hallo-adresruimten die u opgeeft niet overlappen met adresruimten Hallo die u op uw lokale netwerk hebt.
   * **Subnet toevoegen** - inclusief IP-beginadres en het aantal adressen. Er zijn geen aanvullende subnetten nodig.
   * **Gatewaysubnet toevoegen** -klikt u op tooadd hello gatewaysubnet. Hallo gatewaysubnet wordt alleen gebruikt voor de virtuele netwerkgateway Hallo en is vereist voor deze configuratie.<BR>Hallo gatewaysubnet CIDR (aantal adressen) voor ExpressRoute /28 moet of groter (/ 27, / 26 enzovoort.). Hierdoor voldoende IP-adressen in dat subnet tooallow Hallo configuratie toowork. In de klassieke portal hello, als u hebt geselecteerd Hallo selectievakje toouse ExpressRoute, geeft Hallo portal een gatewaysubnet met /28.  U kunt Hallo CIDR-adres telling in de klassieke portal Hallo niet aanpassen. Hallo gatewaysubnet wordt weergegeven als **Gateway** in de klassieke portal hello, hoewel hello echte naam van Hallo gatewaysubnet dat is gemaakt is daadwerkelijk **GatewaySubnet**. U kunt deze naam weergeven met behulp van PowerShell of in hello Azure-portal.
7. Klik op Hallo vinkje Hallo onderaan pagina Hallo en het virtuele netwerk toocreate begint. Wanneer deze is voltooid, ziet u **gemaakt** vermeld onder **Status** op Hallo **netwerken** pagina in de klassieke portal Hallo.

## <a name="gw"></a>Hallo-gateway maken
1. Op Hallo **netwerken** pagina, klikt u op Hallo virtuele netwerk dat u zojuist hebt gemaakt en klik op **Dashboard** bovenaan Hallo Hallo pagina.
2. Aan de onderkant Hallo Hallo **Dashboard** pagina, klikt u op **Gateway maken** en selecteer **dynamische routering**. Klik op **Ja** tooconfirm dat u wilt dat toocreate een gateway.
3. Wanneer het Hallo-gateway maken is gestart, ziet u een bericht waarin wordt aangegeven dat Hallo-gateway is gestart. Het kan Hallo-gateway toocreate too45 minuten duren.
4. Koppel uw netwerk tooa circuit. Volg de instructies Hallo in Hallo artikel [hoe toolink VNets tooExpressRoute circuits](expressroute-howto-linkvnet-classic.md).

## <a name="config"></a>Een bestaande klassieke VNet configureren voor ExpressRoute
Als u al een klassiek VNet hebt, kunt u deze tooconnect tooExpressRoute configureren in de klassieke portal Hallo. Hallo-instellingen zijn Hallo dezelfde als Hallo hierboven, zodat lezen via deze secties toobecome bekend bent met de Hallo instellingen vereist. Als u toocreate een naast elkaar bestaande ExpressRoute/Site-naar-Site-verbinding wilt, Zie [in dit artikel](expressroute-howto-coexist-classic.md) voor Hallo stappen. Ze zijn anders dan Hallo in dit artikel stappen.

1. U moet toocreate Hallo lokale netwerk voordat u Hallo rest van uw VNet-instellingen bijwerken. Klik op toocreate een nieuw lokaal netwerk dat is vereist bij het configureren van ExpressRoute via de klassieke portal hello, **nieuw**  **>**  **netwerkservices**  **>**  **Virtueel netwerk**  **>**  **toevoegen lokale netwerk**. Ga als volgt Hallo wizard stappen toocreate Hallo lokale netwerk.
2. Gebruik **configureren** pagina tooupdate Hallo rest Hallo-instellingen voor uw VNet en tooassociate hello VNet toohello lokale netwerk.
3. Ga na het configureren van instellingen voor Hallo toohello [Hallo-gateway maken](#gw) sectie van dit artikel toocreate Hallo-gateway.

## <a name="next-steps"></a>Volgende stappen
* Als u tooadd virtuele machines tooyour virtueel netwerk wilt, Zie [virtuele Machines leertrajecten](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/).
* Als u meer informatie over ExpressRoute toolearn wilt, raadpleegt u Hallo [overzicht van ExpressRoute](expressroute-introduction.md).

