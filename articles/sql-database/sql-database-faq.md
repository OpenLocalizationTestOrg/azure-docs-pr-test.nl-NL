---
title: Veelgestelde vragen over SQL-Database aaaAzure | Microsoft Docs
description: Antwoorden toocommon vragen klanten vragen over cloud-databases en Azure SQL Database, van Microsoft relationele databasebeheersysteem (RDBMS) en -database als een service in de cloud Hallo.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 1da12abc-0646-43ba-b564-e3b049a6487f
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 02/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 04c02f96e6e91cf314221134ee0ef6d24217ef45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-faq"></a>Veelgestelde vragen over SQL Database

## <a name="what-is-hello-current-version-of-sql-database"></a>Wat is de huidige versie van SQL-Database Hallo?
Hallo huidige versie van SQL Database is V12. Versie V11 buiten gebruik gesteld.

## <a name="what-is-hello-sla-for-sql-database"></a>Wat is Hallo SLA voor SQL-Database?
Wordt gegarandeerd minimaal 99,99% Hallo tijd klanten heeft de verbinding tussen hun individuele of elastische Basic, Standard, of Premium Microsoft Azure SQL Database en de Internet-gateway. Zie voor meer informatie [SLA](http://azure.microsoft.com/support/legal/sla/).

## <a name="how-do-i-reset-hello-password-for-hello-server-admin"></a>Hoe stel ik Hallo-wachtwoord voor het Hallo-Serverbeheer
In Hallo [Azure-portal](https://portal.azure.com) klikt u op **SQL-Servers**Hallo server selecteert in Hallo lijst en klik vervolgens op **wachtwoord opnieuw instellen**.

## <a name="how-do-i-manage-databases-and-logins"></a>Hoe kan ik databases en aanmeldingen beheren?
Zie [databases en aanmeldingen beheren](sql-database-manage-logins.md).

## <a name="how-do-i-make-sure-only-authorized-ip-addresses-are-allowed-tooaccess-a-server"></a>Hoe maak ik ervoor dat alleen geautoriseerde IP-adressen toegestaan tooaccess een server?
Zie [procedure: firewall-instellingen configureren op de SQL-Database](sql-database-configure-firewall-settings.md).

## <a name="how-does-hello-usage-of-sql-database-show-up-on-my-bill"></a>Hoe ook Hallo informatie over het gebruik van SQL-Database wordt getoond op mijn factuur?
Facturen SQL-Database op een voorspelbare per uur tarief op basis van zowel de servicelaag Hallo + prestaties niveau voor individuele databases of edtu's per elastische pool. Werkelijke gebruik wordt berekend en pro rato per uur uitgevoerd, zodat uw factuur mogelijk breuken van een uur weer. Als een database voor 12 uur in een maand bestaat, ziet uw factuur u bijvoorbeeld informatie over het gebruik van 0,5 dagen. Bovendien Servicelagen + prestatieniveau en edtu's per groep worden verbroken out in Hallo factuur toomake deze eenvoudiger toosee Hallo aantal databasedagen die u voor elk in één maand gebruikt.

## <a name="what-if-a-single-database-is-active-for-less-than-an-hour-or-uses-a-higher-service-tier-for-less-than-an-hour"></a>Wat gebeurt er als een individuele database minder dan een uur actief is of gebruikmaakt van een hogere servicelaag minder dan een uur?
U wordt gefactureerd voor elk uur die een database bestaat met hello hoogste servicelaag + prestaties niveau die toegepast tijdens dat uur, ongeacht de informatie over het gebruik of of Hallo database minder dan een uur actief was. Als u een individuele database maken en verwijderen van vijf minuten later duidt uw factuur kosten met zich mee voor één database uur. 

Voorbeelden

* Als u een Basic-database maken en vervolgens onmiddellijk tooStandard S1 bijwerken, u in rekening worden gebracht met Hallo Standard-S1-frequentie voor Hallo eerste uur.
* Als u een database van Basic tooPremium 10:00 uur bijwerkt en de upgrade is voltooid om 1:35 uur op Hallo na dag, u in rekening worden gebracht met Hallo Premium frequentie begint bij 1:00 uur 
* Als u een database van Premium tooBasic om 11:00 uur downgraden 2:15 uur is voltooid en Hallo-database wordt in rekening gebracht Hallo Premium snelheid tot en met 3:00 uur, waarna deze wordt in rekening gebracht volgens de tarieven voor Hallo Basic.

## <a name="how-does-elastic-pool-usage-show-up-on-my-bill-and-what-happens-when-i-change-edtus-per-pool"></a>Hoe wordt gebruik elastische groep van toepassingen weergegeven op mijn factuur- en wat gebeurt er wanneer ik wijzigen edtu's per groep?
Elastische pool kosten weergeven van op uw factuur als elastische dtu's (edtu's) in Hallo stappen die wordt weergegeven onder Edtu per pool op [Hallo pagina met prijzen](https://azure.microsoft.com/pricing/details/sql-database/). Er zijn geen kosten per database voor elastische pools. U wordt gefactureerd voor elk uur die een adresgroep bestaat op de hoogste eDTU hello, ongeacht de informatie over het gebruik of of Hallo groep minder dan een uur actief was. 

Voorbeelden

* Als u een Standard elastische pool met 200 edtu's om 11:18 uur maken, vijf databases toohello-toepassingen toevoegen u in rekening worden gebracht 200 edtu's voor de hele uur hello, beginnend om 11: 00 in de rest van de Hallo van Hallo dag.
* Op dag 2, 5:05 uur Database 1 begint verbruikt 50 edtu's en constante via Hallo dag bevat. Databases 2-5 fluctueren tussen 0 en 80 edtu's. Tijdens Hallo dag, kunt u vijf andere databases die verschillende edtu's gedurende de dag Hallo verbruiken toevoegen. Dag 2 is een volledige dag tegen 200 eDTU in rekening gebracht. 
* Op dag 3, 5 uur u toevoegen een andere 15 databases. Databasegebruik neemt toe in de gehele Hallo dag toohello punt waar u tooincrease edtu's voor toepassingen van 200 too400 Hallo 20:05 uur besluit Kosten op Hallo 200 eDTU niveau waren van kracht tot 8 uur en verhoogt de too400 edtu's voor Hallo resterende vier uur. 

## <a name="elastic-pool-billing-and-pricing-information"></a>Elastische pool facturering en prijzen van informatie
Elastische pools worden gefactureerd per Hallo volgende kenmerken:

* Een elastische pool wordt in rekening gebracht bij het maken ervan, zelfs wanneer er geen databases in Hallo van toepassingen zijn.
* Een elastische pool wordt in rekening gebracht per uur. Dit is dezelfde frequentie als prestatieniveaus van individuele databases voor softwarelicentiecontrole Hallo.
* Als een elastische pool formaat is gewijzigd tooa nieuwe aantal edtu's, klikt u vervolgens Hallo van toepassingen wordt niet in rekening gebracht volgens toohello nieuwe hoeveelheid edtu's tot Hallo grootte wijzigen van de bewerking is voltooid. Dit volgt hetzelfde patroon als gewijzigd Hallo prestatieniveau van individuele databases Hallo.
* Hallo prijs van een elastische groep is gebaseerd op het aantal edtu's van de pool Hallo Hallo. Hallo prijs van een elastische groep is onafhankelijk van Hallo getal en het gebruik van de elastische databases binnen het Hallo.
* Prijs wordt berekend door de (aantal groepen met edtu's) x (eenheidsprijs per eDTU).

prijs per eenheid eDTU Hallo voor een elastische groep is hoger dan Hallo eenheidsprijs DTU voor een individuele database in Hallo dezelfde servicelaag. Zie [de prijsinformatie voor SQL Database](https://azure.microsoft.com/pricing/details/sql-database/) voor meer informatie. 

toounderstand hello Edtu's en-service en lagen, Zie [SQL Database-opties en prestaties](sql-database-service-tiers.md).

## <a name="how-does-hello-use-of-active-geo-replication-in-an-elastic-pool-show-up-on-my-bill"></a>Hoe gebruikt Hallo van actieve geo-replicatie in een elastische pool te zien op mijn factuur?
In tegenstelling tot individuele databases, met behulp van [actieve geo-replicatie](sql-database-geo-replication-overview.md) met elastische databases niet direct facturering gevolgen hebben.  U alleen worden in rekening gebracht voor Hallo edtu's dat is ingericht voor elk Hallo pools (groep primaire en secundaire groep)

## <a name="how-does-hello-use-of-hello-auditing-feature-impact-my-bill"></a>Hoe Hallo gebruikt Hallo controle van de impact van de functie mijn factuur?
Controle is ingebouwd in Hallo SQL Database-service zonder extra kosten en is beschikbaar tooBasic, standaard, Premium en Premium RS databases. Echter auditlogboeken toostore hello, Hallo controle van de functie maakt gebruik van een Azure Storage-account en de tarieven voor tabellen en wachtrijen in Azure Storage toepassen op basis van Hallo grootte van het controlelogboek.

## <a name="how-do-i-find-hello-right-service-tier-and-performance-level-for-single-databases-and-elastic-pools"></a>Hoe vind ik Hallo rechts prijscategorie en prestatieniveau serviceniveau voor individuele databases en elastische pools
Er zijn een aantal hulpprogramma's beschikbaar tooyou. 

* Gebruik voor on-premises-databases, Hallo [DTU sizing advisor](http://dtucalculator.azurewebsites.net/) toorecommend Hallo databases en vereist dtu's en om meerdere databases voor elastische pools evalueren.
* Als een individuele database zou als voordeel dat in een pool, raadt intelligent engine van Azure een elastische pool als er een historisch gebruikspatroon dat ontstane. Zie [bewaken en beheren van een elastische groep met hello Azure-portal](sql-database-elastic-pool-manage-portal.md). Zie voor meer informatie over hoe toodo math Hallo zelf [prijs- en Prestatieoverwegingen voor een elastische pool](sql-database-elastic-pool.md)
* toosee of moet u een individuele database toodial omhoog of omlaag, Zie [prestaties richtlijnen voor individuele databases](sql-database-performance-guidance.md).

## <a name="how-often-can-i-change-hello-service-tier-or-performance-level-of-a-single-database"></a>Hoe vaak kan ik Hallo laag of prestaties serviceniveau van één database wijzigen?
U kunt de servicelaag hello (tussen Basic, Standard, Premium en Premium RS) wijzigen of Hallo prestatieniveau binnen een servicetier (bijvoorbeeld S1 tooS2) zo vaak als u wilt. Voor de databases van eerdere versie, kunt u Hallo laag of prestaties serviceniveau een totaal van vier keer in een periode van 24 uur.

## <a name="how-often-can-i-adjust-hello-edtus-per-pool"></a>Hoe vaak kan ik Hallo Edtu per pool aanpassen?
Zo vaak als u wilt.

## <a name="how-long-does-it-take-toochange-hello-service-tier-or-performance-level-of-a-single-database-or-move-a-database-in-and-out-of-an-elastic-pool"></a>Hoe lang slaat deze nemen toochange Hallo laag of prestaties serviceniveau van één database of een database verplaatsen naar en vanuit een elastische groep?
Hallo servicelaag van een database wijzigen en in en uit het verplaatsen van een groep moeten worden Hallo database toobe op Hallo-platform als een achtergrondbewerking is gekopieerd. Veranderende Hallo servicelaag kan van enkele minuten tooseveral uren, afhankelijk van de grootte Hallo Hallo databases opnemen. In beide gevallen blijven Hallo databases online en beschikbaar tijdens Hallo verplaatsen. Zie voor meer informatie over het wijzigen van individuele databases [wijziging Hallo servicelaag van een database](sql-database-service-tiers.md). 

## <a name="when-should-i-use-a-single-database-vs-elastic-databases"></a>Wanneer moet ik een individuele database versus elastische databases gebruiken?
In het algemeen elastische pools zijn ontworpen voor een typische [patroon software as a service (SaaS)-toepassing](sql-database-design-patterns-multi-tenancy-saas-applications.md), waarbij één database per klant of tenant. Aankopen afzonderlijke databases en toomeet Hallo variabele overmatige inrichting en piek eisen voor elke database vaak niet efficiënt kosten is. Met pools u Hallo collectieve prestaties van Hallo van toepassingen beheren en Hallo databases omhoog en omlaag geschaald automatisch. Azure intelligent engine raadt aan om een pool voor databases wanneer een gebruikspatroon ontstane. Zie voor meer informatie [elastische pool richtlijnen](sql-database-elastic-pool.md).

## <a name="what-does-it-mean-toohave-up-too200-of-your-maximum-provisioned-database-storage-for-backup-storage"></a>Wat houdt het toohave too200% van uw databaseopslag maximale ingerichte voor back-upopslag?
Back-upopslag is Hallo opslag die is gekoppeld aan uw geautomatiseerde database back-ups die worden gebruikt voor [Point-In-Time-herstel](sql-database-recovery-using-backups.md#point-in-time-restore) en [geo-restore](sql-database-recovery-using-backups.md#geo-restore). Microsoft Azure SQL Database biedt een too200% van de maximale ingerichte databaseopslag van back-upopslag zonder extra kosten. Bijvoorbeeld, als er een Standard database-exemplaar met een ingerichte DB-grootte van 250 GB, worden u voorzien van 500 GB aan back-upopslag zonder extra kosten. Als uw database groter is dan de opgegeven back-upopslag Hallo, kunt u kiezen tooreduce Hallo bewaarperiode contact opnemen met de ondersteuning van Azure of betalen voor Hallo aanvullende back-up met standard-geografisch redundante opslag met leestoegang (RA-GRS) frequentie in rekening gebracht. Zie voor meer informatie over de facturering RA-GRS prijsinformatie voor opslag.

## <a name="im-moving-from-webbusiness-toohello-new-service-tiers-what-do-i-need-tooknow"></a>Ik ben verplaatsen van Web/Business toohello nieuwe Servicelagen, wat kan ik tooknow nodig?
Azure SQL-Web- en zakelijke databases zijn nu buiten gebruik gesteld. Hallo Basic, Standard, Premium, Premium RS en elastische lagen vervangen Hallo databases voor Web en Business is buiten gebruik stellen. 

## <a name="what-is-an-expected-replication-lag-when-geo-replicating-a-database-between-two-regions-within-hello-same-azure-geography"></a>Wat is er een vertraging van de verwachte replicatie wanneer geo-replicatie een database tussen twee regio's binnen dezelfde hello Azure Geografie?
Er zijn momenteel ondersteunt een RPO van vijf seconden en vertraging van replicatie Hallo is kleiner zijn dan wanneer Hallo geo-secundaire wordt gehost in Azure gekoppelde regio aanbevolen Hallo en op Hallo dezelfde servicelaag.

## <a name="what-is-an-expected-replication-lag-when-geo-secondary-is-created-in-hello-same-region-as-hello-primary-database"></a>Wat is er een vertraging van de verwachte replicatie als secundaire geo-database wordt gemaakt in Hallo dezelfde regio bevinden als de primaire database Hallo?
Op basis van empirische gegevens, is er niet te veel verschil tussen regio intra- en vertraging van replicatie tussen regio wanneer hello die Azure gekoppelde regio aanbevolen wordt gebruikt. 

## <a name="if-there-is-a-network-failure-between-two-regions-how-does-hello-retry-logic-work-when-geo-replication-is-set-up"></a>Als er een netwerkfout tussen twee regio's, hoe Hallo Pogingslogica werkt wanneer geo-replicatie is ingesteld?
Als er een verbinding verbreken, wordt opnieuw geprobeerd elke 10 seconden toore-verbindingen tot stand brengen.

## <a name="what-can-i-do-tooguarantee-that-a-critical-change-on-hello-primary-database-is-replicated"></a>Wat kan ik doen tooguarantee dat een kritieke wijziging in de primaire database hello wordt gerepliceerd?
Hallo geo-secundaire is een replica async en we tookeep niet proberen deze in de volledige synchronisatie met primaire Hallo. Maar we bieden een methode tooforce synchronisatie tooensure Hallo replicatie van wijzigingen in kritieke (bijvoorbeeld bijwerken van wachtwoorden). Geforceerde synchronisatie van invloed op prestaties omdat de aanroepende thread Hallo worden geblokkeerd totdat alle doorgevoerde transacties worden gerepliceerd. Zie voor meer informatie [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx). 

## <a name="what-tools-are-available-toomonitor-hello-replication-lag-between-hello-primary-database-and-geo-secondary"></a>Welke hulpprogramma's zijn beschikbaar toomonitor Hallo vertraging van replicatie tussen de primaire database Hallo en secundaire geo-database?
We tonen vertraging van Hallo realtime replicatie tussen de primaire database Hallo en geo-secundaire via een DMV. Zie voor meer informatie [sys.dm_geo_replication_link_status](https://msdn.microsoft.com/library/mt575504.aspx).

## <a name="toomove-a-database-tooa-different-server-in-hello-same-subscription"></a>een andere database tooa-server in Hallo toomove hetzelfde abonnement
* In Hallo [Azure-portal](https://portal.azure.com), klikt u op **SQL-databases**, selecteert u een database uit Hallo lijst en klik vervolgens op **kopie**. Zie [kopiëren van een Azure SQL database](sql-database-copy.md) voor meer informatie.

## <a name="toomove-a-database-between-subscriptions"></a>een database tussen abonnementen toomove
* In Hallo [Azure-portal](https://portal.azure.com), klikt u op **SQL-servers** en selecteer vervolgens Hallo-server die als host fungeert voor uw database in de lijst Hallo. Klik op **verplaatsen**, en selecteer vervolgens Hallo resources toomove en Hallo abonnement toomove aan.
