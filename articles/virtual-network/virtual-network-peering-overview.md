---
title: aaaAzure virtueel netwerk peering | Microsoft Docs
description: Meer informatie over peering in virtuele netwerken in Azure.
services: virtual-network
documentationcenter: na
author: NarayanAnnamalai
manager: jefco
editor: tysonn
ms.assetid: eb0ba07d-5fee-4db0-b1cb-a569b7060d2a
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: narayan
ms.openlocfilehash: 46a14b416a7d4389f79a3cd7c55e388b5d312577
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network-peering"></a>Peering op virtueel netwerk
Virtueel netwerk peering kunt u tooconnect twee virtuele netwerken in dezelfde regio via Hallo hello Azure-backbone-netwerk. Als peer is ingesteld, wordt Hallo twee virtuele netwerken weergegeven als een voor connectiviteit doeleinden. Hallo twee virtuele netwerken nog steeds als afzonderlijke resources worden beheerd, maar de virtuele machines in Hallo brengen virtuele netwerken kunnen met elkaar communiceren rechtstreeks met behulp van privé IP-adressen.

Hallo-verkeer tussen virtuele machines in Hallo brengen virtuele netwerken doorgestuurd via de Azure-infrastructuur, dezelfde manier als verkeer wordt gerouteerd tussen virtuele machines in Hallo Hallo hetzelfde virtuele netwerk. Enkele voordelen van het gebruik van virtueel netwerk peering Hallo:

* Een verbinding met lage latentie en hoge bandbreedte tussen resources in verschillende virtuele netwerken.
* Hallo mogelijkheid toouse bronnen zoals netwerkapparaten en VPN-gateways als onderweg punten in een peered virtueel netwerk.
* Hallo mogelijkheid toopeer twee virtuele netwerken die zijn gemaakt via Azure Resource Manager-implementatiemodel Hallo of toopeer één virtueel netwerk zijn gemaakt via Resource Manager tooa virtueel netwerk via de klassieke implementatiemodel Hallo is gemaakt. Lees Hallo [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel toolearn meer over Hallo verschillen tussen de twee hello Azure-implementatiemodellen.

## <a name="requirements-constraints"></a>Vereisten en beperkingen

* Hallo virtuele netwerken brengen moeten aanwezig zijn in Hallo dezelfde Azure-regio. U kunt virtuele netwerken in verschillende Azure-regio's verbinden met een [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V).
* Hallo moet virtuele netwerken brengen niet-overlappende IP-adresruimten.
* Adresruimten kunnen niet worden toegevoegd aan of verwijderd uit een virtueel netwerk wanneer een virtueel netwerk is gekoppeld aan een ander virtueel netwerk.
* Peering in virtuele netwerken vindt plaats tussen twee virtuele netwerken. Er is geen afgeleide transitieve relatie tussen peerings. Bijvoorbeeld, als virtualNetworkA virtualNetworkB is gekoppeld en virtualNetworkB virtualNetworkC is gekoppeld, virtualNetworkA is *niet* toovirtualNetworkC peer is ingesteld.
* U kunt virtuele netwerken die bestaan uit twee verschillende abonnementen, als lang een bevoegde gebruiker peer (Zie [specifieke machtigingen](create-peering-different-deployment-models-subscriptions.md#permissions)) van beide abonnementen toestaat Hallo peering en Hallo-abonnementen worden gekoppeld toohello dezelfde Azure Active Directory-tenant. U kunt een [VPN-Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect virtuele netwerken in abonnementen die zijn gekoppeld toodifferent Active Directory-tenants.
* Virtuele netwerken kunnen peer worden ingesteld als beide via Hallo Resource Manager-implementatiemodel zijn gemaakt of als één virtueel netwerk is gemaakt via Hallo Resource Manager-implementatiemodel en Hallo andere is gemaakt via de klassieke implementatiemodel Hallo. Twee virtuele netwerken die zijn gemaakt via de klassieke implementatiemodel Hallo kunnen brengen tooeach, andere, echter niet. U kunt een [VPN-Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect twee virtuele netwerken via de klassieke implementatiemodel Hallo is gemaakt.
* Hoewel het Hallo-communicatie tussen virtuele machines in virtuele netwerken brengen heeft geen beperkingen extra bandbreedte, is er een maximale netwerkbandbreedte, afhankelijk van de grootte van de virtuele machine Hallo die nog steeds van toepassing is. meer informatie over maximale netwerkbandbreedte voor andere virtuele machine-groottes lezen Hallo toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikelen de grootte van virtuele machine.
* Door Azure verschafte interne DNS-naamomzetting voor virtuele machines werkt niet in gekoppelde virtuele netwerken. Virtuele machines hebben interne DNS-namen die omgezet alleen binnen Hallo lokale virtuele netwerk zijn. U kunt wel virtuele netwerken van virtuele machines verbonden toopeered als DNS-servers voor een virtueel netwerk configureren. Voor meer informatie lezen Hallo [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) artikel.

![Eenvoudige peering van virtuele netwerken](./media/virtual-networks-peering-overview/figure01.png)

## <a name="connectivity"></a>Connectiviteit
Na twee virtuele netwerken brengen, resources in een virtueel netwerk kunnen rechtstreeks verbinding maken met resources in het virtuele netwerk Hallo peer is ingesteld. Hallo twee virtuele netwerken hebben volledige IP-niveau connectiviteit.

Hallo netwerklatentie voor een round trip tussen twee virtuele machines in virtuele netwerken brengen is Hallo dezelfde als voor een round trip binnen één virtueel netwerk. Hallo netwerkdoorvoer is gebaseerd op Hallo-bandbreedte die toegestaan voor Hallo virtuele machine, evenredig tooits grootte. Er is niet meer beperkingen gelden voor bandbreedte binnen het Hallo-peering.

Hallo-verkeer tussen virtuele machines in virtuele netwerken brengen doorgestuurd rechtstreeks via hello Azure back-end-infrastructuur, niet via een gateway.

Virtueel netwerk van virtuele machines verbonden tooa hebben toegang tot Hallo interne taakverdeling eindpunten in het virtuele netwerk Hallo peer is ingesteld. Netwerkbeveiligingsgroepen kunnen worden toegepast in een virtueel netwerk tooblock toegang tooother virtuele netwerken of subnetten, indien gewenst.

Bij het configureren van virtueel netwerk peering, kunt u openen of sluiten Hallo-netwerkbeveiligingsgroepen tussen Hallo virtuele netwerken. Als u volledige connectiviteit tussen brengen virtuele netwerken (dit is de standaardoptie Hallo) opent, kunt u network security groepen toospecific subnetten of virtuele machines tooblock toepassen of specifieke toegang weigeren. Hallo toolearn informatie over netwerkbeveiligingsgroepen, lezen [netwerk beveiligingsgroepen overzicht](virtual-networks-nsg.md) artikel.

## <a name="service-chaining"></a>Servicechaining
U kunt configureren gebruiker gedefinieerde routes die punt toovirtual-machines in virtuele netwerken brengen Hallo 'volgende hop' IP-adres tooenable service-koppeling. Service-koppeling kunt u toodirect verkeer van een virtueel netwerk tooa virtueel apparaat in een peered virtueel netwerk via de gebruiker gedefinieerde routes.

U kunt ook effectief opbouwen type hub en spoke-omgevingen, waar Hallo hub onderdelen van de infrastructuur zoals een virtueel netwerkapparaat kan hosten. Alle Hallo spoke virtuele netwerken kunnen vervolgens peer met Hallo hub virtueel netwerk. Door virtuele netwerkapparaten die worden uitgevoerd in het virtuele netwerk van Hallo hub kan verkeer stromen. Kortom, kan virtuele netwerk peering Hallo volgende hop IP-adres op Hallo gebruiker gedefinieerde route toobe Hallo IP-adres van een virtuele machine in het virtuele netwerk Hallo peer is ingesteld. meer informatie over de gebruiker gedefinieerde routes, Hallo lezen toolearn [overzicht van de gebruiker gedefinieerde routes](virtual-networks-udr-overview.md) artikel.

## <a name="gateways-and-on-premises-connectivity"></a>Gateways en on-premises connectiviteit
Elk virtueel netwerk, ongeacht of u deze kunt met een ander virtueel netwerk brengen kunt nog steeds een eigen gateway en deze tooconnect tooan on-premises netwerk gebruiken. U kunt ook configureren [verbindingen virtueel netwerk-naar-virtueel netwerk](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json) met behulp van gateways, ondanks dat de virtuele netwerken Hallo brengen.

Wanneer beide opties voor interconnectiviteit virtueel netwerk zijn geconfigureerd, Hallo-verkeer tussen virtuele netwerken van Hallo loopt via de peeringconfiguratie Hallo (dat wil zeggen, via hello Azure-backbone).

Wanneer virtuele netwerken brengen, kunt u ook Hallo gateway configureren in het virtuele netwerk Hallo peer is ingesteld als een doorvoer punt tooan on-premises netwerk. Hallo virtueel netwerk dat van een externe gateway gebruikmaakt kan niet in dit geval een eigen gateway hebben. Een virtueel netwerk kan slechts één gateway hebben. Hallo-gateway kan een lokale of externe gateway zijn (in Hallo brengen virtueel netwerk), zoals wordt weergegeven in de volgende afbeelding Hallo:

![Doorvoer VNet-peering](./media/virtual-networks-peering-overview/figure02.png)

Gateway-doorvoer wordt niet ondersteund in Hallo peering relatie tussen virtuele netwerken die zijn gemaakt via verschillende implementatiemodellen. Beide virtuele netwerken in de peering Hallo-relatie moeten zijn gemaakt via Resource Manager voor een gateway onderweg toowork.

Wanneer Hallo virtuele netwerken die een enkele Azure ExpressRoute-verbinding delen brengen, Hallo-verkeer tussen hen Hallo peering relatie doorloopt (dat wil zeggen, via hello Azure-backbone-netwerk). U kunt nog steeds lokale gateways in elk virtueel netwerk tooconnect toohello lokale circuit. U kunt ook een gedeelde gateway gebruiken en de doorvoer voor on-premises connectiviteit configureren.

## <a name="provisioning"></a>Inrichten
Virtueel netwerk-peering is een bevoegde bewerking. Er is een afzonderlijke functie onder Hallo VirtualNetworks naamruimte. Een gebruiker kan worden toegewezen aan de specifieke rechten tooauthorize peering. Een gebruiker met lees-/ schrijftoegang toohello virtueel netwerk overgenomen automatisch deze rechten.

Een gebruiker die ofwel een beheerder is of een bevoorrechte gebruiker van de peering mogelijkheid Hallo kan initiëren voor een peering-bewerking op een ander virtueel netwerk. Als er een overeenkomende aanvraag voor peering op de andere kant Hallo en als andere vereisten wordt voldaan, Hallo peer wordt ingesteld.

## <a name="limits"></a>Limieten
Er gelden beperkingen op Hallo aantal peerings die zijn toegestaan voor één virtueel netwerk. Raadpleeg voor meer informatie, Hallo [Azure netwerken limieten](../azure-subscription-service-limits.md#networking-limits).

## <a name="pricing"></a>Prijzen
Er wordt een nominaal bedrag in rekening gebracht voor inkomend en uitgaand verkeer dat gebruikmaakt van een virtueel netwerk-peering. Zie voor meer informatie, Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/virtual-network).

## <a name="next-steps"></a>Volgende stappen

* Voltooi een zelfstudie voor peering in virtuele netwerken. Een virtueel netwerk peering wordt gemaakt tussen virtuele netwerken die zijn gemaakt via Hallo dezelfde of verschillende implementatiemodellen die aanwezig zijn in dezelfde of verschillende abonnementen Hallo. Een zelfstudie voor een van de volgende scenario's Hallo voltooien:
 
    |Azure-implementatiemodel  | Abonnement  |
    |---------|---------|
    |Beide in Resource Manager |[Hetzelfde](virtual-network-create-peering.md)|
    | |[Verschillend](create-peering-different-subscriptions.md)|
    |Eén in Resource Manager, één klassiek     |[Hetzelfde](create-peering-different-deployment-models.md)|
    | |[Verschillend](create-peering-different-deployment-models-subscriptions.md)|

* Meer informatie over hoe toocreate een [hub en spoke-netwerktopologie](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
* Meer informatie over alle [peering instellingen voor virtueel netwerk en hoe toochange ze](virtual-network-manage-peering.md)
