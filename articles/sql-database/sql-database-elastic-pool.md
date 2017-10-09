---
title: aaaWhat elastische pools zijn? Meerdere SQL-databases - Azure beheren | Microsoft Docs
description: "Beheren en schalen van meerdere SQL-databases - honderden en duizendtallen - met elastische pools. Één prijs voor resources die u distribueren kunt waar nodig."
keywords: meerdere databases, databaseresources en prestaties van de database
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: b46e7fdc-2238-4b3b-a944-8ab36c5bdb8e
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 07/31/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 2098d7817ebe1277b5c131421f23c00803ec78f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-pools-help-you-manage-and-scale-multiple-sql-databases"></a>Elastische pools helpen u te beheren en schalen van meerdere SQL-databases

SQL-Database elastische pools zijn een eenvoudige, rendabele oplossing voor het beheren en schalen van meerdere databases die voldoen aan verschillende en onvoorspelbare veeleisende hebben. Hallo-databases in een elastische pool op één Azure SQL Database-server en een aantal bronnen delen ([elastische Database Transaction Units](sql-database-what-is-a-dtu.md) (Edtu)) op een vaste prijs. Elastische pools in Azure SQL Database inschakelen SaaS ontwikkelaars toooptimize Hallo prijs prestaties voor een groep met databases binnen het budget voorgeschreven elasticiteit voor elke database prestaties leveren.   

> [!NOTE]
> Elastische pools zijn algemeen beschikbaar in alle Azure-regio's, behalve in West-India, waar deze zich momenteel in de previewfase bevinden.  Algemene beschikbaarheid van elastische pools in deze regio zal zo snel mogelijk plaatsvinden.
>

## <a name="what-are-sql-elastic-pools"></a>Wat zijn de elastische pools SQL? 

SaaS-ontwikkelaars ontwikkelen toepassingen boven op grootschalige gegevenslagen die uit meerdere databases bestaan. Een algemene toepassing patroon is tooprovision een individuele database voor elke klant. Maar verschillende klanten hebben vaak verschillende en onvoorspelbare gebruikspatronen en moeilijk toopredict Hallo resourcevereisten van elke gebruiker één database is. Traditioneel moest u twee opties: 

- Te veel bronnen op basis van piekgebruik en via salaris, ter beschikking stellen of
- Onder inrichten toosave kosten op Hallo kosten van de prestaties en klanttevredenheid tijdens pieken. 

Elastische pools oplossen dit probleem door ervoor te zorgen dat databases Hallo prestaties bronnen die zij nodig hebben krijgt wanneer ze deze nodig hebben. Ze bieden een eenvoudig mechanisme voor het toewijzen van resources binnen een voorspelbaar budget. Zie toolearn meer informatie over ontwerppatronen voor SaaS-toepassingen met elastische pools [ontwerppatronen voor multitenant SaaS-toepassingen met Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Elastic-databases-helps-SaaS-developers-tame-explosive-growth/player]
>

Elastische pools inschakelen Hallo developer toopurchase [elastische Database Transaction Units](sql-database-what-is-a-dtu.md) (edtu's) voor een groep die wordt gedeeld door meerdere databases tooaccommodate onvoorspelbare perioden van geheugengebruik door afzonderlijke databases. Hallo eDTU vereiste voor een pool wordt bepaald door de cumulatieve Hallo-gebruik van de databases. het aantal edtu's beschikbaar toohello groep Hallo wordt bepaald door Hallo developer budget. Hallo developer gewoon databases toohello pool wordt toegevoegd, stelt Hallo minimum en maximum aantal edtu's voor databases Hallo en Hallo eDTU van Hallo-groep op basis van hun budget wordt ingesteld. Een ontwikkelaar met behulp van groepen tooseamlessly groeien hun service van een lean opstarten tooa volwassen bedrijf op een steeds groter wordende schaal.

In de pool hello krijgen afzonderlijke databases Hallo flexibiliteit tooauto-scale binnen de ingestelde parameters. Een database kan meer edtu's toomeet vraag gebruiken onder een zware belasting. Databases verbruiken minder bij lichte belasting en verbruiken geen eDTU's als er geen belasting is. Resources voor de hele pool Hallo in plaats van voor individuele databases inrichting vereenvoudigt uw beheertaken. Bovendien hebt u een voorspelbare budget voor Hallo van toepassingen. Aanvullende edtu's tooan bestaande toepassingen zonder uitvaltijd voor de database kunnen worden toegevoegd, behalve dat Hallo databases wellicht toobe verplaatst tooprovide Hallo extra bronnen berekenen voor Hallo nieuwe eDTU-reservering. En als de extra eDTU's niet meer nodig zijn, kunnen ze op elk moment uit een bestaande pool worden verwijderd. En u kunt toevoegen of databases toohello groep afgetrokken. Als een database naar verwachting minder resources nodig heeft, kunt u deze verwijderen.

U kunt maken en beheren van een elastische pool met Hallo [Azure-portal](sql-database-elastic-pool-manage-portal.md), [PowerShell](sql-database-elastic-pool-manage-powershell.md), [Transact-SQL](sql-database-elastic-pool-manage-tsql.md), [C#](sql-database-elastic-pool-manage-csharp.md), en Hallo REST-API. 

## <a name="when-should-you-consider-a-sql-database-elastic-pool"></a>Wanneer moet u rekening houden met een elastische pool in SQL-Database?

Pools zijn geschikt voor een groot aantal databases met specifieke gebruikspatronen. Voor een bepaalde database wordt dit patroon gekenmerkt door een laag gemiddeld gebruik met relatief incidentele gebruikspieken.

Hallo meer databases kunt u toevoegen tooa groep Hallo groter geworden van uw besparing. Afhankelijk van uw toepassing gebruik patroon is het mogelijk toosee besparingen met slechts twee S3-databases.  

Hallo volgende secties u laten zien hoe tooassess als uw specifieke verzameling van databases profiteren kunt van wordt in een pool. Hallo voorbeelden Standard pools gebruiken maar hello dezelfde principes ook toepassen tooBasic en Premium-adresgroepen.

### <a name="assessing-database-utilization-patterns"></a>Databasegebruikspatronen beoordelen

Hallo toont volgende afbeelding een voorbeeld van een database die veel niet-actieve tijd nodig heeft, maar ook periodiek bereikt met de activiteit. Dit is een gebruikspatroon dat geschikt is voor een groep:

   ![een individuele database die geschikt is voor een groep](./media/sql-database-elastic-pool/one-database.png)

Voor Hallo periode van vijf minuten worden weergegeven, DB1 pieken up too90 dtu's, maar het gebruik ervan totale gemiddelde is minder dan 5 dtu's. Een prestatieniveau S3 vereist toorun deze workload in één database, maar dit laat de meeste bronnen Hallo ongebruikte tijdens perioden met weinig activiteit.

Een groep kan deze ongebruikte dtu's toobe gedeeld door meerdere databases en Hallo dtu's nodig hebt en de algehele kosten vermindert.

Voortbouwend op het vorige voorbeeld hello, Stel dat er extra databases met vergelijkbare gebruikspatronen als DB1 zijn. Hallo-gebruik van vier databases in Hallo volgende twee onderstaande afbeeldingen, en 20 databases zijn gelaagd op Hallo grafiek dezelfde tooillustrate Hallo niet-overlappende aard van het-gebruik gedurende een bepaalde periode:

   ![vier databases met een gebruikspatroon dat geschikt is voor een groep](./media/sql-database-elastic-pool/four-databases.png)

  ![twintig databases met een gebruikspatroon dat geschikt is voor een groep](./media/sql-database-elastic-pool/twenty-databases.png)

Hallo cumulatieve DTU-gebruik voor alle 20 databases wordt door Hallo zwarte lijn in Hallo voorgaande afbeelding weergegeven. Dit betekent dat Hallo cumulatieve DTU-gebruik nooit meer dan 100 dtu's en geeft aan dat 20 databases Hallo 100 edtu's gedurende deze periode kunnen delen. Dit resulteert in 20 x verminderde dtu's en een 13 x prijs vermindering vergeleken tooplacing elk van de databases Hallo in S3 prestatieniveaus van individuele databases.

In dit voorbeeld is ideaal voor Hallo volgende redenen:

* Er zijn grote verschillen tussen piekgebruik en gemiddeld gebruik per database.  
* Hallo piek-gebruik voor elke database doet zich op verschillende tijdstippen in de tijd.
* eDTU‘s worden gedeeld tussen meerdere databases.

Hallo prijs van een groep is een functie van Hallo groepen met edtu's. Tijdens het Hallo eDTU prijs per eenheid voor een pool is 1,5 x groter is dan Hallo DTU prijs per eenheid voor een individuele database **groepen met edtu's kan worden gedeeld door veel databases en minder totaal aantal edtu's nodig**. Deze verschillen in de prijzen en eDTU zijn Hallo basis van Hallo prijs besparingen kans dat pools kunnen bieden.  

Hallo volgende regels van miniatuur gerelateerd toodatabase aantal en de database gebruik help tooensure die zorgt voor een pool lagere kosten vergeleken toousing prestatieniveaus voor individuele databases.

### <a name="minimum-number-of-databases"></a>Minimum aantal databases

Als de som Hallo Hallo dtu's prestatieniveaus voor individuele databases meer dan 1,5 x Hallo edtu's die nodig zijn voor Hallo van toepassingen is, zijn een elastische groep is rendabeler. Zie [eDTU- en opslaglimieten voor elastische pools en elastische databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) voor beschikbare grootten.

***Voorbeeld***<br>
Ten minste twee S3 databases of ten minste 15 S0 databases nodig zijn voor een groep 100 eDTU toobe kosteneffectiever zijn dan het gebruik van prestatieniveaus voor individuele databases.

### <a name="maximum-number-of-concurrently-peaking-databases"></a>Maximum aantal gelijktijdig piekende databases

Edtu's dat wordt gedeeld, gebruik niet alle databases in een groep tegelijk edtu's van toohello maximaal beschikbare wanneer prestatieniveaus voor individuele databases. Hallo minder databases die gelijktijdig pieksnelheden, Hallo lagere Hallo groeps-eDTU te kan worden ingesteld en Hallo die meer rendabele Hallo van toepassingen wordt. In het algemeen beperken niet meer dan 2/3 (of 67%) van de Hallo-databases op Hallo van toepassingen moeten tegelijkertijd pieksnelheden tootheir eDTU.

***Voorbeeld***<br>
tooreduce kosten voor drie S3-databases in een 200 eDTU-pool, maximaal twee van deze databases pieksnelheden kunnen gelijktijdig in het gebruik. Als meer dan twee van deze vier S3 databases tegelijk pieksnelheden zou Hallo groep anders toobe grootte toomore dan 200 edtu's hebben. Als Hallo van toepassingen is formaat is gewijzigd toomore dan 200 edtu's, meer S3-databases moet toobe toegevoegd toohello groep tookeep kosten lager is dan prestatieniveaus van individuele databases.

Houd er rekening mee dat in dit voorbeeld houdt geen rekening met gebruik van andere databases in Hallo-groep. Als alle databases sommige gebruik op een willekeurig moment in de tijd hebt, vervolgens kleiner zijn dan 2/3 (of 67%) van Hallo databases kunnen pieksnelheden tegelijkertijd.

### <a name="dtu-utilization-per-database"></a>DTU-gebruik per database
Een grote verschil tussen Hallo piek en het gemiddelde gebruik van een database geeft aan langdurig van laag gebruik en korte perioden van hoge capaciteit. Dit gebruikspatroon is ideaal voor het delen van resources met meerdere databases. Een database zou een geschikte kandidaat voor een groep kunnen zijn als het piekgebruik ongeveer 1,5 keer groter is dan het gemiddelde gebruik.

***Voorbeeld***<br>
Een S3-database die waar de pieken too100 dtu's en Gemiddeld gebruikt 67 dtu's of kleiner is een goede kandidaat voor het delen van edtu's in een pool. U kunt ook een database S1 die waar de pieken too20 dtu's en Gemiddeld gebruikt 13 dtu's of kleiner is een goede kandidaat voor een groep.

## <a name="how-do-i-choose-hello-correct-pool-size"></a>Hoe kies ik de juiste groepsgrootte Hallo?

Hallo beste grootte voor een groep is afhankelijk van Hallo cumulatieve edtu's en storage-resources die nodig zijn voor alle databases in Hallo-groep. Hiervoor moet groter zijn van de volgende Hallo Hallo bepalen:

* Maximale aantal dtu's worden gebruikt door alle databases in Hallo van toepassingen.
* Maximale opslag bytes die door alle databases in de groep hello worden gebruikt.

Zie [eDTU- en opslaglimieten voor elastische pools en elastische databases](#what-are-the-resource-limits-for-elastic-pools) voor beschikbare grootten.

SQL-Database wordt automatisch evalueert Hallo historische brongebruik van de databases op een bestaande SQL-databaseserver en raadt Hallo geschikte groep configuratie in hello Azure-portal. In de toevoeging toohello aanbevelingen, een ingebouwde ervaring maakt een schatting Hallo eDTU-gebruik voor een aangepaste groep van databases op Hallo-server. Hiermee kunt u een 'wat als'-analyse toodo door interactief databases toohello toepassingen toevoegen en verwijderen van tooget resource gebruiksanalyse en advies sizing voordat u uw wijzigingen doorvoert. Zie [Monitor, manage, and size an elastic pool](sql-database-elastic-pool-manage-portal.md) (Een elastische groep bewaken, beheren en van formaat wijzigen) voor instructies.

In gevallen waarin u tooling niet gebruiken, kunt Hallo volgende stapsgewijze u schatten of een groep kosteneffectiever zijn dan de individuele databases is:

1. Schat Hallo edtu's die nodig zijn voor Hallo van toepassingen als volgt:

   MAX(<*Totaal aantal DB's* X *gemiddelde DTU-gebruik per DB*>,<br>
   <*aantal gelijktijdig piekende databases* X *piek-DTU-gebruik per DB*)
2. Schat Hallo opslagruimte die nodig zijn voor Hallo groep door het aantal bytes dat nodig is voor alle Hallo-databases in de groep Hallo Hallo toe te voegen. Hallo eDTU-groepsgrootte waarmee deze hoeveelheid opslag vervolgens bepalen. Zie [eDTU- en opslaglimieten voor elastische pools en elastische databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) voor poolopslaglimieten op basis van de eDTU-poolomvang.
3. Hallo groter Hallo eDTU schattingen nemen uit stap 1 en stap 2.
4. Zie Hallo [pagina met prijzen SQL-Database](https://azure.microsoft.com/pricing/details/sql-database/) en zoeken naar de kleinste eDTU-pool Hallo grootte die groter is dan Hallo schatting vanaf stap 3.
5. Vergelijk Hallo groep prijs uit stap 5 toohello prijs van het gebruik van de juiste prestatieniveaus Hallo voor individuele databases.

### <a name="changing-elastic-pool-resources"></a>Het wijzigen van de resources van elastische groep

U kunt vergroten of verkleinen Hallo resources beschikbaar tooan elastische pool op basis van de resource nodig heeft.

* Hallo min edtu's per database of max edtu's per database doorgaans wijzigen is voltooid in de 5 minuten of minder.
* Hallo edtu's per groep wijzigen hangt af van de totale hoeveelheid ruimte die wordt gebruikt door alle databases in de groep Hallo Hallo. Wijzigingen duren gemiddeld 90 minuten of minder per 100 GB. Bijvoorbeeld, als de totale ruimte hello worden gebruikt door alle databases in de groep Hallo is 200 GB en vervolgens Hallo verwachte latentie voor het wijzigen van Hallo groeps-eDTU per pool is drie uur of minder.

## <a name="what-are-hello-resource-limits-for-elastic-pools"></a>Wat zijn de limieten voor elastische pools Hallo?

Hallo volgende tabellen beschrijven Hallo limieten van elastische pools.  Houd er rekening mee Hallo limieten van de afzonderlijke databases in een elastische pools zijn meestal hetzelfde als die voor individuele databases buiten groepen op basis van dtu's en de servicelaag Hallo Hallo.  Hallo maximumaantal gelijktijdige werknemers voor een database S2 is bijvoorbeeld 120 werknemers.  Hallo maximumaantal gelijktijdige werknemers voor een database in een Standard-pool is dus ook 120 werknemers als Hallo max. DTU per database in de groep Hallo is 50 dtu's (dit is gelijkwaardig tooS2).

[!INCLUDE [SQL DB service tiers table for elastic pools](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Als alle dtu's van een elastische pool worden gebruikt, krijgt elke database in de groep Hallo dezelfde hoeveelheid resources tooprocess query's.  Hallo SQL Database-service biedt billijkheid tussen databases door ervoor te zorgen gelijk stukken tijd compute delen van resources. Elastische pool resource delen billijkheid is bovendien tooany hoeveelheid resource tooeach database anders gegarandeerd wanneer Hallo minimale aantal DTU's per database tooa andere waarde dan nul is ingesteld.

### <a name="database-properties-for-pooled-databases"></a>Database-eigenschappen voor gegroepeerde databases

Hallo volgende tabel beschrijft Hallo-eigenschappen voor gegroepeerde databases.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Maximaal aantal eDTU’s per database |Hallo maximale aantal edtu's die van een database in de groep hello, gebruikmaken mogelijk als beschikbaar is op basis van gebruik door andere databases in de groep Hallo.  Het maximum aantal eDTU's per database is geen resourcegarantie voor een database.  Deze instelling is een algemene instelling die van toepassing tooall databases in Hallo-groep is. Stel max edtu's per database hoog genoeg toohandle pieken in database-gebruik. Een zekere mate van hostgroepcapaciteit wordt verwacht omdat Hallo van toepassingen in het algemeen wordt ervan uitgegaan dat warme en koude gebruikspatronen voor databases waarin alle databases zijn niet tegelijkertijd tot een piek. Stel bijvoorbeeld dat Hallo piek-gebruik per database is 20 edtu's en slechts 20% van 100 Hallo-databases in de groep Hallo piek bij Hallo hetzelfde moment.  Als Hallo eDTU max per database is ingesteld too20 edtu's, is redelijke tooovercommit Hallo van toepassingen op 5 maal en set Hallo Edtu per pool too400. |
| Minimaal aantal eDTU’s per database |minimum aantal edtu's dat een database in de groep Hallo Hallo kan worden gegarandeerd.  Deze instelling is een algemene instelling die van toepassing tooall databases in Hallo-groep is. Hallo min eDTU per database kan worden ingesteld als too0 en is ook Hallo-standaardwaarde. Deze eigenschap is ingesteld tooanywhere tussen 0 en Hallo gemiddeld eDTU-gebruik per database. Hallo product van Hallo aantal databases in Hallo van toepassingen en Hallo min edtu's per database kan niet groter zijn dan Hallo edtu's per groep.  Bijvoorbeeld, als een groep 20 databases is en Hallo eDTU-minimum per database too10 edtu's instellen, moet vervolgens Hallo edtu's per opslaggroep ten minste even groot zijn als 200 edtu's. |
| Maximale gegevensopslag per database |Hallo maximale opslag voor een database in een pool. Gegroepeerde databases delen opslag, toepassingen, zodat de database-opslag is beperkt toohello kleinere van resterende hoeveelheid poolopslag en maximale opslag per database. Maximale opslag per database verwijst toohello maximale grootte van de gegevensbestanden Hallo en omvat geen Hallo ruimte die wordt gebruikt door logboekbestanden. |
|||

## <a name="using-other-sql-database-features-with-elastic-pools"></a>Gebruik van andere functies van de SQL-Database met elastische pools

### <a name="elastic-jobs-and-elastic-pools"></a>Elastische taken en elastische pools

Met een groep worden beheertaken vereenvoudigd door scripts in **[elastische taken](sql-database-elastic-jobs-overview.md)** uit te voeren. Een elastische taak elimineert de meeste saaie handelingen die komen kijken bij grote aantallen databases. toobegin, Zie [aan de slag met elastische taken](sql-database-elastic-jobs-getting-started.md).

Zie [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md) (Uitbreiden met Azure SQL Database) voor meer informatie over andere databasehulpprogramma's voor het werken met meerdere databases.

### <a name="business-continuity-options-for-databases-in-an-elastic-pool"></a>Opties voor bedrijfscontinuïteit voor databases in een elastische pool
Gegroepeerde databases in het algemeen ondersteuning Hallo dezelfde [zakelijke continuïteit functies](sql-database-business-continuity.md) die beschikbaar toosingle databases zijn.

- **Verwijzen naar een bepaald tijstip**: punt in tijd terugzetten maakt gebruik van automatische databaseback-ups toorecover een database in een pool tooa bepaald punt in tijd. Zie [Herstel naar een bepaald tijdstip](sql-database-recovery-using-backups.md#point-in-time-restore)

- **Geo-restore**: Geo-herstel biedt Hallo standaardhersteloptie wanneer een database is niet beschikbaar vanwege een incident in Hallo regio waar Hallo-database wordt gehost. Zie [herstellen van een Azure SQL Database of failover tooa secundaire](sql-database-disaster-recovery.md)

- **Actieve geo-replicatie**: configureren voor toepassingen met agressievere herstelvereisten dan geo-herstel te kan bieden, [actieve geo-replicatie](sql-database-geo-replication-overview.md).

## <a name="manage-sql-database-elastic-pools-using-hello-azure-portal"></a>Elastische SQL-Database-groepen met behulp van hello Azure-portal beheren

### <a name="creating-a-new-sql-database-elastic-pool-using-hello-azure-portal"></a>Maken van een nieuwe SQL-Database elastische pool met hello Azure-portal

Er zijn twee manieren die kunt u een elastische pool in hello Azure-portal. U kunt dit doen vanaf het begin als u Hallo groep instellingen u wilt weet, of met een aanbeveling van Hallo-service. SQL-Database beschikt over ingebouwde intelligentie die raadt aan om een elastische groep is ingesteld als het kostenefficiënte op basis van Hallo voorbij gebruik telemetrie van uw databases. 

Een elastische pool te maken van een bestaand **server** blade in de portal Hallo Hallo gemakkelijkste manier toomove bestaande databases in een elastische groep is. U kunt ook een elastische pool maken door te zoeken naar **elastische SQL-groep** in Hallo **Marketplace** of klikken op **+ toevoegen** in Hallo **SQL elastische pools**blade bladeren. U zijn kunt toospecify een nieuwe of bestaande server via deze werkstroom van toepassingen.

> [!NOTE]
> U kunt meerdere groepen maken op een server, maar u kunt geen databases van verschillende servers toevoegen in Hallo dezelfde groep.
>  

Hallo bepaalt prijscategorie van pool Hallo functies beschikbaar toohello elastics in Hallo pool en Hallo maximumaantal edtu's (eDTU MAX) en opslag (GB) beschikbare tooeach database. Zie voor meer informatie [Servicelagen](#edtu-and-storage-limits-for-elastic-pools).

toochange hello prijscategorie voor Hallo-groep, klikt u op **prijscategorie**, klikt u op de prijscategorie die u wilt en klik vervolgens op Hallo **Selecteer**.

> [!IMPORTANT]
> Nadat u Hallo prijscategorie kiezen en uw wijzigingen door te klikken op **OK** in de laatste stap hello, niet meer kunnen toochange Hallo prijscategorie van Hallo van toepassingen. toochange Hallo prijscategorie voor een bestaande elastische pool, een elastische pool maken in de gewenste prijscategorie Hallo en Hallo databases toothis nieuwe toepassingen te migreren.
>

Hallo-databases waarmee u samenwerkt hebt voldoende gebruikstelemetrie, Hallo **geschat eDTU- en GB-gebruik** grafiek en Hallo **werkelijk eDTU-gebruik** staafdiagram update toohelp maken van configuratie beslissingen te nemen. Bovendien Hallo-service kan bieden u een aanbeveling bericht toohelp u het juiste formaat Hallo van toepassingen.

Hallo SQL Database-service beoordeelt de gebruiksgeschiedenis en beveelt een of meer groepen wanneer deze kosteneffectiever zijn dan het gebruik van individuele databases. Elke aanbeveling wordt geconfigureerd met een unieke subset van Hallo-server-databases die het meest Hallo van toepassingen geschikt.

![aanbevolen groep](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

Hallo groep aanbeveling omvat:

- Een prijscategorie voor Hallo pool (Basic, Standard, Premium of RS Premium)
- De juiste **eDTU’s voor de groep** (ook wel Max eDTU's per groep)
- Hallo **eDTU MAX** en **eDTU Min** per database
- Hallo-lijst met aanbevolen databases voor Hallo van toepassingen

> [!IMPORTANT]
> Hallo service wordt rekening gehouden Hallo afgelopen 30 dagen telemetrie bij het aanbevelen van pools. Voor een database toobe beschouwd als kandidaat voor een elastische pool, moet er ten minste 7 dagen bestaan. Databases die zich al in een elastische pool bevinden, worden niet aanbevolen voor een elastische pool.
>

Hallo service beoordeelt resourcebehoeften en kosteneffectiviteit zwevend Hallo één databases in elke servicelaag naar pools van Hallo dezelfde laag. Alle Standard databases op een server worden bijvoorbeeld beoordeeld op hoe ze in een Standard elastische groep passen. Dit betekent dat het Hallo-service maakt geen cross-aanbevelingen zoals het verplaatsen van een Standard database naar een Premium pool.

Na het toevoegen van databases toohello groep worden aanbevelingen dynamisch gegenereerd op basis van historisch gebruik Hallo Hallo-databases die u hebt geselecteerd. Deze aanbevelingen worden weergegeven in Hallo eDTU- en GB-gebruiksgrafiek en in een banner boven Hallo Hallo **pool configureren** blade. Deze aanbevelingen zijn bedoeld tooassist u bij het maken van een elastische pool geoptimaliseerd voor uw specifieke databases.

![dynamische aanbevelingen](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

### <a name="manage-and-monitor-an-elastic-pool"></a>Beheren en controleren van een elastische pool

In hello Azure-portal, kunt u gebruik van een elastische pool en het Hallo-databases binnen die groep Hallo bewaken. U kunt ook een aantal wijzigingen tooyour elastische pool en dienen alle wijzigingen op Hallo dezelfde tijd. Deze wijzigingen omvatten toevoegen of verwijderen van databases, elastische pool-instellingen wijzigen of database-instellingen wijzigen.

Hallo volgende afbeelding toont een voorbeeld van de elastische groep. Hallo-weergave bevat:

*  De grafieken voor het brongebruik van Hallo elastische pool en Hallo-databases die zijn opgenomen in de groep Hallo.
*  Hallo **configureren** groep knop toomake toohello elastische pool wordt gewijzigd.
*  Hallo **database maken** knop waarmee een database wordt gemaakt en de huidige elastische pool toohello toegevoegd.
*  Groot aantal databases beheren elastische taken die u helpen door te voeren van Transact-SQL-scripts op alle databases in een lijst.

![Toepassingen weergeven](./media/sql-database-elastic-pool-manage-portal/basic.png)

Het Resourcegebruik, kunt u tooa bepaalde toepassingen toosee gaan. Hallo-groep is standaard geconfigureerde tooshow opslag en het eDTU-gebruik voor Hallo afgelopen uur. Hallo-grafiek kunt geconfigureerde tooshow andere metrische gegevens worden via verschillende tijdvensters. Klik op Hallo **Resourcegebruik** grafiek onder **elastische pool bewaking** tooshow een gedetailleerde weergave van Hallo opgegeven metrische gegevens via het opgegeven tijdvenster Hallo.

![Bewaking van de elastische groep](./media/sql-database-elastic-pool-manage-portal/basic-2.png)

![Blade met metrische gegevens](./media/sql-database-elastic-pool-manage-portal/metric.png)

### <a name="toocustomize-hello-chart-display"></a>grafiekweergave van toocustomize Hallo

U kunt Hallo grafiek en Hallo metrische blade toodisplay bewerken andere metrische gegevens zoals CPU-percentage, gegevens-IO-percentage en log-IO-percentage gebruikt.

![Klik op bewerken](./media/sql-database-elastic-pool-manage-portal/edit-metric.png)

Op Hallo **grafiek bewerken** formulier, selecteert u een tijdsbereik (voorbij vandaag de dag, uur of afgelopen week) of klik op **aangepaste** tooselect een datumbereik in Hallo afgelopen twee weken. U kunt kiezen tussen een staaf- of een lijndiagram en selecteer vervolgens Hallo resources toomonitor.

> [!Note]
> Alleen metrische gegevens met dezelfde eenheid kan worden weergegeven in Hallo Hallo grafiek op Hallo dezelfde tijd. Bijvoorbeeld, als u 'eDTU percentage' selecteert kunt vervolgens u alleen selecteren andere metrische gegevens met percentage als eenheid Hallo.
>

[Klik op bewerken](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

### <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Beheren en controleren van de databases in een elastische pool

Afzonderlijke databases kunnen ook worden gecontroleerd voor potentiële problemen. Onder **elastische Database bewaken**, er is een diagram waarin metrische gegevens voor vijf databases. Standaard Hallo diagram toont Hallo bovenste 5 databases in de groep Hallo door gemiddeld eDTU-gebruik in Hallo afgelopen uur. 

![Bewaking van de elastische groep](./media/sql-database-elastic-pool-manage-portal/basic-3.png)

Klik op Hallo **eDTU-gebruik voor de databases voor het afgelopen uur Hallo** onder **elastische database bewaken**. Hiermee opent u **Database Resourcegebruik** en biedt een gedetailleerde weergave van het Databasegebruik Hallo in Hallo van toepassingen. Hallo raster Hallo onder in de blade Hallo gebruikt, kunt u geen databases in Hallo groep toodisplay het gebruik ervan in de grafiek hello (omhoog too5 databases). U kunt ook aanpassen Hallo metrische gegevens en het tijdstip venster wordt weergegeven in de grafiek Hallo door te klikken op **grafiek bewerken**.

![Gebruik van de databaseblade resource](./media/sql-database-elastic-pool-manage-portal/db-utilization.png)

### <a name="toocustomize-hello-view"></a>toocustomize hello weergeven

Hallo grafiek tooselect een tijdsbereik (voorbij uur of afgelopen 24 uur) bewerken of klik op **aangepaste** tooselect een andere dag in Hallo voorbij toodisplay 2 weken.

![Klik op de grafiek bewerken](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

![Klik op aangepast](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

U kunt ook klikken op Hallo **vergelijken databases door** dropdown tooselect verschillende metrische toouse bij het vergelijken van databases.

![Hallo grafiek bewerken](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect databases toomonitor

In de lijst met de Hallo database in Hallo **Database Resourcegebruik** blade kunt u bepaalde databases vinden door te zoeken door Hallo pagina's in de lijst Hallo of door in het Hallo-naam van een database te typen. Hallo selectievakje tooselect Hallo database gebruiken.

![Zoeken naar databases toomonitor](./media/sql-database-elastic-pool-manage-portal/select-dbs.png)


### <a name="add-an-alert-tooan-elastic-pool-resource"></a>Een elastische pool waarschuwing tooan resource toevoegen

Regels tooan elastische groep die e-mail verzenden toopeople of waarschuwing tekenreeksen tooURL eindpunten wanneer Hallo elastische pool treffers een drempelwaarde voor overbenutting die u hebt ingesteld, kunt u toevoegen.

**een waarschuwing tooany resource tooadd:**

1. Klik op Hallo **Resourcegebruik** grafiek tooopen Hallo **metriek** blade klikt u op **waarschuwing toevoegen**, en vult u de informatie in Hallo Hallo **een waarschuwing toevoegen regel** blade (**Resource** automatisch ingesteld toobe Hallo toepassingen waarmee u werkt).
2. Typ een **naam** en **beschrijving** die Hallo waarschuwing tooyou en Hallo ontvangers identificeert.
3. Kies een **metriek** dat u wilt dat tooalert uit Hallo-lijst.

    Hallo diagram toont dynamisch Resourcegebruik voor die metrische toohelp die u kiest een drempelwaarde.

4. Kies een **voorwaarde** (groter dan maximaal, enzovoort) en een **drempelwaarde**.
5. Kies een **periode** hoelang Hallo metriek regel moet worden voldaan voordat de waarschuwing Hallo-triggers.
6. Klik op **OK**.

Zie voor meer informatie [waarschuwingen van de SQL-Database maken in Azure portal](sql-database-insights-alerts-portal.md).

### <a name="move-a-database-into-an-elastic-pool"></a>Een database verplaatsen naar een elastische pool

U kunt toevoegen of verwijderen van databases uit een bestaande groep. Hallo-databases kunnen zich in andere toepassingen. U kunt echter alleen toevoegen databases die zijn op Hallo dezelfde logische server.

 ![Klik op pool configureren](./media/sql-database-elastic-pool-manage-portal/configure-pool.png)

![Klik op toevoegen toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)

![Selecteer de databases tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

![In behandeling pool-toevoegingen](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

![Op Opslaan klikken](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="move-a-database-out-of-an-elastic-pool"></a>Een database verplaatst buiten een elastische pool

![databases weergeven](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

![databases weergeven](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

![voorbeeld database toevoegen en verwijderen](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

![Op Opslaan klikken](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="change-performance-settings-of-an-elastic-pool"></a>Instellingen van de prestaties van een elastische groep wijzigen

Tijdens het controleren van Resourcegebruik Hallo van een pool voor elastische ontdekt u dat bepaalde aanpassingen nodig zijn. Hallo-groep moet mogelijk een wijziging in Hallo prestaties of de opslag limieten. Mogelijk wilt u toochange Hallo database-instellingen in Hallo van toepassingen. U kunt setup Hallo van Hallo van toepassingen die op elk moment tooget Hallo beste balans van prestaties en kosten wijzigen. Zie [wanneer moet een elastische pool worden gebruikt?](sql-database-elastic-pool.md) voor meer informatie.

toochange hello edtu's of opslag limieten per groep van toepassingen en edtu's per database:

![Resourcegebruik van de elastische groep](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

![Bijwerken van een elastische pool en nieuwe maandelijkse kosten](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="manage-sql-database-elastic-pools-using-powershell"></a>Elastische SQL-Database-groepen met behulp van PowerShell beheren

toocreate en elastische pools van de SQL-Database met Azure PowerShell beheren, gebruikt u Hallo volgende PowerShell-cmdlets. Als u tooinstall moet of een upgrade van PowerShell, raadpleegt u [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps). toocreate en beheren van databases, servers en firewallregels, Zie [maken en beheren van Azure SQL Database-servers en -databases met behulp van PowerShell](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-powershell). 

> [!TIP]
> Zie voor PowerShell-voorbeeldscripts, [maken van elastische pools en databases verplaatsen tussen groepen en van een groep met behulp van PowerShell](scripts/sql-database-move-database-between-pools-powershell.md) en [Gebruik PowerShell toomonitor en schaal een elastische SQL-groep in Azure SQL Database](scripts/sql-database-monitor-and-scale-pool-powershell.md).
>

| Cmdlet | Beschrijving |
| --- | --- |
|[Nieuwe AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool)|Een pool voor elastische database maakt op een logische SQL-server.|
|[Get-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/get-azurermsqlelasticpool)|Elastische pools en hun eigenschapswaarden op een logische SQL-server opgehaald.|
|[Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)|Hiermee wijzigt u de eigenschappen van een pool voor elastische database op een logische SQL-server.|
|[Remove-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/remove-azurermsqlelasticpool)|Hiermee verwijdert u een pool voor elastische database op een logische SQL-server.|
|[Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity)|Hallo-status van bewerkingen in een elastische pool op een logische SQL-server opgehaald.|
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Maakt een nieuwe database in een bestaande pool of als een individuele database. |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Hiermee haalt u een of meer databases.|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Stelt eigenschappen van een database of een bestaande database verplaatst naar buiten of tussen elastische pools.|
|[Verwijder AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Hiermee verwijdert u een database.|

> [!TIP]
> Maken van veel databases in een elastische pool kan duren wanneer klaar met Hallo portal of PowerShell-cmdlets die slechts één database tegelijkertijd maken. Zie tooautomate maken voor een elastische pool [CreateOrUpdateElasticPoolAndPopulate](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).
>

## <a name="manage-sql-database-elastic-pools-using-hello-azure-cli"></a>Elastische SQL-Database-groepen met behulp van Azure CLI Hallo beheren

toocreate en beheren van de SQL-Database elastische pools Hello [Azure CLI](/cli/azure/overview), gebruikt u de volgende Hallo [Azure CLI SQL Database](/cli/azure/sql/db) opdrachten. Gebruik Hallo [Cloud Shell](/azure/cloud-shell/overview) toorun Hallo CLI in uw browser of [installeren](/cli/azure/install-azure-cli) op Mac OS-, Linux- of Windows. 

> [!TIP]
> Zie voor Azure CLI-voorbeeldscripts, [gebruik CLI toomove een Azure SQL database in een elastische SQL-groep](scripts/sql-database-move-database-between-pools-cli.md) en [gebruik Azure CLI tooscale een elastische SQL-groep in Azure SQL Database](scripts/sql-database-scale-pool-cli.md).
>

| Cmdlet | Beschrijving |
| --- | --- |
|[elastische sql-AZ-groep maken](/cli/azure/sql/elastic-pool#create)|Maakt een elastische pool.|
|[lijst met AZ sql elastische pool](/cli/azure/sql/elastic-pool#list)|Retourneert een lijst met elastische pools in een server.|
|[AZ sql elastische pool lijst-databases](/cli/azure/sql/elastic-pool#list-dbs)|Retourneert een lijst met databases in een elastische pool.|
|[AZ sql elastische pool-edities](/cli/azure/sql/elastic-pool#list-editions)|Omvat ook beschikbaar DTU groepsinstellingen, opslaglimieten, en per database-instellingen. In de volgorde tooreduce uitgebreidheid aanvullende opslaglimieten en per database kan instellingen zijn standaard verborgen.|
|[update van de elastische pool AZ sql](/cli/azure/sql/elastic-pool#update)|Een elastische pool-updates.|
|[AZ sql elastische groep verwijderen](/cli/azure/sql/elastic-pool#delete)|Hallo elastische groep verwijderd.|

## <a name="manage-sql-database-elastic-pools-using-transact-sql"></a>Elastische SQL-Database-groepen met Transact-SQL beheren

toocreate en de verplaatsing databases binnen de bestaande elastische pools of tooreturn informatie over de elastische groep van een SQL-Database met Transact-SQL, Hallo volgende T-SQL-opdrachten gebruiken. U kunt deze opdrachten hello Azure-portal met de opdracht [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), of een ander programma dat kan verbinding maken met tooan Azure SQL Database-server en doorgeven Transact-SQL de opdrachten. toocreate en beheren van databases, servers en firewallregels, Zie [maken en beheren van Azure SQL Database-servers en met Transact-SQL-databases](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-transact-sql).

> [!IMPORTANT]
> U niet kunt maken, bijwerken of verwijderen van een Azure SQL Database elastische pool met Transact-SQL. U kunt toevoegen of verwijderen van de databases uit een elastische pool en kunt u DMV's tooreturn informatie over bestaande elastische pools.
>

| Opdracht | Beschrijving |
| --- | --- |
|[DATABASE (Azure SQL Database) maken](/sql/t-sql/statements/create-database-azure-sql-database)|Maakt een nieuwe database in een bestaande pool of als een individuele database. U moet verbonden toohello hoofddatabase toocreate een nieuwe database.|
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) |Een database verplaatsen naar, uit of tussen elastische pools.|
|[DATABASE (Transact-SQL) verwijderen](/sql/t-sql/statements/drop-database-transact-sql)|Hiermee verwijdert u een database.|
|[sys.elastic_pool_resource_stats (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-elastic-pool-resource-stats-azure-sql-database)|Retourneert de gebruiksstatistieken resource voor alle Hallo-pools voor elastische databases in een logische server. Voor elke elastische databasegroep moet er één rij voor elke 15 seconden reporting venster (vier rijen per minuut). Dit omvat CPU, IO, logboek, opslagverbruik en gelijktijdige aanvraag/sessie gebruik door alle databases in Hallo van toepassingen.|
|[sys.database_service_objectives (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Retourneert Hallo edition (servicelaag), servicedoelstelling (prijscategorie) en de naam van de elastische groep, indien aanwezig, voor een Azure SQL database of een Azure SQL Data Warehouse. Als u aangemeld bent op de hoofddatabase toohello in een Azure SQL Database-server, retourneert de informatie voor alle databases. Voor Azure SQL Data Warehouse moet u verbonden toohello hoofddatabase.|

## <a name="manage-sql-database-elastic-pools-using-hello-rest-api"></a>SQL-Database van de elastische pools Hallo REST-API met beheren

toocreate en SQL-Database van de elastische pools Hallo REST-API met beheren, Zie [REST-API van Azure SQL Database](/rest/api/sql/).

## <a name="next-steps"></a>Volgende stappen

* Zie voor een video [video loop van de Microsoft Virtual Academy op elastische mogelijkheden van Azure SQL Database](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554)
* Zie toolearn meer informatie over ontwerppatronen voor SaaS-toepassingen met elastische pools [ontwerppatronen voor multitenant SaaS-toepassingen met Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).
* Zie voor een SaaS-zelfstudie met elastische pools, [inleiding toohello Wingtip SaaS-toepassing](sql-database-wtp-overview.md).
