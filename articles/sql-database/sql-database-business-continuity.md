---
title: "bedrijfscontinuïteit aaaCloud - herstel van database - SQL-Database | Microsoft Docs"
description: "Ontdek hoe Azure SQL Database bedrijfscontinuïteit en databaseherstel met behulp van de cloud ondersteunt en u helpt om essentiële cloudtoepassingen ononderbroken uit te voeren."
keywords: "bedrijfscontinuïteit, bedrijfscontinuïteit met de cloud, databasenoodherstel, databaseherstel"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 18e5d3f1-bfe5-4089-b6fd-76988ab29822
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/15/2017
ms.author: sashan
ms.openlocfilehash: c9a6ff86fbbc04ce839a4fca79594b573b71644c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-business-continuity-with-azure-sql-database"></a>Overzicht van bedrijfscontinuïteit met Azure SQL Database

Dit overzicht beschrijft Hallo-mogelijkheden die Azure SQL Database voor bedrijfscontinuïteit en noodherstel biedt. Meer informatie over de opties, aanbevelingen en zelfstudies voor het herstellen van verstoren gebeurtenissen die kunnen leiden tot gegevensverlies van of ervoor zorgen dat uw database en de toepassing toobecome niet beschikbaar. Meer informatie over welke toodo wanneer een gebruiker of toepassing de fout is van invloed op de integriteit van gegevens, een Azure-regio een storing heeft of uw toepassing onderhoud vereist.

## <a name="sql-database-features-that-you-can-use-tooprovide-business-continuity"></a>SQL Database-functies waarmee u tooprovide zakelijke continuïteit kunt

SQL Database bevat verschillende functies voor bedrijfscontinuïteit, zoals geautomatiseerde back-ups en optionele databasereplicatie. Elke functie heeft verschillende kenmerken voor geschatte hersteltijd (ERT) en mogelijk gegevensverlies voor recente transacties. Wanneer u bekend bent met deze opties, kunt u eruit kiezen en ze in de meeste scenario's samen gebruiken voor verschillende doeleinden. Tijdens het ontwikkelen van uw bedrijfscontinuïteitsplan, moet u toounderstand Hallo maximale toegestane tijd Hallo toepassing volledig wordt hersteld na een onderbreking Hallo - dit is uw beoogde hersteltijd (RTO). U moet ook toounderstand maximale hoeveelheid recente gegevens updates (tijdsinterval) Hallo toepassing hello tolereert dat gegevens verloren gaan tijdens het herstellen na verstoren gebeurtenis Hallo - dit is uw herstelpuntdoel (RPO).

Hallo volgende tabel vergelijkt hello invoegen en RPO voor Hallo drie meest voorkomende scenario's.

| Mogelijkheid | Basislaag | Standaardlaag | Premiumlaag |
| --- | --- | --- | --- |
| Herstel naar een bepaald tijdstip vanuit back-up |Willekeurig herstelpunt binnen 7 dagen |Willekeurig herstelpunt binnen 35 dagen |Willekeurig herstelpunt binnen 35 dagen |
| Geo-herstel van back-ups geo-replicatie |ERT < 12 u, RPO < 1 u |ERT < 12 u, RPO < 1 u |ERT < 12 u, RPO < 1 u |
| Herstel vanuit Azure Backup Vault |ERT < 12 u, RPO < 1 wk |ERT < 12 u, RPO < 1 wk |ERT < 12 u, RPO < 1 wk |
| Actieve geo-replicatie |ERT < 30 s, RPO < 5 s |ERT < 30 s, RPO < 5 s |ERT < 30 s, RPO < 5 s |

### <a name="use-database-backups-toorecover-a-database"></a>Database-back-ups toorecover een database gebruiken

SQL-Database wordt automatisch uitgevoerd wekelijks een combinatie van volledige databaseback-ups, differentiële back-ups database per uur en transactie logboekback-ups om de vijf-tien minuten tooprotect van uw bedrijf verlies van gegevens. Deze back-ups worden opgeslagen in geografisch redundante opslag voor 35 dagen voor databases in Hallo Standard en Premium Servicelagen en 7 dagen voor databases in Hallo Basic servicelaag. Zie voor meer informatie [Servicelagen](sql-database-service-tiers.md). Als Hallo bewaarperiode voor de servicetier niet aan uw zakelijke vereisten voldoet, kunt u de bewaarperiode Hallo door verhogen [Hallo servicelaag wijzigen](sql-database-service-tiers.md). Hallo volledige en differentiële back-ups zijn ook gerepliceerde tooa [gekoppeld Datacenter](../best-practices-availability-paired-regions.md) ter bescherming tegen een datacentrum. Zie voor meer informatie [automatische databaseback-ups](sql-database-automated-backups.md).

Als de ingebouwde bewaarperiode Hallo niet voldoende is voor uw toepassing, kunt u deze kunt uitbreiden door het configureren van een bewaarbeleid uit de database op lange termijn. Zie voor meer informatie [lange bewaartermijn](sql-database-long-term-retention.md).

U kunt deze automatische databaseback-ups toorecover een database van verschillende verstoren gebeurtenissen, zowel binnen uw datacenter en tooanother Datacenter gebruiken. Met behulp van automatische databaseback-ups, Hallo geschatte herstel is afhankelijk van verschillende factoren, waaronder Hallo kunt u het totale aantal databases herstellen in Hallo dezelfde regio op Hallo dezelfde tijd, grootte van de database transactielogboekgrootte Hallo Hallo en de netwerkbandbreedte. Hallo hersteltijd is meestal minder dan 12 uur. Tijdens het herstellen van het gegevensgebied tooanother is mogelijk gegevensverlies Hallo beperkt too1 uur door Hallo geografisch redundante opslag van elk uur differentiële back-ups.

> [!IMPORTANT]
> met behulp van toorecover geautomatiseerde back-ups, moet u lid zijn van Hallo Inzender van SQL Server-rol of de eigenaar van het abonnement Hallo - Zie [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md). U kunt herstellen met behulp van hello Azure-portal, PowerShell of Hallo REST-API. U kunt Transact-SQL niet gebruiken.
>

Gebruik automatische back-ups als uw mechanisme voor bedrijfscontinuïteit en herstel als uw toepassing:

* Niet wordt beschouwd als bedrijfskritiek.
* Heeft een binding SLA - een uitvaltijd van 24 uur of langer niet resulteren in financiële verplichting.
* Heeft een lage wijzigingssnelheid gegevens (lage transacties per uur) en verlies van tooan uur van de wijziging wordt een acceptabele gegevensverlies.
* Kostengevoelig is.

Als u sneller herstel nodig hebt, gebruikt u [actieve geo-replicatie](sql-database-geo-replication-overview.md) (naast besproken). Als u toobe kunnen toorecover gegevens van een ouder zijn dan 35 dagen periode nodig hebt, gebruikt u [lange bewaartermijn van de back-](sql-database-long-term-retention.md). 

### <a name="use-active-geo-replication-and-auto-failover-groups-in-preview-tooreduce-recovery-time-and-limit-data-loss-associated-with-a-recovery"></a>Actieve geo-replicatie en automatische failover groepen (in preview) tooreduce herstel tijd- en limit verlies van gegevens die zijn gekoppeld aan een herstelbewerking gebruiken

Bovendien toousing databaseback-ups voor databases herstellen als er een onderbreking van de zakelijke optreedt, kunt u [actieve geo-replicatie](sql-database-geo-replication-overview.md) tooconfigure een database toohave van toofour leesbare secundaire databases in Hallo gebieden van uw keuze. Deze secundaire databases worden gesynchroniseerd met de primaire database Hallo met behulp van een mechanisme voor asynchrone replicatie. Deze functie is gebruikte tooprotect tegen business wordt onderbroken als een datacentrum optreedt of tijdens een upgrade van de toepassing. Actieve geo-replicatie kan ook worden gebruikt tooprovide betere prestaties van query's voor query's voor alleen-lezen toogeographically verdeeld over gebruikers.

tooenable automatisch en transparant failover moet u uw databases geogerepliceerde in indelen groepen met behulp van Hallo [automatische failover groep](sql-database-geo-replication-overview.md) functie van de SQL-Database (in preview).

Als de primaire database Hallo onverwacht offline gaat of u tootake moet offline voor onderhoudsactiviteiten, kunt u snel promoveren van een secundaire toobecome Hallo primaire (ook wel een failover) en toepassingen tooconnect toohello gepromoveerd primaire configureren. Als uw toepassing verbinding toohello-databases via de listener voor de failover hello maakt, hoeft u geen toochange Hallo SQL tekenreeks verbindingsconfiguratie na een failover. Met een geplande failover is er geen gegevensverlies. Met een niet-geplande failover, kan er een kleine hoeveelheid gegevensverlies voor zeer recent transacties vanwege toohello aard van asynchrone replicatie. Automatische failover-groepen (in preview) kunt u Hallo failover-beleid toominimize Hallo mogelijk gegevensverlies aanpassen. U kunt later failback na een failover - volgens tooa planning of wanneer Hallo datacentrum weer online wordt gezet. In alle gevallen moeten gebruikers ondervinden een kleine hoeveelheid uitvaltijd en tooreconnect nodig.

> [!IMPORTANT]
> toouse actieve geo-replicatie en automatische failover-groepen (in preview), moet u een abonnement eigenaar Hallo of hebt u beheerdersmachtigingen in SQL Server. U kunt configureren en een failover uitvoeren met behulp van hello Azure-portal, PowerShell of Hallo REST-API met behulp van Azure-abonnement machtigingen of met behulp van Transact-SQL met SQL Server-machtigingen.
> 

Gebruik van actieve geo-replicatie en automatische failover groepen (in preview) als uw toepassing voldoet aan een van deze criteria voldoen:

* Is bedrijfskritiek.
* Heeft een Service Level Agreement (SLA) op basis waarvan een uitvaltijd van 24 uur of langer niet is toegestaan.
* Uitvaltijd kan leiden tot financiële verplichting.
* Heeft een hoge frequentie van gegevenswijziging en een uur aan gegevensverlies is niet acceptabel.
* Hallo extra kosten van actieve geo-replicatie is lager dan Hallo potentiële financiële aansprakelijkheid en bijbehorende verlies van bedrijven.

>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-protecting-important-DBs-from-regional-disasters-is-easy/player]
>

## <a name="recover-a-database-after-a-user-or-application-error"></a>Een database herstellen na een gebruikers- of toepassingsfout
* Niemand is perfect! Een gebruiker kan mogelijk per ongeluk bepaalde gegevens verwijderen, per ongeluk een belangrijke tabel wissen of zelfs een volledige database verwijderen. Of een toepassing per ongeluk de onbeschadigde gegevens mogelijk overschreven met beschadigde gegevens vanwege tooan toepassing defect.

Dit zijn de opties voor herstel in dit scenario.

### <a name="perform-a-point-in-time-restore"></a>Herstel naar een bepaald tijdstip uitvoeren
U kunt Hallo automatische back-ups toorecover een kopie van uw database tooa bekende goede punt in tijd, mits tijd binnen de bewaarperiode Hallo-database ligt. Nadat het Hallo-database is hersteld, kunt u Hallo oorspronkelijke database niet vervangen met de database hersteld Hallo of Hallo nodig gegevens kopiëren van gegevens Hallo hersteld in de oorspronkelijke database Hallo. Als het Hallo-database maakt gebruik van actieve geo-replicatie, raden wij Hallo vereist gegevens kopiëren van Hallo hersteld kopiëren naar de oorspronkelijke database Hallo. Als u de oorspronkelijke database Hallo met de database hersteld Hallo vervangt, kunt u tooreconfigure moet en opnieuw synchroniseren van actieve geo-replicatie (dat kan lang duren voor een grote database).

Voor meer informatie en voor gedetailleerde stappen voor het herstellen van een database tooa punt in tijd hello Azure-portal of met behulp van PowerShell, raadpleegt u [punt in tijd terugzetten](sql-database-recovery-using-backups.md#point-in-time-restore). U kunt niet herstellen met behulp van Transact-SQL.

### <a name="restore-a-deleted-database"></a>Een verwijderde database herstellen
Als Hallo-database wordt verwijderd, maar Hallo logische server niet is verwijderd, kunt u herstellen Hallo verwijderd database toohello punt waarop deze is verwijderd. Een back-toohello database teruggezet dezelfde logische SQL-server van waaruit het is verwijderd. U kunt herstellen met behulp van de oorspronkelijke naam Hallo of geef een nieuwe naam of de database hersteld Hallo.

Voor meer informatie en voor gedetailleerde stappen voor het herstellen van een verwijderde database met behulp van hello Azure portal of met behulp van PowerShell, Zie [een verwijderde database terugzetten](sql-database-recovery-using-backups.md#deleted-database-restore). U kunt niet herstellen met behulp van Transact-SQL.

> [!IMPORTANT]
> Als de logische server hello wordt verwijderd, kunt u een verwijderde database niet herstellen.
>
>

### <a name="restore-from-azure-backup-vault"></a>Herstel vanuit Azure Backup Vault
Als Hallo-gegevensverlies buiten Hallo huidige bewaarperiode voor automatische back-ups opgetreden en uw database is geconfigureerd voor lange bewaartermijn, kunt u herstellen met een wekelijkse back-up in Azure Backup-kluis tooa nieuwe database. Op dit moment kunt u Hallo oorspronkelijke database niet vervangen met de database hersteld Hallo of Hallo nodig gegevens uit Hallo hersteld database kopiëren naar de oorspronkelijke database Hallo. Als u een oude versie van de upgrade van uw database voorafgaande tooa belangrijke toepassing tooretrieve moet, voldoen aan een aanvraag van auditors of een juridische volgorde, dat kunt u een database met behulp van een volledige back-up zijn opgeslagen in hello Azure Backup-kluis.  Zie [Langetermijnretentie](sql-database-long-term-retention.md) voor meer informatie.

## <a name="recover-a-database-tooanother-region-from-an-azure-regional-data-center-outage"></a>Een regio tooanother herstellen van een storing van Azure regionale data center
<!-- Explain this scenario -->

Hoewel zeldzaam, kan er een storing optreden in een Azure-datacenter. Wanneer er een storing optreedt, veroorzaakt deze een bedrijfsonderbreking die mogelijk slechts een paar minuten maar ook enkele uren kan duren.

* Een mogelijkheid is toowait voor uw database toocome weer online wanneer Hallo datacentrum over. Dit werkt voor toepassingen die betaalbare toohave Hallo database offline. Bijvoorbeeld, een project voor de ontwikkeling of gratis proefversie u hoeft niet toowork op voortdurend. Wanneer een datacenter een storing heeft, weet u niet hoe lang Hallo storing kan duren, zodat u deze optie werkt alleen als u uw database voor een tijdje niet nodig.
* Een andere optie is tooeither mislukken via tooanother gegevensgebied als u van actieve geo-replicatie gebruikmaakt of Hallo een database herstelt via geografisch redundante back-ups (geo-herstel). Failover duurt slechts enkele seconden tijdens het databaseherstel vanuit back-ups uur duurt.

Wanneer u actie onderneemt, hoe lang het duurt u toorecover en hoeveel verlies van gegevens die worden er rekening is afhankelijk van hoe u toouse bepaalt deze zakelijke continuïteit-functies in uw toepassing. Inderdaad, kunt u toouse een combinatie van databaseback-ups en actieve geo-replicatie al naar gelang de toepassingsvereisten van uw. Zie [Een toepassing ontwerpen voor noodherstel via de cloud](sql-database-designing-cloud-solutions-for-disaster-recovery.md) en [Strategieën voor noodherstel voor elastische groepen](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md) voor een bespreking van overwegingen voor het ontwerp van toepassingen voor zelfstandige databases en voor elastische pools met behulp van deze functies voor bedrijfscontinuïteit.

Hallo bevatten volgende secties een overzicht van Hallo stappen toorecover met behulp van de databaseback-ups of actieve geo-replicatie. Zie voor gedetailleerde stappen inclusief het plannen van vereisten, herstelstappen post en informatie over hoe toosimulate een storing tooperform een herstel na noodgevallen inzoomen [een SQL-Database herstellen van een storing](sql-database-disaster-recovery.md).

### <a name="prepare-for-an-outage"></a>Voorbereiden op een storing
Ongeacht Hallo zakelijke continuïteit functie waarmee u, moet u het volgende doen:

* Het identificeren en Hallo-doelserver, zoals firewallregels op serverniveau, aanmeldingen en machtigingen op het niveau hoofddatabase voorbereiden.
* Bepalen hoe tooredirect clients en client toepassingen toohello nieuwe server
* Andere afhankelijkheden documenteren, zoals controle-instellingen en waarschuwingen.

Als u niet bereid juist brengen van uw toepassingen online na een failover of een databaseherstel meer tijd kost en waarschijnlijk ook problemen moet oplossen op een tijdstip van stress - een ongeldige combinatie.

### <a name="fail-over-tooa-geo-replicated-secondary-database"></a>Failover tooa geo-replicatie secundaire database
Als u van actieve geo-replicatie en automatische failover-groepen (in preview) als uw herstelfunctie gebruikmaakt, kunt u beleid voor automatische failover configureren of gebruiken [handmatige failover](sql-database-disaster-recovery.md#fail-over-to-geo-replicated-secondary-database). Eenmaal is gestart, worden de Hallo failover oorzaken Hallo secundaire toobecome Hallo nieuwe primaire en gereed toorecord nieuwe transacties en reageren tooqueries - met minimaal gegevensverlies voor Hallo gegevens nog niet gerepliceerd. Zie voor meer informatie over het ontwerpen van Hallo failoverproces [ontwerpen van een toepassing voor noodherstel voor cloud](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

> [!NOTE]
> Hallo Datacenter weer online wordt gezet Hallo oude primaire automatisch opnieuw verbinding toohello nieuwe primaire als secundaire databases worden. Als u toorelocate Hallo primaire back toohello oorspronkelijke regio nodig hebt, kunt u een geplande failover handmatig starten (failback). 
> 

### <a name="perform-a-geo-restore"></a>Een geo-herstel uitvoeren
Als u automatische back-ups met replicatie geografisch redundante opslag als uw herstelfunctie [starten van een database-herstelbewerking met geo-restore](sql-database-disaster-recovery.md#recover-using-geo-restore). Herstel vindt doorgaans plaats binnen 12 uur - laatste met gegevensverlies van up tooone uur bepaald door de wanneer hello per uur differentiële back-up met genomen en gerepliceerde. Totdat Hallo herstel is voltooid, Hallo of database is toorecord transacties reageren tooany query's. Terwijl dit wordt hersteld op een database toohello laatste punt in tijd, is terugzetten Hallo geo-secundaire tooany punt in tijd momenteel niet ondersteund.

> [!NOTE]
> Als het datacentrum Hallo weer online wordt gezet voordat u uw toepassing via de herstelde database toohello activeert, kunt u Hallo herstel annuleren.  
>
>

### <a name="perform-post-failover--recovery-tasks"></a>Taken na failover/hersteltaken uitvoeren
Na het herstel van een mechanisme voor herstel, moet u uitvoeren Hallo aanvullende taken te volgen voordat uw gebruikers en toepassingen back-up worden en wordt uitgevoerd:

* Omleiden van clients en de client toepassingen toohello nieuwe server en de herstelde database
* Zorg ervoor dat de juiste serverniveau firewallregels zijn voor gebruikers tooconnect (of gebruik [databaseniveau firewalls](sql-database-firewall-configure.md#creating-and-managing-firewall-rules))
* Ervoor zorgen dat er geschikte aanmeldingen en machtigingen op hoofddatabaseniveau aanwezig zijn (of [ingesloten gebruikers](https://msdn.microsoft.com/library/ff929188.aspx) gebruiken)
* Controles configureren, indien van toepassing
* Waarschuwingen configureren, indien van toepassing

## <a name="upgrade-an-application-with-minimal-downtime"></a>Een toepassing upgraden met minimale uitvaltijd
Soms moet een toepassing worden gehouden offline vanwege gepland onderhoud, zoals een upgrade van de toepassing. [Beheren van toepassingsupgrades](sql-database-manage-application-rolling-upgrade.md) wordt beschreven hoe toouse actieve geo-replicatie tooenable rolling upgrades van uw cloud toepassing toominimize uitvaltijd tijdens de upgrade en bieden een herstelpad als er iets mis gaat. 

## <a name="next-steps"></a>Volgende stappen
Zie [Een toepassing ontwerpen voor noodherstel via de cloud](sql-database-designing-cloud-solutions-for-disaster-recovery.md) en [Strategieën voor noodherstel voor elastische pools](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md) voor een bespreking van overwegingen voor het ontwerp van toepassingen voor zelfstandige databases en voor elastische groepen.
