---
title: aaaQuery inzichten voor Azure SQL Database | Microsoft Docs
description: Query-prestaties controleren identificeert Hallo meeste CPU-verbruik wordt gevraagd om een Azure SQL Database.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a>Azure SQL Database Query Performance Insight
Is een uitdaging waarvoor aanzienlijke expertise en investeringen tijd beheren en optimaliseren van Hallo van relationele databases. Inzicht in queryprestaties kunt u toospend minder tijd databaseprestaties oplossen door de volgende Hallo:

* Dieper inzicht in uw databases brongebruik (DTU). 
* Hallo top-query's op het aantal CPU/duur/uitvoering, die mogelijk voor verbeterde prestaties kunnen worden afgestemd.
* Hallo mogelijkheid toodrill omlaag op Hallo gegevens van een query, geven de tekst en de geschiedenis van bronnen beter worden benut. 
* Prestaties afstemmen aantekeningen die acties uitgevoerd door weergeven [SQL Azure Database Advisor](sql-database-advisor.md)  



## <a name="prerequisites"></a>Vereisten
* Query Performance Insight vereist dat [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) actief is op uw database. Als de Query Store niet wordt uitgevoerd, Hallo portal wordt u gevraagd tooturn op.

## <a name="permissions"></a>Machtigingen
Hallo volgende [toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-what-is.md) machtigingen zijn vereist toouse Query Performance Insight: 

* **Lezer**, **eigenaar**, **Inzender**, **SQL DB Contributor**, of **SQL Server Inzender** machtigingen zijn vereist tooview Hallo bovenste resource verbruikt query's en -grafieken. 
* **Eigenaar**, **Inzender**, **SQL DB Contributor**, of **SQL Server Inzender** machtigingen zijn vereist tooview querytekst.

## <a name="using-query-performance-insight"></a>Met behulp van de Query Performance Insight
Inzicht in queryprestaties is eenvoudig toouse:

* Open [Azure-portal](https://portal.azure.com/) en zoeken naar database die u tooexamine wilt. 
  * Selecteer in de linkerkant menu onder ondersteuning en het oplossen van problemen 'Query Performance Insight'.
* Op het eerste tabblad Hallo, bekijk Hallo-lijst van bovenste resource verbruikende query's.
* Selecteer een afzonderlijke query tooview de details ervan.
* Open [SQL Azure Database Advisor](sql-database-advisor.md) en controleer of er geen aanbevelingen beschikbaar zijn.
* Schuifregelaars gebruiken of zoomen pictogrammen toochange waargenomen-interval.
  
    ![Prestatiedashboard](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> Een paar uur van gegevens moet toobe voor SQL-Database tooprovide query performance insights wordt vastgelegd door de Query Store. Als Hallo-database geen activiteiten heeft of Query Store gedurende een bepaalde periode niet actief was, is Hallo grafieken leeg om deze periode weer te geven. U kunt Query Store op elk gewenst moment inschakelen als deze niet wordt uitgevoerd.   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a>Bekijk de hoogste CPU verbruikt query 's
In Hallo [portal](http://portal.azure.com) Hallo te volgen:

1. Blader tooa SQL-database en klik op **alle instellingen** > **ondersteuning + probleemoplossing** > **Query performance insight**. 
   
    ![Inzicht in queryprestaties][1]
   
    Hallo top-query's weergeven wordt geopend en Hallo top CPU in beslag neemt-query's worden vermeld.
2. Klik op rond Hallo-grafiek voor meer informatie.<br>Hallo bovenlijn worden algemene DTU % voor Hallo-database, terwijl Hallo balken CPU-percentage verbruikt door query's Hallo geselecteerd tijdens de geselecteerde hello-interval weergeven (bijvoorbeeld als **afgelopen week** is geselecteerd elke balk vertegenwoordigt één dag).
   
    ![Top-query 's][2]
   
    Hallo onder raster vertegenwoordigt de verzamelde informatie voor Hallo zichtbaar query's.
   
   * Query-ID - de unieke id van de query in de database.
   * CPU per query tijdens waarneembare interval (afhankelijk van statistische functie).
   * Duur per query (afhankelijk van statistische functie).
   * Totaal aantal uitvoeringen voor een bepaalde query.
     
     Selecteren of wissen tooinclude afzonderlijke query's of uitsluiten Hallo grafiek met behulp van de selectievakjes uit.
3. Als uw gegevens verlopen is, klikt u op Hallo **vernieuwen** knop.
4. U kunt gebruiken schuifregelaars en zoomen knoppen toochange observatie-interval en onderzoeken pieken: ![instellingen](./media/sql-database-query-performance/zoom.png)
5. Als u een andere weergave wilt, u kunt eventueel selecteren **aangepaste** tabblad en ingesteld:
   
   * Metrische gegevens (CPU, duur, het aantal keer uitgevoerd)
   * Tijdsinterval (afgelopen week afgelopen maand afgelopen 24 uur). 
   * Aantal query's.
   * Statistische functie.
     
     ![instellingen](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a>Details van de afzonderlijke query's weergeven
details van de query tooview:

1. Klik op een query in de lijst Hallo van top-query's.
   
    ![Meer informatie](./media/sql-database-query-performance/details.png)
2. Hallo detailweergave wordt geopend en aantal Hallo query's CPU-verbruik/duur/uitvoering is onderverdeeld gedurende een bepaalde periode.
3. Klik op rond Hallo-grafiek voor meer informatie.
   
   * Bovenste diagram toont de regel met algemene database DTU % en Hallo balken zijn CPU-percentage verbruikt door Hallo geselecteerde query.
   * Tweede diagram toont de totale duur door Hallo geselecteerde query.
   * Onder diagram toont het aantal uitvoeringen door de geselecteerde query Hallo.
     
     ![Querydetails][3]
4. Optioneel gebruik schuifregelaars, knoppen Inzoomen en uitzoomen of klik op **instellingen** toocustomize hoe querygegevens worden weergegeven of een andere periode toopick.

## <a name="review-top-queries-per-duration"></a>Bekijk meest gebruikte query's per duur
In Hallo recente update van inzicht in queryprestaties, er zijn twee nieuwe metrische gegevens kunt u potentiële knelpunten identificeren geïntroduceerd: aantal duur en uitvoering.<br>

Langlopende query's hebben Hallo grootste kans dat er meer resources vergrendelen, andere gebruikers worden geblokkeerd en schaalbaarheid te beperken. Ze zijn ook Hallo beste kandidaten voor optimalisatie.<br>

tooidentify langlopende query's:

1. Open **aangepaste** tabblad in de Query Performance Insight voor de geselecteerde database
2. Wijzigen van de metrische gegevens toobe **duur**
3. Selecteer het aantal query's en observatie-interval
4. Selecteer de statistische functie
   
   * **Som** tijdens de gehele observatie-interval is de som van alle uitvoeringstijd van de query.
   * **Maximale** vindt u query's welke uitvoeringstijd maximale was op de hele observatie-interval.
   * **Gem.** vindt gemiddelde uitvoeringstijd van alle query uitvoeringen en ziet u boven buiten deze gemiddelden Hallo. 
     
     ![duur van de query][4]

## <a name="review-top-queries-per-execution-count"></a>Bekijk meest gebruikte query's per aantal keer uitgevoerd
Hoog aantal uitvoeringen mogelijk niet beïnvloeden database zelf en gebruik van bronnen kan lage, maar algemene toepassing, haalt traag.

In sommige gevallen, zeer hoge uitvoering aantal tooincrease van het netwerk kan leiden retouren. Retouren aanzienlijk beïnvloeden. Ze zijn onderwerp toonetwork latentie en toodownstream server latentie. 

Bijvoorbeeld: veel gegevensgestuurde websites sterk toegang krijgen tot Hallo-database voor elke aanvraag van gebruiker. Tijdens het groepsgewijze helpt, hello verhoogd kunnen netwerkverkeer en de verwerkingsbelasting op de databaseserver Hallo prestaties nadelig beïnvloeden.  Algemeen advies is tookeep ronde reizen tooan absoluut minimum.

tooidentify uitgevoerd vaak query's ('chatty') query's:

1. Open **aangepaste** tabblad in de Query Performance Insight voor de geselecteerde database
2. Wijzigen van de metrische gegevens toobe **aantal keer uitgevoerd**
3. Selecteer het aantal query's en observatie-interval
   
    ![uitvoering van het aantal query 's][5]

## <a name="understanding-performance-tuning-annotations"></a>Inzicht in prestaties afstemmen aantekeningen
Tijdens het verkennen van de werkbelasting in Query Performance Insight, ziet u mogelijk pictogrammen met verticale lijn boven op het Hallo-grafiek.<br>

Deze pictogrammen zijn aantekeningen; ze hebben betrekking op prestaties beïnvloeden bewerkingen worden uitgevoerd door [SQL Azure Database Advisor](sql-database-advisor.md). Door zwevende aantekening krijgen u algemene informatie over Hallo actie:

![query aantekening][6]

Als u meer tooknow of advisor aanbeveling toepassen, klikt u op Hallo-pictogram. Details van de actie wordt geopend. Als een actieve bevelen kunt u meteen met behulp van opdracht toepassen.

![details van de aantekening query][7]

### <a name="multiple-annotations"></a>Meerdere aantekeningen.
Het is mogelijk dat vanwege zoomniveau, aantekeningen die andere sluiten tooeach ophalen tot één samengevouwen zullen. Hiermee wordt aangegeven door speciale pictogram, erop te klikken wordt geopend nieuwe blade waarin de lijst met aantekeningen gegroepeerd worden weergegeven.
Query's en -prestaties afstemmen acties correleren kunt toobetter inzicht in uw workload. 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a>Hallo Query Store-configuratie voor Query Performance Insight optimaliseren
Tijdens het gebruik van de Query Performance Insight kunnen optreden Hallo Query Store-berichten te volgen:

* 'Query Store is niet goed geconfigureerd op deze database. Klik hier meer toolearn."
* 'Query Store is niet goed geconfigureerd op deze database. Klik hier toochange instellingen." 

Deze berichten worden doorgaans weergegeven wanneer Query Store niet kunnen toocollect nieuwe gegevens. 

Eerste geval gebeurt wanneer Query Store in alleen-lezen status en parameters optimaal zijn ingesteld. U kunt dit oplossen door het vergroten van de Query Store of Query Store uit te schakelen.

![knop qds][8]

Tweede geval gebeurt wanneer de Query Store is uitgeschakeld of de parameters zijn niet optimaal ingesteld. <br>U kunt Hallo bewaren en vastleggen beleid en schakel Query Store wijzigen door het uitvoeren van de onderstaande opdrachten of rechtstreeks vanuit de portal:

![knop qds][9]

### <a name="recommended-retention-and-capture-policy"></a>Aanbevolen bewaren en vastleggen beleid
Er zijn twee soorten bewaarbeleidsregels:

* Grootte gebaseerd - als set tooAUTO deze gegevens automatisch bijna maximale grootte wordt opschonen is bereikt.
* Op basis van de - standaard haaks het too30 dagen, wat betekent dat, als de Query Store wordt tekort aan ruimte, wordt verwijderd query uitvoeren op informatie die ouder zijn dan 30 dagen

Vastleggen van beleid kan worden ingesteld op:

* **Alle** -alle query's worden vastgelegd.
* **Automatische** -incidentele's en query's met verwaarlozen compileren en uitvoering duur worden genegeerd. Drempelwaarden voor de duur voor het aantal, compileren en runtime uitvoeren worden intern bepaald. Dit is de standaardoptie Hallo.
* **Geen** -Query Store stopt u het vastleggen nieuwe query's, maar de runtime-statistieken voor al vastgelegde query's worden nog steeds verzameld.

U wordt aangeraden alle beleidsregels tooAUTO en schone beleid too30 dagen instellen:

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

Verhoog de grootte van de Query Store. Dit kan worden uitgevoerd door de verbindende tooa database- en verlenende volgende query:

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

Deze instellingen zijn toegepast brengt uiteindelijk Query Store verzamelen van de nieuwe query's, maar als u niet dat toowait wilt u Query Store schakelt. 

> [!NOTE]
> Uitvoeren van de volgende query worden alle huidige gegevens in Query Store Hallo verwijderd. 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a>Samenvatting
Inzicht in queryprestaties helpt u begrijpen Hallo impact van uw workload van query's en hoe deze zich verhoudt toodatabase resourceverbruik. Met deze functie wordt u meer informatie over het Hallo-grootste verbruik van query's en eenvoudig hello die toofix identificeren voordat ze een probleem.

## <a name="next-steps"></a>Volgende stappen
Extra aanbevelingen over het verbeteren van Hallo prestaties van uw SQL-database, klikt u op [aanbevelingen](sql-database-advisor.md) op Hallo **Query Performance Insight** blade.

![Performance Advisor](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

