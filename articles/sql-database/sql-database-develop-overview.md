---
title: aaaSQL Database ontwikkelen-overzicht | Microsoft Docs
description: Meer informatie over beschikbare verbinding bibliotheken en best practices voor toepassingen tooSQL Database verbinding te maken.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: genemi
ms.assetid: 67c02204-d1bd-4622-acce-92115a7cde03
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: 17f04db600828f90c42c750c9abdb92cfa4ca817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-application-development-overview"></a>SQL-Database ontwikkelen-overzicht
In dit artikel wordt uitgelegd Hallo basic overwegingen die een ontwikkelaar houden moet rekening bij het schrijven van code tooconnect tooAzure SQL-Database.

> [!TIP]
> Verbinding voor een zelfstudie waarin u hoe toocreate een server, een firewall op de server, server-eigenschappen weergeven, maken verbinding maken met behulp van de query Hallo hoofddatabase van SQL Server Management Studio, een voorbeelddatabase en een lege database maken, query uitvoeren op database-eigenschappen SQL Server Management Studio en query Hallo-voorbeelddatabase gebruikt, Zie [ophalen zelfstudie](sql-database-get-started-portal.md).
>

## <a name="language-and-platform"></a>Taal en platform
Er zijn codevoorbeelden beschikbaar voor verschillende programmeertalen en platforms. Hier vindt u koppelingen toohello codevoorbeelden op: 

* Meer informatie: [Verbindingsbibliotheken voor SQL Database en SQL Server](sql-database-libraries.md)

## <a name="tools"></a>Hulpprogramma's 
U kunt gebruikmaken van open-source-hulpprogramma's zoals [cheetah](https://github.com/wunderlist/cheetah), [sql cli](https://www.npmjs.com/package/sql-cli) of [VS Code](https://code.visualstudio.com/). Daarnaast werkt Azure SQL Database met Microsoft-hulpprogramma's zoals [Visual Studio](https://www.visualstudio.com/downloads/) en [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).  U kunt ook hello Azure Management Portal, PowerShell en REST-API's kunt u extra productiviteit krijgen.

## <a name="resource-limitations"></a>Resourcebeperkingen
Azure SQL Database beheert Hallo resources beschikbaar tooa database met behulp van twee verschillende mechanismen: Resources beheer en afdwinging van limieten.

* Meer informatie: [Azure SQL Database-resourcebeperkingen](sql-database-resource-limits.md)

## <a name="security"></a>Beveiliging
Azure SQL Database biedt resources voor het beperken van toegang, het beveiligen van gegevens en het bewaken van activiteiten in een SQL Database.

* Meer informatie: [Uw SQL Database beveiligen](sql-database-security-overview.md)

## <a name="authentication"></a>Authentication
* Azure SQL Database biedt ondersteuning voor zowel SQL Server-verificatiegebruikers en -aanmeldingen als [Azure Active Directory](sql-database-aad-authentication.md)-verificatiegebruikers en -aanmeldingen.
* U moet een bepaalde database, in plaats van Standaardinstellingenbeleid toohello toospecify *master* database.
* U kunt geen Hallo Transact-SQL gebruiken **gebruik myDatabaseName;** instructie op SQL-Database tooswitch tooanother database.
* Meer informatie: [SQL Database-beveiliging: databasetoegang en aanmeldingsbeveiliging beheren](sql-database-manage-logins.md)

## <a name="resiliency"></a>Flexibiliteit
Wanneer een tijdelijke fout optreedt tijdens het verbinden van tooSQL Database, moet uw code Hallo-aanroep in opnieuw proberen.  U wordt aangeraden dat Pogingslogica backoff logica te gebruiken, zodat deze niet wordt overbelast Hallo SQL-Database met meerdere clients tegelijkertijd opnieuw uit te voeren.

* Codevoorbeelden: codevoorbeelden die aangeven Pogingslogica, vindt u voorbeelden voor de taal van uw keuze op Hallo: [verbindingsbibliotheken voor SQL-Database en SQL Server](sql-database-libraries.md)
* Meer informatie: [Foutberichten voor SQL Database-clientprogramma’s](sql-database-develop-error-messages.md)

## <a name="managing-connections"></a>Verbindingen beheren
* In de logica van uw client-verbinding overschrijven Hallo standaard time-out toobe 30 seconden.  Hallo standaardwaarde van 15 seconden is te kort voor verbindingen die afhankelijk van zijn internet Hallo.
* Als u een [verbindingsgroep](http://msdn.microsoft.com/library/8xx3tyca.aspx), kunnen ervoor tooclose Hallo verbinding Hallo instant uw programma is niet actief gebruikt en niet tooreuse bereidt het.

## <a name="network-considerations"></a>Aandachtspunten voor netwerken
* Controleer op Hallo-computer die als host fungeert voor uw clientprogramma, Hallo firewall staat uitgaande TCP-communicatie op poort 1433.  Meer informatie: [Een Azure SQL Database-firewall configureren](sql-database-configure-firewall-settings.md)
* Als uw clientprogramma verbinding tooSQL Database maakt, terwijl de client wordt uitgevoerd op Azure een virtuele machine (VM), moet u bepaalde poortbereiken op Hallo VM openen. Meer informatie: [poorten buiten 1433 voor ADO.NET 4.5 en SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md)
* Client verbindingen tooAzure SQL-Database soms Hallo proxy omzeilen en rechtstreeks communiceren met de Hallo-database. Andere poorten dan poort 1433 worden belangrijk. Voor meer informatie [Azure SQL Database connectivity architectuur](sql-database-connectivity-architecture.md) en [poorten buiten 1433 voor ADO.NET 4.5 en SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="data-sharding-with-elastic-scale"></a>Gegevens sharding met elastisch schalen
Elastisch schalen vereenvoudigt Hallo schalen (en). 

* [Ontwerppatronen voor SaaS-toepassingen met meerdere tenants met behulp van Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md)
* [Aan de slag met het voorbeeld voor elastisch schalen voor Azure SQL Database](sql-database-elastic-scale-get-started.md)

## <a name="next-steps"></a>Volgende stappen
Alle Hallo verkennen [mogelijkheden van SQL-Database](sql-database-technical-overview.md)
