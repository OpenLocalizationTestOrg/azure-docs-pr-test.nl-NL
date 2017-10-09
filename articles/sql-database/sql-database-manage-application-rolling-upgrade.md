---
title: aaaRolling toepassingsupgrades - Azure SQL Database | Microsoft Docs
description: Meer informatie over hoe Azure SQL Database geo-replicatie toouse toosupport online upgrades van uw cloudtoepassing.
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 58f42859-1e37-463c-a3d8-a3ca2e867148
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/16/2016
ms.author: sashan
ms.openlocfilehash: 18c56300916d129bff141624cc5c416b500408d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-rolling-upgrades-of-cloud-applications-using-sql-database-active-geo-replication"></a>Het beheren van rollende upgrades van cloud-toepassingen met behulp van SQL-Database actieve geo-replicatie
> [!NOTE]
> [Actieve geo-replicatie](sql-database-geo-replication-overview.md) is nu beschikbaar voor alle databases in alle lagen.
> 

Meer informatie over hoe toouse [geo-replicatie](sql-database-geo-replication-overview.md) in SQL-Database tooenable rolling upgrades van uw cloudtoepassing. Omdat de upgrade is een bewerking verstoren, moet het deel van uw zakelijke continuïteit planning en ontwerp. In dit artikel we twee verschillende methoden organiseren Hallo kijken upgradeproces en bespreken Hallo voordelen en -en nadelen van elke optie. Voor de toepassing hello van dit artikel gebruiken we een eenvoudige toepassing die uit een website verbonden tooa individuele database als de gegevenslaag bestaat. Ons doel is tooupgrade versie 1 van Hallo toepassing tooversion 2 zonder aanzienlijke invloed op Hallo eindgebruikerservaring. 

Bij het evalueren van de upgradeopties Hallo moet u Hallo volgende factoren overwegen:

* De impact op de beschikbaarheid van de toepassing tijdens upgrades. Hoe lang Hallo toepassing functie mogelijk beperkt of gedegradeerd.
* Mogelijkheid tooroll terug in het geval van een upgrade mislukt.
* De kwetsbaarheid van de toepassing hello als een niet-verwante onherstelbare fout tijdens de upgrade Hallo optreedt.
* Totaal aantal dollar kosten.  Dit omvat aanvullende redundantie en incrementele kosten van tijdelijke Hallo-onderdelen die door het upgradeproces hello worden gebruikt. 

## <a name="upgrading-applications-that-rely-on-database-backups-for-disaster-recovery"></a>Bijwerken van toepassingen die afhankelijk van de databaseback-ups voor herstel na noodgevallen zijn
Als uw toepassing afhankelijk van automatische databaseback-ups is en geo-herstel voor herstel na noodgevallen gebruikt, is het meestal geïmplementeerde tooa één Azure-regio. In dit geval omvat Hallo upgradeproces het maken van een back-implementatie van alle onderdelen die zijn betrokken bij een upgrade van Hallo. toominimize wordt u gebruikmaken van Azure Traffic Manager (WATM) met Hallo failover profiel Hallo overlast.  Hallo volgende diagram illustreert Hallo operationele omgeving eerdere toohello upgradeproces. Hallo eindpunt <i>contoso 1.azurewebsites.net</i> vertegenwoordigt een productiesite van Hallo-toepassing die toobe bijgewerkt behoeften. tooenable hello mogelijkheid tooroll terug Hallo upgrade, moet u een fase sleuf maken met een volledig gesynchroniseerde kopie van de toepassing hello. Hallo zijn volgende stappen vereist tooprepare Hallo toepassing hello upgrade:

1. Een fase sleuf maken voor Hallo upgrade. toodo die een secundaire database (1) maken en implementeren van een identieke website in Hallo dezelfde Azure-regio. Hallo secundaire toosee bewaken als Hallo seeding van proces is voltooid.
2. Een failover-profiel maken in WATM met <i>contoso 1.azurewebsites.net</i> als online-eindpunt en <i>contoso 2.azurewebsites.net</i> als offline. 

> [!NOTE]
> Opmerking Hallo voorbereidende stappen heeft geen invloed op de toepassing hello in productiesite Hallo en deze kan worden gebruikt in de modus volledige toegang.
>  

![Configuratie van SQL Database Ga-replicatie. Herstel na noodgevallen voor een cloud.](media/sql-database-manage-application-rolling-upgrade/Option1-1.png)

Zodra Hallo voorbereidende stappen zijn voltooid Hallo toepassing is gereed voor de daadwerkelijke upgrade Hallo. Hallo volgende diagram illustreert Hallo stappen voor het Hallo-upgradeproces. 

1. De primaire database Hallo in Hallo productie sleuf tooread alleen-lezen-modus (3) instellen. Dit wordt gegarandeerd dat Hallo productie-exemplaar van de toepassing hello (V1) blijven alleen-lezen tijdens de upgrade van Hallo waardoor wordt voorkomen dat de gegevensdivergentie Hallo tussen hello V1- en V2-database-exemplaren.  
2. Verbreek de verbinding met de secundaire database Hallo Hallo geplande beëindiging modus (4). Er wordt een volledig gesynchroniseerde onafhankelijke kopie van de primaire database Hallo gemaakt. Deze database wordt bijgewerkt.
3. Hallo primaire database tooread schrijven modus inschakelen en Hallo upgrade-script uitvoeren in Hallo fase sleuf (5).     

![Configuratie van SQL Database-geo-replicatie. Herstel na noodgevallen voor een cloud.](media/sql-database-manage-application-rolling-upgrade/Option1-2.png)

Als het Hallo-upgrade is voltooid maar u bent nu klaar tooswitch Hallo eindgebruikers toohello gefaseerde kopie Hallo toepassing. Deze worden nu de productiesite Hallo van Hallo-toepassing.  Dit omvat het een paar meer stappen zoals wordt geïllustreerd op Hallo volgende diagram.

1. Hallo online endpoint te schakelen in Hallo WATM profiel<i>contoso 2.azurewebsites.net</i>, welke punten toohello V2-versie van Hallo-website (6). Nu wordt het Hallo-productiesite Hello V2-toepassing en Hallo eindgebruiker verkeer gerichte tooit is.  
2. U hoeft niet meer Hallo V1-toepassingsonderdelen zodat u veilig kunt verwijderen (7).   

![Configuratie van SQL Database-geo-replicatie. Herstel na noodgevallen voor een cloud.](media/sql-database-manage-application-rolling-upgrade/Option1-3.png)

Als Hallo upgradeproces mislukt is, bijvoorbeeld vanwege fout in Hallo upgrade-script, tooan Hallo fase sleuf moet worden overwogen aangetast. tooroll back Hallo toohello vóór de upgrade toepassingsstatus u gewoon de toepassing hello in Hallo productie sleuf toofull toegang herstellen. Hallo-stappen worden op Hallo volgende diagram weergegeven.    

1. Hallo-database kopiëren tooread schrijven modus (8) instellen. Hiermee herstelt u volledige V1 functioneel in de productiesite Hallo Hallo.
2. Hallo hoofdmap oorzaak analyses uitvoeren en Hallo geknoeid onderdelen verwijderen in Hallo fase sleuf (9). 

Op dit moment Hallo toepassing volledig functioneel is en Hallo Upgradestappen kunnen worden herhaald.

> [!NOTE]
> Hallo terugdraaien vereist geen wijzigingen in WATM profiel als deze al te verwijst<i>contoso 1.azurewebsites.net</i> zoals Hallo actief eindpunt.
> 
> 

![Configuratie van SQL Database-geo-replicatie. Herstel na noodgevallen voor een cloud.](media/sql-database-manage-application-rolling-upgrade/Option1-4.png)

Hallo sleutel **voordeel** van deze optie is een toepassing in één regio met behulp van een aantal eenvoudige stappen te upgraden. Hallo dollar van Hallo upgrade is relatief laag. Hallo belangrijkste **afweging** is dat als er een onherstelbare fout optreedt tijdens Hallo upgrade Hallo toohello vóór de upgrade herstelstatus eruit ziet nieuwe implementatie van de toepassing hello in een andere regio en het Hallo-database herstellen van back-up met behulp van geo-herstel. Dit proces zal leiden tot aanzienlijke downtime.   

## <a name="upgrading-applications-that-rely-on-database-geo-replication-for-disaster-recovery"></a>Bijwerken van toepassingen die afhankelijk van de database geo-replicatie voor herstel na noodgevallen zijn
Als uw toepassing gebruikmaakt van geo-replicatie voor bedrijfscontinuïteit, is het geïmplementeerde tooat minimaal twee verschillende regio's met een actieve implementatie in de primaire regio en een stand-by-implementatie in de regio van de back-up. Bovendien vermeld toohello factoren eerder, Hallo upgradeproces moet garanderen dat:

* Hallo-toepassing blijft te allen tijde tijdens het upgradeproces Hallo onherstelbare fouten beveiligd
* Hallo geografisch redundante componenten van de toepassing hello zijn parallel met actieve Hallo-onderdelen bijgewerkt

tooachieve deze doelstellingen die u zal gebruikmaken van Azure Traffic Manager (WATM) met behulp van failover Hallo profiel met een actieve en drie back-eindpunten.  Hallo volgende diagram illustreert Hallo operationele omgeving eerdere toohello upgradeproces. Hallo websites <i>contoso 1.azurewebsites.net</i> en <i>contoso dr.azurewebsites.net</i> vertegenwoordigen een productiesite van de toepassing hello met volledige geografische redundantie. tooenable hello mogelijkheid tooroll terug Hallo upgrade, moet u een fase sleuf maken met een volledig gesynchroniseerde kopie van de toepassing hello. Omdat u nodig hebt tooensure die toepassing hello snel herstellen kunt als een onherstelbare fout tijdens het upgradeproces hello optreedt, moet Hallo fase sleuf toobe geografisch redundante ook. Hallo zijn volgende stappen vereist tooprepare Hallo toepassing hello upgrade:

1. Een fase sleuf maken voor Hallo upgrade. toodo die een secundaire database (1) maken en implementeren van een identieke kopie van de website Hallo in Hallo dezelfde Azure-regio. Hallo secundaire toosee bewaken als Hallo seeding van proces is voltooid.
2. Een geografisch redundante secundaire database maken met Hallo fase sleuf van geo-replicatie Hallo secundaire database toohello back-regio (dit heet "teruggekoppeld geo-replicatie"). Back-up secundaire toosee Hallo bewaken als Hallo seeding van proces is voltooid (3).
3. Maken van een stand-by-kopie van het Hallo-website in de back-regio Hallo en koppel deze toohello geografisch redundante secundaire (4).  
4. Het toevoegen van extra eindpunten Hallo <i>contoso 2.azurewebsites.net</i> en <i>contoso 3.azurewebsites.net</i> toohello failover-profiel in WATM als offline eindpunten (5). 

> [!NOTE]
> Opmerking Hallo voorbereidende stappen heeft geen invloed op de toepassing hello in productiesite Hallo en deze kan worden gebruikt in de modus volledige toegang.
> 
> 

![Configuratie van SQL Database-geo-replicatie. Herstel na noodgevallen voor een cloud.](media/sql-database-manage-application-rolling-upgrade/Option2-1.png)

Zodra Hallo voorbereidende stappen zijn voltooid, is Hallo fase sleuf gereed voor upgrade Hallo. Hallo volgende diagram illustreert de Upgradestappen Hallo.

1. De primaire database Hallo instellen in Hallo productie sleuf tooread alleen-lezen-modus (6). Dit wordt gegarandeerd dat Hallo productie-exemplaar van de toepassing hello (V1) blijven alleen-lezen tijdens de upgrade van Hallo waardoor wordt voorkomen dat de gegevensdivergentie Hallo tussen hello V1- en V2-database-exemplaren.  
2. Verbreek de verbinding met de secundaire database Hallo in Hallo met behulp van dezelfde regio Hallo geplande beëindiging-modus (7). Er wordt een volledig gesynchroniseerde onafhankelijke kopie van de primaire database hello, wordt automatisch een primaire namelijk na beëindiging van Hallo gemaakt. Deze database wordt bijgewerkt.
3. Hallo primaire database in de modus voor Hallo fase sleuf tooread-schrijven en voeren Hallo upgrade-script (8).    

![Configuratie van SQL Database-geo-replicatie. Herstel na noodgevallen voor een cloud.](media/sql-database-manage-application-rolling-upgrade/Option2-2.png)

Als Hallo-upgrade is voltooid maar u bent nu klaar tooswitch Hallo eindgebruikers toohello V2-versie van Hallo-toepassing. Hallo volgende diagram illustreert Hallo stappen die nodig zijn.

1. Hallo actief eindpunt te schakelen in Hallo WATM profiel<i>contoso 2.azurewebsites.net</i>, welke nu verwijst toohello V2-versie van Hallo-website (9). Wordt nu een productiesite Hello V2-toepassing en eindgebruikers verkeer gerichte tooit is. 
2. Als u niet langer Hallo V1 toepassing zodat u veilig kunt verwijderen (10 en 11).  

![Configuratie van SQL Database-geo-replicatie. Herstel na noodgevallen voor een cloud.](media/sql-database-manage-application-rolling-upgrade/Option2-3.png)

Als Hallo upgradeproces mislukt is, bijvoorbeeld vanwege fout in Hallo upgrade-script, tooan Hallo fase sleuf moet worden overwogen aangetast. tooroll back Hallo toohello vóór de upgrade toepassingsstatus u toousing Hallo toepassing in de productiesite Hallo met volledige toegang herstellen. Hallo-stappen worden op Hallo volgende diagram weergegeven.    

1. Set Hallo primaire database-exemplaar in Hallo sleuf tooread schrijven productiemodus (12). Hiermee herstelt u volledige V1 functioneel in de productiesite Hallo Hallo.
2. Hallo hoofdmap oorzaak analyses uitvoeren en Hallo geknoeid onderdelen verwijderen in Hallo fase sleuf (13 en 14). 

Op dit moment Hallo toepassing volledig functioneel is en Hallo Upgradestappen kunnen worden herhaald.

> [!NOTE]
> Hallo terugdraaien vereist geen wijzigingen in WATM profiel als deze al te verwijst <i>contoso 1.azurewebsites.net</i> zoals Hallo actief eindpunt.
> 
> 

![Configuratie van SQL Database-geo-replicatie. Herstel na noodgevallen voor een cloud.](media/sql-database-manage-application-rolling-upgrade/Option2-4.png)

Hallo sleutel **voordeel** van deze optie is te upgraden zowel Hallo-toepassing en de geografisch redundante kopie parallel zonder uw zakelijke continuïteit tijdens de upgrade Hallo gevaar te brengen. Hallo belangrijkste **afweging** is dat het dubbele redundantie van elk toepassingsonderdeel vereist, en daarom hogere Dollarkosten maakt. Hierbij wordt ook een gecompliceerdere werkstroom. 

## <a name="summary"></a>Samenvatting
Hallo twee upgrade methoden die worden beschreven in artikel Hallo verschillen in complexiteit en het Hallo dollar kosten, maar ze zich richten op Hallo tijd wanneer de eindgebruiker Hallo beperkt tooread alleen-lezen bewerkingen is voor het minimaliseren. Die tijd is rechtstreeks door de duur Hallo van Hallo upgrade-script gedefinieerd. Is niet afhankelijk van de databasegrootte hello, Hallo servicetier u hebt geselecteerd, de websiteconfiguratie Hallo en andere factoren die u kunt eenvoudig niet controleren. Dit komt doordat alle Hallo voorbereidende stappen worden ontkoppeld van de Upgradestappen Hallo en zonder enige impact op Hallo productietoepassing kunnen worden gedaan. Hallo-efficiëntie van Hallo upgrade-script is Hallo van groot belang dat de eindgebruikerservaring Hallo tijdens upgrades bepaalt. Hallo van de beste manier kunt u deze verbeteren is dus uw inspanningen gericht op het Hallo-upgradescript zo efficiënt mogelijk te maken.  

## <a name="next-steps"></a>Volgende stappen
* Zie voor een overzicht van zakelijke continuïteit en scenario's [Business continuity overview](sql-database-business-continuity.md).
* toolearn over Azure SQL Database automatische back-ups, Zie [geautomatiseerde back-ups van SQL-Database](sql-database-automated-backups.md).
* toolearn over het gebruik van automatische back-ups voor herstel, Zie [een database herstellen via automatische back-ups](sql-database-recovery-using-backups.md).
* Zie toolearn over opties voor sneller herstel [actieve geo-replicatie](sql-database-geo-replication-overview.md).


