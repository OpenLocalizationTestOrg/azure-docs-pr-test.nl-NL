---
title: aaaManage Azure SQL Database-schema in een multitenant-app | Microsoft Docs
description: Het schema voor meerdere tenants beheren in een toepassing met meerdere tenants die gebruikmaakt van Azure SQL Database
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
ms.date: 07/28/2017
ms.author: billgib; sstein
ms.openlocfilehash: ea946e556808dabd60dd39cb8173d0512d4bddec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-schema-for-multiple-tenants-in-hello-wingtip-saas-application"></a>Schema voor meerdere tenants in Wingtip SaaS-toepassing hello beheren

Hallo [eerste Wingtip SaaS-zelfstudie](sql-database-saas-tutorial.md) ziet u hoe Hallo app kunt inrichten van een tenant-database en deze te registreren in het Hallo-catalogus. Net als elke toepassing vereist hello Wingtip SaaS-app wordt aangepast, gedurende een bepaalde periode, en soms wijzigingen toohello database. Wijzigingen mogelijk zijn nieuwe of gewijzigde schema, nieuwe of gewijzigde referentiegegevens en routinematig onderhoud taken tooensure optimale app databaseprestaties. Met een SaaS-toepassing moeten deze wijzigingen toobe op gecoördineerde wijze wordt geïmplementeerd op een potentieel grote wagenpark van tenant-databases. Voor deze toobe wijzigingen in de toekomst tenant databases, moeten deze toobe opgenomen in het inrichtingsproces Hallo.

Deze zelfstudie behandelt de twee scenario's - verwijzing Gegevensupdates implementeren voor alle tenants en een index op Hallo retuning tabel met Hallo referentiegegevens. Hallo [elastische taken](sql-database-elastic-jobs-overview.md) functie gebruikte tooexecute deze bewerkingen wordt voor alle tenants en Hallo *gouden* tenant-database die wordt gebruikt als een sjabloon voor nieuwe databases.

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]

> * De account van een taak maken
> * Vragen over meerdere tenants
> * Gegevens in alle tenantdatabases bijwerken
> * Een index in een tabel maken in alle tenantdatabases


toocomplete in deze zelfstudie, zorg ervoor dat Hallo volgende vereisten wordt voldaan:

* Hallo Wingtip SaaS-app wordt geïmplementeerd. Zie toodeploy in minder dan vijf minuten [implementeren en verkennen Hallo Wingtip SaaS-toepassing](sql-database-saas-tutorial.md)
* Azure PowerShell is geïnstalleerd. Zie [Aan de slag met Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps) voor meer informatie.
* Hallo meest recente versie van SQL Server Management Studio (SSMS) is geïnstalleerd. [SSMS downloaden en installeren](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

*Deze zelfstudie maakt gebruik van functies van Hallo SQL Database-service die zich in een beperkte preview (elastische Database taken). Als u wenst dat toodo in deze zelfstudie, geeft u uw abonnements-id tooSaaSFeedback@microsoft.com met de onderwerpnaam = elastische taken Preview. Nadat u een bevestiging dat uw abonnement is ingeschakeld, ontvangt [downloaden en installeren van de meest recente voorlopige versie taken-cmdlets Hallo](https://github.com/jaredmoo/azure-powershell/releases). Dit voorbeeld is beperkt, dus neem contact op met SaaSFeedback@microsoft.com voor vragen over of ondersteuning.*


## <a name="introduction-toosaas-schema-management-patterns"></a>Inleiding tooSaaS patronen Schemabeheer

Hallo één tenant per database SaaS patroon voordelen van tal van manieren Hallo gegevensisolatie die het resultaat, maar op Hallo introduceert hetzelfde moment Hallo extra complexiteit van het onderhouden en beheren van veel databases. [Elastische taken](sql-database-elastic-jobs-overview.md) vereenvoudigt het beheer en het beheer van Hallo SQL gegevenslaag. Taken helpen u toosecurely en betrouwbaar, onafhankelijk van de gebruikersinteractie of invoer, taken (T-SQL-scripts) uitvoeren op een groep met databases. Deze methode kan gebruikte toodeploy schema en de wijzigingen in algemene verwijzingen zijn in alle tenants in een toepassing. Elastische taken kunnen ook worden gebruikt toomaintain een *gouden* exemplaar van database Hallo toocreate nieuwe tenants, heeft altijd de meest recente schema's en verwijzingen gegevens Hallo gezorgd gebruikt.

![scherm](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a>Beperkte preview voor Elastische taken

Er is een nieuwe versie beschikbaar van Elastische taken; dit is nu een ingebouwde functie in Azure SQL Database (waarvoor geen extra services of onderdelen zijn vereist). Van deze nieuwe versie van Elastische taken is momenteel een beperkte preview beschikbaar. Deze beperkte preview biedt ondersteuning voor PowerShell toocreate taakaccounts en T-SQL-toocreate momenteel en beheren van taken.

> [!NOTE]
> *Deze zelfstudie maakt gebruik van functies van Hallo SQL Database-service die zich in een beperkte preview (elastische Database taken). Als u wenst dat toodo in deze zelfstudie, geeft u uw abonnements-id tooSaaSFeedback@microsoft.com met de onderwerpnaam = elastische taken Preview. Nadat u een bevestiging dat uw abonnement is ingeschakeld, ontvangt [downloaden en installeren van de meest recente voorlopige versie taken-cmdlets Hallo](https://github.com/jaredmoo/azure-powershell/releases). Dit voorbeeld is beperkt, dus neem contact op met SaaSFeedback@microsoft.com voor vragen over of ondersteuning.*

## <a name="get-hello-wingtip-application-scripts"></a>Hallo Wingtip toepassingsscripts ophalen

Hallo Wingtip SaaS-scripts en broncode van toepassing zijn beschikbaar in Hallo [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github-opslagplaats. [Stappen toodownload Hallo Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-a-job-account-database-and-new-job-account"></a>Een taakaccountdatabase en een nieuw taakaccount maken

Deze zelfstudie moet dat u PowerShell toocreate Hallo taak database en de taak rekening gebruiken. Elastische taken maakt gebruik van een Azure SQL database zoals MSDB en SQL Agent toostore taakdefinities, taakstatus en de geschiedenis. Als Hallo taak account is gemaakt, kunt u maken en taken onmiddellijk controleren.

1. Open... \\Learning-Modules\\Schemabeheer\\*Demo SchemaManagement.ps1* in Hallo **PowerShell ISE**.
1. Druk op **F5** toorun Hallo script.

Hallo *Demo SchemaManagement.ps1* script aanroepen Hallo *implementeren SchemaManagement.ps1* toocreate script een *S2* database met de naam **jobaccount** op Hallo-catalogusserver. Vervolgens maakt u Hallo taak account, Hallo jobaccount database wordt doorgegeven als een aanroep van parameter toohello taak account maken.

## <a name="create-a-job-toodeploy-new-reference-data-tooall-tenants"></a>Maken van een taak toodeploy nieuwe verwijzing gegevens tooall tenants

Elke tenant-database bevat een set van wetten typen die Hallo soort gebeurtenissen die worden gehost op een wilt definiëren. In deze oefening maakt u een type update tooall hello tenant databases tooadd twee extra u wilt implementeren: *motor race* en *zwemmen vereniging*. Dergelijke wetten overeenkomen toohello achtergrondafbeelding die u in Hallo tenant gebeurtenissen app ziet.

Klik op de vervolgkeuzelijst hello wilt Type en valideren dat alleen 10 wilt type opties beschikbaar zijn en specifiek die 'Motor race' en 'Zwemmen vereniging' niet in de lijst Hallo opgenomen worden.

Nu gaan we maken een taak tooupdate hello *VenueTypes* tabel in alle Hallo tenant databases en Hallo typen u wilt toevoegen.

een nieuwe taak toocreate, gebruiken we een set taken systeem opgeslagen procedures in Hallo jobaccount database gemaakt als Hallo taak account is gemaakt.

1. Open van SSMS en maak verbinding toohello catalogusserver: catalogus -\<gebruiker\>. database.windows.net server
1. Ook toohello tenant server verbinding te maken: tenants1 -\<gebruiker\>. database.windows.net
1. Blader toohello *contosoconcerthall* database op Hallo *tenants1* server en de query Hallo *VenueTypes* tabel tooconfirm die *motor race*  en *zwemmen vereniging* **niet** in de lijst met resultaten Hallo.
1. Open Hallo bestand... \\Learning-Modules\\Schemabeheer\\DeployReferenceData.sql
1. Hallo-instructie wijzigen: Stel @wtpUser = &lt;gebruiker&gt; en vervang Hallo gebruiker waarde gebruikt als u Hallo Wingtip app geïmplementeerd
1. Zorg ervoor dat u bent verbonden toohello jobaccount database en druk op **F5** Hallo-script uit te voeren

* **SP\_toevoegen\_doel\_groep** Hallo doelgroepnaam DemoServerGroup, maakt nu we tooadd doelleden moeten.
* **SP\_toevoegen\_doel\_groep\_lid** voegt een *server* lidtype die acht alle databases binnen die server (Opmerking Dit Hallo tenants1-isgericht&lt; Gebruiker&gt; -server op Hallo tenant databases met) op het moment van taak uitvoering moet worden opgenomen in Hallo-taak Hallo tweede is het toevoegen van een *database* lidtype als doel, speciaal Hallo 'gouden' database ( basetenantdb) die zich in de catalogus -&lt;gebruiker&gt; server, en ten slotte een andere *database* groep lid type tooinclude hello adhocanalytics doeldatabase die wordt gebruikt in een latere zelfstudie.
* Met **sp\_add\_job** maakt u een taak die ook wel 'Implementatie van referentiegegevens' heet
* **SP\_toevoegen\_taakstap** Hallo taakstap met T-SQL-opdracht tekst tooupdate Hallo verwijzingstabel, VenueTypes maakt
* Hallo resterende weergaven in Hallo script weergegeven Hallo bestaan Hallo-objecten en uitvoeren van de monitor-taak. Gebruik deze query's tooreview Hallo-statuswaarde in Hallo **lifecycle** kolom toodetermine wanneer het Hallo-taak is voltooid op alle databases van de tenant en Hallo twee extra databases met de verwijzingstabel Hallo.

1. Blader in SSMS, toohello *contosoconcerthall* database op Hallo *tenants1* server en de query Hallo *VenueTypes* tabel tooconfirm die *motor Race* en *zwemmen vereniging* **zijn** nu in de lijst met resultaten Hallo.


## <a name="create-a-job-toomanage-hello-reference-table-index"></a>Een taak toomanage Hallo verwijzing tabelindex maken

Vergelijkbare toohello vorige oefening deze oefening maakt u een taak toorebuild Hallo index op de primaire sleutel voor de tabel Hallo-verwijzing, een typische management databasebewerking een beheerder kan uitvoeren na het laden van een grote hoeveelheden gegevens in een tabel.

Maken van een taak Hallo met dezelfde taken 'systeem' opgeslagen procedures.

1. Open SSMS en verbind toohello catalogus -&lt;gebruiker&gt;. database.windows.net server
1. Open Hallo bestand... \\Learning-Modules\\Schemabeheer\\OnlineReindex.sql
1. Klik met de rechtermuisknop, selecteer verbinding en verbinding maken met toohello catalogus -&lt;gebruiker&gt;. database.windows.net server, indien nog niet verbonden
1. Zorg ervoor dat u bent verbonden toohello jobaccount database en druk op F5 toorun Hallo script

* Met sp\_add\_job maakt u een nieuwe taak met de naam Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885
* SP\_toevoegen\_taakstap Hallo taakstap met T-SQL-opdracht tooupdate Hallo tekstindex maakt




## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u het volgende geleerd:

> [!div class="checklist"]

> * Een taak account tooquery tussen meerdere tenants maken
> * Gegevens in alle tenantdatabases bijwerken
> * Een index in een tabel maken in alle tenantdatabases

[Zelfstudie over ad-hocanalyses](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a>Aanvullende bronnen

* [Aanvullende zelfstudies waarin voort op Hallo Wingtip SaaS-toepassingsimplementatie bouwen](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Uitgeschaalde clouddatabases beheren](sql-database-elastic-jobs-overview.md)
* [Uitgeschaalde clouddatabases maken en beheren](sql-database-elastic-jobs-create-and-manage.md)
