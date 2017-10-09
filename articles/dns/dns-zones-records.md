---
title: aaaDNS Zones en registreert overzicht - Azure DNS | Microsoft Docs
description: Overzicht van ondersteuning voor hosting van DNS-zones en -records in Microsoft Azure DNS.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: be4580d7-aa1b-4b6b-89a3-0991c0cda897
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: jonatul
ms.openlocfilehash: f214c3e2e810a80a000281820acd35f0aaf5a7e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-dns-zones-and-records"></a>Overzicht van DNS-zones en -records

Deze pagina wordt uitgelegd Hallo belangrijkste concepten van domeinen, DNS-zones, DNS-records en recordsets en hoe ze worden ondersteund in Azure DNS.

## <a name="domain-names"></a>Domeinnamen

Hallo Domain Name System is een hiërarchie van domeinen. Hallo hiërarchie start vanaf Hallo '' hoofddomein, waarvan de naam eenvoudigweg is '**.**'.  Hieronder komen de topleveldomeinen, zoals com, net, org, uk of nl.  Onder de topleveldomeinen komen de secondleveldomeinen, zoals org.uk of co.jp. Hallo-domeinen in Hallo DNS-hiërarchie worden globaal gedistribueerd en gehost door DNS-naamservers Hallo wereld.

Een domeinnaamregistrar is een organisatie waarmee u een domeinnaam, bijvoorbeeld 'contoso.com' toopurchase.  Naam biedt u de juiste toocontrol Hallo DNS-hiërarchie onder de naam die bijvoorbeeld zodat u toodirect Hallo-naam 'www.contoso.com' tooyour bedrijfswebsite Hallo aanschaffen van een domein. Hallo registrar mogelijk Hallo domein in een eigen naamservers namens jou hosten of kunt u toospecify alternatieve naam voor servers.

Azure DNS biedt een serverinfrastructuur naam globaal gedistribueerd, hoge beschikbaarheid, u kunt uw domein toohost gebruiken. Uw domeinen in Azure DNS hosten, kunt u de DNS-records met Hallo beheren dezelfde referenties, API's, hulpprogramma's, facturering en ondersteuning als uw andere Azure-services.

Azure DNS ondersteunt momenteel geen kopen van domeinnamen. Als u een domeinnaam toopurchase wilt, moet u een derde partij domeinnaamregistrar toouse. Hallo registrar brengt doorgaans een kleine jaarlijkse rekening. Hallo-domeinen kunnen vervolgens worden gehost in Azure DNS voor het beheer van DNS-records. Zie [delegeren van een domein tooAzure DNS-](dns-domain-delegation.md) voor meer informatie.

## <a name="dns-zones"></a>DNS-zones

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="dns-records"></a>DNS-records

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

### <a name="time-to-live"></a>Time to live

Hallo tijd toolive of TTL, geeft op hoe lang elke record in de cache geplaatst door clients voordat ze opnieuw worden opgevraagd. In Hallo bovenstaande voorbeeld is het Hallo TTL 3600 seconden oftewel 1 uur.

In Azure DNS Hallo TTL is opgegeven voor de recordset Hallo niet voor elke record, zodat dezelfde waarde wordt gebruikt voor alle records in deze record Hallo ingesteld.  U kunt geen TTL-waarde tussen 1 en 2.147.483.647 seconden opgeven.

### <a name="wildcard-records"></a>Recordsets met jokertekens

Azure DNS ondersteunt [recordsets met jokertekens](https://en.wikipedia.org/wiki/Wildcard_DNS_record). Recordsets met jokertekens worden geretourneerd in antwoord tooany query met een overeenkomende naam (tenzij er een geschikter is van een recordset van niet-jokertekens). Azure DNS ondersteunt recordsets met jokertekens voor alle recordtypen behalve NS en SOA.

toocreate een jokerteken record instellen, gebruikt u Hallo recordnaam '\*'. U kunt ook ook gebruiken een naam met '\*'als de meest linkse label, bijvoorbeeld'\*.foo'.

### <a name="cname-records"></a>CNAME-records

CNAME-recordsets kunnen niet worden gecombineerd met andere recordsets met Hallo dezelfde naam. Bijvoorbeeld, u een CNAME-recordset met Hallo relatieve naam 'www' geen maken en een A vastleggen met Hallo relatieve naam 'www' op Hallo dezelfde tijd.

Omdat het toppunt van Hallo zone (naam = ' @') bevat altijd Hallo NS en SOA-record sets die zijn gemaakt toen Hallo zone werd gemaakt, kan u een CNAME-recordset in het toppunt Hallo zone niet maken.

Deze beperkingen voortvloeien uit Hallo DNS-standaarden en geen beperkingen van Azure DNS.

### <a name="ns-records"></a>NS-records

Hallo NS-recordset in het toppunt Hallo zone (naam ' @') automatisch met elke DNS-zone wordt gemaakt en wordt automatisch verwijderd wanneer de zone hello wordt verwijderd (deze kan niet worden verwijderd afzonderlijk).

Deze recordset Hallo namen bevat van hello Azure DNS-naam servers toegewezen toohello zone. U kunt de naam van de aanvullende servers toothis NS-recordset, toosupport CO domeinen met meer dan één DNS-provider host toevoegen. U kunt ook wijzigen Hallo TTL en metagegevens voor deze recordset. U kan echter verwijderen of wijzigen Hallo vooraf ingestelde Azure DNS-naamservers. 

Houd er rekening mee dat dit alleen toohello NS recordset in het toppunt zone Hallo geldt. Andere NS recordsets in de zone (als gebruikte toodelegate onderliggende zones) kunnen worden gemaakt, gewijzigd en verwijderd zonder beperking.

### <a name="soa-records"></a>SOA-records

Een recordset SOA wordt automatisch gemaakt in de apex Hallo van elke zone (naam = ' @'), en wordt automatisch verwijderd wanneer de zone hello wordt verwijderd.  SOA-records kunnen niet worden gemaakt of afzonderlijk worden verwijderd.

U kunt alle eigenschappen van Hallo SOA-record, met uitzondering van de eigenschap 'host' hello, die vooraf geconfigureerde toorefer toohello primaire naam servernaam verstrekt door Azure DNS kunt wijzigen.

### <a name="spf-records"></a>SPF-records

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="srv-records"></a>SRV-records

[SRV-records](https://en.wikipedia.org/wiki/SRV_record) worden gebruikt door verschillende services toospecify serverlocaties. Bij het opgeven van een SRV-record in Azure DNS:

* Hallo *service* en *protocol* moet zijn opgegeven als deel van naam van de recordset hello, voorafgegaan door onderstrepingstekens bevatten.  Bijvoorbeeld '\_sip.\_ TCP.name'.  Voor een record in het toppunt Hallo zone, is geen toospecify moet ' @' in de recordnaam hello, gewoon gebruiken Hallo-service en het protocol, bijvoorbeeld '\_sip.\_ TCP'.
* Hallo *prioriteit*, *gewicht*, *poort*, en *doel* als parameters van elke record in de recordset Hallo zijn opgegeven.

### <a name="txt-records"></a>TXT-records

TXT-records zijn tekenreeksen die gebruikte toomap domein namen tooarbitrary. Ze worden gebruikt in meerdere toepassingen, met name gerelateerde tooemail configuratiestappen, zoals het Hallo [afzender beleid Framework (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) en [DomainKeys geïdentificeerd Mail (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail).

Hallo DNS-standaarden toe dat een enkele toocontain van de TXT-record meerdere tekenreeksen, die mogelijk van too254 tekens lang zijn. Indien meerdere tekenreeksen worden gebruikt, zijn ze door clients worden samengevoegd en behandeld als één tekenreeks.

Wanneer u hello Azure DNS-REST-API aanroept, moet u toospecify elke tekenreeks TXT afzonderlijk.  Wanneer u hello Azure-portal, PowerShell of CLI interfaces moet u één tekenreeks per record, waarmee automatisch is onderverdeeld in segmenten 254 tekens indien nodig.

meerdere tekenreeksen in een DNS-record moeten niet verwarren met Hallo Hallo meerdere TXT-records in een TXT-Recordset.  Een TXT-recordset kan meerdere records bevatten *die elk* kunnen meerdere tekenreeksen bevatten.  Azure DNS ondersteunt een totaal tekenreekslengte van up too1024 tekens in elke TXT-recordset (voor alle records gecombineerd).

## <a name="tags-and-metadata"></a>Tags en metagegevens

### <a name="tags"></a>Tags

Tags zijn van een lijst met naam / waarde-paren en worden gebruikt door Azure Resource Manager toolabel resources.  Azure Resource Manager gebruikt labels tooenable gefilterde weergaven van uw Azure-factuur en kunt u ook tooset een beleid op welke codes zijn vereist. Zie voor meer informatie over tags [Using tags tooorganize uw Azure-resources](../azure-resource-manager/resource-group-using-tags.md).

Azure DNS ondersteunt het gebruik van Azure Resource Manager-labels op DNS-zone-resources.  Het ondersteunt geen labels op DNS-recordsets, hoewel als een alternatief 'metadata' wordt ondersteund op DNS-recordsets zoals hieronder wordt uitgelegd.

### <a name="metadata"></a>Metagegevens

Als een alternatieve toorecord ingesteld labels, ondersteunt Azure DNS-recordsets met behulp van 'metadata' Aantekeningen maken.  Vergelijkbare tootags metagegevens kunt u tooassociate naam / waarde-paren met elke recordset.  Dit kan handig zijn, bijvoorbeeld toorecord Hallo doel van elke record ingesteld.  In tegenstelling tot tags, metagegevens gebruikte tooprovide een gefilterde weergave van uw Azure-factuur mag niet en kan niet worden opgegeven in een Azure Resource Manager-beleid.

## <a name="etags"></a>Etags

Stel dat twee personen of twee processen toomodify probeert een DNS-record op Hallo dezelfde tijd. Welke wins? En Hallo winnaar weten dat ze wijzigingen die zijn gemaakt door iemand anders hebt overschreven?

Azure DNS maakt gebruik van Etags toohandle gelijktijdige wijzigingen toohello dezelfde resource veilig. Etags zijn gescheiden van [Azure Resource Manager 'Labels'](#tags). Elke DNS-bronrecords (zone of recordset) heeft een Etag die is gekoppeld. Wanneer een resource wordt opgehaald, wordt ook de Etag opgehaald. U kunt kiezen toopass terug Hallo Etag zodat Azure DNS kunt die Hallo Etag op Hallo-komt overeen met server controleren bij het bijwerken van een resource. Omdat elke update tooa resource in het Hallo Etag opnieuw worden gegenereerd resulteert, geeft een Etag komt niet overeen aan dat een gelijktijdige wijziging is doorgevoerd. Etags kan ook worden gebruikt bij het maken van een nieuwe resource tooensure die Hallo resource niet al bestaat.

Azure DNS PowerShell gebruikt standaard Etags tooblock gelijktijdige wijzigingen toozones en recordsets. Hallo optionele *-overschrijven* switch, kunt u gebruikte toosuppress Etag controles in dat geval kan gelijktijdige wijzigingen die zijn opgetreden worden overschreven.

Etags zijn opgegeven met behulp van HTTP-headers op niveau Hallo Hallo REST-API van Azure DNS.  Hun gedrag is opgenomen in de volgende tabel Hallo:

| Koptekst | Gedrag |
| --- | --- |
| Geen |PUT altijd is gelukt (geen Etag-controle) |
| If-match<etag> |PUT slaagt alleen als de bron bestaat en Etag komt overeen met |
| If-match * |PUT slaagt alleen als de bron bestaat |
| If-none-match * |PUT slaagt alleen als resource niet bestaat |


## <a name="limits"></a>Limieten

Hallo standaardlimiet van het volgende van toepassing wanneer u Azure DNS:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

## <a name="next-steps"></a>Volgende stappen

* met behulp van Azure DNS toostart meer informatie over hoe te[maken van een DNS-zone](dns-getstarted-create-dnszone-portal.md) en [DNS-records maken](dns-getstarted-create-recordset-portal.md).
* een bestaande DNS-zone toomigrate meer informatie over hoe te[importeren en exporteren van een DNS-zonebestand](dns-import-export.md).
