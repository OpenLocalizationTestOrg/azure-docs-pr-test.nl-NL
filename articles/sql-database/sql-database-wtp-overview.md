---
title: aaaIntro Wingtip SaaS - multitenant-app van Azure SQL Database | Microsoft Docs
description: Meer informatie over met behulp van een multitenant voorbeeldtoepassing die gebruikmaakt van Azure SQL Database, Hallo Wingtip SaaS-app
keywords: zelfstudie sql-database
services: sql-database
author: stevestein
manager: jhubbard
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: sstein
ms.openlocfilehash: daeed293116fca22718831b780533be6ef2ad178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-wingtip-saas-application"></a>Inleiding toohello Wingtip SaaS-toepassing

Hallo *Wingtip SaaS* toepassing is een voorbeeld multitenant-app die u laat Hallo unieke voordelen van het SQL-Database zien. Hallo app gebruikmaakt van een database-per-tenant, patroon van de SaaS-toepassing, tooservice meerdere tenants. Hallo-app is ontworpen tooshowcase functies van Azure SQL Database waarmee SaaS-scenario's, met inbegrip van verschillende SaaS-ontwerp- en patronen. tooquickly laten en wordt uitgevoerd, Hallo Wingtip SaaS-app implementeert in minder dan vijf minuten!

Bron en het beheer toepassingsscripts zijn beschikbaar in Hallo [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github-opslagplaats. toorun hello scripts, [Hallo-Learning-Modules downloadmap](#download-and-unblock-the-wingtip-saas-scripts) tooyour lokale computer.

## <a name="sql-database-wingtip-saas-tutorials"></a>SQL Database Wingtip SaaS-zelfstudies

Na implementatie van de app hello, verkennen Hallo zelfstudies waarin voort op de eerste implementatie hello bouwen te volgen. Deze zelfstudies verkennen algemene SaaS-patronen die van de ingebouwde functies van SQL-Database, SQL Data Warehouse en andere Azure-services gebruikmaken. Zelfstudies bevatten PowerShell-scripts, met gedetailleerde uitleg die aanzienlijk te, wat vereenvoudigen, en implementeren van Hallo dezelfde SaaS-beheer patronen in uw toepassingen.


| Zelfstudie | Beschrijving |
|:--|:--|
|[Implementeren en verkennen Hallo Wingtip SaaS-toepassing](sql-database-saas-tutorial.md)| **BEGIN HIER!** Implementeer en verkennen Hallo Wingtip SaaS-toepassing tooyour Azure-abonnement. |
|[Inrichten en catalogus tenants](sql-database-saas-tutorial-provision-and-catalog.md)| Informatie over hoe toepassing hello verbinding maakt met behulp van een catalogusdatabase tootenants en hoe Hallo catalogus toegewezen tootheir gegevens tenants. |
|[Bewaken en beheren van prestaties](sql-database-saas-tutorial-performance-monitoring.md)| Meer informatie over hoe toouse bewaking functies van SQL Database, en hoe tooset waarschuwt wanneer drempelwaarden worden overschreden. |
|[Monitor met logboekanalyse (OMS)](sql-database-saas-tutorial-log-analytics.md) | Meer informatie over het gebruik van [logboekanalyse](../log-analytics/log-analytics-overview.md) toomonitor grote hoeveelheden resources, tussen meerdere groepen. |
|[Herstellen van een enkele tenant](sql-database-saas-tutorial-restore-single-tenant.md)| Meer informatie over hoe toorestore tooa van de tenant-database vorig tijdstip voor herstel. Stappen toorestore tooa parallelle database verlaten Hallo bestaande tenant database online is, zijn ook opgenomen. |
|[Schema van de tenant beheren](sql-database-saas-tutorial-schema-management.md)| Meer informatie over hoe tooupdate schema en update verwijzen naar gegevens over alle Wingtip SaaS-tenants. |
|[Ad-hoc-analyses uitvoeren](sql-database-saas-tutorial-adhoc-analytics.md) | Maakt de database van een ad-hoc analytics en realtime gedistribueerde query's uitvoeren op alle tenants.  |
|[Tenant-analyses uitvoeren](sql-database-saas-tutorial-tenant-analytics.md) | Tenant-gegevens ophalen naar een analytics database of de data warehouse voor het uitvoeren van offline analytische query's. |



## <a name="application-architecture"></a>Toepassingsarchitectuur

Hallo Wingtip SaaS app Hallo database per tenant model gebruikt, en maakt gebruik van SQL elastische pools toomaximize efficiëntie. Voor het inrichten en tenants tootheir gegevens wilt toewijzen, wordt een catalogusdatabase gebruikt. Hallo core Wingtip SaaS-toepassing, maakt gebruik van een pool met drie voorbeeld tenants, plus Hallo catalogusdatabase. Veel van Hallo Wingtip SaaS zelfstudies ertoe leiden dat invoegtoepassingen toohello eerste implementatie is voltooid, door de introductie van analytische databases tussen meerdere databases Schemabeheer, enzovoort.


![Wingtip SaaS-architectuur](media/sql-database-wtp-overview/app-architecture.png)


Tijdens het doorlopen van Hallo zelfstudies en werken met Hallo app, is het belangrijk toofocus op Hallo SaaS patronen zoals ze betrekking toohello gegevenslaag hebben. Met andere woorden, ligt de nadruk op Hallo gegevenslaag en niet meer dan Hallo app zelf analyseren. Hallo-implementatie van deze patronen SaaS begrijpen sleutel tooimplementing deze patronen in uw toepassingen is bij het beoordelen van de benodigde wijzigingen voor uw specifieke bedrijfsvereisten.

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Download en blokkering Hallo Wingtip SaaS-scripts

Uitvoerbare inhoud (scripts, dll-bestanden) mogelijk geblokkeerd door Windows als zip-bestanden van een externe bron wordt gedownload en uitgepakt. Bij het Hallo-scripts uit een zip-bestand uitpakken ***stappen Hallo hieronder toounblock Hallo ZIP-bestand voor het uitpakken van***. Dit zorgt ervoor Hallo scripts toorun zijn toegestaan.

1. Te bladeren[github-repo-Hallo Wingtip SaaS](https://github.com/Microsoft/WingtipSaaS).
1. Klik op **klonen of downloaden**.
1. Klik op **ZIP downloaden** en Hallo-bestand op te slaan.
1. Klik met de rechtermuisknop Hallo **WingtipSaaS master.zip** bestand en selecteer **eigenschappen**.
1. Op Hallo **algemene** tabblad **blokkering**.
1. Klik op **OK**.
1. Hallo-bestanden extraheren.

Scripts bevinden zich in Hallo *... \\WingtipSaaS master\\Learning-Modules* map.


## <a name="working-with-hello-wingtip-saas-powershell-scripts"></a>Werken met Hallo Wingtip SaaS PowerShell-Scripts

tooget hello meest moet u buiten het Hallo-voorbeeld toodive in scripts Hallo opgegeven. Gebruik onderbrekingspunten en doorloop Hallo scripts, onderzoeken Hallo details van hoe verschillende SaaS-patronen Hallo worden geïmplementeerd. tooeasily doorlopen Hallo opgegeven scripts en modules voor het beste begrijpt, wordt aangeraden Hallo Hallo [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).

### <a name="update-hello-configuration-file-for-your-deployment"></a>Hallo-configuratiebestand voor uw implementatie bijwerken

Hallo bewerken **UserConfig.psm1** bestand met Hallo resource groeps- en -waarde die u hebt ingesteld tijdens de implementatie:

1. Open Hallo *PowerShell ISE* en laden... \\Learning-Modules\\*UserConfig.psm1* 
1. Update *ResourceGroupName* en *naam* met specifieke waarden Hallo voor uw implementatie (op regels 10 en 11 alleen).
1. Hallo wijzigingen opslaan!

Instellen van deze waarden hier simpelweg blijft u opheft tooupdate deze implementatie-specifieke waarden in elk script.

### <a name="execute-scripts-by-pressing-f5"></a>Voer scripts uit door op F5 te drukken

Gebruik van meerdere scripts *$PSScriptRoot* toonavigate mappen, en *$PSScriptRoot* worden alleen geëvalueerd als scripts worden uitgevoerd door te drukken **F5**.  Syntaxismarkering en een selectie actief (**F8**) kunnen leiden tot fouten, indrukt **F5** wanneer het uitvoeren van scripts.

### <a name="step-through-hello-scripts-tooexamine-hello-implementation"></a>Doorloop Hallo scripts tooexamine Hallo-implementatie

Hallo aanbevolen manier toounderstand Hallo scripts wordt door ze doorlopen toosee wat ze doen. Bekijk Hallo opgenomen **Demo -** scripts die een werkstroom op hoog niveau van eenvoudige toofollow aanwezig. Hallo **Demo -** scripts tonen Hallo stappen vereist tooaccomplish elke taak dus onderbrekingspunten instellen en inzoomen dieper in afzonderlijke Hallo voorziet in toosee implementatiegegevens Hallo verschillende SaaS-patronen.

Tips voor het verkennen en PowerShell-scripts doorlopen:

* Open **Demo -** scripts in Hallo PowerShell ISE.
* Of Ga door met uitvoeren **F5** (met behulp van **F8** wordt niet aanbevolen omdat *$PSScriptRoot* wordt niet geëvalueerd wanneer selecties van een script wordt uitgevoerd).
* Plaats onderbrekingspunten door op een regel te klikken of een regel te selecteren en op **F9** te drukken.
* Stap over een functie of scriptaanroep heen met **F10**.
* Stap in een functie of scriptaanroep met **F11**.
* Stap buiten het huidige Hallo-functie of het script met behulp van aanroep **Shift + F11**.


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a>Bekijk het databaseschema en voer SQL-query’s uit met SSMS

Gebruik [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tooconnect en blader Hallo-toepassingsservers en databases.

Hallo-implementatie in eerste instantie heeft twee SQL-Database servers tooconnect te-Hallo *tenants1 -&lt;gebruiker&gt;*  -server en Hallo *catalogus -&lt;gebruiker&gt;* server. tooensure een geslaagde demo-verbinding, beide servers hebben een [firewallregel](sql-database-firewall-configure.md) toestaan via alle IP-adressen.


1. Open *SSMS* en maak verbinding toohello *tenants1 -&lt;gebruiker&gt;. database.windows.net* server.
1. Klik op **Verbinding maken**  > **Database-engine...**:

   ![catalogusserver](media/sql-database-wtp-overview/connect.png)

1. Referenties voor Demo zijn: Gebruikersnaam = *developer*, Wachtwoord = *P@ssword1*

   ![verbinding](media\sql-database-wtp-overview\tenants1-connect.png)

1. Herhaal stappen 2-3 en verbinding maken met toohello *catalogus -&lt;gebruiker&gt;. database.windows.net* server.

Als de verbinding is geslaagd, ziet u beide servers. Uw lijst met databases mogelijk verschillen, afhankelijk van het Hallo-tenants die u hebt ingericht:

![objectverkenner](media/sql-database-wtp-overview/object-explorer.png)



## <a name="next-steps"></a>Volgende stappen

[Hallo Wingtip SaaS-toepassing implementeren](sql-database-saas-tutorial.md)
