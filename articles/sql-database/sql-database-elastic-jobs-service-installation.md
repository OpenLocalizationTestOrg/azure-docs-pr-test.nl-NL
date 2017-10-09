---
title: aaaInstalling elastische database taken | Microsoft Docs
description: Installatie van Hallo elastische taak functie doorlopen.
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a>Overzicht van de taken installeren elastische Database
[**Elastische Database taken** ](sql-database-elastic-jobs-overview.md) kan worden geïnstalleerd via PowerShell of via hello Azure Classic Portal.You krijgen toegang tot toocreate en beheren van taken met behulp van PowerShell API Hallo alleen als u Hallo PowerShell pakket installeert. Daarnaast Hallo PowerShell APIs bieden aanzienlijk meer functionaliteit dan Hallo-portal op dit moment.

Als u al hebt geïnstalleerd **elastische Database taken** via Hallo Portal van een bestaand **elastische pool**, Hallo nieuwste Powershell voorbeeldweergave scripts tooupgrade uw bestaande installatie. U wordt ten zeerste aanbevolen tooupgrade uw installatie-toohello recente **elastische Database taken** onderdelen in volgorde tootake profiteren van nieuwe functionaliteit die PowerShell APIs Hallo.

## <a name="prerequisites"></a>Vereisten
* Een Azure-abonnement. Zie voor een gratis proefversie [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell. Installeer de meest recente versie Hallo Hallo met [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376). Zie voor gedetailleerde informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).
* [NuGet-opdrachtregelprogramma](https://nuget.org/nuget.exe) gebruikte tooinstall Hallo elastische Database taken pakket is. Zie http://docs.nuget.org/docs/start-here/installing-nuget voor meer informatie.

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a>Download en Hallo elastische Database taken PowerShell pakket importeren
1. Start Microsoft Azure PowerShell-opdrachtvenster en navigeer toohello directory waar u NuGet-opdrachtregelprogramma (nuget.exe) gedownload.
2. Downloaden en importeren **elastische Database taken** pakket in de huidige map Hallo Hello volgende opdracht:
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    Hallo **elastische Database taken** bestanden worden geplaatst in de lokale directory Hallo in een map met de naam **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** waar *x.x.xxxx.x* Hallo-versienummer weerspiegelt. Hallo PowerShell-cmdlets (met inbegrip van de vereiste client-dll's) bevinden zich in Hallo **tools\ElasticDatabaseJobs** submappen en Hallo tooinstall van PowerShell-scripts, bijwerkt en verwijdert het ook zich bevinden in Hallo  **hulpprogramma's voor** onderliggende map.
3. Navigeer toohello extra submap onder de map Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x Hallo door hulpprogramma's voor een cd, bijvoorbeeld in te voeren:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. Hallo.\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello ElasticDatabaseJobs directory in $home\Documents\WindowsPowerShell\Modules uitvoeren. Dit wordt ook automatisch Hallo-module voor gebruik, bijvoorbeeld geïmporteerd:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a>Hallo elastische taken databaseonderdelen installeren met behulp van PowerShell
1. Start een Microsoft Azure PowerShell-opdrachtvenster en navigeer toohello \tools submap onder de map Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x Hallo: Typ cd \tools
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. Hallo.\InstallElasticDatabaseJobs.ps1 PowerShell-script uitvoeren en waarden voor de aangevraagde variabelen opgeven. Dit script maakt Hallo-onderdelen die worden beschreven [elastische Database taken onderdelen en prijzen](sql-database-elastic-jobs-overview.md#components-and-pricing) samen met het configureren van hello Azure Cloud Service tooappropriately Hallo afhankelijke onderdelen gebruiken.

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

Wanneer u deze opdracht een venster uitvoert weergegeven waarin een **gebruikersnaam** en **wachtwoord**. Dit is niet uw Azure-referenties, Hallo-gebruikersnaam en wachtwoord op dat Hallo beheerdersreferenties u toocreate voor de nieuwe server hello wilt opgeven.

Hallo parameters die worden geleverd op voor dit voorbeeld aanroepen kunnen worden gewijzigd voor de gewenste instellingen. de volgende Hallo bevat meer informatie over Hallo gedrag van elke parameter:

<table style="width:100%">
  <tr>
    <th>Parameter</th>
    <th>Beschrijving</th>
  </tr>

<tr>
    <td>resourceGroupName</td>
    <td>Biedt hello Azure naam van een resourcegroep gemaakt toocontain hello Azure onderdelen van een nieuw gemaakt. Deze parameter standaardwaarden te '__ElasticDatabaseJob'. Het is niet aanbevolen toochange deze waarde.</td>
    </tr>

</tr>

    <tr>
    <td>ResourceGroupLocation</td>
    <td>Biedt hello Azure-locatie toobe gebruikt voor hello Azure onderdelen van een nieuw gemaakt. Deze parameter standaard toohello locatie VS-midden.</td>
</tr>

<tr>
    <td>ServiceWorkerCount</td>
    <td>Geeft het aantal service werknemers tooinstall Hallo. Deze parameter standaard too1. Een hoger aantal werknemers mag gebruikte tooscale uit Hallo-service en tooprovide hoge beschikbaarheid. Het verdient aanbeveling toouse '2' voor implementaties die hoge beschikbaarheid van Hallo service vereist.</td>
    </tr>

</tr>
    <tr>
    <td>ServiceVmSize</td>
    <td>Hallo VM-grootte biedt voor gebruik binnen Hallo Cloudservice. Deze parameter standaard tooA0. Parameterwaarden van A0/A1/A2/A3 worden geaccepteerd waardoor Hallo worker rol toouse de grootte van een extra klein/klein/gemiddeld/groot, respectievelijk. Voor meer informatie over grootten voor worker-rol, Zie [elastische Database taken onderdelen en prijzen](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerDatabaseSlo</td>
    <td>Hallo serviceniveaudoelstelling voorziet in een Standard-editie. Deze parameter standaard tooS0. Parameterwaarden van S0/S1/S2/S3 waardoor hello Azure SQL Database worden geaccepteerd toouse Hallo respectieve SLO. Zie voor meer informatie over SQL Database Slo's [elastische Database taken onderdelen en prijzen](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorUserName</td>
    <td>Hallo beheerder gebruikersnaam op voor Hallo nieuw gemaakte Azure SQL Database-server biedt. Wanneer niet wordt opgegeven, wordt een PowerShell-venster referenties tooprompt Hallo referenties geopend.</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorPassword</td>
    <td>Biedt Hallo beheerderswachtwoord voor hello Azure SQL Database-server een nieuw gemaakt. Wanneer niet wordt opgegeven, wordt een PowerShell-venster referenties tooprompt Hallo referenties geopend.</td>
</tr>
</table>

Voor systemen die zijn gericht op een groot aantal taken die worden uitgevoerd op basis van een groot aantal databases parallel met, het is raadzaam toospecify parameters, zoals: - ServiceWorkerCount 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a>Bijwerken van een bestaande onderdelen installatie voor elastische Database taken met behulp van PowerShell
**Elastische Database taken** binnen een bestaande installatie van de schaal en hoge beschikbaarheid kunnen worden bijgewerkt. Dit proces kunt u toekomstige upgrades van servicecode zonder toodrop en maak Hallo beheer database. Dit proces kan ook worden gebruikt binnen Hallo dezelfde versie toomodify Hallo service VM-grootte of Hallo worker aantal servers.

tooupdate hello VM-grootte van een installatie, Voer Hallo script met parameters na bijgewerkt toohello waarden van uw keuze.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th>Parameter</th>
  <th>Beschrijving</th>
</tr>

  <tr>
    <td>resourceGroupName</td>
    <td>Identificeert hello Azure Resourcegroepnaam gebruikt wanneer Hallo elastische Database taak onderdelen in eerste instantie zijn geïnstalleerd. Deze parameter standaardwaarden te '__ElasticDatabaseJob'. Omdat het geen aanbevolen toochange deze waarde u mag geen toospecify deze parameter.</td>
    </tr>
</tr>

</tr>

  <tr>
    <td>ServiceWorkerCount</td>
    <td>Geeft het aantal service werknemers tooinstall Hallo.  Deze parameter standaard too1.  Een hoger aantal werknemers mag gebruikte tooscale uit Hallo-service en tooprovide hoge beschikbaarheid.  Het verdient aanbeveling toouse '2' voor implementaties die hoge beschikbaarheid van Hallo service vereist.</td>
</tr>

</tr>

    <tr>
    <td>ServiceVmSize</td>
    <td>Hallo VM-grootte biedt voor gebruik binnen Hallo Cloudservice. Deze parameter standaard tooA0. Parameterwaarden van A0/A1/A2/A3 worden geaccepteerd waardoor Hallo worker rol toouse de grootte van een extra klein/klein/gemiddeld/groot, respectievelijk. Voor meer informatie over grootten voor worker-rol, Zie [elastische Database taken onderdelen en prijzen](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a>Hallo elastische Database taken onderdelen met Hallo Portal installeren
Zodra u hebt [een elastische pool gemaakt](sql-database-elastic-pool-manage-portal.md), kunt u installeren **elastische Database taken** onderdelen tooenable uitvoeren van beheertaken voor elke database in Hallo elastische pool. In tegenstelling tot wanneer met behulp van Hallo **elastische Database taken** PowerShell APIs's Hallo interface van de portal is momenteel beperkt tooonly uitvoering op een bestaande toepassingen.

**Geschatte tijd toocomplete:** 10 minuten.

1. Van de dashboardweergave Hallo van de elastische groep via Hallo Hallo [Azure Portal](https://portal.azure.com/#) , klikt u op **maken taak**.
2. Als u een taak voor Hallo eerst maakt, moet u **elastische Database taken** door te klikken op **PREVIEW-voorwaarden**.
3. Accepteren Hallo voorwaarden door te klikken op Hallo selectievakje.
4. Klik in de weergave Hallo installeren 'services' op **taak REFERENTIES**.
   
    ![Hallo-services te installeren][1]
5. Typ een gebruikersnaam en wachtwoord voor een database-beheerder. Als onderdeel van Hallo-installatie, wordt een nieuwe Azure SQL Database-server gemaakt. In deze nieuwe server Hallo beheer database, ook wel een nieuwe database wordt gemaakt en toocontain Hallo-metagegevens gebruikt voor elastische Database-taken. Hallo-gebruikersnaam en wachtwoord hier gemaakte worden gebruikt voor het Hallo-doel van de logboekregistratie in toohello beheer database. Een afzonderlijke referentie wordt gebruikt voor het uitvoeren van script Hallo-databases in de pool Hallo.
   
    ![Maak een gebruikersnaam en wachtwoord][2]
6. Klik op OK om Hallo. Hallo-onderdelen worden gemaakt voor u het over enkele minuten in een nieuw [resourcegroep](../azure-resource-manager/resource-group-overview.md). de nieuwe resourcegroep Hallo is vastgemaakt toohello start board, zoals hieronder wordt weergegeven. Taken nadat deze is gemaakt, elastische database (Cloudservice, SQL-Database, Service Bus en opslag) worden gemaakt in de groep Hallo.
   
    ![resourcegroep in start board][3]
7. Als u toocreate probeert of een taak beheren terwijl taken voor elastische database wordt geïnstalleerd bij het opgeven van **referenties** Hallo volgende bericht wordt weergegeven.
   
    ![Implementatie nog in voortgang][4]

Als het verwijderen vereist is, verwijdert u de resourcegroep Hallo. Zie [hoe toouninstall Hallo elastische Database onderdelen taak](sql-database-elastic-jobs-uninstall.md).

## <a name="next-steps"></a>Volgende stappen
Zorg ervoor dat een referentie met de juiste rechten Hallo voor uitvoering van het script wordt gemaakt op elke database in de groep hello, Zie voor meer informatie [SQL Database beveiligen](sql-database-manage-logins.md).
Zie [maken en beheren van de taken voor een elastische Database](sql-database-elastic-jobs-create-and-manage.md) tooget gestart.

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
