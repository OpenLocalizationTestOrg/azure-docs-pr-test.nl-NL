---
title: Azure DNS-probleemoplossingsgids | Microsoft Docs
description: Het oplossen van veelvoorkomende problemen met Azure DNS
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
ms.openlocfilehash: 1d9bb681a864bdc3e5a2f9c9a531d9566b16ada4
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/11/2017
---
# <a name="azure-dns-troubleshooting-guide"></a>Azure DNS-probleemoplossingsgids

Deze pagina bevat informatie over probleemoplossing voor veelgestelde vragen voor Azure DNS.

Als deze stappen uw probleem niet verhelpen, kunt u ook zoeken naar of uw probleem post een bericht op onze [ondersteuning communityforum op MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork). U kunt ook een Azure ondersteuningsaanvraag openen.


## <a name="i-cant-create-a-dns-zone"></a>Ik kan een DNS-zone niet maken.

Probeer een of meer van de volgende stappen om veelvoorkomende problemen op te lossen:

1.  Controleer de auditlogboeken van Azure DNS om de reden van de fout vast te stellen.
2.  Elke DNS-zonenaam moet uniek zijn binnen de resourcegroep. Een resourcegroep kan dus niet twee DNS-zones met dezelfde naam bevatten. Gebruik een andere zonenaam of een andere resourcegroep.
3.  U ziet mogelijk de foutmelding 'Het maximumaantal zones in abonnement {abonnements-id} is bereikt of overschreden'. Gebruik een ander Azure-abonnement, verwijder enkele zones of neem contact op met de ondersteuning van Azure om uw abonnementslimiet te verhogen.
4.  U ziet mogelijk de foutmelding 'De zone {zonenaam} is niet beschikbaar'. Dit betekent dat Azure DNS geen naamservers kan toewijzen voor deze DNS-zone. Gebruik dan een andere zonenaam. Als u de eigenaar van de domeinnaam bent, kunt u ook de ondersteuning van Azure vragen naamservers voor u toe te wijzen.


### <a name="recommended-documents"></a>**Aanbevolen documenten**

[DNS-zones en -records](dns-zones-records.md)
<br>
[Een DNS-zone maken](dns-getstarted-create-dnszone-portal.md)

## <a name="i-cant-create-a-dns-record"></a>Ik kan geen DNS-record maken

Probeer een of meer van de volgende stappen om veelvoorkomende problemen op te lossen:

1.  Controleer de auditlogboeken van Azure DNS om de reden van de fout vast te stellen.
2.  Bestaat de recordset al?  Azure DNS beheert records als *recordsets*. Hierin zijn records met dezelfde naam en van hetzelfde type opgenomen. Als er al een record met dezelfde naam en van hetzelfde type bestaat, kunt u nog een dergelijke record toevoegen door de bestaande recordset te bewerken.
3.  Probeert u een record te maken in de apex (het hoofdniveau) van de DNS-zone? Dan is het de DNS-conventie om het @-teken te gebruiken als recordnaam. De DNS-standaarden staan CNAME-records in de apex van de zone niet toe.
4.  Is er sprake van een CNAME-conflict?  De DNS-standaarden staan niet toe dat een CNAME-record dezelfde naam heeft als een record van een ander type. Als u een bestaande CNAME hebt, kunt u geen record maken met dezelfde naam maar van een ander type.  Op dezelfde manier kunt u ook geen CNAME maken als de naam overeenkomt met een bestaande record van een ander type. Verhelp het conflict door de andere record te verwijderen of een andere recordnaam te kiezen.
5.  Hebt u de limiet voor het aantal toegestane recordsets in een DNS-zone bereikt? Het huidige aantal recordsets en het maximumaantal recordsets worden weergegeven in Azure Portal onder de eigenschappen van de zone. Als u deze limiet hebt bereikt, verwijdert u een aantal recordsets of neemt u contact op met de ondersteuning van Azure om de limiet voor recordsets voor deze zone te laten verhogen. Probeer het vervolgens opnieuw. 


### <a name="recommended-documents"></a>**Aanbevolen documenten**

[DNS-zones en -records](dns-zones-records.md)
<br>
[Een DNS-zone maken](dns-getstarted-create-dnszone-portal.md)



## <a name="i-cant-resolve-my-dns-record"></a>Ik kan mijn DNS-record niet omzetten

De DNS-naamomzetting vereist meerdere stappen en kan om verschillende redenen mislukken. Aan de hand van de volgende stappen kunt u onderzoeken waarom de DNS-omzetting mislukt voor een DNS-record in een zone in Azure DNS.

1.  Controleer of de DNS-records correct zijn geconfigureerd in Azure DNS. Controleer of de zonenaam, de naam en het type van de DNS-records in Azure Portal correct zijn.
2.  Controleer of de DNS-records correct zijn omgezet in de Azure DNS-naamservers.
    - Als u DNS-query's maakt op uw lokale pc, tonen de resultaten in de cache mogelijk niet de huidige status van de naamservers.  Daarnaast maken bedrijfsnetwerken vaak gebruik van DNS-proxyservers, waardoor DNS-query's niet worden doorgestuurd naar specifieke naamservers.  U kunt deze problemen voorkomen door een webservice voor naamomzetting te gebruiken, zoals [digwebinterface](http://digwebinterface.com).
    - Zorg er wel voor dat u de juiste naamservers voor uw DNS-zone opgeeft, zoals weergegeven in Azure Portal.
    - Controleer of de DNS-naam (dit is de volledig gekwalificeerde naam, inclusief de zonenaam) en het recordtype kloppen.
3.  Controleer of de DNS-domeinnaam juist is [gedelegeerd naar de Azure DNS-naamservers](dns-domain-delegation.md). Er zijn [veel websites van derden die de DNS-delegering kunnen valideren](https://www.bing.com/search?q=dns+check+tool). Dit is een delegeringstest voor de *zone*. Geef dus alleen de naam van de DNS-zone op en niet de volledig gekwalificeerde recordnaam.
4.  Nadat u het bovenstaande hebt voltooid, zou uw DNS-record correct moeten worden omgezet. U kunt dit controleren door opnieuw [digwebinterface](http://digwebinterface.com) te gebruiken, maar nu met de standaardinstellingen van de naamserver.


### <a name="recommended-documents"></a>**Aanbevolen documenten**

[Een domein delegeren naar Azure DNS](dns-domain-delegation.md)



## <a name="how-do-i-specify-the-service-and-protocol-for-an-srv-record"></a>Hoe geef ik de 'service' en het 'protocol' voor een SRV-record op?

Azure DNS beheert DNS-records als recordsets. Hierin zijn records met dezelfde naam en van hetzelfde type opgenomen. Voor een SRV-recordset moeten de 'service' en het 'protocol' worden opgegeven als onderdeel van de recordsetnaam. De andere SRV-parameters ('prioriteit', 'gewicht', 'poort' en 'doel') worden afzonderlijk opgegeven voor elke record in de recordset.

Voorbeeld van SRV-recordnamen (servicenaam 'sip', protocol 'tcp'):

- \_sip.\_tcp (er wordt een record gemaakt in de apex van de zone)
- \_sip.\_tcp.sipservice (er wordt een recordset gemaakt met de naam 'sipservice')

### <a name="recommended-documents"></a>**Aanbevolen documenten**

[DNS-zones en -records](dns-zones-records.md)
<br>
[DNS-recordsets en -records maken met Azure Portal](dns-getstarted-create-recordset-portal.md)
<br>
[SRV-recordtype (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)


## <a name="next-steps"></a>Volgende stappen

* Meer informatie over [Azure DNS-zones en records](dns-zones-records.md)
* Om te starten met behulp van Azure DNS, informatie over hoe [maken van een DNS-zone](dns-getstarted-create-dnszone-portal.md) en [DNS-records maken](dns-getstarted-create-recordset-portal.md).
* Voor het migreren van een bestaande DNS-zone meer informatie over hoe [importeren en exporteren van een DNS-zonebestand](dns-import-export.md).

