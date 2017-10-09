---
title: aaaAzure DNS-probleemoplossingsgids | Microsoft Docs
description: Hoe tootroubleshoot algemene problemen met een Azure DNS
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a>Azure DNS-probleemoplossingsgids

Deze pagina bevat informatie over probleemoplossing voor veelgestelde vragen voor Azure DNS.

Als deze stappen uw probleem niet verhelpen, kunt u ook zoeken naar of uw probleem post een bericht op onze [ondersteuning communityforum op MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork). U kunt ook een Azure ondersteuningsaanvraag openen.


## <a name="i-cant-create-a-dns-zone"></a>Ik kan een DNS-zone niet maken.

algemene problemen tooresolve, probeer een of meer Hallo stappen te volgen:

1.  Bekijk hello die Azure DNS audit logboeken toodetermine Hallo foutreden.
2.  Elke DNS-zonenaam moet uniek zijn binnen de resourcegroep. Dat wil zeggen, twee DNS-zones Hello dezelfde naam van een resourcegroep niet delen. Gebruik een andere zonenaam of een andere resourcegroep.
3.  Er wordt een fout "Bereikt of overschreden Hallo maximumaantal zones in abonnement {abonnements-id}." Gebruik een ander Azure-abonnement, verwijder een aantal zones, of neem contact op met ondersteuning van Azure tooraise limiet voor uw abonnement.
4.  Mogelijk ziet u een fout 'hello zone '{zone-name}' is niet beschikbaar'. Deze fout betekent dat Azure DNS naamservers niet kan tooallocate voor deze DNS-zone. Gebruik dan een andere zonenaam. U kunt ook als u de domeineigenaar naam hello, contact op met ondersteuning van Azure, die de naamservers voor u kunt toewijzen.


### <a name="recommended-documents"></a>**Aanbevolen documenten**

[DNS-zones en -records](dns-zones-records.md)
<br>
[Een DNS-zone maken](dns-getstarted-create-dnszone-portal.md)

## <a name="i-cant-create-a-dns-record"></a>Ik kan geen DNS-record maken

algemene problemen tooresolve, probeer een of meer Hallo stappen te volgen:

1.  Bekijk hello die Azure DNS audit logboeken toodetermine Hallo foutreden.
2.  Hallo-Recordset bestaat er al?  Azure DNS beheert records met behulp van de record *ingesteld*, die zijn Hallo verzameling records Hallo dezelfde naam en hetzelfde Hallo type. Als een record met Hallo dezelfde naam en typ het al bestaat, wordt tooadd een andere deze record moet u bestaande record Hallo bewerken ingesteld.
3.  Probeert u toocreate een record op Hallo DNS-zone apex (Hallo 'root' hello zone)? Als dus Hallo DNS-conventie toouse Hallo ' @' teken als Hallo recordnaam. Let ook op dat Hallo DNS-standaarden staan niet toe dat CNAME-records in het toppunt Hallo zone.
4.  Is er sprake van een CNAME-conflict?  Hallo DNS-standaarden toegestaan een CNAME-record met dezelfde naam als een record van een ander type Hallo niet. Als u een bestaande CNAME, het maken van een record met dezelfde naam van een ander type mislukt Hallo hebt.  Maken van een CNAME mislukt op dezelfde manier als Hallo naam overeenkomt met een bestaande record van een ander type. Hallo conflict verwijderen door het verwijderen van Hallo andere record of een andere recordnaam kiezen.
5.  Hallo maximale aantal recordsets zijn toegestaan in een DNS-zone Hallo bereikt? huidige aantal recordsets Hallo en hello zijn maximum aantal recordsets weergegeven in hello Azure-portal onder Hallo eigenschappen voor Hallo zone. Als u deze limiet is bereikt, klikt u vervolgens een aantal recordsets verwijderen of neem contact op met ondersteuning van Azure tooraise de limiet van uw recordset voor deze zone, en probeer het opnieuw. 


### <a name="recommended-documents"></a>**Aanbevolen documenten**

[DNS-zones en -records](dns-zones-records.md)
<br>
[Een DNS-zone maken](dns-getstarted-create-dnszone-portal.md)



## <a name="i-cant-resolve-my-dns-record"></a>Ik kan mijn DNS-record niet omzetten

De DNS-naamomzetting vereist meerdere stappen en kan om verschillende redenen mislukken. Hallo volgende stappen kunt u onderzoeken waarom de DNS-omzetting is mislukt voor een DNS-record in een zone die wordt gehost in Azure DNS.

1.  Bevestig dat Hallo DNS-records correct zijn geconfigureerd in Azure DNS. Bekijk Hallo DNS-records in hello Azure-portal controleren Hallo zonenaam en recordnaam recordtype juist zijn.
2.  Bevestig dat Hallo DNS-records correct op Hallo Azure DNS-naamservers omzetten.
    - Als u DNS-query's van uw lokale PC, ziet u mogelijk resultaten in het cachegeheugen die niet met huidige status van de naamservers Hallo Hallo overeenkomen.  Bedrijfsnetwerken gebruiken ook vaak proxyservers DNS-naamservers toospecific die verhinderen dat DNS-query's worden omgeleid.  tooavoid deze problemen gebruiken op basis van web service voor naamomzetting zoals [digwebinterface](http://digwebinterface.com).
    - Worden ervoor toospecify Hallo juist naamservers voor uw DNS-zone, zoals wordt weergegeven in hello Azure-portal.
    - Controleer of Hallo DNS-naam klopt (u toospecify Hallo volledig gekwalificeerde naam hebben, inclusief de naam van de zone Hallo) en Hallo recordtype juist is
3.  Bevestig dat Hallo DNS-domeinnaam juist is [toohello Azure DNS-naamservers overgedragen](dns-domain-delegation.md). Er zijn [veel websites van derden die de DNS-delegering kunnen valideren](https://www.bing.com/search?q=dns+check+tool). Deze test is een *zone* delegering test, zodat u alleen Hallo DNS-zone en niet Hallo volledig gekwalificeerde naam van de record moet invoeren.
4.  Hallo bovenstaande nadat is voltooid, uw DNS-record moet nu worden omgezet correct. tooverify, die u opnieuw kunt gebruiken [digwebinterface](http://digwebinterface.com), nu met de naam Hallo-server standaardinstellingen.


### <a name="recommended-documents"></a>**Aanbevolen documenten**

[Een domein tooAzure DNS overdragen](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a>Hoe geef ik Hallo 'service' en 'protocol' voor een SRV-record

Azure DNS beheert DNS-records als recordsets-verzameling van records met Hallo dezelfde naam en hetzelfde Hallo Hallo type. Hallo 'service' en 'protocol' moeten een SRV-Recordset toobe opgegeven als deel van naam van de recordset Hallo. Hallo worden andere parameters SRV ('prioriteit', 'gewicht', 'poort' en 'target') afzonderlijk opgegeven voor elke record in de recordset Hallo.

Voorbeeld van SRV-recordnamen (servicenaam 'sip', protocol 'tcp'):

- \_SIP. \_tcp (maakt een record in het toppunt zone Hallo)
- \_sip.\_tcp.sipservice (er wordt een recordset gemaakt met de naam 'sipservice')

### <a name="recommended-documents"></a>**Aanbevolen documenten**

[DNS-zones en -records](dns-zones-records.md)
<br>
[DNS-recordsets en records maken met behulp van hello Azure-portal](dns-getstarted-create-recordset-portal.md)
<br>
[SRV-recordtype (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)


## <a name="next-steps"></a>Volgende stappen

* Meer informatie over [Azure DNS-zones en records](dns-zones-records.md)
* met behulp van Azure DNS toostart meer informatie over hoe te[maken van een DNS-zone](dns-getstarted-create-dnszone-portal.md) en [DNS-records maken](dns-getstarted-create-recordset-portal.md).
* een bestaande DNS-zone toomigrate meer informatie over hoe te[importeren en exporteren van een DNS-zonebestand](dns-import-export.md).

