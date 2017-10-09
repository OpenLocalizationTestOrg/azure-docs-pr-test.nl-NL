---
title: overzicht van aaaAzure DNS-delegering | Microsoft Docs
description: Begrijpen hoe domeindelegering toochange en gebruik Azure DNS name servers tooprovide domeinen te hosten.
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
ms.openlocfilehash: eaf2d2e345004b4d631e8d81d548b8ca23277d05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="delegation-of-dns-zones-with-azure-dns"></a>Delegatie van DNS-zones met Azure DNS

Azure DNS kunt u een DNS-zone toohost en Hallo DNS-records voor een domein in Azure beheren. Om DNS-query's voor een domein tooreach Azure DNS, Hallo domein toobe heeft gedelegeerd tooAzure DNS van Hallo bovenliggende domein. Houd er rekening mee Azure DNS is niet de domeinregistrar Hallo. Dit artikel wordt uitgelegd hoe domeindelegering werkt en hoe toodelegate domeinen tooAzure DNS.

## <a name="how-dns-delegation-works"></a>Hoe DNS-delegering werkt

### <a name="domains-and-zones"></a>Domeinen en zones

Hallo Domain Name System is een hiërarchie van domeinen. Hallo hiërarchie start vanaf Hallo '' hoofddomein, waarvan de naam eenvoudigweg is '**.**'.  Hieronder komen de topleveldomeinen, zoals com, net, org, uk of nl.  Onder deze topleveldomeinen komen de secondleveldomeinen, zoals org.uk of co.jp.  Enzovoort. Hallo-domeinen in Hallo DNS-hiërarchie worden gehost met behulp van afzonderlijke DNS-zones. Deze zones worden globaal gedistribueerd en gehost door DNS-naamservers Hallo wereld.

**DNS-zone** -een domein is een unieke naam in Hallo Domain Name System, bijvoorbeeld 'contoso.com'. Een DNS-zone is gebruikte toohost Hallo DNS-records voor een bepaald domein. Hallo domein 'contoso.com' kan bijvoorbeeld meerdere DNS-records, zoals 'mail.contoso.com' (voor een e-mailserver) en 'www.contoso.com' (voor een website) bevatten.

**Domeinregistrar**: een domeinregistrar is een bedrijf dat internetdomeinnamen kan leveren. Ze controleren als Hallo internetdomein die u wilt toouse beschikbaar en kunt u toopurchase deze. Zodra het Hallo-domeinnaam is geregistreerd, bent u Hallo juridische eigenaar voor Hallo domeinnaam. Als u al een internetdomein hebt, gebruikt u Hallo huidige domein registrar toodelegate tooAzure DNS.

toofind meer informatie over wie de eigenaar van een bepaald domeinnaam of voor informatie over het toobuy een domein, Zie [Internet domein management in Azure AD](https://msdn.microsoft.com/library/azure/hh969248.aspx).

### <a name="resolution-and-delegation"></a>Omzetting en delegering

Er zijn twee typen DNS-servers:

* Een *gezaghebbende* DNS-server host DNS-zones. Deze beantwoordt DNS-query's voor records in deze zones.
* Een *recursieve* DNS-server host geen DNS-zones. De server beantwoordt alle DNS-query's door het aanroepen van de gezaghebbende DNS-servers toogather Hallo gegevens nodig.

Azure DNS biedt een gezaghebbende DNS-service.  Het biedt geen een recursieve DNS-service. Cloudservices en virtuele machines in Azure worden automatisch geconfigureerde toouse een recursieve DNS-service die afzonderlijk wordt geleverd als onderdeel van Azure infrastructuur. Voor informatie over hoe toochange deze DNS-instellingen, Zie [naamomzetting in Azure](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

DNS-clients op pc's of mobiele apparaten roepen een recursieve DNS-server tooperform alle DNS-query's Hallo clienttoepassingen nodig hebben.

Wanneer een recursieve DNS-server een query voor een DNS-record zoals 'www.contoso.com' ontvangt, moet deze eerst toofind Hallo naam server hosting Hallo zone voor Hallo-domein 'contoso.com'. naamserver toofind hello, deze begint bij de basisnaamservers Hallo en zoeken naamservers Hallo Hallo com-zone hosten. Deze bevraagt vervolgens Hallo 'com' name servers toofind Hallo naamservers die Hallo 'contoso.com' zone hosten.  Ten slotte is kunnen tooquery deze naamservers voor 'www.contoso.com'.

Deze procedure is aangeroepen het omzetten van Hallo DNS-naam. Strikt genomen DNS-omzetting aanvullende stappen zoals het volgen van CNAMEs bevat, maar is niet belangrijk toounderstanding hoe DNS-delegering werkt.

Hoe een bovenliggende zone 'wijst' toohello naamservers voor een onderliggende zone? Hiervoor wordt gebruikgemaakt van een speciaal type DNS-record, ook wel een NS-record genoemd (NS staat voor 'naamserver'). Bijvoorbeeld Hallo hoofdzone bevat de NS-records voor 'com' en ziet u de naamservers Hallo voor Hallo com-zone. Hallo com-zone bevat op zijn beurt NS-records voor contoso.com', waarin de naamservers Hallo voor Hallo 'contoso.com' zone. Instellen van Hallo NS-records voor een onderliggende zone in een bovenliggende zone wordt delegatieverlenend Hallo domein genoemd.

Hallo volgende afbeelding toont een voorbeeld van de DNS-query. Hallo contoso.net en partners.contoso.net zijn Azure DNS-zones.

![DNS-naamserver](./media/dns-domain-delegation/image1.png)

1. Hallo clientaanvragen `www.partners.contoso.net` van hun lokale DNS-server.
1. Hallo lokale DNS-server heeft geen record Hallo dus het een verzoek tootheir basisserver naam is.
1. Hallo-hoofdserver naam heeft geen record hello, maar weet Hallo adres Hallo `.net` naamserver, het adres toohello DNS-server biedt
1. Hallo DNS verzendt Hallo aanvraag toohello `.net` naamserver, het heeft geen record van de Hallo maar Hallo-adres van de naamserver voor Hallo contoso.net kent. In dit geval betreft het een DNS-zone die wordt gehost in Azure DNS.
1. Hallo zone `contoso.net` heeft geen record Hallo maar weet Hallo naamserver voor `partners.contoso.net` en reageert met die. In dit geval betreft het een DNS-zone die wordt gehost in Azure DNS.
1. Hallo DNS-server aanvragen Hallo IP-adres van `partners.contoso.net` van Hallo `partners.contoso.net` zone. Het Hallo-A-record bevat en reageert met Hallo IP-adres.
1. Hallo DNS-server biedt Hallo IP-adres toohello client
1. Hallo-client verbinding maakt toohello website `www.partners.contoso.net`.

Elke delegering bevat twee kopieën van de NS-records Hallo; een in Hallo bovenliggende zone toohello onderliggend, en een andere in Hallo onderliggende zone zelf aan te wijzen. Hallo NS-records voor 'contoso.net' bevat Hallo 'contoso.net' zone (in aanvulling toohello NS-records in 'net'). Deze records worden gezaghebbende NS-records genoemd en bevinden zich in de apex Hallo van Hallo onderliggende zone.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe te[uw domein tooAzure DNS overdragen](dns-delegate-domain-azure-dns.md)

