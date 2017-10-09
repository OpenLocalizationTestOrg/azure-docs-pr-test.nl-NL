---
title: maximaal beschikbare aaaDesign-service met behulp van Azure SQL Database | Microsoft Docs
description: Meer informatie over het ontwerp van de toepassing voor maximaal beschikbare services met Azure SQL Database.
keywords: "herstel na noodgevallen, oplossingen voor herstel na noodgevallen, back-up van app-gegevens, geo-replicatie, cloud zakelijke continuïteit plannen"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: e8a346ac-dd08-41e7-9685-46cebca04582
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 04/21/2017
ms.author: sashan
ms.openlocfilehash: 815f754ba7014cd8a1108a2d84c2a8f71d7030a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-services-using-azure-sql-database"></a>Maximaal beschikbare services met behulp van Azure SQL Database ontwerpen

Bij het maken en implementeren van maximaal beschikbare services in Azure SQL-Database, gebruikt u [failover groepen en actieve geo-replicatie](sql-database-geo-replication-overview.md) tooprovide herstelmogelijkheden tooregional fouten en catastrofale uitval en schakel snel herstel toohello secundaire databases. Dit artikel is gericht op algemene patronen van de toepassing en Hallo voordelen en -en nadelen van elke optie, afhankelijk van Hallo toepassing implementatievereisten, Hallo serviceovereenkomst u ontwikkelt, verkeer latentie en kosten. Zie voor meer informatie over actieve geo-replicatie met elastische Pools [elastische Pool disaster recovery strategieën](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

## <a name="design-pattern-1-active-passive-deployment-for-cloud-disaster-recovery-with-a-co-located-database"></a>Bij een ontwerppatroon 1: implementatie actief / passief voor noodherstel voor cloud met een CO-locaties database
Deze optie is het meest geschikt voor toepassingen met Hallo volgende kenmerken:

* Actieve instantie in één Azure-regio
* Sterke afhankelijkheid van alleen-lezen (RW) toegang toodata
* Regio-overschrijdende connectiviteit tussen Hallo-webtoepassing en Hallo-database is niet acceptabel vanwege toolatency en verkeer kosten    

In dit geval wordt Hallo toepassing implementatietopologie geoptimaliseerd voor het verwerken van regionale noodsituaties als alle toepassingsonderdelen worden beïnvloed en toofailover als eenheid moeten. Voor geografische redundantie Hallo toepassingslogica en Hallo database zijn gerepliceerde tooanother regio maar ze worden niet gebruikt voor de werkbelasting van de toepassing hello onder normale omstandigheden Hallo. Hallo-toepassing in Hallo secundaire regio worden geconfigureerde toouse een SQL-verbinding tekenreeks toohello secundaire database. Het Traffic manager is ingesteld op toouse [routeringsmethode voor failover](../traffic-manager/traffic-manager-configure-failover-routing-method.md).  

> [!NOTE]
> [Azure traffic manager](../traffic-manager/traffic-manager-overview.md) alleen ter illustratie in dit artikel wordt gebruikt. U kunt een oplossing voor taakverdeling die ondersteuning biedt voor routeringsmethode voor failover.    
>

Hallo volgende diagram ziet u deze configuratie voordat een storing.

![Configuratie van SQL Database-geo-replicatie. Herstel na noodgevallen voor een cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-1.png)

Na een storing in de primaire regio Hallo detecteert Hallo SQL Database-service die Hallo primaire database is niet toegankelijk en een failover-toohello secundaire database op basis van de parameters Hallo Hallo automatische failover-beleid wordt geactiveerd. Afhankelijk van de SLA voor uw toepassing, kunt u tooconfigure een respijtperiode tussen Hallo detectie Hallo uitval en Hallo failover zelf bepalen. Configureren van een respijtperiode wordt verkleind Hallo gegevens verloren gaan toohello gevallen waarbij Hallo onderbreking onherstelbare is en beschikbaarheid in regio Hallo snel kan niet worden hersteld. Hallo eindpunt failover wordt geïnitieerd door Hallo traffic manager voordat Hallo failover groep triggers Hallo failover van Hallo-database, is webtoepassing Hallo niet als kunnen tooreconnect toohello database. van de toepassing Hello poging tooreconnect slaagt automatisch zodra Hallo database failover is voltooid. 

> [!NOTE]
> tooachieve volledig gecoördineerde failover van de toepassing hello en Hallo-databases, moet u uw eigen bewaking methode ontwerpen en handmatige failover van Hallo web application eindpunten en Hallo databases gebruiken.
>

Nadat de failover van zowel de eindpunten en de database Hallo Hallo-toepassing hello is voltooid, Hallo toepassing wordt opnieuw gestart voor het verwerken van gebruikersaanvragen Hallo in Hallo regio B en CO-locaties met Hallo database blijft omdat Hallo primaire database zich nu in regio B. Dit scenario wordt weergegeven in het volgende diagram Hallo. In alle diagrammen ononderbroken lijnen geven actieve verbindingen, aangegeven door stippellijn onderbroken verbindingen en stop tekenen geven actie triggers.

![Geo-replicatie: Failover toosecondary database. App-gegevens back-up.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-2.png)

Als een storing in de secundaire regio hello gebeurt, Hallo replicatiekoppeling tussen Hallo primaire en secundaire database Hallo is onderbroken, maar Hallo failover is niet geactiveerd omdat de primaire database Hallo wordt niet negatief beïnvloed. beschikbaarheid van de toepassing Hello niet in dit geval wordt gewijzigd, maar toepassing hello blootgestelde werkt en daarom hoger risico in geval beide regio's mislukken achter elkaar.

> [!NOTE]
> Voor herstel na noodgevallen aangeraden het Hallo-configuratie met de toepassing implementatie beperkt tootwo regio's. Dit komt doordat de meeste Hallo Azure locaties slechts twee regio's hebben. Deze configuratie biedt geen bescherming van uw toepassing van een gelijktijdige catastrofale uitval van beide regio's.  U kunt uw databases in een derde regio met herstellen in een onwaarschijnlijke geval van een dergelijke storing [geo-restore-bewerking](sql-database-disaster-recovery.md#recover-using-geo-restore).
>

Wanneer Hallo onderbreking is verholpen, wordt secundaire database hello automatisch opnieuw synchroniseren met primaire Hallo. Tijdens de synchronisatie worden de prestaties van de primaire Hallo kan enigszins beïnvloed, afhankelijk van de hoeveelheid gegevens die moeten worden gesynchroniseerd toobe Hallo. Hallo illustreert volgende diagram een storing in Hallo secundaire regio.

![Secundaire database gesynchroniseerd met de primaire. Herstel na noodgevallen voor een cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-3.png)

Hallo sleutel **voordelen** van dit ontwerppatroon zijn:

* Hallo is dezelfde webtoepassing geïmplementeerde tooboth regio's zonder een willekeurige regio-specifieke configuratie en geen aanvullende logica tooreact toohello failover. 
* Hallo toepassingsprestaties wordt niet beïnvloed door failover als Hallo-webtoepassing en Hallo database zijn altijd CO-locaties.

Hallo belangrijkste **afweging** is dat redundante toepassing hello exemplaar in de secundaire regio hello wordt alleen gebruikt voor herstel na noodgevallen.

## <a name="design-pattern-2-active-active-deployment-for-application-load-balancing"></a>Bij een ontwerppatroon 2: implementatie van de actieve toepassing load balancing
Deze optie voor herstel na noodgevallen cloud is het meest geschikt voor toepassingen met Hallo volgende kenmerken:

* Maximale ratio van database leest toowrites
* Database-latentie is belangrijker voor Hallo eindgebruikerservaring dan Hallo schrijflatentie lezen 
* Alleen-lezen logica kan worden gescheiden van de logica lezen-schrijven met behulp van een andere verbindingsreeks
* Alleen-lezen logica is niet afhankelijk van gegevens volledig worden gesynchroniseerd met de nieuwste updates Hallo  

Als uw toepassingen deze kenmerken hebben, Hallo eindgebruiker verbindingen voor taakverdeling over meerdere exemplaren van een toepassing in verschillende regio's aanzienlijk kan verbeteren Hallo algehele ervaring voor de eindgebruiker. Twee Hallo regio's als Hallo DR-paar moet worden geselecteerd en Hallo failover groep Hallo databases in deze regio's moet worden opgenomen. tooimplement load balancing, moet elke regio hebben een actief exemplaar van de toepassing hello met Hallo lezen-schrijven (RW) logica verbonden toohello lezen-schrijven listener eindpunt van Hallo failover-groep. Het wordt gegarandeerd dat de failover is hello wordt automatisch worden gestart als de primaire database hello wordt beïnvloed door een storing. Hallo alleen-lezen logica (RO) in de webtoepassing Hallo moet verbinding maken met rechtstreeks toohello database in deze regio. Het Traffic manager moet worden ingesteld in toouse [prestaties routering](../traffic-manager/traffic-manager-configure-performance-routing-method.md) met [eindpunt bewaking](../traffic-manager/traffic-manager-monitoring.md) ingeschakeld voor elk toepassingsexemplaar.

Zoals in het patroon #1, moet u een vergelijkbare monitoring-toepassing implementeren. Maar in tegenstelling tot patroon #1 monitoring-toepassing hello niet verantwoordelijk is voor activering Hallo eindpunt failover.

> [!NOTE]
> Terwijl dit patroon maakt gebruik van meer dan één secundaire database, alleen hello secundaire regio b zou worden gebruikt voor de failover- en moet deel uitmaken van Hallo failover-groep.
>

Het Traffic manager moet worden geconfigureerd voor de geografische locatie prestaties routering toodirect Hallo gebruiker verbindingen toohello toepassing exemplaar dichtstbijzijnde toohello van gebruiker. Hallo volgende diagram ziet u deze configuratie voordat een storing.

![Er is geen onderbreking: prestaties routering toonearest toepassing. Geo-replicatie.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-1.png)

Als een onderbreking van de database is gedetecteerd in Hallo regio A, starten Hallo failover groep failover van primaire database in een regio toohello secundaire regio B. Hallo automatisch Hallo lezen-schrijven listener eindpunt tooregion B wordt ook automatisch bijgewerkt zodat alleen-lezen verbindingen in Hallo-webtoepassing wordt niet beïnvloed. Hallo traffic manager Hallo routeringstabel uitsluiten van offline Hallo-eindpunt maar gaat verder met routering Hallo eindgebruiker verkeer toohello resterende online-exemplaren. Hallo SQL-verbindingsreeksen alleen-lezen is niet van invloed als ze altijd toohello database punt in Hallo dezelfde regio. 

Hallo volgende diagram ziet u de nieuwe configuratie Hallo na een failover Hallo.

![Configuratie na een failover. Herstel na noodgevallen voor een cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-2.png)

In geval van een storing in een van de secundaire regio's Hallo wordt Hallo traffic manager automatisch verwijderd Hallo offline eindpunt in deze regio uit Hallo-routeringstabel. Hallo kanaal toohello secundaire replicatiedatabase in deze regio zal worden onderbroken. Omdat de overige gebieden Hallo u extra gebruikersverkeer in dit scenario, worden Hallo toepassingsprestaties beïnvloed tijdens het Hallo-storing. Zodra de onderbreking hello wordt verholpen, hello secundaire database in de betrokken regio Hallo onmiddellijk gesynchroniseerd Hello primaire. Tijdens het Hallo worden de synchronisatieprestaties van Hallo primaire kan enigszins beïnvloed, afhankelijk van de hoeveelheid gegevens die moeten worden gesynchroniseerd toobe Hallo. Hallo volgende diagram ziet u een storing in regio B.

![Storing in een secundaire regio. Noodherstel voor cloud - geo-replicatie.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-3.png)

Hallo sleutel **voordeel** van dit ontwerp is patroon Hallo toepassing werklast over meerdere secundaire replica's tooachieve Hallo eindgebruiker voor optimale prestaties kunt schalen. Hallo **voor-en nadelen** van deze optie zijn:

* Alleen-lezen verbindingen tussen toepassingsexemplaren Hallo en database hebben verschillende latentie en kosten
* Tijdens het Hallo storing is van invloed op toepassingsprestaties

> [!NOTE]
> Een soortgelijke benadering kan worden gebruikt toooffload gespecialiseerde werkbelastingen, zoals rapportage van taken, hulpprogramma's voor bedrijfsinformatie of back-ups. Normaal gesproken deze werkbelastingen aanzienlijke databaseresources verbruiken daarom wordt aanbevolen dat u een Hallo secundaire databases voor hen met Hallo prestaties niveau overeenkomende toohello verwachte werkbelasting wijst.
>

## <a name="design-pattern-3-active-passive-deployment-for-data-preservation"></a>Bij een ontwerppatroon 3: actief / passief-implementatie voor het behoud van gegevens
Deze optie is het meest geschikt voor toepassingen met Hallo volgende kenmerken:

* Verlies van gegevens is grote zakelijke risico. Hallo database failover kan alleen worden gebruikt als een laatste toevlucht als Hallo onderbreking onherstelbare is.
* Hallo toepassing ondersteunt alleen-lezen en lees-/ modi van bewerkingen en kan werken in 'alleen-lezen-modus' voor een bepaalde periode.

In dit patroon wordt toepassing hello tooread alleen-lezen-modus als Hallo alleen-lezen verbindingen start time-outfouten ophalen. Hallo-webtoepassing is geïmplementeerde tooboth regio's en bevatten verbindingseindpunt toohello lezen / schrijven-listener en een andere verbinding toohello alleen-lezen-listener-eindpunt. Hallo Traffic manager moet worden ingesteld in toouse [failover-routering](../traffic-manager/traffic-manager-configure-failover-routing-method.md) met [eindpunt bewaking](../traffic-manager/traffic-manager-monitoring.md) ingeschakeld voor het eindpunt van toepassing hello in elke regio.

Hallo volgende diagram ziet u deze configuratie voordat een storing.

![Actief / passief-implementatie voor failover. Herstel na noodgevallen voor een cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-1.png)

Als Hallo traffic manager een connectiviteit fout tooregion A detecteert, verandert deze automatisch verkeer toohello toepassing gebruikersexemplaar in regio B. Met dit patroon is het belangrijk dat u de respijtperiode Hallo met gegevens verloren gaan tooa voldoende hoge waarde, bijvoorbeeld 24 uur. Dit zorgt ervoor dat gegevens verloren gaan als Hallo onderbreking is verholpen in die tijd is voorkomen. Wanneer Hallo webtoepassing in Hallo regio B is geactiveerd zal Hallo lees-/ schrijfbewerkingen mislukken. Op dat moment moet deze overschakelen toohello alleen-lezen-modus. In deze modus Hallo aanvragen worden automatisch gerouteerde toohello secundaire database. In geval van een onherstelbare fout Hallo Hallo storing niet worden verholpen binnen de respijtperiode Hallo en Hallo failover groep Hallo failover wordt geactiveerd. Na deze Hallo wordt lezen / schrijven-listener beschikbaar en Hallo aanroepen tooit stopt mislukken. Dit wordt geïllustreerd door het volgende diagram Hallo.

![Storing: De toepassing in de modus alleen-lezen. Herstel na noodgevallen voor een cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-2.png)

Als Hallo onderbreking in de primaire regio Hallo binnen de respijtperiode hello wordt verholpen, traffic manager Hallo herstel van de verbinding in de primaire regio Hallo detecteert en verandert verkeer back toohello toepassing gebruikersexemplaar in regio A. Dat toepassingsexemplaar wordt hervat en werkt in de modus lezen / schrijven met behulp van de primaire database Hallo in regio A.

Bij een stroomstoring in Hallo regio B detecteert Hallo traffic manager Hallo mislukt Hallo toepassing eindpunt in regio B en Hallo failover groep switches Hallo alleen-lezen-listener tooregion A. Hallo eindgebruikerservaring heeft geen gevolgen voor de onderbreking van deze maar Hallo primaire database zichtbaar tijdens Hallo storing. Dit wordt geïllustreerd door het volgende diagram Hallo.

![Storing: Secundaire database. Herstel na noodgevallen voor een cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-3.png)

Zodra Hallo onderbreking is verholpen, hello secundaire database is onmiddellijk gesynchroniseerd met primaire Hallo en Hallo alleen-lezen-listener is uitgeschakeld back toohello secundaire database in regio B. Tijdens de synchronisatie worden de prestaties van de primaire Hallo kan enigszins beïnvloed, afhankelijk van de hoeveelheid gegevens die moeten worden gesynchroniseerd toobe Hallo.

Dit ontwerppatroon heeft diverse **voordelen**:

* Dit voorkomt het verlies van gegevens tijdens Hallo tijdelijke storingen.
* Uitvaltijd is afhankelijk van alleen hoe snel Hallo verbindingsfout optreedt, kan worden geconfigureerd in het traffic manager wordt gedetecteerd.

Hallo **afweging** is:

* Toepassing moet kunnen toooperate in de modus alleen-lezen.

> [!NOTE]
> In geval van een permanente servicestoring in Hallo regio u handmatig database failover activeren en accepteren Hallo gegevens verloren gaan. Hallo toepassing zal Hallo secundaire regio met lees-/ schrijftoegang toohello database functioneel zijn.
>

## <a name="business-continuity-planning-choose-an-application-design-for-cloud-disaster-recovery"></a>Zakelijke continuïteit planning: Kies het ontwerp van een toepassing voor noodherstel voor cloud
Uw strategie voor noodherstel specifieke cloud kunt combineren of breid deze ontwerppatronen toobest Hallo voldoen aan de behoeften van uw toepassing.  Zoals eerder vermeld, worden Hallo-strategie die u kiest is gebaseerd op Hallo SLA gewenste toooffer tooyour klanten en Hallo implementatietopologie van toepassing. toohelp hulplijn uw beslissing, Hallo volgende tabel vergelijkt Hallo keuzes op basis van Hallo schatting van de gegevens verlies of herstel beoogde herstelpunt (RPO) en de geschatte hersteltijd (invoegen).

| patroon | RPO | INVOEGEN |
|:--- |:--- |:--- |
| Actief / passief-implementatie voor herstel na noodgevallen met toegang tot de database met CO-locaties |Lees-/ schrijftoegang sec < 5. |Fout detectietijd + DNS TTL |
| Implementatie van de actieve toepassing load balancing |Lees-/ schrijftoegang sec < 5. |Fout detectietijd + DNS TTL |
| Actief / passief-implementatie voor het behoud van gegevens |Alleen-lezentoegang sec < 5. | Alleen-lezentoegang = 0 |
||Lees-/ schrijftoegang = nul | Lees-/ schrijftoegang = fout detectietijd + respijtperiode met verlies van gegevens |
|||

## <a name="next-steps"></a>Volgende stappen
* toolearn over Azure SQL Database automatische back-ups, Zie [geautomatiseerde back-ups van SQL-Database](sql-database-automated-backups.md)
* Zie voor een overzicht van zakelijke continuïteit en scenario's [Business continuity-overzicht](sql-database-business-continuity.md)
* toolearn over het gebruik van automatische back-ups voor herstel, Zie [een database terugzetten vanuit Hallo service geïnitieerde back-ups](sql-database-recovery-using-backups.md)
* Zie toolearn over opties voor sneller herstel [actieve geo-replicatie](sql-database-geo-replication-overview.md)  
* toolearn over het gebruik van automatische back-ups voor archivering, Zie [kopiëren van de database](sql-database-copy.md)
* Zie voor meer informatie over actieve geo-replicatie met elastische Pools [elastische Pool disaster recovery strategieën](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
