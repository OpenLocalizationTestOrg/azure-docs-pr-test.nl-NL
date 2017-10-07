---
title: aaaConsistency niveaus in de Azure DB die Cosmos | Microsoft Docs
description: Azure Cosmos DB heeft vijf consistentie niveaus toohelp saldo uiteindelijke consistentie, beschikbaarheid en latentie-en nadelen.
keywords: uiteindelijke consistentie azure cosmos db, azure, Microsoft azure
services: cosmos-db
author: mimig1
manager: jhubbard
editor: cgronlun
documentationcenter: 
ms.assetid: 3fe51cfa-a889-4a4a-b320-16bf871fe74c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac399c229d0856cd811bc81568536e519af3300f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tunable-data-consistency-levels-in-azure-cosmos-db"></a>Gegevens instelbare consistentieniveaus in Azure Cosmos-DB
Azure Cosmos-DB is uit Hallo gemalen met globale verdeling in gedachten voor elke gegevensmodel ontworpen. Is ontworpen toooffer voorspelbare lage latentie garanties, een SLA van 99,99% beschikbaarheid, en meerdere goed gedefinieerde versoepeld consistentie modellen. Op dit moment Azure Cosmos DB bevat vijf consistentieniveaus: sterk, gebonden-verouderd, sessie, consistente voorvoegsel en uiteindelijk. 

Naast **sterk** en **uiteindelijke consistentie** modellen vaak aangeboden door gedistribueerde databases Azure Cosmos DB biedt drie meer zorgvuldig gecodeerd en geoperationaliseerd consistentie modellen en heeft hun nut tegen werkelijkheid gebruiksvoorbeelden gevalideerd. Dit zijn Hallo **gebonden veroudering**, **sessie**, en **consistent voorvoegsel** consistentieniveaus. Gezamenlijk in deze vijf consistentieniveaus kunt u toomake goed gemotiveerd verschillen tussen de consistentie, beschikbaarheid en latentie. 

## <a name="distributed-databases-and-consistency"></a>Gedistribueerde databases en consistentie
Commerciële gedistribueerde databases kunnen worden onderverdeeld in twee categorieën: databases die helemaal geen duidelijk omschreven, waarschijnlijke consistentiekeuzes bieden en databases die twee mogelijkheden voor extreme programmeerbaarheid bieden (sterke versus mogelijke consistentie). 

Hallo voormalige lasten toepassingsontwikkelaars met minutia van de Replicatieprotocollen en deze toomake moeilijk wisselwerking tussen de consistentie, beschikbaarheid, latentie en doorvoer verwacht. Hallo laatstgenoemde plaatst een zware belasting toochoose een van de twee uiterste Hallo. Ondanks Hallo overvloed aan onderzoek en voorstellen voor meer dan 50 consistentie modellen is hello gedistribueerde database community geen consistentieniveaus kunnen toocommercialize afgezien van sterke en uiteindelijke consistentie. Cosmos DB kan ontwikkelaars toochoose tussen vijf goed gedefinieerde consistentie modellen langs Hallo consistentie spectrum – sterk, gebonden veroudering, [sessie](http://dl.acm.org/citation.cfm?id=383631), consistente voorvoegsel en uiteindelijk. 

![Azure Cosmos DB biedt meerdere (beperkte) consistentie modellen toochoose van goed gedefinieerde](./media/consistency-levels/five-consistency-levels.png)

Hallo volgende tabel ziet u Hallo specifieke garanties verschillende niveaus van de consistentie biedt.
 
**Consistentieniveaus en bijbehorende garanties**

| Consistentieniveau | Garanties |
| --- | --- |
| Sterk | Linearisabiliteit |
| Gebonden veroudering | Consistent prefix. Leesbewerkingen volgen op schrijfbewerkingen met k prefixen of t interval |
| Sessie   | Consistent prefix. Monotone leesbewerkingen, monotone schrijfbewerkingen, read-your-writes, write-follows-reads |
| Consistent prefix | Updates geretourneerd zijn sommige voorvoegsel van alle Hallo updates, geen hiaten |
| Mogelijk  | Leesbewerkingen vinden niet op volgorde plaats |

U kunt configureren Hallo consistentie standaardniveau voor je account Cosmos-DB (en later overschrijven Hallo consistentiecontrole op een specifieke leesaanvraag). Hallo consistentie standaardniveau geldt intern toodata Hallo partitie sets die mogelijk span regio's. Ongeveer 73% van onze tenants gebruik sessieconsistentie en 20% liever gebonden veroudering. We zien dat ongeveer 3% van onze klanten met verschillende consistentieniveaus in eerste instantie experimenteren voordat op een specifieke consistentie keuze voor de toepassing. We merkt ook dat alleen 2% van onze tenants consistentieniveaus op basis van per aanvraag negeren. 

Leesbewerkingen geleverd op consistente voorvoegsel-sessie en uiteindelijke consistentie zijn twee keer als goedkope als leesbewerkingen met sterke of gebonden veroudering consistentie in Cosmos-database. Cosmos DB heeft toonaangevende uitgebreide 99,99% serviceovereenkomsten inclusief consistentie wordt gegarandeerd samen met de beschikbaarheid, doorvoer en latentie. Gebruiken we een [linearizability checker](http://dl.acm.org/citation.cfm?id=1806634), die continu werkt via onze service Telemetrie en eventuele schendingen consistentie tooyou openbaar-rapporten. Voor gebonden veroudering, we bewaken en rapporteren eventuele schendingen duurde en t grenzen. Voor alle vijf beperkte consistentieniveaus, we ook Hallo rapporteren [probabilistische gebonden veroudering metriek](http://dl.acm.org/citation.cfm?id=2212359) rechtstreeks tooyou.  

## <a name="scope-of-consistency"></a>Bereik van de consistentie
Hallo granulatie van de consistentie is binnen het bereik tooa één gebruikersaanvraag. Een schrijfaanvraag mogelijk komen overeen tooan insert, replace, upsert of te verwijderen van de transactie. Net als bij schrijfbewerkingen en wordt een transactie lezen/query ook bereik tooa één gebruikersaanvraag. Hallo-gebruiker is mogelijk vereist toopaginate via een grote resultatenset, spanning meerdere partities, maar elk gelezen transactie bereik tooa één pagina en aangeboden via binnen één partitie.

## <a name="consistency-levels"></a>Consistentieniveaus
U kunt een standaardniveau voor consistentiecontrole configureren op uw databaseaccount die van toepassing is tooall verzamelingen (en databases) onder uw account Cosmos DB. Gebruiker gedefinieerde resources gebruiken standaard alle leesbewerkingen en query's die zijn uitgegeven voor Hallo Hallo consistentie standaardniveau opgegeven op het Hallo-databaseaccount. U kunt Hallo consistentieniveau van een specifieke lezen/query versoepelen aanvragen in elk Hallo met behulp van API's ondersteund. Er zijn vijf typen ondersteund door hello Azure Cosmos DB replicatie protocol consistentieniveaus die een duidelijke compromis tussen specifieke consistentie wordt gegarandeerd en prestaties, bieden zoals beschreven in deze sectie.

**Sterke**: 

* Sterke consistentie biedt een [linearizability](https://aphyr.com/posts/313-strong-consistency-models) garantie Hello leest gegarandeerde tooreturn Hallo meest recente versie van een item. 
* Sterke consistentie wordt gegarandeerd dat een schrijfbewerking is alleen zichtbaar nadat deze definitief is vastgelegd door Hallo meerderheid quorum van replica's. Een schrijfbewerking ofwel synchroon definitief is vastgelegd door zowel primaire Hallo Hallo quorum van secundaire replica's of deze is afgebroken. Lees altijd meerderheid Hallo lezen quorum is bevestigd, een client nooit het terugschrijven van een niet-doorgevoerde of gedeeltelijke kan zien en altijd tooread Hallo laatste erkende schrijven kan worden gegarandeerd. 
* Azure DB Cosmos-accounts die geconfigureerd toouse sterke consistentie zijn kunnen niet meer dan één Azure-regio koppelen aan hun Azure DB die Cosmos-account. 
* Hallo kosten van een leesbewerking (in termen van [aanvraageenheden](request-units.md) verbruikt) met sterke consistentie is hoger dan de sessie en mogelijk, maar dezelfde Hallo als gebonden veroudering.

**Gebonden veroudering**: 

* Consistentie voor gebonden veroudering wordt gegarandeerd dat Hallo leesbewerkingen schrijfbewerkingen door maximaal achterblijven *K* versies of voorvoegsels van een item of *t* tijdsinterval blijft. 
* Daarom bij het kiezen van gebonden veroudering, Hallo 'veroudering' kan worden geconfigureerd op twee manieren: aantal versies *K* van Hallo item waarmee Hallo leesbewerkingen lag achter Hallo geschreven en Hallo tijdsinterval *t* 
* Gebonden veroudering aanbiedingen totale algemene volgorde, behalve binnen Hallo 'veroudering venster'. Hallo monotone lezen garanties bestaat binnen een regio zowel binnen als buiten Hallo 'veroudering venster'. 
* Gebonden veroudering biedt een betere consistentie garantie dan sessie of uiteindelijke consistentie. Globaal gedistribueerde toepassingen, wordt u aangeraden dat u gebonden veroudering voor scenario's waarbij u zou doen toohave sterke consistentie, zoals maar ook 99,99% beschikbaarheid en lage latentie wilt gebruiken. 
* Azure DB Cosmos-accounts die zijn geconfigureerd met consistentie voor gebonden veroudering kunnen een onbeperkt aantal Azure-regio's koppelen aan hun Azure DB die Cosmos-account. 
* kosten van een leesbewerking (in termen van RUs verbruikt) met Hallo gebonden veroudering is hoger dan de sessie en uiteindelijke consistentie, maar dezelfde Hallo als sterke consistentie.

**Sessie**: 

* In tegenstelling tot Hallo globale consistentie modellen die worden aangeboden door consistentieniveaus sterk en gebonden veroudering is sessieconsistentie binnen het bereik tooa clientsessie. 
* Sessieconsistentie is ideaal voor alle scenario's waarbij een apparaat of gebruiker sessie omdat garant monotone leest, monotone schrijfbewerkingen en lezen wordt gegarandeerd dat uw eigen schrijfbewerkingen (RYW) is betrokken. 
* Sessieconsistentie voorziet in voorspelbare consistentie voor een sessie en maximale doorvoer en biedt tegelijkertijd de laagste latentie voor schrijfbewerkingen Hallo en leesbewerkingen gelezen. 
* Azure DB Cosmos-accounts die zijn geconfigureerd met de sessieconsistentie kunnen een onbeperkt aantal Azure-regio's koppelen aan hun Azure DB die Cosmos-account. 
* Hallo kosten van een leesbewerking (in termen van RUs verbruikt) met sessie consistentieniveau kleiner dan sterk en gebonden veroudering, maar meer dan uiteindelijke consistentie is

<a id="consistent-prefix"></a>
**Consistente voorvoegsel**: 

* Consistente voorvoegsel wordt gegarandeerd dat zolang er verder geen schrijfbewerkingen, Hallo replica's binnen Hallo groep uiteindelijk geconvergeerd. 
* Consistente voorvoegsel wordt gegarandeerd dat leesbewerkingen nooit volgorde schrijfbewerkingen te zien. Als schrijfbewerkingen zijn uitgevoerd in de volgorde Hallo `A, B, C`, en vervolgens een client een ziet `A`, `A,B`, of `A,B,C`, maar nooit volgorde zoals `A,C` of `B,A,C`.
* Azure DB Cosmos-accounts die zijn geconfigureerd met consistente voorvoegsel consistentiecontrole kunnen een onbeperkt aantal Azure-regio's koppelen aan hun account Azure Cosmos DB. 

**Uiteindelijke**: 

* Uiteindelijke consistentie wordt gegarandeerd dat zolang er verder geen schrijfbewerkingen, Hallo replica's binnen Hallo groep uiteindelijk geconvergeerd. 
* Uiteindelijke consistentie is Hallo zwakste vorm van consistentie waar een client Hallo-waarden die ouder zijn dan Hallo die was eerder kan verkrijgen.
* Uiteindelijke consistentie voorziet Hallo zwakste lezen van consistentie maar aanbiedingen hello laagste latentie voor zowel lees- en schrijfbewerkingen.
* Azure DB Cosmos-accounts die zijn geconfigureerd met uiteindelijke consistentie kunnen een onbeperkt aantal Azure-regio's koppelen aan hun Azure DB die Cosmos-account. 
* Hallo kosten van een leesbewerking (in termen van RUs verbruikt) met uiteindelijke consistentie Hallo niveau Hallo laagste van alle hello Azure DB die Cosmos-consistentieniveaus is.

## <a name="configuring-hello-default-consistency-level"></a>Hallo-standaardniveau voor consistentiecontrole configureren
1. In Hallo [Azure-portal](https://portal.azure.com/), Snelbalk Hallo in, klik op **Azure Cosmos DB**.
2. In Hallo **Azure Cosmos DB** blade, selecteer Hallo database account toomodify.
3. Klik op Hallo accountblade **consistentie standaard**.
4. In Hallo **standaard consistentie** blade, selecteer Hallo nieuwe consistentieniveau en klik op **opslaan**.
   
    ![Schermopname Hallo Instellingenpictogram en consistentie standaard vermelding markeren](./media/consistency-levels/database-consistency-level-1.png)

## <a name="consistency-levels-for-queries"></a>Consistentieniveaus voor query 's
Standaard voor bronnen die door de gebruiker gedefinieerde consistentieniveau Hallo voor query's is Hallo dezelfde Hallo consistentieniveau voor lezen. Hallo-index wordt standaard synchroon bijgewerkt op elke invoegen, vervangen of verwijderen van een item toohello Cosmos-DB-container. Deze kan Hallo query's toohonor Hallo dezelfde consistentieniveau als die van leesbewerkingen verwijzen. Hoewel Azure Cosmos DB geoptimaliseerd voor schrijven is en volgehouden volumes van schrijfbewerkingen, synchrone index onderhoud ten behoeve van consistente query's ondersteunt, kunt u bepaalde verzamelingen tooupdate de index traag. Vertraagde indexeren verdere verhoogt de schrijfprestaties Hallo en is ideaal voor bulksgewijs opname scenario's wanneer een werkbelasting voornamelijk lezen zware.  

| Indexeren van modus | Leesbewerkingen | Query's |
| --- | --- | --- |
| Consistente (standaard) |Selecteer een van de sterk, gebonden veroudering, sessie, consistente voorvoegsel of uiteindelijke |Selecteer een van de sterk, gebonden-verouderd, sessie of uiteindelijke |
| Vertraagde |Selecteer een van de sterk, gebonden veroudering, sessie, consistente voorvoegsel of uiteindelijke |Mogelijk |
| Geen |Selecteer een van de sterk, gebonden veroudering, sessie, consistente voorvoegsel of uiteindelijke |Niet van toepassing |

Als met leesaanvragen, kunt u Hallo consistentieniveau van een specifieke query-aanvraag in elke API verlagen.

## <a name="next-steps"></a>Volgende stappen
Als u toodo meer lezen over consistentieniveaus en -en nadelen wilt, raden we Hallo resources te volgen:

* Doug Terry. Consistentie van de gerepliceerde gegevens toegelicht door middel van baseball (video).   
  [https://www.YouTube.com/Watch?v=gluIh8zd26I](https://www.youtube.com/watch?v=gluIh8zd26I)
* Doug Terry. Consistentie van de gerepliceerde gegevens worden via baseball beschreven.   
  [http://Research.Microsoft.com/pubs/157411/ConsistencyAndBaseballReport.PDF](http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf)
* Doug Terry. Sessie garanties met betrekking tot zwak consistente gerepliceerde gegevens.   
  [http://DL.ACM.org/Citation.cfm?id=383631](http://dl.acm.org/citation.cfm?id=383631)
* Daniel Abadi. Consistentiecontrole voor-en nadelen in moderne gedistribueerde Database systemen ontwerp: KAPJE wordt slechts een deel van verhaal Hallo ".   
  [http://computer.org/CSDL/mags/CO/2012/02/mco2012020037-ABS.HTML](http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html)
* Peter Bailis, Shivaram Venkataraman, Michael J. Franklin, Joseph Dhr Hellerstein, bewaartermijn Stoica. Probabilistische begrensd veroudering (PBS) voor praktische gedeeltelijke quorum.   
  [http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.PDF](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
* Werner Vogels. Uiteindelijke Consistent - herzien.    
  [http://allthingsdistributed.com/2008/12/eventually_consistent.HTML](http://allthingsdistributed.com/2008/12/eventually_consistent.html)
* Monitoring Naor, Avishai wol Hallo Load, capaciteit en beschikbaarheid van Quorum systemen, SIAM journaal op Computing, v.27 n.2, p.423-447, April 1998.
  [http://epubs.siam.org/DOI/ABS/10.1137/S0097539795281232](http://epubs.siam.org/doi/abs/10.1137/S0097539795281232)
* Sebastian Burckhardt, Chris Dern, Macanal Musuvathi, Roy Tan, de configuratie: een volledige en automatische linearizability checker, verslag van Hallo 2010 ACM SIGPLAN Conferentie over het programmeren van taal ontwerpen en implementeren, juni 05 10 2010 Toronto, Ontario, Canada [doi > 10.1145/1806596.1806634] [http://dl.acm.org/citation.cfm?id=1806634](http://dl.acm.org/citation.cfm?id=1806634)
* Peter Bailis, Shivaram Venkataraman, Michael J. Franklin, Joseph M. Hellerstein, bewaartermijn Stoica, Probabilistically gebonden veroudering voor praktische gedeeltelijke quorum procedure Hallo VLDB ter beschikking, v.5 n.8, April 2012 met p.776 787 [http:// DL.ACM.org/Citation.cfm?id=2212359](http://dl.acm.org/citation.cfm?id=2212359)
