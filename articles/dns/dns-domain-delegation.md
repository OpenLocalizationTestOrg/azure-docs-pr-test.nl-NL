---
title: Overzicht van Azure DNS-delegatie | Microsoft Docs
description: Lees hoe u de domeindelegering wijzigt en DNS-naamservers kunt gebruiken om domeinen te hosten.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: 31a500502a4d3e729ecb79929ed6c1de156d6259
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="delegation-of-dns-zones-with-azure-dns"></a>Delegatie van DNS-zones met Azure DNS

Met Azure DNS kunt u een DNS-zone hosten en de DNS-records voor een domein in Azure beheren. Het domein moet vanaf het bovenliggende domein worden gedelegeerd naar Azure DNS om ervoor te zorgen dat DNS-query's voor een domein Azure DNS bereiken. Houd er rekening mee Azure DNS is niet de domeinregistrar. In dit artikel wordt uitgelegd hoe domeindelegering werkt en hoe domeinen naar Azure DNS delegeert.

## <a name="how-dns-delegation-works"></a>Hoe DNS-delegering werkt

### <a name="domains-and-zones"></a>Domeinen en zones

Het Domain Name System is een hiërarchie van domeinen. De hiërarchie start vanaf het hoofddomein. De naam van dit domein is eenvoudigweg '**.**'.  Hieronder komen de topleveldomeinen, zoals com, net, org, uk of nl.  Onder deze topleveldomeinen komen de secondleveldomeinen, zoals org.uk of co.jp.  Enzovoort. De domeinen in de DNS-hiërarchie worden gehost met behulp van afzonderlijke DNS-zones. Deze zones worden globaal gedistribueerd en gehost door DNS-naamservers over de hele wereld.

**DNS-zone**: een domein is een unieke naam in het Domain Name System, bijvoorbeeld contoso.com. Een DNS-zone wordt gebruikt om de DNS-records voor een bepaald domein te hosten. Het domein contoso.com kan bijvoorbeeld een aantal DNS-records bevatten, zoals mail.contoso.com (voor een e-mailserver) en www.contoso.com (voor een website).

**Domeinregistrar**: een domeinregistrar is een bedrijf dat internetdomeinnamen kan leveren. Het bedrijf controleert of het internetdomein dat u wilt gebruiken, beschikbaar is en biedt u de mogelijkheid om de naam te kopen. Zodra de domeinnaam is geregistreerd, bent u de juridische eigenaar van de domeinnaam. Als u al een internetdomein hebt, gebruikt u de huidige domeinregistrar om te delegeren naar Azure DNS.

Zie [Internetdomeinbeheer in Azure AD](https://msdn.microsoft.com/library/azure/hh969248.aspx) voor meer informatie over wie de eigenaar is van een bepaald domein of voor informatie over het kopen van domein.

### <a name="resolution-and-delegation"></a>Omzetting en delegering

Er zijn twee typen DNS-servers:

* Een *gezaghebbende* DNS-server host DNS-zones. Deze beantwoordt DNS-query's voor records in deze zones.
* Een *recursieve* DNS-server host geen DNS-zones. De server beantwoordt alle DNS-query's door gezaghebbende DNS-servers aan te roepen om de benodigde gegevens te verzamelen.

Azure DNS biedt een gezaghebbende DNS-service.  Het biedt geen een recursieve DNS-service. Cloudservices en virtuele machines in Azure worden automatisch geconfigureerd voor het gebruik van een recursieve DNS-service die afzonderlijk wordt geleverd als onderdeel van de infrastructuur van Azure. Raadpleeg [Naamomzetting in Azure](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) voor meer informatie over het wijzigen van deze DNS-instellingen.

DNS-clients op pc's of mobiele apparaten roepen een recursieve DNS-server om de DNS-query's uit te voeren die de clienttoepassingen nodig hebben.

Wanneer een recursieve DNS-server een query voor een DNS-record zoals www.contoso.com ontvangt, moet eerst de naamserver worden gezocht die de zone voor het domein contoso.com host. Om de naamserver te zoeken, wordt er begonnen bij de basisnaamservers, om vervolgens de naamservers te vinden die de com-zone hosten. Vervolgens wordt er een query op de com-naamservers uitgevoerd om de naamservers te zoeken die de zone contoso.com hosten.  Tot slot wordt er op deze naamservers een query uitgevoerd om www.contoso.com te zoeken.

Deze procedure wordt het omzetten van de DNS-naam genoemd. Strikt genomen omvat de DNS-omzetting aanvullende stappen zoals het volgen van CNAMEs, maar dat is niet belangrijk om te begrijpen hoe de DNS-delegering werkt.

Hoe 'wijst' een bovenliggende zone naar de naamservers voor een onderliggende zone? Hiervoor wordt gebruikgemaakt van een speciaal type DNS-record, ook wel een NS-record genoemd (NS staat voor 'naamserver'). De hoofdzone bevat bijvoorbeeld NS-records voor com en toont u de naamservers voor de com-zone. De com-zone bevat op zijn beurt NS-records voor contoso.com, die u de naamservers toont voor de zone contoso.com. Het instellen van de NS-records voor een onderliggende zone in de bovenliggende zone wordt het delegeren van het domein genoemd.

In de volgende afbeelding ziet u een voorbeeld van een DNS-query. Contoso.net en partners.contoso.net zijn Azure-DNS-zones.

![DNS-naamserver](./media/dns-domain-delegation/image1.png)

1. De client vraagt `www.partners.contoso.net` aan van zijn lokale DNS-server.
1. De lokale DNS-server beschikt niet over de record en vraagt deze daarom op bij de hoofdnaamserver.
1. De hoofdnaamserver beschikt niet over de record, maar kent het adres van de `.net`-naamserver. Dit adres wordt aan de DNS-server doorgegeven
1. De DNS-server stuurt de aanvraag naar de `.net`-naamserver. Deze beschikt niet over de record, maar kent het adres van de naamserver van contoso.net. In dit geval betreft het een DNS-zone die wordt gehost in Azure DNS.
1. De zone `contoso.net` beschikt niet over de record, maar kent de naamserver voor `partners.contoso.net` en retourneert deze. In dit geval betreft het een DNS-zone die wordt gehost in Azure DNS.
1. De DNS-server vraagt het IP-adres van `partners.contoso.net` op bij de zone `partners.contoso.net`. Deze bevat de A-record en antwoordt met het IP-adres.
1. De DNS-server verstrekt het IP-adres aan de client
1. De client maakt verbinding met de website `www.partners.contoso.net`.

Elke delegering bevat twee kopieën van de NS-records. De ene kopie bevindt zich in de bovenliggende zone en wijst naar de onderliggende zone, terwijl de andere kopie zich in de onderliggende zone zelf bevindt. De zone contoso.net bevat de NS-records voor contoso.net (naast de NS-records in 'net'). Deze records worden gezaghebbende NS-records genoemd en bevinden zich in de apex van de onderliggende zone.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe u [uw domein delegeert naar Azure DNS](dns-delegate-domain-azure-dns.md)

