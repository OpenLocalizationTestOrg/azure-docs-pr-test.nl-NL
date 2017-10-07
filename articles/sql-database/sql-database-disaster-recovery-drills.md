---
title: aaaSQL Database Noodhersteloefeningen | Microsoft Docs
description: Informatie over richtlijnen en aanbevolen procedures voor het gebruik van Azure SQL Database tooperform disaster recovery zoomt toohelp Houd uw missie bedrijfskritieke toepassingen robuuste toofailures en storingen.
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a>Disaster Recovery inzoomen uitvoeren
Het is raadzaam dat validatie van de gereedheid van de toepassing voor herstelwerkstroom regelmatig wordt uitgevoerd. Gedrag van de toepassing controleren Hallo en implicaties van gegevens verloren gaan en/of Hallo onderbreking moet u dat de failover is een goede gewoonte engineering. Het is ook een vereiste door de meeste industrienormen als onderdeel van zakelijke continuïteit-certificering.

Uitvoeren van een herstel na noodgevallen detailanalyse bestaat uit:

* Onderbreking van de laag Simulating gegevens
* Herstellen
* Toepassingsherstel integriteit post valideren

Afhankelijk van hoe u [ontworpen van uw toepassing voor bedrijfscontinuïteit](sql-database-business-continuity.md), Hallo werkstroom tooexecute Hallo inzoomen kan variëren. Hieronder worden beschreven Hallo aanbevolen procedures voor het uitvoeren van een detailanalyse van het herstel na noodgevallen in de context Hallo van Azure SQL Database.

## <a name="geo-restore"></a>Geo-herstel
tooprevent Hallo mogelijk gegevensverlies bij het uitvoeren van een herstel na noodgevallen detailanalyse, wordt aangeraden uitvoeren Hallo inzoomen met behulp van een testomgeving door een kopie van de productieomgeving Hallo maken en deze werkstroom tooverify Hallo van de toepassing.

#### <a name="outage-simulation"></a>Storing simulatie
toosimulate Hallo onderbreking, kunt u verwijderen of wijzig de naam van de brondatabase Hallo. Dit zorgt ervoor dat de problemen met de toepassingen.

#### <a name="recovery"></a>Herstel
* Hallo geo-herstel van database Hallo uitvoeren in een andere server, zoals wordt beschreven [hier](sql-database-disaster-recovery.md).
* Wijziging Hallo toepassing configuratie tooconnect toohello herstelde database en volg Hallo [na het herstel van een database te configureren](sql-database-disaster-recovery.md) toocomplete Hallo herstel leiden.

#### <a name="validation"></a>Validatie
* Volledige Hallo inzoomen door Hallo integriteit post toepassingsherstel (inclusief verbindingsreeksen, aanmeldingen, testen van de basisfunctionaliteit of andere onderdeel validaties van standaardtoepassing ondertekeningen procedures) te verifiëren.

## <a name="geo-replication"></a>Geo-replicatie
Voor een database die is beveiligd met geo-replicatie Hallo inzoomen omvat oefening geplande failover toohello secundaire database. Hallo geplande failover zorgt ervoor dat Hallo primaire en secundaire databases Hallo synchroon blijven wanneer Hallo rollen worden omgeschakeld. In tegenstelling tot Hallo van niet-geplande failover, deze bewerking niet resulteren in verlies van gegevens, zodat Hallo inzoomen kan worden uitgevoerd in de productieomgeving Hallo.

#### <a name="outage-simulation"></a>Storing simulatie
toosimulate hello onderbreking, kunt u Hallo-webtoepassing of virtuele machine verbonden toohello database uitschakelen. Dit resulteert in Hallo verbindingsfouten voor Hallo webserver en webclients.

#### <a name="recovery"></a>Herstel
* Configuratie van de toepassing of Hallo maken in Hallo DR regio punten toohello voormalige secundaire hello wordt volledig toegankelijk nieuwe primaire.
* Voer [geplande failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake Hallo secundaire database een nieuwe primaire
* Ga als volgt Hallo [na het herstel van een database te configureren](sql-database-disaster-recovery.md) toocomplete Hallo herstel leiden.

#### <a name="validation"></a>Validatie
* Volledige Hallo inzoomen door Hallo integriteit post toepassingsherstel (inclusief verbindingsreeksen, aanmeldingen, testen van de basisfunctionaliteit of andere onderdeel validaties van standaardtoepassing ondertekeningen procedures) te verifiëren.

## <a name="next-steps"></a>Volgende stappen
* toolearn over zakelijke continuïteit scenario's, Zie [continuïteit scenario's](sql-database-business-continuity.md)
* toolearn over Azure SQL Database automatische back-ups, Zie [geautomatiseerde back-ups van SQL-Database](sql-database-automated-backups.md)
* toolearn over het gebruik van automatische back-ups voor herstel, Zie [een database terugzetten vanuit Hallo service geïnitieerde back-ups](sql-database-recovery-using-backups.md)
* Zie toolearn over opties voor sneller herstel [actieve geo-replicatie](sql-database-geo-replication-overview.md)  
