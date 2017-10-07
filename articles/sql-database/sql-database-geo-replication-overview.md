---
title: aaaFailover groepen en actieve geo-replicatie - Azure SQL Database | Microsoft Docs
description: Automatische failover groepen met actieve geo-replicatie kunt u toosetup 4 replica's van uw database in een hello Azure-datacenters en autoomatically failover in Hallo-gebeurtenis van een storing.
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2a29f657-82fb-4283-9a83-e14a144bfd93
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 07/10/2017
ms.author: sashan
ms.openlocfilehash: 7a39af8505624c0f19c5abccff051af836b1f9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-failover-groups-and-active-geo-replication"></a>Overzicht: Failover-groepen en actieve geo-replicatie
Actieve geo-replicatie kunt u tooconfigure van toofour leesbare secundaire databases in Hallo dezelfde of verschillende datacenters locaties (regio's). Secundaire databases zijn beschikbaar voor het uitvoeren van query's en failover in geval van een data center onderbreking of Hallo onvermogen tooconnect toohello primaire database Hallo. Hallo failover moet handmatig worden gestart door de toepassing hello van Hallo-gebruiker. Na een failover heeft de nieuwe primaire Hallo het eindpunt van een andere verbinding. 

> [!NOTE]
> Actieve geo-replicatie is beschikbaar voor alle databases in alle Servicelagen in alle regio's.
>  

Azure SQL Database automatische failover groepen (in preview) is een voorziening waarmee SQL-Database tooautomatically beheren relatie geo-replicatie, connectiviteit en failover op grote schaal. Met deze Hallo klanten voordeel Hallo mogelijkheid tooautomatically meerdere verwante databases in de secundaire regio Hallo herstellen na onherstelbare regionale fouten of andere niet-geplande gebeurtenissen die leiden verlies van volledige of gedeeltelijke Hallo SQL Database-service tot beschikbaarheid in Hallo primaire regio. Bovendien kan Hallo leesbare secundaire databases toooffload alleen-lezen werkbelastingen worden gebruikt.  Omdat automatische failover groepen hebben betrekking op meerdere databases die moeten ze zijn geconfigureerd op de primaire server Hallo. Primaire en secundaire servers zich bevinden in Hallo hetzelfde abonnement. Automatische failover groepen ondersteuning voor replicatie van alle databases in Hallo groep tooonly één secundaire server in een andere regio. Actieve geo-replicatie, zonder automatische failover-groepen, kunt u too4 secundaire replica's in elke regio.

Als u van actieve geo-replicatie gebruikmaakt en voor de primaire database is mislukt reden of gewoon behoeften toobe offline gezet, kunt u failover tooany van de secundaire databases starten. Wanneer failover geactiveerde tooone van Hallo secundaire databases, andere secundaire replica's worden automatisch gekoppelde toohello nieuwe primaire. Als u automatische failover databaseherstel toomanage (in preview) en een storing die van invloed is op een of meer databases in de resultaten van Groepsbeleid Hallo in automatische failover Hallo gegroepeerd. U kunt automatische failover-beleid voor Hallo die het beste voldoet aan de behoeften van uw toepassing configureren of kunt u opt-out en handmatige activering gebruiken. Bovendien automatisch een failover-groepen (in preview) Geef alleen-lezen en alleen-lezen-listener-eindpunten die blijven ongewijzigd tijdens failovers. Of u handmatig of automatisch failover-activering gebruikt, verandert failover alle secundaire databases in Hallo groep tooprimary. Nadat Hallo database failover is voltooid, is Hallo DNS-record automatisch bijgewerkt tooredirect Hallo eindpunten toohello nieuw gebied.

U kunt replicatie en failover van een individuele database of een set van databases op een server of in een elastische pool van actieve geo-replicatie beheren. U kunt doen dat met Hallo [Azure-portal](sql-database-geo-replication-portal.md), [PowerShell](sql-database-geo-replication-powershell.md), [Transact-SQL](sql-database-geo-replication-transact-sql.md), of Hallo [REST-API](https://msdn.microsoft.com/library/azure/mt163685.aspx). Controleert de verificatievereisten Hallo voor uw server en database zijn geconfigureerd op de nieuwe primaire Hallo na een failover. Zie voor meer informatie [beveiliging van SQL Database na het herstel na noodgevallen](sql-database-geo-replication-security-config.md). Dit geldt beide tooactive geo-replicatie en automatische failover groepen (in preview).

Actieve geo-replicatie maakt gebruik van Hallo [altijd op](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) technologie van SQL Server-tooasynchronously doorgevoerde transacties op Hallo primaire database tooa secundaire database read committed-momentopname-isolatie (RCSI) met repliceren. Automatische failover groepen bieden Hallo groep semantiek boven op actieve geo-replicatie maar Hallo mechanisme voor dezelfde asynchrone replicatie wordt gebruikt. Wanneer ze op een willekeurig moment Hallo secundaire database is mogelijk enigszins achter de primaire database hello, Hallo secundaire gegevens kan worden gegarandeerd toonever gedeeltelijke transacties hebben. Regio-overschrijdende redundantie kan toepassingen tooquickly herstellen vanuit een permanente verlies van een hele datacenter of delen van een datacenter veroorzaakt door een natuurramp, onherstelbare menselijke fouten of schadelijke acties uit. Hallo specifieke RPO gegevens kan worden gevonden op [overzicht van zakelijke continuïteit](sql-database-business-continuity.md).

Hallo toont volgende afbeelding een voorbeeld van actieve geo-replicatie geconfigureerd met een primaire in Hallo Noordelijk Centraal, VS regio en secundaire in Hallo Zuid-centraal VS regio.

![geo-replicatie-relatie](./media/sql-database-active-geo-replication/geo-replication-relationship.png)

Omdat secundaire databases Hallo kunnen gelezen worden, worden ze gebruikte toooffload alleen-lezen werkbelastingen, zoals rapportage van taken. Als u actieve geo-replicatie gebruikt, is het mogelijk toocreate Hallo secundaire database in Hallo dezelfde regio met primaire hello, maar niet verhogen van de toepassing hello herstelmogelijkheden toocatastrophic fouten. Als u automatische failover-groepen (in preview) gebruikt, wordt de secundaire database altijd gemaakt in een andere regio.

Bovendien kan toodisaster herstel actieve geo-replicatie worden gebruikt in Hallo volgen scenario's:

* **Migratie van de database**: kunt u actieve geo-replicatie toomigrate een database van één server tooanother online met minimale downtime.
* **Toepassingsupgrades**: U kunt een extra secundaire als een mislukken back-up maken tijdens toepassingsupgrades.

tooachieve echte bedrijfscontinuïteit, toe te voegen databaseredundantie tussen datacentra is slechts een deel van het Hallo-oplossing. Herstellen van een toepassing (service) end-to-end nadat een onherstelbare fout is vereist voor herstel van alle onderdelen die deel uitmaken van Hallo-service en afhankelijke services. Voorbeelden van deze onderdelen zijn Hallo-clientsoftware (bijvoorbeeld een browser met een aangepaste JavaScript), web-front-ends, opslag- en DNS. Het is essentieel dat alle onderdelen robuuste toohello dezelfde fouten zijn en beschikbaar binnen de Hallo beoogde hersteltijd (RTO) van uw toepassing. Daarom moet tooidentify alle afhankelijke services en begrijpen Hallo garanties en mogelijkheden bieden. Vervolgens moet u passende stappen tooensure die uw servicefuncties tijdens de failover van Hallo services waarvan deze afhankelijk is, Hallo nemen. Zie voor meer informatie over het ontwerpen van oplossingen voor herstel na noodgevallen [Cloudoplossingen voor Disaster Recovery met actieve geo-replicatie ontwerpen](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

## <a name="active-geo-replication-capabilities"></a>Mogelijkheden van actieve geo-replicatie
Hallo actieve geo-replicatie functie biedt Hallo essentiële mogelijkheden te volgen:
* **Automatische asynchrone replicatie**: U kunt alleen een secundaire database maken door de bestaande database tooan toe te voegen. Hallo secundaire kan worden gemaakt in een Azure SQL Database-server. Zodra gemaakt, wordt Hallo secundaire database ingevuld met Hallo-gegevens van de primaire database Hallo gekopieerd. Dit proces staat bekend als seeding. Nadat de secundaire database is gemaakt en seeding, primaire database toohello asynchroon zijn updates toohello secundaire database automatisch gerepliceerd. Asynchrone replicatie betekent dat transacties worden vastgelegd op de primaire database Hallo voordat u deze gerepliceerde toohello secundaire database. 
* **Leesbare secundaire databases**: een toepassing heeft toegang tot een secundaire database voor alleen-lezen bewerkingen met behulp van Hallo dezelfde of verschillende beveiligings-principals die wordt gebruikt voor toegang tot de primaire database Hallo. Hallo secundaire databases werkt met snapshot-isolatie modus tooensure replicatie van Hallo-updates van primaire hello (logboek replay) niet door query's die worden uitgevoerd op de secundaire Hallo is vertraagd.

   > [!NOTE]
   > Hallo logboek replay is vertraagd op Hallo secundaire database als er schema-updates of wordt ontvangen van Hallo primaire waarvoor een schemavergrendeling op Hallo secundaire database. 
   > 

* **Meerdere secundaire databases**: twee of meer secundaire databases verhogen redundantie en niveau van beveiliging voor de primaire database Hallo en toepassingen. Als er meerdere secundaire databases bestaan, blijft toepassing hello beveiligd zelfs als een van de secundaire databases Hallo mislukt. Als er slechts één secundaire database, en dit mislukt, de toepassing hello wordt blootgesteld toohigher risico totdat er een nieuwe secundaire database is gemaakt.

   > [!NOTE]
   > Als u van actieve geo-replicatie toobuild een globaal gedistribueerde toepassing gebruikmaakt en moet tooprovide alleen-lezen toegang toodata in meer dan 4 regio's, kunt u secundaire van een secundaire (dit proces wordt '-koppeling genoemd). Op deze manier kunt u vrijwel onbeperkt schalen van databasereplicatie bereiken. Bovendien verminderd chaining Hallo van replicatie vanaf de primaire database Hallo. Hallo nadeel is Hallo verbeterde replication lag op Hallo leaf meest secundaire databases. . 
   >

* **Ondersteuning van de elastische groep databases**: actieve geo-replicatie kan worden geconfigureerd voor een database in een elastische pool. Hallo secundaire database kan worden in een andere elastische pool. Voor gewone databases Hallo secundaire worden een elastische pool en omgekeerd zolang Hallo Servicelagen zijn Hallo dezelfde. 
* **Configureerbare prestatieniveau van de secundaire database Hallo**: een secundaire database kan worden gemaakt met een lager prestatieniveau dan Hallo primaire. Primaire en secundaire databases zijn vereist toohave Hallo dezelfde servicelaag. Deze optie wordt niet aanbevolen voor toepassingen met hoge database schrijfactiviteiten omdat Hallo verbeterde replication lag Hallo risico van gegevensverlies aanzienlijke na een failover verhoogt. Nadat de failover Hallo toepassing prestaties beïnvloed tot Hallo nieuwe primaire is bovendien bijgewerkte tooa hogere prestaties niveau. Hallo logboek IO percentage diagram in Azure portal biedt een goede manier tooestimate Hallo minimaal prestatieniveau van Hallo secundaire die vereiste toosustain Hallo replicatie laden. Bijvoorbeeld, als uw primaire database P6 (1000 DTU) en het logboek-i/o-procent is heeft toobe ten minste 50% Hallo secundaire P4 (500 DTU). U kunt ook ophalen Hallo logboek IO gegevens met [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) of [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) weergaven van de database.  Zie voor meer informatie over Hallo SQL-Database prestatieniveaus [SQL Database-opties en prestaties](sql-database-service-tiers.md). 
* **Gebruiker beheerde failover en failback**: een secundaire database expliciet geschakelde toohello primaire rol kan zijn op elk gewenst moment door de toepassing hello of Hallo gebruiker. Tijdens een werkelijke storing Hallo moet 'niet-geplande' worden gebruikt, die direct bijdraagt aan een secundaire toobe Hallo primaire. Wanneer Hallo mislukte primaire wordt hersteld en is beschikbaar opnieuw Hallo systeem automatisch aanhalingstekens Hallo hersteld als een secundaire primaire en brengt u het up-to-date blijven met de nieuwe primaire Hallo. Vervaldatum toohello asynchrone aard van replicatie, kan een kleine hoeveelheid gegevens worden verbroken tijdens niet-geplande failovers als een primaire mislukt voordat het Hallo meest recente wijzigingen toohello secundaire wordt gerepliceerd. Als een primaire met meerdere secundaire replica's failover wordt uitgevoerd, Hallo system Hallo Replicatierelaties automatisch geconfigureerd en koppelingen Hallo resterende secundaire servers toohello zojuist gepromoveerd primaire zonder tussenkomst van de gebruiker. Nadat het Hallo-uitval waardoor Hallo failover wordt verholpen, kan het wenselijk tooreturn Hallo toepassing toohello primaire regio zijn. toodo dat Hallo failover-opdracht moet worden aangeroepen met Hallo 'gepland' optie. 
* **Referenties en firewallregels synchroon te houden**: wordt u aangeraden [database firewallregels](sql-database-firewall-configure.md) voor databases geogerepliceerde zodat deze regels kunnen worden gerepliceerd met Hallo database tooensure wordt alle secundaire databases hebt Hallo dezelfde firewallregels als primaire Hallo. Deze aanpak overbodig Hallo voor klanten toomanually configureren en firewallregels op servers die als host fungeert voor zowel de primaire en secundaire databases Hallo onderhouden. Op deze manier met behulp van [databasegebruikers opgenomen](sql-database-manage-logins.md) voor gegevens toegang zorgt ervoor dat zowel primaire als secundaire databases hebben altijd dezelfde gebruikersreferenties zodat tijdens een failover geen onderbrekingen is Hallo vanwege toomismatches met aanmeldingen en wachtwoorden. Met Hallo toevoeging van [Azure Active Directory](../active-directory/active-directory-whatis.md), klanten toegang tooboth primaire en secundaire gebruikersdatabases kunnen beheren en elimineren Hallo nodig voor het beheren van referenties in databases kan worden overgeslagen.

## <a name="auto-failover-group-capabilities"></a>Mogelijkheden voor automatische failover-groep

Automatische failover groepsfunctie biedt een krachtige abstractie van actieve geo-replicatie door de groep niveau replicatie en automatische failover-ondersteuning. Daarnaast verwijdert deze Hallo noodzaak toochange Hallo-SQL-verbindingsreeks na een failover doordat Hallo aanvullende listener-eindpunten. 

* **Failover-groep**: een of meer groepen van failover kunnen worden gemaakt tussen twee servers in verschillende regio's (primaire en secundaire servers). Elke groep kan een of meer databases die worden hersteld als een eenheid voor het geval alle of sommige primaire databases niet meer beschikbaar is vanwege onderbreking in de primaire regio Hallo tooan bevatten.  
* **Primaire server**: een server die als host fungeert voor Hallo primaire databases in Hallo failover-groep.
* **Secundaire server**: een server die als host fungeert voor Hallo secundaire databases in Hallo failover-groep. Hallo secundaire server kan niet in Hallo dezelfde regio bevinden als de primaire server Hallo.
* **Toe te voegen toofailover databasesgroep**: U kunt verschillende databases binnen een server te plaatsen of in een elastische pool in Hallo dezelfde failover-groep. Als u een zelfstandige database toohello groep toevoegt, wordt automatisch een secundaire database gemaakt met behulp van hetzelfde niveau van edition en prestaties Hallo. Als de primaire database Hallo in een elastische pool, Hallo secundaire wordt automatisch gemaakt in Hallo elastische pool Hello dezelfde naam. Als u een database die al een secundaire database in de secundaire server Hallo toevoegt, wordt die geo-replicatie wordt overgenomen door Hallo-groep.

   > [!NOTE]
   > Wanneer u een database die al een secundaire database in een server die geen deel uitmaakt van Hallo failover groep toevoegt, wordt een nieuwe secundaire gemaakt in Hallo secundaire server. 
   >

* **Failover-groep lezen-schrijven listener**: een DNS CNAME-record wordt gevormd als  **&lt;failover groepsnaam&gt;. database.windows.net** die de huidige primaire server-URL toohello verwijst. Hallo lezen-schrijven SQL-toepassingen kunt tootransparently toohello primaire database opnieuw verbinding maken wanneer Hallo primaire gewijzigd na een failover. 
* **Failover-groep alleen-lezen-listener**: een DNS CNAME-record wordt gevormd als  **&lt;failover groepsnaam&gt;. secondary.database.windows.net** die toohello secundaire server URL verwijst. Het Hallo kan alleen-lezen SQL-toepassingen tootransparently verbinding toohello secundaire database met behulp van Hallo opgegeven regels voor taakverdeling. U kunt eventueel opgeven als u wilt dat Hallo alleen-lezen toobe verkeer automatisch omgeleid toohello primaire server als de secundaire server Hallo niet beschikbaar is.
* **Beleid voor automatische failover**: Hallo failover-groep is standaard geconfigureerd met een beleid voor automatische failover. Hallo system activeert failover als Hallo storing wordt gedetecteerd. Als u toocontrol Hallo de werkstroom van de toepassing hello wilt, kunt u automatische failover uitschakelen. 
* **Handmatige failover**: U kunt failover handmatig op elk gewenst moment ongeacht Hallo automatische failover-configuratie. Als automatische failover-beleid niet geconfigureerd voor handmatige failover is is het vereiste toorecover databases in Hallo failover-groep. U kunt de geforceerde of beschrijvende failover (met volledige gegevenssynchronisatie) starten. Hallo laatstgenoemde kan gebruikte toorelocate Hallo actieve server toohello primaire regio worden. Als de failover is voltooid zijn Hallo DNS-records automatisch bijgewerkt tooensure connectiviteit toohello juiste server.
* **Respijtperiode met gegevensverlies**: omdat Hallo primaire en secundaire databases worden gesynchroniseerd met de asynchrone replicatie Hallo failover kan leiden tot verlies van gegevens. U kunt Hallo automatische failover beleid tooreflect aanpassen van uw toepassing tolerantie toodata gegevensverlies. Door het configureren van **GracePeriodWithDataLossHours**, kunt u bepalen hoe lang Hallo-systeem wacht voordat het Hallo-failover die waarschijnlijk tooresult gegevensverlies is gestart. 

   > [!NOTE]
   > Wanneer systeem detecteert dat de databases in de groep Hallo Hallo nog steeds online zijn (bijvoorbeeld Hallo onderbreking alleen van invloed op Hallo service besturingselement vlak), wordt onmiddellijk Hallo failover met volledige gegevenssynchronisatie (beschrijvende failover) ongeacht Hallo waarde geactiveerd ingesteld door **GracePeriodWithDataLossHours**. Dit gedrag zorgt ervoor dat er geen gegevens verloren gaan tijdens het Hallo-herstel. Hallo respijtperiode heeft alleen effect als een beschrijvende failover niet mogelijk is. Als Hallo onderbreking is verholpen voordat Hallo respijtperiode is verlopen, Hallo failover niet is geactiveerd.
   >

* **Meerdere failover groepen**: U kunt meerdere groepen voor failover voor Hallo configureren dezelfde combinatie van servers toocontrol Hallo schaal van failovers. Elke groep onafhankelijk failover wordt uitgevoerd. Als uw toepassing met meerdere tenants elastische pools gebruikt, kunt u deze mogelijkheid toomix primaire en secundaire databases in elke groep. Op deze manier kunt u beperken Hallo gevolgen van een storing tooonly helft Hallo tenants.

## <a name="best-practices-of-building-highly-available-service"></a>Aanbevolen procedures van het bouwen van maximaal beschikbare service

een maximaal beschikbare service die gebruikmaakt van Azure SQL database Hallo klanten toobuild moet als volgt:
- **Failover-groep gebruiken**: een of meer groepen van failover kunnen worden gemaakt tussen twee servers in verschillende regio's (primaire en secundaire servers). Elke groep kan een of meer databases die worden hersteld als een eenheid voor het geval alle of sommige primaire databases niet meer beschikbaar is vanwege onderbreking in de primaire regio Hallo tooan bevatten. Hallo failover groep maakt geo-secundaire database met dezelfde service doelstelling als primaire Hallo Hallo. Als u een bestaande geo-replicatie relatie toohello failover groep Zorg ervoor dat Hallo geo-secundaire is geconfigureerd met dezelfde service level objective als Hallo toevoegt Hallo primaire.
- **Gebruik alleen-lezen-listener voor OLTP-werkbelasting**: bij het uitvoeren van OLTP-bewerkingen gebruik  **&lt;failover groepsnaam&gt;. database.windows.net** zoals Hallo server-URL en het Hallo-verbindingen zijn automatisch gerichte toohello primaire. Deze URL wordt niet gewijzigd na een failover Hallo.  
Opmerking Hallo failover omvat het bijwerken van Hallo DNS-record dus Hallo clientverbindingen omgeleide toohello nieuwe primaire is alleen geldig na Hallo client DNS-cache is vernieuwd.
- **Gebruik van alleen-lezen-listener voor de werkbelasting van alleen-lezen**: als u een logisch is geïsoleerd alleen-lezen-werkbelasting die fouttolerante toocertain veroudering van gegevens hebt, kunt u Hallo secundaire database in de toepassing hello. Voor alleen-lezen-sessies gebruiken  **&lt;failover groepsnaam&gt;. secondary.database.windows.net** zoals Hallo server-URL en het Hallo-verbinding automatisch gerichte toohello secundaire zijn. Het is ook raadzaam die u hebt opgegeven in de verbindingsreeks bedoeling lezen met behulp van **ApplicationIntent ReadOnly =**. 
- **Worden voorbereid voor de prestaties nadelig beïnvloeden**: SQL failover besluit is onafhankelijk van het Hallo rest van de toepassing hello of andere services die worden gebruikt. Hallo-toepassing worden "gecombineerd" met een aantal onderdelen in één regio en sommige in een andere. tooavoid hello degradatie, zorg Hallo redundante toepassingsimplementatie in Hallo DR regio en Hallo richtlijnen in dit artikel.  
Opmerking Hallo toepassing in Hallo DR regio geen toouse een andere verbindingsreeks.  
- **Voorbereiden voor gegevensverlies**: als er een storing wordt gedetecteerd, SQL lezen-schrijven failover automatisch geactiveerd als er geen gegevens verloren gaan toohello aanbevolen van onze kennis. Anders dat wordt gewacht totdat u door het opgegeven Hallo-periode **GracePeriodWithDataLossHours**. Als u hebt opgegeven **GracePeriodWithDataLossHours**, worden voorbereid op verlies van gegevens. In het algemeen tijdens uitval, Azure meer gericht op beschikbaarheid. Als u geen enkele gegevens verloren gaan, zorg ervoor dat tooset **GracePeriodWithDataLossHours** tooa voldoende getal, zoals 24 uur. 


## <a name="upgrading-or-downgrading-a-primary-database"></a>Een upgrade of een primaire database downgraden
U kunt de upgrade of een prestatieniveau van primaire database tooa verschillende downgraden (binnen Hallo dezelfde servicelaag) zonder te verbreken geen secundaire databases. Bij het bijwerken, wordt aangeraden dat u eerst de secundaire database Hallo upgraden en werk vervolgens Hallo primaire. Wanneer downgraden, Hallo volgorde omkeren: Hallo primaire eerst downgraden en vervolgens gebruik maken van secundaire Hallo. Wanneer u bijwerkt of Hallo database tooa verschillende servicelaag downgraden wordt deze aanbeveling afgedwongen. 

> [!NOTE]
> Als u een secundaire database als onderdeel van de failoverconfiguratie groep Hallo gemaakt is het niet aanbevolen toodowngrade Hallo secundaire database. Dit is tooensure uw gegevenslaag is voldoende capaciteit tooprocess uw reguliere werkbelasting nadat de failover is geactiveerd. 
>

## <a name="preventing-hello-loss-of-critical-data"></a>Hallo verlies van kritieke gegevens te voorkomen
Doorlopend kopiëren gebruikt vanwege toohello hoge latentie voor wide area network, een mechanisme voor asynchrone replicatie. Asynchrone replicatie maakt gegevensverlies onvermijdelijke als er een fout optreedt. Sommige toepassingen vereisen echter geen verlies van gegevens. tooprotect deze essentiële updates, een toepassingsontwikkelaar kunnen aanroepen Hallo [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx) system procedure onmiddellijk na het Hallo-transactie doorvoeren. Het aanroepen van **sp_wait_for_database_copy_sync** blokken Hallo thread aanroepen totdat Hallo laatste doorgevoerde transactie is verzonden toohello secundaire database. Echter, het wacht niet Hallo verzonden transacties toobe opnieuw afgespeeld en doorgevoerd op de secundaire Hallo. **sp_wait_for_database_copy_sync** is binnen het bereik tooa specifieke doorlopend kopiëren koppeling. Elke gebruiker met Hallo verbinding rechten toohello primaire database kunt deze procedure aanroept.

> [!NOTE]
> **sp_wait_for_database_copy_sync** wordt gegevensverlies voorkomen na een failover, maar deze wordt niet gegarandeerd dat volledige synchronisatie voor leestoegang. Hallo vertraging veroorzaakt door een **sp_wait_for_database_copy_sync** procedureaanroep kan aanzienlijke en is afhankelijk van grootte van het transactielogboek Hallo HALLO hallo gelijktijdig met Hallo-aanroep. 
> 

## <a name="programmatically-managing-failover-groups-and-active-geo-replication"></a>Failover-groepen en actieve geo-replicatie programmatisch te beheren
Zoals eerder besproken automatische failover-groepen (in preview) en actief is geo-replicatie kan ook worden beheerd via een programma met Azure PowerShell en Hallo REST-API. Hallo volgende tabellen beschrijven Hallo reeks opdrachten die beschikbaar zijn.

**Azure Resource Manager-API en op rollen gebaseerde beveiliging**: actieve geo-replicatie bevat een set met Azure Resource Manager-API's voor beheer, met inbegrip van Hallo [REST-API van Azure SQL Database](https://docs.microsoft.com/rest/api/sql/) en [Azure PowerShell-cmdlets](https://docs.microsoft.com/powershell/azure/overview). Deze API's vereisen Hallo gebruik van resourcegroepen en ondersteuning voor beveiliging op basis van rollen (RBAC). Zie voor meer informatie over hoe tooimplement toegang krijgen tot rollen, [rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-what-is.md).

> [!NOTE]
> Veel nieuwe functies van actieve geo-replicatie worden alleen ondersteund met [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) op basis van [REST-API van Azure SQL](https://msdn.microsoft.com/library/azure/mt163571.aspx) en [Azure SQL Database PowerShell-cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx). Hallo [(klassiek) REST-API](https://msdn.microsoft.com/library/azure/dn505719.aspx) en [cmdlets van Azure SQL Database (klassiek)](https://msdn.microsoft.com/library/azure/dn546723.aspx) worden ondersteund voor neerwaartse compatibiliteit met behulp van hello Azure Resource Manager gebaseerde API's worden aanbevolen. 
> 

## <a name="manage-sql-database-failover-using-using-transact-sql"></a>SQL database failover met behulp van Transact-SQL beheren

| Opdracht | Beschrijving |
| --- | --- |
| [ALTER DATABASE (Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) |SECUNDAIRE ON-SERVER toevoegen argument toocreate een secundaire database gebruiken voor een bestaande database en start gegevensreplicatie |
| [ALTER DATABASE (Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) |Gebruik een FAILOVER of FORCE_FAILOVER_ALLOW_DATA_LOSS tooswitch een secundaire database toobe primaire tooinitiate failover |
| [ALTER DATABASE (Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) |Gebruik secundaire ON-SERVER verwijderen tooterminate een gegevensreplicatie tussen een SQL-Database en het Hallo opgegeven secundaire database. |
| [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx) |Retourneert informatie over alle bestaande replicatiekoppelingen voor elke database op logische hello Azure SQL Database-server. |
| [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx) |Opgehaald Hallo tijd van laatste replicatie, laatste vertraging van replicatie en andere informatie over de replicatiekoppeling Hallo voor een bepaalde SQL-database. |
| [sys.dm_operation_status bevat (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx) |Hallo-status voor alle databasebewerkingen waaronder Hallo status van replicatiekoppelingen Hallo bevat. |
| [sp_wait_for_database_copy_sync (Azure SQL Database)](https://msdn.microsoft.com/library/dn467644.aspx) |zorgt ervoor dat Hallo toepassing toowait totdat alle doorgevoerde transacties zijn gerepliceerd en bevestigd door Hallo actieve secundaire database. |
|  | |

## <a name="manage-sql-database-failover-using-using-powershell"></a>SQL database failover met behulp van PowerShell beheren

| Cmdlet | Beschrijving |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Hiermee haalt u een of meer databases. |
| [Nieuwe AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary) |Hiermee maakt u een secundaire database voor een bestaande database en start gegevensreplicatie. |
| [Set-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary) |Een secundaire database toobe primaire tooinitiate failover verandert. |
| [Verwijder AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) |Beëindigt gegevensreplicatie tussen een SQL-Database en het Hallo opgegeven secundaire database. |
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) |Hiermee haalt u Hallo geo-replicatiekoppelingen tussen een Azure SQL Database en een resourcegroep of SQL Server. |
| [Nieuwe AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Deze opdracht maakt een failover-groep en registreert deze op de primaire en secundaire servers|
| [Verwijder AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/remove-azurermsqldatabasefailovergroup) | Hallo failover groep verwijdert van Hallo-server en alle secundaire databases opgenomen Hallo groep verwijderd |
| [Get-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/get-azurermsqldatabasefailovergroup) | Configuratie van failover Hallo opgehaald |
| [Set-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Hallo-configuratie van Hallo failover groep wijzigen |
| [Switch-AzureRMSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/switch-azurermsqldatabasefailovergroup) | Triggers failover van Hallo failover groep toohello secundaire server |
|  | |

> [!IMPORTANT]
> Zie voor voorbeelden van scripts, [en failover een individuele database met behulp van actieve geo-replicatie configureren](scripts/sql-database-setup-geodr-and-failover-database-powershell.md), [en failover een gegroepeerde database met behulp van actieve geo-replicatie configureren](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md), en [configureren en failover een failover-groep voor één database (preview)] (scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md.
>

## <a name="manage-sql-database-failover-using-hello-rest-api"></a>SQL database failover via Hallo REST-API beheren
| API | Beschrijving |
| --- | --- |
| [Maken of de Database-Update (createMode = herstellen)](/rest/api/sql/Databases/CreateOrUpdate) |Gemaakt, bijgewerkt of hersteld van een primaire of secundaire database. |
| [Get maken of bijwerken van de databasestatus](/rest/api/sql/Databases/CreateOrUpdate) |Retourneert Hallo status tijdens een bewerking voor maken. |
| [Secundaire Database instellen als primaire (geplande Failover)](https://docs.microsoft.com/rest/api/sql/replicationlinkss#ReplicationLinks_Failover) |Hiermee wordt ingesteld welke replica-database door de storing worden overgenomen uit de huidige primaire replica-database Hallo primaire is. |
| [Secundaire Database instellen als primaire (niet-geplande Failover)](https://docs.microsoft.com/rest/api/sql/replicationlinks#ReplicationLinks_FailoverAllowDataLoss) |Hiermee wordt ingesteld welke replica-database door de storing worden overgenomen uit de huidige primaire replica-database Hallo primaire is. Deze bewerking kan leiden tot verlies van gegevens. |
| [Replicatiekoppeling ophalen](/rest/api/sql/replicationlinks/get) |Hiermee haalt een bepaalde replicatiekoppeling voor een gegeven SQL-database in een associatie geo-replicatie. Het ophalen van Hallo informatie zichtbaar is in de catalogusweergave Hallo-sys.geo_replication_links. |
| [Koppelingen voor databasereplicatie - lijst per Database](/rest/api/sql/replicationlinks/listbydatabase) | Hiermee haalt alle koppelingen voor databasereplicatie voor een gegeven SQL-database in een associatie geo-replicatie. Het ophalen van Hallo informatie zichtbaar is in de catalogusweergave Hallo-sys.geo_replication_links. |
| [Replicatiekoppeling verwijderen](/rest/api/sql/databases/delete) | Hiermee verwijdert u een databasereplicatiekoppeling. Tijdens de failover kan niet worden uitgevoerd. |
| [Maken of Failover-Update groep] / rest/api/sql/failovergroups/createorupdate) | Maken of bijwerken van een failover-groep |
| [Failover-groep verwijderen](/rest/api/sql/failovergroups/delete) | Hallo failover groep verwijdert van Hallo-server |
| [Failover (gepland)](/rest/api/sql/failovergroups/failover) | Failover van Hallo huidige primaire server toothis server. |
| [Force Failover verlies van gegevens toestaan](/rest/api/sql/failovergroups/forcefailoverallowdataloss) |ails via van Hallo huidige primaire server toothis server. Deze bewerking kan leiden tot verlies van gegevens. |
| [Get-Failover-groep](/rest/api/sql/failovergroups/get) | Hiermee haalt u een failover-groep. |
| [Lijst met failover-groepen door Server](/rest/api/sql/failovergroups/listbyserver) | Een lijst met groepen van Hallo-failover in een server. |
| [Failover-Updategroep](/rest/api/sql/failovergroups/update) | Een groep failover-updates. |
|  | |

## <a name="next-steps"></a>Volgende stappen
* Zie voor voorbeeldscripts:
   - [Configureren en failover een individuele database met behulp van actieve geo-replicatie](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
   - [Configureren en failover een gegroepeerde database met behulp van actieve geo-replicatie](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md)
   - [Configureren en failover een failover-groep voor één database (preview)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md)
* Zie voor een overzicht van zakelijke continuïteit en scenario's [Business continuity-overzicht](sql-database-business-continuity.md)
* toolearn over Azure SQL Database automatische back-ups, Zie [geautomatiseerde back-ups van SQL-Database](sql-database-automated-backups.md).
* toolearn over het gebruik van automatische back-ups voor herstel, Zie [een database terugzetten vanuit Hallo service geïnitieerde back-ups](sql-database-recovery-using-backups.md).
* toolearn over de verificatievereisten voor voor een nieuwe primaire server en database, Zie [beveiliging van SQL Database na het herstel na noodgevallen](sql-database-geo-replication-security-config.md).

