---
title: aaaUnderstand Azure Active Directory-architectuur | Microsoft Docs
description: Wordt uitgelegd wat een Azure AD-tenant is, en hoe toomanage Azure via Azure Active Directory
services: active-directory
documentationcenter: 
author: MarkusVi
writer: v-lorisc
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: markvi
ms.openlocfilehash: 799943c012dcc309907ed3c36372038a0aad222a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-active-directory-architecture"></a>Azure Active Directory-architectuur begrijpen
Azure Active Directory (Azure AD) kunt u toosecurely toegang tooAzure services en resources voor uw gebruikers beheren. Azure AD omvat een volledige suite met mogelijkheden voor identiteitsbeheer. Zie [Wat is Azure Active Directory?](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis) voor meer informatie over de functies van Azure AD.

In Azure AD, kunt u maken en beheren van gebruikers en groepen uit en machtigingen tooallow inschakelen en tooenterprise resources voor de toegang weigert. Zie voor meer informatie over identity management [Hallo grondbeginselen van Azure identiteitsbeheer](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity).

## <a name="azure-ad-architecture"></a>Azure AD-architectuur
Azure AD geografisch verspreide architectuur combineert uitgebreide bewaking, het omleiden van geautomatiseerde, failover en herstelfuncties ons toodeliver op bedrijfsniveau beschikbaarheid en prestaties tooour klanten in staat.

Hallo na architectuur elementen worden in dit artikel behandeld:
 *  Servicearchitectuurontwerp
 *  Schaalbaarheid 
 *  Continue beschikbaarheid
 *  Datacenters

### <a name="service-architecture-design"></a>Servicearchitectuurontwerp
Hallo meest voorkomende manier toobuild een schaalbare, maximaal beschikbare, gegevens rich-systeem via onafhankelijke bouwstenen of schaaleenheden voor de gegevenslaag hello Azure AD is, schaaleenheden heten *partities*. 

Hallo gegevenslaag heeft diverse front-end-services die de mogelijkheid hebben alleen-lezen. Hallo diagram hieronder ziet u hoe Hallo onderdelen van een één-mappartitie in datacenters geografisch verdeeld worden gedistribueerd. 

  ![Partities met één map](./media/active-directory-architecture/active-directory-architecture.png)

Hallo-onderdelen van Azure AD-architectuur zijn een replica van primaire en secundaire replica's.

**Primaire replica**

Hallo *primaire replica* ontvangt alle *schrijft* voor Hallo partitie hoort bij. Een bewerking wordt onmiddellijk gerepliceerde tooa secundaire replica in een ander datacenter voordat er wordt teruggekeerd geslaagd toohello beller, zodat geografisch redundante duurzaamheid van schrijfbewerkingen schrijven.

**Secundaire replica's**

Alle *leesbewerkingen* in een map worden afgehandeld vanuit *secundaire replica's*, die zich in datacenters op verschillende fysieke locaties bevinden. Er zijn veel secundaire replica's, omdat gegevens asynchroon worden gerepliceerd. Directory leest, zoals verificatieaanvragen worden van datacenters die klanten sluiten tooour verwerkt. Hallo secundaire replica's zijn verantwoordelijk voor lezen schaalbaarheid.

### <a name="scalability"></a>Schaalbaarheid

Schaalbaarheid is Hallo mogelijkheid van een service tooexpand toomeet toenemende prestatie-eisen. Schaalbaarheid wordt bereikt door het partitioneren van Hallo gegevens worden geschreven. Lees schaalbaarheid wordt bereikt door het repliceren van gegevens uit één partitie toomultiple secundaire replica's die over het hele Hallo wereld.

Aanvragen van directory-toepassingen zijn doorgaans gerouteerde toohello datacenter die ze fysiek die het dichtst bij. Schrijfbewerkingen zijn transparant omgeleide toohello primaire replica tooprovide lezen-schrijven consistentie. Secundaire replica's uitbreiden aanzienlijk Hallo schaal van partities omdat Hallo mappen meestal voor leesbewerkingen meestal Hallo zijn.

Directory-toepassingen verbinding toohello dichtstbijzijnde datacenters. Hierdoor worden de prestaties verbeterd, wat uitschalen mogelijk maakt. Aangezien een mappartitie veel secundaire replica's hebben kan, kunnen secundaire replica's dichter toohello directory-clients worden geplaatst. Alleen interne directory service-onderdelen die rechtstreeks wegschrijven-intensieve doel Hallo active primaire replica.

### <a name="continuous-availability"></a>Continue beschikbaarheid

Definieert de Hallo mogelijkheid van een ononderbroken system tooperform beschikbaarheid (of bedrijfstijd). Hallo sleutel tooAzure AD van hoge beschikbaarheid is dat onze services snel verkeer via meerdere geografisch verspreide datacenters kunnen veranderen. Elk datacenter is onafhankelijk. Dit maakt het gebruik van gedecorreleerde foutmodi mogelijk.

Azure AD partitie ontwerp is vereenvoudigd vergeleken toohello enterprise AD-ontwerp, wat van essentieel belang voor het schalen van Hallo-systeem. We maken gebruik van een single-master-ontwerp dat een zorgvuldig geregisseerd en deterministisch failoverproces omvat voor de primaire replica.

**Fouttolerantie**

Een systeem is meer beschikbaar als het fouttolerante toohardware-, netwerk- en fouten. Voor elke partitie op Hallo directory, de replica van een maximaal beschikbare master bestaat: Hallo primaire replica. Alleen schrijfbewerkingen toohello partitie worden uitgevoerd op deze replica. Deze replica wordt voortdurend en nauw bewaakt en schrijfbewerkingen onmiddellijk verplaatste tooanother replica kunnen worden (die wordt Hallo nieuwe primaire) als er een storing wordt gedetecteerd. Tijdens de failover kan er een verlies van schrijfbeschikbaarheid optreden. Dit duurt meestal maar 1-2 minuten. De leesbeschikbaarheid wordt gedurende deze tijd niet beïnvloed.

Leesbewerkingen (dat schrijfbewerkingen outnumber door bruikbare) gaat alleen toosecondary replica's. Omdat secundaire replica's idempotent zijn, verlies van een één replica in een bepaalde partitie eenvoudig wordt gecompenseerd door Hallo leesbewerkingen tooanother replica, meestal in Hallo hetzelfde datacenter.

**Duurzaamheid van gegevens**

Een schrijfbewerking is blijvend doorgevoerd tooat minimaal twee datacenters eerdere tooit wordt bevestigd. Dit gebeurt door eerst doorvoeren Hallo schrijven op Hallo van primaire en vervolgens onmiddellijk repliceren Hallo schrijven tooat minimaal één andere Datacenter. Dit zorgt ervoor dat een potentieel onherstelbare gegevensverlies Hallo data center hosting Hallo primaire niet leidt verlies van gegevens tot.

Azure AD onderhoudt een nul [herstel tijd Objective (RTO)](https://en.wikipedia.org/wiki/Recovery_time_objective) voor uitgifte van tokens en directory leest en schrijft in volgorde van minuten (~ 5 minuten) RTO voor directory Hallo. Er geldt ook een [RPO (herstelpuntdoel)](https://en.wikipedia.org/wiki/Recovery_point_objective) van nul en tijdens failovers gaan er geen gegevens verloren.

### <a name="data-centers"></a>Datacenters

Azure AD-replica's worden opgeslagen in de gehele Hallo wereld datacenters. Zie [Azure-datacenters](https://azure.microsoft.com/en-us/overview/datacenters) voor meer informatie.

Azure AD werkt via datacenters Hello volgende kenmerken:

 * Verificatie, grafiek en andere AD-services zich achter Hallo Gateway-service. Hallo Gateway beheert taakverdeling van deze services. Als er via transactionele tests beschadigde servers worden gedetecteerd, wordt er automatisch een failover uitgevoerd. Op basis van deze statuscontroles, routeert Hallo Gateway dynamisch verkeer toohealthy datacenters.
 * Voor *leest*, Hallo directory heeft secundaire replica's en bijbehorende front-end-services in een actief / actief-configuratie die in meerdere datacenters. In geval van een storing van een heel datacentrum worden verkeer automatisch gerouteerde tooa verschillende datacenter.
 *  Voor *schrijft*, Hallo directory wordt failover primaire (master) replica via datacenters via geplande (nieuwe primaire is gesynchroniseerde tooold primaire) of noodgevallen failover-procedures. Gegevens duurzaamheid wordt bereikt door het repliceren van een commit tooat minimaal twee-datacenters.

**Gegevensconsistentie**

Hallo directory model is een van de uiteindelijke consistentie. Een typische probleem met gedistribueerde asynchroon replicerende systemen is geretourneerd van een replica 'name' Hallo-gegevens mogelijk niet up toodate. 

Azure AD levert de consistentie van de lezen-schrijven voor toepassingen die gericht is op een secundaire replica door de primaire replica van schrijfbewerkingen toohello Routering en synchroon binnenhalen Hallo schrijft terug toohello secundaire replica.

Toepassing worden geschreven met behulp van Hallo Graph API van Azure AD gescheiden affiniteit tooa directory replica voor alleen-lezen consistentie te handhaven. Hello Azure AD Graph service onderhoudt een logische-sessie met affiniteit tooa secundaire replica gebruikt voor leesbewerkingen; affiniteit is vastgelegd in een "replica token' Hallo grafiek service caches met behulp van een gedistribueerde cache. Dit token wordt vervolgens gebruikt voor verdere bewerkingen in Hallo dezelfde logische sessie. 

 >[!NOTE]
 >Schrijfbewerkingen onmiddellijk worden gerepliceerd toohello secundaire replica toowhich Hallo logische sessie van leesbewerkingen zijn uitgegeven.
 >

**Back-upbeveiliging**

Hallo directory implementeert voorlopig verwijderd, in plaats van vaste verwijderen, klikt u voor gebruikers en tenants voor eenvoudig herstel in geval van een onopzettelijk verwijderen door de klant. Als uw tenantbeheerder per ongeluk gebruikers verwijdert, kunnen ze gemakkelijk ongedaan maken en herstellen van gebruikers Hallo verwijderd. 

Met Azure AD worden dagelijkse back-ups van alle gegevens geïmplementeerd. Daarom kunnen gegevens bindend worden teruggezet in het geval van logische verwijderingen of beschadigingen. Voor onze gegevenslagen wordt gebruikgemaakt van codes voor het corrigeren van fouten, zodat er kan worden gecontroleerd op fouten en bepaalde typen schijffouten automatisch kunnen worden gecorrigeerd.

**Metrische gegevens en controles**

Voor het uitvoeren van een service met een hoge beschikbaarheid zijn uitstekende mogelijkheden voor metrische gegevens en controle vereist. Met Azure AD worden belangrijke metrische gegevens met betrekking tot de status van de service voortdurend geanalyseerd voor elk van de services. Metrische gegevens, controle en waarschuwingen worden doorlopend ontwikkeld en verfijnd voor elk scenario, zowel binnen de afzonderlijke Azure AD-service als op serviceoverstijgend niveau.

Als u een Azure AD-service werkt niet zoals verwacht, neemt er onmiddellijk actie toorestore functionaliteit zo snel mogelijk. Hallo belangrijkste metrische gegevens van Azure AD-nummers is hoe snel we kunt opsporen en verhelpen van een klant of live site probleem. We investeren sterk in bewaking en waarschuwingen toominimize tijd toodetect (TTD doel: < 5 minuten) en de gereedheid van de operationele toominimize tijd toomitigate (TTM doel: < 30 minuten).

**Veilige bewerkingen**

We gebruiken operationele besturingselementen zoals MFA (Multi-Factor Authentication), zowel voor elke bewerking afzonderlijk als om alle bewerkingen te controleren. We gebruiken bovendien een just-in-time-uitbreiding toogrant benodigde tijdelijke toegang tot het systeem voor elke operationele taak op verzoek voortdurend. Zie voor meer informatie [Hallo Cloud vertrouwde](https://azure.microsoft.com/en-us/support/trust-center).

## <a name="next-steps"></a>Volgende stappen
[Ontwikkelaarshandleiding voor Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide)

