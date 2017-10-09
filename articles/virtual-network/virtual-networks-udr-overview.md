---
title: aaaUser gedefinieerde routes en doorsturen via IP in Azure | Microsoft Docs
description: Meer informatie over hoe tooconfigure gebruiker gedefinieerde routes (UDR) en tooforward doorsturen via IP-verkeer toonetwork virtuele apparaten in Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: c39076c4-11b7-4b46-a904-817503c4b486
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f1f1d46166d5a7c776f472b7ade1354d943ece10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-routes-and-ip-forwarding"></a>Door de gebruiker gedefinieerde routes en doorsturen via IP

Als u virtuele machines (VM's) tooa virtueel netwerk (VNet) in Azure toevoegt, ziet u dat Hallo virtuele machines kunnen toocommunicate met elkaar via Hallo netwerk, automatisch worden. U hoeft niet toospecify een gateway, ondanks het feit Hallo virtuele machines in verschillende subnetten. Hallo geldt ook voor communicatie vanaf Hallo VMs toohello Internet en zelfs tooyour on-premises netwerk wanneer u een hybride verbinding is tussen Azure tooyour eigenaar datacenter aanwezig is.

Deze communicatiestroom is mogelijk omdat een reeks system routes toodefine hoe IP-verkeersstromen maakt gebruik van Azure. Systeemroutes bepalen de communicatiestroom Hallo in Hallo volgen scenario's:

* Hallo van binnen hetzelfde subnet.
* Van een subnet tooanother binnen een VNet.
* Van virtuele machines toohello Internet.
* Van een VNet tooanother VNet via een VPN-gateway.
* Van een VNet tooanother VNet via VNet-Peering (Service-koppeling).
* Van een VNet tooyour on-premises netwerk via een VPN-gateway.

Hallo-afbeelding hieronder ziet u eenvoudige configuratie met een VNet, twee subnetten en enkele virtuele machines, plus Hallo systeemroutes waarmee IP-verkeer tooflow.

![Systeemroutes in Azure](./media/virtual-networks-udr-overview/Figure1.png)

Hoewel Hallo gebruik van systeemroutes verkeer automatisch voor uw implementatie vereenvoudigt, zijn er ook gevallen waarin u wilt toocontrol Hallo routering van pakketten via een virtueel apparaat. U kunt dus door gebruiker gedefinieerde routes maken opgeeft Hallo volgende hop voor pakketten tooa specifiek subnet toogo tooyour virtueel apparaat in plaats daarvan en inschakelen, IP Hallo doorsturen voor virtuele machine wordt uitgevoerd als Hallo virtueel apparaat.

Hallo afbeelding hieronder toont een voorbeeld van de gebruiker gedefinieerde routes en tooforce pakketten doorsturen via IP tooone subnet van een andere toogo via een virtueel apparaat op een derde subnet worden verzonden.

![Systeemroutes in Azure](./media/virtual-networks-udr-overview/Figure2.png)

> [!IMPORTANT]
> Gebruiker gedefinieerde routes worden toegepaste tootraffic zonder een subnet van een bron (zoals netwerkinterfaces gekoppeld tooVMs) in Hallo subnet. U kunt geen routes toospecify maken hoe verkeer krijgt een subnet vanaf Internet, Hallo voor exemplaar. Hallo toestel u verkeer toocannot doorstuurt liggen Hallo hetzelfde subnet waar Hallo verkeer afkomstig is. Maak altijd een apart subnet voor uw apparaten. 
> 
> 

## <a name="route-resource"></a>Bron routeren
Pakketten worden gerouteerd via een TCP/IP-netwerk op basis van een routetabel die op elk knooppunt in het fysieke netwerk Hallo gedefinieerd. Een routetabel is dat een verzameling van afzonderlijke routes gebruikt toodecide waar tooforward pakketten op basis van Hallo doel-IP-adres. Een route bestaat uit Hallo volgende:

| Eigenschap | Beschrijving | Beperkingen | Overwegingen |
| --- | --- | --- | --- |
| Adresvoorvoegsel |Hallo doel-CIDR toowhich Hallo route van toepassing, zoals 10.1.0.0/16. |Moet een geldig CIDR-bereik van adressen op Hallo openbare Internet, virtuele Azure-netwerk of on-premises datacentrum. |Zorg ervoor dat Hallo **adresvoorvoegsel** bevat geen Hallo-adres voor Hallo **adres van volgende hop**, anders treedt de pakketten in een lus van Hallo bron toohello volgende hop zonder ooit bereikt Hallo bestemming. |
| Volgend hoptype |Hallo type hop in Azure waarnaar Hallo pakket moet worden verzonden naar. |Moet een Hallo volgende waarden: <br/> **Virtueel netwerk**. Hallo lokale virtuele netwerk vertegenwoordigt. Bijvoorbeeld, hebt u twee subnetten, 10.1.0.0/16 en 10.2.0.0/16 in hetzelfde virtuele netwerk Hallo, Hallo route voor elk subnet in de routetabel Hallo heeft een volgende hop-waarde van *virtueel netwerk*. <br/> **Gateway voor een virtueel netwerk**. Hiermee geeft u een Azure S2S VPN-gateway op. <br/> **Internet**. Hiermee geeft u Hallo standaard internetgateway van hello Azure-infrastructuur. <br/> **Virtueel apparaat**. Hiermee geeft u een virtueel apparaat dat u hebt toegevoegd tooyour virtuele Azure-netwerk. <br/> **Geen**. Hiermee geeft u een black hole op. Pakketten die zijn doorgestuurd tooa black hole worden helemaal niet doorgestuurd. |Overweeg het gebruik van **virtueel apparaat** toodirect verkeer tooa VM of Azure Load Balancer interne IP-adres.  Dit type kunnen Hallo-specificatie van een IP-adres zoals hieronder wordt beschreven. Overweeg het gebruik van een **geen** Typ toostop pakketten van stromende tooa opgegeven bestemming. |
| Adres van de volgende hop |adres van volgende hop Hallo bevat Hallo IP-adres waarnaar pakketten moeten worden doorgestuurd naar. Volgende hopwaarden zijn alleen toegestaan in routes waar het volgende hoptype Hallo is *virtueel apparaat*. |Moet een IP-adres dat bereikbaar is binnen Hallo virtueel netwerk waarin Hallo door de gebruiker gedefinieerde Route is toegepast, zonder tussenkomst van een **virtuele netwerkgateway**. Hallo IP-adres heeft toobe op Hallo hetzelfde virtuele netwerk wanneer deze wordt toegepast, of op een peered virtueel netwerk. |Als Hallo IP-adres een VM vertegenwoordigt, controleert u of u inschakelen [doorsturen via IP](#IP-forwarding) in Azure voor Hallo VM. Als hello IP-adres vertegenwoordigt Hallo interne IP-adres van Azure Load Balancer, controleert u of er een overeenkomende taakverdelingsregel voor elke poort wilt tooload verdelen.|

Enkele waarden voor 'NextHopType' hello hebben verschillende namen in Azure PowerShell:

* Virtueel netwerk is VnetLocal
* De gateway van het virtuele netwerk is VirtualNetworkGateway
* Het virtuele apparaat is VirtualAppliance
* Internet is Internet
* Geen is Geen

### <a name="system-routes"></a>Systeemroutes
Elk subnet dat is gemaakt in een virtueel netwerk is automatisch gekoppeld aan een routetabel met Hallo volgende systeemrouteregels:

* **Lokale VNnet-regel**: deze regel wordt automatisch gemaakt voor elk subnet in een virtueel netwerk. Dit geeft aan dat er een directe koppeling tussen VM's Hallo in Hallo VNet en er zonder tussenliggende volgende hop is.
* **On-premises regel**: met deze regel van toepassing is tooall verkeer dat is bestemd toohello lokale-adresbereik en maakt gebruik van VPN-gateway als bestemming voor volgende hop Hallo.
* **Regel voor Internet**: deze regel wordt toegepast op alle verkeer dat is bestemd toohello Internet (adres voorvoegsel 0.0.0.0/0) en maakt gebruik van Hallo infrastructuur internet-gateway als Hallo van volgende hop voor alle verkeer dat is bestemd toohello Internet.

### <a name="user-defined-routes"></a>Door de gebruiker gedefinieerde routes
Voor de meeste omgevingen moet u alleen Hallo systeemroutes al zijn gedefinieerd door Azure. U kunt echter een routetabel toocreate moet en toevoegen van een of meer routes in bepaalde gevallen, zoals:

* Geforceerde tunneling toohello Internet via uw on-premises netwerk.
* Gebruik van virtuele apparaten in uw Azure-omgeving.

In bovenstaande Hallo gevallen moet u toocreate een routetabel en door de gebruiker gedefinieerde routes tooit toevoegen. U kunt meerdere routetabellen hebben en hello dezelfde routetabel kan worden gekoppeld tooone of meer subnetten. En elk subnet kan alleen worden gekoppeld tooa één routetabel. Alle virtuele machines en cloudservices in een subnet gebruik Hallo route tabel die is gekoppeld toothat subnet.

Subnetten zijn afhankelijk van systeemroutes totdat een routetabel gekoppeld toohello subnet is. Zodra een dergelijke koppeling bestaat, vindt routering plaats op basis van het LPM (Longest Prefix Match, langste overeenkomende voorvoegsel) van door de gebruiker gedefinieerde routes en systeemroutes. Als er is meer dan één route met Hallo dezelfde LPM overeenkomen en vervolgens een route geselecteerd op basis van de oorsprong in Hallo volgorde:

1. Door de gebruiker gedefinieerde route
2. BGP-route (wanneer u ExpressRoute gebruikt)
3. Systeemroute

toolearn hoe toocreate door de gebruiker gedefinieerde routes, Zie [hoe tooCreate Routes en doorsturen via IP in Azure inschakelen](virtual-network-create-udr-arm-template.md).

> [!IMPORTANT]
> De gebruiker gedefinieerde routes worden alleen toegepast tooAzure VM's en cloudservices. Bijvoorbeeld als u wilt dat een virtueel apparaat van de firewall tussen uw on-premises netwerk en Azure tooadd, hebt u toocreate een door de gebruiker gedefinieerde route voor uw Azure-routetabellen waarmee alle verkeer toohello lokaal adresruimte toohello virtuele gaan worden doorgestuurd apparaat. U kunt ook een gebruiker gedefinieerde route (UDR) toohello GatewaySubnet tooforward al het verkeer van de lokale tooAzure via Hallo virtueel apparaat toevoegen. Dit is een recente toevoeging.
> 
> 

### <a name="bgp-routes"></a>BGP-routes
Als u een ExpressRoute-verbinding tussen uw on-premises netwerk en Azure hebt, kunt u BGP-routes voor toopropagate kunt inschakelen via de tooAzure van uw lokale netwerk. Deze BGP-routes worden gebruikt in Hallo dezelfde manier als systeemroutes en de gebruiker gedefinieerde routes in elk Azure-subnet. Zie [Inleiding tot ExpressRoute](../expressroute/expressroute-introduction.md) voor meer informatie.

> [!IMPORTANT]
> U kunt uw Azure-omgeving toouse force tunneling via uw on-premises netwerk door het maken van een gebruiker gedefinieerde route voor subnet 0.0.0.0/0 die gebruikmaakt van Hallo VPN-gateway als de volgende hop Hallo configureren. Dit werkt alleen als u een VPN-gateway gebruikt en niet ExpressRoute. Voor ExpressRoute wordt geforceerde tunneling geconfigureerd via BGP.
> 
> 

## <a name="ip-forwarding"></a>Doorsturen via IP
Zoals hierboven beschreven, een Hallo hoofdredenen toocreate is een door de gebruiker gedefinieerde route tooforward verkeer tooa virtueel apparaat. Een virtueel apparaat is niets meer dan een virtuele machine die een toepassing die wordt gebruikt toohandle-netwerkverkeer in een bepaalde manier, zoals een firewall of een NAT-apparaat wordt uitgevoerd.

Deze virtueel apparaat die VM kunnen tooreceive inkomend verkeer die moet worden verholpen niet tooitself. een VM-verkeer tooreceive tooallow geadresseerd tooother bestemmingen, u moet voor Hallo VM doorsturen via IP inschakelen. Dit is een Azure-instelling, niet een instelling in het gastbesturingssysteem Hallo.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[routes maakt in de Resource Manager-implementatiemodel Hallo](virtual-network-create-udr-arm-template.md) en deze toosubnets koppelt. 
* Meer informatie over hoe te[routes maakt in het klassieke implementatiemodel Hallo](virtual-network-create-udr-classic-ps.md) en deze toosubnets koppelt.

