---
title: een Azure SQL database in een multitenant-app aaaRestore | Microsoft Docs
description: "Meer informatie over hoe toorestore één tenants SQL database na het per ongeluk verwijderen van gegevens"
keywords: zelfstudie sql-database
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: billgib;sstein
ms.openlocfilehash: 8507ecec2424c135f1859b88ebf2bb4e17538a58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-wingtip-saas-tenants-sql-database"></a>Een Wingtip SaaS tenants SQL-database herstellen

Hallo Wingtip SaaS app gebouwd met behulp van een database per tenant-model, waarbij elke tenant hun eigen database heeft. Een van de voordelen Hallo van dit model is dat deze is eenvoudig toorestore één tenant gegevens in isolatie zonder enige impact op andere tenants.

In deze zelfstudie leert u twee data recovery patronen:

> [!div class="checklist"]

> * Een database herstellen naar een parallelle database (side-by-side)
> * Een database in place herstellen


|||
|:--|:--|
| **Tenant tooa voorafgaande punt in tijd, in een parallelle database herstellen** | Dit patroon kan worden gebruikt door Hallo tenant voor controle, controle en naleving, enz. Hallo oorspronkelijke database online en ongewijzigd blijft. |
| **Tenant in-place herstellen** | Dit patroon is gewoonlijk gebruikte toorecover een tenant tooa voorafgaande punt in tijd, nadat de gegevens in een tenant per ongeluk worden verwijderd. Hallo oorspronkelijke database wordt offline gezet en vervangen door de herstelde database Hallo. |
|||

toocomplete in deze zelfstudie, zorg ervoor dat Hallo volgende vereisten zijn voltooid:

* Hallo Wingtip SaaS-app wordt geïmplementeerd. Zie toodeploy in minder dan vijf minuten [implementeren en verkennen Hallo Wingtip SaaS-toepassing](sql-database-saas-tutorial.md)
* Azure PowerShell is geïnstalleerd. Zie [Aan de slag met Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps) voor meer informatie.

## <a name="introduction-toohello-saas-tenant-restore-pattern"></a>Inleiding toohello SaaS tenant terugzetten patroon

Voor de tenant Hallo herstellen patroon, zijn er twee eenvoudige patronen voor het herstellen van gegevens van een afzonderlijke tenant. Omdat de tenant-databases zijn geïsoleerd van elkaar, heeft herstellen van een tenant geen invloed op een andere tenant-gegevens.

Gegevens worden teruggezet in de eerste patroon hello, in een nieuwe database. Hallo tenant krijgt vervolgens toegang toothis database naast hun productiegegevens. Dit patroon toestaat dat een tenant admin tooreview Hallo hersteld gegevens en wordt mogelijk gebruikt tooselectively huidige gegevenswaarden overschrijven. Is toohello SaaS app designer toodetermine hoe geavanceerde hello gegevensherstel opties moeten zijn. Eenvoudig gegevens kunnen tooreview Hallo status in op een bepaald tijdstip was wordt mogelijk alle die vereist is in sommige scenario's. Als het Hallo-database maakt gebruik van [geo-replicatie](sql-database-geo-replication-overview.md), het is raadzaam Hallo vereist gegevens kopiëren van Hallo hersteld kopiëren naar de oorspronkelijke database Hallo. Als u de oorspronkelijke database Hallo met de database hersteld Hallo vervangt, kunt u tooreconfigure moet en geo-replicatie opnieuw synchroniseren.

In de tweede patroon hello, waarbij ervan wordt uitgegaan dat Hallo tenant heeft gehad een verlies of beschadiging van gegevens, productiedatabase Hallo-tenant is teruggezet tooa voorafgaande punt in tijd. In de Hallo herstellen in place patroon, wordt Hallo tenant offline gezet gedurende een korte periode tijdens het Hallo-database is hersteld en weer online. Hallo oorspronkelijke database wordt verwijderd, maar kan nog steeds worden hersteld vanuit als u back tooan toogo moet zelfs eerdere punt in tijd. Hallo-database in plaats van te verwijderen, kan wijzigen in een variant van dit patroon naamswijzigingen Hallo database biedt geen extra voordelen in termen van de beveiliging van gegevens.

## <a name="get-hello-wingtip-application-scripts"></a>Hallo Wingtip toepassingsscripts ophalen

Hallo Wingtip SaaS-scripts en broncode van toepassing zijn beschikbaar in Hallo [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github-opslagplaats. [Stappen toodownload Hallo Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="simulate-a-tenant-accidentally-deleting-data"></a>Simuleren van een tenant per ongeluk verwijderen van gegevens

toodemonstrate deze herstelscenario's, moeten we te*per ongeluk* sommige gegevens in een van Hallo tenant databases verwijderen. Terwijl u elke record verwijderen kunt, ophalen door referentiële integriteit schendingen Hallo volgende stap ingesteld Hallo demo toonot geblokkeerd! Ook worden sommige ticket inkoopgegevens kunt u later in Hallo *Wingtip SaaS Analytics zelfstudies*.

Hallo ticket generator script uitvoeren en aanvullende gegevens te maken. Hallo ticket generator komt opzettelijk niet kopen van tickets voor elke laatste gebeurtenis van tenants.

1. Open... \\Learning-Modules\\hulpprogramma's\\*Demo TicketGenerator.ps1* in Hallo *PowerShell ISE*
1. Druk op **F5** toorun Hallo script en genereren van klanten en verkoopgegevens ticket.


### <a name="open-hello-events-app-tooreview-hello-current-events"></a>Hallo gebeurtenissen app tooreview Hallo huidige gebeurtenissen openen

1. Open Hallo *gebeurtenissen Hub* (http://events.wtp.&lt; gebruiker&gt;. trafficmanager.net) en klik op **Contoso overleg Hall**:

   ![events hub](media/sql-database-saas-tutorial-restore-single-tenant/events-hub.png)

1. Blader Hallo lijst met gebeurtenissen en noteer de laatste gebeurtenis Hallo in Hallo lijst:

   ![laatste gebeurtenis](media/sql-database-saas-tutorial-restore-single-tenant/last-event.png)


### <a name="run-hello-demo-scenario-tooaccidentally-delete-hello-last-event"></a>Hallo demo scenario tooaccidentally Hallo laatste verwijderingsgebeurtenis uitvoeren

1. Open... \\Learning-Modules\\voor bedrijfscontinuïteit en noodherstel\\RestoreTenant\\*Demo RestoreTenant.ps1* in Hallo *PowerShell ISE*, en set Hallo waarde te volgen:
   * **$DemoScenario** = **1**stelt te**1** -gebeurtenissen met geen verkopen ticket verwijderen.
1. Druk op **F5** toorun Hallo script en verwijderen van de laatste gebeurtenis Hallo. U ziet een bevestiging bericht vergelijkbaar toohello volgende:

   ```Console
   Deleting unsold events from Contoso Concert Hall ...
   Deleted event 'Seriously Strauss' from Contoso Concert Hall venue.
   ```

1. Hallo Contoso gebeurtenissen pagina wordt geopend. Schuif naar beneden en controleer of het Hallo-gebeurtenis is verwijderd. Als Hallo gebeurtenis nog steeds in de lijst hello wordt, klikt u op vernieuwen en controleer of dat het is verwijderd.

   ![laatste gebeurtenis](media/sql-database-saas-tutorial-restore-single-tenant/last-event-deleted.png)


## <a name="restore-a-tenant-database-in-parallel-with-hello-production-database"></a>Een tenant-database in combinatie met de productiedatabase Hallo herstellen

In deze oefening herstelt Hallo Contoso overleg Hall database tooa punt in tijd voordat het Hallo-gebeurtenis is verwijderd. Nadat Hallo-gebeurtenis in de vorige stappen Hallo is verwijderd, kunt u toorecover wilt en Hallo verwijderde gegevens zien. U hoeft niet toorestore uw productiedatabase met Hallo verwijderde record, maar u toorecover Hallo oude database tooaccess Hallo oude gegevens nodig voor andere zakelijke redenen.

 Hallo *terugzetten TenantInParallel.ps1* script maakt een parallelle tenant-database en een parallelle catalogusvermelding beide met de naam *ContosoConcertHall\_oude*. Dit patroon van terugzetten is het meest geschikt is voor het herstellen van een secundaire gegevensverlies of voor compatibiliteit en controle herstelscenario's. Het is ook aanbevolen benadering wanneer u Hallo [geo-replicatie](sql-database-geo-replication-overview.md).

1. Volledige Hallo [simuleren van een gebruiker per ongeluk verwijderen van gegevens](#simulate-a-tenant-accidentally-deleting-data) sectie.
1. Open... \\Learning-Modules\\voor bedrijfscontinuïteit en noodherstel\\RestoreTenant\\_Demo RestoreTenant.ps1_ in Hallo *PowerShell ISE*.
1. Stel **$DemoScenario** = **2**, stel deze optie te**2** te*terugzetten tenant parallel*.
1. Druk op **F5** toorun Hallo script.

Hallo script herstelt Hallo tenant-database (tooa parallelle database) tooa punt in tijd voordat u Hallo-gebeurtenis in de vorige sectie Hallo verwijderd. Deze maakt een tweede database, verwijdert u alle bestaande catalogus metagegevens die voorkomt in deze database en voegt Hallo database toohello catalogus onder Hallo *ContosoConcertHall\_oude* vermelding.

Hallo demoscript opent Hallo gebeurtenissen pagina in uw browser. Opmerking van Hallo URL: ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` gegevens uit de database hersteld Hallo zien waar *_old* toohello-naam is toegevoegd.

Scroll Hallo gebeurtenissen in Hallo browser tooconfirm die gebeurtenis verwijderd in de vorige sectie Hallo Hallo is hersteld.

Houd er rekening mee dat exposing Hallo hersteld tenant als een extra tenant, met een eigen gebeurtenissen app toobrowse-tickets onwaarschijnlijk toobe hoe u een tenant toegang tot toorestored gegevens, maar fungeert tooeasily illustreren Hallo terugzetten patroon wilt bieden.

In werkelijkheid, zou u waarschijnlijk alleen deze herstelde database behouden voor een opgegeven periode. U kunt Hallo hersteld tenant vermelding verwijderen zodra u klaar bent met aanroepen Hallo *verwijderen RestoredTenant.ps1* script.

1. Stel **$DemoScenario** te**4** tooselect hello *verwijderen hersteld tenant* scenario.
1. **Uitvoeren van** **met** **F5**
1. Hallo *ContosoConcertHall\_oude* vermelding is nu verwijderd uit de catalogus Hallo. Opwekken en Hallo gebeurtenissen pagina voor deze tenant in uw browser te sluiten.


## <a name="restore-a-tenant-in-place-replacing-hello-existing-tenant-database"></a>Een tenant aanwezig is, vervangt Hallo bestaande tenant-database herstellen

In deze oefening herstelt Hallo Contoso overleg Hall tenant tooa punt in tijd voordat het Hallo-gebeurtenis is verwijderd. Hallo *terugzetten TenantInPlace* script herstelt Hallo huidige tenant database tooa nieuwe database wijzen tooa vorige punt in tijd en verwijderingen Hallo oorspronkelijke database. Dit patroon van terugzetten is het meest geschikt voor het herstellen van ernstige gegevensbeschadiging omdat er mogelijk belangrijke gegevens verloren gaan die tenant Hallo tooaccommodate zou hebben.

1. Open **Demo RestoreTenant.ps1** bestand in PowerShell ISE
1. Stel **$DemoScenario** te**5** tooselect hello *tenant in place scenario herstellen*.
1. Uitvoeren met behulp van **F5**.

Hallo script herstelt Hallo tenant database tooa punt vijf minuten voordat het Hallo-gebeurtenis is verwijderd. Dit wordt uitgevoerd door de eerste duurt Hallo Contoso overleg Hall tenant offline zodat er geen verdere toohello gegevens bijgewerkt. Vervolgens een parallelle database is gemaakt door te herstellen vanaf herstelpunt Hallo en de naam met een tijdstempel tooensure Hallo databasenaam niet in strijd met bestaande tenant Hallo-databasenaam. Vervolgens Hallo oude tenant-database wordt verwijderd en de herstelde database Hallo hernoemde toohello oorspronkelijke databasenaam is. Ten slotte brengen Contoso overleg Hall online tooallow Hallo app access toohello hersteld-database.

U hersteld Hallo database tooa punt in tijd voordat het Hallo-gebeurtenis is verwijderd. Hallo gebeurtenissen wordt geopend, dus controleer Hallo laatste gebeurtenis is hersteld.


## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]

> * Een database herstellen naar een parallelle database (side-by-side)
> * Een database in place herstellen

[Tenant-databaseschema beheren](sql-database-saas-tutorial-schema-management.md)

## <a name="additional-resources"></a>Aanvullende bronnen

* Aanvullende [zelfstudies waarin voort op Hallo Wingtip SaaS-toepassing bouwen](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Overzicht van zakelijke continuïteit met Azure SQL Database](sql-database-business-continuity.md)
* [Meer informatie over back-ups van SQL-Database](sql-database-automated-backups.md)
