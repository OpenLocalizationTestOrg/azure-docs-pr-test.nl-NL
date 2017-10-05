---
title: Interne load balancer overzicht | Microsoft Docs
description: Overzicht voor de interne load balancer en de bijbehorende functies. De werking van een load balancer voor Azure en mogelijke scenario's voor het configureren van interne eindpunten
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
ms.openlocfilehash: d324aaf8ec2c8766d5cf11452158d14c19cba4d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="internal-load-balancer-overview"></a>Interne load balancer-overzicht

In tegenstelling tot het Internet gerichte load balancer, stuurt de interne load balancer (ILB) verkeer alleen bronnen in de cloudservice of via VPN voor toegang tot de Azure-infrastructuur. De infrastructuur de toegang beperkt tot de taakverdeling virtuele IP-adressen (VIP's) van een Cloudservice of een virtueel netwerk, zodat ze wordt nooit worden rechtstreeks blootgesteld aan een Internet-eindpunt. Dit kan interne line-of-business (LOB)-toepassingen voor uitvoeren in Azure en is toegankelijk vanuit de cloud of via lokale.

## <a name="why-you-may-need-an-internal-load-balancer"></a>Waarom moet u mogelijk een interne load balancer

Azure interne Load Balancing (ILB) zorgt voor taakverdeling tussen virtuele machines die zich in een cloudservice of een virtueel netwerk met een regionaal bereik bevinden. Zie voor meer informatie over het gebruik en de configuratie van virtuele netwerken met een regionaal bereik [regionale virtuele netwerken](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in de Azure-blog. Bestaande virtuele netwerken die zijn geconfigureerd voor een affiniteitsgroep kunnen ILB niet gebruiken.

ILB maakt gebruik van de volgende soorten taakverdeling:

* Binnen een cloudservice van virtuele machines naar een set van virtuele machines die zich in dezelfde cloudservice bevinden (Zie afbeelding 1).
* Binnen een virtueel netwerk van virtuele machines in het virtuele netwerk naar een set van virtuele machines die zich in dezelfde cloudservice van het virtuele bevinden netwerk (Zie afbeelding 2).
* Voor een virtueel netwerk cross-premises van lokale computers naar een set van virtuele machines die zich in dezelfde cloudservice van het virtuele bevinden netwerk (Zie afbeelding 3).
* Internetgerichte toepassingen met meerdere lagen waarin de back-end-lagen zijn niet verbonden met Internet, maar is taakverdeling voor verkeer van de internetgerichte tier.
* Taakverdeling van LOB-toepassingen die zijn gehost in Azure, zonder dat extra load balancer-hardware of software. Met inbegrip van lokale servers in de set van computers waarvan het verkeer is de belasting van taakverdeling.

## <a name="internet-facing-multi-tier-applications"></a>Internetgericht toepassingen met meerdere lagen

De weblaag internetgerichte eindpunten voor Internet-clients heeft en deel uitmaakt van een set met gelijke taakverdeling. De load balancer wordt binnenkomende verkeer van de webserver en webclients voor TCP-poort 443 (HTTPS) met de webservers.

De database-servers zich achter een ILB-eindpunt waarvan de webservers voor de opslag gebruikt. Deze database-service met gelijke taakverdeling eindpunt, welk verkeer gelijkmatig verdeeld over de databaseservers in de set ILB wordt.

De volgende afbeelding toont de Internetgericht toepassing met meerdere lagen in dezelfde cloudservice.

![Interne load balancing één cloudservice](./media/load-balancer-internal-overview/IC736321.png)

Afbeelding 1: Internetgericht toepassing met meerdere lagen

Ook gebruiken voor een toepassing met meerdere lagen is wanneer de ILB geïmplementeerd op een andere cloudservice dan het gebruiken van de service voor de ILB.

Cloudservices met hetzelfde virtuele netwerk hebben toegang tot de ILB-eindpunt. De volgende afbeelding toont de front-end web servers bevinden zich in een andere cloud-service van de back-end van de database en het gebruik van het ILB-eindpunt in hetzelfde virtuele netwerk.

![Interne taakverdeling tussen cloudservices](./media/load-balancer-internal-overview/IC744147.png)

Afbeelding 2 - front-servers in een andere cloud-service

## <a name="intranet-line-of-business-applications"></a>Intranet line-of-business-toepassingen

Verkeer van clients op de on-premises netwerk ophalen taakverdeling op de set van LOB-servers met behulp van VPN-verbinding met Azure-netwerk.

De clientcomputer hebben toegang tot een IP-adres van de Azure VPN-service gebruikt naar-site VPN. Kunt u het gebruik LOB-toepassing die wordt gehost achter de ILB-eindpunt.

![Interne taakverdeling met behulp van de punt naar-site VPN](./media/load-balancer-internal-overview/IC744148.png)

Afbeelding 3 - LOB-toepassingen die worden gehost achter de Load Balancer-eindpunt

Een ander scenario voor het LOB is om een site naar site VPN met het virtuele netwerk waarin de ILB-eindpunt is geconfigureerd. Hiermee worden lokale netwerkverkeer worden doorgestuurd naar de ILB-eindpunt.

![Interne taakverdeling met behulp van site naar site VPN](./media/load-balancer-internal-overview/IC744150.png)

Afbeelding 4: On-premises netwerkverkeer doorgestuurd naar de ILB-eindpunt

## <a name="limitations"></a>Beperkingen

Interne Load Balancer-configuraties ondersteunen geen snat omzetten. In de context van dit document verwijst snat omzetten naar poort onechte bron netwerkadresomzetting.  Dit geldt voor scenario's waarbij een virtuele machine in een load balancer-groep nodig heeft om de respectieve interne Load Balancer frontend-IP-adres. Dit scenario wordt niet ondersteund voor de interne Load Balancer. Verbindingsfouten uitgevoerd wanneer de stroom wordt verdeeld op de virtuele machine die afkomstig is van de stroom. U moet een proxy stijl load balancer gebruiken voor dergelijke scenario's.

## <a name="next-steps"></a>Volgende stappen

[Ondersteuning voor Azure Load Balancer van Azure Resource Manager](load-balancer-arm.md)

[De load balancer van een Internetgericht configureren aan de slag](load-balancer-get-started-internet-arm-ps.md)

[Een interne load balancer configureren aan de slag](load-balancer-get-started-ilb-arm-ps.md)

[Een distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)
