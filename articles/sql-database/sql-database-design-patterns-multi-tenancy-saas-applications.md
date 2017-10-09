---
title: aaaDesign patronen voor multitenant SaaS-toepassingen en Azure SQL Database | Microsoft Docs
description: Dit artikel worden besproken Hallo en algemene gegevens architectuur patronen van meerdere tenants databasetoepassingen die worden uitgevoerd in een cloudomgeving moeten tooconsider en Hallo verschillende voor-en nadelen die zijn gekoppeld aan deze patronen. Ook wordt uitgelegd hoe Azure SQL Database met elastische pools en elastische extra helpen deze vereisten voldoen op een wijze inbreuk op Nee.
keywords: 
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 1dd20c6b-ddbb-40ef-ad34-609d398d008a
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-design
ms.date: 02/01/2017
ms.author: srinia
ms.openlocfilehash: a4b58935b08cb78792e65a675d680de708b709fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multi-tenant-saas-applications-and-azure-sql-database"></a>Ontwerppatronen voor multitenant SaaS-toepassingen en Azure SQL Database
In dit artikel kunt u lezen over Hallo vereisten en algemene gegevens architectuur patronen van meerdere tenants software als een dienst (SaaS)-database-toepassingen die worden uitgevoerd in een cloudomgeving. Hierin wordt ook uitgelegd Hallo factoren u tooconsider nodig hebt en Hallo-en nadelen van verschillende ontwerppatronen. Elastische pools en elastische hulpprogramma's in Azure SQL Database kunt u uw specifieke behoeften zonder andere doelstellingen gevaar te brengen.

Ontwikkelaars maken soms keuzes die op basis van hun op lange termijn belang werken bij het ontwerpen van tenancymodus modellen voor gegevenslagen Hallo van multitenant-toepassingen. In eerste instantie is ten minste een ontwikkelaar mogelijk over denken gebruiksgemak ontwikkelings- en cloud serviceprovider kosten te verlagen als belangrijker dan de tenant-isolatie of Hallo schaalbaarheid van een toepassing. Deze keuze kan leiden toocustomer tevredenheid problemen en een kostbare loop-correctie later.

Een multitenant-toepassing is een toepassing die wordt gehost in een cloudomgeving en biedt Hallo dezelfde set services toohundreds of duizenden tenants die niet delen of elkaars gegevens zien. Een voorbeeld is een SaaS-toepassing die voorziet in tootenants in een omgeving met cloud-gebaseerde services.

## <a name="multi-tenant-applications"></a>Multitenant-toepassingen
In toepassingen met meerdere tenants, kunnen gegevens en werkbelasting eenvoudig worden gepartitioneerd. U kunt partitioneren gegevens en de belasting, bijvoorbeeld langs de grenzen van de tenant, omdat de meeste aanvragen worden uitgevoerd binnen de grenzen Hallo van een tenant. Die eigenschap is inherent aan het Hallo-gegevens en Hallo werkbelasting en deze Hiermee Hallo toepassing patronen besproken in dit artikel worden verbeterd.

Dit type toepassing ontwikkelaars gebruiken in de hele spectrum Hallo van cloud-gebaseerde toepassingen, waaronder:

* Partner databasetoepassingen die overgezet toohello worden cloud als SaaS-toepassingen
* Gebouwd voor cloud Hallo van Hallo gemalen van SaaS-toepassingen
* Directe, klantgerichte toepassingen
* Werknemers gerichte bedrijfstoepassingen

SaaS-toepassingen die zijn ontworpen voor cloud Hallo en die met hoofdmappen zoals databasetoepassingen partner meestal multitenant-toepassingen zijn. Deze SaaS-toepassingen bieden een gespecialiseerde softwaretoepassing als een service tootheir tenants. Tenants kunnen toegang krijgen tot de toepassingsservice Hallo en volledige eigendom van de bijbehorende gegevens die zijn opgeslagen als onderdeel van de toepassing hello hebben. Maar tootake profiteren van de voordelen van SaaS, tenants Hallo moet afstand enige controle over hun eigen gegevens. Ze vertrouwen Hallo SaaS-serviceprovider tookeep hun gegevens veilig en geïsoleerd van andere tenants gegevens. Voorbeelden van dit soort multitenant SaaS-toepassing zijn MYOB SnelStart en Salesforce.com. Elk van deze toepassingen kan worden gepartitioneerd langs de grenzen van de tenant en ondersteuning Hallo toepassing ontwerppatronen in dit artikel besproken.

Toepassingen die een directe service toocustomers of tooemployees binnen een organisatie (vaak waarnaar wordt verwezen tooas gebruikers plaats tenants) bieden zijn een andere categorie op Hallo multitenant toepassing spectrum. Klanten toohello service abonneren en niet de eigenaar serviceprovider Hallo Hallo gegevens verzameld en opgeslagen. Serviceproviders hebben minder strenge vereisten tookeep gegevens van hun klanten van elkaar geïsoleerd buiten overheid voorgeschreven privacy voorschriften. Voorbeelden van dergelijke klantgerichte multitenant toepassing zijn inhoudsproviders van media zoals Netflix, Spotify en Xbox LIVE. Andere voorbeelden van toepassingen eenvoudig partitioneerbare klantgerichte, Internet-toepassingen of toepassingen van Internet der dingen (IoT) in elke klant of het apparaat kan fungeren als een partitie. Grenzen van partities kunnen afzonderlijke gebruikers en apparaten.

Niet alle toepassingen partitie eenvoudig langs één eigenschap zoals tenant, klant, gebruiker of apparaat. Een complexe ERP-toepassing (ERP), heeft bijvoorbeeld producten, orders en klanten. Deze heeft meestal een complexe schema met duizenden maximaal gekoppelde tabellen.

Een strategie voor geen enkele partitie kan toepassen tooall tabellen en werkt via een toepassing werklast. Dit artikel is gericht op een multitenant-toepassingen waarvoor eenvoudig partitioneerbare gegevens en werkbelastingen.

## <a name="multi-tenant-application-design-trade-offs"></a>Ontwerp-en nadelen multitenant-toepassing
Hallo ontwerppatroon voor een multitenant-toepassingsontwikkelaar normaal gesproken kiest is gebaseerd op een afweging van Hallo volgende factoren:

* **Tenantisolatie**. Hallo de ontwikkelaar moet tooensure er is geen tenant gegevens heeft die ongewenste toegang tooother tenants. Hallo isolatie vereiste breidt tooother eigenschappen, zoals beveiliging bieden van veel ruis veroorzaken neighbors, kunnen toorestore worden gegevens van een tenant en tenantspecifieke aanpassingen implementeren.
* **Kosten van de resource cloud**. Een SaaS-toepassing moet toobe kostenbesparende cloudoplossing. Een ontwikkelaar van multitenant-toepassingen mogelijk toooptimize voor lagere kosten kiezen in het Hallo-gebruik van cloudresources, zoals opslag en berekeningen kosten.
* **Gebruiksgemak DevOps**. Een ontwikkelaar van toepassingen met meerdere tenants moet tooincorporate isolatie beveiliging, onderhouden, en Hallo status van hun toepassingen en -databaseschema controleren en problemen met tenant. Complexiteit in de ontwikkeling van toepassingen en bewerking zet rechtstreeks tooincreased kosten en uitdagingen met tevredenheid tenant.
* **Schaalbaarheid**. Hallo mogelijkheid tooincrementally meer tenants en capaciteit toevoegen voor tenants die nodig is het noodzakelijk tooa geslaagde SaaS-bewerking.

Elk van deze factoren heeft verschillen vergeleken tooanother. Hallo laagste kosten cloud aanbieden Hallo gemakkelijkste ontwikkeling biedt niet aanbieden. Het is belangrijk voor een ontwikkelaar toomake geïnformeerd keuzes over deze opties en hun verschillen tijdens ontwerpproces Hallo-toepassing.

Een patroon populaire ontwikkeling is toopack meerdere tenants naar een of meer databases. Hallo voordelen van deze benadering zijn lagere kosten, omdat u voor enkele databases en relatief eenvoudig hello betaalt van het werken met een beperkt aantal databases. Maar na verloop van tijd een ontwikkelaar van de SaaS-multitenant-toepassingen wordt Houd er rekening mee dat deze keuze aanzienlijke nadelen in isolatie van tenants en schaalbaarheid heeft. Als de isolatie van tenants is belangrijk, is extra moeite vereist tooprotect tenant gegevens in gedeelde opslag tegen onbevoegde toegang of neighbors veel ruis veroorzaken. Deze extra moeite kan aanzienlijk verbeteren ontwikkelingsinspanningen en isolatie onderhoudskosten. Op dezelfde manier als voor het toevoegen van tenants vereist is, is dit ontwerppatroon doorgaans expertise tooredistribute tenant gegevens over databases tooproperly scale Hallo gegevenslaag van een toepassing.  

Isolatie van tenants vaak is een fundamenteel vereiste in SaaS-toepassingen voor meerdere tenants die inspelen op de toobusinesses en organisaties. Een ontwikkelaar kan verleiding komen door merkbare voordelen in eenvoud en kosten ten opzichte van de isolatie van tenants en schaalbaarheid. Deze wisselwerking kan bewijzen complexe en dure als Hallo service groeit en de vereisten voor tenant-netwerkisolatie worden meer belangrijke en beheerde op Hallo toepassingslaag. Echter, in multitenant-toepassingen die een directe, consumentgerichte service toocustomers bieden isolatie van tenants mogelijk een lagere prioriteit dan optimaliseren voor de kosten van de resource cloud.

## <a name="multi-tenant-data-models"></a>Multitenant gegevensmodellen
Algemene ontwerp procedures voor het plaatsen van gegevens van de tenant volgen drie verschillende modellen, weergegeven in afbeelding 1.

![multitenant toepassingsgegevensmodellen](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-multi-tenant-data-models.png)

Afbeelding 1: Algemene ontwerp procedures voor meerdere tenants gegevensmodellen

* **Database per tenant**. Elke tenant heeft zijn eigen database. Alle gegevens van de tenant-specifieke is beperkt toohello-tenant-database en geïsoleerd van andere tenants en hun gegevens.
* **Gedeelde database shard**. Meerdere tenants delen één van meerdere databases. Een unieke set van tenants is tooeach database toegewezen met behulp van een strategie voor partitionering zoals hash, bereik of lijst partitioneren. Deze gegevens distributie-strategie is vaak sharding tooas waarnaar wordt verwezen.
* **Database-enkel gedeeld**. Een enkelvoudige, soms grote-database bevat gegevens voor alle tenants, met de ondubbelzinnig kunnen worden gemaakt in een tenant-ID-kolom.

> [!NOTE]
> Een ontwikkelaar van toepassingen mogelijk tooplace van verschillende tenants in verschillende databaseschema kiezen en vervolgens Hallo schema naam toodisambiguate Hallo verschillende tenants worden gebruikt. We raden deze benadering niet omdat hiervoor meestal Hallo gebruik van dynamische SQL en kan niet effectief in het plan opslaan in cache. Hallo rest van dit artikel richten we op Hallo gedeeld tabel benadering voor deze categorie van multitenant-toepassing.
> 
> 

## <a name="popular-multi-tenant-data-models"></a>Populaire multitenant gegevensmodellen
Het is belangrijk tooevaluate Hallo verschillende soorten multitenant gegevensmodellen in termen van Hallo toepassing ontwerp-en nadelen die we al hebt geïdentificeerd. Deze factoren helpen kenmerkend Hallo drie meest voorkomende multitenant gegevensmodellen eerder beschreven en hun Databasegebruik zoals aangegeven in afbeelding 2.

* **Isolatie**. Hallo mate van isolatie tussen de tenants mag een meting van hoeveel isolatie van tenants een gegevensmodel bereikt.
* **Kosten van de resource cloud**. Hallo hoeveelheid resources delen tussen tenants kunt optimaliseren resourcekosten van de cloud. Een bron kan worden gedefinieerd als Hallo berekenings- en kosten.
* **DevOps kosten**. Hallo eenvoudig ontwikkelen van toepassingen, implementatie en beheerbaarheid vermindert de totale kosten voor SaaS-bewerking.  

In afbeelding 2 toont Hallo Y-as Hallo niveau van de isolatie van tenants. Hallo X-as geeft Hallo niveau van het delen van bronnen. Hallo-grijs pijl in het midden Hallo geeft Hallo-richting van DevOps kosten, stationskleppen tooincrease of afname.

![Ontwerppatronen voor populaire multitenant-toepassing](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-popular-application-patterns.png)

Afbeelding 2: Populaire multitenant gegevensmodellen

Hallo rechterbenedenhoek in afbeelding 2 ziet u een patroon van de toepassing die gebruikmaakt van een individuele database potentieel grote, gedeeld en Hallo gedeeld tabel (of apart schema) benadering. Het is goed voor resource delen omdat alle huurders Hallo dezelfde bronnen (CPU, geheugen en input/output) in een individuele database database gebruiken. Maar isolatie van tenants is beperkt. Mogelijk moet u tootake extra stappen tooprotect tenants van elkaar op de toepassingslaag Hallo. Deze aanvullende stappen kunnen Hallo DevOps kosten voor het ontwikkelen en beheren van de toepassing hello aanzienlijk verbeteren. Schaalbaarheid wordt beperkt door Hallo schaal van Hallo-hardware die als host fungeert voor Hallo-database.

Hallo linksonder Kwadrant in afbeelding 2 ziet u meerdere tenants shard tussen meerdere databases (doorgaans de andere hardware eenheden schalen). Elke database als host fungeert voor een subset van tenants, waarvan Hallo schaalbaarheid betrekking van andere patronen. Als meer capaciteit vereist voor meer tenants is, kunt u eenvoudig hello tenants plaatsen op nieuwe databases toonew hardware schaaleenheden toegewezen. Echter wordt Hallo hoeveelheid resources delen verminderd. Alleen tenants op Hallo dezelfde geplaatst schaaleenheden resources delen. Deze aanpak biedt weinig verbetering tootenant isolatie omdat veel tenants nog steeds worden geplaatst zonder wordt automatisch beveiligd tegen elkaars acties. Complexiteit van de toepassing blijft hoog.

Hallo linksboven Kwadrant in afbeelding 2 is Hallo derde benadering. Gegevens van elke tenant wordt in een eigen database. Deze aanpak goede isolatie van tenants eigenschappen heeft, maar beperkt resources delen wanneer elke database een eigen toegewijde bronnen heeft. Deze methode is geschikt als alle tenants voorspelbare werkbelastingen hebben. Als tenantwerkbelastingen minder voorspelbaar worden, Hallo-provider is niet geoptimaliseerd resources delen. Onvoorspelbaarheid is gebruikelijk voor SaaS-toepassingen. Hallo-provider moet ofwel te veel inrichten toomeet eisen of lager resources. De actie resulteert in hogere kosten of lager tevredenheid van de tenant. Een hogere mate van resources te delen met tenants wordt kosteneffectiever-wenselijk toomake Hallo oplossing. Toenemende Hallo aantal databases DevOps kosten toodeploy verhoogt ook en onderhouden van de toepassing hello. Deze methode biedt ondanks deze problemen Hallo aanbevolen en eenvoudigste isolatie voor tenants.

Deze factoren ook van invloed zijn op Hallo ontwerppatroon voor die een klant kiest:

* **Eigendom van gegevens van de tenant**. Hallo-patroon van één database per tenant meer gericht op een toepassing waarin tenants eigendom van hun eigen gegevens behouden.
* **Schalen**. Een toepassing die gericht is op honderden of duizenden of miljoenen tenants Hiermee worden verbeterd benaderingen zoals sharding deling van databases. Vereisten voor netwerkisolatie kunnen nog steeds uitdagingen opleveren.
* **Waarde en zakelijke model**. Als een toepassing per-tenant omzet als zinvol klein (minder dan een dollar), de vereisten voor netwerkisolatie minder kritiek is geworden en een gedeelde database. Als omzet per tenant, enkele euro is, wordt een model database per tenant haalbaar is. Deze kan u helpen ontwikkelingskosten te verlagen.

Opgegeven Hallo ontwerp-en nadelen wordt weergegeven in afbeelding 2, moet een ideaal multitenant-model tooincorporate goed tenant isolatie eigenschappen met optimale resources te delen tussen de tenants. Dit model past in Hallo categorie wordt beschreven in Hallo hoofdletters pas van afbeelding 2.

## <a name="multi-tenancy-support-in-azure-sql-database"></a>Ondersteuning voor multitenancy in Azure SQL Database
Azure SQL Database ondersteunt alle multitenant toepassing patronen die worden beschreven in afbeelding 2. Het ondersteunt ook het patroon van een toepassing die goede resources delen combineert met elastische pools en Hallo isolatie voordelen van het Hallo-database per tenant benadering (Zie Hallo hoofdletters pas in afbeelding 3). Elastische database en -mogelijkheden in SQL-Database te verminderen Hallo kosten toodevelop en gebruiken van een toepassing met veel databases (weergegeven in het gebied van Hallo grijs weergegeven in afbeelding 3). Deze hulpprogramma's kunt u maken en beheren van toepassingen die van Hallo meerdere databases patronen gebruikmaken.

![Patronen in Azure SQL Database](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-patterns-sqldb.png)

Afbeelding 3: Multitenant toepassing patronen in Azure SQL Database

## <a name="database-per-tenant-model-with-elastic-pools-and-tools"></a>Database per tenant-model met elastische pools en hulpprogramma 's
Isolatie van tenants combineren elastische pools in SQL-Database met resources delen tussen tenant databases toobetter ondersteuning Hallo database per tenant benadering. SQL-Database is een oplossing voor laag voor SaaS-providers die meerdere tenants toepassingen maken. Hallo last van resources te delen tussen tenants verschuift van Hallo laag toohello database service toepassingslaag. Hallo complexiteit te beheren en uitvoeren van query's op grote schaal tussen databases wordt vereenvoudigd met elastische taken, elastische query elastische transacties en Hallo-clientbibliotheek voor elastische database.

| Toepassingsvereisten | Mogelijkheden van de SQL-database |
| --- | --- |
| Isolatie van tenants en resources delen |[Elastische pools](sql-database-elastic-pool.md): toewijzen van een verzameling resources van de SQL-Database en het Hallo-resources te delen tussen de verschillende databases. Ook afzonderlijke databases kunnen net zoveel bronnen uit de groep Hallo als tekenen benodigde tooaccommodate capaciteit vraag pieken vanwege toochanges in tenantwerkbelastingen. Hallo elastische pool zelf kan worden geschaald omhoog of omlaag naar behoefte. Elastische pools bieden ook beheergemak en bewaking en probleemoplossing op Hallo van toepassingen niveau. |
| Gebruiksgemak DevOps voor databases |[Elastische pools](sql-database-elastic-pool.md): als u eerder hebt genoteerd. |
| | [Elastische query](sql-database-elastic-query-horizontal-partitioning.md): Query voor databases voor rapportage of analyse cross-tenant. |
| | [Elastische taken](sql-database-elastic-jobs-overview.md): pakket en database onderhoudsbewerkingen veilig te implementeren of databaseschema toomultiple databases wordt gewijzigd. |
| | [Elastische transacties](sql-database-elastic-transactions-overview.md): proces tooseveral databases in een atomic- en geïsoleerde manier gewijzigd. Elastische transacties zijn nodig wanneer u toepassingen nodig 'Alles of niets' garanties over verschillende databasebewerkingen. |
| | [Clientbibliotheek voor elastische database](sql-database-elastic-database-client-library.md): gegevens distributies beheren en kaart toodatabases tenants. |

## <a name="shared-models"></a>Gedeelde modellen
Zoals eerder beschreven, voor de meeste SaaS-providers is een gedeeld model benadering oplevert problemen met tenant isolatie problemen en complexiteit met de ontwikkeling van toepassingen en onderhoud. Echter, voor multitenant-toepassingen die een service bieden direct tooconsumers, tenant-isolatievereisten mogelijk niet als hoge prioriteit als de kosten te minimaliseren. Ze kunnen toopack tenants in een of meer databases op een high-density tooreduce kosten mogelijk. Gedeelde databasemodellen met behulp van een individuele database of meerdere shard databases kunnen leiden tot extra efficiëntie in delen en de algehele kosten van de resource. Azure SQL Database biedt een aantal functies waarmee klanten isolatie voor betere beveiliging en beheer in de gegevenslaag Hallo bouwen.

| Toepassingsvereisten | Mogelijkheden van de SQL-database |
| --- | --- |
| Isolatie van beveiligingsfuncties |[Beveiliging](https://msdn.microsoft.com/library/dn765131.aspx) |
| [-Databaseschema](https://msdn.microsoft.com/library/dd207005.aspx) | |
| Gebruiksgemak DevOps voor databases |[Elastische query](sql-database-elastic-query-horizontal-partitioning.md) |
| | [Elastische taken](sql-database-elastic-jobs-overview.md) |
| | [Elastische transacties](sql-database-elastic-transactions-overview.md) |
| | [Clientbibliotheek voor Elastic Database](sql-database-elastic-database-client-library.md) |
| | [Samenvoegen en splitsen elastische database](sql-database-elastic-scale-overview-split-and-merge.md) |

## <a name="summary"></a>Samenvatting
Vereisten voor tenant-netwerkisolatie zijn belangrijk voor de meeste multitenant SaaS-toepassingen. Hallo aanbevolen optie tooprovide isolatie leans aanzienlijke richting Hallo database per tenant benadering. Hallo vereist andere twee benaderingen investeringen in complexe toepassingslagen waarvoor ervaren ontwikkeling personeel tooprovide isolatie, waardoor aanzienlijk kosten en risico's. Als vereisten voor netwerkisolatie niet voor vroeg in serviceontwikkeling hello verwerkt zijn, zijn met terugwerkende kracht ze nog meer kostbare in de eerste twee modellen Hallo. de belangrijkste nadelen Hallo Hallo database per tenant model gekoppeld zijn verwante tooincreased cloud resourcekosten vanwege tooreduced delen, en het onderhoud en het beheer van veel databases. Ontwikkelaars van SaaS-toepassingen is vaak het moeilijk wanneer ze deze verschillen.

Hoewel de verschillen mogelijk belangrijke barrières met de meeste cloudserviceproviders voor database, elimineert Azure SQL Database Hallo barrières met de elastische groep en de mogelijkheden van de elastische database. SaaS-ontwikkelaars kunnen combineren Hallo isolatie kenmerken van een database per tenant-model en resource delen en Hallo verbeteringen in beheerbaarheid van veel databases optimaliseren door elastische pools en bijbehorende hulpprogramma's.

Multitenant toepassing providers die geen vereisten voor tenant-netwerkisolatie hebben en die tenants kunt verpakken in een database op een high-density wellicht dat de gedeelde gegevens resultaat in extra efficiëntie bij het delen van bronnen modellen en verlagen de totale kosten. Azure SQL Database elastische database-hulpprogramma's, sharding-bibliotheken en beveiligingsfuncties helpen aanbieders van SaaS ontwikkelen en beheren van multitenant-toepassingen.

## <a name="next-steps"></a>Volgende stappen
[Aan de slag met hulpprogramma's voor elastische database](sql-database-elastic-scale-get-started.md) met een voorbeeld-app die u laat Hallo-clientbibliotheek zien.

Maak een [aangepaste dashboard van de elastische groep voor SaaS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools-custom-dashboard) met een voorbeeld-app die gebruikmaakt van elastische pools voor een rendabele, schaalbare databaseoplossing.

Hello Azure SQL Database-hulpprogramma's te gebruiken[migreren van bestaande databases tooscale uit](sql-database-elastic-convert-to-use-elastic-tools.md).

een elastische pool met toocreate hello Azure portal, Zie [maken van een elastische pool](sql-database-elastic-pool-manage-portal.md).  

Meer informatie over hoe te[bewaken en beheren van een elastische pool](sql-database-elastic-pool-manage-portal.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Implementeren en een multitenant-toepassing die gebruikmaakt van Azure SQL Database - Wingtip SaaS verkennen](sql-database-saas-tutorial.md)
* [Wat is een Azure elastische groep?](sql-database-elastic-pool.md)
* [Uitbreiden met Azure SQL Database](sql-database-elastic-scale-introduction.md)
* [multitenant-toepassingen met elastische database-hulpprogramma's en beveiliging](sql-database-elastic-tools-multi-tenant-row-level-security.md)
* [Verificatie in multitenant-apps met behulp van Azure Active Directory en OpenID Connect](../guidance/guidance-multitenant-identity-authenticate.md)
* [De toepassing Tailspin Surveys](../guidance/guidance-multitenant-identity-tailspin.md)


## <a name="questions-and-feature-requests"></a>Vragen en functieaanvragen

Volg ons voor vragen in Hallo [SQL Database-forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted). Toevoegen van een functie-aanvraag in Hallo [forum met feedback van SQL-Database](https://feedback.azure.com/forums/217321-sql-database/).

