---
title: aaaDesign-noodhersteloplossingen - Azure SQL Database | Microsoft Docs
description: Meer informatie over hoe toodesign uw cloudoplossing voor herstel na noodgevallen door te kiezen Hallo juiste failover-patroon.
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2db99057-0c79-4fb0-a7f1-d1c057ec787f
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 9d9eca7570c7a01c992d0b33d449721709b471c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-strategies-for-applications-using-sql-database-elastic-pools"></a>Disaster recovery strategieën voor toepassingen met elastische pools SQL-Database
Hallo jaren hebt u geleerd dat cloudservices niet betrouwbare zijn en onherstelbare incidenten optreden. SQL-Database biedt verschillende mogelijkheden tooprovide voor bedrijfscontinuïteit Hallo van uw toepassing, wanneer deze incidenten optreden. [Elastische pools](sql-database-elastic-pool.md) en individuele databases Hallo ondersteunen dezelfde soort mogelijkheden voor herstel na noodgevallen. In dit artikel beschrijft enkele DR strategieën voor elastische pools die gebruikmaken van deze functies van SQL Database business continuity.

In dit artikel maakt gebruik van Hallo canonieke ISV SaaS-toepassing patroon volgen:

<i>Een moderne cloud-gebaseerde webtoepassing voorziet in een SQL-database voor elke gebruiker. Hallo ISV veel klanten gebruikt, en daarom veel databases, tenant-databases genoemd. Omdat Hallo tenant databases doorgaans onvoorspelbare activiteit patronen hebben, Hallo ISV maakt gebruik van een elastische pool toomake hello databasekosten zeer voorspelbare gedurende langere perioden. Hallo elastische pool vereenvoudigt ook Hallo prestatiebeheer wanneer Hallo gebruikersactiviteit bereikt. Daarnaast toohello tenant databases Hallo toepassing ook gebruik van verschillende databases toomanage gebruikersprofielen, beveiliging, verzamelen gebruikspatronen enzovoort. Beschikbaarheid van individuele tenants Hallo heeft geen gevolgen voor de beschikbaarheid van de toepassing hello als geheel. Echter hello beschikbaarheid en prestaties van databases management is essentieel voor een functie van de toepassing hello en als Hallo management databases zijn offline Hallo gehele toepassing offline is.</i>  

Dit artikel wordt beschreven DR strategieën die betrekking hebben op een aantal scenario's uit kosten gevoelige opstarten toepassingen tooones met strenge beschikbaarheidsvereisten.

## <a name="scenario-1-cost-sensitive-startup"></a>Scenario 1. Kosten gevoelige opstarten
<i>Ik ben een bedrijf opstarten en zeer gevoelige ben kosten.  Ik wil toosimplify implementatie en beheer van de toepassing hello en kan ik een SLA beperkt hebben voor individuele klanten. Maar ik wil tooensure Hallo toepassing als geheel nooit offline is.</i>

toosatisfy hello eenvoud vereiste alle databases van de tenant implementeren in een elastische pool in hello Azure-regio van uw keuze en beheer databases als individuele databases geogerepliceerde implementeren. Gebruik voor noodherstel Hallo van tenants, geo-herstel, wordt geleverd zonder extra kosten. tooensure hello beschikbaarheid van Hallo management databases, geo-replicatie ze tooanother regio met een automatisch failover-groep (in-preview) (stap 1). Hallo lopende kosten van het Hallo-noodherstelconfiguratie in dit scenario is de totale kosten gelijk toohello van Hallo secundaire databases. Deze configuratie wordt weergegeven in het volgende diagram Hallo.

![Afbeelding 1](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-1.png)

Als er een storing optreedt in de primaire regio hello, Hallo herstel stappen toobring online in uw toepassing met het volgende diagram Hallo worden geïllustreerd.

* Hallo failover groep initieert automatische failover van Hallo management database toohello DR regio. Hallo-toepassing is automatisch opnieuw aangesloten toohello nieuwe primaire en alle nieuwe accounts en tenant-databases in Hallo DR regio worden gemaakt. Hallo bestaande klanten hun eigen gegevens zien tijdelijk niet beschikbaar.
* Hallo elastische pool maken met de Hallo dezelfde configuratie als de oorspronkelijke Hallo-groep (2).
* Geo-restore toocreate kopieën van Hallo tenant databases (3) gebruiken. U kunt overwegen activerende Hallo afzonderlijke herstelacties door Hallo eindgebruiker verbindingen of sommige andere toepassingsspecifieke prioriteit schema gebruiken.


Op dit moment uw toepassing weer online is in Hallo DR regio, maar sommige klanten krijgen met vertraging bij het openen van hun gegevens.

![Afbeelding 2](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-2.png)

Als Hallo onderbreking tijdelijke, is het mogelijk dat Hallo primaire regio is hersteld door Azure voordat alle Hallo database herstelbewerkingen voltooid in Hallo DR regio zijn. In dit geval indelen zwevend Hallo toepassing back toohello primaire regio. Hallo proces duurt Hallo stappen in het volgende diagram Hallo geïllustreerd.

* Annuleer alle openstaande geo-restore-aanvragen.   
* Failover-overschakeling Hallo management databases toohello primaire regio (5). Na het herstel van de regio Hallo Hallo oude primaire geworden automatisch secundaire replica's. Nu overgeschakeld rollen opnieuw. 
* Wijzigen van de toepassing hello connection string toopoint back toohello primaire regio. Nu worden alle nieuwe accounts en tenant-databases gemaakt in de primaire regio Hallo. Sommige klanten hun eigen gegevens zien tijdelijk niet beschikbaar.   
* Stel alle databases in Hallo DR groep alleen-tooread tooensure, die kunnen niet worden gewijzigd in Hallo DR regio (6). 
* Voor elke database in Hallo DR-groep die is gewijzigd sinds Hallo herstel hernoemen of verwijderen van de bijbehorende databases Hallo in Hallo primaire groep (7). 
* Kopiëren Hallo bijgewerkt databases van Hallo DR groep toohello primaire groep (8). 
* Hallo DR-groep (9) verwijderen

De toepassing is op dit moment online in de primaire regio Hallo met alle tenant databases beschikbaar in de primaire groep Hallo.

![Afbeelding 3](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-3.png)

Hallo sleutel **profiteren** is van deze strategie lage lopende kosten voor gegevensredundantie laag. Back-ups worden automatisch gemaakt door Hallo SQL Database-service met geen herschrijven van de toepassing en zonder extra kosten.  Hallo kosten worden alleen wanneer Hallo elastische databases zijn hersteld. Hallo **nadeel** is dat Hallo volledige herstel van alle databases van de tenant aanzienlijke tijd. Hallo tijd is afhankelijk van totaal aantal herstelacties die u in Hallo DR start Hallo regio en de totale grootte van Hallo tenant-databases. Zelfs als u bepaalde tenants herstelacties boven andere prioriteit, beconcurreren u alle Hello andere herstelacties die geïnitieerd zijn in dezelfde regio Hallo Hallo service arbitrates en bandbreedte toominimize Hallo algehele impact op Hallo bestaande klanten databases. Bovendien Hallo herstel van Hallo tenant databases kan pas worden gestart Hallo nieuwe elastische pool in Hallo DR regio wordt gemaakt.

## <a name="scenario-2-mature-application-with-tiered-service"></a>Scenario 2. Volwassen toepassing met gelaagde service
<i>Ik ben een goed ontwikkelde SaaS-toepassing met gelaagde service aanbiedingen en andere serviceovereenkomsten voor proefversie klanten en voor het betalen van klanten. Ik heb tooreduce Hallo zo veel mogelijk kosten voor Hallo proefversie klanten is. Proefversie klanten uitvaltijd kunnen duren, maar ik wil tooreduce de kans op. Voor Hallo betalende klanten, is geen downtime vlucht risico. Dus ik wil zorgen dat betalende klanten altijd kunnen tooaccess toomake hun gegevens.</i> 

Dit scenario, afzonderlijke Hallo proeftenants van toosupport betaald tenants door ze in afzonderlijke elastische pools te plaatsen. Hallo proefversie klanten hebben lagere eDTU per tenant en lagere SLA met een langere periode voor herstel. Hallo betalende klanten zijn in een pool met hogere eDTU per tenant en een hogere SLA. tooguarantee hello laagste hersteltijd Hallo betalende klant tenant databases zijn geo-replicatie. Deze configuratie wordt weergegeven in het volgende diagram Hallo. 

![Afbeelding 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-4.png)

Zoals in het eerste scenario Hallo Hallo management databases behoorlijk actief zijn zodat u één geogerepliceerde database voor (1 gebruiken). Dit zorgt ervoor Hallo voorspelbare prestaties voor het nieuwe klantabonnementen profielupdates en andere beheerbewerkingen. Hallo regio waarin Hallo primaire van Hallo management databases zich bevinden is Hallo primaire regio en Hallo-regio waarin Hallo secundaire replica's van Hallo management databases zich bevinden is Hallo DR regio.

Hallo zijn betalende klanten tenant databases active databases in Hallo 'betaald' ingericht in de primaire regio Hallo van toepassingen. Een secundaire groep met dezelfde naam in Hallo DR regio Hallo inrichten. Elke tenant is secundaire geo-replicatie toohello van toepassingen (2). Hierdoor kunnen snel herstel van de tenant-databases met behulp van failover. 

Als er een storing optreedt in de primaire regio hello, Hallo herstel stappen toobring online in uw toepassing worden weergegeven in het volgende diagram Hallo:

![Afbeelding 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-5.png)

* Onmiddellijk een failover Hallo management databases toohello DR regio (3).
* Wijzigen van de toepassing hello connection string toopoint toohello DR regio. Nu worden alle nieuwe accounts en tenant-databases gemaakt in Hallo DR regio. Hallo bestaande proefversie klanten hun eigen gegevens zien tijdelijk niet beschikbaar.
* Failover van tenant databases toohello van toepassingen in Hallo DR regio tooimmediately betaald Hallo herstel hun beschikbaarheid (4). Aangezien Hallo failover een wijziging voor het niveau van snelle metagegevens is, houd rekening met een optimalisatie waar Hallo afzonderlijke failovers door Hallo eindgebruiker verbindingen zijn geactiveerd op verzoek. 
* Als de grootte van uw secundaire pool-eDTU is lager dan de primaire Hallo omdat Hallo secundaire databases alleen vereiste Hallo capaciteit tooprocess Hallo wijziging logboeken terwijl ze zijn secundaire replica's, verhoogt onmiddellijk Hallo groepscapaciteit nu tooaccommodate Hallo volledige de werkbelasting van alle tenants (5). 
* Hallo nieuwe elastische pool maken met Hallo dezelfde naam geven en Hallo dezelfde configuratie in Hallo DR regio voor Hallo proefversie klanten databases (6). 
* Zodra Hallo proefversie klanten groep is gemaakt, gebruikt u geo-restore toorestore hello proeftenant afzonderlijke databases in Hallo nieuwe pool (7). Overweeg activerende Hallo afzonderlijke herstelacties door Hallo eindgebruiker verbindingen of sommige andere toepassingsspecifieke prioriteit schema gebruiken.

De toepassing is op dit moment weer online in Hallo DR regio. Alle betalende gebruikers hebben toegang tot gegevens tootheir terwijl Hallo proefversie klanten treedt vertraging op wanneer de toegang tot hun gegevens.

Wanneer de primaire regio Hallo is hersteld door Azure *nadat* toepassing hello in Hallo DR-regio die u kunt doorgaan met het Hallo-toepassing wordt uitgevoerd in deze regio is hersteld of u kunt ervoor kiezen toofail back toohello primaire regio. Als de primaire regio Hallo is hersteld *voordat* Hallo failover-proces is voltooid, kunt mislukt back meteen. Hallo failback wordt weergegeven in het volgende diagram Hallo Hallo-stappen: 

![Afbeelding 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-6.png)

* Annuleer alle openstaande geo-restore-aanvragen.   
* Failover-overschakeling Hallo management databases (8). Na het herstel van de regio Hallo Hallo oude primaire automatisch worden Hallo secundaire. Nu wordt het Hallo opnieuw primaire.  
* Failover-overschakeling Hallo betaald tenant databases (9). Op deze manier na het herstel van de regio Hallo Hallo oude primaire automatisch worden Hallo secundaire replica's. Nu worden Hallo primaire opnieuw. 
* Set Hallo hersteld proefversie databases die zijn gewijzigd in Hallo DR regio tooread alleen-lezen (10).
* Voor elke database in Hallo proefversie klanten DR groep gewijzigd sinds Hallo herstel, hernoemen of verwijderen van de bijbehorende database Hallo in Hallo proefversie klanten primaire-pool (11). 
* Kopiëren Hallo bijgewerkt databases van Hallo DR groep toohello primaire groep (12). 
* Hallo DR-groep (13) verwijderen 

> [!NOTE]
> Hallo failover-bewerking is asynchroon. toominimize is het belangrijk dat u Hallo tenant databases failover-opdracht in batches van ten minste 20 databases uitvoeren Hallo hersteltijd. 
> 
> 

Hallo sleutel **profiteren** van deze strategie is dat u de hoogste SLA Hallo voor Hallo klanten betalen. Ook wordt hiermee gegarandeerd Hallo nieuwe proefversies zijn geblokkeerd zodra Hallo proefversie DR-adresgroep is gemaakt. Hallo **nadeel** klanten is dat deze installatie verhoogt de totale kosten Hallo van Hallo tenant databases door Hallo kosten van Hallo secundaire DR-adresgroep voor betaald. Bovendien, als secundaire groep Hallo een andere grootte heeft, Hallo betalende klanten ondervinden lagere prestaties na een failover totdat hello pool in Hallo DR regio is bijgewerkt. 

## <a name="scenario-3-geographically-distributed-application-with-tiered-service"></a>Scenario 3. Geografisch verspreide toepassing met gelaagde service
<i>Ik heb een goed ontwikkelde SaaS-toepassing met gelaagde service biedt. Ik toooffer een zeer agressief SLA toomy betaald klanten willen en Hallo risico van impact minimaliseren wanneer er storingen optreden omdat zelfs korte onderbreking leiden klant ergernis tot kan. Het is essentieel dat klanten betalen Hallo altijd toegang tot hun gegevens. Hallo proefversies zijn gratis en een SLA tijdens de proefperiode Hallo niet wordt aangeboden.</i> 

toosupport dit scenario, gebruik drie afzonderlijke elastische pools. Twee gelijke grootte-pools inrichten met hoge edtu's per database in twee verschillende regio's toocontain Hallo betaald klanten tenant databases. derde Hallo-groep met Hallo proeftenants kan lagere edtu's per database en in een van twee gebieden Hallo worden ingericht.

tooguarantee hello laagste hersteltijd tijdens uitval, Hallo betalende klant tenant databases zijn geogerepliceerde met 50% van de primaire databases Hallo op elk van Hallo twee regio's. Daarnaast heeft elke regio 50% van Hallo secundaire databases. Op deze manier als een regio offline is, slechts 50% van Hallo betaald klanten databases worden beïnvloed en toofail via hebben. Hallo blijven andere databases behouden. Deze configuratie wordt weergegeven in het volgende diagram Hallo:

![Afbeelding 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-7.png)

Als in Hallo vorige scenario's Hallo management databases behoorlijk actief zijn zodat ze configureren als individuele databases geogerepliceerde (1). Dit zorgt ervoor Hallo voorspelbare prestaties van de nieuwe klantabonnementen hello, profielupdates en andere beheerbewerkingen. Regio A is de primaire regio Hallo voor Hallo management databases en Hallo regio B wordt gebruikt voor herstel van Hallo management-databases.

Hallo betalende klant tenant databases zijn ook geogerepliceerde maar met primaire en secundaire servers verdeeld tussen regio A en B (2) de regio. Op deze manier Hallo tenant primaire databases beïnvloed door Hallo storing kunnen failover toohello andere regio en beschikbaar is. Hallo andere helft Hallo tenant databases zijn niet van invloed op alle. 

Hallo volgende diagram illustreert Hallo herstel stappen tootake als er een storing optreedt in regio A.

![Afbeelding 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-8.png)

* Onmiddellijk een failover Hallo management databases tooregion B (3).
* Wijzigen van de toepassing hello verbinding tekenreeks toopoint toohello management databases in de regio B. wijzigen Hallo management databases toomake ervoor dat nieuwe accounts Hallo en tenant-databases worden gemaakt in de regio B en Hallo bestaande tenant databases zijn er gevonden als goed. Hallo bestaande proefversie klanten hun eigen gegevens zien tijdelijk niet beschikbaar.
* Failover-overschakeling van de tenant Hallo betaald databases toopool 2 in de regio B tooimmediately herstellen hun beschikbaarheid (4). Aangezien Hallo failover een snelle metagegevens niveau wijzigen is, kunt u overwegen een optimalisatie waar Hallo afzonderlijke failovers door Hallo eindgebruiker verbindingen zijn geactiveerd op verzoek. 
* Aangezien nu toepassingen 2 alleen primaire databases bevat, Hallo totale werkbelasting in Hallo groep toeneemt en mogelijk onmiddellijk groter eDTU (5). 
* Hallo nieuwe elastische pool maken met Hallo dezelfde naam geven en Hallo dezelfde configuratie in Hallo regio B voor Hallo proefversie klanten databases (6). 
* Eenmaal Hallo toepassingen gebruik geo-restore toorestore Hallo afzonderlijke proeftenant database gemaakt in de groep hello (7). U kunt overwegen activerende Hallo afzonderlijke herstelacties door Hallo eindgebruiker verbindingen of sommige andere toepassingsspecifieke prioriteit schema gebruiken.

> [!NOTE]
> Hallo failover-bewerking is asynchroon. hersteltijd toominimize hello, is het belangrijk dat u Hallo tenant databases failover-opdracht in batches van ten minste 20 databases uitvoeren. 
> 

Op dit moment is uw toepassing weer online in regio B. Alle betalende gebruikers hebben toegang tot gegevens tootheir terwijl Hallo proefversie klanten treedt vertraging op wanneer de toegang tot hun gegevens.

Wanneer een regio kunnen worden hersteld moet u als u wilt dat toouse regio B voor de proefversie klanten of failback toousing Hallo proefversie klanten van toepassingen in de regio A. toodecide Een criteria zijn Hallo % proeftenant databases is gewijzigd sinds Hallo herstel. Ongeacht deze beslissing moet u toore saldo Hallo betaald tenants tussen twee groepen. Hallo volgende diagram illustreert het proces voor het Hallo wanneer Hallo proeftenant databases back tooregion A. mislukken  

![Afbeelding 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-9.png)

* Annuleer alle openstaande geo-restore aanvragen tootrial DR-groep.   
* Failover-overschakeling Hallo Beheerdatabase (8). Na het herstel van het Hallo-regio is de oude primaire Hallo automatisch Hallo secundaire geworden. Nu wordt het Hallo opnieuw primaire.  
* Selecteer welke databases betaald tenant mislukken back toopool 1 en initiëren failover tootheir secundaire replica's (9). Na het herstel van de regio Hallo werden alle databases in de groep 1 automatisch secundaire replica's. Nu 50% van deze primaire opnieuw worden. 
* Hallo verkleinen van groep 2 toohello oorspronkelijke eDTU (10).
* Alle hersteld proefversie databases in Hallo regio B tooread alleen-lezen (11).
* Voor elke database in het proefabonnement DR toepassingen hello, die is gewijzigd sinds Hallo herstel, hernoemen of verwijderen van de bijbehorende database Hallo in Hallo proefversie primaire-pool (12). 
* Kopiëren Hallo bijgewerkt databases van Hallo DR groep toohello primaire groep (13). 
* Hallo DR-groep (14) verwijderen 

Hallo sleutel **voordelen** van deze strategie zijn:

* Het ondersteunt Hallo agressief SLA voor klanten betalen omdat Hiermee zorgt u ervoor dat een storing kan geen invloed heeft op meer dan 50% van de tenant-databases Hallo Hallo. 
* Dit zorgt ervoor Hallo nieuwe proefversies zijn geblokkeerd zodra Hallo audittrail DR-groep is gemaakt tijdens het Hallo-herstel. 
* Kunt u efficiënter gebruikmaken van de groepscapaciteit Hallo als 50% van de secundaire databases in groep 1 en 2 van de toepassingen zijn gegarandeerd toobe minder actieve dan primaire Hallo-databases.

Hallo belangrijkste **-en nadelen** zijn:

* Hallo CRUD-bewerkingen op Hallo management databases hebben lagere latentie voor Hallo eindgebruikers verbonden tooregion A dan voor Hallo eindgebruikers verbonden tooregion B, zoals ze worden uitgevoerd tegen Hallo primaire van Hallo management databases.
* Complexere ontwerp van Hallo management database vereist. Elke record tenant heeft bijvoorbeeld een locatiecode waarvoor toobe gewijzigd tijdens failover en failback.  
* Hallo betalende klanten ondervinden lagere prestaties dan normaal totdat hello upgrade van de groep van toepassingen in regio B is voltooid. 

## <a name="summary"></a>Samenvatting
Dit artikel is gericht op Hallo disaster recovery strategieën voor het Hallo databaselaag gebruikt door een multitenant SaaS ISV toepassing. Hallo strategie die u kiest is op basis van Hallo behoeften van de toepassing hello, zoals bedrijfsmodel hello, Hallo SLA u wilt dat toooffer tooyour klanten, budget beperking enzovoort. Elk beschreven strategie overzichten Hallo voordelen en afweging zodat u een gefundeerde beslissing nemen kunt. Uw specifieke toepassing die waarschijnlijk is tevens andere Azure-onderdelen. Zodat u hun zakelijke continuïteit richtlijnen bekijken en Hallo herstel van de databaselaag Hallo met hen organiseren. toolearn meer informatie over het beheren van herstel van databasetoepassingen in Azure, te verwijzen[cloudoplossingen ontwerpen voor herstel na noodgevallen](sql-database-designing-cloud-solutions-for-disaster-recovery.md).  

## <a name="next-steps"></a>Volgende stappen
* toolearn over Azure SQL Database automatische back-ups, Zie [geautomatiseerde back-ups van SQL-Database](sql-database-automated-backups.md).
* Zie voor een overzicht van zakelijke continuïteit en scenario's [Business continuity overview](sql-database-business-continuity.md).
* toolearn over het gebruik van automatische back-ups voor herstel, Zie [een database terugzetten vanuit Hallo service geïnitieerde back-ups](sql-database-recovery-using-backups.md).
* Zie toolearn over opties voor sneller herstel [actieve geo-replicatie](sql-database-geo-replication-overview.md).
* toolearn over het gebruik van automatische back-ups voor archivering, Zie [kopiëren van de database](sql-database-copy.md).

