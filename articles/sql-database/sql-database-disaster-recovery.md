---
title: SQL Database-noodherstel | Microsoft Docs
description: Informatie over het herstellen van een database van een onderbreking van de regionale datacenter of mislukt met de Azure SQL Database actieve geo-replicatie en mogelijkheden van geo-herstel.
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
ms.openlocfilehash: e33f69bf04b32a31aae3c311c41aa44e4da5016a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-database-or-failover-to-a-secondary"></a>Een Azure SQL Database of een failover naar een secundaire herstellen
Azure SQL Database biedt de volgende mogelijkheden voor het herstellen van een storing:

* [Actieve Geo-replicatie](sql-database-geo-replication-overview.md)
* [Geo-herstel](sql-database-recovery-using-backups.md#point-in-time-restore)

Zie voor meer informatie over zakelijke continuïteit-scenario's en de onderdelen van deze scenario's ondersteunen, [bedrijfscontinuïteit](sql-database-business-continuity.md).

### <a name="prepare-for-the-event-of-an-outage"></a>Voorbereiden voor het geval er een storing
Voor een correcte werking met herstel naar een ander gegevensgebied met behulp van actieve geo-replicatie of geografisch redundante back-ups moet u een server voorbereiden in een ander datacenter onderbreking om te worden van de nieuwe primaire server indien nodig ook goed gedefinieerde stappen gedocumenteerde en geteste om ervoor te zorgen een smooth hebben veroorzaakt. Deze voorbereidende stappen omvatten:

* Identificeer de logische server in een andere regio worden de nieuwe primaire server. Met actieve geo-replicatie, wordt dit ten minste één en mogelijk een van de secundaire servers zijn. Geo-Herstel dit in het algemeen is een server in de [gekoppelde regio](../best-practices-availability-paired-regions.md) voor de regio waar uw database zich bevindt.
* Identificeren en eventueel definieert, de firewallregels voor een niveau van de server nodig is voor gebruikers toegang krijgen tot de nieuwe primaire database op.
* Bepalen hoe u gaat om gebruikers te leiden naar de nieuwe primaire server, zoals door verbindingsreeksen wijzigen of door het wijzigen van DNS-vermeldingen.
* Identificeren en u kunt maken met de aanmeldingen die moeten worden gebruikt in de hoofddatabase op de nieuwe primaire server en zorg ervoor dat deze aanmeldingen geschikte machtigingen hebben in de database master, indien van toepassing. Zie voor meer informatie [beveiliging van SQL Database na het herstel na noodgevallen](sql-database-geo-replication-security-config.md)
* Regels voor waarschuwingen die moeten worden bijgewerkt om te worden toegewezen aan de nieuwe primaire database identificeren.
* Documenteer de controle-configuratie op de huidige primaire database
* Voer een [disaster recovery inzoomen](sql-database-disaster-recovery-drills.md). U kunt om te simuleren een storing voor geo-herstel, verwijderen of wijzig de naam van de brondatabase als u de toepassing verbindingsfout optreedt. Om te simuleren een storing voor actieve geo-replicatie, kunt u de webtoepassing of de virtuele machine verbonden met de database of failover van de database om te leiden tot problemen met de toepassingen kunt uitschakelen.

## <a name="when-to-initiate-recovery"></a>Wanneer u herstel Start
De herstelbewerking heeft gevolgen voor de toepassing. Het wijzigen van de SQL-verbindingsreeks of met behulp van DNS-omleiding is vereist en kan leiden tot permanent verlies van gegevens. Daarom mag deze alleen worden uitgevoerd wanneer de onderbreking is waarschijnlijk langer dan de beoogde hersteltijd van uw toepassing. Wanneer de toepassing wordt geïmplementeerd naar productie moet u reguliere bewaking van de toepassingsstatus uitvoeren en dat het herstel is gerechtvaardigd assert met de volgende gegevenspunten:

1. Permanente verbinding is mislukt van de tier toepassing naar de database.
2. De Azure-portal geeft een waarschuwing over een incident in de regio met brede gevolgen.
3. De Azure SQL Database-server wordt gemarkeerd als beschadigd.

U kunt de volgende herstelopties overwegen, afhankelijk van uw toepassing tolerantie uitvaltijd en mogelijke business aansprakelijkheid.

Gebruik de [herstelbare Database ophalen](https://msdn.microsoft.com/library/dn800985.aspx) (*LastAvailableBackupDate*) om op te halen van de meest recente herstelpunt voor Geo-replicatie.

## <a name="wait-for-service-recovery"></a>Wachttijd voor het herstel
Het werk Azure teams naar eer en geweten om terug te zetten van de beschikbaarheid van services zoals snel, afhankelijk van de hoofdmap, maar mogelijk tot gevolg hebben dat kan uren of dagen duren.  Als uw toepassing aanzienlijke downtime tolereren kan kunt u gewoon wacht u totdat het herstel te voltooien. In dit geval is geen actie ondernemen vereist. U ziet de status van de huidige op onze [Azure Service Health Dashboard](https://azure.microsoft.com/status/). Na het herstel van de regio wordt van uw toepassing beschikbaarheid hersteld.

## <a name="fail-over-to-geo-replicated-secondary-database"></a>Failover naar de database op secundaire geo-replicatie
Als uitvaltijd van uw toepassing tot zakelijke aansprakelijkheid leiden kan moet u databases geo-replicatie in uw toepassing. De toepassing voor snel herstel beschikbaarheid in een andere regio bij een stroomstoring wordt het ingeschakeld. Meer informatie over hoe [geo-replicatie configureren](sql-database-geo-replication-portal.md).

U moet Start de failover naar de secundaire geo-replicatie met een van de ondersteunde methoden voor het herstellen van de beschikbaarheid van de databases.

Gebruik een van de volgende handleidingen failover naar een geo-replicatie secundaire database:

* [Failover naar een secundaire geo-replicatie met Azure Portal](sql-database-geo-replication-portal.md)
* [Failover naar een secundaire geo-replicatie met PowerShell](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
* [Failover naar een secundaire geo-replicatie met T-SQL](sql-database-geo-replication-transact-sql.md)

## <a name="recover-using-geo-restore"></a>Herstellen met behulp van geo-herstel
Als uw toepassing uitvaltijd niet in business aansprakelijkheid resulteert kunt u [geo-restore](sql-database-recovery-using-backups.md) als een methode voor het herstellen van de databases van uw toepassing. Een kopie van de database wordt gemaakt van de meest recente geografisch redundante back-up.

## <a name="configure-your-database-after-recovery"></a>Uw database na herstel configureren
Als u gebruikmaakt van geo-replicatie, failover of geo-herstel van een storing wilt herstellen, moet u ervoor zorgen dat de verbinding met de nieuwe databases correct is geconfigureerd, zodat de normale toepassing-functie kan worden hervat. Dit is een controlelijst van taken bij het klaarstomen van uw productieomgeving herstelde database.

### <a name="update-connection-strings"></a>Verbindingstekenreeksen bijwerken
Omdat de herstelde database bevindt zich in een andere server, moet u de verbindingsreeks van uw toepassing om te verwijzen naar die server bijwerken.

Zie voor meer informatie over het wijzigen van tekenreeksen voor de ontwikkeling van de juiste taal voor uw [verbindingsbibliotheek](sql-database-libraries.md).

### <a name="configure-firewall-rules"></a>Firewallregels configureren
U moet ervoor zorgen dat de firewallregels voor server en de database geconfigureerd overeenkomen met die die zijn geconfigureerd op de primaire server en de primaire database. Zie voor meer informatie [procedure: Firewall-instellingen configureren (Azure SQL Database)](sql-database-configure-firewall-settings.md).

### <a name="configure-logins-and-database-users"></a>Aanmeldingen en databasegebruikers configureren
U moet ervoor zorgen dat alle aanmeldingen gebruikt door de toepassing bestaat op de server die als host de herstelde database fungeert. Zie voor meer informatie [beveiligingsconfiguratie voor de geo-replicatie](sql-database-geo-replication-security-config.md).

> [!NOTE]
> U moet configureren en testen van de firewallregels voor server en aanmeldingen (en hun machtigingen) tijdens een herstel na noodgevallen detailanalyse. Deze objecten van het niveau van de server en de bijbehorende configuratie mogelijk niet beschikbaar tijdens de onderbreking.
> 
> 

### <a name="setup-telemetry-alerts"></a>Telemetrie-waarschuwingen instellen
Zo moet u ervoor dat de bestaande instellingen voor de waarschuwingsregel worden bijgewerkt als u wilt toewijzen aan de herstelde database en de andere server.

Zie voor meer informatie over database waarschuwingsregels [waarschuwing meldingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) en [bijhouden servicestatus](../monitoring-and-diagnostics/insights-service-health.md).

### <a name="enable-auditing"></a>Controle inschakelen
Als controle is vereist voor toegang tot uw database, moet u controleren na het databaseherstel van de inschakelen. Zie voor meer informatie [Databasecontrole](sql-database-auditing.md).

## <a name="next-steps"></a>Volgende stappen
* Voor meer informatie over Azure SQL Database geautomatiseerde back-ups, Zie [geautomatiseerde back-ups van SQL-Database](sql-database-automated-backups.md)
* Zie voor meer informatie over zakelijke continuïteit ontwerp- en herstelinstellingen scenario's [continuïteit scenario's](sql-database-business-continuity.md)
* Zie voor meer informatie over het gebruik van automatische back-ups voor herstel, [een database herstellen vanuit back-ups service is gestart](sql-database-recovery-using-backups.md)

