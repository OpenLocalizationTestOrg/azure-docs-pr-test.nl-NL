---
title: 'Toevoegen van een virtueel netwerk gateway tooa VNet voor ExpressRoute: Portal: Azure | Microsoft Docs'
description: Dit artikel begeleidt u bij het toevoegen van een virtueel netwerk gateway tooan al gemaakt Resource Manager VNet voor ExpressRoute.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: cherylmc
ms.openlocfilehash: 9e922af1f3676eeebc569b57c3ae3a22d4e0b395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-hello-azure-portal"></a>Configureren van een virtuele netwerkgateway voor ExpressRoute met hello Azure-portal
> [!div class="op_single_selector"]
> * [Resource Manager - Azure Portal](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Klassieke - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - Azure-portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Dit artikel begeleidt u bij Hallo stappen tooadd een virtuele netwerkgateway voor een bestaande VNet. Dit artikel begeleidt u bij Hallo stappen tooadd, vergroten of verkleinen en de gateway van een virtueel netwerk (VNet) verwijderen voor een bestaande VNet. Hallo-stappen voor deze configuratie zijn specifiek voor VNets die zijn gemaakt met behulp van Hallo Resource Manager-implementatiemodel dat wordt gebruikt in een ExpressRoute-configuratie. Zie voor meer informatie over virtuele netwerkgateways en configuratie-instellingen voor ExpressRoute gateway [over virtuele netwerkgateways voor ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Voordat u begint

stappen voor deze taak gebruik een VNet Hallo gebaseerd op Hallo waarden in Hallo configuratielijst verwijzing te volgen. We gebruiken deze lijst in onze voorbeelden van stappen. U kunt Hallo lijst toouse kopiëren als een verwijzing, waarbij Hallo waarden vervangt door uw eigen.

**Lijst van configuratie-verwijzing**

* Virtuele-netwerknaam = "TestVNet"
* Virtuele adresruimte van het netwerk 192.168.0.0/16 =
* Subnetnaam = 'FrontEnd' 
    * Subnetadresruimte = '192.168.1.0/24'
* Resourcegroep = "TestRG"
* Locatie = 'VS-Oost'
* De naam van de gateway-Subnet: 'GatewaySubnet' u moet altijd een gatewaysubnet de naam *GatewaySubnet*.
    * Gateway-Subnet-adresruimte = "192.168.200.0/26"
* Gatewaynaam = 'ERGW'
* De naam van de IP-gateway = "MyERGWVIP"
* Gatewaytype = "ExpressRoute" dit type is vereist voor een ExpressRoute-configuratie.
* De naam van de gateway-openbare IP-adres = "MyERGWVIP"

U ziet een [Video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network) van de volgende stappen voordat u begint met de configuratie.

## <a name="create-hello-gateway-subnet"></a>Hallo gatewaysubnet maken

1. In Hallo [portal](http://portal.azure.com), toohello Resource Manager virtueel netwerk waarvoor u een virtuele netwerkgateway toocreate wilt navigeren.
2. In Hallo **instellingen** sectie van de blade van het VNet, klikt u op **subnetten** blade tooexpand Hallo-subnetten.
3. Op Hallo **subnetten** blade, klikt u op **+ gatewaysubnet** tooopen hello **subnet toevoegen** blade. 
   
    ![Hallo gatewaysubnet toevoegen](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "hello gatewaysubnet toevoegen")


4. Hallo **naam** voor uw subnet wordt automatisch gevuld met Hallo waarde 'GatewaySubnet'. Deze waarde is vereist om Azure toorecognize Hallo subnet als het Hallo-gateway-subnet. Hallo automatisch gevulde aanpassen **-adresbereik** waarden toomatch uw configuratievereisten. Het is raadzaam een gatewaysubnet maken met een/27 of groter (/ 26/25 enz.). Klik vervolgens op **OK** toosave Hallo waarden en Hallo gatewaysubnet maken.

    ![Hallo subnet toevoegen](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "Hallo subnet toevoegen")

## <a name="create-hello-virtual-network-gateway"></a>Hallo virtuele netwerkgateway maken

1. Klik in de portal Hallo aan de linkerkant hello, op  **+**  en typ 'Virtuele netwerkgateway' in de zoekopdracht. Zoek **virtuele netwerkgateway** in Hallo zoeken retourneren en klikt u op Hallo vermelding. Op Hallo **virtuele netwerkgateway** blade, klikt u op **maken** Hallo Hallo blade onderaan in. Hiermee opent u Hallo **virtuele netwerkgateway aanmaken** blade.
2. Op Hallo **virtuele netwerkgateway aanmaken** blade invullen Hallo waarden voor uw virtuele netwerkgateway.

    ![Velden van de blade Gateway van het virtuele netwerk maken](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "Velden van de blade Gateway van het virtuele netwerk maken")
3. **Naam**: naam van uw gateway. Dit is niet gelijk aan de naamgeving van een gatewaysubnet Hallo. Het Hallo-naam van Hallo gateway-object maken van de.
4. **Gatewaytype**: Selecteer **ExpressRoute**.
5. **SKU**: Selecteer Hallo gateway-SKU uit Hallo vervolgkeuzelijst.
6. **Locatie**: Hallo aanpassen **locatie** veld toopoint toohello locatie van het virtuele netwerk. Als Hallo locatie niet toohello regio waar uw virtuele netwerk is opgeslagen verwijst, weergegeven niet virtueel netwerk Hallo Hallo 'Kies een virtueel netwerk' vervolgkeuzelijst.
7. Kies Hallo virtueel netwerk toowhich gewenste tooadd deze gateway. Klik op **virtueel netwerk** tooopen hello **Kies een virtueel netwerk** blade. Selecteer Hallo VNet. Als u uw VNet niet ziet, zorg ervoor dat Hallo **locatie** veld wijst toohello regio waarin het virtuele netwerk bevindt.
9. Kies een openbaar IP-adres. Klik op **openbaar IP-adres** tooopen hello **openbare IP-adres kiezen** blade. Klik op **+ maken van nieuwe** tooopen hello **openbare IP-adres-blade maken**. Geef een naam op voor uw openbare IP-adres. Deze blade maakt een openbare object toowhich voor IP-adres die een openbaar IP-adres dynamisch wordt toegewezen. Klik op **OK** toosave uw wijzigingen toothis-blade.
10. **Abonnement**: Controleer of deze Hallo juiste abonnement is geselecteerd.
11. **Resourcegroep**: deze instelling wordt bepaald door Hallo virtuele netwerk dat u selecteert.
12. Hallo niet aanpassen **locatie** nadat u de vorige instellingen Hallo hebt opgegeven.
13. Hallo-instellingen te controleren. Als u wilt dat uw gateway tooappear op Hallo dashboard, kunt u **pincode toodashboard** Hallo Hallo blade onderaan in.
14. Klik op **maken** toobegin Hallo gateway te kunnen maken. Hallo-instellingen worden gevalideerd en Hallo gateway implementeert. Maken van de virtuele netwerkgateway kan duren too45 minuten toocomplete.

## <a name="next-steps"></a>Volgende stappen
Nadat u Hallo VNet gateway hebt gemaakt, kunt u uw VNet tooan ExpressRoute-circuit kunt koppelen. Zie [koppelen van een virtueel netwerk tooan ExpressRoute-circuit](expressroute-howto-linkvnet-portal-resource-manager.md).
