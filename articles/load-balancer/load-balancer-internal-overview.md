---
title: aaaInternal load balancer overzicht | Microsoft Docs
description: Overzicht voor de interne load balancer en de bijbehorende functies. De werking van een load balancer voor Azure en mogelijke scenario's tooconfigure interne eindpunten
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a>Interne load balancer-overzicht

In tegenstelling tot Hallo Internet gerichte load balancer Hallo interne load balancer (ILB) zorgt ervoor dat alleen tooresources verkeer binnen het Hallo-cloudservice of met behulp van VPN-tooaccess hello Azure-infrastructuur. Hallo infrastructuur beperkt toegang toohello taakverdeling virtuele IP-adressen (VIP's) van een Cloudservice of een virtueel netwerk, zodat ze kunnen niet rechtstreeks blootgesteld tooan Internet eindpunt. Dit kan interne line-of-business (LOB)-toepassingen toorun in Azure en is toegankelijk vanuit binnen Hallo cloud of bronnen on-premises.

## <a name="why-you-may-need-an-internal-load-balancer"></a>Waarom moet u mogelijk een interne load balancer

Azure interne Load Balancing (ILB) zorgt voor taakverdeling tussen virtuele machines die zich in een cloudservice of een virtueel netwerk met een regionaal bereik bevinden. Zie voor meer informatie over het Hallo-gebruik en de configuratie van virtuele netwerken met een regionaal bereik [regionale virtuele netwerken](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello Azure-blog. Bestaande virtuele netwerken die zijn geconfigureerd voor een affiniteitsgroep kunnen ILB niet gebruiken.

ILB kunt Hallo typen taakverdeling te volgen:

* Binnen een cloudservice van virtuele machines tooa set van virtuele machines die zich binnen een Hallo dezelfde cloudservice (Zie afbeelding 1).
* Binnen een virtueel netwerk van virtuele machines in Hallo virtueel netwerk tooa set virtuele machines die zich binnen een Hallo dezelfde cloudservice Hallo virtuele netwerk (Zie afbeelding 2).
* Voor een virtueel netwerk cross-premises van lokale computers tooa set van virtuele machines die zich binnen een Hallo dezelfde cloudservice Hallo virtuele netwerk (Zie afbeelding 3).
* Internetgerichte toepassingen met meerdere lagen waarin Hallo back-end lagen zijn niet verbonden met Internet, maar is taakverdeling voor verkeer van Hallo internetgerichte tier.
* Taakverdeling van LOB-toepassingen die zijn gehost in Azure, zonder dat extra load balancer-hardware of software. Met inbegrip van lokale servers in Hallo set computers waarvan het verkeer is de belasting van taakverdeling.

## <a name="internet-facing-multi-tier-applications"></a>Internetgericht toepassingen met meerdere lagen

Hallo weblaag internetgerichte eindpunten voor Internet-clients heeft en deel uitmaakt van een set met gelijke taakverdeling. Hallo-taakverdeling inkomend verkeer van de webserver en webclients voor TCP-poort 443 (HTTPS) toohello webservers.

Hallo databaseservers zich achter een ILB-eindpunt dat Hallo-webservers voor de opslag gebruikt. Deze database-service met gelijke taakverdeling eindpunt, welk verkeer gelijkmatig verdeeld zijn over Hallo databaseservers in Hallo ILB set is.

Hallo volgende afbeelding toont Hallo Internetgericht toepassing met meerdere lagen binnen Hallo dezelfde cloudservice.

![Interne load balancing één cloudservice](./media/load-balancer-internal-overview/IC736321.png)

Afbeelding 1: Internetgericht toepassing met meerdere lagen

Ook gebruiken voor een toepassing met meerdere lagen is wanneer Hallo ILB geïmplementeerd tooa andere cloudservice dan één consumerende Hallo-service voor Hallo ILB Hallo.

Cloud services met behulp van Hallo hetzelfde virtuele netwerk hebben toegang tot toohello ILB-eindpunt. Hallo de volgende afbeelding ziet u front-endwebservers in een andere cloudservice vanuit Hallo database back-end zijn en het gebruik van Hallo ILB-eindpunt in Hallo hetzelfde virtuele netwerk.

![Interne taakverdeling tussen cloudservices](./media/load-balancer-internal-overview/IC744147.png)

Afbeelding 2 - front-servers in een andere cloud-service

## <a name="intranet-line-of-business-applications"></a>Intranet line-of-business-toepassingen

Verkeer van clients op Hallo on-premises netwerk ophalen taakverdeling op Hallo set van LOB-servers met behulp van VPN-verbinding tooAzure netwerk.

Hallo-clientcomputer heeft toegang tooan IP-adres uit Azure VPN-service via de VPN-punt toosite. Kunt u Hallo gebruik Hallo LOB-toepassing die wordt gehost achter Hallo ILB-eindpunt.

![Interne load balancing via punt toosite VPN](./media/load-balancer-internal-overview/IC744148.png)

Afbeelding 3 - LOB-toepassingen die worden gehost achter Hallo LB-eindpunt

Een ander scenario voor Hallo LOB is toohave toosite VPN-toohello virtueel netwerk met een site waarop Hallo ILB-eindpunt is geconfigureerd. Hiermee worden lokale netwerkverkeer gerouteerd toobe toohello ILB-eindpunt.

![Interne taakverdeling met behulp van site toosite VPN](./media/load-balancer-internal-overview/IC744150.png)

Afbeelding 4 - On-premises netwerkverkeer gerouteerd toohello ILB-eindpunt

## <a name="limitations"></a>Beperkingen

Interne Load Balancer-configuraties ondersteunen geen snat omzetten. In de context van de Hallo van dit document verwijst snat omzetten tooport onechte bron netwerkadresomzetting.  Dit geldt tooscenarios waarin een virtuele machine in een load balancer-pool tooreach Hallo respectieve interne Load Balancer frontend-IP-adres moet. Dit scenario wordt niet ondersteund voor de interne Load Balancer. Verbindingsfouten uitgevoerd wanneer het Hallo-stroom taakverdeling toohello VM Hallo stroom afkomstig is. U moet een proxy stijl load balancer gebruiken voor dergelijke scenario's.

## <a name="next-steps"></a>Volgende stappen

[Ondersteuning voor Azure Load Balancer van Azure Resource Manager](load-balancer-arm.md)

[De load balancer van een Internetgericht configureren aan de slag](load-balancer-get-started-internet-arm-ps.md)

[Een interne load balancer configureren aan de slag](load-balancer-get-started-ilb-arm-ps.md)

[Een distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)
