---
title: Database-noodherstel aaaSQL | Microsoft Docs
description: Meer informatie over hoe toorecover een database van een storing in regionale datacenter of falen met hello Azure SQL Database actieve geo-replicatie en geo-restore-mogelijkheden.
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 4800960e-3f9d-40ce-9e55-fb7f2784c067
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: sashan
ms.openlocfilehash: bae08485863067748107ec4808e52d8e88e2de0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-database-or-failover-tooa-secondary"></a>Een Azure SQL Database of failover tooa secundaire herstellen
Azure SQL Database biedt Hallo mogelijkheden voor het herstellen van een storing te volgen:

* [Actieve Geo-replicatie](sql-database-geo-replication-overview.md)
* [Geo-herstel](sql-database-recovery-using-backups.md#point-in-time-restore)

toolearn over zakelijke continuïteit-scenario's en Hallo-functies ondersteunen van deze scenario's, Zie [bedrijfscontinuïteit](sql-database-business-continuity.md).

### <a name="prepare-for-hello-event-of-an-outage"></a>Hallo-gebeurtenis van een storing voorbereiden
Geslaagd en herstel tooanother-gegevensgebied met behulp van actieve geo-replicatie of geografisch redundante back-ups, moet u tooprepare een server in een ander datacenter onderbreking toobecome Hallo nieuwe primaire server moet Hallo moet zich voordoen als goed gedefinieerde stappen hebben gedocumenteerde en geteste tooensure smooth herstel. Deze voorbereidende stappen omvatten:

* Identificeer Hallo logische server in een andere regio toobecome Hallo nieuwe primaire server. Met actieve geo-replicatie, wordt dit ten minste één en mogelijk een van de secundaire servers Hallo zijn. Geo-Herstel dit in het algemeen is een server in Hallo [gekoppelde regio](../best-practices-availability-paired-regions.md) voor Hallo regio waarin uw database zich bevindt.
* Identificeren en desgewenst definiëren, Hallo serverniveau firewallregels nodig op voor gebruikers tooaccess Hallo nieuwe primaire database.
* Bepalen hoe u tooredirect gebruikers toohello nieuwe primaire server gaat zoals door verbindingsreeksen wijzigen of door het wijzigen van DNS-vermeldingen.
* Identificeren, en desgewenst maken, Hallo aanmeldingen die moeten aanwezig zijn in de hoofddatabase Hallo op Hallo van de nieuwe primaire server en zorg ervoor dat deze aanmeldingen geschikte machtigingen hebben in de hoofddatabase hello, indien van toepassing. Zie voor meer informatie [beveiliging van SQL Database na het herstel na noodgevallen](sql-database-geo-replication-security-config.md)
* Regels voor waarschuwingen die toobe bijgewerkte toomap toohello nieuwe primaire database moet identificeren.
* Document Hallo controleconfiguratie op Hallo van de huidige primaire database
* Voer een [disaster recovery inzoomen](sql-database-disaster-recovery-drills.md). toosimulate een storing voor geo-restore kunt u verwijderen of wijzig de naam van Hallo bron toocause toepassing connectiviteit databasefout. toosimulate een storing voor actieve geo-replicatie, kunt u Hallo-webtoepassing of virtuele machine verbonden toohello database of failover Hallo database toocause connectiviteit toepassingsfouten uitschakelen.

## <a name="when-tooinitiate-recovery"></a>Wanneer tooinitiate herstel
Hallo-toepassing heeft gevolgen voor Hallo herstelbewerking wordt uitgevoerd. Het wijzigen van het SQL-verbindingsreeks Hallo of met behulp van DNS-omleiding is vereist en kan leiden tot permanent verlies van gegevens. Daarom mag deze alleen worden uitgevoerd wanneer Hallo onderbreking waarschijnlijk toolast langer is dan de beoogde hersteltijd van uw toepassing is. Wanneer hello toepassing geïmplementeerde tooproduction moet u regelmatige controle van de toepassingsstatus Hallo uitvoert en Hallo punten tooassert die Hallo herstel gerechtvaardigd is gegevens te volgen:

1. Permanente verbindingsfout van laag Hallo-toohello toepassingsdatabase.
2. Hello Azure-portal geeft een waarschuwing over een incident in Hallo-gebied met een grote impact.
3. Hello Azure SQL Database-server is gemarkeerd als beschadigd.

U kunt Hallo volgende herstelopties overwegen, afhankelijk van uw toepassing tolerantie toodowntime en mogelijke business aansprakelijkheid.

Gebruik Hallo [herstelbare Database ophalen](https://msdn.microsoft.com/library/dn800985.aspx) (*LastAvailableBackupDate*) tooget Hallo nieuwste geogerepliceerde herstelpunt.

## <a name="wait-for-service-recovery"></a>Wachttijd voor het herstel
Hello samenwerken Azure teams naar eer en geweten toorestore servicebeschikbaarheid snel mogelijk, maar, afhankelijk van de hoofdoorzaak Hallo duren uren of dagen voordat kan.  Als uw toepassing aanzienlijke downtime tolereren kan kunt u eenvoudig hello herstel toocomplete wachten. In dit geval is geen actie ondernemen vereist. U kunt de huidige servicestatus Hallo zien op onze [Azure Service Health Dashboard](https://azure.microsoft.com/status/). Na het herstel van de regio Hallo Hallo wordt beschikbaarheid van uw toepassing hersteld.

## <a name="fail-over-toogeo-replicated-secondary-database"></a>Failover toogeo gerepliceerde secundaire database
Als uitvaltijd van uw toepassing tot zakelijke aansprakelijkheid leiden kan moet u databases geo-replicatie in uw toepassing. Hallo tooquickly terugzetten beschikbaarheid in een andere regio bij een stroomstoring wordt het ingeschakeld. Meer informatie over hoe te[geo-replicatie configureren](sql-database-geo-replication-portal.md).

beschikbaarheid van Hallo toorestore database(s) u moet tooinitiate Hallo failover toohello geo-replicatie secundaire met een van de methoden Hallo ondersteund.

Gebruik een van de Hallo handleidingen toofail via tooa geo-replicatie secundaire database te volgen:

* [Failover tooa geo-replicatie secundaire met Azure Portal](sql-database-geo-replication-portal.md)
* [Failover-tooa-secundaire geo-replicatie met PowerShell](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
* [Failover tooa geo-replicatie secundaire met T-SQL](sql-database-geo-replication-transact-sql.md)

## <a name="recover-using-geo-restore"></a>Herstellen met behulp van geo-herstel
Als uw toepassing uitvaltijd niet in business aansprakelijkheid resulteert kunt u [geo-restore](sql-database-recovery-using-backups.md) als een methode toorecover de databases van uw toepassing. Een kopie van Hallo-database wordt gemaakt van de meest recente geografisch redundante back-up.

## <a name="configure-your-database-after-recovery"></a>Uw database na herstel configureren
Als u van geo-replicatie, failover of toorecover geo-herstel van een storing gebruikmaakt, moet u ervoor zorgen dat Hallo connectiviteit toohello nieuwe databases correct is geconfigureerd, zodat Hallo normale toepassing functie kan worden hervat. Dit is een controlelijst met taken tooget de herstelde database productie gereed.

### <a name="update-connection-strings"></a>Verbindingstekenreeksen bijwerken
Omdat de herstelde database bevindt zich in een andere server, moet u tooupdate van uw toepassing connection string toopoint toothat-server.

Zie voor meer informatie over het wijzigen van verbindingsreeksen Hallo ontwikkeling van de juiste taal voor uw [verbindingsbibliotheek](sql-database-libraries.md).

### <a name="configure-firewall-rules"></a>Firewallregels configureren
Moet u ervoor dat Hallo firewallregels zijn geconfigureerd op de server en op Hallo database overeen die zijn geconfigureerd op de primaire server Hallo en de primaire database toomake. Zie voor meer informatie [procedure: Firewall-instellingen configureren (Azure SQL Database)](sql-database-configure-firewall-settings.md).

### <a name="configure-logins-and-database-users"></a>Aanmeldingen en databasegebruikers configureren
Moet u ervoor dat alle Hallo aanmeldingen gebruikt door de toepassing op Hallo-server die als host de herstelde database fungeert toomake. Zie voor meer informatie [beveiligingsconfiguratie voor de geo-replicatie](sql-database-geo-replication-security-config.md).

> [!NOTE]
> U moet configureren en testen van de firewallregels voor server en aanmeldingen (en hun machtigingen) tijdens een herstel na noodgevallen detailanalyse. Deze objecten van het niveau van de server en de bijbehorende configuratie mogelijk niet beschikbaar tijdens het Hallo-storing.
> 
> 

### <a name="setup-telemetry-alerts"></a>Telemetrie-waarschuwingen instellen
Moet u ervoor dat de bestaande instellingen voor de waarschuwingsregel bijgewerkte toomap toohello herstelde database en Hallo andere server toomake.

Zie voor meer informatie over database waarschuwingsregels [waarschuwing meldingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) en [bijhouden servicestatus](../monitoring-and-diagnostics/insights-service-health.md).

### <a name="enable-auditing"></a>Controle inschakelen
Als controle vereist tooaccess is de database, moet u tooenable controle na het herstel van Hallo-database. Zie voor meer informatie [Databasecontrole](sql-database-auditing.md).

## <a name="next-steps"></a>Volgende stappen
* toolearn over Azure SQL Database automatische back-ups, Zie [geautomatiseerde back-ups van SQL-Database](sql-database-automated-backups.md)
* toolearn over zakelijke continuïteit ontwerp- en herstelinstellingen scenario's, Zie [continuïteit scenario's](sql-database-business-continuity.md)
* toolearn over het gebruik van automatische back-ups voor herstel, Zie [een database terugzetten vanuit Hallo service geïnitieerde back-ups](sql-database-recovery-using-backups.md)

