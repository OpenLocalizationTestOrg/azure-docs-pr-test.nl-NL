---
title: aaaDistribute gegevens globaal met Azure Cosmos DB | Microsoft Docs
description: Meer informatie over de wereld scale geo-replicatie, failover en gegevens herstellen met globale databases van Azure Cosmos DB, een globaal gedistribueerd, zijn voor het model database-service.
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: ba5ad0cc-aa1f-4f40-aee9-3364af070725
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/14/2017
ms.author: arramac
ms.openlocfilehash: b50e8433dc7e70c54d68c4c2f99954a13f4951f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodistribute-data-globally-with-azure-cosmos-db"></a>Hoe toodistribute gegevens globaal met Azure Cosmos-DB
Azure is alomtegenwoordige - heeft een algemene footprint tussen 30 + geografische regio's en continu groter wordt. Met de wereldwijde aanwezigheid is een van de Hallo allemaal een andere mogelijkheden die Azure ontwikkelaars tooits biedt mogelijkheid toobuild hello, implementeren en globaal gedistribueerde toepassingen eenvoudig te beheren. 

[Azure Cosmos DB](../cosmos-db/introduction.md) is de wereldwijd gedistribueerde databaseservice met meerdere modellen van Microsoft voor essentiële toepassingen. Azure Cosmos DB biedt klare distributielijsten [elastisch schalen van doorvoer en opslag](../cosmos-db/partition-data.md) overal ter wereld, één cijfer milliseconde latenties op Hallo 99th percentiel, [vijf goed gedefinieerde consistentieniveaus ](consistency-levels.md), hoge beschikbaarheid, alle back-ups door gegarandeerd [toonaangevende Sla's](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure Cosmos DB [indexeert automatisch gegevens](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) zonder dat u toodeal met schema- en management. Azure Cosmos DB beschikt over meerdere modellen en ondersteunt modellen voor document-, sleutelwaarde-, grafiek- en kolomgegevens. Als een service cloud geboren is Azure Cosmos DB zorgvuldig ontworpen met multi-tenancymodus en globale verdeling van Hallo gemalen.

**Één Azure Cosmos DB verzameling gepartitioneerd en verdeeld over meerdere Azure-regio 's**

![Azure DB Cosmos-verzameling is gepartitioneerd en verdeeld over drie gebieden](./media/distribute-data-globally/global-apps.png)

Als er tijdens het maken van Azure DB die Cosmos hebt geleerd, toe te voegen globale verdeling kan niet worden pas achteraf overwogen - deze mag niet 'bout eenmalige aanmelding' op een systeem van de database "één site". Hallo-mogelijkheden die worden aangeboden door een wereldwijd gedistribueerde database span afgezien van dat van traditionele geografische disaster recovery (geografisch DR) die worden aangeboden door 'één site' databases. Databases van één site Geo-DR-mogelijkheid bieden zijn een strikte subset van globaal gedistribueerde databases. 

Met Azure Cosmos DB klare globale verdeling ontwikkelaars hebben geen toobuild hun eigen steigers replicatie door middel van beide Hallo Lambda-patroon (bijvoorbeeld [AWS DynamoDB replicatie](https://github.com/awslabs/dynamodb-cross-region-library/blob/master/README.md)) via het databaselogboek Hallo of door tijdens het doorzoeken van 'dubbele schrijfbewerkingen' over meerdere regio's. We niet raden deze benaderingen omdat het onmogelijk tooensure juistheid van deze methoden en geluid Sla's bieden. 

In dit artikel bieden we een overzicht van Azure Cosmos DB algemene distributie-mogelijkheden. We beschrijven ook Azure Cosmos DB unieke benadering tooproviding uitgebreide Sla's. 

## <a id="EnableGlobalDistribution"></a>Klare globale distributiepunt inschakelen
Azure Cosmos DB biedt de volgende Hallo wereld scale toepassingen schrijven voor mogelijkheden tooenable u tooeasily. Deze mogelijkheden zijn beschikbaar via hello Azure Cosmos DB van resource provider gebaseerde [REST-API's](https://docs.microsoft.com/rest/api/documentdbresourceprovider/) evenals hello Azure-portal.

### <a id="RegionalPresence"></a>De alomtegenwoordige regionale aanwezigheid 
Azure is de geografische aanwezigheid voortdurend groeiende doordat [nieuwe gebieden](https://azure.microsoft.com/regions/) online. Azure Cosmos DB is beschikbaar in alle nieuwe Azure-regio's standaard. Hiermee kunt u een geografische regio met uw Azure DB die Cosmos-databaseaccount tooassociate als Azure nieuw gebied hello voor bedrijven wordt geopend.

**Azure Cosmos DB is beschikbaar in alle Azure-regio's standaard**

![Azure Cosmos DB beschikbaar op alle Azure-regio 's](./media/distribute-data-globally/azure-regions.png)

### <a id="UnlimitedRegionsPerAccount"></a>Een onbeperkt aantal regio's koppelen aan uw Azure DB die Cosmos-databaseaccount
Azure Cosmos-database kunt u tooassociate een willekeurig aantal Azure-regio's met uw Azure-Cosmos-DB account database. Er zijn geen beperkingen op het aantal regio's die gekoppeld aan uw Azure DB die Cosmos-databaseaccount worden kunnen Hallo buiten geofencing beperkingen (bijvoorbeeld de Duitse, China). Hallo volgende afbeelding ziet u een database-account geconfigureerd toospan over 25 Azure-regio's.  

**Een tenant Azure Cosmos DB database account spanning 25 Azure-regio 's**

![Azure DB Cosmos-databaseaccount spanning 25 Azure-regio 's](./media/distribute-data-globally/spanning-regions.png)

### <a id="PolicyBasedGeoFencing"></a>Geofencing op basis van beleid
Azure Cosmos DB is ontworpen toohave op basis van beleid geofencing-mogelijkheden. Geofencing is een belangrijk onderdeel tooensure gegevens bestuur en naleving beperkingen waardoor mogelijk een specifiek gebied koppelen aan uw account. Voorbeelden van geofencing bevatten (maar niet beperkt tot), scoping globale distributie toohello regio's binnen een soevereine cloud (bijvoorbeeld China en Duitsland) of binnen een grens van een government belasting (bijvoorbeeld, Australië). Hallo-beleid worden beheerd met behulp van de metagegevens Hallo van uw Azure-abonnement.

### <a id="DynamicallyAddRegions"></a>Dynamisch toevoegen en verwijderen van de regio 's
Azure Cosmos-database kunt u tooadd (koppelen) of verwijderen (ontkoppelen) regio's tooyour databaseaccount op elk gewenst moment (Zie [voorgaande afbeelding](#UnlimitedRegionsPerAccount)). Doordat het repliceren van gegevens meerdere partities parallel Azure Cosmos DB zorgt ervoor dat wanneer een nieuw gebied online wordt gezet, Azure Cosmos DB beschikbaar binnen 30 minuten een willekeurige plaats in Hallo wereld voor up too100 TBs. 

### <a id="FailoverPriorities"></a>Failover-prioriteiten
exacte reeks regionale failover wanneer er een storing meerdere regionale Azure Cosmos DB toocontrol kunt u tooassociate Hallo prioriteit toovarious regio's die zijn gekoppeld aan het databaseaccount hello (Zie de volgende afbeelding Hallo). Azure Cosmos DB zorgt ervoor dat Hallo automatische failover gebeurt in volgorde van prioriteit Hallo die u hebt opgegeven. Zie voor meer informatie over regionale failovers [automatische regionale failovers voor bedrijfscontinuïteit in Azure Cosmos DB](regional-failover.md).

**Een tenant van Azure DB die Cosmos kunt Hallo failover prioriteitsvolgorde (rechterdeelvenster) voor de regio's die zijn gekoppeld aan een databaseaccount configureren**

![Failover prioriteiten configureren met Azure Cosmos-DB](./media/distribute-data-globally/failover-priorities.png)

### <a id="OfflineRegions"></a>Een regio dynamisch 'offline' moet worden gezet
Azure Cosmos-database kunt u tootake de database offline account in een specifieke regio en later weer online brengen. Gebieden gemarkeerd offline niet actief deelnemen aan replicatie en maken geen deel uit van Hallo failover-reeks. Hiermee kunt u toofreeze Hallo laatst bekende goede database installatiekopie in een Hallo regio's te lezen voordat tooyour toepassing mogelijk schadelijke rolling upgrades.

### <a id="ConsistencyLevels"></a>Meerdere, goed gedefinieerde consistentie modellen voor algemeen gerepliceerde databases
Beschrijft de Azure Cosmos DB [meerdere goed gedefinieerde consistentieniveaus](consistency-levels.md) back-up Sla's. U kunt een specifieke consistentie model (uit Hallo lijst met beschikbare opties), afhankelijk van werkbelasting Hallo/scenario's. 

### <a id="TunableConsistency"></a>Instelbare consistentie voor globaal gerepliceerde databases
Azure Cosmos-database kunt u tooprogrammatically onderdrukking en versoepelen Hallo standaardkeuze consistentie op basis van per aanvraag, tijdens runtime. 

### <a id="DynamicallyConfigurableReadWriteRegions"></a>Dynamisch configureerbare lezen en schrijven regio 's
Azure Cosmos DB, kunt u tooconfigure Hallo regio's (gekoppeld aan het Hallo-database) voor 'lezen', 'schrijven' of ' lezen/schrijven' regio's. 

### <a id="ElasticallyScaleThroughput"></a>Elastisch schalen doorvoer op Azure-regio 's
U kunt schalen een verzameling Azure Cosmos DB door inrichting doorvoer programmatisch. Hallo-doorvoer is toegepaste tooall Hallo gebieden Hallo verzameling wordt gedistribueerd in.

### <a id="GeoLocalReadsAndWrites"></a>Geo-local leest en schrijft
Hallo belangrijk voordeel van een globaal gedistribueerde database is toooffer lage latentie toegang tot toohello gegevens overal ter wereld Hallo. Azure Cosmos DB biedt lage latentie garanties op P99 voor verschillende databasebewerkingen. Dit zorgt ervoor dat alle leesbewerkingen gerouteerde toohello dichtstbijzijnde lokale lezen regio. tooserve een leesaanvraag Hallo quorum lokale toohello regio waarin Hallo lezen is uitgegeven wordt gebruikt; Hallo geldt toohello schrijfbewerkingen. Een schrijfbewerking is bevestigd pas nadat een meerderheid van replica's blijvend Hallo schrijven heeft toegekend lokaal maar zonder op externe replica's tooacknowledge Hallo schrijfbewerkingen wordt geregeld. Anders gezegd, opereert Hallo replicatie protocol van Azure DB die Cosmos onder Hallo veronderstelling dat Hallo lezen en schrijven quorum zijn altijd lokale toohello lezen en schrijven van de regio's, respectievelijk in welke Hallo-aanvraag is uitgegeven.

### <a id="ManualFailover"></a>Handmatig starten van regionale failover
Azure Cosmos-database kunt u tootrigger Hallo failover Hallo database account toovalidate Hallo *tooend eindigen* eigenschappen van de beschikbaarheid van de gehele toepassing hello (anders dan Hallo database). Aangezien beide Hallo veiligheid en liveness eigenschappen van detectie en opvulteken keuze van Hallo fout gegarandeerd, wordt gegarandeerd dat Azure Cosmos DB *nul gegevensverlies* voor het uitvoeren van een handmatige failover-tenant is gestart.

### <a id="AutomaticFailover"></a>Automatische failover
Azure Cosmos DB ondersteunt automatische failover in geval van een of meer regionale uitval. Tijdens een regionale failover houdt Azure Cosmos DB de lezen latentie, bedrijfstijd beschikbaarheid, consistentie en doorvoer Sla's. Azure Cosmos DB biedt een bovengrens op Hallo duur van een automatische failover bewerking toocomplete. Dit is Hallo venster van mogelijk gegevensverlies tijdens Hallo regionale uitval.

### <a id="GranularFailover"></a>Ontworpen voor verschillende failover granulaties
Momenteel Hallo automatische en handmatige failover mogelijkheden beschikbaar Hallo samenvattingen van Hallo databaseaccount. Opmerking, intern Azure Cosmos DB is ontworpen toooffer *automatische* failover fijner samenvattingen van een database, de verzameling of zelfs een partitie (van een verzameling die eigenaar is van een bereik van sleutels). 

### <a id="MultiHomingAPIs"></a>Multihoming API's in Azure Cosmos DB
Azure Cosmos-database kunt u toointeract met Hallo-database met een logische (regio networkdirect) of fysieke (regiospecifieke)-eindpunten. Logische eindpunten zorgt ervoor dat de toepassing hello transparant multihomed in geval van een failover worden kan. Hallo laatstgenoemde, fysieke eindpunten, bieden nauwkeuriger beheer toohello toepassing tooredirect leest en schrijft toospecific regio's.

U vindt meer informatie over hoe tooconfigure voorkeuren voor Hallo Lees [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md), [Graph API](../cosmos-db/tutorial-global-distribution-graph.md), [tabel API](../cosmos-db/tutorial-global-distribution-table.md), en [MongoDB API](../cosmos-db/tutorial-global-distribution-mongodb.md)in hun respectieve gekoppeld artikelen.

### <a id="TransparentSchemaMigration"></a>De schema- en migratie transparant en consistent database 
Azure Cosmos DB is volledig [schema networkdirect](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf). Hallo uniek ontwerp van de database-engine toestaat dat deze tooautomatically en alle Hallo gegevens het opgenomen zonder dat een schema of secundaire indexen van u synchroon te indexeren. Dit kunt u tooiterate uw globaal gedistribueerde toepassing snel zonder dat u de migratie van de schema- en index van de database of de coördinatie van meerdere fase toepassingsimplementaties van wijzigingen in het schema. Azure Cosmos DB zorgt ervoor dat eventuele wijzigingen tooindexing beleidsregels expliciet door u uitgevoerde resulteert niet in een vermindering van prestaties of beschikbaarheid.  

### <a id="ComprehensiveSLAs"></a>Uitgebreide Sla's (anders dan alleen hoge beschikbaarheid)
Als een globaal gedistribueerde database-service biedt Azure Cosmos DB goed gedefinieerde SLA voor **verlies van gegevens**, **beschikbaarheid**, **latentieperiode P99**, **doorvoer**  en **consistentie** voor de database als geheel, ongeacht het aantal gebieden die zijn gekoppeld aan de database Hallo HALLO hallo.  

## <a id="LatencyGuarantees"></a>Latentie garanties
Hallo belangrijk voordeel van een globaal gedistribueerde database-service, zoals Azure Cosmos DB zijn toooffer lage latentie toegang tooyour gegevens overal in Hallo wereld. Azure Cosmos DB biedt gegarandeerde lage latentie op P99 voor verschillende databasebewerkingen. Hallo replicatie protocol die gebruikmaakt van Azure DB die Cosmos zorgt ervoor dat Hallo databasebewerkingen (in het ideale geval leest en schrijft) worden altijd uitgevoerd in Hallo regio lokale toothat van Hallo-client. Hallo latentie die Sla Azure Cosmos DB bevat P99 voor zowel leest, (synchroon) geïndexeerde schrijfbewerkingen en wordt opgevraagd voor verschillende grootten voor aanvraag en -antwoord. Hallo latentie garanties met betrekking tot schrijfbewerkingen bevatten duurzame meerderheid quorum doorvoeracties binnen Hallo lokale datacentrum.

### <a id="LatencyAndConsistency"></a>Latentie van relatie met consistentiecontrole 
Voor een globaal gedistribueerde service toooffer sterke consistentie in een globaal gedistribueerde installatie, moet toosynchronously repliceren Hallo schrijfbewerkingen of synchrone regio-overschrijdende leesbewerkingen – Hallo snelheid van licht en Hallo wide area network betrouwbaarheid vereisen uitvoeren die sterke consistentie resulteert in hoge latentie en lage beschikbaarheid van databasebewerkingen. Hallo-service moet daarom in volgorde toooffer gegarandeerd lage latenties op P99 en 99.99 beschikbaarheid, alvast asynchrone replicatie. Deze beurt vereist dat de service Hallo ook bieden moet [goed gedefinieerde, beperkte consistentie choice(s)](consistency-levels.md) – zwakkere dan sterk (toooffer lage latentie en beschikbaarheid garanties) en in het ideale geval sterker zijn dan ('uiteindelijke' consistentie toooffer een intuïtieve programmeermodel).

Azure Cosmos DB zorgt ervoor dat een leesbewerking niet vereist toocontact replica's in meerdere regio's toodeliver Hallo specifieke consistentie niveau garantie. Ook kan Hiermee zorgt u ervoor dat een schrijfbewerking komt niet ophalen wordt geblokkeerd terwijl Hallo gegevens wordt gerepliceerd in alle regio's voor hello (dat wil zeggen schrijfbewerkingen zijn asynchroon gerepliceerd tussen regio's). Meerdere beperkte consistentieniveaus zijn beschikbaar voor accounts voor meerdere landen/regio-database. 

### <a id="LatencyAndAvailability"></a>Latentie van relatie met de beschikbaarheid van 
Beschikbaarheid en latentie zijn twee zijden Hallo Hallo dezelfde medaille. We hebben over de latentie van Hallo-bewerking in de actieve status en beschikbaarheid in Hallo face van fouten. Uit oogpunt van de toepassing hello wordt traag uitgevoerd een databasebewerking te onderscheiden van een database die niet beschikbaar is. 

hoge latentie toodistinguish uit niet beschikbaar zijn, Azure Cosmos DB biedt een absolute bovengrens voor de latentie van verschillende databasebewerkingen. Als de databasebewerking Hallo langer dan Hallo bovengrens toocomplete duurt, retourneert Azure Cosmos DB een time-outfout. Hello Azure Cosmos DB beschikbaarheids-SLA zorgt ervoor dat time-outs Hallo tegen Hallo beschikbaarheids-SLA worden geteld. 

### <a id="LatencyAndThroughput"></a>Latentie van relatie met doorvoer
Azure Cosmos-database maakt geen u kiezen tussen latentie en doorvoer. Het Hallo-SLA voor beide latentieperiode P99 respecteert en leveren Hallo doorvoer die u hebt ingericht. 

## <a id="ConsistencyGuarantees"></a>Consistentie wordt gegarandeerd
Tijdens het Hallo [sterke consistentie model](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) is Hallo goud standaard van programmeerbaarheid, deze wordt gezet op Hallo steile prijs van hoge latentie (in de actieve status) en verlies van beschikbaarheid (in Hallo face van fouten). 

Azure Cosmos DB biedt met een goed gedefinieerde programming model tooyou tooreason over consistentie van de gerepliceerde gegevens. In volgorde tooenable u toobuild multihomed toepassingen, Hallo consistentie modellen die worden weergegeven door Azure Cosmos DB ontworpen toobe regio-networkdirect zijn en niet afhankelijk is van het Hallo-regio waar Hallo lees- en schrijfbewerkingen worden geleverd. 

SLA voor Azure Cosmos-DB-consistentie wordt gegarandeerd dat dat 100% van leesaanvragen voldoen aan de Hallo consistentie garantie voor Hallo consistentieniveau aangevraagd door u ofwel (Hallo consistentie standaardniveau op Hallo databaseaccount of hallo overschreven waarde op Hallo-aanvraag ). Een leesaanvraag als toohave voldaan Hallo consistentie SLA beschouwd als alle Hallo consistentie wordt gegarandeerd Hallo consistentieniveau gekoppeld is voldaan. Hallo bevat volgende tabel Hallo consistentie wordt gegarandeerd dat toospecific consistentieniveaus die worden aangeboden door Azure Cosmos DB overeenkomen.

**Consistentie wordt gegarandeerd die zijn gekoppeld aan een bepaalde consistentieniveau in Azure Cosmos-DB**

<table>
    <tr>
        <td><strong>Consistentieniveau</strong></td>
        <td><strong>Consistentie kenmerken</strong></td>
        <td><strong>SLA</strong></td>
    </tr>
    <tr>
        <td rowspan="3">Sessie</td>
        <td>Lezen van uw eigen schrijven</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Monotone lezen</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Consistente voorvoegsel</td>
        <td>100%</td>
    </tr>
    <tr>
        <td rowspan="3">Gebonden veroudering</td>
        <td>Monotone gelezen (binnen een regio)</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Consistente voorvoegsel</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Gebonden veroudering &lt; K, T</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Consistente voorvoegsel</td>
        <td>Consistente voorvoegsel</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Sterk</td>
        <td>Linearizable</td>
        <td>100%</td>
    </tr>
</table>

### <a id="ConsistencyAndAvailability"></a>Relatie van de consistentie met beschikbaarheid
Hallo [onmogelijk resultaat](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) Hallo [CAP stelling van](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf) blijkt dat het inderdaad onmogelijk op Hallo system tooremain beschikbaar en linearizable consistentie van de aanbieding in Hallo face van fouten is. Hallo database-service moet kiezen toobe CP of AP - CP systemen beschikbaarheid voor linearizable consistentie beheercluster terwijl Hallo Azië systemen beheercluster [linearizable consistentie](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) voor beschikbaarheid. Azure Cosmos DB nooit is in strijd met Hallo aangevraagd consistentieniveau, waardoor formeel een CP-systeem. Echter, in de praktijk consistentiecontrole is niet een toegevoegde alles of niets: Er zijn meerdere goed gedefinieerde consistentie modellen langs Hallo consistentie spectrum tussen linearizable en uiteindelijke consistentie. In Azure Cosmos DB we tooidentify hebben geprobeerd meerdere Hallo consistentie modellen versoepeld met concrete toepasselijkheid en een intuïtieve programmeermodel. Azure Cosmos DB navigeert voor-en nadelen Hallo consistentie beschikbaarheid door het aanbieden van 99.99 beschikbaarheid SLA samen met [meerdere versoepeld nog goed gedefinieerde consistentieniveaus](consistency-levels.md). 

### <a id="ConsistencyAndAvailability"></a>Consistentie van relatie met een latentie
Een uitgebreidere variatie CAP is voorgesteld door Prof. Daniel Abadi en deze wordt aangeroepen [PACELC](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf), die ook is verantwoordelijk voor de latentie en consistentie-en nadelen in de actieve status. Vermeld dat in de actieve status, moet Hallo database system kiezen tussen de consistentie en latentie. Azure Cosmos DB met meerdere beperkte consistentie modellen (ondersteund door de asynchrone replicatie en lokale lezen, schrijven quorum), zorgt u ervoor dat alle lees- en schrijfbewerkingen lokale toohello lezen zijn en regio's respectievelijk schrijven.  Hiermee wordt gegarandeerd dat Azure Cosmos DB toooffer lage latentie binnen de regio Hallo voor consistentieniveaus Hallo.  

### <a id="ConsistencyAndThroughput"></a>De relatie van de consistentie met doorvoer
Omdat Hallo-implementatie van een specifieke consistentie-model, is afhankelijk van Hallo keuze van een [quorumtype](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf), Hallo doorvoer ook varieert op basis van Hallo keuze van de consistentie. Bijvoorbeeld, in Azure Cosmos DB is hello doorvoer met sterke consistent leesbewerkingen ongeveer half toothat uiteindelijk consistent leesbewerkingen. 
 
**Relatie van meer capaciteit voor een specifieke consistentieniveau in Azure Cosmos-DB**

![Relatie tussen de consistentie en doorvoer](./media/distribute-data-globally/consistency-and-throughput.png)

## <a id="ThroughputGuarantees"></a>Doorvoer garanties 
Azure Cosmos-database kunt u tooscale doorvoer (evenals, opslag), elastisch over verschillende regio's, afhankelijk van het Hallo-aanvraag. 

**Één Azure Cosmos DB verzameling gepartitioneerd (in drie shards) en vervolgens verdeeld over drie Azure-regio 's**

![Azure Cosmos DB gedistribueerd en gepartitioneerde verzamelingen](../cosmos-db/media/introduction/azure-cosmos-db-global-distribution.png)

Een verzameling Azure Cosmos DB opgehaald gedistribueerd met behulp van twee dimensies – binnen een regio en vervolgens tussen regio's. Dit doet u al volgt: 

* In één regio is een verzameling Azure Cosmos DB uitgebreid in termen van de resource-partities. Elke partitie resource beheert een set van sleutels en sterke consistent en maximaal beschikbaar is op grond van de replicatie van machine staat tussen een set van replica's. Azure Cosmos-database is een systeem volledig resource geregeld waar een resource-partitie is verantwoordelijk voor het leveren van een deel van de doorvoer voor Hallo budget van system resources toegewezen tooit. Hallo schalen van een verzameling Azure Cosmos DB is volledig transparant – Azure Cosmos DB Hallo resource partities beheert en splitst en zo nodig Hiermee worden samengevoegd. 
* Alle partities van Hallo resource wordt vervolgens verdeeld over meerdere regio's. Resource partities die eigenaar is van dezelfde reeks sleutels op verschillende gebieden formulier partitieset Hallo (Zie [voorgaande afbeelding](#ThroughputGuarantees)).  Resource partities binnen een partitieset worden gecoördineerd met replicatie van machine staat voor Hallo meerdere regio's. Afhankelijk van Hallo consistentieniveau geconfigureerd, zijn Hallo resource partities binnen een partitieset geconfigureerd dynamisch met verschillende topologieën (bijvoorbeeld ster, keten, structuur enz.). 

Doordat een uiterst responsieve partitie management, taakverdeling en strikte resource beheeracties, Azure Cosmos DB, kunt u tooelastically scale doorvoer over meerdere Azure-regio's op een verzameling Azure Cosmos DB. Veranderende doorvoer op een verzameling is een Runtimebewerking in Azure DB die Cosmos - zoals met andere databasebewerkingen die Hallo absolute bovengrens voor de latentie voor uw aanvraag toochange Hallo doorvoer wordt gegarandeerd dat Azure Cosmos DB. Bijvoorbeeld ziet Hallo volgende afbeelding u verzameling van een klant met elastisch ingerichte doorvoer (variëren van 1-10M aanvragen per seconde tussen twee regio's) op basis van vraag Hallo.
 
**Een klant-verzameling met elastisch ingerichte doorvoer (1-10M aanvragen per seconde)**

![Elastisch ingerichte doorvoer Azure Cosmos-DB](./media/distribute-data-globally/elastic-throughput.png)

### <a id="ThroughputAndConsistency"></a>Doorvoer van relatie met consistentiecontrole 
Hetzelfde als [relatie van de consistentie met doorvoer](#ConsistencyAndThroughput).

### <a id="ThroughputAndAvailability"></a>Relatie met de beschikbaarheid van de doorvoer
Azure Cosmos DB blijft toomaintain de beschikbaarheid wanneer hello om toohello doorvoer wordt gewijzigd. Azure Cosmos DB beheert transparant partities (bijvoorbeeld gesplitste, samenvoegen, kloon operations) en zorgt ervoor dat Hallo operations doen geen nadelige invloed op prestaties of beschikbaarheid, terwijl de toepassing hello elastisch verhoogt of verlaagt u Hiermee doorvoer. 

## <a id="AvailabilityGuarantees"></a>Beschikbaarheidsgaranties
Azure Cosmos DB biedt een beschikbaarheids-SLA van 99,99% beschikbaarheid voor elk Hallo gegevens- en vlak-bewerkingen. Zoals eerder beschreven, omvatten beschikbaarheidsgaranties Azure Cosmos DB een absolute bovengrens voor de latentie voor elke vlak gegevens en bewerkingen. Hallo beschikbaarheidsgaranties solide eenheid zijn en niet wijzigen met Hallo aantal gebieden of geografische afstand tussen regio's. Beschikbaarheidsgaranties toepassen met zowel handmatig als, automatische failover. Azure Cosmos DB biedt transparante multihoming API's die ervoor zorgen dat uw toepassing kan worden uitgevoerd tegen logische eindpunten en transparant Hallo aanvragen toohello nieuw gebied in geval van een failover kunt versturen. Anders gezegd, uw toepassing hoeft niet opnieuw geïmplementeerd bij regionale failover toobe en Hallo beschikbaarheids-Sla's worden bewaard.

### <a id="AvailabilityAndConsistency"></a>Beschikbaarheid van relatie met de consistentiecontrole, latentie en doorvoer
Beschikbaarheid van relatie met de consistentiecontrole, latentie en doorvoer wordt beschreven in [relatie met de beschikbaarheid van de consistentie](#ConsistencyAndAvailability), [relatie met de beschikbaarheid van de latentie](#LatencyAndAvailability) en [Relatie met de beschikbaarheid van de doorvoer](#ThroughputAndAvailability). 

## <a id="GuaranteesAgainstDataLoss"></a>Garanties en systeemgedrag voor 'gegevensverlies'
In Azure Cosmos DB elke partitie (van een verzameling) is maximaal beschikbaar is gemaakt door een aantal replica's worden verdeeld over ten minste 10-20 domeinen met fouten. Alle schrijfbewerkingen zijn synchroon en blijvend vastgelegd door een quorum meerderheid van replica's voordat ze toohello client zijn bevestigd. Asynchrone replicatie wordt toegepast met coördinatie meerdere partities verdeeld over meerdere regio's. Azure Cosmos DB zorgt ervoor dat er geen verlies van gegevens voor een tenant geïnitieerde handmatige failover is. Tijdens de automatische failover garandeert Azure Cosmos DB een bovengrens van Hallo geconfigureerd gebonden veroudering interval Hallo gegevens verloren gaan venster als onderdeel van de SERVICEOVEREENKOMST.

## <a id="CustomerFacingSLAMetrics"></a>Klantgerichte serviceovereenkomstmetrieken
Azure Cosmos DB beschrijft transparant Hallo doorvoer, latentie, consistentie en beschikbaarheid metrische gegevens. Deze metrische gegevens zijn toegankelijk via een programma en via hello Azure-portal (Zie de volgende afbeelding). U kunt ook waarschuwingen op verschillende drempelwaarden voor gebruik van Azure Application Insights instellen.
 
**Consistentie, latentie, doorvoer en beschikbaarheid metrische gegevens zijn transparant beschikbaar tooeach tenant**

![Azure DB Cosmos zichtbaar is voor een klant serviceovereenkomstmetrieken](./media/distribute-data-globally/customer-slas.png)

## <a id="Next Steps"></a>Volgende stappen
* globale replicatie tooimplement op uw Azure DB die Cosmos-account met Azure portal, Zie Hallo [tooperform Azure Cosmos DB globale database replicatie met Hallo hoe Azure-portal](tutorial-global-distribution-documentdb.md).
* toolearn over het tooimplement meerdere masters architecturen met Azure Cosmos DB Zie [hoofddatabase meerdere architecturen met Azure Cosmos DB](multi-region-writers.md).
* toolearn informatie over hoe automatische en handmatige failover werken in Azure Cosmos DB raadpleegt [regionale Failovers in Azure Cosmos DB](regional-failover.md).

## <a id="References"></a>Verwijzingen
1. Eric Brewer. [Voor robuuste gedistribueerde systemen](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf)
2. Eric Brewer. [KAPJE twaalf jaar Later – hoe Hallo regels zijn gewijzigd](http://informatik.unibas.ch/fileadmin/Lectures/HS2012/CS341/workshops/reportsAndSlides/PresentationKevinUrban.pdf)
3. Geurts, Lynch. - [Brewer &#39; s gissingen en haalbaarheid van consistente, beschikbaar, partitie fouttolerante webservices](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf)
4. Daniel Abadi. [Consistentiecontrole voor-en nadelen in moderne gedistribueerde Database systemen ontwerp](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf)
5. To Kleppmann. [Stop het aanroepen van databases CP of Azië](https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html)
6. Peter Bailis et al. [Probabilistische gebonden veroudering (PBS) voor praktische gedeeltelijke quorum](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
7. Naor en wol. [Laden en de capaciteit en beschikbaarheid in een Quorum-systemen](http://www.cs.utexas.edu/~lorenzo/corsi/cs395t/04S/notes/naor98load.pdf)
8. Herlihy en volgende. [Lineralizability: Een juistheid voorwaarde voor gelijktijdige objecten](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf)
9. [SLA voor Azure Cosmos-DB](https://azure.microsoft.com/support/legal/sla/cosmos-db/)
